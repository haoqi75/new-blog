# NodeAuth部署指南

![Images](https://cp.qtdt.qzz.io/api/p/HuggingFace_Dataset/puplic_blog/nodeauth.png?download=true&sign=Dken65rTXHcTUXeCm0b3yvMEGczKZFYtMUiSQdRCVc4%3D%3A0)

## NodeAuth是什么？

NodeAuth是基于CF里的2FA程序，完美解决了现场没有2FA程序的尴尬，这个软件有手就可以部署。

## 优点

- 完全安全，不用怕偷窃以及恐怕行为。
- Serverless云部署，无服务器，直接高速加载网页。无需信用卡。
- 内含一系列功能。
- 支持多平台登陆方式。
- 更多功能。

## 准备工作

- 最少你有个电子邮件吧
- 一个[GitHub](https://github.com/login)帐户（最好超过半年的）。
- 一个[CloudFlare](https://dash.cloudflare.com/login)账户（部署服务器）。
- 一个[DNSHE](https://my.dnshe.com/clientarea.php)账户（用来绑定域名，需要GitHub验证）。
- 一个[NodeLoc](https://www.nodeloc.com/login)账户（用来获取邀请码的）。

## 部署方式

- [直接部署到CloudFlare Workers](https://wiki.nodeauth.io/deploy/cf-worker.html)：直接部署，小白建议。缺点就是不能更新，更新后会丢失变量以及绑定，需要修改配置文件，信息很容易暴露在外。
- [部署到私人VPS/NAS（Docker）](https://wiki.nodeauth.io/deploy/docker.html)：最安全，但是不是每个人都有。
- [通过GitHub Actions部署到CloudFlare Workers](https://wiki.nodeauth.io/deploy/github-action.html)：这个帖子的步骤，很难但不会丢失。