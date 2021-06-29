# SDK

## Sequelize

> nodejs 的 ORM 库

### 获取原始对象

Sequelize 获取的数据是封装之后对象，无法直接修改属性，需要对实例通过 get 方法

```jsx
const user = models.User.findOne() // user 是 Sequelize 封装的对象
const userValue = user.get({plain: true}) // userValue 是普通的对象
```

### 修改

```jsx
User.update({name: 'newName'}, {
  where: {...}
})
```

## TypeOrm

> 对 typescript 和 es6 友好的 orm 库，支持 MySQL, PostgreSQL, MariaDB, SQLite, MS SQL Server, Oracle, SAP Hana, WebSQL 等数据库. 可以在 NodeJS, Browser, Ionic, Cordova and Electron 平台运行.

## Babel

[Babel原理](https://mp.weixin.qq.com/s/kI9nm5_hpTvGHHE61fzHNQ?forceh5=1)

## PKG

[vercel](https://github.com/vercel)/[pkg](https://github.com/vercel/pkg)

将 nodejs 代码打包成一个可执行文件，包含 nodejs 运行环境，在目标机器上可以直接运行

```bash
pkg dist/server.js --targets node12-macos-x64
```

