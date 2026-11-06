# JMeter 接口 & 性能测试学习笔记

> 一份面向初学者的 Apache JMeter 实操笔记，覆盖**环境搭建 → 入门接口测试 → 断言 → 参数化 → 关联（JSON/正则提取）→ 连接数据库**的完整学习路径，并附带可直接打开运行的 `.jmx` 脚本。

---

## 📚 项目简介

本仓库整理了 JMeter 的常用功能与实战练习，采用「知识点 + 步骤截图 + 配套脚本」的形式，适合作为接口功能测试、接口性能测试的入门资料。

涵盖内容：

- **环境搭建**：JDK 与 JMeter 的安装、环境变量配置、主题与语言切换
- **接口入门**：线程组、HTTP 请求取样器、查看结果树监听器
- **断言**：响应断言、JSON 断言（自动判定预期与实际结果是否一致）
- **参数化**：用户定义的变量、CSV Data Set Config（多组数据循环调用）
- **关联（依赖）**：JSON 提取器、正则表达式提取器（请求间的数据传递）
- **连接数据库**：MySQL 驱动配置、JDBC Connection Configuration、JDBC Request

---

## 📂 目录结构

```text
jmeter/
├── 01-环境搭建.md            # JDK / JMeter 安装与配置
├── 02-入门.md                # 第一个 HTTP 接口请求
├── 03-断言.md                # 响应断言 / JSON 断言
├── 04-jmeter参数化.md         # 用户变量 / CSV 参数化
├── 05-JMeter依赖.md           # JSON 提取器 / 正则提取器（关联）
├── 06-jmeter连接数据库.md      # MySQL JDBC 连接与查询
├── 参数化-CSV.jmx            # 根目录示例脚本
├── jmeter脚本/               # 配套 JMeter 脚本
│   ├── JSON提取器.jmx
│   ├── json断言.jmx
│   ├── 参数化-CSV.jmx
│   ├── 参数化-用户变量.jmx
│   ├── 连接数据库.jmx
│   └── test_data.csv         # CSV 参数化测试数据
└── img/                      # 笔记配图（37 张）
```

---

## 🗺️ 建议学习路线

1. `01-环境搭建.md` —— 先把 JDK 8/11 与 JMeter 5.4+ 跑起来
2. `02-入门.md` —— 用线程组 + HTTP 请求访问一个接口
3. `03-断言.md` —— 给请求加断言，自动校验结果
4. `04-jmeter参数化.md` —— 用 CSV 实现多组账号/数据循环
5. `05-JMeter依赖.md` —— 用 JSON 提取器做请求间关联
6. `06-jmeter连接数据库.md` —— 用 JDBC 直接查库做数据校验

每篇笔记都对应 `jmeter脚本/` 下可直接用 JMeter 打开运行的 `.jmx` 文件。

---

## 🧰 环境与版本要求

| 组件      | 推荐版本                         | 说明                                   |
| --------- | -------------------------------- | -------------------------------------- |
| JDK       | JDK 8 或 JDK 11                  | JMeter 5.4+ 推荐；多版本切换改 `Path` 即可 |
| JMeter    | 5.4+                             | 解压路径**不要含中文或空格**           |
| MySQL     | 8.0（连接数据库章节）            | 驱动类用 `com.mysql.cj.jdbc.Driver`    |
| 操作系统  | Windows / macOS / Linux          | 笔记以 Windows 截图为准                |

> ⚠️ 常见坑：MySQL 8 连接需加 `serverTimezone=Asia/Shanghai`；执行多条 SQL 需开启 `allowMultiQueries=true`；JDK 8 只支持 `java -version`，不支持 `-ver` 简写。

---

## 🚀 快速开始

```bash
# 1. 校验 Java
java -version

# 2. 解压 JMeter 后，进入 bin 目录启动（保持命令行窗口打开）
jmeter          # Windows
# 或
./jmeter        # macOS / Linux

# 3. 在 JMeter 中打开 jmeter脚本/ 下的 .jmx 文件即可运行
```

---

## ⚠️ 关于图片与 Obsidian 语法说明

笔记中的图片引用使用了 **Obsidian 的 Wiki 链接语法**（如 `![[Pasted image xxx.png]]`），这种写法在 **GitHub 上无法渲染**。

- 如果你使用 **Obsidian** 打开本仓库，图片可正常显示；
- 如果你直接在 **GitHub** 浏览，图片会显示为纯文本链接。

如需在 GitHub 上正常显示图片，有两种方式：

1. 将图片引用改为标准 Markdown 语法，例如：
   `![环境校验](img/Pasted%20image%2020261105095844.png)`
2. 或在本地用 Obsidian 打开仓库阅读（推荐，体验最佳）。

---

## 📤 上传到 GitHub

```bash
git init
git add .
git commit -m "docs: 初始化 JMeter 学习笔记仓库"
git branch -M main
git remote add origin <你的仓库地址>
git push -u origin main
```

> 提示：仓库已包含 `.gitignore`，会自动忽略 `jmeter.log`、结果文件、IDE 配置等本地垃圾文件，无需手动清理。

---

## 📄 许可证

本项目笔记与脚本以 **CC BY 4.0**（署名-非商业性使用-相同方式共享，或根据个人需求自行调整）发布，欢迎学习与转发。
