# ADR-0002：Java 服务端采用 Maven 与 Maven Wrapper

- 状态：已接受
- 日期：2026-07-22

## 背景

CodePulse 的 Java 服务端需要统一完成依赖下载、源代码编译、自动化测试、应用打包和构建插件执行。项目需要让不同开发环境和后续自动化流程使用相同的构建入口，而不能依赖每台电脑恰好安装了兼容版本的全局构建工具。

项目开发者尚未实际使用 Maven 或 Gradle。当前主要学习目标是 Spring 和 Java Web 工程实践；未来可能开发 Android 应用，而 Android 通常使用 Gradle 和 Android Gradle Plugin 构建。

构建工具的选择应服务于当前项目，同时为以后比较其他构建模型提供基础。CodePulse 不需要通过同时维护 Maven 和 Gradle 来证明二者都能工作。

## 决策因素

- 学习 Java 依赖、测试、打包和构建生命周期的基础概念；
- 减少学习 Spring 时同时引入的新语言和构建 DSL；
- 为开发者、编辑器和自动化流程提供统一命令；
- 固定构建工具版本，不要求预先安装全局 Maven；
- 保持第一版单体服务端的构建配置直接且容易检查；
- 避免维护两套能够产生同一应用的构建定义。

## 考虑过的方案

### Maven 与 Maven Wrapper

Maven 使用 `pom.xml` 声明项目坐标、依赖、插件和构建配置，并通过固定生命周期组织编译、测试和打包。Maven Wrapper 将启动脚本和版本配置保存在仓库中，使项目能够通过 `./mvnw` 使用指定 Maven 版本，而不依赖全局 `mvn`。

该方案的约定较固定，适合先理解常见 Java 构建阶段。代价是 XML 配置可能较冗长，复杂定制也不如通用构建 DSL 灵活。

### Gradle 与 Gradle Wrapper

Gradle 使用任务图和 Groovy 或 Kotlin DSL 描述构建，支持灵活定制、增量构建和多模块工程。Android 项目通常使用 Gradle，因此现在选择它可以提前接触部分 Android 构建语法。

但 CodePulse 当前并不需要 Android Gradle Plugin、Android 构建变体或复杂构建逻辑。此时引入 Gradle 会要求项目开发者在学习 Spring 的同时理解新的 DSL 和任务模型，而这些 Android 特有知识仍需在真实 Android 项目中重新学习。

### 手工调用 Java 工具

直接使用 `javac`、`java` 和 `jar` 能够展示编译与打包的底层步骤，但不能合理承担 Spring 依赖解析、测试执行、插件配置和可重复构建。它适合作为小型学习实验，不适合作为 CodePulse 的项目构建方式。

### 依赖全局 Maven

只要求开发者安装全局 Maven 可以减少仓库中的 Wrapper 文件，但不同电脑可能使用不同版本，首次配置也需要额外安装步骤。项目开发者当前没有全局 `mvn`，而项目没有必要制造这项机器级前置条件。

## 决策

CodePulse 的 Java 服务端使用 Maven 作为唯一构建工具，并在创建 Java 项目时提交 Maven Wrapper。

项目通过 `./mvnw` 执行日常编译、测试和打包。Maven 版本在 Java 服务端里程碑开始时固定；现在不提前生成 Wrapper、`pom.xml` 或下载依赖。

本决策不决定具体 Spring 版本、Java 依赖、插件配置、模块划分或发布格式。这些内容在对应实现里程碑中按实际需要确定。

## 影响

### 正面影响

- 项目开发者能够在较固定的生命周期中学习 Java 构建基础；
- 仓库提供统一构建入口，不要求安装全局 Maven；
- Maven 与 Spring 项目的常见结构和测试流程能够直接配合；
- 以后学习 Gradle 时，可以比较依赖、仓库、插件、Wrapper、任务和生命周期等概念。

### 负面影响

- `pom.xml` 可能比等价的 Gradle 构建文件更冗长；
- 该项目不会直接训练 Android 所需的 Gradle、Kotlin DSL 和 Android Gradle Plugin 配置；
- Maven 固定生命周期对高度定制的构建不如 Gradle 灵活；
- Wrapper 第一次获取指定 Maven 发行版以及依赖时仍然需要网络，不能把首次构建误认为完全离线。

## 重新评估条件

出现以下情况之一时重新评估本决策：

- Java 服务端发展为复杂多模块工程，并出现 Maven 难以维护的实际构建需求；
- 构建性能经过测量后成为显著开发瓶颈，且 Gradle 能提供可验证的改进；
- 项目需要与一个已有的 Gradle 多项目构建统一；
- Maven 或 Maven Wrapper 无法继续获得项目所需的维护与安全支持。

未来 Android 项目使用 Gradle 不会自动推翻本决策，因为两个项目可以根据各自生态选择不同构建工具。若 CodePulse 自身更换构建工具，应创建新的 ADR 取代本文档，而不是同时维护 Maven 和 Gradle。
