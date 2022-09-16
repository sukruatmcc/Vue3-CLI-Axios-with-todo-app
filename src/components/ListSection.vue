<template>
  <li v-for="item in itemList" :key="item" class="d-flex justify-content-between align-items-center text-black">
    {{item.title}}
    <button @click="$emit('on-delete',item)" class="red">Delete</button>
  </li>
</template>
<script>
export default {
  props:['itemList']
}
</script>
