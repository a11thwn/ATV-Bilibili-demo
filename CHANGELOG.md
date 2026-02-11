# Changelog

## Build 5 — 2026-02-11

### 合并上游更新

从 `yichengchen/ATV-Bilibili-demo` 同步了 14 个提交（使用 rebase 方式，个性化改动保留在最上层）：

- feat: 播放器添加下一集按钮 (#179)
- feat: 限制图片缓存大小为500MB (#176)
- feat: 历史记录显示观看时间和进度 (#174)
- feat: 个人中心增加追番追剧页面 (#170)
- feat: 搜索页增加直播搜索和搜索历史 (#169)
- feat: up主页增加顶部工具栏 (#168)
- fix: 修复视频播放无限加载问题 (#186)
- fix: 加载尺寸过大的头像时崩溃 (#184)
- fix: 修正webid缓存条件判断错误 (#178)
- fix: 修正番剧继续播放和进度上报 (#177)
- fix: 再次修正直播列表-352错误 (#175)
- fix: 非全屏下还是会显示底部弹幕 (#173)
- fix: 修正直播列表-352错误 (#172)
- fix: fix ci build (#167)

### Build 号更新

- `CURRENT_PROJECT_VERSION`（pbxproj）：4 → 5
- `CFBundleVersion`（Info.plist）：4 → 5

> **备忘：打包 TestFlight 需要同时改两个地方的 build 号！**
> 1. `BilibiliLive.xcodeproj/project.pbxproj` → `CURRENT_PROJECT_VERSION`（Debug + Release 两处）
> 2. `BilibiliLive/Supporting Files/Info.plist` → `CFBundleVersion`

### 同步上游操作备忘

```bash
# 1. 添加 upstream（只需一次）
git remote add upstream https://github.com/yichengchen/ATV-Bilibili-demo.git

# 2. 拉取上游
git fetch upstream

# 3. 查看差异
git log --oneline main..upstream/main      # upstream 新增的
git log --oneline upstream/main..main      # 本地独有的

# 4. rebase 合并（个性化提交保持在上层）
git rebase upstream/main

# 5. 推送（rebase 重写了历史，需要 force push）
git push --force-with-lease
```

---

## Build 4 — 2025-11-27

- feat: 添加 App Store 图标和应用图标
- feat: 更新启动界面图片
- feat: 更新 Top Shelf 背景为毛绒玩具合照
- fix: 修复 Top Shelf 背景图片比例问题
- fix: 添加 App Icon 的 2x 分辨率图片
- fix: 添加 Top Shelf Image 的 1x 和 2x 版本
- chore: 更新仓库链接和截图
- chore: 添加出口合规声明
