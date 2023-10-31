<template>
  <main>
    <section class="unload">
      <div class="unload__left">
        <UnloadLeftTitle :title="'Выгрузка'" :sub-title="'Выполняет работу:'" :list="list"/>
        <div class="notice" v-if="selected.id === ''" data-color="light-purple">
          Для того, чтобы просмотреть информацию о выгрузке, а также ее скачать, нажмите на треюбуемую выгрузку в столбце слева.
        </div>
        <UnloadSelected v-if="selected.id !== ''" :selected="selected" @hide-select="hideSelectCard"/>
        <UnloadLeftCard
                v-for="(item, idx) of values"
                v-show="selected.id !== idx"
                :key="item.id" :item="item"
                @click="selectCard(idx, 'show')"/>
      </div>
      <div class="unload__right">
        <div class="notice" v-if="selected.id === ''" data-color="light-purple">
          Для того, чтобы просмотреть информацию о выгрузке, а также ее скачать, нажмите на треюбуемую выгрузку в столбце слева.
        </div>
        <UnloadSelected v-if="selected.id !== ''" :selected="selected" @hide-select="hideSelectCard"/>
      </div>
    </section>
  </main>
</template>

<script setup>
  import "~/assets/styles/pages/unload.scss";
  import { useAPIFetch } from "../../composables/useAPIFetch";

  const list = reactive(['Собирает фотографии из заказов пользователей.', 'Выгружает по папкам']);
  const selected = reactive({id: '', obj: {}});

  let { data: values } = await useAPIFetch('https://dev-cabinet.seenday.com/e.scripts?page=pages:unload&event=get', {
    onResponse({response}) {
      values = JSON.parse(response._data).response.data;
    },
  });

  function selectById(id) {
    let { data: selectValue } = useAPIFetch('https://dev-cabinet.seenday.com/e.scripts?page=pages:unload&event=get&unload_id=' + values[id].id, {
      onResponse({ response }) {
        selectValue = JSON.parse(response._data).response.data;
        selected.obj = selectValue[0];
      },
    });
  }

  function selectCard(id, btnEvent) {
    if (btnEvent === 'show') {
      selected.id = id;
      selectById(id);
    }
  }

  function hideSelectCard() {
    selected.id = '';
  }
</script>
