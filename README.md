# NovaShell

NovaShell 是一个面向新项目启动的 React Native 模板仓库，目标是提供一套可以直接继续开发的工程基线，而不是一个已经接好业务流程的成品应用。

当前仓库已经完成了以下基础能力：

- React Native + TypeScript 工程底座
- Tailwind-first 的样式方案
- 常见业务依赖预装
- API 客户端生成脚本
- Android / iOS 清理与打包脚本
- 基础目录分层和路径别名

它适合作为团队内部模板、PoC 起始工程、或者新 App 的第一版脚手架。  
它目前还不是“开箱即用就能直接上线”的模板，导航流、环境变量体系、签名配置、CI 等仍需要按真实项目补齐。

## 1. 模板定位

NovaShell 的定位不是演示 React Native 官方默认页面，而是提供一套偏工程化的起点，减少每次新项目反复做这些初始化工作的成本：

- 统一目录结构
- 统一样式写法
- 统一 API 接入方式
- 统一原生构建脚本
- 统一版本号来源

这个模板优先解决的是“怎么快速开始一个规范项目”，而不是“模板本身展示多少业务功能”。

## 2. 当前包含的能力

### 2.1 工程底座

- React Native `0.84.1`
- React `19.2.3`
- TypeScript
- Babel alias，支持 `~/` 指向 `src/*`
- ESLint / Prettier / Jest 基础配置

### 2.2 UI 层

- 使用 `twrnc` 提供 Tailwind 风格 utility class
- `tailwind.config.js` 中集中定义设计 token
- `src/ui/tailwind-extend.ts` 作为共享 `tw` 入口
- 示例组件 `AppButton`
- 示例页面 `HomeScreen`

### 2.3 业务常用依赖

- `@react-navigation/native`
- `@react-navigation/native-stack`
- `zustand`
- `axios`
- `axios-cache-interceptor`
- `react-native-webview`
- `react-native-safe-area-context`
- `react-native-gesture-handler`
- `react-native-screens`

### 2.4 API 工具链

- 通过 `swagger-typescript-api` 从 OpenAPI schema 生成客户端
- 默认输出目录为 `src/api/generated`
- 在真正生成之前，仓库保留了一个占位导出，保证项目可编译

### 2.5 原生脚本

- Android clean 脚本
- iOS clean 脚本
- Android APK 构建脚本
- Android AAB 构建脚本
- iOS IPA 构建脚本

## 3. 当前不包含的能力

这部分很重要。模板里虽然已经安装了一些常用依赖，但不代表这些能力已经全部接好。

当前仓库还没有完整提供：

- 真正的导航结构和页面路由体系
- 统一的 Zustand store 示例
- 基于真实后端的接口调用示例
- 多环境配置体系，例如 `dev / staging / prod`
- CI 工作流
- 自动化发版流程
- Android 正式签名配置
- iOS 导出配置文件与团队签名信息
- 模板一键改名脚本

换句话说，这个仓库现在是“工程骨架”，不是“业务模板成品”。

## 4. 技术栈

| 领域 | 方案 |
| --- | --- |
| App runtime | `react`, `react-native` |
| 语言 | `typescript` |
| 样式 | `twrnc`, `tailwind.config.js` |
| 导航 | `@react-navigation/native`, `@react-navigation/native-stack` |
| 状态管理 | `zustand` |
| 网络请求 | `axios` |
| 请求缓存 | `axios-cache-interceptor` |
| Web 容器 | `react-native-webview` |
| API 代码生成 | `swagger-typescript-api` |
| 代码规范 | `eslint`, `prettier` |
| 测试 | `jest`, `react-test-renderer` |

## 5. 环境要求

### 5.1 Node / Ruby

- Node.js `>= 22.11.0`
- Ruby `>= 2.6.10`

### 5.2 iOS 开发环境

- macOS
- Xcode
- CocoaPods
- Bundler

### 5.3 Android 开发环境

- Android Studio
- Android SDK
- JDK
- 至少一个模拟器或已连接真机

## 6. 首次启动

下面的步骤适用于第一次 clone 仓库之后的初始化。

### 6.1 安装 JavaScript 依赖

```sh
npm install
```

### 6.2 安装 Ruby gem

```sh
bundle install
```

### 6.3 安装 iOS Pods

