<template>
  <q-layout view="lHh Lpr lFf">
    <q-header elevated>
      <q-toolbar class="flex bg-white q-py-md">
        <strong class="text-accent text-h5 q-mr-lg">Kaiinos</strong>
        <q-input rounded standout="bg-white" v-model="search" class="search-field" dense label="Search">
          <template v-slot:append>
            <q-btn
              unelevated
              rounded
              style="min-width: 70px;"
              color="accent"
              icon="search"
            />
          </template>
        </q-input>
        <div class="btns q-ml-auto">
          <q-btn outline rounded color="accent" class="q-mr-sm" no-caps icon="mail" label="Mail" />
          <q-btn outline rounded color="accent" class="q-mr-sm" no-caps label="Sign in" />
          <q-btn outline round color="accent" no-caps icon="person" style="min-height: 35px; min-width: 35px;" />
        </div>
      </q-toolbar>
    </q-header>

    <q-drawer
      v-model="leftDrawerOpen"
      show-if-above
      bordered
      class="bg-accent main-drawer"
      :mini="miniState"
    >
      <q-btn
        flat
        dense
        round
        icon="menu"
        aria-label="Menu"
        @click="toggleLeftDrawer"
        size="lg"
        class="q-ml-xs q-mt-sm"
      />
      <q-list>
        <EssentialLink
          v-for="link in linksList"
          :key="link.title"
          v-bind="link"
        />
      </q-list>
    </q-drawer>

    <q-page-container>
      <router-view />
    </q-page-container>
  </q-layout>
</template>

<script>
import { defineComponent } from "vue";
import EssentialLink from "components/EssentialLink.vue";

const linksList = [
  {
    title: "Docs",
    caption: "quasar.dev",
    icon: "school",
    link: "https://quasar.dev",
  },
  {
    title: "Github",
    caption: "github.com/quasarframework",
    icon: "code",
    link: "https://github.com/quasarframework",
  },
  {
    title: "Discord Chat Channel",
    caption: "chat.quasar.dev",
    icon: "chat",
    link: "https://chat.quasar.dev",
  },
  {
    title: "Forum",
    caption: "forum.quasar.dev",
    icon: "record_voice_over",
    link: "https://forum.quasar.dev",
  },
  {
    title: "Twitter",
    caption: "@quasarframework",
    icon: "rss_feed",
    link: "https://twitter.quasar.dev",
  },
  {
    title: "Facebook",
    caption: "@QuasarFramework",
    icon: "public",
    link: "https://facebook.quasar.dev",
  },
  {
    title: "Quasar Awesome",
    caption: "Community Quasar projects",
    icon: "favorite",
    link: "https://awesome.quasar.dev",
  },
];

export default defineComponent({
  name: "MainLayout",

  components: {
    EssentialLink,
  },

  data() {
    return {
      search: "",
      linksList,
      leftDrawerOpen: true,
      miniState: true,
    };
  },

  methods: {
    toggleLeftDrawer() {
      this.miniState = !this.miniState;
    },
  },
});
</script>

<style lang="scss">
.main-drawer {
  color: white;
}
.search-field {
  max-width: 480px;
  width: 100%;
  .q-field__control {
    padding-right: 0;
  }
}
</style>
