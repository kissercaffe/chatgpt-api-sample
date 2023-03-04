<script lang="ts">
    import type ListItem from "../models/list-item";
	import Card from "./UI/Card.svelte";
    
    export let list: ListItem[];

	const addClass = (name: string) => {
      if (name == "YOU"){
         return "message-right"
      } else {
         return "message-left"
      }
    } ;
    
    $: isEmpty = !list.length;
    
</script>
    
<section>
    {#if isEmpty}
    <Card>
      <p>No Items in List</p>
    </Card>
    {:else}
    {#each list as item (item.id)}
    <div class="message {addClass(item.name)}">
      <Card>
        <h3>{item.name}</h3>
        <p>{item.contents}</p>
      </Card>
    </div>
    {/each}
    {/if}
</section>
    
<style>
    .message {
      width: 90%;
      max-width: 800px;
      margin: 1rem auto 0 auto;
    }

    .message-right {
      text-align: right;
    }

    .message-left {
      text-align: left;
    }

    h3 {
      text-align: left;
      margin: 0 0 0.5rem 0;
    }
</style>
