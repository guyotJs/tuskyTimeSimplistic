<script>
  import tt from './tt.json';
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
  let selectedDate = date;
  let selectedMonth = month;
  let selectedDay = day;
  let selectedYear = year;
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
<main>
  <h1>Buskybime</h1>
  <div class="custom-date">
    <div class="selected"  on:click={toggle}>
      {dateString}&nbsp; <i class="fa fa-calendar" style="font-size:20px"></i>
    </div>

    <div class="dates {active ? 'active' : ''}">

      <div class="month">
        <div class="arrows prev" on:click={prev}>&lt;</div>
        <div class="mth">{months[month]+ ' ' + year}</div>
        <div class="arrows next" on:click={post}>&gt;</div>

      </div>
      <div class="days">
        {#each Array(monthNum[month]) as _, i}
            <div class="day" on:click={() => select(i+1)}>{(i+1).toString()}</div>
        {/each}
      </div>
      
    </div>
  </div>
  {dateString}
  {#if tt[dateString] != undefined }
    {tt[dateString].TT}{:else}NO SCHOOL you absolute BUFFOON
  {/if}
  <br/>{day}
</main>