```sh
cd ios
bundle exec pod install
cd ..
```

### 6.4 启动 Metro

```sh
npm start
```

### 6.5 运行 iOS

```sh
npm run ios
```

### 6.6 运行 Android

```sh
npm run android
```

## 7. 日常开发命令

### 7.1 基础命令

| 命令 | 说明 |
| --- | --- |
| `npm start` | 启动 Metro dev server |
| `npm run ios` | 编译并启动 iOS |
| `npm run android` | 编译并启动 Android |
| `npm run lint` | 运行 ESLint |
| `npm test` | 运行 Jest |

### 7.2 清理命令

| 命令 | 说明 |
| --- | --- |
| `npm run ios:clean` | 清理 iOS 构建产物 |
| `npm run android:clean` | 清理 Android 构建产物 |

这些脚本适合在以下场景使用：

- 升级原生依赖后出现奇怪构建错误
- 切换分支后缓存污染
- Debug / Release 构建状态异常

### 7.3 打包命令

| 命令 | 说明 |
| --- | --- |
| `npm run build:apk` | 构建 Android release APK |
| `npm run build:aab` | 构建 Android release AAB |
| `npm run build:ipa` | 构建 iOS IPA |

构建日志默认输出到：

- `android/build/logs`
- `ios/build/logs`

### 7.4 API 生成命令

```sh
npm run api:generate -- ./openapi.json
```

或：

```sh
npm run api:generate -- https://example.com/openapi.json
```

如果你希望指定输出目录：

```sh
npm run api:generate -- ./openapi.json src/api/generated
```

## 8. 目录结构说明

```text
.
|-- App.tsx
|-- index.js
|-- src
|   |-- api
|   |   |-- generated
|   |   |-- http.ts
|   |   `-- index.ts
|   `-- ui
|       |-- components
|       |-- screens
|       `-- tailwind-extend.ts
|-- scripts
|-- android
`-- ios
```

### 8.1 根目录

- `App.tsx`  
  当前应用入口组件，当前直接挂载 `HomeScreen`，还没有真正的导航容器。

- `index.js`  
  React Native 注册入口，并提前引入 `react-native-gesture-handler`。

- `package.json`  
  依赖、脚本、版本号来源都在这里。

### 8.2 `src/api`

- `http.ts`  
  封装了基础 HTTP client 和 cache client 的创建方法。

- `generated/`  
  OpenAPI 生成的客户端代码输出目录。

- `index.ts`  
  对外统一导出 `generated` 和 `http`。

### 8.3 `src/ui`

- `components/`  
  放可复用 UI 组件。

- `screens/`  
  放页面级组件。

- `tailwind-extend.ts`  
  创建共享的 `tw` 实例，统一读取 `tailwind.config.js`。

### 8.4 `scripts`

这里放跨平台 shell 脚本，当前包含：

- `android-clean.sh`
- `ios-clean.sh`
- `build-apk.sh`
- `build-aab.sh`
- `build-ipa.sh`
- `generate-api.js`

## 9. 当前代码现状说明

为了避免 README 看起来像“已经全部接好了”，这里把现状讲清楚。

### 9.1 App 入口

当前 `App.tsx` 只做了两件事：

- 挂载 `SafeAreaProvider`
- 渲染示例页 `HomeScreen`

也就是说：

- 还没有 `NavigationContainer`
- 还没有全局 store provider
- 还没有鉴权流、Tab、Stack、Splash 等业务壳

### 9.2 示例页面

`HomeScreen` 目前主要用于表达模板的 UI 基线：

- Tailwind-first 样式写法
- 组件组合方式
- 视觉 token 使用方式
- 模板当前已预装的技术栈

它是一个“说明性示例页”，不是业务首页。

### 9.3 API 目录

`src/api/generated/index.ts` 当前是占位文件。  
只有在你执行过 `npm run api:generate` 后，才会生成真实客户端文件。

这意味着模板当前只提供了 API 接入方式，还没有绑定任何真实后端接口。

## 10. 样式约定

NovaShell 的样式策略是 Tailwind-first，而不是 StyleSheet-first。

建议遵守以下规则：

