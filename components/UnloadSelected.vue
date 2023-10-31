<template>
    <div class="selected">
        <div class="selected__top">
            <div class="selected__info">
                <div class="selected__id">{{selected.obj.id}}</div>
                <div class="selected__name" v-html="selected.obj.event"></div>
            </div>
            <div class="selected__close" @click="selectCard('hide')">
                <svg width="35" height="50" viewBox="0 0 48 48" fill="none" xmlns="http://www.w3.org/2000/svg">
                    <rect width="48" height="48" fill="white" fill-opacity="0.01"/>
                    <path d="M14 14L34 34" stroke="#fff" stroke-width="3" stroke-linecap="round" stroke-linejoin="round"/>
                    <path d="M14 34L34 14" stroke="#fff" stroke-width="3" stroke-linecap="round" stroke-linejoin="round"/>
                </svg>
            </div>
        </div>
        <div class="block">
            <div class="prompt">
                <i class="fa-solid fa-lightbulb"></i>
                Если после клика на ссылку загрузка не пошла, проверьте не блокирует ли браузер скачивание архива.
            </div>
            <h3 class="text-bold link-title text-16px">Ссылка для скачивания архива Выгрузки (.zip):</h3>
            <a :href="selected.obj.download_link" download class="link">{{selected.obj.download_link}}</a>
            <a class="span-link" @click="copyLink(selected.obj.download_link)">cкопировать ссылку</a>
            <div class="selected__close"><span @click="selectCard('hide')">Закрыть</span></div>
        </div>
    </div>
</template>

<script>
  export default {
    props: {
      selected: {
        type: Object,
      },
    },
    emits: ['hide-select'],
    methods: {
      selectCard(btnEvent) {
        if (btnEvent === 'hide') {
          this.$emit('hide-select');
        }
      },
      copyLink(link) {
        navigator.clipboard.writeText(link);
        document.execCommand('copy');
      }
    }
  }
</script>
