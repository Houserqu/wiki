# Sequelize

## 获取原始对象

Sequelize 获取的数据是封装之后对象，无法直接修改属性，需要对实例通过 get 方法

```jsx
const user = models.User.findOne() // user 是 Sequelize 封装的对象
const userValue = user.get({plain: true}) // userValue 是普通的对象
```

## 改

```jsx
User.update({name: 'newName'}, {
  where: {...}
})
```