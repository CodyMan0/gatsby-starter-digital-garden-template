
# 🚀 학습 목표


- [ ] `데이터베이스(Database)`의 개념을 이해합니다.
- [ ] `관계형 데이터베이스 (RDBMS)`가 무엇이며, 왜 사용하는지 이해합니다.
- [ ] `테이블(Table)`이 무엇인지 이해하고, `Column`, `Row`를 설명할 수 있습니다.
- [ ] 테이블(Table)의 관계 - `One to One`, `One to Many`, `Many to Many` 예시를 나열할 수 있습니다.
- [ ] `Primary Key` 와 `Foreign Key` 의 관계를 설명하고, 테이블에 지정할 수 있습니다.
- [ ] `관계형 데이터베이스`와 `비관계형 데이터베이스`의 차이를 알 수 있습니다.
- [ ]  ERD 구성도로 데이터 관계를 `모델링` 할 수 있습니다.


# 1. 데이터베이스 기본 개념

데이터베이스는 우리가 사용하는 정보의 **총 집합**이라고 할 수 있습니다. 

## 1-1. **Database 기초 이해**

`데이터베이스` 라는 개념을 오늘 처음 접하셨나요? 거창해보이지만 사실 많이 어렵지는 않습니다. 데이터베이스라는 단어는 `데이터` 라는 단어와 `베이스` 라는 단어가 합쳐져 만들어졌습니다.

데이터베이스를 다루는 회사 가운데 가장 유명한 `Oracle` 이 설명하는 데이터베이스의 개념을 한 번 소개하겠습니다. 영어로 쓰여있어 다소 어렵게 느껴질 수 있으나 친절한 설명을 접하기 전, 영어로 한 번 읽어보세요 🙌

