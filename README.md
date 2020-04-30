# To-do List 만들기

### Vue.js
- SPA Framework

* * *

### 목적
- Vue.js를 사용해보고 이해하기
- Vue Devtools 설치 후 사용하기

* * *

### 공부 일지
1. 2020.04.29.
- 사용 Tool : Eclipse
- CDN 방식을 이용해서 Vue.js 사용하기
```html
<!-- development version, includes helpful console warnings -->
<script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
```
- Vue Devtools를 이용하여 value값 확인하기

- Mustache 구문을 사용하여 데이터 바인딩하기
```html
<div id="app">
	<input type="text" id="user_id" v-model="userID">
	<input type="password" id="user_password" v-model="userPassword">
	<button type="button">로그인</button>
	<br />
	아이디 : {{ userID }}
	<br />
	비밀번호 : {{ userPassword }}
</div>
```
* * *
- List출력하기
- 반복문 사용 : v-for
- v-for = "항목을 담을 변수 in 반복문에 사용할 배열"
- 2개 이상의 태그를 반복하여 사용한다면 template을 사용
```html
<div id="app">
	<ul style="list-style:none;">
		<template v-for="item in items">
			<li >
				<img :src="item.image">
			</li>
			<li>
				{{ item.title }}
			</li>
		</template>
	</ul>
</div>
```
* * *
2. 2020.04.30.
- attribute binding : 'v-bind:' 또는 단축표현인 콜론(:) 사용
- style or  class같은 경우 배열이나 json을 이용해서 관리 가능
- style은 json의 key에 css항목을 넣고 value에 설정값
- class는 json의 key에 적용할 클래스명을 넣고 value에 true/false로 클래스 적용여부를 정해줌

```javascript
<div id="app">
	<div :class="[dropdown,toggle]">
		<ul>
			<li><a href="#">메뉴1</a></li>
			<li><a href="#">메뉴2</a></li>
		</ul>
	</div>
</div>
```
```javscript
<script>
let app = new Vue({
		el : '#app',
		data(){
			return{
				id: 1,
				image : 'https://picsum.photos/200/200/?image=353',
				// 유동적인 스타일은 json으로 관리하는 것이 편함
				style:{
					background: 'red',
				},
				fontStyle:{
					fontSize: '10px',
					fontFamily: 'dotum'
				},
				dropdown: 'dropdown',
				toggle:{
					on: false
				}
			};
		}
	});
</script>
```
* * *
- 메소드 선언 방법과 이벤트 바인딩
- 메소드 선언 방법
```javascript
<script>
let app = new Vue({
	el: '#app',
	data(){
		return{
			counter: 0
		};
	},
	methods:{
		// '=>' 사용 불가
		add(){
			this.counter++;
		},
		keyUp(ev){
			if(ev.keyCode != 13){
				console.log('엔터키가 아님');
				return;
			}
			
			console.log('엔터키가 눌림');
		}
	}
});
</script>
```
- 이벤트 바인딩 : 'v-on:이벤트명' 또는 단축표현인 '@이벤트명' 사용
- v-on을 이용하여 이벤트를 받아오는 방법
- v-on:이벤트명 = "" : ""안이 javascript영역이 되어 연산작업을 하거나 메소드를 호출가능
- ※ 연산작업을 하게 되는 경우 가독성이 떨어져 보통 메소드를 선언하여 연결해줌
- 특정 키가 입력되었을 때만 메소드가 실행될 수 있도록 할 수도 있음
```javascript
<div id="app">
	<button type="button" @click="add">더하기</button>
	{{ counter }}
	
	<!-- @keyup.enter : enter키에만 동작하도록 설정  -->
	<input type="text" @keyup.enter="keyUp">
</div>
```

* * *
- Component
- Vue.js에서 컴포넌트를 사용하면 반복되는 태그 묶음을 한 곳에 모아 관리할 수 있고, 여러 곳에서 사용할 수 있음
```html
<div id="app">
	<div class="container mx-auto mt-10">
		<div class="flex">
			<product
				image="https://picsum.photos/300/200?image=0"
				avartor="https://picsum.photos/30/30?image=80"
				title="노트북"
				description="노트북 상품 설명"
			></product>
			<product
				image="https://picsum.photos/300/200?image=3"
				avartor="https://picsum.photos/30/30?image=100"
				title="아이폰"
				description="아이폰 상품 설명"
			></product>
			<product
				image="https://picsum.photos/300/200?image=23"
				avartor="https://picsum.photos/30/30?image=110"
				title="포크"
				description="포크 상품 설명"
			></product>
			<product
				image="https://picsum.photos/300/200?image=24"
				avartor="https://picsum.photos/30/30?image=70"
				title="책"
				description="책 상품 설명"
			></product>
		</div>
	</div>
</div>
```
```javascript
<script>
Vue.component('product',{
	// 설정값 - json형식
	props: ['image','title','description','avartor'],
	template: `
	<div class="flex-1 px-5">
		<div class="max-w-sm rounded overflow-hidden shadow-lg">
			<img class="w-full" :src="image">
			<div class="px-6 py-4">
				<div class="relative">
					<div class="absolute pin-l pin-t bg-white border border-pear-dark rounded-full" style="...">
						<img class="block rounded-full" :src="avartor" width="30">
					</div>
				</div>
				<div class="font bold text-xl mb-2">{{ title }}</div>
				<p class="text-grey-darker text-base">
					{{ description }}
				</p>
			</div>
		</div>
	</div>
	`
});
</script>
```
