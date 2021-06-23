<script>
  let chosen = 0;

  const choose = (e) => {
    chosen = Math.floor(Math.random() * 120 + 1);
    console.log(chosen);
  }
 </script>
 <div class="randomize-box">
  <p class="chosen">{chosen}</p>
  <button class="btn" on:click={choose}>Choose</button>
 </div>
