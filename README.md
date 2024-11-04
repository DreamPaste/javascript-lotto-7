# javascript-lotto-precourse

## 1. 과제 진행 및 프로그래밍 요구사항(공통)
- AngularJS Git Commit Message Conventions 준수
- Airbnb JS 스타일 가이드 준수, 변수명 및 클래스명 영문, 상수명 SNAKE_CASE 사용
- nvm을 통한 Node.js 20.17.0 환경에서 개발 
- App.js의 run()의 프로그램 시작점
- 파일 및 패키지 수정 금지
- 프로그램 종료시 process.exit() 금지
- indent의 depth 3 미만(2까지만 허용, 필요시 메서드 분리)
- 3항 연산자 금지
- else를 지양하고 if에서 return 권장
- 함수가 한가지 일만 하도록 작게 만듦
- 함수(또는 메서드)의 길이가 15라인을 넘어가지 않도록 구현한다.
- Jest를 사용하여 테스트 코드로 확인
- @woowacourse/mission-utils 의 [Random, Console] API 사용

    - MissionUtils.Random.pickNumberInRange() 을 사용해 랜덤한 정수 값 반환
        > `pickUniqueNumbersInRange(startInclusive, endInclusive,count)`
        
        - param : 시작범위, 끝 범위, 반환할 숫자 개수
        ```
        MissionUtils.Random.pickUniqueNumbersInRange(1, 45, 6);
        ```
    - MissionUtils.Console.readLineAsync()와 MissionUtils.Console.print() 를 사용하여 입출력 활용
        > `readLineAsync(query)`
        - 주어진 질문을 화면에 출력하고, 사용자가 입력한 답변을 Promise를 통해 반환한다.
        ```js
        async function getUsername() {
            try {
                const username = await Console.readLineAsync('닉네임을 입력해주세요.');
            } catch (error) {
        // reject 되는 경우
            }
        }
        ```
        > `print(message)`
        - 주어진 문자열을 콘솔에 출력한다.
        ```js
        Console.print('안녕하세요.');
        ```

- Lotto 클래스
    - 제공된 Lotto 클래스를 사용하여 구현해야 한다.
    - Lotto에 numbers 이외의 필드(인스턴스 변수)를 추가할 수 없다.
    - numbers의 접근 제어자인 #은 변경할 수 없다.
    - Lotto의 패키지를 변경할 수 있다.

## 2. 기능 요구사항
- 로또 번호의 숫자 범위는 1~45까지이다.

- 1개의 로또를 발행할 때 중복되지 않는 6개의 숫자를 뽑는다.

- 당첨 번호 추첨 시 중복되지 않는 숫자 6개와 보너스 번호 1개를 뽑는다.

- 당첨은 1등부터 5등까지 있다. 당첨 기준과 금액은 아래와 같다.

    >1등: 6개 번호 일치 / 2,000,000,000원

    >2등: 5개 번호 + 보너스 번호 일치 / 30,000,000원

    >3등: 5개 번호 일치 / 1,500,000원

    >4등: 4개 번호 일치 / 50,000원

    >5등: 3개 번호 일치 / 5,000원

- 로또 구입 금액을 입력하면 구입 금액에 해당하는 만큼 로또를 발행해야 한다.

- 로또 1장의 가격은 1,000원이다.

- 당첨 번호와 보너스 번호를 입력받는다.
- 사용자가 구매한 로또 번호와 당첨 번호를 비교하여 당첨 내역 및 수익률을 출력하고 로또 게임을 종료한다.

- 사용자가 잘못된 값을 입력할 경우 "[ERROR]"로 시작하는 메시지와 함께 Error를 발생시키고 해당 메시지를 출력한 다음 해당 지점부터 다시 입력을 받는다.

## 3. 입출력 요구사항

### 입력
- 로또 구입 금액을 입력 받는다. 구입 금액은 1,000원 단위로 입력 받으며 1,000원으로 나누어 떨어지지 않는 경우 예외 처리한다.

    >14000
- 당첨 번호를 입력 받는다. 번호는 쉼표(,)를 기준으로 구분한다.
    >1,2,3,4,5,6
- 보너스 번호를 입력 받는다.
    >7
### 출력
- 발행한 로또 수량 및 번호를 출력한다. 로또 번호는 오름차순으로 정렬하여 보여준다.
    ```
    8개를 구매했습니다.
    [8, 21, 23, 41, 42, 43] 
    [3, 5, 11, 16, 32, 38] 
    [7, 11, 16, 35, 36, 44] 
    [1, 8, 11, 31, 41, 42] 
    [13, 14, 16, 38, 42, 45] 
    [7, 11, 30, 40, 42, 43] 
    [2, 13, 22, 32, 38, 45] 
    [1, 3, 5, 14, 22, 45]
    ```
- 당첨 내역을 출력한다.
    ```
    3개 일치 (5,000원) - 1개
    4개 일치 (50,000원) - 0개
    5개 일치 (1,500,000원) - 0개
    5개 일치, 보너스 볼 일치 (30,000,000원) - 0개
    6개 일치 (2,000,000,000원) - 0개
    ```
- 수익률은 소수점 둘째 자리에서 반올림한다. (ex. 100.0%, 51.5%, 1,000,000.0%)
    ```
    총 수익률은 62.5%입니다.
    ```

- 예외 상황 시 에러 문구를 출력해야 한다. 단, 에러 문구는 "[ERROR]"로 시작해야 한다.
    ```
    [ERROR] 로또 번호는 1부터 45 사이의 숫자여야 합니다.
    ```
### 실행 결과 예시
```
구입금액을 입력해 주세요.
8000

8개를 구매했습니다.
[8, 21, 23, 41, 42, 43] 
[3, 5, 11, 16, 32, 38] 
[7, 11, 16, 35, 36, 44] 
[1, 8, 11, 31, 41, 42] 
[13, 14, 16, 38, 42, 45] 
[7, 11, 30, 40, 42, 43] 
[2, 13, 22, 32, 38, 45] 
[1, 3, 5, 14, 22, 45]

당첨 번호를 입력해 주세요.
1,2,3,4,5,6

보너스 번호를 입력해 주세요.
7

당첨 통계
---
3개 일치 (5,000원) - 1개
4개 일치 (50,000원) - 0개
5개 일치 (1,500,000원) - 0개
5개 일치, 보너스 볼 일치 (30,000,000원) - 0개
6개 일치 (2,000,000,000원) - 0개
총 수익률은 62.5%입니다.
```


## 구현

### 1. Lotto.js 구현
#### validate 메서드 구현
- 번호의 개수가 6개인지 확인(구현)
- 번호에 중복된 숫자가 없는지 확인
- 모든 번호가 1 이상 45 이하의 숫자인지 확인
#### Lottotest 구현
- 번호의 개수가 6개 이상
- 번호에 중복된 숫자가 존재
- 숫자가 아닌 번호가 입력됨
- 45 이상의 숫자가 입력됨

### 2. Purchase.js 구현
- money, tickets 를 가짐
- 입력받은 돈의 유효성을 검증
- 구입한 티켓 수를 출력


### 3. run()메서드 구현
#### 실행흐름
1. 구입 금액 입력 및 Purchase 객체 생성
    - 금액 검증 및 티켓 수 출력
2. 로또 발행 및 출력
3. 당첨 번호 입력 및 검증
4. 보너스 번호 입력 및 검증
5. 당첨 통계 출력
6. 수익률 출력
