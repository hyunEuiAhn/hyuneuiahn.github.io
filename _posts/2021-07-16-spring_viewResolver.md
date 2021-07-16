---
layout: post
title:  "spring viewResolver"
date:   2021-07-16
excerpt: "스프링 프레임워크"
java: true
tag:
- 스프링
- viewresolver
comments: false
---


# 목차
* viewresolver

---


## viewresolver

오늘은 스프링의 기능 중 하나인 ViewResolver에 대해서 알아 보겠습니다.

ViewResolver는 클라이언트가 URL을 통해 서버에 요청을 보냈을 시 요청에 대한 응답 값으로 View 페이지를 렌더링하여 클라이언트에게 반환합니다.

Controller는 클라이언트의 요청에 View의 name을 리턴합니다. (ex. /login.jsp) 

그 다음은 dispatcherServlet의 ViewResolver가 해당하는 View 값을 찾아 렌더링하는 작업을 거칩니다.


ViewResolver를 통해 생성된 View Object의 값은 한 번 생성되면 캐싱이 되기 때문에 지속적으로 렌더링이 발생하지 않아 성능 면에서 장점이라 말할 수 있습니다.

저는 최근 실무에서 velocity를 사용하며 viewResolver를 다루어 보았지만, default로 사용되고 많이 활용되는 jsp를 기준으로 예제를 보여드리겠습니다.

먼저 web.xml에 dispatcherServlet을 추가합니다.

{% highlight xml %}
<servlet> 
    <servlet-name>dispatcher</servlet-name> 
    <servlet-class>org.springframework.web.servlet.DispatcherServlet</servlet-class> 
    <init-param> 
        <param-name>contextConfigLocation</param-name> 
        <param-value>WEB-INF/spring-config/dispatcher-servlet.xml</param-value> 
    </init-param> 
    <load-on-startup>1</load-on-startup> 
</servlet> 
<servlet-mapping> 
<servlet-name>dispatcher</servlet-name> 
<url-pattern>/</url-pattern> 
</servlet-mapping>

{% endhighlight %}

위에서 파일 형식으로 dispatcherServlet을 등록하였기 때문에 
WEB-INF/spring-config/dispatcher-servlet.xml 해당 경로에 파일을 추가해 줍니다.

{% highlight xml %}

<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xmlns:mvc="http://www.springframework.org/schema/mvc"
       xmlns:aop="http://www.springframework.org/schema/aop"
       xsi:schemaLocation="http://www.springframework.org/schema/beans 
                           http://www.springframework.org/schema/beans/spring-beans-4.0.xsd
                           http://www.springframework.org/schema/aop 
                           http://www.springframework.org/schema/aop/spring-aop-4.0.xsd">
     
    <bean id="/index" class="webprj.IndexController">
    <bean class="org.springframework.web.servlet.view.InternalResourceViewResolver">
        <property name="prefix" value="/WEB-INF/views/"/>
        <property name="suffix" value=".jsp"/>
    </bean>
     
</beans>

{% endhighlight %}

위에서 prefix, suffix 설정을 통해 실제 컨트롤러에 리턴된 View의 지정 주소를 간결하게 나타낼 수 있습니다. 

/WEB-INF/views/index.jsp 문장을 접두어(/WEB-INF/views)는 prefix에 기제하고, 
접미어(jsp)는 suffix에 기제하여 컨트롤러에서 return을 할 때에는 "index" 라는 값만 리턴하여도 
원하는 jsp 파일을 쉽게 찾을 수 있습니다.
