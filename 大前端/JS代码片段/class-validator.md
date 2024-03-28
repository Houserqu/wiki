```ts
/**
 * 相对时间校验
 * @param property [数量，时间单位]，时间单位参考 dayjs，例如 1 年前，[1, 'year']
 * @param validationOptions
 * @returns
 */
 const IsRelativeDate = function (property: [number, string], validationOptions?: ValidationOptions) {
  return function (object: Object, propertyName: string) {
    registerDecorator({
      name: 'IsRelativeDate',
      target: object.constructor,
      propertyName,
      constraints: [property],
      options: validationOptions,
      validator: {
        validate(value: any, args: ValidationArguments) {
          const [rule] = args.constraints;

          const minStartTime = dayjs().subtract(rule[0], rule[1])
            .valueOf();

          return value * 1 > minStartTime;
        },
      },
    });
  };
};
```

