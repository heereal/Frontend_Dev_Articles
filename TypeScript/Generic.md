# Generic

## 제네릭이란?
- Generic이란 데이터의 타입을 일반화한다(generalize)한다는 것을 의미한다. 
- 즉, 선언 시점이 아니라 **생성 시점에 타입을 명시하여 하나의 타입만이 아닌 다양한 타입을 사용**할 수 있도록 하는 기법이다.
- 한 번의 선언으로 다양한 타입에 **재사용이 가능**하다는 장점이 있다.

<br/>

## 만약에 제네릭이 없다면?
![images_edie_ko_post_f05da4ea-4856-49cf-b6a5-8ee8c7182373_image](https://github.com/heereal/Frontend_Dev_Articles/assets/117061017/197e7210-7d31-4c3f-ae83-fcf82a53f770)
- 타입을 미리 지정하면 확실한 타입체크가 이뤄질 수 있지만 항상 `number`라는 타입을 받아야 하므로 범용성이 떨어진다.
- `any`를 사용한다면 자료의 타입을 제한할 수 없을 뿐더러, 이 함수를 통해 어떤 타입의 데이터가 리턴되는지 알 수 없다.

<br/>

## 제네릭 사용 방법
### 기본적 사용 방법
![images_edie_ko_post_e3daaa93-7578-4ecf-94cb-8f026aa77e70_image](https://github.com/heereal/Frontend_Dev_Articles/assets/117061017/381891c8-c24a-4f53-860f-1988b4230ef6)
- `<T>(arg: T):T` 여기서 `<T>`는 Type의 약자로 제네릭을 선언할 때 `T`를 관용적으로 사용한다.
- 다이아몬드 연산자 안에 있는 `T`는 **타입 변수**라고 한다.
- 이제 이 `identify` 함수는 `T`라는 타입 변수를 갖게 된다. 그리고 `arg`와 `return`의 type은 `T`라는 타입 변수로 동일하다.

![images_edie_ko_post_7b0a2881-803b-427e-9e2d-c1389de4c46a_image](https://github.com/heereal/Frontend_Dev_Articles/assets/117061017/c994d80e-d872-4eaf-9492-5fe722a59ab9)
- 만약에 `arg.length`라는 코드를 추가한다면 타입 에러가 발생한다.
- `T`의 타입을 명확하게 지정하지 않았기 때문이다.

![images_edie_ko_post_f38c8dd1-ffc2-4ecb-9888-f3452023a5e5_image](https://github.com/heereal/Frontend_Dev_Articles/assets/117061017/14ee01f7-5995-4cc7-ae08-9829a60a711a)
- 만약에 인자와 return 값에 배열 형태의 `T`를 설정한다면 `identify([1, 2, 3])`과 같은 형태로 함수를 사용할 수 있다.

<br/>

### 두 개 이상의 제네릭 사용하기
![images_edie_ko_post_99cea239-52d1-4999-ba19-92926ee91dfe_image](https://github.com/heereal/Frontend_Dev_Articles/assets/117061017/7749bada-c405-4ee6-a9b9-59a92a5e0bd0)
- 두 변수의 타입이 다를 경우 두 가지의 타입 변수가 필요하다. 이 때 제네릭을 사용할 수 있다.
- 관용적으로 사용하는 `T` 다음으로 오는 알파벳을 순서대로 사용하면 된다.

<br/>

### 조건부 타입으로 Generic 사용하기
![images_edie_ko_post_5905b74a-009c-401c-b9ea-fb737be14fba_image](https://github.com/heereal/Frontend_Dev_Articles/assets/117061017/538d5f94-1209-40f0-bd9a-b6ceae8d063e)
- 특정 인터페이스 내에서 `extends`와 삼항 연산자를 이용해서 타입을 지정할 수 있다.

<br/>

## Reference
- [TypeScript | Generic 제네릭](https://velog.io/@edie_ko/TypeScript-Generic-%EC%A0%9C%EB%84%A4%EB%A6%AD-feat.-TypeScript-%EB%91%90-%EB%8B%AC%EC%B0%A8-%ED%9B%84%EA%B8%B0)
