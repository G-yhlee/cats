#### typeclass 쓰는 이유

```hs
plusOne :: Int ->  Int
plusOne a = a + 1

plusOneFloat :: Float -> Float
plusOneFloat a = a + 1

plusOnePoly :: a -> a -- 에러발생
plusOnePoly a = a + 1


plusOnePoly :: Num a => a -> a -- 타입클래스로 해결
plusOnePoly a = a + 1

```

#### Num

```hs
class Num a where
  (+) :: a -> a -> a
  (-) :: a -> a -> a
  (*) :: a -> a -> a
  negate :: a -> a
  abs :: a -> a
  signum :: a -> a
  fromInteger :: Integer -> a
```
