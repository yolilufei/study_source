# tsconfig.json
### allowUnreachableCode
#### 属性值
- undefined 默认值
- true
- false
#### 属性释义
允许代码块中存在永远都不会执行的代码。当设置不同值时，ts 行为如下
1. 为 true 时，**忽略**代码块中永远都不会执行的代码
2. 为 false 时，当代码块中存在永远都不会执行的代码时，**抛出类型检查错误**
3. 为 undefined 时，当代码块中存在永远都不会执行的代码时，**提出告警而不会抛出类型检查错误**

#### example
[试一试](https://www.typescriptlang.org/play?noFallthroughCasesInSwitch=false&allowUnreachableCode=false#code/GYVwdgxgLglg9mABMMAKAhgLkWEBbAIwFMAnASkQG8AoROxGYRDRAHkQAYKb7fESiUECSToA3LXoBfREQA2AZyJVJffoOFIOE3lNXqhIxAEYO26lKA)
```typescript
    // tsconfig.json
    {
        "allowUnreachableCode": false
    }
    // test.ts
    function fn(a: number) {
        if (a < 0) {
            return a;
        } else {
            return 0;
        }
        return 100; // 抛出错误：Unreachable code detected.(7027)
    }
```

### alwaysStrict
#### 属性值
- true 默认值
- false
#### 属性释义
开启[严格模式](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Strict_mode)。一般来说，现代项目生成的js文件都是默认严格模式的，因此无需过多关注此属性，除非你的项目存在非严格模式文件。

### noFallthroughCasesInSwitch
#### 属性值
- true
- false
#### 属性释义
当为 true 时，switch 块中任意**非空case子句**都必须要有**结束声明**，避免case子句执行完成后继续执行下一个case子句。为 false 则不校验。
`非空case子句`：case 子句块内容不为空，例如：
```typescript
switch(match){
    case 0: // 空子句
    case 1: // 非空子句
        console.log(...);
        ...other logic
}
```
`结束声明`: 一般在 case 子句中通过 `break` 关键字结束匹配。其余结束声明还有 `return` 和 `throw`。

#### example
[试一试](https://www.typescriptlang.org/play?noFallthroughCasesInSwitch=true#code/FAGwpgLgBAtghhAxgCygXigRgNzGAZwHcBLJZACnjIEooBvYKJqROfMKABgC5Hn-EAewB2+QeAB0IQQHNyAck5Ri+WAhRgAJvOq4BbDpl78BIsZOlz5mZaqobtuviagAjAE5g4Aaz3NW7FAAzMbMmmAAZnAAriAQoS4eXr7AAL5AA)
```typescript
let match = 1;

switch(match) {
    case 0: // error: fallThrough case in switch
        console.log('0 is matched');
    case 1:
        console.log('1 is matched');
        break;
    case 3:
    default:
        break;
}
```
