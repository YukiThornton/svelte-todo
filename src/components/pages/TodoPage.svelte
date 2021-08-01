<script lang="ts">
    import Input from '../atoms/Input.svelte';
    import Button from '../atoms/Button.svelte';
    import ItemList from './../organisms/ItemList.svelte'
    
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
        <ItemList items={todos} on:toggleDone={toggleDone} color="#9dd28b" emptyMessage="Add your todos!">
            <h2 slot="title">TODO!</h2>
        </ItemList>
        <ItemList items={dones} on:toggleDone={toggleDone} emptyMessage="Nothing to show">
            <h2 slot="title">DONE!</h2>
            <Button slot="action" on:click={removeDones} disabled={dones.length === 0}>Clear All</Button>
        </ItemList>
    </div>
    <Input value='' on:inputFinished={addTodo}/>
</main>

<style>
    main {
        padding: 30px;
    }
    .lists {
        display: grid;
        grid-template-columns: 1fr 1fr;
        grid-template-rows: 1fr;
        column-gap: 20px;
    }
</style>