# Operating System

## Signal
- signal이란?
  - 사전적인 뜻은 '신호'라는 의미로 linux에서는 process끼리 서로 통신할 때 사용
  - UNIX, UNIX 계열, POSIX 호환 운영 체제에 쓰이는 제한된 형태의 프로세스 간 통신
  - 다른 process나 동일 process 내의 특정 thread로 전달되는 비동기식 통보
  - linux에서 사용하는 signal
    - interrupt key를 사용하여 발생시키는 signal
    - process가 발생시키는 signal
    - hardware가 발생시키는 signal
    - 등등 매우 다양함
- signal in OS
  - 인간과 OS 사이에는 응용프로그램이 존재함
  - 물론 메세지로 데이터 통신을 할 수도 있겠지만 굳이 복잡한 통신이 필요하지 않다면 불필요함
  - 때문에 OS는 여러 signal을 지원하여 단순한 통신을 가능하게 하였음
- signal의 종류
    signal number | 값 | 의미 | 기본값
    |:---:|:---:|:---:|:---:
    | 1 | `SIGHUP(HUP)` | *hang up*의 약어<br /> 로그아웃과 같이 터미널에서 접속이 끊겼을 때 보내지는 signal<br />데몬 관련 환경 설정 파일을 변경시키고 변화된 내용을 적용하기 위해 재시작할 때 이 signal 사용 | 종료 |
    | 2 | `SIGINT(INT)` | *interrupt*의 약어<br /> 키보드로부터 오는 interrutpt signal로 실행을 중지시킴<br /> **CTRL + C** 입력 시에 보내지는 signal | 종료 |
    | 3 | `SIGQUIT(QUIT)` | 키보드로부터 오는 실행 중지 signal<br />**CTRL + W** 입력 시에 보내지는 signal<br />기본적으로 process를 종료시킨 뒤 코어를 덤프하는 역할 | 코어 덤프 |
    | 4 | `SIGILL(ILL)` | *illegal instruction*의 약어<br />잘못된 명령을 사용했을 때 발생 | 코어 덤프
    | 5 | `SIGTRAP(TRAP)` | trace, breakpoint에서 TRAP 발생 시 발생 | 코어 덤프 |
    | 6 | `SIGABRT(ABRT)` | *abort*의 약어<br />비정상 종료 function에 의해 발생(abort 시스템 호출하였을 때 발생) | 코어 덤프 |
    | 7 | `SIGBUS(BUS)` | memory 접근 에러시 발생하는 signal | 코어 덤프 |
    | 9 | `SIGKILL(KILL)` | process 강제 종료 | 종료 |
    | 11 | `SIGSEGV(SEGV)` | invalid memory reference | 종료 + 코어 덤프 |
    | 13 | `SIGPIPE(PIPE)` | 절단된 network socket 등에 데이터를 쓰려고 했을 때 발생 | 종료 |
    | 15 | `SIGTERM(TERM)` | *terminate*의 약어<br />정상 종료시키는 signal<br />kill 명령의 기본 signal | 종료 |
    | 17 | `SIGCHLD(CHLD)` | 자식 process가 stop되거나 종료되었을 때 부모 process에게 전달되는 signal | 무시 |
    | 18 | `SIGCONT(CONT)` | *continue*의 약어<br />SIGSTOP에 의해 정지된 process를 재실행 | 재시작 |
    | 19 | `SIGSTOP(STOP)` | 터미널에서 입력된 정지 signal<br />SIGCONT로 재실행 가능 | 중지 |
    | 20 | `SIGTSTP(TSTP)` | 실행 정지 후 다시 실행을 계속하기 위해 대기시키는 signal<br />**CTRL + Z** 입력 시에 보내지는 signal<br />SIGCONT로 재실행 가능 | 중지 |
    | 29 | `SIGIO(IO)` | 비동기 IO가 발생했을 경우 발생하는 signal(I/O not possible) | 종료 |
- example code
  - SIGINT
    ~~~c
    #include <stdio.h>
    #include <signal.h>
    #include <stdlib.h>

    void handler(int sig) {
        if (sig == SIGINT) {
            printf("Do you want to quit?");
            if (getchar() == 'y') exit(0);
        }
    }

    int main() {
        signal(SIGINT, handler);
        while(1);
    }
    ~~~
  - SIGTERM
    ~~~c
    #include <stdio.h>
    #include <signal.h>
    #include <stdlib.h>

    void handler(int sig) {
        if (sig == SIGINT) {
            printf("Do you want to quit?");
            if (getchar() == 'y') exit(0);
        }
    }

    int main() {
        int d;
        // exit을 코드로 작성하는 것보다 유저가 언제든 끌 수 있게 signal로 하는 것이 좋음
        // 두 개의 프로그램 사이에 signal로 통신할 수 있음
        // 간단하게 서로에게 신호를 줄 수 있음 (signal 자체로는 데이터를 주고 받을 수는 없음)
        signal(SIGTERM, handler);
        scanf("%d", &d);
    }
    ~~~