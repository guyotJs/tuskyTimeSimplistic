<script>
  import tt from './tt.json';
  import Header from './lib/Header.svelte';
  let active = false;
  function toggle(){
    if(active){active = false;}
    else{active = true;}
  }
  let months = ['January','Febuary','March','April','May','June','July','August','September','October','November','December']
  let monthNum = [31,28,31,30,31,30,31,31,30,31,30,31]

  let date = new Date();
  let day = date.getDate();
  let month = date.getMonth();
  let year = date.getFullYear();
  let dateString;
  function prev(){month --; if(month < 0){year --; month = 11}}
  function post(){month ++; if(month > 11){year ++; month = 0}}
  function compileTT(){
    if(day <= 9 ){
      return year + "-" + (month+1) + "-0" + day;
    }else{
      return year + "-" + (month+1) + "-" + day;
    }
  }
  
  function select(input){
    day = input;
    dateString = compileTT();
  }
  dateString = compileTT();
</script>
<link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/4.7.0/css/font-awesome.min.css">
<style>
h1{
  font-size: 50px;
}
</style>
<main>
  <Header/>
  <div class="options">
    TODAY 
  {#if tt[dateString] != undefined}
    IS 
    {#if tt[dateString].day == "A"}
      AN
      {:else}
      A
    {/if}<br/>
    <h1>{tt[dateString].day}</h1>
    DAY<br/>
    AND TODAY IS TUSKY TIME<br/>
    <h1>{tt[dateString].TT}</h1>
    {:else}
    THERE IS NO SCHOOL
  {/if}
  </div>

  <div class="custom-date">
    <div class="selected"  on:click={toggle}>
      &nbsp;<i class="fa fa-calendar" style="font-size:20px"></i>&nbsp;{dateString.replace(/-/g,'/')}
    </div>
    <div class="dates {active ? 'active' : ''}">
      <div class="month">
        <div class="arrows prev" on:click={prev}>&lt;</div>
        <div class="mth">{months[month]+ ' ' + year}</div>
        <div class="arrows next" on:click={post}>&gt;</div>
      </div>
      <div class="days">
        {#each Array(monthNum[month]) as _, i}
            {#if day <= 9}
              <div class="day {year+"-"+(month+1)+"-0"+(i+1) == dateString ? 'daySelect' : ''}" on:click={() => select(i+1)}>{(i+1).toString()}</div>
              {:else}
              <div class="day {year+"-"+(month+1)+"-"+(i+1) == dateString ? 'daySelect' : ''}" on:click={() => select(i+1)}>{(i+1).toString()}</div>
            {/if}
        {/each}
      </div>
    </div>
  </div>
</main>