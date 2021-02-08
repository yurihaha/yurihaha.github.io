---
layout: post
title: "타입스크립트"
date: 2021-02-04 17:39:22 +0900
categories: chapter
# image: assets/images/11.jpg
toc: true
comments: true
tag: [타입스크립트, typescript]
---

## 타입지정

- 타입스크립트는 일반 변수, 매개변수(Parameter), 객체속성(Property) 등에: Type과 같은 형태로 타입을 지정할 수 있습니다.

### Boolean

```javascript
let isBoolean: boolean;
let isDone: boolean = false;
```

### Number

```javascript
let num: number;
let integer: number = 6;
let float: number = 3.14;
let hex: number = 0xf00d; // 61453
let binary: number = 0b1010; // 10
let octal: number = 0o744; // 484
let infinity: number = Infinity;
let nan: number = NaN;
```

### 문자열: string

`'`, `""` 뿐만아니라 ES6 문자열도 지원합니다.

```javascript
let str: string;
let red: string = "Red";
let green: string = "Green";
let myColor: string = `My color ${red}`;
let yourColor: string = "Your color is" + green;
```

### 배열: Array

1. 순차적으로 값을 가지는 일반 배열을 나타냅니다. 배열은 다음과 같이 두가지 방법으로 타입선언 할 수 있다.

```javascript
let fruits: string[] = ["Apple", "Banana", "Mango"];
//또는 let fruits: Array<string>=['Apple', 'Banana', 'Mango'];

2. 숫자만 가지는 배열
let oneToSeven: number[] = [1, 2, 3, 4, 5, 6, 7];
//또는 let oneToSeven: Array<number> = [1,2,3,4,5,6,7];
```

3. 유니언 타입(다중 타입)의 '문자열과 숫자를 동시에 가지는 배열'도 선언할 수 있습니다.
   `|`를 사용하여 여러타입중 하나를 사용 할 수 있다.

```javascript
let array: (string | number)[] = ["Apple", 1, 2, "Banana", "Mango", 3];
// or
let array: Array<string | number> = ["Apple", 1, 2, "Banana", "Mango", 3];
```

4. 배열이 가지는 항목의 값을 단언할 수 없다면 any를 사용할 수 있습니다.

```javascript
let someArr: any[] = [0, 1, {}, [], "str", false];
```

5. 인터페이스나 커스텀 타입을 사용할 수도 있습니다.

```javascript
interface IUser {
  name: string;
  age: number;
  isValid: boolean;
}
let usrArr: IUser[] = [
  {
    name: "유리",
    age: 50,
    isValid: true
  },
  {
    name: "도윤",
    age: 20,
    isValid: false
  },
  {
    name: "재현",
    age: 19,
    isValid: true
  }
];
```

6. 다음과 같이 특정한 값으로 타입을 대신해 작성할 수도 있습니다. (유용하지 x)

```javascript
let array = 10[];
array= [10];
array.push(10);
array.push(11);
```

7. 읽기 전용 배열을 생성할 수도 있습니다. readonly 키워드나 ReadonlyArray 타입을 사용하면 됩니다.

```javascript
let arrA: readonly number[] = [1, 2, 3, 4];
let arrB: ReadonlyArray<number> = [0, 9, 8, 7];

arrA [0] = 123;
arrA.push(123);
arrB[0]= 123;
arrB.push(123);

```

### 튜플

- Tuple 타입은 배열과 매우 유사합니다. 차이점이라면 정해진 타입의 고정된 길이 배열을 표현합니다.

```javascript
let tuple: [string, number];
tuple = ["a", 1];
tuple = ["a", 1, 2];
tuple = [1, "a"];
```

- 다음과 같이 데이터를 개별변수로 지정하지 않고 단일 Tuple 타입으로 지정해 사용할 수 있습니다.

```javascript
// Variables
let userId: number = 1234;
let userName: string = "HEROPY";
let isValid: boolean = true;

//Tuple
let user: [number, string, boolean] = [12345, "HEROPY", true];
console.log(user[0]);
console.log(user[1]);
console.log(user[2]);
```

<hr>

- Tuple을 사용해서 2차원 배열 만들기

