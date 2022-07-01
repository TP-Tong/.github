# BIGAI X THU Servers 101

## Users Guide

### Basic Information

Please contact [Yuyang Li](mailto:i@aidenli.net) for the Server List Google Docs. Note that you can only access them

- with BIGAI VPNs - for servers at "BIGAI 3F"
- at Central Building Room 501 - for servers at "THU Central 501"



### Preliminaries

To make sure that you're capable of using a server for computation, it's suggested that you go through several stuffs as preliminaries. Remember that it's common to be frustrated dealing with a command line Linux, but you will master it after try-and-errors. Good luck!



#### Linux

Instead of fully learning Linux, you can just go through:

- [An Intro to Linux](https://www.runoob.com/linux/linux-intro.html)
- [Linux System Contents](https://www.runoob.com/linux/linux-system-contents.html)
- [Remote Login (with PuTTY)](https://www.runoob.com/linux/linux-remote-login.html)
  - Note that you can also login with `ssh` command or other softwares like Termius and VSCode
- [File Attributes and Permissions](https://www.runoob.com/linux/linux-file-attr-permission.html)
- [[Vi/Vim](https://www.runoob.com/linux/linux-vim.html)](https://www.runoob.com/linux/linux-file-attr-permission.html)



#### Conda

You should work in virtual environments to isolate packages among your projects to avoid bad dependencies. You can go through:

- [An Intro to Anaconda](https://zhuanlan.zhihu.com/p/351348108)

> The latest Anaconda installer can be found on the server. See [Useful Resources](##Useful Resources)



#### SSH

You need SSH to login to the server. You can go through this [SSH guide](https://wangdoc.com/ssh/).



### Login

Use SSH to login to the server:

```shell
ssh USERNAME@HOSTNAME.gpu.t.tp-tong.xyz
```

Note that you should change the `USERNAME` and `HOSTNAME` to your account name and the server hostname. E.g. To login to the server `snape` with account `yuyang`, use:

```shell
ssh yuyang@snape.gpu.t.tp-tong.xyz
```



#### Cloudflared Tunnel for Remote Connection

> Note that this method provides temporary access for those with no BIGAI VPNs or are out of the campus.
>
> Compared to other methods, tt has much higher latency.

##### Installing `cloudflared`

First you need to install `cloudflared`, an [open source project](https://github.com/cloudflare/cloudflared) maintained by Cloudflare for Cloudflare Tunnel. Please follow [its instructions](https://developers.cloudflare.com/cloudflare-one/connections/connect-apps/install-and-setup/installation/).

##### SSH Configuration

Modify your ssh configuration file (typically `~/.ssh/config`) and add:

```ini
Host *.tp-tong.xyz
	ProxyCommand cloudflared access ssh --hostname %h
```

##### Connection with Zero-Trust Auth

Then you can login to the server with SSH:

```shell
ssh USERNAME@HOSTNAME.tp-tong.xyz
```

Note that the address is slightly different.

For the first time you connect to a new server, you should see something like:

<img src="https://blog-img-1302618638.cos.ap-beijing.myqcloud.com/uPic/Screen%20Shot%202022-07-01%20at%2015.25.21.png" alt="Screen Shot 2022-07-01 at 15.25.21" style="zoom: 25%;" />

Here's an authentication powered by Cloudflare Zero-Trust. **You should enter an e-mail address ending with `@mails.tsinghua.edu.cn` or `@bigai.ai` to receive an One-Time-Password (OTP)**. By entering the password in the next step, you get the access to the server, then ssh would work.

> This authentication will expire after 24 hours.



## Tips

### Changing Mirrors

Changing mirrors helps boost your package installation with conda, pip, etc, for they download data. Typically we show ways of switching to [TUNA](https://tuna.moe)'s mirrors.

#### Anaconda

We show a common way of [switching to TUNA's Anaconda mirror](https://mirrors.tuna.tsinghua.edu.cn/help/anaconda/).



### Pip (pipi)

We show a common way of  [switching to TUNA's pypi mirror](https://mirrors.tuna.tsinghua.edu.cn/help/pypi/).



## Useful Resources

Useful resources like softwares and datasets are pre-stored on the server to save your time. Here's a list:

#### Softwares

| Name       | Path                 | Latest Version | Reminder                                         |
| ---------- | -------------------- | -------------- | ------------------------------------------------ |
| Anaconda 3 | `/mnt/public/conda/` | `3-2022.05`    | Directly select and run a shell code to install. |
| Miniconda  | `/mnt/public/conda/` | `py38_4.12.0`  | Directly select and run a shell code to install. |



#### Datasets

Only available on `snape`. Please contact [Yuyang](mailto:i@aidenli.net) to send a copy to your directory.

| Name     | Path                           | Field     | Size   |
| -------- | ------------------------------ | --------- | ------ |
| Acronym  | `/mnt/public/dataset/Acronym`  | HOI       | `1.6G` |
| ShapeNet | `/mnt/public/dataset/ShapeNet` | 3D Vision | `69G`  |
| HO3D     | `/mnt/public/dataset/HO3D/`    | HOI       | `67G`  |
| EGAD     | `/mnt/public/dataset/EGAD/`    | HOI       | `265M` |
| YCB      | `/mnt/public/dataset/YCB/`     | 3D Vision | `1.8G` |
