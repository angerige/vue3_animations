<template>
	<div class="about">
		<transition
			appear
			@before-enter="beforeEnter"
			@enter="enter"
			@after-enter="afterEnter"
		>
			<h1>About</h1>
		</transition>
		<p>
			Lorem ipsum dolor sit amet consectetur adipisicing elit. Cum aperiam
			officia possimus delectus inventore quod quisquam culpa voluptas iusto,
			quae maiores quo dolorum, corporis laboriosam a dolore consequatur
			assumenda nam!
		</p>
		<p>
			Lorem ipsum dolor sit amet consectetur adipisicing elit. Cum aperiam
			officia possimus delectus inventore quod quisquam culpa voluptas iusto,
			quae maiores quo dolorum, corporis laboriosam a dolore consequatur
			assumenda nam!
		</p>
		<p>
			Lorem ipsum dolor sit amet consectetur adipisicing elit. Cum aperiam
			officia possimus delectus inventore quod quisquam culpa voluptas iusto,
			quae maiores quo dolorum, corporis laboriosam a dolore consequatur
			assumenda nam!
		</p>
	</div>
</template>

<script lang="ts">
import { defineComponent } from "@vue/runtime-core";

// js 动画库
import gsap from "gsap";

export default defineComponent({
	name: "About",
	setup() {
		const beforeEnter = (el: HTMLElement): void => {
			el.style.transform = "translateY(-60px)";
			el.style.opacity = "0";
		};
		const enter = (el: HTMLElement, done: (...args: any[]) => {}): void => {
			gsap.to(el, {
				duration: 1,
				y: 0,
				opacity: 1,
				ease: "bounce.out",
				onComplete: done,
			});
		};

		const afterEnter = (el: HTMLElement) => {
			console.log("afterEnter");
		};

		return {
			beforeEnter,
			enter,
			afterEnter,
		};
	},
});
</script>

<style scoped>
.about {
	max-width: 600px;
	margin: 20px auto;
}
</style>
