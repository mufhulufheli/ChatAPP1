<script>
    import {Collection} from 'sveltefire'
    import {tick} from 'svelte'
    import AppendMessage from './AppendMessage.svelte'
    export let user
    let chatsElements
    async function scrollToTheEnd(){
        await tick()
        chatsElements.scrollTo(0, chatsElements.scrollHeight)
    }
</script>
<style>
    .is-sender{
        text-align: right;
        margin-left : 100px;
    }
    .is-receiver{
        text-align: left;
        margin-right : 100px;
    }
    .chat-box{
        flex: 1;
        display : flex;
        flex-direction: column;
        overflow-y: auto;
    }
</style>
<Collection path={'/chat'} let:ref={chatsRef} let:data={messages} on:data={scrollToTheEnd}>
    <div class="box chat-box" bind:this={chatsElements}>
        {#each messages.sort((a,b) => a.date - b.date) as {message,uid}}
            <div class="notification {uid == user.uid ? 'is-info is-sender' : 'is-success is-receiver'}">
                {message}
            </div>
        {/each}
    </div>
    <AppendMessage {chatsRef} {user} />
</Collection>
