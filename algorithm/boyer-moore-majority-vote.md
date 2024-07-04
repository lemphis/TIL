# Boyer-Moore Majority Vote Algorithm

보이어-무어 다수결 투표 알고리즘(Boyer-Moore Majority Vote Algorithm)은 배열에서 과반수(majority) 원소를 찾는 효율적인 알고리즘

- 목적
  - 배열에서 과반수(전체 원소의 절반을 초과하여 등장하는) 원소를 찾기 위함
- 시간 복잡도
  - O(n)
- 공간 복잡도
  - O(1)
- 작동 방식
    1. 후보 원소와 카운터 유지
    2. 배열을 순회하면서 카운터가 0이면 현재 원소를 후보로 선택
    3. 현재 원소가 후보와 같으면 카운터를 증가시키고, 다르면 감소시킴
    4. 순회가 끝난 후 남은 후보가 과반수 원소일 가능성이 있음
- 주의사항
  - 이 알고리즘은 과반수 원소가 존재한다는 가정 하에 작동
  - 실제 과반수 여부는 추가 확인이 필요함

```rust
fn boyer_moore_majority(nums: &[i32]) -> i32 {
    let mut major = 0;
    let mut count = 0;
    for &num in nums {
        if count == 0 {
            major = num;
        }
        count += if major == num { 1 } else { -1 }
    }
    major
}
```
