# 스케줄러(Scheduler)

# 스케줄링 대상

스케줄링 대상은 모든 Queue에 존재하는 프로세스이며, 프로세스를 관리하는 큐의 종류는 다음과 같다.

1. Job Queue: 현재 시스템 내에 있는 모든 프로세스의 집합
2. Ready Queue: 현재 메모리 내에 있으면서 CPU 자원 할당을 대기하는 프로세스의 집합
3. Device Queue: Device I/O 작업을 대기하고 있는 프로세스의 집합

# 스케줄링 종류

![Scheduler%209f02de2b46384ae7b5aeed0d370e68fd/Untitled.png](Scheduler%209f02de2b46384ae7b5aeed0d370e68fd/Untitled.png)

## 장기 스케줄러(Long-term Scheduler, Job Scheduler)

메모리는 한정되어 있는데 많은 프로세스들이 한꺼번에 메모리에 올라올 경우, 대용량 메모리(일반적으로 디스크)에 임시로 저장한다. 이 pool에 저장되어 있는 프로세스 중 어떤 프로세스를 메모리에 할당하여 Ready Queue로 보낼지 결정하는 역할을 한다.

- 디스크와 메모리 사이의 스케줄링을 담당
- 프로세스에 메모리 및 각종 자원을 할당한다(Admit)
- Degree of Multiprogramming 제어: 메모리에 몇 개의 프로그램이 올라갈 것인지를 제어
- 프로세스의 상태: New → Ready (in memory)

## 단기 스케줄러(Short-term Scheduler, CPU Scheduler)

- CPU와 메모리 사이의 스케줄링을 담당
- Ready Queue에 존재하는 프로세스 중 어떤 프로세스를 Running할지 결정
- 프로세스에 CPU를 할당(Scheduler Dispatch)
- 프로세스의 상태: Ready → Running → Waiting → Ready

## 중기 스케줄러(Medium-term Scheduler, Swapper)

- 여유 메모리 공간 확보를 위해 Ready 상태인 프로세스들을 메모리에서 디스크로 이동.
- 프로세스에 할당된 메모리를 해제
- Degree of Multiprogramming 제어
- 현재 시스템에서 메모리에 너무 많은 프로그램이 동시에 올라가는 것을 조절하는 스케줄러
- 프로세스의 상태: Ready → Suspended

### Suspended(Stopped) 상태

외부적인 이유로 프로세스의 수행이 정지된 상태로 메모리에서 내려간 상태를 의미한다. 프로세스 전부 디스크로 swap out된다. Blocked 상태는 다른 I/O 작업을 기다리는 상태이기 때문에 스스로 Ready 상태로 돌아갈 수 있지만, Suspended 상태는 외부적인 이유로 중지되었기 때문에 스스로 돌아갈 수 없다.

---

# CPU 스케줄러

## 스케줄링 대상

CPU 스케줄러의 스케줄링 대상은 Ready Queue에 존재하는 프로세스들이다.

## 스케줄링 기법

### FCFS(First Come First Served)

- 특징
    - 먼저 온 프로세스를 먼저 처리하는 선입선출 방식
    - 비선점형(Non-Preemptive) 스케줄링
    : 일단 CPU를 선점하면 프로세스가 완료될 때까지 CPU를 반환하지 않는다. 할당되었던 CPU가 반환될 때만 스케줄링이 이루어진다.
- 문제점
    - Convoy Effect
    : 소요시간이 긴 프로세스가 먼저 도달하여 효율성을 낮추는 현상

### SJF(Shortest Job First)

- 특징
    - 새로운 프로세스가 도착할 때마다 새로운 스케줄링이 이루어진다.
    - 선점형(Preemptive) 스케줄링
- 문제점
    - Starvation
    : 소요시간이 긴 프로세스는 소요시간이 짧은 프로세스에게 우선순위에서 계속 밀려 영원히 처리되지 않는 현상

### SRTF(Shortest Remaining Time First)

- 특징
    - 새로운 프로세스가 도착할 때마다 새로운 스케줄링이 이루어진다.
    - 선점형 스케줄링
    : 현재 수행 중인 프로세스의 남은 burst time보다 더 짧은 burst time을 가지는 새로운 프로세스가 도착하면 CPU를 뺏긴다.
- 문제점
    - Starvation
    - 새로운 프로세스가 도달할 때마다 스케줄링을 다시 하기 때문에 CPU 사용시간을 측정할 수가 없다.

### Priority Scheduling(우선순위 스케줄링)

- 특징
    - 우선순위가 가장 높은 프로세스에게 CPU를 할당한다. 우선순위는 정수로 표현하며, 숫자가 작을 수록 우선순위가 높다.
    - 선점형 스케줄링 방식
    : 더 높은 우선순위의 프로세스가 도착하면 실행 중인 프로세스를 멈추고 CPU를 선점한다.
    - 비선점형 스케줄링 방식
    : 더 높은 우선순위의 프로세스가 도착하면 Ready Queue의 Head에 넣는다.
- 문제점
    - Starvation
    - 무기한 봉쇄(Indefinite Blocking)
    : 실행 준비는 되어있으나 우선순위가 낮아 CPU를 사용하지 못하는 프로세스를 CPU가 무한정 대기하는 상태
- 해결책
    - Aging
    : 우선순위가 낮아 처리되지 않는 프로세스의 우선순위를 점차 올려주는 방식

### Round Robin

- 특징
    - 현대적인 CPU 스케줄링
    - 각 프로세스는 동일한 크기의 할당 시간(time quantum, time slice)을 갖게 된다.
    - 할당 시간이 지나면 프로세스는 선점당하고 Ready Queue의 제일 뒤로 가서 대기한다.
    - RR은 CPU 사용시간이 랜덤한 프로세스들이 섞여 있을 경우에 효율적이다.
    - RR이 가능한 이유는 프로세스의 context를 save할 수 있기 때문이다.
- 장점
    - Response Time이 빨라진다.
    : n개의 프로세스가 Ready Queue에 있고 할당시간이 q(time quantum)인 경우, 어떤 프로세스도 (n - 1)q time unit 이상 기다리지 않는다.
    - 프로세스가 기다리는 시간이 CPU를 사용할 만큼 증가한다. → 공정한 스케줄링
- 주의할 점

설정한 time quantum이 너무 커지면 FCFS와 같아진다. 또 너무 작아지면 잦은 context switch로 오버헤드가 발생한다. 그래서 적당한 time quantum을 설정하는 것이 중요하다.