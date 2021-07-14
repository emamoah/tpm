<template>
  <v-card link outlined
    class="pa-1"
    :to="`/db/${dbkey}?name=${dbname}`"
  >
    <v-card-title
      class=""
      style="word-break: unset"
    >
      <span>{{ dbname }}</span>
    </v-card-title>
    <v-card-text class="db-info">
      <span class="info-key">Engine:</span>
      <span class="info-val">{{ dbengine }}</span>
    </v-card-text>
  </v-card>
</template>

<script>
export default {
  name: 'DBCard',
  props: ['dbname', 'dbkey', 'dbengine']
}
</script>

<style lang="scss" scoped>
.db-info {
  display: grid;
  grid-template: none / max-content 1fr;
  gap: 0 16px;
  .info-key {
    font-weight: 500;
  }
  .info-val {
    font-weight: 300;
  }
}

.db-engine-chip {
  font-weight: 500;
}

.status {
  text-transform: lowercase;
  font-weight: 400 !important;
  &::before {
    content: '';
    display: inline-block;
    vertical-align: middle;
    width: .6em;
    height: .6em;
    border-radius: 50%;
    margin-right: .3em;
    position: relative;
  }
  &.online {
    color: green;
    &::before {
      background: green;
    }
  }
  &.offline {
    opacity: .5;
    &::before {
      background: #aaa;
    }
  }
}
</style>