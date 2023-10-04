# linux-service

Linux 能够使用 systemd 管理服务，包管理软件安装的服务，其 service 文件一般存放于 `[/usr]/lib/systemd/` 中，而管理员编写的 service 文件一般存放于 `/etc/lib/systemd/`

> 一般 systemd 可以管理的称为“单元”，包括但不限于：
> - 服务（.service）
> - 挂载点（.mount）
> - 设备（.device）
> - 套接字（.socket）
>
> 但本文局限于服务，一是写成“单元”会增加理解难度，二是一般还是使用服务比较多。

## 系统单元&用户单元

系统单元随系统启动，存放于 `systemd/system/` ，用户单元随用户登录启动，存放于 `systemd/user/`

## 例子

例如，我有一个名为filebrowser的服务，该服务可执行文件位于 `/opt/filebrowser/filebrowser` 。

```toml
[Unit]
Description=start filebrower https service on port 80
Documentation=https://github.com/filebrowser/filebrowser
Wants=network-online.target

[Service]
Type=simple
ExecStart=/opt/filebrowser/filebrowser -p 80 -a 0.0.0.0 

[Install]
WantedBy=multi-user.target

```

## 字段解释

**TODO**

## 相关链接

1. [https://wiki.archlinuxcn.org/wiki/Systemd#编写单元文件](https://wiki.archlinuxcn.org/wiki/Systemd#%E7%BC%96%E5%86%99%E5%8D%95%E5%85%83%E6%96%87%E4%BB%B6)
2. [https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux/7/html/system_administrators_guide/chap-managing_services_with_systemd#sect-Managing_Services_with_systemd-Unit_Files](https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux/7/html/system_administrators_guide/chap-managing_services_with_systemd#sect-Managing_Services_with_systemd-Unit_Files)
3. [https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux/9/html/configuring_basic_system_settings/working-with-systemd-targets_configuring-basic-system-settings#doc-wrapper](https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux/9/html/configuring_basic_system_settings/working-with-systemd-targets_configuring-basic-system-settings#doc-wrapper)