<script>
  import Scroller from '@sveltejs/svelte-scroller';
  import { onMount } from 'svelte';
  import * as d3 from 'd3';
  import Graph from "./Graph.svelte";
  let count, index, offset, progress;
  $:console.log(index)

  let hillaryData = [];
  let trumpData = [];
  let common_words = [];

  let prefix = "";
  let inputText = "";
  let filtered_hillary;
  let filtered_trump;

  let suggest_words;
  let top_five_words;
  let if_empty = false;

  //load data
  onMount(async () => {
    const res = await fetch('hillary_words.csv'); 
    const csv = await res.text();
    hillaryData = d3.csvParse(csv, d3.autoType)
  });
  onMount(async () => {
    const res = await fetch('trump_words.csv'); 
    const csv = await res.text();
    trumpData = d3.csvParse(csv, d3.autoType)
  });
  onMount(async () => {
    const res = await fetch('words_in_common.csv'); 
    const csv = await res.text();
    common_words = d3.csvParse(csv, d3.autoType)
  });
  //suggest words
  function handleClick(word) {
   prefix = word;
   inputText = word;
  }
  //get frequency for input word
  $: filtered_hillary = hillaryData.filter((d) => d.Word == prefix.toLowerCase());
  $: filtered_trump = trumpData.filter((d) => d.Word == prefix.toLowerCase());
  //get five suggest words when typing in
  $: if (inputText !== "") {
    suggest_words = common_words.filter((d) => String(d.Word).startsWith(inputText.toLowerCase())).slice(0, 5);
    top_five_words = suggest_words.map(d => d.Word);
  } else{
    top_five_words = []
  }
  //check if words in data, and message if not
  $: if_empty = inputText !== "" && top_five_words.length === 0;
  //if clear inputbox, clear everything
  $: if (inputText == "") {
    prefix = ""
  }
</script>

  <div class="left-panel">
    <div class=graph-container>
    <Graph {index} {filtered_hillary} {filtered_trump} {prefix}{inputText}/>
  </div>
  </div>
  <div class="right-panel">
    <Scroller
      top={0.0}
      bottom={1}
      threshold={0.5}
      bind:count
      bind:index
      bind:offset
      bind:progress
    >
      <div slot="foreground">
        <section class="centered-content">
          <p>Example text: Twitter has played an increasingly prominent role in the 2016 US Presidential Election. Debates have raged and candidates have risen and fallen based on tweets. </p>
          <p>This dataset provides approximately 3000 recent tweets from Hillary Clinton and Donald Trump, the two major-party presidential nominees.</p>
        </section>
        <section class="centered-content">This is the second section.</section>
        <section class="centered-content">This is the third section.</section>
        <section class="centered-content">
          <div>
            <div class="centered-content">
            <p>Type in a word to see how many time it appears in each nominees' tweet</p>
            <p>Remember, the frequency is out of ~3000 tweets for each of them. And is counting how many tweets contained the word of your choice </p>
            <p>Take your time to explore the topic you want! </p>
            <div class="input-container">
              <input type="text" bind:value={inputText} placeholder="Type in a word" />
            </div>
            {#if if_empty}
              <p>Try different word!</p>
            {/if}
            <div class="suggestions">
              {#each top_five_words as word}
                <button on:click={() => handleClick(word)}>{word}</button>
              {/each}
            </div>
          </div>
          </div>
        </section>
      </div>
    </Scroller>
  </div>

<div class="header">
  <h1 class="sectionHeader">Campaigning on Twitter</h1>
  <p class="introText">Twitter has played an increasingly prominent role in the 2016 US Presidential Election. Debates have raged and candidates have risen and fallen based on tweets. This dataset provides approximately 3000 recent tweets from Hillary Clinton and Donald Trump, the two major-party presidential nominees.</p>
</div>

<style>
  .header {
    position: absolute;
    left:0;
    width: 101vw;
    height: 60vh;
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    background-color: #0073d8;
    color: #ffffff;
    z-index: 99;
    top: 0px;
  }

  .sectionHeader {
    font-size: 3.5em;
    margin: 0;
    text-align: center;
  }
  .introText {
    font-size: 1em;
    max-width: 50%;
  }

.left-panel {
  left:0;
  top:0;
  position:fixed;
  height:100vh;
  width: 65%;
  background-color: rgba(95, 141, 170, 0.502);
}
.right-panel {
    position: absolute;
    right: 0;
    top:60vh;
    width: 36%;
    margin-right: -1vw;
    background-color: #ffffff80;
  }

  section {
    min-height: 110vh; 
    color: black;
    background-color: #4ba9e380;
  }

  .centered-content {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
}
  p {
    font-family: "Times New Roman", Times, serif;
    line-height: 2;
    max-width: 70%;
  }
  .suggestions {
  display: flex;
  flex-direction: column;
}
.suggestions button {
  width: 150px;
  height: 25px;
  background-color: rgb(243, 243, 251);
  background-color: #f0f0f0; 
  border: 0.7px solid #d0d0d0e2; 
  font-size: 15px;
  border-radius: 0.2em;
}
.suggestions button:hover {
  opacity: 0.7;
}

.graph-container {
  margin-top: 160px; 
}
input {
  width: 147px;
  border: 1px solid #ccc;
  padding: 9px;
  font-size: 15px;
  transition: width 0.2s;
  border-radius: 1em;
}

</style>
