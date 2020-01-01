---
title: SSO
date: 2019-7-23 15:02:22
categories: SSO
---

### 单点登录
单点登录（Single Sign On，SSO），就是在多个系统中，用户只需登录一次，各个系统便可感知该用户已经登录。

### 单系统实现SSO
- 用户登录时，验证用户的账户和密码；
- 生成一个Token保存在数据库中，并写入Cookie中；
- 将用户数据保存在Session中；
- 发起请求时都会带上Cookie，检查Session中有没有登录，如果已登录就继续。