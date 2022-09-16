<template>
  <input type="text" @keydown.enter="$emit('add-section-list',$event)">
</template>
