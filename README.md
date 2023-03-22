# 10.모듈소개 ~ 15.타입 할당 및 타입 추론하기

## 1. 모듈 소개

<aside>
📌 TypeScript가 어떤 유형을 제공하고 지원하는지, 유형들로 작업하는 방법, 유형을 할당하는 방법, 유형을 사용하면서 얻어지는 이점, 흥미로운 것들을 살펴볼 것입니다.

</aside>

## 2. Using Types

<aside>
📌 자바 스크립트가 지닌 핵심 타입부터 시작해서 어떤 타입이 지원되는지, 자바스크립트가 지니 타입과 해당 타입을 사용하는 타입스크립트의 차이점이 무엇을 의미하는지 살펴보자

</aside>

### Core Type

| number  | 1, 5.3, -10      | All numbers, no differentiation between integers or floats |
| ------- | ---------------- | ---------------------------------------------------------- |
| string  | ‘Hi’, “Hi”, `Hi` | All text values                                            |
| boolean | true, false      | Just these two, no “truthy” or “falsy” values              |

```tsx
// index.html 파일에 js파일이 script되어 있기 때문에 error가 뜬다.
// 파일의 타입을 컴파일해서 자바스크립트 파일을 내보내자
console.log("Time to get started..."); // tsc app.ts를 실행하여 새 탭을 열자.
```

### Number

```tsx
function add(n1, n2) {
  return n1 + n2;
}

const number1 = "5"; // 문자 열이기 때문에 add함수를 실행 시키면 52.8 문자열 연결하는 식으로 계산
const number2 = 2.8;

const result = add(number1, number2);
console.log(result);
```

```tsx
function add(n1: number, n2: number) {
  return n1 + n2;
}

const number1 = 5;
const number2 = 2.8;

const result = add(number1, number2);
console.log(result);
```

- 타입을 지정하더라도 위의 코드처럼 문자열로 되어있다면 에러가 출력된다.
- 브라우저에는 내장 타입스크립트 지원이 없기 때문에 런타임에서 자바스크립트가 다른 식으로 작동하도록 변경하지 않는다
- 타입스크립트 코드를 자바스크립트로 컴파일 하기 전까지 개발 도중에만 유용하겠지만 이는 추가적인 단계와 추가적인 온전성 검사를 추가하기 때문에 아주 유용하다
- 실수가 있는 경우 이를 수정할 수 있다.
- 타입스크립트는 컴파일을 차단하지 않고 이 실수에 대해 알려주며 지적한다. 절대 js파일에 관여하지 않는다.

## 3. TypeScript 타입 vs JavaScript 타입

```tsx
function add(n1: number, n2: number) {
	if (typeof n1 !== 'number' || typeof n2 !== 'number' {
		throw new Error('Incorrect input!');
		// 둘 중 하나가 숫자형이 아니라면 '잘못된 입력'이라는 새로운 에러를 발생
	}
	return n1 + n2;
}

const number1 = '5';
const number2 = 2.8;

const result = add(number1, number2);
console.log(result);
```

- 위 코드처럼 런타임에는 실패하지만 여기서 실패하는 것이 이전에 있었던 잘못된 출력이 표시되는 것보다 나을 수 있다. 따라서 이는 자바스크립트에만 해당하는 입력을 확인하는 방법이 된다
- 타입스크립트를 사용하여 개발하는 동안 피할 수 있는 것을 확인하고 있다는 단점이 있다.
- 애플리케이션에는 실행 중인 애플리케이션을 저장하기 위해 다른 동작으로 되돌아갈 수 있는 측정 기능이 내장되어 있을지도 모른다. 여전히 우리는 애초에 발생할 필요가 없는 에러를 발생시키고 있다. 이를 타입스크립트로 막을 수 있다.

### JavaScript 와 TypeScript의 차이점

- **JavaScript**
  - 자바스크립트는 동적 타입이다. 이는 즉, 나중에 문자열을 할당할 때 처음에 숫자형을 잡아둘 수 있는 변수가 있더라도 전혀 문제 없다는 것을 의미
  - 그래서 특정 타입에 의존하는 코드가 있는 경우, 런타임에서 무언가의 현재의 타입을 확인할 수 있게 해주는 typeof연산자를 사용한다
- **TypeScript**
  - 반면 타입스크립트는 정적 타입으로, 이는 즉 개발 도중에 끝나는 변수와 매개변수의 타입을 정의한다는 것을 의미
  - 런타임 중에 갑자기 변경되지는 않는다
  - 변수에 할당하는 코드를 작성하고 문자열을 할당하면 개발 도중에 에러가 발생하므로 어떤 타입을 보유할 수 있는지 여부를 명확히 할 수 밖에 없다.

