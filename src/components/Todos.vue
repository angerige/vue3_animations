<template>
	<div class="todos">
		<input
			type="text"
			v-model="newTodo"
			@keypress.enter="addTodo"
			placeholder="Add a new todo..."
		/>
		<transition name="switch" mode="out-in">
			<div v-if="todos.length">
				<!-- https://v3.cn.vuejs.org/guide/migration/transition-group.html#%E6%A6%82%E8%A7%88 -->
				<transition-group tag="ul" name="list" appear>
					<li v-for="todo in todos" :key="todo.id" @click="deleteTodo(todo.id)">
						{{ todo.text }}
					</li>
				</transition-group>
			</div>
			<div v-else>Woohoo, nothing left todo!</div>
		</transition>
	</div>
</template>

<script lang="ts">
import { defineComponent, reactive, ref, toRefs } from "@vue/runtime-core";

interface State {
	todos: {
		text: string;
		id: number;
	}[];
}

export default defineComponent({
	name: "Todos",
	setup(prosp, { emit }) {
		const state = reactive<State>({
			todos: [
				{ text: "make the bed", id: 1 },
				{ text: "play video games", id: 2 },
			],
		});

		const newTodo = ref<string>("");

		const addTodo = (): void => {
			if (newTodo.value) {
				const id = Math.random();
				state.todos = [
					{
						text: newTodo.value,
						id,
					},
					...state.todos,
				];
				newTodo.value = "";
			} else {
				emit("badValue");
			}
		};

		const deleteTodo = (id: number): void => {
			state.todos = state.todos.filter(todo => todo.id != id);
		};
		return {
			...toRefs(state),
			newTodo,
			addTodo,
			deleteTodo,
		};
	},
});
</script>

<style scoped>
.todos {
	max-width: 400px;
	margin: 20px auto;
	position: relative;
}
input {
	width: 100%;
	padding: 12px;
	border: 1px solid #eee;
	border-radius: 10px;
	box-sizing: border-box;
	margin-bottom: 20px;
}
.todos ul {
	position: relative;
	padding: 0;
}
.todos li {
	list-style-type: none;
	display: block;
	margin-bottom: 10px;
	padding: 10px;
	background: white;
	box-shadow: 1px 3px 5px rgba(0, 0, 0, 0.1);
	border-radius: 10px;
	width: 100%;
	box-sizing: border-box;
}
.todos li:hover {
	cursor: pointer;
}

/* list transitions */
.list-enter-from,
.list-leave-to {
	opacity: 0;
	transform: scale(0.6);
}
.list-enter-to,
.list-leave-from {
	opacity: 1;
	transform: scale(1);
}
.list-enter-active,
.list-leave-active {
	transition: all 0.4s ease;
}

.list-leave-active {
	position: absolute;
}

.list-move {
	transition: all 0.3s ease;
}

/* switch transitions */
.switch-enter-from,
.switch-leave-to {
	opacity: 0;
	transform: translateY(20px);
}

/* .switch-enter-to,
.switch-leave-from {
	opacity: 1;
	transform: translateY(0);
} */
.switch-enter-active,
.switch-leave-active {
	transition: all 0.5s ease;
}
</style>
