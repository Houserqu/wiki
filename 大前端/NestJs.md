# Nest.js

基于Node.js 和 Typescript 的 AOP 开发框架，灵活且强大。个人开发了基于 [Nest](https://github.com/nestjs/nest) 快速启动项目 [nestjs-start](https://github.com/Houserqu/nestjs-start)，包含了项目开发常用功能模块和最佳实践。
[中文文档](https://docs.nestjs.cn/)

![Nestjs](http://qiniu.houserqu.com/Nestjs.png)

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

## 日志

### 请求ID

请求ID可以将一个请求周期内所有打印的日志都带上相同的 ID，便于问题定位
https://blog.goncharov.page/nodejs-logging-made-right

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

