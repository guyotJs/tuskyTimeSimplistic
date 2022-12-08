<script>
  import tt from './lib/tt.json';
  var today = new Date();
  var dd = today.getDate();
  var mm = today.getMonth()+1;
  var yyyy = today.getFullYear();
  var dateString;
  var input;
  if(dd <= 9){
    dateString = yyyy+"-"+mm+"-"+"0"+dd
    input = yyyy+"-"+mm+"-"+"0"+dd
  }else{
    dateString = yyyy+"-"+mm+"-"+dd
    input = dateString = yyyy+"-"+mm+"-"+dd
  }
  function changeDay(){
    dateString = input
  }
</script>
<style>
  .btn{background-color: white; border: 1;border-radius: 5px;}
</style>
<main>
  Today is
  {#if tt[dateString] != undefined}
  {#if tt[dateString].day == "A"}
    an{:else}a
  {/if}<br/>
  {tt[dateString].day}<br/>
  day<br/>
  And it's Tuskytime<br/>
  {(tt[dateString].TT).replace("TT",'')}
  {:else}
  <br/>NO SCHOOL<br/>You absolute BUFFOON
  {/if}
  <form>
    <input type="date" id="birthday" class="btn" name="birthday" bind:value={input}>
    <input type="submit" value="Select" class="btn" on:click|preventDefault={changeDay}>
  </form>
</main>