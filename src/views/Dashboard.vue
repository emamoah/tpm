<template>
  <div class="dashboard">
      <h1>Databases</h1>
      <div class="cards-row-container pa-2 ma-n2">
        <p class="placeholder-text" v-if="loading">Loading items...</p>
        <p class="placeholder-text" v-else-if="!dbs.length">No data available.</p>
        <DBCard
          v-for="db in dbs"
          :key="db.id"
          :dbname="db.name"
          :dbkey="db.key"
          :dbengine="db.engine"
        />
      </div>
  </div>
</template>

<script>
import DBCard from '@/components/DBCard'
import remoteConfig from '@/config/remoteConfig'

export default {
  name: 'Dashboard',
  components: { DBCard },
  data: () => ({
    loading: true,
    dbs: []
  }),
  created() {
    let { baseUrl } = remoteConfig;
    let endpoint = `${baseUrl}/nia/info`;

    console.log('fetching from: ', endpoint);

    fetch(endpoint)
      .then(res => {
        return res.json()
      })
      .then(data => {
        this.dbs = data.data;
        console.log(data.data);
        this.loading = false;
      })
      .catch(err => {
        console.log('An error occured while fetching databases: ', err);
        this.loading = false;
      });
  }
}
</script>

<style scoped lang="scss">
div.dashboard {
  height: calc(100% - 16px);
  max-height: calc(100% - 16px);
  display: grid;
  grid-template: auto 1fr / none;
  gap: 16px 0;
  .cards-row-container {
    overflow-y: auto;
    display: grid;
    align-content: start;
    gap: 24px;
  }
  @media screen and (min-width: 600px) {
    .cards-row-container {
      grid-template-columns: 1fr 1fr;
    }
  }
  @media screen and (min-width: 960px) {
    .cards-row-container {
      grid-template-columns: repeat(3, 1fr);
    }
  }
  @media screen and (min-width: 1264px) {
    .cards-row-container {
      grid-template-columns: repeat(4, 1fr);
    }
  }
}

.placeholder-text {
  color: rgba(0, 0, 0, .54);
}
</style>