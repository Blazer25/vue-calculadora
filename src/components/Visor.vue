<template>
  <div class="visor">
      {{ valor }}
  </div>
</template>

<script>
export default {
    name: 'Visor-',
    props:['valor']
}
</script>

<style>
    .visor{
        grid-column: span 4;
        display: flex;
        color: white;
        background-color: black;
        justify-content: flex-end;
        align-items: center;
        padding: 15px;
        overflow: hidden;
        font-size: 2rem;
    }
</style>
