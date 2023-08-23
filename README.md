# Noteonline

一个类似与 Note.ms 的开源项目，基于 Vue + Vite，使用 LeanCloud 实现无服务器部署。

[Demo]() 演示

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