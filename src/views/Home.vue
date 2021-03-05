<template>
	<div class="home">
		<transition name="toast">
			<Toast v-if="showToast" />
		</transition>
		<Todos @badValue="triggerToast" />
	</div>
</template>

<script lang="ts">
import { defineComponent, ref } from "@vue/runtime-core";

import Toast from "@/components/Toast.vue";
import Todos from "@/components/Todos.vue";

export default defineComponent({
	name: "Home",
	components: {
		Toast,
		Todos,
	},
	setup() {
		const showToast = ref<boolean>(false);
		const triggerToast = (): void => {
			showToast.value = true;
			setTimeout(() => {
				showToast.value = false;
			}, 3000);
		};

		return {
			showToast,
			triggerToast,
		};
	},
});
</script>

<style>
/* enter classes */
/* .toast-enter-from {
	opacity: 0;
	transform: translateY(-60px);
}
.toast-enter-to {
	opacity: 1;
	transform: translateY(0);
} */
.toast-enter-active {
	/* transition: all 0.3s ease; */
	animation: wobble 0.5s ease;
}

/* leave classes */
.toast-leave-from {
	opacity: 1;
	transform: translateY(0px);
}
.toast-leave-to {
	opacity: 0;
	transform: translateY(-60px);
}
.toast-leave-active {
	transition: all 0.3s ease;
}

@keyframes wobble {
	0% {
		opacity: 0;
		transform: translateY(-60px);
	}
	50% {
		opacity: 1;
		transform: translateY(0px);
	}

	60% {
		transform: translateX(8px);
	}
	70% {
		transform: translateX(-8px);
	}
	80% {
		transform: translateX(4px);
	}
	90% {
		transform: translateX(-4px);
	}
	100% {
		transform: translateX(0);
	}
}
</style>
