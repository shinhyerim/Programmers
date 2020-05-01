# To-do List 만들기

### Vue.js
- SPA(Single Page Application) Framework
- 백엔드 개발 트렌드인 MVC패턴에서 뷰를 분리하여 하나의 어플리케이션으로 만들고 백엔드는 API형태로 동작하는 것
	Vue CLI는 이런 환경을 만들어주는 도구임

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
```javascript
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
```javascript
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

3. 2020.05.01.
- CDN방식이 아닌 CLI방식을 이용하여 Vue js 사용하기
- npm 사용 전 nodejs를 먼저 설치해야함 -> nodejs.org에서 다운로드 가능
	npm? JavaScript 패키지 설치를 도와주는 Tool (java의 maven과 비슷함)
- node.js 설치 후 cmd창에 아래 명령어 입력
	-g 옵션 : 사용자 홈 디렉토리 안에 설치하는 옵션, nodejs 설치 시 g옵션으로 설치하는 경로가 추가됨
```
npm install -g @vue/cli
```
- Eclipse에서 Vue js를 사용할 때는 Help > Eclipse Marketplace > Vue 검색 후 설치


- v-for 복습
	v-for를 사용할 때 v-bind:key를 추가하지 않으면
	'Expected 'v-bind:key' directive to use the variables which are defined by the 'v-for' directive  vue/valid-v-for' 오류 발생!
```javscript
<template v-for="todo in activeTodoList"><!-- 변수처럼 사용 가능 -->
    <todo v-bind:key="todo"
       :label="todo.label" 
       @componentClick="toggleTodoState(todo)"
    />
</template>
```
- class의 getter와 같은 동작을 하는 computed
```javascript
...
,computed{

}
```
- component 분리 방법
```javascript
<!-- 1. src\component에 새로운 Vue 파일 생성 후 코드 분리-->
<template>
	<button class="list-group-item text-left" :key="todo" @click="clickButton">
		{{ label }}<!-- 출력 값을 todo.label에서 label로 변경 -->
    </button>
</template>
<script>
	export default {
		props:['label'],
		methods:{
			clickButton(){
				//$emit 메소드로 이벤트 발생시켜줌
				this.$emit('componentClick');
			}
		}
	};
</script>
```
```javascript
<script>
// 2. component에 생성한 vue파일 import
import todo from './components/todo';

...

export default {
  
  ...
  
  // 3. import한 todo파일 components에 추가
  components: {
    todo
  }
}
</script>
```

- component에서 이벤트를 발생시키는 방법: $emit 사용

