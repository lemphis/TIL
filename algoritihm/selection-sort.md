# Selection Sort

선택 정렬은 현재 위치에 들어갈 값을 찾아 정렬하는 방식  
현재 위치에 저장될 값의 크기가 작은가 큰가에 따라 최소 선택 정렬(Min-Selection Sort)와 최대 선택 정렬(Max-Selection Sort)로 구분할 수 있다  
최소 선택 정렬은 오름차순으로 정렬되고, 최대 선택 정렬은 내림차순으로 정렬됨  

이 정렬 알고리즘은 n-1개, n-2개, ... 1개씩 비교를 반복함  
배열이 어떻게 되어 있든지 간에 전체 비교를 진행하므로 시간 복잡도는 O(n^2)이다

~~~kotlin
fun selectionSort(arr: Array<Int>) {
    val lastIdx = arr.lastIndex
    for (i in 0..lastIdx) {
        var tempIdx = i
        for (j in i..lastIdx) {
            if (arr[tempIdx] > arr[j]) {
                tempIdx = j
            }
        }
        val temp = arr[tempIdx]
        arr[tempIdx] = arr[i]
        arr[i] = temp
    }
}
~~~

- 결과  
0 5 2 6 9 4 1 3 8 7  
0 1 2 6 9 4 5 3 8 7  
0 1 2 6 9 4 5 3 8 7  
0 1 2 3 9 4 5 6 8 7  
0 1 2 3 4 9 5 6 8 7  
0 1 2 3 4 5 9 6 8 7  
0 1 2 3 4 5 6 9 8 7  
0 1 2 3 4 5 6 7 8 9  
0 1 2 3 4 5 6 7 8 9  
0 1 2 3 4 5 6 7 8 9
