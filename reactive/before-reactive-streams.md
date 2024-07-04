# Before Reactive Streams

`Reactive Streams` 라는 표준이 나오기 전에는 아래와 같이 data를 handling
> Reactive Streams is an initiative to provide a standard for asynchronous stream processing with non-blocking back
> pressure.  
> This encompasses efforts aimed at runtime environments (JVM and JavaScript) as well as network protocols.  
> For more information, see <https://www.reactive-streams.org/>.

## Iterable

```java
class Demo {
	public static void main(String[] args) {
		Iterable<Integer> iterable = () -> new Iterator<Integer>() {
			int i = 0;
			final int MAX = 10;

			@Override
			public boolean hasNext() {
				return i < MAX;
			}

			@Override
			public Integer next() {
				return i++;
			}
		};

		for (int i : iterable) {
			System.out.println(i);
		}
	}
}
```

## Observable (Java 9부터 deprecated, Reactive Streams로 대체)

```java
class Demo {
	static class IntObservable extends Observable implements Runnable {
		@Override
		public void run() {
			for (int i = 0; i < 10; ++i) {
				setChanged();
				notifyObservers(i);
			}
		}
	}

	public static void main(String[] args) {
		Observer observer = (observable, arg) -> System.out.println(arg);
		IntObservable observable = new IntObservable();
		observable.addObserver(observer);

		observable.run();
	}
}
```

## Iterable vs Observable

|                            | Iterable |     Observable     |
|----------------------------|:--------:|:------------------:|
| 데이터 방향                     |   pull   |        push        |
| 함수 호출                      |  next()  | notifyObservers(i) |
| return 값                   |    있음    |         없음         |
| 여러 개의 Observer가 동시에 데이터 받기 |   어려움    |         쉬움         |
| multi thread 동작 제어         |   어려움    |         쉬움         |
