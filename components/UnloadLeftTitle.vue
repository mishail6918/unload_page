<template>
    <div class="title-card block">
        <h2 class="text-bold title-card__heading">{{title}}</h2>
        <div class="text-bold title-card__subheading">{{subTitle}}</div>
        <ul class="title-card__list">
            <li v-for="(item, idx) of list" :key="idx">{{item}}</li>
        </ul>
    </div>
</template>

<script>
    export default {
      props: {
        title: {
          type: String,
        },
        subTitle: {
          type: String
        },
        list: {
          type: Array
        }
      }
    }
</script>
