---
title: "PostgreSQL 安装与使用"
date: 2020-05-26T19:17:49+08:00
tags: ["sql"]
draft: false
---

- Ubuntu 18.04

## 安装

编辑 `/etc/apt/sources.list.d/pgdg.list`，添加：

```text
deb http://apt.postgresql.org/pub/repos/apt/ bionic-pgdg main
```

执行：

```shell
wget --quiet -O - https://www.postgresql.org/media/keys/ACCC4CF8.asc | sudo apt-key add -
sudo apt-get update
sudo apt install postgresql-12 pgadmin4
```

- pgadmin4 图形客户端

## 常用命令

- 通过用户 `postgres` 启动客户端

  ```shell
  sudo su - postgres
  psql
  ```

- 以指定角色（用户）登录指定数据库

  ```shell
  psql -h 127.0.0.1 -U example -d example_db
  ```

- 创建具备登录权限的角色

  ```psql
  CREATE ROLE example LOGIN PASSWORD 'YOUR_PASSWORD';
  ```
- 删除角色

  ```psql
  DROP ROLE example;
  ```

- 修改密码

  ```psql
  ALTER ROLE example PASSWORD 'NEW_PASSWORD';
  ```

- 创建数据库并指定所有者

  ```psql
  CREATE DATABASE example_db WITH owner = example;
  ```

- 删除数据库

  ```psql
  DROP DATABASE example_db;
  ```

## .pgpass 免密登录

新建 `~/.pgpass` 文件，添加：

```text
127.0.0.1:5432:example_db:example:YOUR_PASSWORD
```

修改文件权限：

```shell
chmod 0600 ~/.pgpass
```

免密登录：

```shell
psql -h 127.0.0.1 -U example -d example_db
```

## 参考

- [Linux downloads (Ubuntu)](https://www.postgresql.org/download/linux/ubuntu/)
- [The Password File](https://www.postgresql.org/docs/12/libpq-pgpass.html)
