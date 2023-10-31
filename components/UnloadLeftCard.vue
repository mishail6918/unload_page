<template>
    <div class="block item-card" :id="item.id" :class="item.status">
        <div v-html="item.task_date"></div>
        <div>Статус выгрузки: <span class="text-bold">{{item.status_text}}</span></div>
        <div>ID выгрузки: <span class="text-bold">{{item.id}}</span></div>
        <div v-html="item.event"></div>
        <div>Размер выгрузки <span class="text-bold">{{item.size}}</span></div>
    </div>
</template>

<script>
  export default {
    props: {
      item: {
        type: Object,
      },
    }
  }
</script>
