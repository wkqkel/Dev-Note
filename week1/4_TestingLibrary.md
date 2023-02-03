## 학습 키워드

- Jest
- Describe-Context-It 패턴
- React Testing Library

### Jest
Mocha와 Chai처럼 RSpec의 describe-it을 지원하고, expect로 단언(assertion)할 수 있고, Mocking도 다양한 레벨에서 쉽게 사용할 수 있다.
### [Mocking관련](https://www.youtube.com/watch?v=RoQtNLl-Wko)  
아샬님은 Mock을 굉장히 많이 씀.     
이것은 테스트를 작성할 때 모킹을 하는 테스트를 작성하는 것이 아님.  
이는 개발을 빨리 하기 위해 모킹을 많이 한단 것.
1. 모킹을 너무 많이 해서 어렵다는 것은 설계가 잘못됐을 가능성이 큼.
2. 아니면 지금 작성하는 테스트코드가 핵심 로직이 아님(UI나 애플리케이션 레이어).    
    이는 도메인 객체들한테 비즈니스로직이나 중요한 처리들을 넘기고 있지 않단 것. 

### [프론트엔드에서의 tdd](https://www.youtube.com/watch?v=-kUmsKRmOnA)
간단한 해법     
복잡하거나 자주 바뀔만한 부분은 테스트하지 않음. 
```
특정 위치의 텍스트가 있는지 확인한다 // Bad
화면 안의 텍스트 중에 제목이 있느냐 // Good 

next버튼이 클릭돼서 페이지가 넘어간다 // Bad _버튼이 변경될 수 있음
페이지 넘어가는 함수를 호출한다. // Good _헬퍼메서드를 호출
```

UI가 아닌 연결된 컨트롤러, 모델들, 서비스들을 분리해서 테스트하는 쪽으로 방향을 잡으면 훨씬 쉬움.

서비스에 물리는 http같은 것을 DI를 해주면 목킹하기 굉장히 쉬움.

테스트는 로직에 관한 걸로, 화면에 보여주는게 중요한게 아니라,       
장바구니의 수량을 변경하는, 동일 상품의 경우엔 수량을 늘려주는 것 과 같은 것을 테스트.  

관심사의 분리, 책임의 분리, 좋은 프로그램 구조

### [rspec 잘쓰고 계신가요?](https://marocchino.net/2016/12/04/about-rspec/)
BDD는 서브젝트에 대해 조건을 주고 그 결과를 확인하는 3단계로 나누어 작성하는게 특징    
describe - (context - before) - it      
describe: 사양서의 Given, 테스트할 대상 지정        
context: 사양서의 만일(When), 조건을 정의할 때 사용     
it:  it 하나에 expect하나 이상 사용하는것은 좋지않은 징후

### [Given-When-Then](https://megaptera.notion.site/Given-When-Then-a5c37e9ad60b44f28cab5a2e5d784c98)
테스트코드를 시작할 때 가장 좋은 방법 중 하나는 템플릿 사용. Given-When-Then    
약간만 시간을 내서 Given - When - Then 템플릿에 맞춰서 내가 하려는 게 뭔지 생각해보기

### [코딩을 하기 전에 해야 할 일](https://www.youtube.com/watch?v=N4FV788fNiQ)
코딩하기 전에 충분히 생각(계획)하기

1. 어떤 문제를 해결하려는지 요구사황을 명확하게 하기(엉뚱한 것을 만들 수 있음)
2. 명세(요구사항)를 좀 더 명확히(예제를 만들면서 명확하게)    
    버그란 명세대로 작동하지않는, 명세에 정의되지않는 것.       
    올바르게 동작하는 것은 명세대로 동작하는 것.    
3. 이전까지 명세를 명확히했다면, 명세를 간단히
    그리고 이러한 명세들을 테스트코드로 작성.
4. 코딩을 하면서 이건 이렇게 발전, 이 설계는 틀려먹었어 하면서 개선하고 코딩을 변경하는 작업을 반복. 
    => 리팩토링

뭐를 만들려는지 알고, 필요한 것들을 결정하고, 이루어지도록.


