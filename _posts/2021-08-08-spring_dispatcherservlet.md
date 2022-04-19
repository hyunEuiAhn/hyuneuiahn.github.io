---
layout: post
title:  "spring dispatcherservlet"
date:   2021-08-08
excerpt: "스프링 프레임워크"
java: true
tag:
- 스프링
- dispatcherservlet
- MVC
comments: false
---


# 목차
* dispatcher servlet
* MVC 패턴

---


## dispatcher servlet

dispatcher servlet은 스프링의 프론트 컨트롤러 역할을 합니다. 

프론트 컨트롤러는 HTTP로 들어온 요청을 제일 먼저 받아들입니다. 

스프링의dispatcher servlet 역시 요청을 받아 보안을 처리하거나, 디코딩을 수행할 수 있습니다. 

스프링에서 dispatcher servlet은 web.xml 파일에 정의 하여 사용할 수 있습니다. 

흐름도를 파악해 보면 HTTP 요청을 전달받은 dispatcher servlet은 해당 요청에 대응하는 controller에 요청을 전달합니다. 

전달받은 controller는 모델을 생성하고 뷰가 존재하면 뷰의 정보를 다시 dispatcher servlet으로 전달합니다. 

dispatcher servlet은 전달받은 view 값을 찾아 view를 생성하여 사용자에게 전달합니다.


## MVC 패턴

위에서 설명한 패턴이 바로 MVC 패턴이 됩니다. MVC 패턴은 Model View Controller를 의미합니다. 

여기서 각각의 역할과 기능에 대해 간략히 알아보면,
Controller는 요청에 대한 Model을 생성하고 뷰의 정보를 반환하는 역할을 합니다.

Model은 사용자에게 필요한 객체 정보를 쿼리에서 조회해 오거나 controller의 작업에 의해 생성되어 집니다.

view는 사용자에게 보여지는 화면을 의미하며 사용자가 원하는 정보나 필요한 정보를 model을 통해 가져오고 해당 정보를 보여주는 역할을 합니다.

