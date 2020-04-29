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
