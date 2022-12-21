#### monad 클래스 활용하여 추상화

- 모나드 클래스를 활용해서, 어떤 연산을 추상화할수 있다.
- 보통의 경우, 추상화레벨을 높이는것이 활용성측면에서 더 좋다

```hs
doSomething :: (Monad m) => a -> m b
doSomething :: a -> Maybe b

```
