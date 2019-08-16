<script>
  import TodosList from "./TodosList.svelte";

  let todoItems = [];
  let newTodo = "";
  let notComplitedItems = [];
  let complitedItems = [];

  const addTodo = () => {
    newTodo = newTodo.trim();
    if (!newTodo || todoItems.find(item => item.text === newTodo)) {
      return;
    }

    const todo = {
      text: newTodo,
      checked: false,
      id: Date.now()
    };

    todoItems = [...todoItems, todo];
    newTodo = "";

    getComplitedItems();
  };

  const toggleDone = id => {
    const index = todoItems.findIndex(item => item.id === Number(id));
    todoItems[index].checked = !todoItems[index].checked;

    getComplitedItems();
  };

  const deleteTodo = id => {
    todoItems = todoItems.filter(item => item.id !== Number(id));

    getComplitedItems();
  };

  const getComplitedItems = () => {
    notComplitedItems = todoItems.filter(item => !item.checked);
    complitedItems = todoItems.filter(item => item.checked);
  };
</script>

<div>
  <TodosList
    {notComplitedItems}
    {complitedItems}
    {addTodo}
    {toggleDone}
    {deleteTodo}
    bind:newTodo />
</div>
