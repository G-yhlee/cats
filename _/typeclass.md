```haskell
(==) :: (Eq a) => a -> a -> Bool
-- Eq 클래스의 타입인 두 a 를 받아서 , Bool 을 리턴한다

(+) :: Num a => a -> a -> a
```

#### Ord 타입

```haskell
(<) :: Ord a => a -> a -> Bool

ghci> "Abrakadabra" < "Zebra"
True
ghci> "Abrakadabra" `compare` "Zebra"
LT
ghci> 5 >= 2
True
ghci> 5 `compare` 3
GT
```

#### Show 타입

```haskell
show :: Show a => a -> String

ghci> show 3
"3"
ghci> show 5.334
"5.334"
ghci> show True
"True"
```

#### Read 타입

```haskell
read :: Read a => String -> a

ghci> read "True" || False
True
ghci> read "8.2" + 3.8
12.0
ghci> read "5" - 2
3
ghci> read "[1,2,3,4]" ++ [3]
[1,2,3,4,3]

```

#### Read 타입 어노테이션

```hs
ghci> read "5" :: Int
5
ghci> read "5" :: Float
5.0
ghci> (read "5" :: Float) * 4
20.0
ghci> read "[1,2,3,4]" :: [Int]
[1,2,3,4]
ghci> read "(3, 'a')" :: (Int, Char)
(3, 'a')
```

#### Enum

```hs
ghci> ['a'..'e']
"abcde"
ghci> [LT .. GT]
[LT,EQ,GT]
ghci> [3 .. 5]
[3,4,5]
ghci> succ 'B'
'C'
```

#### Bounded

```hs
ghci> minBound :: Int
-2147483648
ghci> maxBound :: Char
'\1114111'
ghci> maxBound :: Bool
True
ghci> minBound :: Bool
False
```

#### Num

```hs
ghci> :t 20
20 :: (Num t) => t
ghci> 20 :: Int
20
ghci> 20 :: Integer
20
ghci> 20 :: Float
20.0
ghci> 20 :: Double
20.0

```

#### :t

```hs
ghci> :t []
[] :: [a]

ghci> :t [1]
[1] :: Num a => [a]

ghci> :t [True]
[True] :: [Bool]


ghci> :t (*)
(*) :: Num a => a -> a -> a

fromIntegral (length [1,2,3,4]) + 3.2
```

#### length 는 잘 디자인 되었는가?

- length 는 length :: [a] -> Int 으로 디자인 되어있는데,
  어떤이유인지 몰라도, 이는 바보스럽다.

- (Num b) => length :: [a] -> b 로 디자인하는것이 더 좋았을듯하다
- fromIntegral 함수를 사용해서, length + 1.1 를 해보자.

```hs
fromIntegral :: (Num b, Integral a) => a -> b
ghci> fromIntegral (length [1,2,3,4]) + 1.1
5.1
```
