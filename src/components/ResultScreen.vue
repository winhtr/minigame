<template>
  <div class="screen">
    <h1>✨ Congratulations ✨</h1>
    <p> {{Math.round(timer / 1000)}} seconds </p>
    <button> Start again </button>
  </div>
</template>

<script>
export default {
    props: {
        timer: {
            type: Number,
            required: true,
        }
    }

}
</script>

<style>

</style>