# scratch-gui

## **⚠️ 注意：仓库迁移到单体仓库 ⚠️**

Scratch 团队已将 `scratch-gui` 模块迁移到新的单体仓库
[`scratch-editor`](https://github.com/scratchfoundation/scratch-editor)。这个独立的 `scratch-gui` 仓库
**将被归档**。任何新的问题或拉取请求都应该在单体仓库中提出。

新的单体仓库版本的 `scratch-gui` 已发布到 NPM 注册表，包名为
[`@scratch/scratch-gui`](https://www.npmjs.com/package/@scratch/scratch-gui)。

**贡献者：**

* 我要感谢所有过去为这个仓库做出贡献的人。
* 如果您知道有价值的问题或拉取请求，请考虑在单体仓库中重新提出。如果您这样做，
  请将新的问题或拉取请求链接到此仓库中的原始问题，以帮助其他人找到它并减少重复工作的可能性。
* 我们为造成的不便表示歉意，非常感谢您在这次过渡中的帮助！

更多信息，请参见 [GitHub 上的 `scratch-editor` 仓库](https://github.com/scratchfoundation/scratch-editor)。

## 概述

Scratch GUI 是一组 React 组件，构成了创建和运行 Scratch 3.0 项目的界面。

在 Github Pages 上打开当前构建版本：

<https://scratchfoundation.github.io/scratch-gui/>

## 安装

这需要您安装 Git 和 Node.js。

在您自己的 node 环境/应用程序中：

```bash
npm install https://github.com/scratchfoundation/scratch-gui.git
```

如果您想要编辑/自己测试：

```bash
git clone https://github.com/scratchfoundation/scratch-gui.git
cd scratch-gui
npm install
```

**您可能想要在 `git clone` 命令中添加 `--depth=1`，因为 [git 仓库历史中有一些大文件](https://github.com/scratchfoundation/scratch-gui/issues/5140)。**

## 开始使用

运行项目需要安装 Node.js。

## 运行

在仓库中打开命令提示符或终端并运行：

```bash
npm start
```

然后访问 [http://localhost:8601/](http://localhost:8601/) - playground 输出默认的 GUI 组件

## 与其他 Scratch 仓库并行开发

### 让另一个仓库指向此代码

如果您希望在开发 `scratch-gui` 的同时并行开发依赖于它的其他 scratch 仓库，您可能希望
让其他仓库使用您本地的 `scratch-gui` 构建，而不是获取使用 `npm install` 默认找到的
当前生产版本的 scratch-gui。

以下是如何将您的本地 `scratch-gui` 代码链接到另一个项目的 `node_modules/scratch-gui`。

#### 配置

1. 在您本地的 `scratch-gui` 仓库顶层：
    1. 确保您已运行 `npm install`
    2. 通过运行 `BUILD_MODE=dist npm run build` 构建 `dist` 目录
    3. 通过运行 `npm link` 建立到此仓库的链接

2. 从依赖于 `scratch-gui` 的每个仓库（如 `scratch-www`）的顶层：
    1. 确保您已运行 `npm install`
    2. 运行 `npm link scratch-gui`
    3. 构建或运行仓库

#### 使用 `npm run watch`

您可以使用 `BUILD_MODE=dist npm run watch` 代替 `BUILD_MODE=dist npm run build`。这将监视
您的 `scratch-gui` 代码更改，并在有更改时自动重新构建。有时这可能不太可靠；如果您遇到问题，
请尝试回到 `BUILD_MODE=dist npm run build` 直到您解决它们。

#### 哦不！它不工作

如果您无法让链接正常工作，请尝试：

* 按照上述步骤逐步进行，不要更改顺序。特别重要的是在 `npm link` _之前_ 运行 `npm install`，
  因为在链接后安装会重置链接。
* 确保仓库在您机器的文件树中是同级的，比如
  `.../.../MY_SCRATCH_DEV_DIRECTORY/scratch-gui/` 和 `.../.../MY_SCRATCH_DEV_DIRECTORY/scratch-www/`。
* 一致的 node.js 版本：如果您为不同的 Scratch 仓库打开了多个终端标签或窗口，
  请确保在所有终端中使用相同的 node 版本。
* 如果其他方法都不起作用，请在两个仓库中运行 `npm unlink` 来取消链接，然后重新开始。

## 测试

### 文档

在编写测试时，您可能想要查看 [Jest](https://facebook.github.io/jest/docs/en/api.html) 和
[Enzyme](http://airbnb.io/enzyme/docs/api/) 的文档。

更多选项请参见 [jest cli 文档](https://facebook.github.io/jest/docs/en/cli.html#content)。

### 运行测试

_注意：如果您是 Windows 用户，请在 Windows `cmd.exe` 中运行这些脚本，而不是 Git Bash/MINGW64。_

在运行任何测试之前，请确保您已从此（scratch-gui）仓库的顶层运行 `npm install`。

#### 主要测试命令

要一次运行 linter、单元测试、构建和集成测试：

```bash
npm test
```

#### 运行单元测试

单独运行单元测试：

```bash
npm run test:unit
```

在监视模式下运行单元测试（监视代码更改并持续运行测试）：

```bash
npm run test:unit -- --watch
```

您可以运行单个集成测试文件（在此示例中，是 `button` 测试）：

```bash
$(npm bin)/jest --runInBand test/unit/components/button.test.jsx
```

#### 运行集成测试

集成测试使用无头浏览器来操作仓库产生的实际 HTML 和 javascript。您不会看到这种活动
（尽管当播放声音时您可以听到！）。

要运行集成测试，您首先需要安装 Chrome、Chromium 或其变体，以及 Chromedriver。

请注意，集成测试需要您首先创建一个可以在浏览器中加载的构建：

```bash
npm run build
```

然后，您可以运行所有集成测试：

```bash
npm run test:integration
```

或者，您可以运行单个集成测试文件（在此示例中，是 `backpack` 测试）：

```bash
$(npm bin)/jest --runInBand test/integration/backpack.test.js
```

如果您想要在测试运行时观察浏览器，而不是无头运行，请使用：

```bash
USE_HEADLESS=no $(npm bin)/jest --runInBand test/integration/backpack.test.js
```

## 故障排除

### 忽略可选依赖项

运行 `npm install` 时，您可能会收到关于可选依赖项的警告：

```text
npm WARN optional Skipping failed optional dependency /chokidar/fsevents:
npm WARN notsup Not compatible with your operating system or architecture: fsevents@1.2.7
```

您可以通过添加 `no-optional` 开关来抑制它们：

```bash
npm install --no-optional
```

进一步阅读：[Stack Overflow](https://stackoverflow.com/questions/36725181/not-compatible-with-your-operating-system-or-architecture-fsevents1-0-11)

### 解决依赖项

首次安装时，您可能会收到需要解决的警告：

```text
npm WARN eslint-config-scratch@5.0.0 requires a peer of babel-eslint@^8.0.1 but none was installed.
npm WARN eslint-config-scratch@5.0.0 requires a peer of eslint@^4.0 but none was installed.
npm WARN scratch-paint@0.2.0-prerelease.20190318170811 requires a peer of react-intl-redux@^0.7 but none was installed.
npm WARN scratch-paint@0.2.0-prerelease.20190318170811 requires a peer of react-responsive@^4 but none was installed.
```

您可以检查哪些版本可用：

```bash
npm view react-intl-redux@0.* version
```

您需要安装所需的版本：

```bash
npm install  --no-optional --save-dev react-intl-redux@^0.7
```

依赖项本身可能有更多缺失的依赖项，这将显示如下：

```bash
user@machine:~/sources/scratch/scratch-gui (491-translatable-library-objects)$ npm install  --no-optional --save-dev react-intl-redux@^0.7
scratch-gui@0.1.0 /media/cuideigin/Linux/sources/scratch/scratch-gui
├── react-intl-redux@0.7.0
└── UNMET PEER DEPENDENCY react-responsive@5.0.0
```

您也需要安装这些：

```bash
npm install  --no-optional --save-dev react-responsive@^5.0.0
```

进一步阅读：[Stack Overflow](https://stackoverflow.com/questions/46602286/npm-requires-a-peer-of-but-all-peers-are-in-package-json-and-node-modules)

## 发布到 GitHub Pages

您可以将 GUI 发布到 github.io，以便互联网上的其他人可以查看它。
[阅读 wiki 获取分步指南。](https://github.com/scratchfoundation/scratch-gui/wiki/Publishing-to-GitHub-Pages)

## 理解项目状态机

由于整个 scratch-gui 中的大量代码都依赖于项目的状态，项目会经历许多不同的
加载、显示和保存阶段，我们创建了一个"有限状态机"来明确它在任何时候处于哪种状态。
这包含在文件 src/reducers/project-state.js 中。

理解 src/reducers/project-state.js 中的代码可能很困难。有几种类型的数据和函数
被使用，它们相互关联：

### 加载状态

这些包括状态常量字符串，如：

* `NOT_LOADED`（默认状态），
* `ERROR`，
* `FETCHING_WITH_ID`，
* `LOADING_VM_WITH_ID`，
* `REMIXING`，
* `SHOWING_WITH_ID`，
* `SHOWING_WITHOUT_ID`，
* 等等。

### 转换

这些是导致状态更改的动作名称。一些示例有：

* `START_FETCHING_NEW`，
* `DONE_FETCHING_WITH_ID`，
* `DONE_LOADING_VM_WITH_ID`，
* `SET_PROJECT_ID`，
* `START_AUTO_UPDATING`，

### 转换如何与加载状态相关

如这个项目状态机图表所示，各种转换动作可以将我们从一个加载状态移动到另一个：

![项目状态图](docs/project_state_diagram.svg)

_注意：为了清晰起见，上面的图表排除了与错误处理相关的状态和转换。_

#### 示例

这是状态如何转换的示例。

假设用户点击一个项目，页面开始使用 URL `https://scratch.mit.edu/projects/123456` 加载。

以下是项目状态机中将发生的情况：

![项目状态示例](docs/project_state_example.png)

1. 当应用首次挂载时，项目状态是 `NOT_LOADED`。
2. `SET_PROJECT_ID` redux 动作被派发（来自 src/lib/project-fetcher-hoc.jsx），`projectId` 设置为
   `123456`。这将状态从 `NOT_LOADED` 转换为 `FETCHING_WITH_ID`。
3. `FETCHING_WITH_ID` 状态。在 src/lib/project-fetcher-hoc.jsx 中，`projectId` 值 `123456` 被用来
   从服务器请求该项目的数据。
4. 当服务器响应数据时，src/lib/project-fetcher-hoc.jsx 派发 `DONE_FETCHING_WITH_ID`
   动作，设置 `projectData`。这将状态从 `FETCHING_WITH_ID` 转换为 `LOADING_VM_WITH_ID`。
5. `LOADING_VM_WITH_ID` 状态。在 src/lib/vm-manager-hoc.jsx 中，我们将 `projectData` 加载到
   Scratch 的虚拟机（"vm"）中。
6. 加载完成时，src/lib/vm-manager-hoc.jsx 派发 `DONE_LOADING_VM_WITH_ID` 动作。这将
   状态从 `LOADING_VM_WITH_ID` 转换为 `SHOWING_WITH_ID`。
7. `SHOWING_WITH_ID` 状态。现在项目正常显示，可以播放和编辑。

## 捐赠

我们免费提供 [Scratch](https://scratch.mit.edu)，并希望保持这种方式！请考虑
[捐赠](https://www.scratchfoundation.org/donate) 来支持我们持续的工程、设计、社区和
资源开发工作。任何金额的捐赠都值得赞赏。谢谢您！
