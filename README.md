# jasmine-cheat-sheet

## Suite and Spec

| 名稱 | 功能說明  |
| ------| ------ |
| **describe**| 描述 **一組** 測試內容 |
| **it** | 描述 **一個** 測試項目 |

`範例一`

```alias
describe('登入頁功能', () => {

  it('應該檢核帳密輸入', () => {
    expect something...
  })

  it('若登入成功，應該跳轉到系統頁', () => {
    expect something...
  })

})
```

`範例二 (可嵌套)`

```alias
describe('登入頁功能', () => {

  it('應該檢核帳密輸入', () => {
    expect something...
  })

  describe('登入成功後', () => {

    it('應該跳轉到系統頁', () => {
      expect something...
    })

  })

})
```

`範例三 (使用 f (focus)，執行特定的 describe 與 it)`

```alias
describe('登入頁功能', () => {      // 不執行

  it('應該檢核帳密輸入', () => {     // 不執行
    expect something...
  })

})

fdescribe('登入成功後', () => {    // 執行

  it('應儲存使用者資料', () => {    // 不執行
    expect something...
  })

  fit('應該跳轉到系統頁', () => {  // 執行
    expect something...
  })

})
```

`範例三 (使用 x ，跳過特定的 describe 與 it)`

```alias
xdescribe('登入頁功能', () => {      // 不執行

  it('應該檢核帳密輸入', () => {     // 不執行
    expect something...
  })

})

describe('登入成功後', () => {    // 執行

  xit('應儲存使用者資料', () => {    // 不執行
    expect something...
  })

  it('應該跳轉到系統頁', () => {  // 執行
    expect something...
  })

})
```

`範例四 (xdescribe 遇到 fit 時)`

```alias
xdescribe('登入頁功能', () => {      // 不執行

  it('應該檢核帳密輸入', () => {     // 不執行
    expect something...
  })

})

xdescribe('登入成功後', () => {    // 因為fit的關係，所也會執行

  fit('應儲存使用者資料', () => {    // 還是會執行!
    expect something...
  })

  it('應該跳轉到系統頁', () => {  // 執行
    expect something...
  })

})
```

## Setup and Teardown

| 名稱 | 功能說明 |
| ------| ------ |
| **beforeEach**| describe 執行後，it 被執行前，執行 beforeEach |
| **afterEach** | 每個 it 執行後，執行 afterEach |
| **beforeAll**| describe 執行後，it 被執行前，調用 beforeEach (只執行一次)) |
| **afterAll** | 全部 it 執行後，調用 afterAll |

`示範`

```alias
fdescribe('示範', () => {

  beforeEach(() => {
    // do something ...
  });

  afterEach(() => {
    // do something ...
  });

  beforeAll(() => {
    // do something ...
  });

  afterAll(() => {
    // do something ...
  });

});
```

## Expect

| 名稱 | 功能說明 |
| ------| ------ |
| **expect** | 預期 參數 或 函式 執行後 為 某數值 或 某行為 |
| **expectAsync** | 同上，異步使用 (如:promise) |

`示範`

```alias
  expect(a).toBe(500); // 預期 a 應該等於 500
  expect(bFun).toHaveBeenCalled(); // 預期 b 函式 應該被呼叫
```

## Matchers

