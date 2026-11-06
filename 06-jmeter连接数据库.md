![连接数据库](连接数据库.jpg)
## 关键配置：
### 1.添加MySQL驱动jar包
+ 方式一：在测试计划面板点击“浏览...”按钮，将jdbc驱动添加进jmeter 目录下
+ 方式二：将MySQL驱动jar包放到lib/目录下，重启jmeter
## 2.配置数据库连接信息
- 添加方式：测试计划-线程组-右键添加配置元件-JDBC Connection Configuration
![[Pasted image 20261105163253.png]]
- 添加JDBC请求：测试计划-线程组-取样器-JDBC-Request
![[Pasted image 20261105161947.png]]

- 查看结果树
![[Pasted image 20261105163408.png]]

> [!注意：]
> 

1. 旧版5.x 版本驱动类是：`com.mysql.jdbc.Driver`
新版MySQL8.0驱动类是：`com.mysql.cj.jdbc.Driver`
 2. Database URL

```
jdbc:mysql://localhost:3306/jmeter_db?serverTimezone=Asia/Shanghai&useSSL=false&allowMultiQueries=true
```

- `serverTimezone=Asia/Shanghai`：解决时区报错（MySQL8 高频坑）
- `useSSL=false`：本地开发关闭 ssl
- `allowMultiQueries=true`：**开启一条 JDBC 请求里执行多条 SQL（用；分隔）**

3. JDBC 本身执行单条 SQL 的时候不需要分号；分号是 Navicat、MySQL 客户端这类工具的语法结束标记。
  - 单条 select：带不带 `;` 大多都能执行
  - 如果后面要写多条 SQL（用`;`分隔），需要在 JDBC 连接配置里额外开启 `allowMultiQueries=true`如果只是单条 select，**不需要加 allowMultiQueries**，只有一次性执行多条 SQL 才需要