- 静态布局、间距、圆角、边框、颜色、字号优先使用 `tw\`...\``
- 条件样式和变体使用 `tw.style(...)`
- 只有在以下情况才使用原生 style object：
  - 运行时计算值
  - Animated 插值结果
  - 某些 Tailwind 不好表达的平台 API 样式

推荐做法：

- 颜色、语义 token 放到 `tailwind.config.js`
- 通用按钮、卡片、标签、列表项抽到 `src/ui/components`
- 页面本身只负责组合，不要在 screen 文件里堆大量重复视觉样式

不推荐做法：

- 到处散落十六进制颜色
- 一边写 `tw` 一边大量回退到 `StyleSheet.create`
- 每个页面都从零拼按钮、标题栏、表单项

## 11. API 层约定

### 11.1 HTTP client

`src/api/http.ts` 暴露了两个方法：

- `createHttpClient`
- `createCachedHttpClient`

适用思路：

- 纯请求客户端用 `createHttpClient`
- 需要缓存拦截器时用 `createCachedHttpClient`

### 11.2 OpenAPI 生成

模板希望把“接口类型定义”和“请求方法封装”尽量从手写迁移到生成。

推荐流程：

1. 后端提供 OpenAPI schema
2. 使用 `npm run api:generate -- <schema>`
3. 在 `src/api/generated` 中获得生成代码
4. 在业务层再按模块做二次封装

建议不要把生成代码和业务逻辑直接混在一起。  
更合理的方式是：

- `generated` 放纯生成物
- 业务项目自己再加一层 `services` / `repositories` / `queries`

## 12. 版本号策略

版本号来源统一放在 `package.json`：

- `version`
- `android_version`
- `android_version_code`
- `ios_version`

### 12.1 Android

Android 构建时会从 `package.json` 读取：

- `android_version` 作为 `versionName`
- `android_version_code` 参与生成 `versionCode`

模板里已经做了版本换算逻辑，避免每次去 Gradle 里手改版本号。

### 12.2 iOS

iOS 工程里配置了 build phase，会从 `package.json` 中同步：

- `ios_version`
- `android_version_code`

因此原则上也不应该手动长期维护 Xcode 中的版本号。

## 13. 原生打包说明

### 13.1 Android APK

执行：

```sh
npm run build:apk
```

这是一个 release APK 打包命令。  
如果你想使用脚本原生能力而不是 npm 脚本包装，可以直接运行：

```sh
bash ./scripts/build-apk.sh
```

直接调用脚本时支持：

- `APK_BUILD_TYPE=debug`
- `APK_BUILD_TYPE=release`
- `OPEN_ARTIFACT_DIR=0`

注意：

- `npm run build:apk` 在 `package.json` 中已经固定为 release
- Android release 当前默认仍使用 debug keystore 签名
- 这适合模板验证，不适合真实上线

### 13.2 Android AAB

执行：

```sh
npm run build:aab
```

如果直接跑脚本：

```sh
bash ./scripts/build-aab.sh
```

脚本支持：

- `AAB_BUILD_TYPE=debug`
- `AAB_BUILD_TYPE=release`
- `OPEN_ARTIFACT_DIR=0`

同样需要注意：

- npm script 固定走 release
- 真实发版前必须替换签名配置

### 13.3 iOS IPA

执行：

```sh
npm run build:ipa
```

这个脚本内部会：

1. 找到 workspace 或 project
2. 推导 scheme
3. 执行 archive
4. 执行 exportArchive
5. 在导出目录中查找 `.ipa`

常用环境变量：

- `IOS_WORKSPACE_PATH`
- `IOS_PROJECT_PATH`
- `IOS_SCHEME`
- `IOS_CONFIGURATION`
- `IOS_EXPORT_OPTIONS_PLIST`
- `IOS_ARCHIVE_PATH`
- `IOS_EXPORT_PATH`
- `IPA_VERBOSE=1`
- `OPEN_ARTIFACT_DIR=0`

重要限制：

- 当前仓库没有内置 `ios/exportOptions.plist`
- 真实项目必须自行提供导出配置
- 真实打包还需要正确配置签名团队、证书、Provisioning Profile

## 14. 模板初始化时必须修改的内容

当你用这个仓库启动一个新项目时，至少要完成下面这些改造。

### 14.1 应用标识

- 修改 `app.json` 中的名称
- 修改 Android 应用名
- 修改 iOS Display Name
- 修改 Android `applicationId`
- 修改 iOS `PRODUCT_BUNDLE_IDENTIFIER`

