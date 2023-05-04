# Week2 study 내용 정리 !

----------------------------

### 3) 변수 선언
- let a: number;
- let s = string;
- let b : boolean;

##### typescript 에서는 위와 같이 변수 타입 필요!
##### a 변수에는 숫자만 대입, s 변수에는 문자열만 대입, b 변수에는 true/false 값만 대입 가능!

- export {}
**이 모듈은 아무것도 export 하지 않는다는 선언. 이 선언이 필요한 이유는?**
**모듈의 명시적인 형태를 유지하기 위해서, 가독성과 유지 보수성을 향상시키는데에 도움 !**

### 4) 타입의 종류
- number : 숫자
- string: 문자열
- boolean: true/false
- any : 어떤 타입의 값이나 다 허용하는 타입, 이 타입 사용은 바람직 하지 않다.
- undefined: undefined는 값이면서 타입이기도 하다
- void: 리턴 값이 없는 함수의 타입

### 6) 함수 선언
```ts
function add( a: number, b: number) : number{
    return a+b;
}

const result : number = add(3,4);
console.log(result);

export {}
```

```ts
function add(a: number, b:number) : number{
    add 함수의 파라미터 a, b의 타입은 number
    add 함수의 리턴 타입도 number.
}
```
```ts
const res : number = add(3,4);
result 의 타입도 number 이다.
```

- 화살표 함수 문법으로 add 함수를 구현!
```ts
const add = (a: number, b: number) : number =>{
    return a+b;
}

const result: number = add(3,4);
console.log(result);

export {}
```

- add 함수를 화살표 함수 문법으로 구현
```ts
const add = (a: number, b: number) : number => a+ b;
const result: number = add(3,4);
console.log(result);

export {}
```

### 7) 타입 별칭(type alias)
```ts
type Person = { name : string, age: number};
// Person 타입을 선언, Person 타입은 객체이고 이 객체에는 name 속성과 age 속성이 존재
const p1:Person = {name: "홍길동", age: 16};
const p2 : Person = {name: "임꺽정", age: 19};
console.log(p1);
console.log(p2);

***************************
const p3 : Person = { name: "홍길동" };
// 이 경우에는 age 속성값을 부여하지 않았으므로 컴파일 에러가 발생

const p2: Person = { name: "임꺽정", age: 19, email : "lim@skhu.net" };
// Person 타입에 포함되지 않은 email 속성값을 부여했으므로 컴파일 에러가 발생

export{}
```


**Optional Property**
```ts
type Person = { name: string, age?: number, email?: string};
// 속성 이름에 ? 기호가 붙으면, 생략 가능한 속성

const p1 : Person = {name: "홍길동"};
// age, email 속성값을 부여하지 않았지만
// 이 두속성이 생략 가능한 속성이기 때문에 에러 발생 X
const p2 : Person = {name: "임꺽정" , age : 19, email : "lim@skhu.net" };

console.log(p1);
console.log(p2);

export {}
```

**readonly Property**
```ts
type Person = { readonly name: string, age: number, email: string};

const p1 : Person = {name" 홍길동", age: 16, email : "asd@naver.com"}

p1.age = 17;
p1. name = "Hone, Gil" // 컴파일 에러
console.log(p1);

// readonly 키워드를 속성 이름 앞에 붙이면
// 그 속성은 객체를 처음 생성할 때만 값을 지정 가능
// 그 이후로는 값 변경 X
// 즉, 컴파일 에러 발생!

export{}
```

**배열**
```ts
type Person = {readonly name: string, age: number};

const a : Person[] = [{name: "홍길동", age: 16}, {name: "임꺽정", age: 19}]

for (let person of a)
console.log(person);

export{}
```

**열거형**
```ts
enum Color {BLACK, RED, GREEN, BLUE, WHITE}

const color1 : Color = Color.RED:

console.log(color1);

export {}
```
- 출력 결과: 1

**타입 스크립트는 왜 쓸까???**
- 좀 더 코드를 있어보이게 쓰기 위해 !


**type과 interface 선언에서의 차이?**

- 'interface'는 'type'과 마찬가지로 객체의 타입의 이름을 지정하는 또다른 방법!

### 차이점??
**확장하는 방법**에서의 차이
```ts
interface PeopleInterface{
    name: string
    age: number
}

interface StudentInterface extends PeopleInterface{
    school: string
}

type PeopleType = {
    name: string
    age: number
}

type StudentType = PeopleType &{
    school: string
}
```

### 선언적 확장
**interface에서 할 수 있는 대부분의 기능들은 'type'에서 가능하지만, 한 가지 중요한 차이점은 'type'은 새로운 속성을 추가하기 위해서 다시 같은 이름으로 선언할 수 없지만, 'interface'는 항상 선언적 확장이 가능하다는 것!**

```ts
interface Window{
    title: string
}

interface Window{
    ts: TypeScriptAPI
}

// 같은 interface 명으로 Window를 다시 만든다면, 자동 확장!

const src = 'const a = "Hello World"
window.ts.transpileModule(src, {})
```

```ts
type Window ={
    title : string
}

type Window ={
    ts : TypeScriptAPI
}

// Error: Duplicate identifier 'Window'.
// 타입은 불가 !
```

### 성능은 type 보다 interface를 사용하는 것이 더 좋다?

** 여러 'type'혹은 'interface'를 '&' 하거나
'extends'할 때를 생각.

'interface'는 속성간 출동을 해결하기 위해 단순한 객체 타입을 만듦.

왜냐하면 interface는 객체의 타입을 만들기 위한 것,
어차피 객체만 오기 때문에 단순히 합치기만 하면 됨

그러나 타입의 경우, 재귀적으로 순회하면서 속성을 머지하는데, 이 경우에 일부 'never'가 나오면서 제대로 머지가 안될 가능성이 존재!

'interface'와는 다르게 'type은 원시 타입이 올수도 있어, 충돌이 나서 제대로 머지가 안되는 경우에는 'never'가 떨어진다.