| 名稱   | 功能說明 | 範例 |
| ------| ------ | ------ |
| **not**   | 相反的預期結果 | expect(something).not.toBe(true); |
| **nothing** | 明確的知道不會有預期 | expect().nothing(); |
| **toBe** | 等於某值 (===) | expect(a).toBe(1); |
| **toEqual** | 等於某值 (深度比較) | expect(bigObject).toEqual({"foo": ['bar', 'baz']}); |
| **toBeCloseTo(expected, precision opt)** | 接近於某值 | expect(0.1 + 0.2).toBeCloseTo(0.3, 0); |
| **toBeDefined** | 已被定義 | expect(component.name).toBeDefined(); |
| **toBeUndefined** | 未被定義 | expect(component.name).toBeUndefined(); |
| **toBeNaN** | 等於 NaN | expect(thing).toBeNaN(); |
| **toBeNull** | 等於 Null | expect(thing).toBeNull(); |
| **toBeFalse** | 等於 False | expect(result).toBeFalse(); |
| **toBeTrue** | 等於 True | expect(result).toBeTrue(); |
| **toBeFalsy** | 等於 Falsy | expect(result).toBeFalsy(); |
| **toBeTruthy** | 等於 Truthy | expect(result).toBeTruthy(); |
| **toBeGreaterThan** | 大於某值 | expect(4).toBeGreaterThan(3); |
| **toBeGreaterThanOrEqual** | 大於或等於某值 | expect(4).toBeGreaterThan(4); |
| **toBeLessThan** | 小於某值 | expect(2)).toBeGreaterThan(3); |
| **toBeLessThanOrEqual** | 小於或等於某值 | expect(4).toBeGreaterThan(4); |
| **toBeInstanceOf** | 為某類別的實例 | expect('foo').toBeInstanceOf(String); |
| **toBeNegativeInfinity** |  等於 -infinity | expect(thing).toBeNegativeInfinity(); |
| **toBePositiveInfinity** | 等於 infinity | expect(thing).toBePositiveInfinity(); |
| **toContain** | 包含某特定值 | expect([{ v: 'a' }, { v: 'b' }]).toContain({ v: 'a' });  |
|   |  | expect('Hello World !!').toContain('World'); |
| **toHaveBeenCalled**  | spy 是否被呼叫過 | expect(mySpy).toHaveBeenCalled();  |
| **toHaveBeenCalledTimes**  | spy 被呼叫的次數 | expect(mySpy).toHaveBeenCalledTimes(3);  |
| **toHaveBeenCalledBefore** | 預期 aSpy 在 bSpy 調用前，已先被調用  | expect(aSpy).toHaveBeenCalledBefore(bSpy);  |
| **toHaveBeenCalledWith** | 某特定 args 至少被使用過一次  | expect(mySpy).toHaveBeenCalledWith('foo', 'bar', 2);  |
| **toHaveClass** | Dom element 包含 某 class  | expect(el).toHaveClass('bar');  |
| **toMatch** | 符合某正規化表達式  | expect("my string").toMatch(/string$/);  |
| **toThrow** | 預期丟出一個錯誤  |  expect(() => a.open(null)).toThrow('not found'); |
| **toThrowError** | 預期丟出一個 特定的錯誤類別 或 match error message  |  const a = () => { throw new TypeError('foo bar baz'); };  |
|  |   | expect(() => { a(); }).toThrowError(TypeError, 'foo bar baz'); |
|  |   | expect(() => { a(); }).toThrowError(TypeError, /bar/);  |
|  |   | expect(() => { a(); }).toThrowError(TypeError); |
|  |   | expect(() => { a(); }).toThrowError(/foo/); |
|  |   | expect(() => { a(); }).toThrowError(); |
| **toThrowMatching** | 預期丟出指定錯誤值  | expect(() => { throw new Error('nope'); }).toThrowMatching((thrown) =>  thrown.message === 'nope');  |
| **withContext** | 當 matcher fails 時，顯示的訊息 (終端機) | expect(aSpy).withContext(' a函式 應該被呼叫!!').toHaveBeenCalled();  |
| **jasmine.any** | 是否為特定 class / construct 的 instance | class Dog {}; class Cat {}; |
|  | 需搭配相關等於的matcher | const myDog = new Dog(); |
|  |  | expect(myDog).toEqual(jasmine.any(Dog));|
|  | | expect(myDog).not.toEqual(jasmine.any(Cat));|
| **jasmine.anything** | 比對 非 undefined 或 null 的值 | expect('').toEqual(jasmine.anything()); |
|  | 需搭配相關等於的matcher | expect(undefined).not.toEqual(jasmine.anything()); |
|  |  | expect(null).not.toEqual(jasmine.anything());|
| **jasmine.truthy** | 比對 為 true / truthy 的值 | expect(true).toEqual(jasmine.truthy()); |
| | 需搭配相關等於的matcher | expect({}).toEqual(jasmine.truthy()); |
| |  | expect(1).toEqual(jasmine.truthy()); |
| **jasmine.falsy** | 比對 為 false / falsy 的值 | expect(false).toEqual(jasmine.falsy()); |
| | 需搭配相關等於的matcher | expect('').toEqual(jasmine.falsy()); |
| |  | expect(0).toEqual(jasmine.falsy()); |
| **jasmine.empty** | 比對為空的值| expect('').toEqual(jasmine.empty()); |
|| 需搭配相關等於的matcher | expect({}).toEqual(jasmine.empty());|
||  | expect([]).toEqual(jasmine.empty()); |
| **jasmine.notEmpty** | 比對 非空的值 | expect('a').toEqual(jasmine.notEmpty()); |
|| 需搭配相關等於的matcher | expect({ a: '1' }).toEqual(jasmine.notEmpty()); |
||  | expect(['a']).toEqual(jasmine.notEmpty()); |
| **jasmine.arrayContaining(sample)** | 是否為包在陣列的項目 | expect([1, 2, 5, 6]).toEqual(jasmine.arrayContaining([2, 6])); |
| | 需搭配相關等於的matcher | expect([{ a: '1' }, { b: '2' }]).toEqual(jasmine.arrayContaining([{ a: '1' }])); |
| |  | expect([1, 3, 5]).not.toEqual(jasmine.arrayContaining([2])); |
| **jasmine.arrayWithExactContents(sample)** | 是否為包在陣列的全部項目(不管順序) | expect([1, 2, 3]).toEqual(jasmine.arrayWithExactContents([3, 2, 1])); |
| | 需搭配相關等於的matcher | expect([1, 2, 3]).not.toEqual(jasmine.arrayWithExactContents([1, 2])); |
| |  | expect([{ a: '1' }, { b: '2' }]).toEqual(jasmine.arrayWithExactContents([{ b: '2' }, { a: '1' }])); |
| **jasmine.mapContaining(sample)** | 是否包含在 Map 裡 的 Key/value | const map = new Map([['a', 'a1'], ['b', 'b2'], ['c', 'c3']]); |
| | 需搭配相關等於的matcher | const map2 = new Map([['b', 'b2'], ['c', 'c3']]); |
| |  | expect(map).toEqual((jasmine as any).mapContaining(map2)); |
| **jasmine.objectContaining(sample)** | 是否包含在 Object 裡 的 Key/value | const obj = { a: '1', b: '2', c: '3' }; |
| | 需搭配相關等於的matcher | const obj2 = { b: '2', c: '3' }; |
| |  | expect(obj).toEqual(jasmine.objectContaining(obj2)); |
| **jasmine.stringMatching(sample)** | 是否包含字串裡的某些文字| const str = 'hi my name is joe'; |
| | 需搭配相關等於的matcher | const str2 = 'my name'; |
| |  | expect(str).toEqual(jasmine.stringMatching(str2)); |
| **jasmine.setContaining(sample)** | 是否包含在 Set 裡 的 Key | const set = new Set([1, 2, 3, 4, 5]); |
| | 需搭配相關等於的matcher | const set2 = new Set([3, 4, 5]); |
| |  | expect(set).toEqual((jasmine as any).setContaining(set2)); |

