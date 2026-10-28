# 来源、证据与缺口

- 上游：[syncthing/syncthing](https://github.com/syncthing/syncthing)，源码提交 `ed38528d7fba3dd6a42c9c9fc6780af432dc15d2`；README 标示 MPL-2.0。
- 阅读 README、源码文件清单与官方 [同步工作原理](https://docs.syncthing.net/users/syncing.html)、[BEP v1](https://docs.syncthing.net/specs/bep-v1.html) 部分内容。线上文档可能随时间变化，尚需与固定源码版本核对。
- 尚未实际运行上游、对照两个客户端或生成任何替代实现。BEP 完整消息、互操作性、鉴权、冲突选择、删除、版本历史、文件元数据/权限、平台差异、网络与恢复都未完整提取或验收。
- `quality` 和 `design` 是固定版本的设计与质量配方，不是同步运行时依赖。不能把它们视作安全或数据保护证明。
