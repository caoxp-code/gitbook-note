## Getting Start
#### 安装
```
yarn add -D jest
或
npm i --save-dev jest
```
#### 创建
创建xx.test.js,jest默认会查询根目录下所有的.test.js文件。使用expect断言进行测试
```
test('adds 1 + 2 to equal 3', () => {
  expect(sum(1, 2)).toBe(3);
});
```
可以直接使用命令行进行测试
```
jest my-test --notify --config=config.json

config为jest的配置文件
notify 激活测试结果通知
```
其他详细jest命令可以查看[jest命令](./cli.md)
#### 配置
> 使用命令初始化配置文件 jest --init
> 配置babel
```
yarn add -D babel-jest @babel/preset-env @babel/preset-typescript

.babelrc
{
  "presets": [
      ["@babel/preset-env", {"targets": {"browsers": ["last 3 versions", "Safari >= 8", "iOS >= 8"]}}],
      "@babel/preset-typescript"
  ]
}
```
#### 匹配断言
详细的匹配api可以查看[expect](./expect.md)
1. 简单匹配
```
test('two plus two is four', () => {
  expect(2 + 2).toBe(4);
});
```
toBe是匹配器，通过使用Object.is来测试相等，如果需要对象相等，请使用toEqual，toEqual将递归检查对象或数组的每一个字段。
2. 相反匹配
```
test('adding positive numbers is not zero', () => {
  for (let a = 1; a < 10; a++) {
    for (let b = 1; b < 10; b++) {
      expect(a + b).not.toBe(0);
    }
  }
});
```
3. undefined、null、false匹配
   > toBeNull 只匹配null

   > toBeUndefined 只匹配undefined

   > toBeDefined 与toBeUndefined相反

   > toBeTruthy 匹配任何if为真

   > toBeFalsy 匹配任何if为假

4. 数字匹配都有等价的匹配器，比较浮点数时，需要使用ToBeCloseTO，可以排除小数点误差
```
test('两个浮点数字相加', () => {
  const value = 0.1 + 0.2;
  //expect(value).toBe(0.3);           这句会报错，因为浮点数有舍入误差
  expect(value).toBeCloseTo(0.3); // 这句可以运行
});
```
5. 字符串匹配使用toMatch正则
```
test('but there is a "stop" in Christoph', () => {
  expect('Christoph').toMatch(/stop/);
});
```
6. Array和Iterables,可以使用toContain匹配
```
const shoppingList = [
  'diapers',
  'kleenex',
  'trash bags',
  'paper towels',
  'beer',
];

test('the shopping list has beer on it', () => {
  expect(shoppingList).toContain('beer');
  expect(new Set(shoppingList)).toContain('beer');
});
```
7. 异常,可以使用toThrow来剖出
```
function compileAndroidCode() {
  throw new Error('you are using the wrong JDK');
}

test('compiling android goes as expected', () => {
  expect(compileAndroidCode).toThrow();
  expect(compileAndroidCode).toThrow(Error);

  // You can also use the exact error message or a regexp
  expect(compileAndroidCode).toThrow('you are using the wrong JDK');
  expect(compileAndroidCode).toThrow(/JDK/);
});
```
#### 异步测试
1. 执行done方法，标识测试完成
```
test('the data is peanut butter', done => {
  function callback(data) {
    try {
      expect(data).toBe('peanut butter');
      done();
    } catch (error) {
      done(error);
    }
  }

  fetchData(callback);
});
```
2. promise

可以直接返回promise值，通过.then获取数据进行断言
```
test('the data is peanut butter', () => {
  return fetchData().then(data => {
    expect(data).toBe('peanut butter');
  });
});
```
可以不通过then方法，使用.resolves/.rejects来获取异步数据
```
test('the data is peanut butter', () => {
  return expect(fetchData()).resolves.toBe('peanut butter');
});
```
#### 测试准备
有时在测试前和测试后，需要做一些准备和整理工作，可以使用 
1. 多次执行的beforeEach，afterEach，其中可以使用done参数，来执行异步操作
2. 只执行一次的beforeAll, afterAll

使用describe对测试进行分组（设定作用域），jest会顺序执行describe中的代码后，再按照test进行顺序输出。
这也是需要在before和after中添加准备工作的原因
```
describe('outer', () => {
  console.log('describe outer-a');

  describe('describe inner 1', () => {
    console.log('describe inner 1');
    test('test 1', () => {
      console.log('test for describe inner 1');
      expect(true).toEqual(true);
    });
  });

  console.log('describe outer-b');

  test('test 1', () => {
    console.log('test for describe outer');
    expect(true).toEqual(true);
  });

  describe('describe inner 2', () => {
    console.log('describe inner 2');
    test('test for describe inner 2', () => {
      console.log('test for describe inner 2');
      expect(false).toEqual(false);
    });
  });

  console.log('describe outer-c');
});

// describe outer-a
// describe inner 1
// describe outer-b
// describe inner 2
// describe outer-c
// test for describe inner 1
// test for describe outer
// test for describe inner 2
```
#### mock方法 jest.fn()
```
const mockCallback = jest.fn(x => 42 + x);
forEach([0, 1], mockCallback);

// 此 mock 函数被调用了两次
expect(mockCallback.mock.calls.length).toBe(2);

// 第一次调用函数时的第一个参数是 0
expect(mockCallback.mock.calls[0][0]).toBe(0);

// 第二次调用函数时的第一个参数是 1
expect(mockCallback.mock.calls[1][0]).toBe(1);

// 第一次函数调用的返回值是 42
expect(mockCallback.mock.results[0].value).toBe(42);
```
###### .mock属性
1. .calls 调用方法信息，返回多维数组信息，表示方法调用几次，每次的参数是什么
   ```
   expect(someMockFunction.mock.calls[0][0]).toBe('first arg');
   ```
2. .results 返回结果
    ```
    expect(someMockFunction.mock.results[0].value).toBe('return value');
    ```
3. .instances 返回对象信息
   ```
   expect(someMockFunction.mock.instances[0].name).toEqual('test');
   ```
##### 插入值 mockReturnValueOnce
在测试过程中，通过链式调用可以插入不同的值
    ```
    const filterTestFn = jest.fn();

    // 插入第一次为true，第二次调用时为false
    filterTestFn.mockReturnValueOnce(true).mockReturnValueOnce(false);

    const result = [11, 12].filter(num => filterTestFn(num));

    console.log(result);
    // > [11]
    ```





