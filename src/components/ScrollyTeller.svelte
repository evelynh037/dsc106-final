<script>
  import Scroller from "@sveltejs/svelte-scroller";
  import { onMount } from 'svelte';
  import * as d3 from 'd3';
  let count, index, offset, progress;
  $:console.log(index)

  //load data
  let hillaryData = [];
  onMount(async () => {
    const res = await fetch('hillary_words.csv'); 
    const csv = await res.text();
    hillaryData = d3.csvParse(csv, d3.autoType)
  });
  let trumpData = [];
  onMount(async () => {
    const res = await fetch('trump_words.csv'); 
    const csv = await res.text();
    trumpData = d3.csvParse(csv, d3.autoType)
  });

 //for searchbox, filter data 
  let prefix = "no input";
  let inputText = "";
  let showWarning = false;
  let filtered_hillary;
  let filtered_trump;
  function handleSubmit() {
    if (inputText == '') {
      showWarning = true;
    } else {
      prefix = inputText;
      showWarning = false;
      console.log(prefix)
    }
  }
  $: filtered_hillary = hillaryData.filter((d) => d.Word == prefix.toLowerCase());
  $: filtered_trump = trumpData.filter((d) => d.Word == prefix.toLowerCase());
</script>


<div class="container">
  <div class="left-panel">
    <section>graph</section>
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
            <div class="input-container">
              <input type="text" bind:value={inputText} placeholder="Type in a word" />
              <button on:click={handleSubmit}>Submit</button>
            </div>
            
            {#if showWarning}
              <div class="warning-message">
                <p1>Where is the word? try again :p</p1>
              </div>
            {/if}
            
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
  .container {
  width:100%;
  display: flex;
  flex-direction: row;
  min-height: 100vh;
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
    height: calc(200vh);
  }

  section {
    min-height: 100vh; 
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
</style>
