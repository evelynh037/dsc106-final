<script>
  import Scroller from "@sveltejs/svelte-scroller";
  let count, index, offset, progress;
</script>
<div class="header">
  <h1 style="text-align: center" class="sectionHeader">Campaigning on Twitter</h1>
</div>

<div class="container">
  <div class="right-panel">
    <section class="centered-content">
      graph
    </section>
  </div>
  <div class="left-panel">
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
          <p>Example text: Twitter has played an increasingly prominent role in the 2016 US Presidential Election. Debates have raged and candidates have risen and fallen based on tweets.   This dataset provides approximately 3000 recent tweets from Hillary Clinton and Donald Trump, the two major-party presidential nominees.</p>
        </section>
        <section class="centered-content">This is the second section.</section>
        <section class="centered-content">This is the third section.</section>
        <section class="centered-content">This is the fourth section.</section>
      </div>
    </Scroller>
  </div>
</div>

<style>
  .container {
    display: flex;
    height: 100vh; 
  }

  .right-panel {
  width: 60%; 
  height: 100vh; 
  background-color: #18a5d880;;
  justify-content: center;
  align-items: center;
}

  .left-panel {
    width: 40%;
    overflow: auto; 
  }

  section {
    min-height: 100vh; 
    background-color: #81d5f380;
    max-width: 750px;
    color: black;
  }
  .centered-content {
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100vh;
}

p {
  font-family: "Times New Roman", Times, serif;
  line-height: 2;
  max-width: 70%;
}
</style>





