<script>
import { each } from "svelte/internal";

    let todos = [
        // {task:"Get milk", completed: true, date: "27-1-2022"},
        // {task:"Get egg", completed: false, date: "28-1-2022"},
        // {task:"Get bread", completed: true, date: "29-1-2022"},
    ];
    let task_added = "";
    let error = "";

    
    const addTodo = () => {
        let todo = {
        task:task_added,
        isComplete:false,
        createdAt: new Date(),
    };
        if (todo.task !== ""){
            todos = [...todos, todo];
            error = ""
        } else {
            error = "Please add task"
        }
        
        task_added = "";
    };

    const markTodoasCompleted = (index) => {
        todos[index].isComplete = !todos[index].isComplete
        //console.log(todos[index])
       
    }

    const deleteTodo = (index) => {
        let deleteItem = todos[index];
        todos = todos.filter((item) => item != deleteItem)
    }

    const keyIsPressed = (event) => {
       //console.log(event) - inspect key
       if (event.key === "Enter"){
            addTodo();
       }
    }
    

</script>


<div class="block p-6 rounded-lg shadow-lg bg-white max-w-sm">
    <div class="form-group mb-6">
<input class="form-control
block
w-full
px-3
py-1.5
text-base
font-normal
text-gray-700
bg-white bg-clip-padding
border border-solid border-gray-300
rounded
transition
ease-in-out
m-0
focus:text-gray-700 focus:bg-white focus:border-blue-600 focus:outline-none" id="exampleInputEmail1" type="text"  placeholder="Add a task"  bind:value={task_added}/>
<button on:click={addTodo} class="
    px-6
    py-2.5
    bg-blue-600
    text-white
    font-medium
    text-xs
    leading-tight
    uppercase
    rounded
    shadow-md
    hover:bg-blue-700 hover:shadow-lg
    focus:bg-blue-700 focus:shadow-lg focus:outline-none focus:ring-0
    active:bg-blue-800 active:shadow-lg
    transition
    duration-150
    ease-in-out m-5">Add</button>

<ol>
    {#each todos as todo, index}
    <!-- class component = complete -->
        <li class:complete={todo.isComplete}>
            <span>
                 {todo.task}
            </span>
            <span>
                <button on:click={()=> markTodoasCompleted (index)} > ✔ </button>
                <button on:click={()=> deleteTodo(index)}> ✘ </button>
            </span>
       </li>   
       {:else}
       <p>No todos found</p>  
    {/each}
    <p class="text-red-600">{error}</p>
</ol>
</div>
</div>

<svelte:window on:keydown={keyIsPressed} />

<style>
    .complete {
      text-decoration: line-through;
    }
</style>