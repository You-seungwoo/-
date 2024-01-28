# 국회의원 비례대표 의석수 계산기

# 1) 개발동기
최근 뉴스기사에서 비례대표에 관한 기사를 접하게 되었는데,
이를 보고 대한민국에서 비례대표제를 통하여 국회의원을 임명하는 방식에 흥미가 생겨 조사하게 되었다.
조사 끝에 비례대표 선거 득표율에 따른 정당별 의석배분을 계산해주는 프로그램을 개발하기로 결정했다.

# 2) 프로젝트 과정
    
대한민국 현행 국회의원 비례대표제에서 의석분배에 사용되고 있는 계산법은 다음과 같다.
        
> 1. 총 투표수를 47(전체 의석수)로 나누어 기준득표수를 얻는다.
> 2. 각 정당의 득표수를 앞서 구한 기준득표수로 나눈 몫의 정수 부분 만큼의 의석을 배분한다. 또한 이를 1차 배분이라고 한다.
> 3. 배분되지 않은 의석을 배분하기 위해 앞서 구한 몫의 소수 부분이 큰 정당 별로 분배한다. 또한 이를 2차 배분이라고 한다.

위 계산법을 구현하기 위해 아래와 같이 구현했다.

- 우선, 사용자로부터 입력받을때마다 try 문을 사용하는것이 번거롭기 때문에 ask 함수를 만들어 반복적인 과정을 줄였다.
        
- 사용자로부터 정당 개수를 입력받은 후, 그 개수 만큼 이름과 득표율을 입력받는다. 그리고, 이 정보가 지정된 Calculate의 인스턴스를 가진 객체를 생성한다. (이때, 이 객체를 전역변수로 지정하기 위해 globals 함수를 이용했다.)

- Calculate 클래스에 one_cal 함수를 생성하고, one_cal 함수에 정당정보가 지정된 클래스 객체를 보내준다. one_cal 함수는 기준득표수를 입력받고, 이를 통해 기준득표수 ÷ 득표수의 몫을 리턴한다.

- 1차 배분을 위하여 앞서 받은 몫을 modf 함수를 통해 정수부분, 소수부분으로 나눈뒤, one_result 딕셔너리에 정당 이름과 정수부분을 지정한다

- 2차 배분을 위하여 앞서 받은 몫을 modf 함수를 통해 정수부분, 소수부분으로 나눈뒤, two_result 딕셔너리에 정당 이름과 소수부분을 지정한다. 또한 이를 sorted 함수를 통해 소수부분의 내림차순으로 정렬 한다.

- 배분 완료를 위해 one_result를 복사한(copy) final_result를 생성하고, 배정되지 않은 의석만큼 two_result 딕셔너리에서 소수부분이 큰 정당 순서대로 1씩 의석을 배분시켜줌으로써 의석배분이 완료된다.
