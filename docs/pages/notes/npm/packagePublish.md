# npm 包发布过程

::: tip
[npm 常用命令](./npmCommand.md)
:::
## 账号
- 前往 [npm](https://www.npmjs.com/) 官网创建自己的账号
- 私有包可以查看[用户管理](./privateNpm.md#用户管理)

## 创建项目

```javascript
mkdir nec && cd nec
```
## 初始化项目

```javascript
npm init -y
```
## 修改 package.json
```javascript
{
    "name": "@your-name/nec", //这里的@your-name一定要和author的保持一致
    "version": "0.0.1", // 包版本,发布前需要修改此版本
    "description": "",
    "main": "index.js",
    "directories": {
        "lib": "lib"
    },
    "scripts": {
        "test": "echo \"Error: no test specified\" && exit 1"
    },
    "keywords": [],
    "author": "@your-name",
    "license": "ISC",
    "dependencies": {}
}
```
## 检测 npm 源

```javascript
npm config set registry
```
::: warning
如果是淘宝源则需要设置回 npm 源
:::
```javascript
npm config set registry http://registry.npmjs.org
```
## 登录npm
::: tip
进入到终端
:::
```javascript
npm adduser 
// or
npm login
```
## 发布
```javascript
npm publish
```
::: info
这个当你的包名为@your-name/your-package时，npm publish会默认发布为私有包，但是 npm 的私有包需要付费，所以需要添加如下参数进行发布:
:::
```javascript
npm publish --access public
```
## 问题
::: danger
402 You must sign up for private packages
:::
```javascript
//@youe-name开头会被认为是发布私有包 通过如下命令开放包
npm publish --access public
```
::: danger
403 这个是你的源设置成第三方源的时候才有可能发生
:::
```javascript
npm config set registry http://registry.npmjs.org
```
::: danger
403  也可能是你重名,需要你修改一下包名称 重新上传
:::