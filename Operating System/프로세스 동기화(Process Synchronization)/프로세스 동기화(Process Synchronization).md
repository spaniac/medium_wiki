# 프로세스 동기화(Process Synchronization)

# 임계 영역(Critical Section)

멀티 스레딩에서 동일한 자원을 동시에 접근하는 작업(ex. 전역변수 사용, 동일 파일에 동시 접근)을 실행하는 코드 영역을 임계 영역이라고 한다.

## 임계 영역 문제(Critical Section Problems)

프로세스들이 임계영역을 함께 사용할 수 있는 프로토콜을 설계하는 것이다.

### 임계 영역 문제의 해결을 위한 전제 조건(Requirements)

- 상호 배제(Mutual Exclusion, MutEx, 뮤텍스)
: 프로세스 P1이 임계 영역에서 실행 중이라면, 다른 프로세스들은 임계 영역에서 실행될 수 없다.
- 진행(Progress)
: 임계 영역에서 실행 중인 프로세스가 없고, 별도의 동작이 없는 프로세스들만 임계 영역 진입 후보로 포함될 수 있다.
- 한정된 대기(Bounded Waiting)
: 프로세스 P1이 임계 영역에 진입 요청 후부터 승인될 때까지 다른 프로세스들이 임계 영역에 접근하는 횟수는 제한이 있어야 한다.

## 해결책

### Lock

하드웨어 기반 해결책이다.
동시에 공유 자원에 접근하는 것을 막기 위해 임계 영역에 진입하는 프로세스는 Lock을 획득한다. Lock을 획득했던 프로세스가 임계 영역을 빠져나올 때는 Lock을 방출한다. 이렇게 임계 영역 내에 프로세스의 유무에 따라 Lock의 여부가 결정됨에 따라 Lock이 되었다면 다른 프로세스는 접근할 수 없도록 하여 동시 접근을 방지한다.

- 한계
: 다중처리기 환경에서는 시간적인 효율성 측면에서 적용할 수 없다.

### 세마포어(Semaphores)

소프트웨어 기반 해결책이다. 소프트웨어 상에서 임계 영역 문제를 해결하기 위한 동기화 도구이다.

- 종류
OS는 Counting / Binary 세마포어를 구분한다.
    - 카운팅 세마포어(Counting Semaphore)
    : 가용한 개수를 가진 자원에 대한 접근 제어용으로 사용되며, 세마포어는 그 가용한 자원의 개수로 초기화된다. 자원을 점유하면 세마포어가 감소, 해제하면 세마포어가 증가한다.
    - 이진 세마포어(Binary Semaphore)
    : MutEx 라고도 부르며, 상호 배제(Mutual Exclusion)의 약자이다. 0과 1 사이에서의 값만 가능하며, 다중 프로세스들 사이의 임계 영역 문제를 해결하기 위해 사용한다.
- 단점
    - 바쁜 대기(Busy Waiting)
    : Spin Lock이라 불리는 세마포어 초기 버전에서 임계 영역에 진입해야 하는 프로세스는 진입 코드를 계속 반복 실행해야 하며, CPU 시간을 낭비했었다. 이를 Busy Waiting이라고 부르며, 대체적으로 비효율적이다. 일반적으로는 세마포어에서 임계 영역으로 진입을 시도했지만 실패한 프로세스에 대해 Block시킨 뒤, 임계 영역이 빌 때 다시 깨우는 방식을 사용한다. 이 경우 Busy Waiting으로 인한 시간 낭비 문제가 해결된다.
    - 교착 상태(Deadlock)
    : 세마포어가 Ready Queue를 가지고 있고, 둘 이상의 프로세스가 임계 영역 진입을 무한정 기다리고 있고, 임계 영역에서 실행되는 프로세스는 진입 대기 중인 프로세스가 실행되어야만 빠져나올 수 있는 상황을 말한다.

### 모니터(Monitor)

- 고급 언어의 설계 구조물로서, 개발자의 코드를 상호 배제하게끔 만든 추상화된 데이터 형태이다.
- 공유 자원에 접근하기 위한 키 획득과 자원 사용 후 해제를 모두 처리한다. (세마포어는 직접 키 해제와 공유 자원 접근 처리가 필요하다.)