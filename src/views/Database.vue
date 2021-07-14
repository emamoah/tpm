<template>
  <div class="database">
    <h1>{{ $route.query.name }}</h1>
    <div class="table-container pa-2 ma-n2">
      <v-data-table
        :loading="loading"
        :headers="headers"
        :items="items"
        :items-per-page="10"
      ></v-data-table>
    </div>
  </div>
</template>

<script>
import remoteConfig from '@/config/remoteConfig'

export default {
  name: 'Database',
  data: () => ({
    loading: true,
    headers: [],
    items: []
  }),
  created() {
    let dbkey = this.$route.params.dbkey;
    let { baseUrl } = remoteConfig;
    let endpoint = `${baseUrl}/${dbkey}/data`;

    console.log('fetching from: ', endpoint);

    fetch(endpoint)
      .then(res => {
        return res.json();
      })
      .then(data => {
        console.log(data.data);
        this.headers = data.data.headers;
        this.items = data.data.payload;
        this.loading = false;
      })
      .catch(err => {
        console.log('There was an error getting table info: ',  err);
        this.loading = false;
      });
  },
  mounted() {
  },
}
</script>

<style lang="scss" scoped>
div.database {
  height: calc(100% - 16px);
  max-height: calc(100% - 16px);
  display: grid;
  grid-template: auto 1fr / none;
  gap: 16px 0;
}
div.table-container {
  overflow: auto;
}
</style>