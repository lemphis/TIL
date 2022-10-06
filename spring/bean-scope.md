# Bean Scope

Spring Bean의 scope는 `singleton`, `prototype`이 존재함  
Spring의 내부 `ConfigurableBeanFactory`를 보면 `singleton`, `prototype` 두 가지 속성을 나타내고 있음

```java
public interface ConfigurableBeanFactory extends HierarchicalBeanFactory, SingletonBeanRegistry {

 /**
  * Scope identifier for the standard singleton scope: "singleton".
  * Custom scopes can be added via {@code registerScope}.
  * @see #registerScope
  */
 String SCOPE_SINGLETON = "singleton";

 /**
  * Scope identifier for the standard prototype scope: "prototype".
  * Custom scopes can be added via {@code registerScope}.
  * @see #registerScope
  */
 String SCOPE_PROTOTYPE = "prototype";

 ...

}
```

일반적으로 생성되는 빈들은 모두 `singleton`으로 생성됨  
즉 아래 두 개의 Bean은 동일하게 singleton으로 생성됨

```java
@Component
public class Single {}


@Component
@Scope("singleton")
public class Single {}
```

`singleton`으로 생성하게 되면 어디서나 1개의 인스턴스를 참조하여 사용함  
`prototype`은 매번 새로운 인스턴스를 생성하여 Bean의 생명주기가 필요할 때 사용함

이런 scope 특성들은 각각 사용하거나 prototype에서 singleton을 가지고 사용하는 것에는 문제가 없음  
반대로 singleton에서 prototype을 가지고 있는 경우에는 의도한 것과 다른 결과를 낼 수 있음

이미 singleton으로 생성되는 시점에 prototype이 생성되어 들어오기 때문에 singleton 내부의 prototype을 호출하게 되면 매번 같은 값을 가져오게 됨  
