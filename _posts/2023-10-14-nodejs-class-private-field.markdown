---
layout: post
title: Node.js 기여시 알면 좋은 것들 - Class의 Private field
date: 2023-10-14 16:25:00 +0900
category: Opensource
---

안녕하세요. 코돌이입니다~  

Javascript에서 Class의 Private field 사용하는 방법을 알아 보겠습니다.  

ES6에 새로운 타입인 `Symbol`이 추가되었습니다. 이 새로운 타입은 불변(immutable)하며,

string과 같이 속성의 키값으로 사용됨으로써 메타프로그래밍 용도로 종종 사용됩니다.  

`Symbol`은 로컬과 글로벌 2가지 타입이 있습니다. 객체의 `Symbol`을 키값으로 가지는 속성은 `JSON.stringify()`의 결과로는 포함되지 않지만, `util.inspect()` 함수에서는 디폴트로 포함합니다.  

`Symbol`에 대한 보다 상세한 설명은 [여기](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Symbol)를 보시면 됩니다.

# Symbol(string)

Symbol(string)을 통해 만들어지는 `Symbol`은 호출하는 함수에서 로컬입니다. 이런 이유로 Private field를 시뮬레이트하는데 종종 사용됩니다.

```
const kField = Symbol('kField');

console.log(kField === Symbol('kField')); // false

class MyObject {
  constructor() {
    this[kField] = 'something';
  }
}

module.exports.MyObject = MyObject;
```

`Symbol`은 완전히 Private하지는 않아서 아래와 같은 방법으로 데이터를 접근할 수 있습니다.

```
for (const s of Object.getOwnPropertySymbols(obj)) {
  const desc = s.toString().replace(/Symbol\((.*)\)$/, '$1');
  if (desc === 'kField') {
    console.log(obj[s]); // 'something'
  }
}
```

하지만 로컬 `Symbol`은 `_`를 Prefix로 가지는 속성보다는 Private field를 몽키 패치 또는 접근하는 것을 어렵게 만듭니다.  

따라서 `_`를 Prefix로 가지는 속성보다는 로컬 `Symbol`을 사용하는 것이 좋습니다.

# Private instance fields

ECMA2022에서 `#`을 Prefix로 가진 속성을 통해 Private instance field를 표기할 수 있는 방법이 추가되었습니다.  

```
class ClassWithPrivateField {
  #privateField;

  constructor() {
    this.#privateField = 42;
    this.#randomField = 444; // Syntax error
  }
}

const instance = new ClassWithPrivateField();
instance.#privateField === 42; // Syntax error
```

정리하자면, private field를 표기하기 위한 방법은 아래와 같이 3가지 있습니다.  

1. `_` Prefix를 가지는 속성  

2. `Symbol`을 키값으로 가지는 속성  

3. `#` Prefix를 가지는 속성  

제가 알기로는 3번 방법과 2번 방법이 주로 사용되며, 1번 방법은 되도록이면 사용하지 않는 것이 좋습니다.

감사합니다.

# Reference

* Symbol 사용하기: [https://github.com/nodejs/node/blob/main/doc/contributing/using-symbols.md](https://github.com/nodejs/node/blob/main/doc/contributing/using-symbols.md)

* Private class(Private instance fields): [https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Classes/Private_class_fields#private_instance_fields](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Classes/Private_class_fields#private_instance_fields)