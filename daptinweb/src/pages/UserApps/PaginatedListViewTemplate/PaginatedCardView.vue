<template>
  <div id="dropArea" class="row">
    <div class="col-1 col-xs-3 col-sm-2 col-md-1 col-xl-1" @touchstart.stop @contextmenu.stop style="padding: 8px"
         v-for="item in items" v-if="item.is_dir">
      <q-menu context-menu>
        <q-list dense style="min-width: 100px">
          <q-item clickable v-close-popup>
            <q-item-section>Open</q-item-section>
          </q-item>
          <q-item cl ickable v-close-popup>
            <q-item-section>Rename</q-item-section>
          </q-item>
          <q-separator/>
          <q-item @click="deleteItem(item)" clickable v-close-popup>
            <q-item-section>Delete</q-item-section>
          </q-item>
          <q-separator/>
          <q-separator/>
        </q-list>
      </q-menu>
      <q-card @click="itemClicked(item)" class="table-item" flat :style="{cursor: 'pointer', color: item.color}">
        <q-tooltip :delay="1000">{{ item.name }}</q-tooltip>
        <q-card-section class="text-center" avatar>
          <q-icon size="2.5em" :name="item.icon"/>
        </q-card-section>
        <q-card-section class="text-center text-white" style="padding: 1px; overflow-wrap: anywhere; overflow: hidden">
          {{ item.name.substring(0, item.name.length > 20 ? 20 : item.name.length) }}
        </q-card-section>
      </q-card>
    </div>
    <div class="col-1 col-xs-3 col-sm-2 col-md-1 col-xl-1" @touchstart.stop @contextmenu.stop style="padding: 8px"
         v-for="item in items" v-if="!item.is_dir">
      <q-menu context-menu>
        <q-list dense style="min-width: 100px">
          <q-item clickable v-close-popup>
            <q-item-section>Open</q-item-section>
          </q-item>
          <q-item cl ickable v-close-popup>
            <q-item-section>Rename</q-item-section>
          </q-item>
          <q-separator/>
          <q-item @click="deleteItem(item)" clickable v-close-popup>
            <q-item-section>Delete</q-item-section>
          </q-item>
          <q-separator/>
          <q-separator/>
        </q-list>
      </q-menu>
      <q-card @click="itemClicked(item)" class="table-item" flat :style="{cursor: 'pointer', color: item.color}">
        <q-tooltip :delay="1000">{{ item.name }}</q-tooltip>
        <q-card-section class="text-center" avatar>
          <q-icon size="2.5em" :name="item.icon"/>
        </q-card-section>
        <q-card-section class="text-center text-white" style="padding: 1px; overflow-wrap: anywhere; overflow: hidden">
          {{ item.name.substring(0, item.name.length > 20 ? 20 : item.name.length) }}
        </q-card-section>
      </q-card>
    </div>
  </div>
</template>
<style>
.table-item:hover {
  background: rgb(80, 80, 90);
}

.table-item {
  border-radius: 5px;
  background: transparent;
}
</style>
<script>
import {mapActions} from "vuex";

export default {
  name: "PaginatedCardView",
  props: ["items"],
  methods: {
    deleteItem(item) {
      console.log("Item deleted", item)
      this.$emit('item-deleted', item)
    },
    itemClicked(item) {
      console.log("Item clicked", item)
      this.$emit('item-clicked', item)
    },
    ...mapActions([]),
    refreshData() {
      const that = this;
    }
  },
  mounted() {
    console.log("Mounted paginated table view", this.parameters);
    const that = this;
    that.refreshData();

  }
}
</script>
