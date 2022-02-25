<template>
  <v-container>
    <h1>Axion</h1>
    <h2>Covid-19</h2>
    <v-btn depressed color="primary" @click="loadData()">
      รายงานสถานการณ์ COVID-19 ประจำวัน
    </v-btn>
    <v-btn depressed color="primary" class="mx-3" @click="loadDataCity()">
      รายงานสถานการณ์ COVID-19 ประจำวัน แยกตามรายจังหวัด
    </v-btn>
    <v-btn
      depressed
      color="primary"
      class="mx-3 my-5"
      @click="(httpdata = ''), (cityData = '')"
    >
      ลบข้อมูลทั้งหมด
    </v-btn>
    <p>{{ httpdata }}</p>
    <div class="d-flex flex-wrap">
      <v-card
        class="mx-auto my-5"
        max-width="344"
        outlined
        v-for="(item, index) in cityData"
        :key="index"
      >
        <v-list-item three-line>
          <v-list-item-content>
            <v-list-item-title class="text-h5 mb-1">
              {{ item.province }}
            </v-list-item-title>
            <v-list-item-subtitle class="black--text text-body-1">
              New Case:
              <samp class="red--text mr-5">{{ item.new_case }}</samp> Total
              Case:
              <samp class="red--text">{{
                item.new_case_excludeabroad
              }}</samp></v-list-item-subtitle
            >
            <v-list-item-subtitle class="black--text"> </v-list-item-subtitle>
          </v-list-item-content>
        </v-list-item>

        <v-card-actions>
          <v-btn outlined rounded text> Button </v-btn>
        </v-card-actions>
      </v-card>
    </div>
  </v-container>
</template>

<script>
import axios from "axios";
export default {
  data() {
    return {
      httpdata: "",
      cityData: "",
    };
  },
  methods: {
    loadData() {
      axios
        .get("https://covid19.ddc.moph.go.th/api/Cases/today-cases-all")
        .then((result) => {
          this.httpdata = result.data;
        });
    },
    loadDataCity() {
      axios
        .get(
          "https://covid19.ddc.moph.go.th/api/Cases/today-cases-by-provinces"
        )
        .then((result) => {
          this.cityData = result.data;
        });
    },
  },
  mounted() {},
  created() {},
};
</script>

<style></style>
