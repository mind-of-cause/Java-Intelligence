--
принцип Spring, согласно которому бины не создают зависимости самостоятельно, а получают их из внешних источников
```java
*Main.java*
time = bean.getTimer().getTime();
```


```java
*Timer.java*
@Component  
public class Timer {  
  
    private Long nanoTime = System.nanoTime();  
  
    public Long getTime() {  
        return nanoTime;  
    }  
}

```

```java
*AnimalsCage.java*
@Component  
public class AnimalsCage {  
  
    @Autowired  
    private Timer timer;  
  
    public Timer getTimer() {  
        return timer;  
    }  
}
```

В данном случае, `Timer` - это зависимость `AnimalsCage`, и `AnimalsCage` получает экземпляр `Timer`, когда он создается. Это увеличивает гибкость и модульность вашего кода, поскольку вы можете легко заменить `Timer` на другую реализацию без изменения кода `AnimalsCage`.

  

Кроме того, использование `getTimer().getTime();` позволяет вам получать разные значения для времени каждый раз, когда вы вызываете этот метод. Это может быть полезно, если `Timer` представляет собой сервис для отслеживания актуального времени или времени, прошедшего с какого-то момента, и вы хотите получать обновленное время при каждом вызове.