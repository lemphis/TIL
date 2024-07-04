# Zero-Based, Half-Open Convention

## Expression

* `{ x | a <= x < b }`
* `[a, b)`
* `a <= x < b`

## Why use zero-based, half-open convention

1. index의 range를 표현할 때 half-open convention이 가장 좋음
    * range를 표현할 수 있는 방법은 아래와 같이 네 가지이다.
        1. `(a, b]`
        2. `[a, b)`
        3. `(a, b)`
        4. `[a, b]`
    * 그 중 `시작 수와 마지막 수의 차 == 집합의 크기`에 해당하는 case는 half-open case임 (1, 2번)
        1. (a, b] -> `b - a = N`
        2. [a, b) -> `b - a = N`
        3. (a, b) -> `b - a = N + 1`
        4. [a, b] -> `b - a = N - 1`
2. 집합을 붙일 때 편리함
    * `[a, k) + [k, b] + ...`
    * `[...arr.slice(0, 2), ...arr.slice(2, 4), ...]`
3. index가 시작 수를 포함하지 않는 convention은 0을 포함한 양의 정수를 표현할 때 자연수보다 작은 수(-1)를 넣어야 함
    * `(a, b]`, `(a, b)` 의 case에서 `0부터 9까지` 10개의 범위를 포함해야 한다고 가정하면 a에 `-1`이 들어가야 함
    * ex) `(a, b]` -> `for (int i = -1; i < b; ++i)`
    * ex) `(a, b)` -> `for (int i = -1; i <= b; ++i)`
4. index가 마지막 수를 포함하는 convention은 0을 포함한 양의 정수를 표현할 때 자연수보다 작은 수(-1)를 넣어야 함
    * `(a, b]`, `[a, b]` 의 case에서 공집합을 표현해야 한다고 가정하면 b에 `-1`이 들어가야 함
    * ex) `(a, b]` -> `for (int i = 0; i <= -1; ++i)`
    * ex) `[a, b]` -> `for (int i = -1; i <= -1; ++i)`
