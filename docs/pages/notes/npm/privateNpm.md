# npm 私有化过程

## 前言

- 开发过程中经常有多个项目使用相同功能模块的情况出现,一直都是复制 复制 复制,这样每次有变化就需要去多个地方修改,非常麻烦,当然可以选择使用 `npm` 发布管理,但是 `npm` 是公开的(`npm` 也有私有化收费服务),这样大家就都可以看到你的包并且使用,如果是自己业务关联比较强的,那就不太合适了,这个时候私有 `npm` 就闪亮登场了.

## npm 私有仓库

### npm 私有仓库的好处

- 1.安全性角度的考虑：安全性(布署在内网，资产安全性高)
- 2.开发效率角度的考虑：复用性，开发效率，版本管理(立足之根本)
- 3.下载速度角度的考虑：下载速度提升
- 4.技术积累角度的考虑：技术资产积累
- 5.版本角度的考虑：相当于一个容器，统一管理需要的包，保持版本的唯一
- 6.开发效率角度考虑：使私有公共业务或组件模块能以共有包一样的管理组织方式，保持一致性，提高开发效率.

### npm 私有仓库的原理

![](https://raw.githubusercontent.com/mayunlongtx/my-drawing-bed/main/marldown-img/20221015124053.png)

- 用户 `install` 后向私有 `npm` 发起请求，服务器会先查询所请求的这个模块是否是我们自己的私有模块或已经缓存过的公共模块，如果是则直接返回给用户；如果请求的是一个还没有被缓存的公共模块，那么则会向上游源请求模块并进行缓存后返回给用户。上游的源可以是 `npm` 仓库，也可以是淘宝镜像。

### npm 私有仓库选型

#### 搭建方式

- 付费购买 npm 企业私有仓库
- 使用 git + ssh 这种方式直接引用到 GitHub 项目地址
- 开源代码源代码方式或者 docker 化构建

#### 常用私有 npm 

- Npm 付费服务
- [Sinopia](https://github.com/rlidwka/sinopia)  --- 不再维护
- [Verdaccio](https://verdaccio.org/)   --- 基于Sinopia
- [cnpm](https://npmmirror.com/) 

这里我们选择使用 `Verdaccio`,因为 `Verdaccio` 构建成本比较低，后期也好维护.
### 常用的仓库地址
- npm —— https://registry.npmjs.org
- cnpm —— http://r.cnpmjs.org
- taobao —— https://registry.npm.taobao.org
- nj —— https://registry.nodejitsu.com
- rednpm —— http://registry.mirror.cqupt.edu.cn
- npmMirror —— https://skimdb.npmjs.com/registry
- edunpm —— http://registry.enpmjs.org

<!-- #- [npm](https://registry.npmjs.org)
#- [cnpm](http://r.cnpmjs.org) -->

### Verdaccio 框架

- `Verdaccio`  是一个 Node.js创建的轻量的私有npm proxy registry
- 基于 `Node.js` 的网页应用程序
- 私有  [npm registry](https://verdaccio.org/zh-cn/docs/what-is-verdaccio/#whats-a-registry)
- 本地网络 [proxy](https://verdaccio.org/zh-cn/docs/what-is-verdaccio/#proxy)
- 可插入式应用程序
- 易安装和使用
- 提供 Docker 和 Kubernetes 支持
- 与 yarn, npm 和 pnpm 100% 兼容
- forked 于 sinopia@1.4.0 并且 100% 向后兼容。

![](https://raw.githubusercontent.com/mayunlongtx/my-drawing-bed/main/marldown-img/20221015130515.png)

## Verdaccio
 - Verdaccio is a Node.js private and proxy registry. 在安装之前，您需要确保系统环境已满足以下条件。

![](https://raw.githubusercontent.com/mayunlongtx/my-drawing-bed/main/marldown-img/20221015142604.png)

### 最低要求
- Node.js v12 或更高.(建议使用nvm做版本控制)

- 你喜爱的Node包管理器 npm，pnpm 或 yarn(classic 以及 berry)。

- 我们强烈建议使用最新版本的Node包管理工具，比如> npm@6.x | yarn@1.x | | yarn@2.x | pnpm@6.x。 不再支持npm@5.x或更低版本。

- 使用现代浏览器以访问Web界面， 支持使用 Chrome、 Firefox、 Edge和IE11 浏览器。
Verdaccio 将根据 Node. js 发布工作组 的推荐支持最新的 Node. js 版本。

### npm 方式安装
1. Nodejs 环境下全局安装 verdaccio.
```yaml
vim /root/.config/verdaccio/config.yaml
```
- 加上 -–unsafe-perm 的原因是防止报 grywarn 权限的错。
2. 修改配置文件
- verdaccio 的特点是，你在哪个目录运行，它的就会在对应的目录下创建自己的文件。目录下默认有两个文件：config.yaml 和 storage，htpasswd 是添加用户之后自动创建的。
- 打开默认启动的 config.yaml 文件：
```yaml
vim /root/.config/verdaccio/config.yaml
```
	
```yaml
auth:
	htpasswd:
		file: ./htpasswd
		# Maximum amount of users allowed to register, defaults to "+inf".
		# You can set this to -1 to disable registration.
		max_users: -1
uplinks:
	npmjs:
		url: https://registry.npmjs.org/
	cnpm:
		url: https://registry.npm.taobao.org
packages:
		@aemp/*":
		access: $authenticated
		publish: $authenticated
		unpublish: $authenticated
	"@*/*":
		access: $all
		publish: $authenticated
		unpublish: $authenticated
		proxy: npm
	"**":
		access: $all
		publish: $authenticated
		unpublish: $authenticated
		proxy: npm
```
- access 是访问权限控制，总共有三种身份：所有人($all)、匿名用户($anonymous)、认证(登陆)用户($authenticated)。

3. 对外开放 4873 端口
- verdaccio 继承了 sinopia，端口号 4873 依然不变。
```yaml
firewall-cmd --state                 # 先查看防火墙状态，
service firewalld start              # 开启防火墙:
firewall-cmd --zone=public --add-port=4873/tcp –permanent  # 开放4873端口
firewall-cmd --reload                # 重新载入
firewall-cmd --zone=public --query-port=4873/tcp    # 查看是否添加成功
```
4. 启动 verdaccio
```yaml
verdaccio
```
5. pm2 守护 verdaccio 进程
- 安装 [pm2](../node/pm2.md)：
```yaml
npm install -g pm2 --unsafe-perm
```
- 使用 pm2 启动 verdaccio：
```yaml
pm2 start “which verdaccio”
```
- 可以看到下边这样的内容,就说明已经启动成功了
![](https://raw.githubusercontent.com/mayunlongtx/my-drawing-bed/main/marldown-img/20221015140507.png)
- 查看 pm2 守护下的进程 verdaccio 的实时日志：
```yaml
pm2 show verdaccio
```
  
### Docker 方式安装
1. 拉取 Verdaccio 的 docker 镜像

```yaml
docker pull verdaccio/verdaccio
```

2. 在根目录下创建 docker 文件

```yaml
mkdir -p ~/docker/data
cd ~/docker/data
```
	
3. 从 git 拉取示例到 data 到目录下

```yaml
git clone https://github.com/verdaccio/docker-examples
cd ~/docker/data/docker-examples
```
	
4. 移动配置文件

```yaml
mv docker-local-storage-volume ~/docker/verdaccio
```
	
5. 设置文件夹权限

```yaml
chown -R 100:101 ~/docker/verdaccio
```
	
6. 启动镜像
 - 使用 docker-compose 启动:
```yaml
cd ~/docker/verdaccio
docker-compose build
docker-compose up
```
- 或者使用 docker run 命令启动:
```yaml
V_PATH=~/docker/verdaccio; docker run -it --rm --name verdaccio \
-p 4873:4873 \
-v $V_PATH/conf:/verdaccio/conf \
-v $V_PATH/storage:/verdaccio/storage \
-v $V_PATH/plugins:/verdaccio/plugins \
```
- 打开 'http:ip//:4873' 就可以看到已经启动起来了

![](https://raw.githubusercontent.com/mayunlongtx/my-drawing-bed/main/marldown-img/verdaccio-docker.4f5f3a9a.png)
::: tip
 本地可以将 ip  换成  localhost
:::
## 用户管理
- 1.设置仓库源
::: tip
建议使用 [nrm](./nrm.md) 控制
:::
```yaml
npm set registry http://ip:4873
```
- 2.添加用户
```yaml
#输入 username、password 以及 Email 即可
npm adduser --registry http://ip:4873
```
## 私有包管理
::: tip
也可以参考 [npm 包发布](./packagePublish.md)
:::
- 1. 登录
```yaml
npm login --registry http://ip:4873
```
- 2. 上传私有包
```yaml
npm publish --registry http://ip:4873
```