### [내가 한 일 증명하기](https://www.youtube.com/watch?v=wd8OmjB_eUI)
내가 만든 것이 제대로 동작하는지 증명. 내가 테스트한 케이스까지 보여줌.      
할 수 있으면 100%의 커버리지 작성. 90퍼가 되면, 어떤 것을 깨게 되면 알아채지 못함.

### [JUnit5로 계층 구조의 테스트 코드 작성하기](https://johngrib.github.io/wiki/junit5-nested/#describe---context---it-%ED%8C%A8%ED%84%B4)

Describe - (Context- before) - (It - expect) 패턴  
[BETTER SPECS](https://www.betterspecs.org/) → RSpec 베스트 프랙티스 모음. 그대로 쓸 수는 없지만, 참고하자.
```
Describe	설명할 테스트 대상을 명시한다.
Context	테스트 대상이 놓인 상황을 설명한다.
It	테스트 대상의 행동을 설명한다.

Describe	테스트 대상이 되는 클래스, 메소드 이름을 명시한다.
Context	테스트할 메소드에 입력할 파라미터를 설명한다.
It	테스트 대상 메소드가 무엇을 리턴하는지 설명한다.

// 한국어로 표현하기
Describe는 테스트 대상을 명사로 작성한다.
Context는 ~인 경우, ~할 때, 만약 ~ 하다면 과 같이 상황 또는 조건을 기술한다.
It은 위에서 명사로 작성한 테스트 대상의 행동을 작성한다.
테스트 대상의 행동은 ~이다, ~한다, ~를 갖는다가 적절한다.
~된다 같은 수동형 표현은 좋지 않다.
```
장점
테스트 코드를 계층 구조로 만들어 준다.
테스트 코드를 추가하거나 읽을 때 스코프 범위만 신경쓰면 된다.
"빠뜨린" 테스트 코드를 찾기 쉽다.
높은 테스트 커버리지가 필요한 경우 큰 도움이 된다.
재미있다. 중독성이 있다

### 이어서 읽었을 때 비문이 아닌 하나의 좋은 문장이 되도록 작성하는 것이 중요
 하나의 완전한 문장이 되는지 체크하며 작성하는 습관을 기를 필요가 있다.
```
Bad _ "toString 메소드는… 문자열이 된다" 이므로 비문이다. 즉 올바른 문장이 아니다.
"ComplexNumber 클래스의 toString 메소드는 만약 실수값만 읽고 허수값이 없다면, 실수부만 표현한 문자열이 된다"
Good
"ComplexNumber 클래스의 toString 메소드는 만약 실수값만 있고 허수값이 없다면, 실수부만 표현한 문자열을 리턴한다"

```

[이상한모임](https://www.youtube.com/watch?v=tLG0X-4xB64)
[TDD on Spring](https://www.youtube.com/watch?v=-hqiLswBiY8)


```
function add(x: number, y: number): number {
  return x + y;
};

describe("add function", () => {
  it("returns som of two numbers", () => {
    expect(add(1, 2)).toBe(3);
  });
});

test('Greeting', () => {
  render(<Greeting name="world" />);

  screen.getByText('Hello, world!');

  screen.getByText(/Hello/);

  expect(screen.queryByText(/Hi/)).not.toBeInTheDocument();
});

```

## 강의내용

Jest

Mocha와 Chai처럼 RSpec의 describe-it을 지원하고, expect로 단언(assertion)할 수 있고, Mocking도 다양한 레벨에서 쉽게 사용할 수 있다.


describe에는 주어 쓰고
it에는 행동을 묘사
context는 시츄에이션을 묘사 (if처럼 사용하는듯)

저런식으로 BDD스타일로 잡아주면 표현력이 좋아지고,
고민할 수 있게해줌. => 표현력이 좋아지니까 이러면 어떻게 될까 이러면 어떻게 될까

getByText에 문자열을 주면 정확하게 일치해야함(이걸로 엘리멑트를 찾으려하기때문에)
일부만 가고 하고싶으면 정규표현식으로 쓰면됨

npx jest --verbose
npm run watch:test -- --verbose

toBeFalsy보다 더 좋은게 not.toBeInTheDocument

React Testing Library UI testing에 특화됨 + jestdom -> matcher