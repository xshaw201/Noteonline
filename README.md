# Noteonline

一个类似与 Note.ms 的开源项目，基于 Vue + Vite，使用 LeanCloud 实现无服务器部署。

[Demo](https://note.xshaw.xyz) 演示

## 目前功能

1. 你可以在地址（`https://note.xshaw.xyz`）后任意添加内容来创建一个页面（不限制任何符号，甚至你还可以创建分页、中文链接，但一些特殊表示除外，比如`@info`）。
2. 你可以任何页面中的编辑框里写笔记，你的笔记将会实时存储在云端，之后再访问你编辑过的页面便可再次看到你写的笔记。
3. 你可以在一个页面的链接后面加上`@info`（根页面请加`/@info`）以查看该页面的创建时间、更新时间、更新者的一些信息（ip 地址等，所以请不要试图在这里散播违法内容！）、查看次数、编辑次数等。
4. 支持夜间模式（其实是 Vue 内置的）。
5. 统一使用鸿蒙字体（遥遥领先），引入了 [Pangu.js](https://github.com/vinta/pangu.js)，刷新页面后会自动分割中英文，优化阅读体验。

## 部署

首先请确保你已符合以下条件

- 最新版的 Node.js 再进行以下步骤
- 有一个 LeanCloud 账号
- 一个已创建好的 LeanCloud 应用

第一步，克隆本仓库到本地：

```bash
git clone git@github.com:imtgs/Noteonline.git
```

第二步，安装依赖：

```bash
npm install
```

第三步，进入`/src/App.vue`，跟改以下代码中的`xxxxxxxxx`为你 LeanCloud 应用的`设置 => 应用凭证`里的 AppID、AppKey

```js
LC.init({
  appId: "xxxxxxxxx",
  appKey: "xxxxxxxxx",
  serverURL: "https://lc.xshaw.xyz",
});
```

第四步，运行以下几个命令构建页面：

```bash
npm run build
cd dist
cp index.html 404.html 
```

现在只需要将`dist`里的文件上传到你喜欢的静态页面托管服务商即可，例如 [Vercel](https://vercel.com)