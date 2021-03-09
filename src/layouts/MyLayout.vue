<template>
  <q-layout view="hHh Lpr fFf">
    <!-- Be sure to play with the Layout demo on docs -->

    <!-- (Optional) The Header -->
    <q-header elevated class="row justify-start">
      <q-toolbar class="col">
        <q-toolbar-title>
          Stores
        </q-toolbar-title>
      </q-toolbar>
    </q-header>

    <q-page-container>
      <!-- This is where pages get injected -->
      <h4 class="text-center">
        Welcome to our stores
      </h4>

      <div class="q-pa-md row q-gutter-md justify-evenly">
        <card v-for="store in stores" :store="store" :key="store.id"></card>
      </div>
    </q-page-container>
  </q-layout>
</template>

<script>
import { mapGetters, mapActions } from "vuex";

export default {
  // name: 'LayoutName',
  data() {
    return {};
  },
  computed: {
    ...mapGetters("storesModule", { stores: "getStores" })
  },
  methods: {
    ...mapActions["storesModule/updateStores"],
    showInfo(store) {
      this.$q.dialog({
        title: `${store.name} (${store.storeType})`,
        message: `Location: ${store.address} ${store.postCode} ${store.city} ${store.countryCode}`
      });
    }
  },
  async created() {
    const storesRequest = await this.$axios.get(
      "https://demoapi.thedenstore.com/api/service?Request=Stores&amp;Language=en-us"
    );
    this.$store.dispatch("storesModule/updateStores", storesRequest.data);
  },
  components: {
    card: require("components/card.vue").default
  }
};
</script>
