<script>
  export let courseGoal;
  $: shouldHighlight = courseGoal.includes('!')
</script>

<!-- <h1 class="header" class:header-alt="{courseGoal.includes("!")}">{courseGoal}</h1> -->
<h1 class="header" class:header-alt="{shouldHighlight}">{courseGoal}</h1>

<style>
  .header {
    font-size: 1rem;
  }
  .header-alt{
    color: red;
  }
</style>
