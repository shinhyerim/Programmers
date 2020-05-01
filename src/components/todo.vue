<template>
<!-- App.vue의 <button> 소스 분리
click이벤트를 처리해야함
-> todo객체를 받아오지 않으니 내부에서 state값을 변경할 방법이 없는 문제 발생
	설령 컴포넌트 내부에서 state값을 변경할 수 있는 방법이 있다고 해도
	변수값은 개발자가 예상 가능한 곳에서 변경해야 하므로 여기서 변경하는 것이 적절하지 않아보임
-> 이러한 경우에는 컴포넌트에서 발생할 이벤트를 외부에 알려주는 방식으로 개발해야 함 -->
	<button class="list-group-item text-left" :key="todo" @click="clickButton">
		{{ label }}<!-- 출력 값을 todo.label에서 label로 변경 -->
    </button>
</template>
<script>
	export default {
		// 외부에서 입력받을 label항목을 props에 지정
		props:['label'],
		methods:{
			clickButton(){
				//$emit 메소드로 이벤트 발생시켜줌
				this.$emit('componentClick');
			}
		}
	};
</script>