### 14.2 品牌资源

- App icon
- Splash / LaunchScreen
- 主题色
- 业务品牌 token

### 14.3 发版配置

- Android release keystore
- Android signing config
- iOS Team ID
- iOS signing settings
- `ios/exportOptions.plist`

### 14.4 权限说明

检查并补齐 `Info.plist` 中的权限文案，例如：

- 定位
- 相机
- 相册
- 麦克风
- 通知

当前模板中某些权限描述仍为空，不能直接带到正式项目中。

### 14.5 业务基础设施

- 导航结构
- 鉴权流
- 用户会话管理
- 环境变量
- API base URL
- 错误处理
- loading / empty / error 状态组件

## 15. 建议的新项目接入顺序

如果你准备把 NovaShell 作为真正的模板使用，建议按这个顺序推进：

1. 改名和包名
2. 接入环境变量体系
3. 建立导航骨架
4. 建立 Zustand store 基础切片
5. 接入一个真实 OpenAPI schema
6. 写一个真实接口请求示例
7. 建立登录态或首屏流程
8. 配置 Android / iOS 正式签名
9. 补 lint / test / build 的 CI

这样做的好处是，模板会尽快从“静态壳”变成“可以承载业务的项目骨架”。

## 16. 测试与质量检查

### 16.1 Lint

```sh
npm run lint
```

### 16.2 Test

```sh
npm test
```

如果当前环境中 Watchman 不可用或权限受限，Jest 可能失败。  
这种情况下可以使用：

```sh
npm test -- --runInBand --watchman=false
```

### 16.3 当前测试现状

当前仓库只有非常基础的 smoke test，作用主要是验证 App 可以被渲染。  
它还没有覆盖：

- 导航行为
- 状态管理逻辑
- API 层逻辑
- 复杂 UI 组件

如果要把模板作为团队长期复用基线，建议后续补：

- API 工具层测试
- store 单元测试
- 核心 UI 组件快照或行为测试

## 17. 包管理器说明

当前仓库同时存在：

- `package-lock.json`
- `yarn.lock`

这意味着仓库还没有完全收口到单一包管理器。  
团队落地时建议明确只保留一种：

- 如果统一用 npm，就删除 `yarn.lock`
- 如果统一用 Yarn，就删除 `package-lock.json`

否则长期会出现依赖漂移和安装结果不一致的问题。

## 18. 已知限制

为了避免误判模板成熟度，这里再集中列一次当前已知限制：

- README 现在已经说明清楚，但模板本身还没完全产品化
- 导航依赖已安装，但导航容器还没有真正接入
- Zustand 已安装，但还没有真实 store 样例
- WebView 已安装，但没有嵌入页面示例
- API 代码生成已就绪，但没有真实 schema 示例
- Android release 仍默认使用 debug keystore
- iOS 缺少默认 `exportOptions.plist`
- 缺少 CI 工作流
- 缺少 `.env.example` 和环境切换方案

## 19. 这个模板适合什么场景

适合：

- 公司内部统一 React Native 启动模板
- 新业务线快速起盘
- POC 和 MVP 项目
- 希望从一开始就统一样式和目录约定的团队

不太适合：

- 需要零配置直接上线的商业模板
- 希望模板内已经内建完整鉴权、路由、数据层、CI 的团队

## 20. 后续推荐补齐项

如果要把 NovaShell 继续打磨成“更完整的模板项目”，建议优先做这几件事：

1. 接入真实 `NavigationContainer` 和初始路由结构
2. 提供一个标准 Zustand store 示例
3. 增加 `.env.example` 和配置读取层
4. 提供一个真实 API 模块示例
5. 修正 Android release signing
6. 补 `ios/exportOptions.plist` 示例
7. 增加 GitHub Actions 或其他 CI
8. 收口到单一包管理器

## 21. 总结

NovaShell 当前已经是一个比 React Native 默认初始化项目更接近真实开发的模板基线。  
它的优势在于工程底座已经搭好，继续开发会比从零初始化快很多。  
它的边界也很明确：现在完成的是“起步工程”，不是“交付成品模板”。

如果你的目标是作为团队统一模板长期复用，建议把第 20 节里的内容继续补完。