💡A database generally refers to **a structured collection of structured information or data stored electronically in a computer system**. The database is usually controlled by a **database management system (DBMS)**. Data and DBMS are referred to as 'database systems' along with related applications, and are also collectively referred to as 'databases' for short. ([Oracle](https://www.oracle.com/kr/database/what-is-database/))

데이터베이스는 **컴퓨터 시스템에 저장된 정보나 데이터를 모두 모아 놓은 집합**을 의미한다고 생각하시면 쉽게 다가옵니다. 말 그대로 **데이터를 많이 모아놓은 베이스** 라는 뜻입니다.

실제로 데이터베이스는 아래 사진과 같이 생긴 커다란 기계에 숫자나 문자열로 이루어진 데이터들이 가득 가득 가득 가득 들어있습니다 🤣 물리적인 공간을 많이 차지하기 때문에 데이터센터는 아주 넓은 땅에 큰 건물을 지어서 안전하게 관리합니다.

![session img](https://api-media-storage.s3.amazonaws.com/session-media/e46f6c4992984cd0b5166d65a827e109?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=ASIASTLUR2MMXDFFG7PJ%2F20220723%2Fap-northeast-2%2Fs3%2Faws4_request&X-Amz-Date=20220723T102639Z&X-Amz-Expires=60&X-Amz-SignedHeaders=host&X-Amz-Security-Token=IQoJb3JpZ2luX2VjECoaDmFwLW5vcnRoZWFzdC0yIkcwRQIgd6KJ0pOshB%2Fa%2BvUv%2BMkkBTeI5pnkWUWUuz4plN6ZEsECIQDnQhqJASxDfaU%2B8XD1WWpQZfCu26hRL%2FTmR1GWo0XMnSrrAghzEAQaDDE3OTAyMjQ1MTQ4MSIMuIc%2FIhiHAyrSkVWvKsgCNeopKfEH6bRe1lqS8twmNPcHv8IgM%2BAcK49JSYoxKfCrZ1RYyQUX7l0WUGYP3RzuksKx0vwdcarzcgclBVMiyj2Zr966HjVaJ5lgN7r3chAY6KYa0wgqpVxYD3YmO3TeXKShfkJkfn%2BQ40I2iGltPBn8UbH66OdoCP7niQnec4BwX9GkybBr88SnE6zXMXZCDlo6yJxdA4vma7oUzfYnuO%2BcKF4jdmAw2wYWNMlr%2FWED0x5XpW9jrTZ01OshpLtrLDyHHpnj8%2F4v21RWKb4esPFXE%2BVSh5AubELCJL1T58iSZUDEbwwyjAg%2FeGFjG5Fyd137%2BVa4wsghXm9hvt6ePxQ8w%2BnFPX4KGSq85pvg4dC%2BtKRxA%2FV%2FQzBXYkSDersd2aOMA4XKFCeJ%2FJwTzrXNRNwRQyxhN0QMKNWR8j3clNC2%2B8ucaZTHKjDAjO%2BWBjqeAXHmoJlr6S9HjXaiEC%2F30y6kgZAxkXO5b%2BUAdcc3hN%2FRoGrdZDoGFkXt6cnn2QhFnLBwOVmdl0egMcKKy4iYZhVO4yyvpmxinPyxJ6ttSCxY%2FdnpbZvfe70b4HYON3OLkUWqcpobHFZoCN2PJubjLQJ46Vy1cRYHbTOvO9BRkAJDOSbzis94jU3pmGyR2efX3bHymVWnZpkH6XEiWlUZ&X-Amz-Signature=0b12771903092bf701cc4b3d846f2590c15c532bed3f30024e61d210c24e4407)

데이터베이스 내부에 들어있는 데이터는 어떻게 생겼는지 궁금하신가요? 모두 같은 모양은 아니지만, 보통 아래 사진과 같이 조금 딱딱한 엑셀 표, 혹은 스프레드 시트와 비슷하게 생겼답니다. 아래 예시는 영화 데이터로, 영화의 `title, release_year, length, replacement_cost`를 저장하고 있네요.

![session img](https://api-media-storage.s3.amazonaws.com/session-media/b07197e0b2114b09bc856f39588712e4?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=ASIASTLUR2MMXDFFG7PJ%2F20220723%2Fap-northeast-2%2Fs3%2Faws4_request&X-Amz-Date=20220723T102639Z&X-Amz-Expires=60&X-Amz-SignedHeaders=host&X-Amz-Security-Token=IQoJb3JpZ2luX2VjECoaDmFwLW5vcnRoZWFzdC0yIkcwRQIgd6KJ0pOshB%2Fa%2BvUv%2BMkkBTeI5pnkWUWUuz4plN6ZEsECIQDnQhqJASxDfaU%2B8XD1WWpQZfCu26hRL%2FTmR1GWo0XMnSrrAghzEAQaDDE3OTAyMjQ1MTQ4MSIMuIc%2FIhiHAyrSkVWvKsgCNeopKfEH6bRe1lqS8twmNPcHv8IgM%2BAcK49JSYoxKfCrZ1RYyQUX7l0WUGYP3RzuksKx0vwdcarzcgclBVMiyj2Zr966HjVaJ5lgN7r3chAY6KYa0wgqpVxYD3YmO3TeXKShfkJkfn%2BQ40I2iGltPBn8UbH66OdoCP7niQnec4BwX9GkybBr88SnE6zXMXZCDlo6yJxdA4vma7oUzfYnuO%2BcKF4jdmAw2wYWNMlr%2FWED0x5XpW9jrTZ01OshpLtrLDyHHpnj8%2F4v21RWKb4esPFXE%2BVSh5AubELCJL1T58iSZUDEbwwyjAg%2FeGFjG5Fyd137%2BVa4wsghXm9hvt6ePxQ8w%2BnFPX4KGSq85pvg4dC%2BtKRxA%2FV%2FQzBXYkSDersd2aOMA4XKFCeJ%2FJwTzrXNRNwRQyxhN0QMKNWR8j3clNC2%2B8ucaZTHKjDAjO%2BWBjqeAXHmoJlr6S9HjXaiEC%2F30y6kgZAxkXO5b%2BUAdcc3hN%2FRoGrdZDoGFkXt6cnn2QhFnLBwOVmdl0egMcKKy4iYZhVO4yyvpmxinPyxJ6ttSCxY%2FdnpbZvfe70b4HYON3OLkUWqcpobHFZoCN2PJubjLQJ46Vy1cRYHbTOvO9BRkAJDOSbzis94jU3pmGyR2efX3bHymVWnZpkH6XEiWlUZ&X-Amz-Signature=8fef83a8142610c141eff215537ab50c9c139c005a9a2c5f46141de757d6d885)

이러한 데이터들은 보통 `데이터베이스 관리시스템 (DBMS, Database Management System)` 으로 제어하고 관리합니다. **데이터와 데이터베이스 관리 시스템, 그리고 이와 연관된 다른 어플리케이션들을 통틀어서 데이터베이스 시스탬** 으로 일컬어지며, 더 짧게 `데이터베이스` 라고 통칭되기도 합니다. 혹, `DB` 로 아주 짧게 줄여 부르기도 합니다.

즉, 데이터베이스는 위와 같이 데이터들이 가득 모여있는 기계를 부르는 말이기도 하면서, **데이터베이스를 관리하는 시스템 자체**를 통틀어 부르는 말이기도 합니다.

## 1-2. 데이터베이스를 사용하는 이유

#이유 
> 데이터를 오랜기간 저장 및 보존하기 위해서 데이터 베이스를 사용합니다.

작은 어플리케이션에서도 물론 데이터를 잠깐동안 임시로 저장할 수는 있습니다. 그러나 우리가 저장하지 않은 데이터는 컴퓨터를 껐다 켜면 사라지죠? 메모리에 존재하는 데이터는 오래 보존이 되지 않습니다. 어플리케이션이 종료되면 메모리에 있던 데이터들은 다시는 읽어들일 수 없습니다. 따라서, 필요한 자료를 계속 보존하기 위해 데이터베이스를 사용합니다.

> 데이터를 체계적으로 **보존하고 관리**하기 위해 사용합니다.

> 데이터는 여러 서비스에 걸쳐 사용될 확률이 높은데 각 서버가 데이터를 모두 가지고 있다면 용량이 커짐


데이터베이스에는 **데이터가 아무렇게나 어질러 저장되지 않고 체계적으로 정리되어 입력됩니다.** 다시 찾고자 할 때 어렵지 않게 정보를 얻을 수 있습니다. 위 영화 데이터도 표 모양으로 깔끔하게 날짜별로 저장되어 있죠? 이렇듯 데이터를 체계적으로 정리하여 보관하기 위해 데이터베이스를 사용합니다.

## 1-3. Summary

1.  데이터베이스는 단어에서 알 수 있듯, 데이터를 많이 모아놓은 베이스입니다. **컴퓨터 시스템에 저장된 정보나 데이터를 모두 모아 놓은 집합**을 의미한다고 생각하시면 쉽게 다가옵니다.
2.  데이터베이스를 사용하는 이유는 데이터를 휘발성으로 사라지게 하지 않고, 오래 기간 저장하며, 동시에 체계적으로 보관하기 위해서입니다.

