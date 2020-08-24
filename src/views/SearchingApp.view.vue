<template>
  <div class="container mx-auto text-center">
    <div class="flex justify-center my-16">
      <form>
        <div class="inline">
          <search-box v-model="searchValue" v-on:change="filtering"/>
          <p
            v-if="this.searchValue.length > 0"
            class="char inline p-3 rounded-lg ml-2 bg-teal-400 text-white"
          >{{ searchValue.length }}</p>
          <p
            v-if="this.searchValue.length > 0 && this.searchValue.length < 3"
            class="bg-red-200 rounded-lg mt-2"
          >{{ message.character }}</p>
          <p
            v-if="this.message.loading"
            class="bg-blue-200 rounded-lg mt-2"
          >Sedang mencari...</p>
        </div>
      </form>
    </div>
    <list-rendering :data="filteringData"/>
  </div>
</template>
<script>
// import Data Dummy
import dataDummy from "@/dummy/dataDummy.js"
// import Component
import SearchBox from "@/components/SearchBox.vue"
import ListRendering from "@/components/ListRendering.vue"

export default {
    name: "SearchingApp",
    components: {
        SearchBox,
        ListRendering
    },
    data() {
        return {
            message: {
                character: "",
                loading: false,
            },
            filteringData: [],
            searchValue: "",
            jsonItem: dataDummy,
        };
    },
    created() {
        this.filtering()
    },
    methods: {
        filtering() {
            const lengthValue = this.searchValue.length
            const resultFilter = this.jsonItem.filter(data => data.title
                .toLowerCase()
                .includes(this.searchValue.toLowerCase()));

            if (lengthValue > 0 && lengthValue < 3) {
                this.message.character = "Minimal Character 3 Huruf";
                this.filteringData = []
            } else if (lengthValue >= 3) {
                setTimeout(() => {
                    this.message.loading = true;
                }, 200);
                setTimeout(() => {
                    this.message.loading = false;
                }, 500);
                this.filteringData = resultFilter
            } else {
                this.filteringData = this.jsonItem
            }
        }
    }
};
</script>
