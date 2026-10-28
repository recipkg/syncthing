# 同机双进程同步观察

## 环境与边界

源代码固定为 [syncthing/syncthing](https://github.com/syncthing/syncthing/tree/ed38528d7fba3dd6a42c9c9fc6780af432dc15d2) 提交 `ed38528d7fba3dd6a42c9c9fc6780af432dc15d2`。本机 Linux、Go 1.27.3 使用 `go build -tags noassets -o <临时路径> ./cmd/syncthing` 构建；版本输出为 `unknown-dev`，该构建不含完整 GUI。直接 `go build` 因缺少生成的 GUI 资源失败，不应把本测试当成标准发布构建或 GUI 验收。

为每个进程独立生成配置、密钥、设备 ID 和空文件夹；文件夹 ID 相同，双方分别配置对方的固定本机 TCP 地址。关闭全局/本地发现、转发、NAT、崩溃报告、自动升级和使用情况报告；禁用文件监视器，用扫描 API 触发扫描。配置目录、数据、监听地址和文件都只属于测试；不使用现有设备、账号或目录。

## 已观察行为

1. 两个进程建立连接并进入空闲；A 写入 `sample.txt` 内容 `initial\n` 并扫描，B 读到相同字节。
2. B 写入 `new.txt` 内容 `from B\n` 并扫描，A 读到相同字节；A 删除该文件并扫描后，B 的同名文件消失。
3. 停止两端后，A、B 分别将 `sample.txt` 写成 `offline A\n`、`offline B\n`；分别单独启动并扫描本地修改，再停止，之后同时启动并重新连接。
4. 两端最终包含相同的两个 `sample` 开头文件，文件内容集合为 `offline A\n`、`offline B\n`，其中一个文件名含 `.sync-conflict-`。胜出内容及冲突副本名由具体状态决定，验收不固定哪端获胜或时间戳。

以上黑盒样本在该构建环境运行两次，且均通过。它们只验证临时环境下观察到的路径，不能证明任意失败、删除、权限、断电、网络分区或真实设备上的数据安全，也不能将同步作为备份。测试在 [standard-library-verification](https://github.com/recipkg/standard-library-verification) 的 `tests/test_syncthing.py` 中，可指定待验收二进制重复运行；上游通过不是重建通过。
