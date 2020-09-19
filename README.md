# mydashboard
用 podman 把 grafana &amp; loki &amp; prometheus 组成一个用于显示不仅仅是 v2ray 使用情况的 pod  
当然，它显示什么得看你怎么调整配置文件  
prometheus 如何与 exporter 交互之类的看 `service` 文件吧，我不想说了（如果打算用多个 exporter 建议~~再运行等同于 exporter 数量的 socat 容器或者~~暴露 prometheus 端口）

## 使用时需要什么？
安装 `podman` 和 `v2ray-exporter` 才能正常工作并显示 `v2ray` 使用情况 ~~（为了正常观看建议从[这里](https://grafana.com/grafana/dashboards/11545)导入 dashboard）~~  
`v2ray-exporter` 如何使用使用建议看[v2ray-exporter 主页](https://github.com/wi1dcard/v2ray-exporter)  
如果你想看 log 就动手装 `promtail` ，然后按照自己的需求改配置

## 如何使用？
把 `mydashboard/etc` 下面的所有东西 `cp -a` 进 `/etc`（记得设置好权限（参考附带的 tar）），然后 `systemd-tmpfiles --create`、enable --now mdd-p...  
~~然后你可能会发现服务跑不起来，如果是的话建议重启机器再试。可能是我遗漏了什么~~  
`grafana` 用 `socket 文件`监听，位置~~自己找~~是 `/run/mydashboard/grafana/grafana.sock`

## 已知问题
~~默认提供的 v2ray dashboard 在显示上有严重问题，建议自行制作或者从[这里](https://grafana.com/grafana/dashboards/11545)导入~~ 已经删掉了  
~~如果你发现服务一直在重启，建议 exporter 早于容器启动~~ 在 socat 参数中加入了重试选项，不会出问题了

## Special Thanks

[v2ray-exporter](https://github.com/wi1dcard/v2ray-exporter)  
没有这个我就不知道怎么办了，~~总不能只是为了看情况就使 [SSPanle UIM](https://github.com/Anankke/SSPanel-Uim) 吧~~  

[NickCao](https://nichi.co/)  
提供了大量技术支持
