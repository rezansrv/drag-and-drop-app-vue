<template>
    <div class="drag-zone" @drop="onDrop($event , 1)" @dragenter.prevent @dragover.prevent>
      <div v-for="item in getList(1)" :key="item.id" class="drag-el" draggable="true" @dragstart="startDrag($event, item)">
        {{ item.title }}
      </div>
    </div>
    <div class="drag-zone" @drop="onDrop($event , 2)" @dragenter.prevent @dragover.prevent>
      <div v-for="item in getList(2)" :key="item.id" class="drag-el" draggable="true" @dragstart="startDrag($event, item)">
        {{ item.title }}
      </div>
    </div>
    <div class="drag-zone" @drop="onDrop($event , 3)" @dragenter.prevent @dragover.prevent>
      <div v-for="item in getList(3)" :key="item.id" class="drag-el" draggable="true" @dragstart="startDrag($event, item)">
        {{ item.title }}
      </div>
    </div>
  </template>
  
  <script setup>
  const items = ref([
    {id: 0, title: 'Item A', list: 1},
    {id: 1, title: 'Item B', list: 1},
    {id: 2, title: 'Item C', list: 2},
    {id: 3, title: 'Item D', list: 2},
    {id: 4, title: 'Item E', list: 3},
  ])
  
  function getList(list) {
    return items.value.filter((item) => item.list == list)
  }
  
  function startDrag(event, item) {
    event.dataTransfer.dropEffect = 'move';
    event.dataTransfer.effectAllowed = 'move';
    event.dataTransfer.setData('itemID', item.id)
  }
  
  function onDrop(event , list){
    const itemID = event.dataTransfer.getData('itemID');
    const item = items.value.find((item) => item.id == itemID);
    item.list = list;
  }
  </script>
  
  <style scoped>
  .drag-zone {
    width: 50%;
    margin: 50px auto;
    background-color: #ecf0f1;
    padding: 10px;
    min-height: 10px;
  }
  
  .drag-el {
    background-color: #3498db;
    color: white;
    padding: 5px;
    cursor: pointer;
    margin-bottom: 10px;
  }
  
  </style>