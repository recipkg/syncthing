# Syncthing 配方（提取中）

```toml
format = "recipkg/1"

[package]
name = "syncthing"
version = "0.1.1"
kind = "software"
description = "Syncthing 多设备文件同步软件的重建配方；当前仍在提取。"
entry = "BUILD_PROMPT.md"

[dependencies.quality]
git = "https://github.com/recipkg/recipkg.git"
rev = "41e5b55c6612a9a5a10e499b5ace6a1a3fed0f2b"
subdir = "recipes/software-quality"

[dependencies.design]
git = "https://github.com/recipkg/design-directions.git"
rev = "f86b3eca87356a073274248eb48b6a5b6756db59"
```

来源：[syncthing/syncthing](https://github.com/syncthing/syncthing)，观察提交 `ed38528d7fba3dd6a42c9c9fc6780af432dc15d2`；上游 README 标明 MPL-2.0。当前是未完成草案，不证明可安全重建或同步真实数据；见 `COVERAGE.md`。