```javascript
let users: [number, string, boolean][];
//or
// let users: Array<[number,string,boolean];
users = [
  [1, "유리", true];
  [2, "재현", true];
  [3, "도윤", false];
]

//역시 값으로 타입을 대신할 수 있다.
let tuple: [1, number];
tuple = [1,2];
tuple = [1,3];
tuple = [2,3];

// 에러코드를 확인할 수 있다.
let tuple: [string, number];
tuple = ['a', 1];
tuple = ['a', 1, 2]; // Error - TS2322
tuple = [1, 'a']; // Error - TS2322
```

- Tuple 정해진 타입의 고정된 길이 배열을 표현하지만, 이는 할당(Assign)에 국한됩니다.
- .push()나 .spice() 등을 통해 값을 넣는 행위는 막을 수 없습니다.

```javascript
let tuple: [string, number];
tuple = ["a", 1];
tuple = ["b", 2];
tuple.push(3);
console.log(tuple);
tuple.push(true);
```

- 배열에서 사용한것과 같이 readonly 키워드를 사용해 읽기 전용 튜플을 생성할 수도 있습니다.

```javascript
let a: readonly [string, number] = ["Hello", 123];
a[0] = "World";

//열거형
enum Week {
  Sun,
  Mon,
  Tue,
  Wed,
  Thu,
  Fri,
  Sat
}
```

- 수동으로 값을 변경할 수 있으며, 값을 변경한 부분부터 다시 1씩 증가한다.
- Week 를 콘솔로 출력합니다.

```javascript
console.log(Week);
console.log(Week.Sun);
console.log(Week["Sun"]);
console.log(Week[0]);
```

- 추가로, Enum은 숫자 값 열거뿐만아니라 다음과 같이 문자열 값으로 초기화할 수 있습니다.
- 이 방법은 역방향 매핑(Reverse Mapping)을 지원하지 않으며 개별적으로 초기화해야 하는 단점이 있습니다.

```javascript
// enum 예제 타입스크립트
enum Color {
  Red = "red",
  Green = "green",
  Blue = "blue"
}
console.log(Color.Red);
console.log(Color["Green"]);
```

```javascript
//enum 예제 자바스크립트로 변환된 코드
var Color;
(function (Color) {
  Color["Red"] = "red";
  Color["Green"] = "green";
  Color["Blue"] = "blue";
})(Color || (Color = {}));
```

- 위에꺼보단 union type을 사용하는게 좋음
- enum의 내용이 트랜스파일할 때 인라인으로 확장된다는 점이 다릅니다.

```javascript
const Color = {
  Red: "red",
  Green: "green",
  Blue: "blue"
} as const;
type Color = typeof Color[keyof typeof Color]; // 'Red' | 'Green | Blue'
```

```javascript
const Color = {
  Red: "red",
  Green: "green",
  Blue: "blue"
};
```

### 모든타입: Any

- Any는 모든 타입을 의미한다. 따라서 일반적인 자바스크립트 변수와 동일하게 어떤타입의 값도 할당할 수 있다. 외부자원을 활용해 개발할때 불가피하게 타입을 단언할 수 없는 경우, 유용할 수 있다.

```javascript
let any: any = 123;
any = "Hello world";
any = {};
any = null;
```

- 다양한 값을 포함하는 배열을 나타낼 때 사용할 수도 있습니다.

```javascript
const list: any[] = [1, true, "Anything!"];
```

- 강한 타입 시스템의 장점을 유지하기 위해 Any 사용을 엄격하게 금지하려면, 컴파일 옵션 "noImplicitAny: true"를 통해 Any 사용시 에러를 발생시킬 수 있다.

### 알수없는 타입: Unknown

- Any와 같이 최상위 타입인 Unknown은 알수없는 타입을 의미합니다.
- Any와 같이 Unknown에느 어떤타입의 값도 할당할 수 있지만, Unknown을 다른 타입에는 할당할 수 없다.
- 일반적인 경우 Unknown은 타입단언이나 타입가드를 필요로 합니다. 타입 단언이나 가드에 대한 내용을 다른파트에서 정리합니다.
