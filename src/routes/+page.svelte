<h1>Todo List</h1>

<script>
    let todos = [
        { id: 1, text: 'Grocery shopping', completed: false },
        { id: 2, text: 'Go to the gym', completed: true },
        { id: 3, text: 'Homework', completed: false }
    ];

    let newTodoText = '';

    function addTodo() {
        if (newTodoText.trim() !== '') {
            todos = [
                ...todos,
                {
                    id: Math.max(...todos.map(todo => todo.id)) + 1,
                    text: newTodoText.trim(),
                    completed: false
                }
            ];
            newTodoText = '';
        }
    }

    function editTodo(todoId, newText) {
        todos = todos.map(todo => {
            if (todo.id === todoId) {
                return {
                    ...todo,
                    text: newText.trim()
                };
            }
            return todo;
        });
    }

    function deleteTodo(todoId) {
        todos = todos.filter(todo => todo.id !== todoId);
    }
</script>

<div>
    <input type="text" bind:value={newTodoText}>
    <button on:click={addTodo}>Add</button>
</div>

<ul>
    {#each todos as todo}
        <li>
            <input type="checkbox" bind:checked={todo.completed}>
            <input type="text" value={todo.text} on:change={(event) => editTodo(todo.id, event.target.value)}>
            <button on:click={() => deleteTodo(todo.id)}>Delete</button>
        </li>
    {/each}
</ul>
