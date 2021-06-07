# Nest.js

基于Node.js 和 Typescript 的 AOP 开发框架，灵活且强大。
[中文文档](https://docs.nestjs.cn/)

![picture 27](../../images/77d711ecbfa7d1bee9c150a460af2d70ba3e57e13a31cf0150755b585c8d7515.png)  

## 一些装饰器

### controller

```jsx
@Request()  req
@Response() @Res()*	res  // 使用该注解时必须调用res.json(…)或 res.send(…)返回响应
@Next()	next
@Session()	req.session
@Param(key?: string)	req.params / req.params[key]
@Body(key?: string)	req.body / req.body[key]
@Query(key?: string)	req.query / req.query[key]
@Headers(name?: string)	req.headers / req.headers[name]
@Ip()	req.ip
```

## 文件命名规范

### 模块内文件

以 user 模块为例

```jsx
user.module.ts
user.controller.ts
user.service.ts
user.entity.ts     // 数据库 model, 可以存在其他 model，如 profile.entity.ts
user.constant.ts   // 常量文件
user.interface.ts  // type 和 interface
user.dto.ts        // 参数对象

user.decorator.ts  // 装饰器
user.guard.ts      // 守卫
```

## 常用代码

返回静态文件，例如 html

```typescript
  @Get('report')
  async report(@Res() res: Response) {
    res.sendFile('report.html', {
      root: path.resolve(__dirname, '..', '..', '..', 'static')
    })
  }
```