### **결론**

- 타입 스크립트는 자바스크립트보다 훨씬 많은 타입을 알고 있고 런타임 검사는 타입스크립트로 수행할 수 있는 것만큼 유연하거나 강력하지 않다
- 위 코드처럼 런타임에서 타입을 가져오는 것이 유용할 수 있겠지만, 개발 도중에 가져오는 것이 훨씬 나을 때도 있다.
- 자바스크립트 엔진에 내장되어 있지 않기 때문에 타입스크립트를 사용하면 개발 도중에만 지원 받을 수 있다.
- 그래서 이 로직은 브리우저에서 실행할 수 없고, 오직 개발 도중 코드를 컴파일할 때만 실행할 수 있다

### 중요 : 타입 케이스

```tsx
타입스크립트에서는 항상 String 또는 number와 같은 타입을 다룹니다.
```

**중요: string, number등이 아니라 String 및 Number등 입니다.**

**타입스크립트의 주요 원시 타입은 모두 소문자입니다!**

## 4. 숫자 문자열 및 불리언 작업하기

```tsx
function add(n1: number, n2: number, showResult: boolean, phrase: string) {
  // if (typeof n1 !== 'number' || typeof n2 !== 'number' {
  //	throw new Error('Incorrect input!');
  // }
  const result = n1 + n2;
  // 이를 피하기위해 위 처럼 상수를 선언해주고 사용하면 버그를 피할 수 있다.
  if (showResult) {
    // console.log(phrase + n1 + n2); // 52.8
    // 두 숫자형과 결합한 문자열을 만들었기 때문에 버그가 나타난다.
    console.log(phrase + result);
  } else {
    return result;
  }
}

const number1 = 5;
const number2 = 2.8;
const printResult = true; // 타입을 지정해줘야 에러가 나지 않는다.
const resultPhrase = "Result is: ";

add(number1, number2, printResult);

console.log(result);
```

## 타입 할당 및 타입 추론하기

타입 스크립트는 result를 계산할 때 타입 추론(type inference)이라는 내장 기능을 활용하기 때문에 위 처럼 result에 타입을 배정하지 않아도 된다.

# 16. 객체 형태

IDE가 nickname이라는 속성이 해당 타입에 존재하지 않는다고 표시

| number  | 1, 5.3, -10      | All numbers, no differentiation between integers or floats               |
| ------- | ---------------- | ------------------------------------------------------------------------ |
| string  | ‘Hi’, “Hi”, `Hi` | All text values                                                          |
| boolean | true, false      | Just these two, no “truthy” or “falsy” values                            |
| object  | {age: 30}        | Any JavaScript object, more specific types (type of object) are possible |

```tsx
const person: object = {
  name: "Maximilian",
  age: 30,
};

console.log(person.name);
```

- name을 입력해도 에러가 발생 name은 이미 존재하기 때문이다.
- 여기서 타입스크립트는 어떤 정보도 주지 않는 객체가 있다고 이해하기 때문이다.
- 타입스크립트는 객체에 대한 정보가 없으므로 어떤 타입의 속성도 지원하지 않으므로 보다 구체적인 객체탕ㅂ을 지정해야함으로써 추론된 모든것을 자동으로 입력하도록 상세히 지정해야 한다.

```tsx
const person: {
  name: string;
  age: number;
} = {
  name: "Maximilian",
  age: 30,
};

console.log(person.name);
```

- 타입스크립트는 명시적으로 타입을 지정하은 것은 좋은 작업 방식이 아니다
- 타입스크립트가 객체 타입을 이해하려면 다음과 같이 입력해야 한다.

```tsx
const person {
  name: "Maximilian",
  age: 30,
};

console.log(person.name);
```

# 17. 중첩된 개체 및 타입

물론 객체 타입은 중첩 객체에 대해서도 생성할 수 있습니다.

다음과 같은 자바스크립트 객체가 있다고 가정해봅시다:

```jsx
const product = {
  id: "abc1",
  price: 12.99,
  tags: ["great-offer", "hot-and-new"],
  details: {
    title: "Red Carpet",
    description: "A great carpet - almoist brand-new!",
  },
};
```

이러한 객체의 타입은 아래와 같습니다.

```jsx
{
	id: string;
	price: number;
	tags: string[];
	details: {
		title: string;
		description: string;
	}
}
```

따라서 객체 타입안에 객체 타입이 있다고 말할 수 있습니다.

| number  | 1, 5.3, -10      | All numbers, no differentiation between integers or floats |
| ------- | ---------------- | ---------------------------------------------------------- |
| string  | ‘Hi’, “Hi”, `Hi` | All text values                                            |
| boolean | true, false      | Just these two, no “truthy” or “falsy” values              |

