```typescript
// 有原数组如下
const data1 = [
  {
    a1: 'a',
    b1: 'b',
    c1: 'c'
  }
];
// 实现一个函数 transformData ，传递一个keyMap后，结果返回经过keyMap转换后的数组

const A2 = transformData(data1, { a1: 'a2' }); // 返回 [{a2: 'a'}]
const A2 = transformData(data1, { a1: 'a2',b2: 'b1' }); // 返回 [{a2: 'a', b2: 'b']

// 要求用ts完成，必须有完善类型推断，不能出现any
// a1 的值替换为 传入的 值，b

```