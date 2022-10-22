# Edge Trigger(ET) and Level Trigger(LT)

시스템에서 특정 이벤트를 감지하기 위해 trigger 라는 개념을 사용한다.  
trigger는 크게 Edge Trigger와 Level Trigger로 나눌 수 있다.

## Edge Trigger

- `상태 변수가 변하는 순간`을 기준으로 동작한다.
- 상태가 0에서 1로 변하는 순간(Rising Edge)을 검출하거나 1에서 0으로 변하는 순간(Falling Edge)을 검출할 수 있다.

## Level Trigger

- `상태 변수의 현재 상황`을 기준으로 동작한다.
- 상태가 1인 경우를 체크하기 위한 level trigger는 체크 당시 상태가 1이면 이벤트를 발생시킨다.