---
layout: post
title:  "Class Component LifeCycle"
date:   2020-06-10
excerpt: "클래스 컴포넌트 라이프 사이클 함수"
react: true
tag:
- react 
- LifeCycle
comments: false
---


# 목차
* 라이프 사이클 메서드
* 함수 종류

---


## 라이프 사이클 메서드

### 마운트, 업데이트, 언마운트 

#### 마운트 : DOM이 웹 브라우저상에 나타나는 것

호출되는 메서드

- constructor : 컴포넌트를 새로 만들 때마다 호출되는 클래스 생성자 메서드

- getDerivedStateFromProps : props에 있는 값을 state에 넣을 때 사용하는 메서드

- render : 우리가 준비한 UI를 렌더링하는 메서드

- componentDidMount : 컴포넌트가 웹 브라우저상에 나타난 후 호출하는 메서드

---

#### 업데이트 : 업데이트는 총 네 가지 경우 진행됩니다.

1. props가 바뀔 때

2. state가 바뀔 때

3. 부모 컴포넌트가 리렌더링 될 때

4. this.forceUpdate로 강제 렌더링을 트리거할 때

  - getDerivedStateFromProps : 업데이트 시작 전 호출, props의 변화에 따라 state 값에 변화를 줄 때 사용

  - shouldComponentUpdate : 컴포넌트가 리렌더링을 해야 할지 말지를 결정하는 메서드, true, false 값을 반환해야 되며,
 true는 다음 라이프사이클 메서드를 계속 실행,
 false는 작업 중지 시켜 컴포넌트 리렌더링 되지 않음.
만약 특정 함수에서 this.forceUpdate() 함수를 호출한다면 이 과정을 생력하고 바로 render 함수를 호출

  - render : 컴포넌트를 리렌더링

  - getSnapshotBeforeUpdate : 컴포넌트 변화를 DOM에 반영하기 바로 직전에 호출하는 메서드

  - componenetDidUpdate : 컴포넌트의 업데이트 작업이 끝난 후 호출하는 메서드

---

#### 언마운트 : 마운트의 반대 과정, 컴포넌트를 DOM에서 제거하는 것

- componentWillUnmount : 컴포넌트가 웹 브라우저상에서 사라지기 전에 호출하는 메서드




---

## 함수 종류

#### render() 함수

- 컴포넌트의 모양새를 정의한다. this.props, this.state 애 접근 가능하며, 리액트 요소를 반환. (div, 따로 선언한 컴포넌트)

- 아무것도 보여주고 싶지 않다면 null, false를 반환

- 이벤트 설정이 아닌 곳에 setState를 설정하면 안 되며, 브라우저의 DOM에 접근해도 안된다. DOM정보를 가져오거나 state에 변화를 줄 때 componentDidMount를 사용



#### construct(props) 메서드

- 컴포넌트의 생성자 메서드로 컴포넌트를 처음 만들 때 실행, 초기 state를 정할 수 있습니다.

#### getDerivedStateFromProps 메서드

- props로 받아온 값을 state에 동기화 시키는 용도, 컴포넌트가 마운트 될 때, 업데이트 될 때 호출

ex)

{% highlight javascript %}
static getDerivedStateFromProps(nextProps, prevState) {
	if(nextProps.calue !== prevState.value) {  // 조건에 따라 특정 값 동기화
	   return { value: nextProps.value };
	}
           return null;   // state를 변경할 필요가 없다면 null 반환
}
{% endhighlight %}

#### componentDidMount 메서드

- 컴포넌트를 만들고, 첫 렌더링을 다 마친 후 실행

- 이 안에서 다른 자바스크립트 라이브러리 또는 프레임워크의 함수를 호출하거나 이벤트 등록

- setTimeout, setInterval, 네트워크 요청 같은 비동기 작업을 처리


#### shouldComponentUpdate 메서드

- props, state를 변경했을 때 리렌더링을 시작할 지 여부를 지정하는 메서드

- default 값은 true이며, true나 false 값을 반환해야 됩니다.

- false를 반환하면 업데이트 과정은 여기서 중지됩니다.

- 이 메서드 안에서 현재 props와 state는 this.props, this.state로 접근

- 새로 설정 될 props, state는 nextProps, nextState로 접근

- 프로젝트 성능 최적화, 리렌더링을 방지할 때 false 반환


#### getSnapshotBeforeUpdate 메서드

- render에서 만들어진 결과물이 브라우저에 실제로 반영되기 직전에 호출

- 이 메서드에서 반환하는 값은 componentDidUpdate에서 세 번째 파라미터인 snapshot 값으로 전달받을 수 있습니다.

- 업데이트 직전 값을 참고할 일이 있을 경우 활용

ex)

{% highlight javascript %}
getSnapshotBeforeUpdate(prevProps, prevState) {
	if(prevState.array !== this.state.array) {
	  const { scrollTop, scrollHeight } = this.list
	   return { scrollTop, scrollHeight };
	}
}
{% endhighlight %}



#### componentDidUpdate 메서드

- 리렌더링 완료한 후 실행

- 업데이트가 끝난 직후이므로, DOM 관련 처리를 해도 무방

- prevProps 또는 prevState를 사용하여 컴포넌트가 이전에 가졌던 데이터에 접근 가능

- getSnapshotBeforeUpdate 에서 반환 값이 있다면 snapshot 값을 전달받을 수 있습니다.


#### componentWillUnmount 메서드

- 컴포넌트를 DOM에서 제거할 때 실행

- componentDidMount에 등록한 이벤트, 타이머, 직접 생성한 DOM이 있다면 여기서 제거 작업.


#### componentDidCatch 메서드

- 컴포넌트 렌더링 도중에 에러가 발생했을 때 애플리케이션이 먹통이 되지 않고 오류 UI를 보여 줄 수 있게 해줍니다.

ex)

{% highlight javascript %}
componentDidCatch(error, info) {
	this.setState({
	   error : true
	});
	console.log({error, info});
}
{% endhighlight %}

- error는 파라미터에 어떤 에러가 발생했는지 알려주며, info 파라미터는 어디에 있는 코드에서 오류가 발생했는지 정보를 줍니다.

- API로 호출하여 오류를 수집할 수 있습니다.

- 메서드를 사용할 때는 컴포넌트 자신에게 발생하는 에러를 잡아낼 수 없고 자신의 this.props.children으로 전달되는 컴포넌트에서 발생하는 에러만 잡아낼 수 있습니다. 



---




