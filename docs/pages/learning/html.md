# html

```vue
<template>
	<button>123</button>
</template>

```


## ywUi ![](https://img.shields.io/badge/Version-1.0.0-ff974d.svg?style=plastic)

ywUi 驾驶舱数据配置页面

## 安装

```javascript
npm install -D ywUi
```

## 依赖

- [Ant-Design-Vue](https://www.antdv.com/components/overview-cn/)
- [node](http://nodejs.org/) 和 [git](https://git-scm.com/) -项目开发环境
- [Vite](https://vitejs.dev/) - 熟悉 vite 特性
- [Vue3](https://v3.vuejs.org/) - 熟悉 Vue 基础语法 ***
- [TypeScript](https://www.typescriptlang.org/) - 熟悉`TypeScript`基本语法

![](https://img.shields.io/badge/Node->=16.0.0-076214.svg?style=plastic)
![](https://img.shields.io/badge/Vue->=3.2.31-42b883.svg?style=plastic)
![](https://img.shields.io/badge/Vite->=3.2.31-6372fa.svg?style=plastic)
![](https://img.shields.io/badge/TypeScript->=4.6.2-246fbb.svg?style=plastic)
![](https://img.shields.io/badge/AntDesign-3.0-0066fa.svg?style=plastic)
## API
| 参数 | 说明 | 类型 | 默认值 |版本 |
| ----------- | ----------- | ----------- |----------- |----------- |
| allModuleApi      | 全部模块接口方法 (axios 请求函数 )   | function |
| moduleApi   | 单独模块接口方法   (axios 请求函数 )  | function |
| ruleApi   | 规则接口方法 (axios 请求函数 ) | function | 
| submitApi   | 提交接口方法  (axios 请求函数 )  | function |
| complexTypes   | 复杂类型数组  | string[] | ["list", "table"] 
| expandAll   | 展开所有树节点  | boolean | false
<!-- ## 事件  -->

## 使用
- step1
```javascript
// main.ts
import YwUi from 'ywUi';
import 'yw-ui/lib/style.css';

const app = createApp(App);
app.use(YwUi);
app.mount("#app");

```
- step2
```javascript
// xxx.vue
<template>
  <div class="cockpit">
    <CockpitData
      :all-module-api="xxx"
      :module-api="xxx"
      :rule-api="xxx"
      :submit-api="xxx"
    />
  </div>
</template>

```
![](https://img.shields.io/badge/yw-ui-ff974d)


