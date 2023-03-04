<script lang="ts">
	import NewItem from "./components/NewItem.svelte";
	import MessageForm from "./components/UI/MessageForm.svelte";
	  import ItemList from "./components/ItemList.svelte";
	  import type ListItem from "./models/list-item"
  
	let list: ListItem[] = [];
  
	const addNewItem = (name: string, contents: string, role: string) => {
	  list = [...list, { id: Math.random().toString(12), name, contents, role}];
	  return list;
	};
  </script>
  
  <svelte:head>
    <script src="https://cdn.jsdelivr.net/npm/openai@3.2.1/dist/index.min.js"></script>
  </svelte:head>
  
  <main>
	<div id="messagewrap">
	  <MessageForm>
	    <NewItem addNewItem={addNewItem} list={list} />
	  </MessageForm>
	</div>
	<ItemList {list} />
  </main>
  
  <style>
    :global(body) {
      background-color:cornsilk;
	}

    main {
	  text-align: center;
	  margin: 0 auto;
    }
	
	#messagewrap {
	  width: 90%;
      margin: 0 auto;
	}
	
  </style>