# 18. 배열 타입

| number  | 1, 5.3, -10      | All numbers, no differentiation between integers or floats                         |
| ------- | ---------------- | ---------------------------------------------------------------------------------- |
| string  | ‘Hi’, “Hi”, `Hi` | All text values                                                                    |
| boolean | true, false      | Just these two, no “truthy” or “falsy” values                                      |
| object  | {age: 30}        | Any JavaScript object, more specific types (type of obkject) are possible          |
| Array   | [1, 2, 3]        | Any JavaScript array, type can be flexible or strict (regarding the element types) |

```tsx
const person = {
  name: "Maximilian",
  age: 30,
  hobbies: ["Sports", "Cooking"],
};

let favoriteActivities: string[];
favoriteActivities = ["Sports", 1];
```

- Sports을 배열로 감싸면 이낸 배열이 되므로 에러가 발생하지 않는다.
- 숫자를 추가해서 문자열과 숫자를 지닌 배열을 만들었을 때는 에러가 발생
- any타입을 쓰면 혼합된 배열을 사용할 수 있다.
- 배열은 객체와 객체가 지닌 속성과 같이 타입스크립트의 타입 추론이 얼마나 역동적인지 알려주기 좋은 예이다.

```tsx
const person = {
  name: "Maximilian",
  age: 30,
  hobbies: ["Sports", "Cooking"],
};

let favoriteActivities: string[];
favoriteActivities = ["Sports"];

console.log(person.name);

for (const hobby of person.hobbies) {
  console.log(hobby);
}
```

- 위 코드를 컴파일하면 Sprots, Cooking이 for문을 통해 순차적으로 나오는 것을 알 수 있다.

```tsx
const person = {
  name: "Maximilian",
  age: 30,
  hobbies: ["Sports", "Cooking"],
};

let favoriteActivities: string[];
favoriteActivities = ["Sports"];

console.log(person.name);

for (const hobby of person.hobbies) {
  console.log(hobby.toUpperCase());
  //
}
```

- toUpperCase() 메소드를 써도 자동완성도 작동하고 타입스크립트 에러도 발생하지 않음
- 타입스크립트가 hobbies가 이를 문자열의 배열 타입이라고 이해하기 때문이다

# 19. 튜플 작업하기

| number  | 1, 5.3, -10      | All numbers, no differentiation between integers or floats                         |
| ------- | ---------------- | ---------------------------------------------------------------------------------- |
| string  | ‘Hi’, “Hi”, `Hi` | All text values                                                                    |
| boolean | true, false      | Just these two, no “truthy” or “falsy” values                                      |
| object  | {age: 30}        | Any JavaScript object, more specific types (type of obkject) are possible          |
| Array   | [1, 2, 3]        | Any JavaScript array, type can be flexible or strict (regarding the element types) |
| Tuple   | [1, 2]           | Added by TypeScript: Fixed-length array and Type                                   |

```tsx
const person = {
  name: "Maximilian",
  age: 30,
  hobbies: ["Sports", "Cooking"],
  role: [2, "author"],
};

person.role.push("admin");
person.role[1] = 10;
```

- 2개의 요소 중 첫 번째는 요소는 숫자, 두 번째 요소는 문자열이어야 한다는걸 타입스크립트는 알지 못한다.
- 이때 튜플을 사용하면 좋다. 어떤 role이어야 하는지 role의 타입을 명시적으로 설정함으로써 타입스크립트에게 인식을 시켜야한다.

```tsx
const person: {
  name: string;
  age: number;
  hobbies: string[];
  role: [number, string];
} = {
  name: "Maximilian",
  age: 30,
  hobbies: ["Sports", "Cooking"],
  role: [2, "author"],
};

person.role.push("admin");
person.role[1] = 10; // 배열[1]은 문자열이기 떄문에 error가 뜬다.

person.role = [0, "admin", "user"]; // 인덱스[2]에는 타입이 정해지지 않아 error가 뜬다. 길이도 고정된다.
```

- push가 이루어지는 이유는 role에는 정확히 두 개의 요소만 있어야 한다는 게 성립이 됐기 때문이다.
- push는 예외적으로 튜플에서 허용되기에 안타깝게도 타입스크립트가 이런 에러를 걸러내질 못하지만 적어도 잘못된 값을 할당하지는 않는다.
- 배열에 정확히 x개의 값이 필요하고 각 값의 타입을 미리 알고 있는 상황에서는 배열보다는 튜플을 사용하여 작업 중인 데이터 타입과 알고 있는 상황에서는 배열보다는 튜플을 사용하여 작업 중인 데이터 타입과 예상되는 데이터 타입을 보다 명확하게 파악할 수 있다.

