# JavaScript

### Reference Resources (參考資源)

* http://speakingjs.com/es5/index.html
* http://exploringjs.com/es6/index.html
* http://exploringjs.com/es2016-es2017/index.html
* https://github.com/getify/You-Dont-Know-JS
* https://github.com/getify/Functional-Light-JS

***

### Table of Contents (目錄)

* [Asynchronous Processing (非同步處理)](#asynchronous-processing-非同步處理)
  * [Promises (承諾)](#promises-承諾)
  * [Generators (產生器)](#generators-產生器)
  * [Async Functions (非同步函式)](#async-functions-非同步函式)
  * [Observables (可觀察)](#observables-可觀察)
* [Functional Programming (函式型程式設計)](#functional-programming-函式型程式設計)
  * Collection (集合)
    * [Immutable (不可變性)](#immutable-不可變性)
  * Recursion (遞迴)
    * [Tail Call Optimization (尾端呼叫優化)](#tail-call-optimization-尾端呼叫優化)
    * [Trampoline (繃跳區)](#trampoline-繃跳區)
  * [Function Composition (函式組合)](#function-composition-函式組合)
    * [Currying (柯里化)](#currying-柯里化)
    * [Reducer (減速器)](#reducer-減速器)
    * Transducer (傳感器)
  * Macro (巨集)
  * Monadic (單化)
  * Concurrent (並發)
  * Arity (元數)
  * Algebraic (代數)
  * Lenses (透鏡)
* [Data structures & Algorithms (資料結構和演算法)](#data-structures-algorithms-資料結構和演算法)
  * Heap (堆疊)
  * [Queues (佇列)](#queues-佇列)
  * Linked Lists (鏈結列表)
  * Sets (集)
  * Hash table (雜湊表)
  * Trees (樹)
  * Graphs (圖形)
  * Sorting (排序)
  * Primes (素數)
  * Searching (搜索)
  * Shuffle (洗牌)
* [Design Patterns (設計模式)](#design-patterns-設計模式)
  * [Creational (建立型)](#creational-建立型)
    * Abstract Factory (抽象工廠)
    * Builder (建造器)
    * [Factory (工廠)](#factory-工廠)
    * Prototype (原型)
    * [Singleton (單體)](#singleton-單體)
  * Structural (結構型)
    * Adapter (匹配器)
    * Bridge (橋梁)
    * Composite (組合)
    * Decorator (修飾)
    * Facade (外觀)
    * Flyweight (享元)
    * Proxy (代理)
  * Behavioral (行為型)
    * Chain of Responsibility (職責鏈)
    * Command (命令)
    * Interpreter (翻譯者)
    * Iterator (迭代器)
    * Mediator (中介者)
    * Memento (備忘錄)
    * Observer (觀察者)
    * State (狀態)
    * Strategy (策略)
    * Template (模板)
    * Visitor (遊客)
* [Regular Expressions (規則運算式)](#regular-expressions-規則運算式)
  * [Common (共用)](#common-共用)
  * General (一般)
  * Anchors (錨點)
  * Meta Sequences (後設資料佇列)
  * Quantifiers (量詞)
  * Group Constructs (群組建構)
  * Character Classes (字元符號)
  * Flags/Modifiers (旗標/修改)
  * Substitution (代換)
* [Type Annotations (型別註釋)](#type-annotations-型別註釋)
  * Types (型別)
  * Primitive (原始)
  * Generics (泛型)
  * Interfaces (介面)

***

## Asynchronous Processing (非同步處理)

### Promises (承諾)

```js
const foo = () => {
  console.log(1);

  const bar = new Promise((resolve, reject) => {
    setTimeout(() => resolve(console.log(2)), 0);
  });

  console.log(3);

  return bar;
};

foo().then(() => console.log(4));
// 1
// 3
// 2
// 4
```

Parallel (平行)

```js
Promise
  .all([p1(), p2()])
  .then(data => {
    console.log(data[0]);  // p1 結果
    console.log(data[1]);  // p2 結果
  });
```

Parallel and competition (平行且競賽)

```js
Promise
  .race([
    p1(),  // 假設 p1 為主體
    p2()  // p2 不一定要執行，通常是 p1 的超時處理
  ])
  .then(() => {
    // ...
  });
```

Error handling (錯誤處理)

```js
foo()
  .then(() => console.log(4))
  .catch(error => console.error(error));
```

Chaining (鏈接)

```js
foo()
  .then(() => console.log(4))
  .then(() => console.log(6))
  .then(() => console.log(8))
  .catch(error => console.error(error));
```

### Generators (產生器)

```js
function *foo(x) {
  let y = x * (yield);  // pause here (在這裡暫停)
  return y;
};

let it = foo(2);  // 通常會已使用 `it` 來控制產生器
it.next();  // 執行 foo 函式，但會停在 yield 的地方

let result = it.next(3);  // 執行 foo 函式，這次會從暫停的地方開始
result.value;  // 2 * 3 = 6
```

```js
const foo = {
  *bar() {
    let index = 0;
    while (true) yield index++;
  }
};

const it = foo.bar();
it.next().value;  // 0
it.next().value;  // 1
```

### Async Functions (非同步函式)

Function Declarations (函式宣告式)

```js
async function foo() {
  const result = await bar();
  console.log(result);
}
```

Function Expressions (函式表示式)

```js
const foo = async function () {
  const result = await bar();
  console.log(result);
};
```

Arrow Functions (箭頭函式)

```js
const foo = async () => {
  const result = await bar();
  console.log(result);
};
```

Method Definitions (方法定義)

```js
const thing = {
  async foo() {
    const result = await bar();
    console.log(result);
  }
};
```

Class prototype methods (類別原型方法)

```js
class Thing {
  async foo() {
    const result = await bar();
    console.log(result);
  }
}
```

Parallel (平行)

```js
const foo = async () => {
  const [result1, result2] = await Promise.all([bar(), baz()]);
  console.log(result1, result2);
};
```

```js
const pagination = async (page, row) => {
  const row = Number(row);
  const list = await List.find({}).exec();
  const _data = [];

  for (let i = 0; i < list.length / row; i++) {
    if (Number(page) === (i + 1)) {
      _data.push(List.find({}).skip(i * row).limit(row));
    }
  }

  const data = await Promise.all(_data);

  return data;
};
```

Error handling (錯誤處理)

```js
const foo = async () => {
  try {
    const result = await bar();
    console.log(result);
  } catch (error) {
    console.error(error);
  }
};
```

Returned Promises (返回承諾):

```js
const foo = async () => {
  const result = await bar();

  if (result) {
    return `Foo, ${result}`;
  } else {
    throw new Error('Problem!');
  }
};

foo()
  .then(value => console.log(value))
  .catch(error => console.error(error));
```

### Observables (可觀察)

```js
// an observer (一個觀察者)
new Observable(observer => {
    // callback method (回呼方法): next(), error(), & complete()
    setTimeout(() => observer.next('foo'), 0);
    setTimeout(() => observer.next('bar'), 1000);
    setTimeout(() => observer.next('baz'), 2000);
    setTimeout(() => observer.complete(), 3000);
  })
  .subscribe(  // 訂閱一個或多個 Observable (可觀察的物件)
    value => console.log(value),
    error => console.error(error),
    () => console.log('done')
  );
  // foo
  // bar
  // baz
  // done
```

```js
Observable.of(1, 2, 3)
  .subscribe(value => console.log(value));
  // 1
  // 2
  // 3
```

```js
const map1 = Map({ a: 1, b: 2, c: 3 });
const map2 = map1.set('b', 4);

Observable.from(map2)
  .subscribe(value => console.log(value));
  // ["a", 1]
  // ["b", 4]
  // ["c", 3]
```

## Functional Programming (函式型程式設計)

#### Immutable (不可變性)

```js
const state = { value: 0 };

const counter1 = () => state.value += 1;
const counter2 = () => state.value += 5;

counter1();  // 1
counter2();  // 6

// immutable

const counter1 = () => Object.assign({}, state, { value: state.value + 1 });
const counter2 = () => Object.assign({}, state, { value: state.value + 5 });

counter1().value;  // 1
counter2().value;  // 5

// rest parameters

const counter1 = () => ({ ...state, { value: state.value + 1 } });
const counter2 = () => ({ ...state, { value: state.value + 5 } });
```

#### Tail Call Optimization (尾端呼叫優化)

```js
const factorial = num => {
  if (num === 0) return 1;
  return num * factorial(num - 1);
};

const factorial = (num, acc = 1) => {
  if (num === 0) return acc;
  return factorial(num - 1, num * acc);
};
```

```js
const tco = func => {
  const accumulated = [];

  let value = null;
  let active = false;

  return (...arg) => {
    accumulated.push(arg);

    if (!active) {
      active = true;

      while (accumulated.length) {
        value = func.apply(this, accumulated.shift());
      }

      active = false;

      return value;
    }
  };
};

const sum = tco((x, y) => {
  if (y > 0) return sum(x + 1, y - 1)
  return x;
});

sum(1, 100000);  // 100001
```

#### Trampoline (繃跳區)

```js
const trampoline = func => {
  while (typeof func === 'function') {
    func = func();
  }

  return func;
};

const odd = n =>
  n === 0 ? false : even(n - 1);

const even = n =>
  n === 0 ? true : odd(n - 1);

odd(100000);  // Uncaught RangeError: Maximum call stack size exceeded

const odd = n =>
  () =>
    n === 0 ? false : even(n - 1);

const even = n =>
  () =>
    n === 0 ? true : odd(n - 1);

trampoline(odd(100000));  // false
```

### Function Composition (函式組合)

```js
const inc = num => num + 1;
const dbl = num => num * 2;
const sqr = num => num * num;

const pipe = (...funcs) =>
  init =>
    funcs.reduce((acc, func) => func(acc), init);

pipe(inc, dbl, sqr)(2);  // 36
// 2 + 1 = 3
// 3 * 2 = 6
// 6 * 6 = 36

[inc, dbl, sqr].reduce((acc, func) => func(acc), 2);  // 36
```

#### Currying (柯里化)

```js
const curry = f => a => b => f(a, b);
const uncurry = f => (a, b) => f(a)(b);

const add = (a, b) => a + b;
const curriedAdd = a => b => a + b;

add(1, 2);  // 3
curriedAdd(1)(2);  // 3

uncurry(curry(add))(1, 2);  // 3
curry(uncurry(curriedAdd))(1)(2);  // 3
```

#### Reducer (減速器)

```js
const sumReducer = (acc, num) => acc + num;
const multReducer = (acc, num) => acc * num;

[1, 2, 3, 4, 5].reduce(sumReducer, 0);  // 15
[1, 2, 3, 4, 5].reduce(multReducer, 1);  // 120
```

## Data structures & algorithms (資料結構和演算法)

### Queues (佇列)

佇列的原則是先進先出 (先來先服務)

```js
export class Queue {
  queueArray = [];

  constructor(item, priority) {
    this.item = item;
    this.priority = priority;
  }

  // 排隊
  enqueue(item) {
    this.queueArray.push(item);
  }

  // 離隊
  dequeue() {
    return this.queueArray.shift();
  }

  // 隊伍首項
  front() {
    return this.queueArray[0];
  }

  // 檢查是否為空佇列
  isEmpty() {
    return this.queueArray.length === 0;
  }

  // 清空佇列
  clear() {
    this.queueArray = [];
  }

  // 佇列的數量
  size() {
    return this.queueArray.length;
  }

  // 打印佇列
  print() {
    console.log(this.queueArray.toString());
  }
}

const q1 = new Queue();

q1.isEmpty();  // true

q1.enqueue('Vanilla');
q1.enqueue('Angular');
q1.enqueue('React');
q1.enqueue('Vue');

q1.print();
```

## Design patterns (設計模式)

### Creational (建立型)

#### Factory (工廠)

```js
class Product {
  constructor() {
    console.log('Product Created');
  }
}

class ConcreteProduct extends Product {
  constructor() {
    super();
    console.log('ConcreteProduct Created');
  }
}

class Creator {
  constructor() {
    console.log('Creator Created');
  }

  Factory() { }

  AnOperation() {
    console.log('Creator - AnOperation()');
    this.product = this.Factory();
    console.log(this.product instanceof ConcreteProduct);
  }
}

class ConcreteCreator extends Creator {
  constructor() {
    super();
    console.log('ConcreteCreator Created');
  }

  Factory() {
    return new ConcreteProduct();
  }
}

const Factory = () => {
  const factory = new ConcreteCreator();
  factory.AnOperation();
};

Factory();
// Creator Created
// ConcreteCreator Created
// Creator - AnOperation()
// Product Created
// ConcreteProduct Created
// true
```

#### Singleton (單體)

```js
class Singleton {
  constructor() {
    if (typeof Singleton.instance === 'object') {
      return Singleton.instance;
    }

    Singleton.instance = this;

    return this;
  }
}

const instance1 = new Singleton();
const instance2 = new Singleton();

instance1 === instance2;  // true
```

## Regular expressions (規則運算式)

### Common (共用)

(1) 匹配 a、b 或 c 字元

```js
let regex = /[abc]+/g;

regex.test('a-bb-ccc');  // true
```

比對: `a`-`bb`-`ccc`

(2) 匹配除了 a、b 或 c 之外的任何字元

```js
let regex = /[^abc]+/g;

regex.test('Anything-but-abc');  // true
```

比對: `Anything-`b`ut-`abc`

(3)

```js
let regex = /[a-z]+/g;
```

```js
let regex = /[^a-z]+/g;
```

```js
let regex = /[a-zA-Z]+/g;
```

```js
let regex = /.+/;
```

## Type Annotations (型別註釋)

```js
// @flow

let foo: boolean = true;
let bar: boolean = false;
```

```js
// @flow

let foo: number = 18;  // decimal (十進制)
```
