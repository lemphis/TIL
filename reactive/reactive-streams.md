# Reactive Streams

Reactive Streams의 목적은 non-blocking backpressure를 이용하여 비동기 스트림 처리의 표준을 제공하는 것이다.
> The purpose of Reactive Streams is to provide a standard for asynchronous stream processing with non-blocking backpressure.

```java
class Demo {

	public static void main(String[] args) {
		List<Integer> items = Arrays.asList(0, 1, 2, 3, 4, 5, 6, 7, 8, 9);
		ExecutorService executorService = Executors.newSingleThreadExecutor();

		Publisher<Integer> publisher = subscriber -> subscriber.onSubscribe(new Subscription() {
			private final Iterator<Integer> iterator = items.iterator();

			@Override
			public void request(long n) {
				executorService.execute(() -> {
					long now = 0;
					try {
						while (now++ < n) {
							if (iterator.hasNext()) {
								subscriber.onNext(iterator.next());
							} else {
								subscriber.onComplete();
								break;
							}
						}
					} catch (RuntimeException e) {
						subscriber.onError(e);
					}
				});
			}

			@Override
			public void cancel() {

			}
		});

		Subscriber<Integer> subscriber = new Subscriber<Integer>() {
			private Subscription subscription;

			@Override
			public void onSubscribe(Subscription subscription) {
				this.subscription = subscription;
				subscription.request(1);
			}

			@Override
			public void onNext(Integer value) {
				System.out.println(value);
				subscription.request(1);
			}

			@Override
			public void onError(Throwable t) {
				System.out.println("Error! message: " + t.getMessage());
			}

			@Override
			public void onComplete() {
				System.out.println("Complete!");
			}
		};

		publisher.subscribe(subscriber);
	}

}
```