> 需搭配相關等於的 Matcher (e.g. toEqual, toContain, toHaveBeenCalledWith)

## Spies

| 名稱   | 參數  | 用法  |
| ------| ------ |  ------ |
| **spyOn** | 原本就有obj，也有method，直接 spy obj 的 method | spyOn(obj , 'methodName') |
| **jasmine.createSpy** | 原本就有obj， 但不管有無 method，都可以幫建立一個 spy 的 method | jasmine.createSpy( baseName , originalFn )|
| **jasmine.createSpyObj** | 原本就沒有obj ，幫建立一個 obj 和 n 個 spy 的 method | jasmine.createSpyObj( ObjName , methodNames) |
| **spyOnProperty** | spy obj 的 getter 或 setter method | spyOnProperty( obj , 'propertyName' , 'get' / 'set' ) |
| **spyOnAllFunctions** | spy obj 全部的 method | spyOnAllFunctions(obj) |

`spyOn`

```alias
const car = {
  run:()=>{ do something ... }
}

spyOn( car , 'car');
```

`jasmine.createSpy`

```alias
const car = {
  run:()=>{ do something ... }
};

car.run = jasmine.createSpy();

or

const car = {};
car.run = jasmine.createSpy();
```

`jasmine.createSpyObj`

```alias
const pig = jasmine.createSpyObj('pig', [ 'run' , 'fly' ]);  

pig.run.and.callFake(()=>'go!!');
pig.fly.and.callFake(()=>'impossible!!');
```

