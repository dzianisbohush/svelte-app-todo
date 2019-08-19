<script>
  import { afterUpdate } from "svelte";
  import TodoItem from "./TodoItem.svelte";

  export let todoItems;
  export let addTodo;
  export let newTodo;
  export let toggleDone;
  export let deleteTodo;

  $: notComplitedItems = todoItems.filter(item => !item.checked);
  $: complitedItems = todoItems.filter(item => item.checked);
</script>

<form on:submit|preventDefault={addTodo}>
  <input
    class="js-todo-input"
    type="text"
    aria-label="Enter a new todo item"
    placeholder="Enter a new todo item"
    bind:value={newTodo} />
</form>
<ul class="todo-list">
  {#each notComplitedItems as todo (todo.id)}
    <TodoItem {todo} {toggleDone} {deleteTodo} />
  {/each}
  {#if complitedItems.length}
    <p class="complited-title">Complited:</p>
    {#each complitedItems as todo (todo.id)}
      <TodoItem {todo} {toggleDone} {deleteTodo} />
    {/each}
  {/if}
</ul>

<style>
  input {
    width: 100%;
  }
  ul {
    list-style: none;
    padding: 0;
  }
  .complited-title {
    font-weight: bold;
  }
</style>
