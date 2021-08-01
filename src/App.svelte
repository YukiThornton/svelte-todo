<script lang="ts">
    import Input from './Input.svelte';
    import Item from './Item.svelte';
    import Button from './Button.svelte';
    
    let uid = 1;
    let todos = [
        {id: uid++, text: 'Get milk', done: false},
        {id: uid++, text: 'Get flour', done: false},
        {id: uid++, text: 'Get egg', done: false},
    ]
    let dones = []

    function addTodo(e) {
        todos = [
            ...todos,
            {
                id: uid++,
                text: e.detail.value,
                done: false
            }
        ]
    }
    function toggleDone(event) {
        const id = event.detail.id
        const matchedTodo = todos.find(todo => todo.id === id)
        if (matchedTodo) {
            todos = todos.filter(todo => todo.id !== id)
            dones = [...dones, {...matchedTodo, done: true}]
        } else {
            const matchedDone = dones.find(done => done.id === id)
            dones = dones.filter(done => done.id !== id)
            todos = [...todos, {...matchedDone, done: false}]
        }
    }
    
    function removeDones(event) {
        dones = [];
    }
</script>

<main>
    <div class="lists">
        <div class="container">
            <h2>TODO!</h2>
            {#each todos as {id, text, done} (id)}
                <Item {id} {text} {done} on:toggleDone={toggleDone} />
            {/each}
        </div>
        <div class="container">
            <h2>DONE!</h2>
            {#each dones as {id, text, done} (id)}
                <Item {id} {text} {done} on:toggleDone={toggleDone} />
            {/each}
            <Button on:click={removeDones} disabled={dones.length === 0}>Clear All</Button>
        </div>
    </div>
    <Input value='' on:inputFinished={addTodo}/>
</main>

<style>
    main {
        padding: 30px;
    }
    .lists {
        display: flex;
    }
    .container {
        width: 50vw;
    }
</style>