`spyOnProperty`

```alias
const people = {
  _name: null,
  get name() {
    return this._name;
  },
  set name(name) {
    this.name = name;
  }
};

spyOnProperty(people, 'name', 'get').and.callFake(() => 'joe');
spyOnProperty(people, 'name', 'set').and.callFake((name) => console.log('do something...'));
```

`spyOnAllFunctions`

```alias
const obj = {
  say: () => console.log('hi~'),
  do: () => console.log('something...')
};

spyOnAllFunctions(obj);

obj.say();

expect(obj.say).toHaveBeenCalled();
expect(obj.do).not.toHaveBeenCalled();
```

## Spy.withArgs

| 名稱   | 功能  | 範例 |
| ------| ------ | ------ |
| **withArgs** | 可指定傳入的參數，做不同的事情 |  spyOn(obj, 'getData').withArgs('a').and.returnValue('aa'); |

`示範`

```alias
const mockData = 'bbbb';
const mockData2 = 'cccc';

const obj = {
  getData: (key) => 'aaaa'
};

spyOn(obj, 'getData')
  .withArgs('b').and.returnValue(mockData)
  .withArgs('c').and.returnValue(mockData2);

expect(obj.getData('b')).toBe(mockData);
expect(obj.getData('c')).toBe(mockData2);
```

## Spy.and

| 名稱   | 功能  | 範例 |
| ------| ------ | ------ |
| **callThrough** | 執行原本函式的程式碼 |  spyOn(obj, 'say').and.callThrough(); |
| **callFake** | 寫程式碼取代原本要執行的函式 | spyOn(obj, 'say').and.callFake((name) => console.log('My name is ' + name)); |
| **returnValue** | 直接設定函式的回傳值 | spyOn(obj, 'geUserName').and.returnValues('Joe'); |
| **returnValues** | 設定多次呼叫函式的回傳值 | spyOn(obj, 'geUserName').and.returnValues('Joe', 'Damin'); |
| **stub** | 防止去呼函式的程式碼 | spyOn(obj, 'callApi').and.stub(); |
| **throwError** | 執行函式時，丟出一個錯誤 | spyOn(obj, 'say').and.throwError(('error message')); |

> **spyOn(obj, 'say');** 與 **spyOn(obj, 'say').and.stub();** 都是去呼叫一個空函式 => function(){}  
> **and.stub()** 通常用於使用 **and.callThrough()** 後，但遇到不想呼真實函式時，就可以使用它變回預設值.

`示範`

```alias
const api = {
  getData: () => ['1']
};

spyOn(api , 'getData').and.returnValue(['100']);

expect(api.getData()).toEqual(['100']);
```

## Spy.calls

| 名稱   | 功能  | 範例 |
| ------| ------ | ------ |
| **any** | 是否被調用過 (true/false) | mySpy.calls.any(); |
| **all** | 回傳全部調用時的紀錄 (n 個 { object: '', args: '', returnValue: '' } 的陣列) | mySpy.calls.all(); |
| **allArgs** | 回傳全部調用的 args 陣列 | mySpy.calls.allArgs(); |
| **argsFor(index)** | 回傳第n次調用的args | mySpy.calls.argsFor(0); |
| **count** | 回傳被調用的次數 | mySpy.calls.count(); |
| **first** | 回傳第一次被調用時的紀錄 | mySpy.calls.first(); |
| **mostRecent** | 回傳最近被調用的紀錄 | mySpy.calls.mostRecent(); |
| **reset** | 清除所有追蹤的紀錄 | mySpy.calls.reset(); |

