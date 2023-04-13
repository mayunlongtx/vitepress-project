```javascript
//  创建用户
npm adduser
// 登录
npm login
// 查看是否登录成功
npm whoami
// 退出登录
npm logout
// 查看全局node包安装位置
npm root -g 
// 查看node安装位置
npm get prefix
// 查看当前目录下安装了那些node包
npm ls
// npm 发包
 npm publish 
//注意版本号和包名称是否占用
//包的名称和版本就是你项目里package.json里的name和version哦！
//还有一点要注意的是npm对包名的限制：不能有大写字母/空格/下滑线!
//包文件 不许含有README.md  package.json  index.js

// npm 撤销发布包
npm unpublish <pkg>[@<version>]  --force
//如果报权限方面的错，加上--force

//npm 查看配置文件
//查看用户配置文件路径。
npm config get userconfig
//查看全局配置文件路径。
npm config get globalconfig
//内置配置文件。
//安装npm的目录下的npmrc文件。


```

