<template>
  <Layout>
    <v-container>
        <h1 class="horiz-center">Finder</h1>

        <client-only>
          <ais-instant-search :index-name="indexName"
                              :search-client="searchClient" class="horiz-center searchbox">

            <ais-configure :hits-per-page.camel="8"/>

            <ais-powered-by/>
            <ais-search-box/>

            <ais-hits class="clear-above">
              <div slot-scope="{ items }">
                <v-layout d-flex flex-wrap>
                  <v-row d-flex cols="1">
                    <v-col cols="12" md="3"
                           class="d-flex child-flex"
                           v-for="(item, index) in items" :key="index">
                      <JoseCard :repo="{ title: item.title, name:
                  item.name, nameWithOwner: item.nameWithOwner,
                  description: item.description, cardImage: item.cardImage,
                  summaryDoc: item.cardSummary, summaryImage: item.cardImage }"/>
                    </v-col>
                  </v-row>
                </v-layout>
              </div>
            </ais-hits>

          </ais-instant-search>
        </client-only>
    </v-container>
  </Layout>
</template>

<script>

  import algoliasearch from 'algoliasearch'
  import store from '~/store'
  import JoseCard from '../components/JoseCard'

  export default {
    metaInfo: {
      title: 'Finder'
    },
    data: function () {
      return {
        numberRepos: 3,
        indexName: store.getters.algoIndexName,
        searchClient: algoliasearch(
          store.getters.algoAppId,
          store.getters.algoSearchKey
        )
      }
    },
    components: { JoseCard },
  }
</script>

<style scoped>
  .horiz-center {
    margin: 0 auto;
    text-align: center;
  }
  .searchbox {
    margin: 15px;
  }
  .low-attention {
    font-size: x-small;
  }
  .clear-above {
    margin-top: 10px;
  }
</style>
