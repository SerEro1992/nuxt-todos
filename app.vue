<template>
	<div class="container">
		<UCard class="cards">
			<h1>My Todos</h1>
			<div class="add-todo">
				<input v-model="input" type="text" placeholder="Add new todo..." />
				<UButton @click.prevent="handleClick" color="white" variant="solid"
					>Add
				</UButton>
			</div>
			<UCard
				@click="() => updateTodo(todo.id)"
				class="main-card"
				v-for="todo in todos"
				:key="todo.id"
			>
				<div class="card">
					<h4 :class="todo.completed ? 'complete' : null">{{ todo.item }}</h4>
					<p @click.prevent="() => deleteTodo(todo.id)">x</p>
				</div>
			</UCard>
		</UCard>
	</div>
</template>

<script setup lang="ts">
const input = ref('');
const { todos, addTodo, updateTodo, deleteTodo } = useTodos();

const handleClick = () => {
	addTodo(input.value);
	input.value = '';
};
</script>

<style scoped>
.container {
	padding: 2rem;
	margin: 0 auto;
	max-width: 50%;
}
.cards {
	padding: 5rem;
	margin-top: 1rem;
}
.main-card {
	padding: 0.5 rem;
	margin-top: 1rem;
	cursor: pointer;
}

.card {
	display: flex;
	align-items: center;
	justify-content: space-between;
}
.add-todo {
	display: flex;
	justify-content: space-between;
	margin-bottom: 10px;
}

input {
	outline: none;
}
p {
	font-size: 20px;
	padding: 5px;
}

.complete {
	text-decoration: line-through;
}
</style>
