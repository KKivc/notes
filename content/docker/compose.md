---
title: compose
space: docker
---

# Basic

- 通过一个yml文件，定义一组和关联的应用容器为一个项目

## 命令

```bash
#启用
docker compose up

#启用并后台运行
docker compose up -d 

#删除
docker compose down

#显示进程
docker compose ps

#检查配置
docker compose config

#检查配置且有问题才输出
docker compose config -q
```



