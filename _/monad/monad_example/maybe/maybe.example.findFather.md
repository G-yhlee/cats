#### 가계도 검색 프로그램

```hs
father :: Person -> Maybe Person -- 아빠를 찾아준다.
mother :: Person -> Maybe Person -- 엄마를 찾아준다

```

#### 외할아버지 찾기

```hs
-- maternalGrandfather :: p 의( 엄마를 찾고 , 엄마가 있으면)엄마의 아빠를 찾는다.
maternalGrandfather :: Person -> Maybe Person
maternalGrandfather p =
    case mother p of -- p 의 엄마를 찾는다.
        Nothing -> Nothing -- 엄마가 없다.
        Just mom -> father mom -- 엄마가 있으면, 아빠를 찾는다
```

#### 외할아버지 찾기 - bind 함수 활용

```hs
maternalGrandfather :: Person -> Maybe Person
maternalGrandfather p = mother p >>= father -- p 를 mother 함수가 maybe 로 반환하기 때문에, return 함수가 필요없다.
maternalGrandfather p = (return p) >>= mother >>= father -- 만약 mother 함수가 maybe로 반환하지 않으면, return 으로 p를 maybe 타입으로 감싸주어야 할것이다.

-- TODO :: maybe 모나드의 >>= 스펙을 알아봐야할듯
```

#### 친할아버지, 외할아버지 찾기

```hs
bothGrandfathers :: Person -> Maybe (Person, Person)
bothGrandfathers p =
    case father p of -- p 의 검색 시작점
        Nothing -> Nothing
        Just dad ->
            case father dad of
                Nothing -> Nothing
                Just gf1 -> -- p 의 친할아버지
                    case mother p of -- p 의 검색 시작점
                        Nothing -> Nothing
                        Just mom ->
                            case father mom of
                                Nothing -> Nothing
                                Just gf2 -> -- p 의 외할아버지
                                    Just (gf1, gf2) -- 검색 완료
```

#### 친할아버지, 외할아버지 찾기 - bind 함수 활용

```hs
bothGrandfathers :: Person -> Maybe (Person, Person)
bothGrandfathers p =
   father p >>= -- p 의 검색 시작점
       (\dad -> father dad >>= -- p 의 친할아버지
           (\gf1 -> mother p >>=  -- p 의 검색 시작점
               (\mom -> father mom >>= -- p 의 외할아버지
                   (\gf2 -> return (gf1,gf2) )))) -- 검색 완료
```

#### maybe monad example \_ do 표현식

```hs
-- do 표현식
mothersPaternalGrandfather :: Sheep -> Maybe Sheep
mothersPaternalGrandfather s = do m  <- mother s
                                  gf <- father m
                                  father gf

-- >>= 표현식
mothersPaternalGrandfather s = mother s >>= (\m ->
                               father m >>= (\gf ->
                               father gf))
```
