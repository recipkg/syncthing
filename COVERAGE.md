# 来源、证据与缺口

- 上游：[syncthing/syncthing](https://github.com/syncthing/syncthing)，源码提交 `ed38528d7fba3dd6a42c9c9fc6780af432dc15d2`；README 标示 MPL-2.0。
- 阅读 README、源码文件清单与官方 [同步工作原理](https://docs.syncthing.net/users/syncing.html)、[BEP v1](https://docs.syncthing.net/specs/bep-v1.html) 部分内容。线上文档可能随时间变化，尚需与固定源码版本核对。
- 从固定提交用 Go 1.27.3 构建上游；直接 `go build` 缺少生成的 GUI 资源，故使用 `go build -tags noassets`，输出版本标识为 `unknown-dev`。本机构建未包含完整网页界面。两次在隔离临时配置、目录和本机 TCP 连接上运行双进程样本：双向新增、删除及双方离线修改冲突后保留两份内容；测试结束后关闭测试进程。细节见 `SYNC-OBSERVED.md`。
- 尚未跨真实设备运行或生成任何替代实现。BEP 完整消息、互操作性、鉴权、冲突裁决、版本历史、文件元数据/权限、平台差异、网络故障与恢复都未完整提取或验收。单个冲突样本不能证明整体数据安全。
- `quality` 和 `design` 是固定版本的设计与质量配方，不是同步运行时依赖。不能把它们视作安全或数据保护证明。
