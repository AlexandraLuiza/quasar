<template>
  <q-card
    dark
    bordered
    class="bg-red-9 col-xs-12 col-sm-5 col-md-3"
    @click="showInfo(store)"
  >
    <q-card-section>
      <div class="text-h6">{{ store.name }}</div>
    </q-card-section>
  </q-card>
</template>

<script>
export default {
  props: ["store"],
  methods: {
    showInfo(store) {
      this.$q.dialog({
        title: `${store.name} (${store.storeType})`,
        message: `Location: ${store.address} ${store.postCode} ${store.city} ${store.countryCode}`
      });
    }
  }
};
</script>
