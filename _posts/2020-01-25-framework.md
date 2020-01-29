---
title: "[SPRING] Framework"
categories: SPRING
date: 2020-01-25
---

# [Spring Framework]
Spring은 Framework이다. Framework란 무엇일까?

## Library, API, Framework
Library, API, Framework의 차이를 통해 Spring Framework에 대해 알아보자.

### Library
프로그래밍을 좀 더 쉽게 하기 위한, 재사용이 가능한 코드의 집합.

### API: Application Programming Interface
응응프로그램(Application)의 프로그래밍에 사용되는(Programming) 인터페이스(Interface)라는 뜻이다.<br>인터페이스는 서로 다른 두 개 이상의 것들을 이어주는 '매개체'이므로, API는 응용 프로그램을 프로그래밍 할 때 필요한 매개체라고 볼 수 있다.<br> 예를 들어 라이브러리를 사용할 때, 라이브러리 메소드들의 필요한 인자나 리턴 타입 등을 통해 개발하는 어플리케이션에 연결할 수 있으므로 라이브러리에서는 인자나 리턴타입 등이 API가 되는 것이다.

### Framework
프레임워크를 한국어로 표현하면 '틀'이다. 복잡한 문제가 생겼을 때 '틀'에 맞춰 행동하면 쉽게 해결할 수 있다.<br>프레임워크는 그 뜻처럼, 개발을 할 때 일정한 '틀'을 제공함으로서 프로그래밍을 보다 쉽게 도와준다. 

### Framework와 Library의 차이
프레임워크는 응용프로그램 등을 쉽게 만들기 위한 거대한 '틀'이자 '형식'으로 보면 적당하고, 라이브러리는 개발자가 모든 기능을 처음부터 끝까지 만들기에는 무리가 있으니 이미 다른 사람이 완성한 코드를 프로그래밍에 활용하는 것이라고 생각하면 될 듯하다.<br>즉, 라이브러리는 개발자의 목적에 맞게 중간중간 필요한 부분만 따로 가져오고 변형해서 쓸 수 있는 형태인 반면, 프레임워크는 그 자체로 프로그램을 만드는 거대한 틀이기 때문에 프레임워크의 본디 목적과 다른 프로그램은 만들 수가 없다. 

### Spring Framework
Spring은 자바기반의 대표적인 소프트웨어 프레임워크이다. Spring에서 제공하는 틀을 따르면 좀 더 효율적이고 쉽게 **웹페이지**를 만들 수 있다.


## Spring의 모듈과 특징
그렇다면 Spring Framework는 어떤 '틀'을 제공함으서 개발자로 하여금 쉽게 개발을 할 수 있도록 할까? Spring에서 제공하는 모듈을 통해 살펴보자.

### 모듈
보통은 어플리케이션 내부에서 기능별로 나뉘어지는 프로그램을 가르켜 모듈이라 한다. 파일 단위로 나뉘는 것이 보통이며, 관련된 데이터와 함수들이 묶여서 모듈을 이룬다.

### Spring의 모듈들
1. Spring Core 
	- Spring 프레임워크의 근간이 되는요소. IoC(또는 DI) 기능을 지원하는 영역을 담당. 
	- BeanFactory를 기반으로 Bean 클래스들을 제어할 수 있는 기능을 지원

2.	Spring Context
	-	Spring Core 바로 위에 있으면서 Spring Core에서 지원하는 기능외에 추가적인 기능들과 좀 더 쉬운 개발이 가능하도록 지원

3.	**Spring DAO**
	- DataBase Access Object
	-	JDBC를 통하여 DB에 연결하기 위해서는 드라이버(Driver)를 로드하고 커넥션(connection) 객체를 받아와야 한다.
	- JDBC를 사용하면 사용자가 요청을 할 때마다 매번 드라이버를 로드하고 커넥션 객체를 생성하여 연결하고 종료하기 때문에 매우 비효율적이다.
	- 이런 문제를 해결하기 위해서 커넥션풀(DBCP)를 사용한다.
	- 지금까지 우리들이 일반적으로 많이 사용해왔던 JDBC 기반하의 DAO개발을 좀 더 쉽고, 일관된 방법으로 개발하는 것이 가능하도록 지원
	- Spring DAO를 이용할 경우 지금까지 개발하던 DAO보다 적은 코드와 쉬운 방법으로 DAO를 개발하는 것이 가능

4.	Spring ORM
	-	Object Relation Mapping
	-	프레임워크인 Hibernate, IBatis, JDO와의 결합을 지원하기 위한 기능
	-	Spring ORM을 이용할 경우 Hibernate, IBatis, JDO 프레임워크와 쉽게 통합하는 것이 가능

5.	Spring AOP
	- Aspect Oriented Programming
	-	Spring 프레임워크에 Aspect Oriented Programming을 지원하는 기능이다.

7.	Spring Web
	-	Web Application 개발에 필요한 Web Application Context와 Multipart Request등의 기능을 지원
	-	또한 Struts, Webwork와 같은 프레임워크의 통합을 지원하는 부분을 담당

8.	Spring Web MVC
	-	Spring 프레임워크에서 독립적으로 Web UI Layer에 Model-View-Controller를 지원하기 위한 기능


[프레임워크, 라이브러리, api를 정리하는데 있어 참고한 자료](https://eine.tistory.com/entry/라이브러리-API-ABI-뜻-비교-정리)

