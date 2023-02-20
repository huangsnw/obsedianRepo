# 简介

RabbitMQ 是一个消息代理：它接受和转发消息。您可以把它想象成一个邮局：当您将要投寄的邮件放入邮箱时，您可以确定邮递员最终会将邮件投递给您的收件人。在这个类比中，RabbitMQ 是一个邮箱、一个邮局和一个邮递员。

# docker运行rabbitmq

```Bash
// 运行
docker run -id --hostname myrabbit --name rabbitmq1 -p 15672:15672 -p 5672:5672 rabbitmq

// 进入容器
docker exec -it rabbitmq1 /bin/bash

// 下载插件
rabbitmq-plugins enable rabbitmq_management


```

访问地址 [http://localhost:15672/](http://localhost:15672/#/) 账号密码初始是guest

# 七种模式

## Hello World

## Work Queues

## Publish/Subscribe

## Routing

## Topics

## RPC

## Publisher Confirms