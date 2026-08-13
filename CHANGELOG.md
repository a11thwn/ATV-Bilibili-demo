# Changelog

## [2026-08-13] - Build 7 同步上游并发布 TestFlight

### 问题描述

- 本地 fork 尚未包含原项目 `yichengchen/ATV-Bilibili-demo` 的近期更新
- 本地保留了签名、Bundle ID、应用名称、图标、启动图和 Top Shelf 等个性化内容，不能被上游版本覆盖
- TestFlight 需要使用未重复的构建号，本次发布构建号为 7

### 分析原因

- `origin/main` 与 `upstream/main` 已产生分叉：本地保留 12 个个性化提交，上游新增 39 个提交
- 直接覆盖或 rebase 容易改写本地历史；未提交修改存在时直接 pull 也会被 Git 拒绝
- 仓库中已提交的构建号仍为 5，需要同时更新 Xcode 工程和 `Info.plist`

### 解决方案

- 使用三方合并将 `upstream/main` 合入本地 `main`，不重写本地 12 个个性化提交
- 保留 Team `ZU6TTDY78P`、Bundle ID `com.zhi.tv.BilibiliLive`、应用名称及定制资源
- 将 Debug、Release 和 `Info.plist` 中的构建号统一更新为 7
- 完成 Release 归档、签名校验，并上传至 App Store Connect

### 改动内容

- 同步上游 39 个提交，主要包括：
  - 新增 TV 推荐独立页面、关注页沉浸式播放、Featured 内容安全过滤和播放器发现面板
  - 新增播放器内画质选择、直播线路选择、视频选集范围跳转和 1.75 倍速
  - 新增导航栏自定义排序、热搜入口及 UP 主空间按播放量排序
  - 改善海外网络高码率播放、PCDN 回退、播放预加载与取消竞态
  - 修复关注页崩溃、退出播放后音频残留、连续播放清理、投屏及番剧花絮播放问题
  - 升级 Swift Package 依赖并调整播放器、Feed 和 TabBar 结构
- 更新 `BilibiliLive.xcodeproj/project.pbxproj`：两处 `CURRENT_PROJECT_VERSION` 从 5 更新为 7
- 更新 `BilibiliLive/Supporting Files/Info.plist`：`CFBundleVersion` 从 5 更新为 7

### 影响范围

- 涉及 tvOS 推荐、关注、搜索、个人中心、播放器、直播、投屏和导航栏
- 最低系统版本仍为 tvOS 16.0，应用版本仍为 1.0
- 本机签名、Bundle ID、应用名称、图标、启动图和 Top Shelf 定制保持不变

### 验证结果

- Xcode 26.3 Release Archive 成功，产物为 arm64 tvOS App Archive
- 归档信息确认版本 `1.0 (7)`、Bundle ID `com.zhi.tv.BilibiliLive`、Team `ZU6TTDY78P`
- `codesign --verify --deep --strict` 校验通过
- 2026-08-13 15:12（GMT+8）已成功上传至 Apple，等待 App Store Connect 完成处理

### 后续计划

- 在 App Store Connect 中确认构建 7 处理完成并进入 TestFlight 可测试状态

---

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
