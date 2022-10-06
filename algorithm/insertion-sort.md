# Insertion Sort

삽입 정렬은 현재 위치 이하의 인덱스를 가진 원소들을 비교하여 자신이 들어갈 위치를 찾아 그 위치에 삽입하는 정렬 방식  
최악의 경우(역으로 정렬되어 있을 경우)에는 n-1개, n-2개, ..., 1개씩 비교를 반복하여 시간 복잡도는 O(n^2)이다  
이미 정렬되어 있는 최상의 경우에는 한 번씩만 비교를 하기 때문에 시간 복잡도는 O(n)이다

~~~kotlin
fun insertionSort(arr: Array<Int>) {
    val lastIdx = arr.lastIndex
    for (i in 1..lastIdx) {
        val key = arr[i]
        var j = i - 1
        while (j >= 0 && key < arr[j]) {
            arr[j + 1] = arr[j]
            j--
        }
        arr[j + 1] = key
    }
}
~~~

- 결과  
  5 8 2 6 9 4 1 3 0 7  
  2 5 8 6 9 4 1 3 0 7  
  2 5 6 8 9 4 1 3 0 7  
  2 5 6 8 9 4 1 3 0 7  
  2 4 5 6 8 9 1 3 0 7  
  1 2 4 5 6 8 9 3 0 7  
  1 2 3 4 5 6 8 9 0 7  
  0 1 2 3 4 5 6 8 9 7  
  0 1 2 3 4 5 6 7 8 9