# 20. 열거형으로 작업하기

<aside>
📌 Enum이란 숫자로 표혀

</aside>

| number  | 1, 5.3, -10      | All numbers, no differentiation between integers or floats                         |
| ------- | ---------------- | ---------------------------------------------------------------------------------- |
| string  | ‘Hi’, “Hi”, `Hi` | All text values                                                                    |
| boolean | true, false      | Just these two, no “truthy” or “falsy” values                                      |
| object  | {age: 30}        | Any JavaScript object, more specific types (type of obkject) are possible          |
| Array   | [1, 2, 3]        | Any JavaScript array, type can be flexible or strict (regarding the element types) |
| Tuple   | [1, 2]           | Added by TypeScript: Fixed-length array and Type                                   |
| Enum    | enum {NEW, OLD}  | Added by TypeScript: Automatically enumerated global constant identifiers          |

- Enum 라벨들은 0부터 시작하는 숫자로 변환된다.

```tsx
const ADMIN = 0;
const READ_ONLY = 1;
const AUTHOR = 2;
// 자바스크립트 경우 보통 전역 상수를 정의해서 관리한다.

const person = {
  name: "Maximilian",
  age: 30,
  hobbies: ["Sports", "Cooking"],
  role: ADMIN,
};

if (person.role === ADMIN) {
  console.log("is read only");
}
```

- enum 키워드로 enum을 생성하는데 키워드를 대문자로 시작하는 Role로 지정한다.
- enum은 사용자 지정 타입이기 때문에 중괄호 쌍과 쌍반점을 입력한다.

```tsx
enum Role {
  ADMIN,
  READ_ONLY,
  AUTHOR,
}

const person = {
  name: "Maximilian",
  age: 30,
  hobbies: ["Sports", "Cooking"],
  role: Role.ADMIN,
};

if (person.role === Role.ADMIN) {
  console.log("is read only");
}
```

- enum의 경우, 기본 동작에 국한되지 않는다. 특정 이유로 시작 숫자를 0으로 시작하지 않으려는 경우, 식별자에 등호를 추가하여 다른 숫자를 입력할 수 있다.

```tsx
enum Role {
  ADMIN = "ADMIN",
  READ_ONLY = 100,
  AUTHOR = 500,
}

const person = {
  name: "Maximilian",
  age: 30,
  hobbies: ["Sports", "Cooking"],
  role: Role.ADMIN,
};

if (person.role === Role.ADMIN) {
  console.log("is read only");
}
```

- 기본값은 0 이지만 숫자를 지정할 수 있고 첫번 째 숫자만 지정한 경우 다음 값부터 증가하는 숫자를 가질 수 있다.
- 또한 고유한 숫자와, 문자도 가능하다.

# 21. Any 타입

<aside>
📌 Any 타입은 타입스크립트에서 할당할 수 있는 타입 중 가장 유연한 타입이다. 이 타입은 타입스크립트에 어떤 것도 이해시키지 않는다. 따라서 모든 종류의 값을 저장할 수 있다.

</aside>

| number  | 1, 5.3, -10      | All numbers, no differentiation between integers or floats                         |
| ------- | ---------------- | ---------------------------------------------------------------------------------- |
| string  | ‘Hi’, “Hi”, `Hi` | All text values                                                                    |
| boolean | true, false      | Just these two, no “truthy” or “falsy” values                                      |
| object  | {age: 30}        | Any JavaScript object, more specific types (type of obkject) are possible          |
| Array   | [1, 2, 3]        | Any JavaScript array, type can be flexible or strict (regarding the element types) |
| Tuple   | [1, 2]           | Added by TypeScript: Fixed-length array and Type                                   |
| Enum    | enum {NEW, OLD}  | Added by TypeScript: Automatically enumerated global constant identifiers          |
| Any     | \*               | Any kind of value, no specific type assignment                                     |

- any는 아주 유연하고 훌륭한 타입 같지만 큰 단점 때문에 가능한 한 any를 쓰지 않는게 좋다.
- 이는 타입스크립트가 주는 모든 장점을 any가 상쇄시켜 바닐라 자바스크립트를 쓰는 것과 다를 바 없게 되기 때문이다.
- any 타입을 사용하는 모든 위치에서는 타입스크립트 컴파일러가 작동을 하지않게 되기 때문에 어떤 값이나 종류의 데이터가 어디에 저장될지 전혀 알 수 없는 경우에 대비하거나 런타임 검사를 수행하는 경우 특정 값에 수행하고자 하는 작업의 범위를 좁히기 위해 any를 사용하면 된다.