`示範`

```alias
const obj = {
  say: (name, position) => name + ' is a ' + position,
};

const mySpy = spyOn(obj, 'say').and.callThrough();

obj.say('Joe', 'front end engineer'); // return 'Joe is a front end engineer'
obj.say('Abel', 'backend engineer'); // return 'Abel is a backend engineer'

console.log(mySpy.calls.any()); // true

console.log(mySpy.calls.all());
// [{
//   object:{say: ...},
//   invocationOrder: 0,
//   args: ['Joe', 'front end engineer'],
//   returnValue: 'Joe is a front end engineer'
//  },
//  {
//   object:{say: ...},
//   invocationOrder: 1,
//   args: ['Abel', 'backend engineer'],
//   returnValue: 'Abel is a backend engineer'
// }]

console.log(mySpy.calls.allArgs());
// [['Joe', 'front end engineer'], ['Abel', 'backend engineer']]

console.log(mySpy.calls.argsFor(1)); // ['Abel', 'backend engineer']

console.log(mySpy.calls.count()); // 2

console.log(mySpy.calls.first());
// {
//  object:{say: function (a,b) { ... }},
//  invocationOrder: 0,
//  args: ['Joe', 'front end engineer'],
//  returnValue: 'Joe is a front end engineer'
// }

console.log(mySpy.calls.mostRecent());
// {
//  object:{say: function (a,b) { ... }},
//  invocationOrder: 0,
//  args: ['Joe', 'front end engineer'],
//  returnValue: 'Joe is a front end engineer'
// }
```

## Clock

| 名稱   | 功能  | 範例 |
| ------| ------ | ------ |
| **install** | 安裝一個 clock | jasmine.clock().install(); |
| **uninstall** | 解除一個 clock | jasmine.clock().uninstall(); |
| **tick(millis)** | 快轉一段時間 | jasmine.clock().tick(1000); |
| **mockDate** | mock 現在時間 為 某某時間 | jasmine.clock().mockDate(new Date(2019, 1, 1)); |

`示範`

```alias
describe('clock範例', () => {

  beforeEach(() => {
    jasmine.clock().install(); // 安裝一個時鐘
  });

  afterEach(() => {
    jasmine.clock().uninstall(); // 解除一個時鐘
  });

  it('示範測試異步程式碼', () => {

    let a = 0;

    setTimeout(() => {
      a = 100;
    }, 3000);

    expect(a).toBe(0);

    jasmine.clock().tick(3000); // 快轉 3s

    expect(a).toBe(100);

  });

  it('示範使用 mock date', () => {

    const startTime = new Date(2019, 1, 1);

    jasmine.clock().mockDate(startTime); // mock 當前時間為 2019/01/01 00:00:00

    console.log(new Date()); // Fri Feb 01 2019 00:00:00 GMT+0800 (台北標準時間)

    expect(new Date().getTime()).toEqual(startTime.getTime());

    jasmine.clock().tick(120000); // 快轉 2 minute

    console.log(new Date()); // Fri Feb 01 2019 00:02:00 GMT+0800 (台北標準時間)

    expect(new Date().getTime()).toEqual(startTime.getTime() + 120000);

  });

});
```

## Done

| 名稱   | 功能  | 範例 |
| ------| ------ | ------ |
| **done** | 等異步有反應後，通知執行驗證 | done() |

`示範`

```alias
it('示範測試異步程式碼', (done) => {

  let a = 0;

  setTimeout(() => {

    a = 100;

    expect(a).toBe(100);

    done(); // 等待callback後，通知驗證 (非快轉，真的等3秒)

  }, 3000);

  expect(a).toBe(0);

});
```

> 使用 **done()** 是會等 callback 時間的 ， 所以要注意 每個 spec (it) 預設等待驗證時間為 5s，超過的話，spec 還是報錯.  
> 若要 調整 spec 的 驗證時間，可以使用 **jasmine.DEFAULT_TIMEOUT_INTERVAL** 去修改 spec 等待驗證 的 時間.
