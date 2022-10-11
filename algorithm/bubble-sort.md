# Bubble Sort

버블 정렬은 매번 연속된 두 개 인덱스를 비교하여, 정한 기준의 값을 뒤로 넘겨 정렬하는 방식  
오름차순으로 정렬하고자 할 경우, 비교시마다 큰 값이 뒤로 이동하여, 1바퀴 돌 시 가장 큰 값이 맨 뒤에 저장됨  
맨 마지막에는 비교하는 수들 중 가장 큰 값이 저장되기 때문에 (전체 배열의 크기 - 현재까지 순환한 바퀴 수) 만큼만 반복해 주면 된다

버블 정렬은 1부터 비교를 시작하여 n-1개, n-2개, ..., 1개씩 비교를 반복하며,  
선택 정렬과 같이 배열이 어떻게 되어 있든지 상관없이 전체 비교를 진행하므로 시간 복잡도는 O(n^2)이다

~~~kotlin
fun bubbleSort(arr: Array<Int>) {
    val lastIdx = arr.lastIndex
    for (i in 0 until lastIdx) {
        for (j in 1..lastIdx) {
            if (arr[j] < arr[j - 1]) {
                val temp = arr[j]
                arr[j] = arr[j - 1]
                arr[j - 1] = temp
            }
        }
    }
}
~~~

- 결과  
  5 2 6 8 4 1 3 0 7 9  
  2 5 6 4 1 3 0 7 8 9  
  2 5 4 1 3 0 6 7 8 9  
  2 4 1 3 0 5 6 7 8 9  
  2 1 3 0 4 5 6 7 8 9  
  1 2 0 3 4 5 6 7 8 9  
  1 0 2 3 4 5 6 7 8 9  
  0 1 2 3 4 5 6 7 8 9  
  0 1 2 3 4 5 6 7 8 9