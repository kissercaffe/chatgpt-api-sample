<script lang="ts">
    import {Configuration, OpenAIApi } from "openai";
    import type ListItem from "../models/list-item";

    export let addNewItem: (
      name: string,
      contents: string,
      role: string
    ) => ListItem[];

    export let list: ListItem[];
  
    let name: string;
    let contents: string;
    let tokenNum: number = 0; 
    
    const handleSubmit = (event: Event) => {
      const itemList = addNewItem("YOU", contents, "user");
      const messages = itemList.map(d => {return {"role": d.role,  "content": d.contents}})
      const configuration = new Configuration({
        apiKey: "キーを入れてください",
      });
      const openai = new OpenAIApi(configuration);

      (async () => {
        const completion = await openai.createChatCompletion({
          model: "gpt-3.5-turbo",
          messages: messages
          // max_tokens: 200 
        });
        console.log(completion.data);
        tokenNum = tokenNum + completion.data.usage.total_tokens
        addNewItem("ChatGPT", completion.data.choices[0].message.content, "system");
      })();
      console.log(messages);
    };
  </script>
  
  <form class="form" on:submit|preventDefault={handleSubmit}>
    <div>
      <label for="contents">Contents</label>
      <input type="text" name="contents" bind:value={contents} />
    </div>
    <button type="submit">talk</button>
  </form>
  <div class="tokennum">
    <p>token number: {tokenNum}</p>
  </div>

  <style>
    .form {
      display: flex;
      flex-direction: column;
      text-align: left;
    }
  
    .form div {
      margin-bottom: 1rem;
    }
  
    .form label {
      margin-bottom: 0.3rem;
    }
  
    .form input {
      width: 100%;
    }
  </style>
  