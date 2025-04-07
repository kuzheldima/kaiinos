<template>
  <q-page class="body-background sla">
    <div class="full-width flex items-center q-px-md q-py-xs">
      <div class="breadcrumbs">
        <q-breadcrumbs>
          <q-breadcrumbs-el label="Home" />
          <q-breadcrumbs-el label="Block Load Data" />
        </q-breadcrumbs>
      </div>
      <div class="btns-group q-ml-auto">
        <!-- <q-btn
          flat
          round
          :icon="showFilters ? 'filter_alt_off' : 'filter_alt'"
          @click="showFilters = !showFilters"
        >
          <q-tooltip>{{
            showFilters ? "Hide filters" : "Show filters"
          }}</q-tooltip>
        </q-btn> -->
        <q-btn flat round icon="sym_r_monitoring" @click="showAnalytic = true">
          <q-tooltip>Show analytic</q-tooltip>
        </q-btn>
      </div>
    </div>
    <div class="full-width">
      <div
        v-if="showFilters"
        class="row wrap items-center q-gutter-md q-pr-md full-width q-pb-md"
      >
        <div class="col">
          <q-select
            dense
            outlined
            label-color="white"
            label="Section name"
          ></q-select>
        </div>
        <div class="col">
          <q-select
            dense
            outlined
            label-color="white"
            label="Subsection name"
          ></q-select>
        </div>
        <div class="col">
          <q-select
            dense
            outlined
            label-color="white"
            label="Feeder name"
          ></q-select>
        </div>
        <div class="col">
          <q-select
            dense
            outlined
            label-color="white"
            label="Date range"
          ></q-select>
        </div>
        <q-btn
          color="primary"
          size="12px"
          style="height: 38px"
          label="Apply filters"
          no-caps
        ></q-btn>
        <q-btn flat :ripple="false" round icon="restart_alt">
          <q-tooltip>Reset</q-tooltip>
        </q-btn>
      </div>
      <div class="row wrap q-col-gutter-md q-px-md q-pb-md">
        <div class="col">
          <div class="card-holder flex column items-center">
            <img width="30px" :src="$options.meter" alt="" />
            <span>Total Meters</span>
            <strong>30678</strong>
            <p class="flex items-center q-mb-none">
              updated: Apr 2, 2025 21:45
            </p>
          </div>
        </div>
        <div class="col">
          <div class="card-holder flex column items-center">
            <img width="30px" :src="$options.weekly" alt="" />
            <span>Performance</span>
            <strong>98.73%</strong>
            <p class="flex items-center q-mb-none">
              <q-icon name="trending_down" color="negative" size="20px"></q-icon
              ><b class="text-negative q-mr-xs">-0.50%</b>vs last week
            </p>
          </div>
        </div>
        <div class="col">
          <div class="card-holder flex column items-center">
            <img width="30px" :src="$options.meter" alt="" />
            <span>Meters Not Responded</span>
            <strong>4.22%</strong>
            <p class="flex items-center q-mb-none">
              <q-icon name="trending_down" color="negative" size="20px"></q-icon
              ><b class="text-negative q-mr-xs">-1.26%</b>vs last week
            </p>
          </div>
        </div>
        <div class="col">
          <div class="card-holder flex column items-center">
            <img width="30px" :src="$options.sla" alt="" />
            <span>8 hours SLA</span>
            <strong>90.06%</strong>
            <p class="flex items-center q-mb-none">
              <q-icon name="trending_down" color="negative" size="20px"></q-icon
              ><b class="text-negative q-mr-xs">-0.43%</b>vs last week
            </p>
          </div>
        </div>
        <div class="col">
          <div class="card-holder flex column items-center">
            <img width="30px" :src="$options.sla" alt="" />
            <span>12 hours SLA</span>
            <strong>94.51%</strong>
            <p class="flex items-center q-mb-none">
              <q-icon name="trending_up" color="positive" size="20px"></q-icon
              ><b class="text-positive q-mr-xs">-0.76%</b>vs last week
            </p>
          </div>
        </div>
      </div>
      <div class="row wrap q-col-gutter-md q-px-md q-pb-md">
        <div class="col-6">
          <div class="glass-card">
            <div class="flex items-center justify-between">
              <strong class="text-h6 q-pl-md">Performance</strong>
              <q-btn
                @click="showFullScreen = true"
                flat
                round
                class="q-ml-auto"
                icon="fullscreen"
              >
                <q-tooltip>Full screen</q-tooltip>
              </q-btn>
            </div>
            <div class="chart-btns full-width flex q-mt-sm q-pl-md">
              <q-btn
                :class="{ active: selection['chart'] === 'one_day' }"
                color="0c1d44"
                size="sm"
                @click="filterChart('chart', 'one_day')"
                label="1D"
              ></q-btn>
              <q-btn
                :class="{ active: selection['chart'] === 'one_week' }"
                color="0c1d44"
                size="sm"
                @click="filterChart('chart', 'one_week')"
                label="1W"
              ></q-btn>
              <q-btn
                :class="{ active: selection['chart'] === 'one_month' }"
                color="0c1d44"
                size="sm"
                @click="filterChart('chart', 'one_month')"
                label="1M"
              ></q-btn>
              <q-btn
                :class="{ active: selection['chart'] === 'three_month' }"
                color="0c1d44"
                size="sm"
                @click="filterChart('chart', 'three_month')"
                label="3M"
              ></q-btn>
              <q-btn
                :class="{ active: selection['chart'] === 'six_month' }"
                color="0c1d44"
                size="sm"
                @click="filterChart('chart', 'six_month')"
                label="6M"
              ></q-btn>
            </div>
            <vue-apex-charts
              width="100%"
              height="400px"
              :options="options"
              :series="options.series"
              ref="chart"
            ></vue-apex-charts>
          </div>
        </div>
        <div class="col-6">
          <div class="glass-card">
            <div class="flex items-center justify-between">
              <strong class="text-h6 q-pl-md">Meters Not Responded</strong>
              <q-btn
                @click="showFullScreen = true"
                flat
                round
                class="q-ml-auto"
                icon="fullscreen"
              >
                <q-tooltip>Full screen</q-tooltip>
              </q-btn>
            </div>
            <div class="chart-btns full-width flex q-mt-sm q-pl-md">
              <q-btn
                :class="{ active: selection['chart2'] === 'one_day' }"
                color="0c1d44"
                size="sm"
                @click="filterChart('chart2', 'one_day')"
                label="1D"
              ></q-btn>
              <q-btn
                :class="{ active: selection['chart2'] === 'one_week' }"
                color="0c1d44"
                size="sm"
                @click="filterChart('chart2', 'one_week')"
                label="1W"
              ></q-btn>
              <q-btn
                :class="{ active: selection['chart2'] === 'one_month' }"
                color="0c1d44"
                size="sm"
                @click="filterChart('chart2', 'one_month')"
                label="1M"
              ></q-btn>
              <q-btn
                :class="{ active: selection['chart2'] === 'three_month' }"
                color="0c1d44"
                size="sm"
                @click="filterChart('chart2', 'three_month')"
                label="3M"
              ></q-btn>
              <q-btn
                :class="{ active: selection['chart2'] === 'six_month' }"
                color="0c1d44"
                size="sm"
                @click="filterChart('chart2', 'six_month')"
                label="6M"
              ></q-btn>
            </div>
            <vue-apex-charts
              width="100%"
              height="400px"
              :options="options"
              :series="options.series"
              ref="chart2"
            ></vue-apex-charts>
          </div>
        </div>
        <div class="col-6">
          <div class="glass-card">
            <strong class="text-h6 q-pl-md">8 hours SLA</strong>
            <vue-apex-charts
              width="100%"
              height="400px"
              :options="options"
              :series="options.series"
            ></vue-apex-charts>
          </div>
        </div>
        <div class="col-6">
          <div class="glass-card">
            <strong class="text-h6 q-pl-md">12 hours SLA</strong>
            <vue-apex-charts
              width="100%"
              height="400px"
              :options="options"
              :series="options.series"
            ></vue-apex-charts>
          </div>
        </div>
      </div>
      <div class="row wrap q-col-gutter-md q-px-md q-pb-md">
        <div class="col-6">
          <div class="impact">
            <span class="block text-h6">Impact</span>
            <div class="row wrap q-col-gutter-md q-pt-md q-px-xs q-pb-md">
              <div class="col-6">
                <div class="item-holder">
                  <span>Revenue loss</span>
                  <vue-apex-charts
                    width="100%"
                    :options="radialOptions"
                    :series="radialOptions.series"
                  ></vue-apex-charts>
                </div>
              </div>
              <div class="col-6">
                <div class="item-holder">
                  <span>Units loss</span>
                  <vue-apex-charts
                    width="100%"
                    :options="radialOptions2"
                    :series="radialOptions2.series"
                  ></vue-apex-charts>
                </div>
              </div>
              <div class="col-12">
                <div class="item-holder linear">
                  <span>Top loss by category</span>
                  <div class="flex no-wrap items-center">
                    <span class="linear-title" style="min-width: 100px"
                      >Railway</span
                    >
                    <q-linear-progress
                      rounded
                      size="10px"
                      value="0.24"
                      color="info"
                      class="q-mx-lg"
                    />
                    <strong>24%</strong>
                  </div>
                  <div class="flex no-wrap items-center">
                    <span class="linear-title" style="min-width: 100px"
                      >Agriculture</span
                    >
                    <q-linear-progress
                      rounded
                      size="10px"
                      value="0.45"
                      color="info"
                      class="q-mx-lg"
                    />
                    <strong>45%</strong>
                  </div>
                  <div class="flex no-wrap items-center">
                    <span class="linear-title" style="min-width: 100px"
                      >Commercial</span
                    >
                    <q-linear-progress
                      rounded
                      size="10px"
                      value="0.67"
                      color="info"
                      class="q-mx-lg"
                    />
                    <strong>67%</strong>
                  </div>
                </div>
              </div>
              <div class="col-8">
                <div class="item-holder meters">
                  <span>Meters</span>
                  <div class="meters-holder">
                    <p class="q-mb-xs">Revenue lost: <b>12%</b></p>
                    <p class="q-mb-xs">Amount lost: <b>3752$</b></p>
                    <p class="q-mb-xs">Units lost: <b>42MW</b></p>
                  </div>
                </div>
              </div>
              <div class="col-4">
                <div class="item-holder">
                  <span>Zones affected</span>
                  <strong class="block text-h3 text-center text-bold"
                    >37</strong
                  >
                </div>
              </div>
            </div>
          </div>
        </div>
        <div class="col-6">
          <div class="impact">
            <span class="block text-h6">Suggestions</span>
            <div class="row wrap q-col-gutter-md q-pt-md q-px-xs q-pb-md">
              <div class="col-12">
                <div class="suggestion-card">
                  <div class="suggestion-header">
                    <span class="impact-label high">High Impact</span>
                  </div>
                  <div class="flex items-end">
                    <p class="suggestion-text q-mb-none">
                      Replace 128 meters in zones A and B
                    </p>
                    <q-btn
                      class="q-ml-auto"
                      color="primary"
                      size="12px"
                      label="Create ticket"
                      no-caps
                    ></q-btn>
                  </div>
                </div>
              </div>
              <div class="col-12">
                <div class="suggestion-card">
                  <div class="suggestion-header">
                    <span class="impact-label quick-fix">Quick Fix</span>
                  </div>
                  <div class="flex items-end">
                    <p class="suggestion-text q-mb-none">
                      Check collector connectivity with Airtel
                    </p>
                    <q-btn
                      class="q-ml-auto"
                      color="primary"
                      size="12px"
                      label="Create ticket"
                      no-caps
                    ></q-btn>
                  </div>
                </div>
              </div>
              <div class="col-12">
                <div class="suggestion-card high-impact">
                  <div class="suggestion-header">
                    <span class="impact-label high">High Impact</span>
                    <span class="impact-label quick-fix">Quick Fix</span>
                  </div>
                  <div class="flex items-end">
                    <p class="suggestion-text q-mb-none">
                      Replace SIM cards in 78 meters to Vodafone
                    </p>
                    <q-btn
                      class="q-ml-auto"
                      color="primary"
                      size="12px"
                      label="Create ticket"
                      no-caps
                    ></q-btn>
                  </div>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
    <q-drawer
      side="right"
      class="analytic-bar"
      width="350"
      v-model="showAnalytic"
      overlay
    >
      <div class="full-height">
        <div
          class="head q-pl-md q-pr-sm q-py-xs flex items-center justify-between"
        >
          <span class="text-h6">Analytics Dashboard</span>
          <q-btn
            flat
            round
            icon="sym_r_close"
            @click="showAnalytic = false"
          ></q-btn>
        </div>
        <div class="content q-px-md q-py-sm">
          <span class="block bar-label q-mb-sm">Advanced Analytics</span>
          <q-table
            class="analytic-table q-mb-md"
            :rows="rows"
            hide-pagination
            flat
            :columns="columns"
            dense
          >
            <template v-slot:body-cell="props">
              <q-td :props="props">
                <span :class="`text-${props.row.class}`">{{
                  props.value
                }}</span>
              </q-td>
            </template>
          </q-table>
          <span class="block bar-label q-mb-sm">Diagnosis</span>
          <div class="block-graph flex items-center q-mb-md">
            <div class="graph-legend">
              <span>
                <q-icon
                  name="sym_r_wifi"
                  size="18px"
                  color="dark"
                  class="q-mr-sm"
                ></q-icon>
                Communication: 1.6%
              </span>
              <span>
                <q-icon
                  name="sym_r_settings"
                  color="negative"
                  class="q-mr-sm"
                  size="18px"
                ></q-icon>
                MNR: 0.5%
              </span>
              <span>
                <q-icon
                  name="sym_r_api"
                  color="secondary"
                  class="q-mr-sm"
                  size="18px"
                ></q-icon>
                Software 0.7%
              </span>
            </div>
            <div class="graph-holder">
              <vue-apex-charts
                width="100%"
                height="150px"
                :options="analyticOptions.chartOptions"
                :series="analyticOptions.series"
              ></vue-apex-charts>
            </div>
          </div>
          <span class="block bar-label q-mb-sm">
            Details
            <q-btn icon="sym_r_download" flat round size="sm">
              <q-tooltip>Download report</q-tooltip>
            </q-btn>
          </span>
          <div class="block-graph q-mb-md">
            <strong style="font-size: 15px">Meters</strong>
            <div class="flex items-center justify-between q-mb-md">
              <p class="q-mb-none">To replace or fix: 500 meters</p>
              <q-btn
                class="q-ml-auto"
                color="primary"
                size="10px"
                label="Request service"
                no-caps
              ></q-btn>
            </div>
            <strong style="font-size: 15px">Communication</strong>
            <div class="row communication">
              <div class="col">
                <b style="color: #289df9">RF: 1% (1000 Meters)</b>
                <span>HW: 0.3% (300)</span>
                <span>Signal: 0.7% (700)</span>
              </div>
              <div class="col">
                <b style="color: #49cec3">Cellular: 0.6% (589 Meters)</b>
                <span>SIM: 0.2% (196)</span>
                <span>Signal: 0.4% (393)</span>
              </div>
            </div>
            <span class="block text-negative" style="font-size: 14px"
              >Meters non responding >2 days: 125</span
            >
            <div class="flex items-center justify-between q-mb-md">
              <p class="q-mb-none">Request service</p>
              <q-btn
                class="q-ml-auto"
                color="primary"
                size="10px"
                label="Request service"
                no-caps
              ></q-btn>
            </div>
            <strong style="font-size: 15px">Software</strong>

            <div class="meters-holder software block full-width q-mb-md">
              <a href="#" class="q-mb-xs"
                >Data Anomaly <b>0.03% (30 meters)</b></a
              >
              <a href="#" class="q-mb-xs"
                >Validation Failures: <b>0.04% (40 meters)</b></a
              >
              <a href="#" class="q-mb-xs"
                >Data Loss :<b>0.03% (30 meters)</b></a
              >
            </div>
            <div class="flex items-center justify-between q-mb-sm">
              <q-btn
                class="q-ml-auto"
                color="primary"
                size="10px"
                label="Request service"
                no-caps
              ></q-btn>
            </div>
          </div>
          <span class="block bar-label q-mb-sm">Last 7 Days Trend</span>
          <div class="block-graph-no-padding q-mb-md">
            <vue-apex-charts
              width="100%"
              height="150px"
              :options="analyticLineOptions.chartOptions"
              :series="analyticLineOptions.series"
            ></vue-apex-charts>
          </div>
          <q-btn color="primary" class="full-width"
            ><q-icon name="sym_r_download"></q-icon>Download report</q-btn
          >
        </div>
      </div>
    </q-drawer>
  </q-page>
  <q-dialog
    v-model="showFullScreen"
    persistent
    maximized
    transition-show="slide-up"
    transition-hide="slide-down"
  >
    <q-card class="full-screen-chart text-white">
      <q-bar class="flex items-center justify-between q-py-lg">
        <span class="text-h5">Performance</span>
        <q-btn
          @click="showFullScreen = false"
          flat
          round
          class="q-ml-auto"
          icon="close"
        >
          <q-tooltip>Close</q-tooltip>
        </q-btn>
      </q-bar>
      <q-card-section class="q-py-lg q-px-lg">
        <div class="chart-btns full-width flex q-mt-sm q-pl-md">
          <q-btn
            :class="{ active: selection['chart'] === 'one_day' }"
            color="0c1d44"
            size="sm"
            @click="filterChart('chart', 'one_day')"
            label="1D"
          ></q-btn>
          <q-btn
            :class="{ active: selection['chart'] === 'one_week' }"
            color="0c1d44"
            size="sm"
            @click="filterChart('chart', 'one_week')"
            label="1W"
          ></q-btn>
          <q-btn
            :class="{ active: selection['chart'] === 'one_month' }"
            color="0c1d44"
            size="sm"
            @click="filterChart('chart', 'one_month')"
            label="1M"
          ></q-btn>
          <q-btn
            :class="{ active: selection['chart'] === 'three_month' }"
            color="0c1d44"
            size="sm"
            @click="filterChart('chart', 'three_month')"
            label="3M"
          ></q-btn>
          <q-btn
            :class="{ active: selection['chart'] === 'six_month' }"
            color="0c1d44"
            size="sm"
            @click="filterChart('chart', 'six_month')"
            label="6M"
          ></q-btn>
        </div>
        <vue-apex-charts
          width="100%"
          height="600px"
          :options="options"
          :series="options.series"
          ref="chart"
        ></vue-apex-charts>
      </q-card-section>
    </q-card>
  </q-dialog>
</template>

<script>
import { defineComponent } from "vue";
import VueApexCharts from "vue3-apexcharts";
import weekly from "../assets/weekly.png";
import meter from "../assets/meter.png";
import sla from "../assets/sla.png";

export default defineComponent({
  name: "IndexPage",
  components: {
    VueApexCharts,
  },
  weekly,
  meter,
  sla,
  methods: {
    filterChart(chart, timeline) {
      {
        this.selection[chart] = timeline;

        switch (timeline) {
          case "one_day":
            this.$refs[chart].zoomX(
              new Date("27 Jan 2012").getTime(),
              new Date("28 Jan 2012").getTime()
            );
            break;
          case "one_week":
            this.$refs[chart].zoomX(
              new Date("27 Jan 2012").getTime(),
              new Date("4 Feb 2012").getTime()
            );
            break;
          case "one_month":
            this.$refs[chart].zoomX(
              new Date("27 Jan 2012").getTime(),
              new Date("27 Feb 2012").getTime()
            );
            break;
          case "three_month":
            this.$refs[chart].zoomX(
              new Date("27 Jan 2012").getTime(),
              new Date("27 Apr 2012").getTime()
            );
            break;
          case "six_month":
            this.$refs[chart].zoomX(
              new Date("27 Jan 2012").getTime(),
              new Date("27 Jul 2012").getTime()
            );
            break;
          default:
        }
      }
    },
  },
  data() {
    return {
      showFullScreen: false,
      selection: {
        chart: "",
        chart2: "",
      },
      columns: [
        { name: "what", label: "", field: "what", align: "left" },
        { name: "today", label: "Today %", field: "today" },
        { name: "mtd", label: "MTD %", field: "mtd" },
      ],
      rows: [
        { what: "System Performance", today: 97.9, mtd: "98.1" },
        { what: "Faliures", today: 2.1, mtd: "1.9", class: "negative" },
        { what: "0-8 hours", today: 1.8, mtd: "1.3" },
        { what: "8-12 hours", today: 1.9, mtd: "1.6" },
        { what: ">12 hours", today: 0.8, mtd: "0.6" },
      ],
      showAnalytic: false,
      showFilters: true,
      options: {
        series: [
          {
            data: [
              [1327359600000, 30.95],
              [1327446000000, 31.34],
              [1327532400000, 31.18],
              [1327618800000, 31.05],
              [1327878000000, 31.0],
              [1327964400000, 30.95],
              [1328050800000, 31.24],
              [1328137200000, 31.29],
              [1328223600000, 31.85],
              [1328482800000, 31.86],
              [1328569200000, 32.28],
              [1328655600000, 32.1],
              [1328742000000, 32.65],
              [1328828400000, 32.21],
              [1329087600000, 32.35],
              [1329174000000, 32.44],
              [1329260400000, 32.46],
              [1329346800000, 32.86],
              [1329433200000, 32.75],
              [1329778800000, 32.54],
              [1329865200000, 32.33],
              [1329951600000, 32.97],
              [1330038000000, 33.41],
              [1330297200000, 33.27],
              [1330383600000, 33.27],
              [1330470000000, 32.89],
              [1330556400000, 33.1],
              [1330642800000, 33.73],
              [1330902000000, 33.22],
              [1330988400000, 31.99],
              [1331074800000, 32.41],
              [1331161200000, 33.05],
              [1331247600000, 33.64],
              [1331506800000, 33.56],
              [1331593200000, 34.22],
              [1331679600000, 33.77],
              [1331766000000, 34.17],
              [1331852400000, 33.82],
              [1332111600000, 34.51],
              [1332198000000, 33.16],
              [1332284400000, 33.56],
              [1332370800000, 33.71],
              [1332457200000, 33.81],
              [1332712800000, 34.4],
              [1332799200000, 34.63],
              [1332885600000, 34.46],
              [1332972000000, 34.48],
              [1333058400000, 34.31],
              [1333317600000, 34.7],
              [1333404000000, 34.31],
              [1333490400000, 33.46],
              [1333576800000, 33.59],
              [1333922400000, 33.22],
              [1334008800000, 32.61],
              [1334095200000, 33.01],
              [1334181600000, 33.55],
              [1334268000000, 33.18],
              [1334527200000, 32.84],
              [1334613600000, 33.84],
              [1334700000000, 33.39],
              [1334786400000, 32.91],
              [1334872800000, 33.06],
              [1335132000000, 32.62],
              [1335218400000, 32.4],
              [1335304800000, 33.13],
              [1335391200000, 33.26],
              [1335477600000, 33.58],
              [1335736800000, 33.55],
              [1335823200000, 33.77],
              [1335909600000, 33.76],
              [1335996000000, 33.32],
              [1336082400000, 32.61],
              [1336341600000, 32.52],
              [1336428000000, 32.67],
              [1336514400000, 32.52],
              [1336600800000, 31.92],
              [1336687200000, 32.2],
              [1336946400000, 32.23],
              [1337032800000, 32.33],
              [1337119200000, 32.36],
              [1337205600000, 32.01],
              [1337292000000, 31.31],
              [1337551200000, 32.01],
              [1337637600000, 32.01],
              [1337724000000, 32.18],
              [1337810400000, 31.54],
              [1337896800000, 31.6],
              [1338242400000, 32.05],
              [1338328800000, 31.29],
              [1338415200000, 31.05],
              [1338501600000, 29.82],
              [1338760800000, 30.31],
              [1338847200000, 30.7],
              [1338933600000, 31.69],
              [1339020000000, 31.32],
              [1339106400000, 31.65],
              [1339365600000, 31.13],
              [1339452000000, 31.77],
              [1339538400000, 31.79],
              [1339624800000, 31.67],
              [1339711200000, 32.39],
              [1339970400000, 32.63],
              [1340056800000, 32.89],
              [1340143200000, 31.99],
              [1340229600000, 31.23],
              [1340316000000, 31.57],
              [1340575200000, 30.84],
              [1340661600000, 31.07],
              [1340748000000, 31.41],
              [1340834400000, 31.17],
              [1340920800000, 32.37],
              [1341180000000, 32.19],
              [1341266400000, 32.51],
              [1341439200000, 32.53],
              [1341525600000, 31.37],
              [1341784800000, 30.43],
              [1341871200000, 30.44],
              [1341957600000, 30.2],
              [1342044000000, 30.14],
              [1342130400000, 30.65],
              [1342389600000, 30.4],
              [1342476000000, 30.65],
              [1342562400000, 31.43],
              [1342648800000, 31.89],
              [1342735200000, 31.38],
              [1342994400000, 30.64],
              [1343080800000, 30.02],
              [1343167200000, 30.33],
              [1343253600000, 30.95],
              [1343340000000, 31.89],
              [1343599200000, 31.01],
              [1343685600000, 30.88],
              [1343772000000, 30.69],
              [1343858400000, 30.58],
              [1343944800000, 32.02],
              [1344204000000, 32.14],
              [1344290400000, 32.37],
              [1344376800000, 32.51],
              [1344463200000, 32.65],
              [1344549600000, 32.64],
              [1344808800000, 32.27],
              [1344895200000, 32.1],
              [1344981600000, 32.91],
              [1345068000000, 33.65],
              [1345154400000, 33.8],
              [1345413600000, 33.92],
              [1345500000000, 33.75],
              [1345586400000, 33.84],
              [1345672800000, 33.5],
              [1345759200000, 32.26],
              [1346018400000, 32.32],
              [1346104800000, 32.06],
              [1346191200000, 31.96],
              [1346277600000, 31.46],
              [1346364000000, 31.27],
              [1346709600000, 31.43],
              [1346796000000, 32.26],
              [1346882400000, 32.79],
              [1346968800000, 32.46],
              [1347228000000, 32.13],
              [1347314400000, 32.43],
              [1347400800000, 32.42],
              [1347487200000, 32.81],
              [1347573600000, 33.34],
              [1347832800000, 33.41],
              [1347919200000, 32.57],
              [1348005600000, 33.12],
              [1348092000000, 34.53],
              [1348178400000, 33.83],
              [1348437600000, 33.41],
              [1348524000000, 32.9],
              [1348610400000, 32.53],
              [1348696800000, 32.8],
              [1348783200000, 32.44],
              [1349042400000, 32.62],
              [1349128800000, 32.57],
              [1349215200000, 32.6],
              [1349301600000, 32.68],
              [1349388000000, 32.47],
              [1349647200000, 32.23],
              [1349733600000, 31.68],
              [1349820000000, 31.51],
              [1349906400000, 31.78],
              [1349992800000, 31.94],
              [1350252000000, 32.33],
              [1350338400000, 33.24],
              [1350424800000, 33.44],
              [1350511200000, 33.48],
              [1350597600000, 33.24],
              [1350856800000, 33.49],
              [1350943200000, 33.31],
              [1351029600000, 33.36],
              [1351116000000, 33.4],
              [1351202400000, 34.01],
              [1351638000000, 34.02],
              [1351724400000, 34.36],
              [1351810800000, 34.39],
              [1352070000000, 34.24],
              [1352156400000, 34.39],
              [1352242800000, 33.47],
              [1352329200000, 32.98],
              [1352415600000, 32.9],
              [1352674800000, 32.7],
              [1352761200000, 32.54],
              [1352847600000, 32.23],
              [1352934000000, 32.64],
              [1353020400000, 32.65],
              [1353279600000, 32.92],
              [1353366000000, 32.64],
              [1353452400000, 32.84],
              [1353625200000, 33.4],
              [1353884400000, 33.3],
              [1353970800000, 33.18],
              [1354057200000, 33.88],
              [1354143600000, 34.09],
              [1354230000000, 34.61],
              [1354489200000, 34.7],
              [1354575600000, 35.3],
              [1354662000000, 35.4],
              [1354748400000, 35.14],
              [1354834800000, 35.48],
              [1355094000000, 35.75],
              [1355180400000, 35.54],
              [1355266800000, 35.96],
              [1355353200000, 35.53],
              [1355439600000, 37.56],
              [1355698800000, 37.42],
              [1355785200000, 37.49],
              [1355871600000, 38.09],
              [1355958000000, 37.87],
              [1356044400000, 37.71],
              [1356303600000, 37.53],
              [1356476400000, 37.55],
              [1356562800000, 37.3],
              [1356649200000, 36.9],
              [1356908400000, 37.68],
              [1357081200000, 38.34],
              [1357167600000, 37.75],
              [1357254000000, 38.13],
              [1357513200000, 37.94],
              [1357599600000, 38.14],
              [1357686000000, 38.66],
              [1357772400000, 38.62],
              [1357858800000, 38.09],
              [1358118000000, 38.16],
              [1358204400000, 38.15],
              [1358290800000, 37.88],
              [1358377200000, 37.73],
              [1358463600000, 37.98],
              [1358809200000, 37.95],
              [1358895600000, 38.25],
              [1358982000000, 38.1],
              [1359068400000, 38.32],
              [1359327600000, 38.24],
              [1359414000000, 38.52],
              [1359500400000, 37.94],
              [1359586800000, 37.83],
              [1359673200000, 38.34],
              [1359932400000, 38.1],
              [1360018800000, 38.51],
              [1360105200000, 38.4],
              [1360191600000, 38.07],
              [1360278000000, 39.12],
              [1360537200000, 38.64],
              [1360623600000, 38.89],
              [1360710000000, 38.81],
              [1360796400000, 38.61],
              [1360882800000, 38.63],
              [1361228400000, 38.99],
              [1361314800000, 38.77],
              [1361401200000, 38.34],
              [1361487600000, 38.55],
              [1361746800000, 38.11],
              [1361833200000, 38.59],
              [1361919600000, 39.6],
            ],
          },
        ],
        chart: {
          id: "area-datetime",
          type: "area",
          foreColor: "#fff",
          toolbar: {
            tools: {
              selection: true,
              reset: false,
              pan: true,
              zoom: true,
            },
          },
          zoom: {
            autoScaleYaxis: true,
          },
        },
        grid: {
          borderColor: "#438bca",
        },
        dataLabels: {
          enabled: false,
          style: {
            fontSize: "40px",
          },
        },
        markers: {
          size: 0,
          style: "hollow",
        },
        xaxis: {
          type: "datetime",
          min: new Date("01 Mar 2012").getTime(),
          tickAmount: 1,
          axisBorder: {
            show: true,
            color: "#438bca",
          },
          axisTicks: {
            show: true,
            color: "#438bca",
          },
        },
        tooltip: {
          x: {
            format: "dd MMM yyyy",
          },
        },
        stroke: {
          width: 2,
          colors: ["#63eff8"],
        },
        fill: {
          type: "gradient",
          colors: ["#2c82c2", "#FFF"],
          gradient: {
            shadeIntensity: 1,

            opacityFrom: 0.9,
            opacityTo: 0.1,
            stops: [0, 100],
          },
        },
      },
      analyticOptions: {
        series: [87, 55, 67],
        chartOptions: {
          chart: {
            height: 350,
            type: "radialBar",
            background: "transparent",
          },
          
          plotOptions: {
            radialBar: {
              track: {
              background: "rgba(255, 255, 255, 0.1)",
            },
              dataLabels: {
                name: {
                  fontSize: "12px",
                },
                value: {
                  fontSize: "12px",
                },
                total: {
                  show: false,
                },
              },
            },
          },
          labels: ["Comm", "MNR", "Software"],
          colors: ["#24649c", "#cd1806", "#ffd166"],
        },
      },
      analyticLineOptions: {
        series: [
          {
            name: "series1",
            data: [31, 40, 28, 51, 42, 109, 100],
          },
        ],
        chartOptions: {
          chart: {
            height: 350,
            type: "area",
            foreColor: "#fff",
            toolbar: {
              tools: {
                selection: false,
                reset: false,
                pan: false,
                zoom: false,
              },
            },
            zoom: {
              autoScaleYaxis: true,
            },
          },
          dataLabels: {
            enabled: false,
          },
          grid: {
            borderColor: "#438bca",
          },
          stroke: {
            width: 2,
            colors: ["#63eff8"],
          },
          fill: {
            type: "gradient",
            colors: ["#2c82c2", "#FFF"],
            gradient: {
              shadeIntensity: 1,
              opacityFrom: 0.9,
              opacityTo: 0.1,
              stops: [0, 100],
            },
          },
          xaxis: {
            type: "datetime",
            categories: [
              "2018-09-19T00:00:00.000Z",
              "2018-09-19T01:30:00.000Z",
              "2018-09-19T02:30:00.000Z",
              "2018-09-19T03:30:00.000Z",
              "2018-09-19T04:30:00.000Z",
              "2018-09-19T05:30:00.000Z",
              "2018-09-19T06:30:00.000Z",
            ],
          },
          tooltip: {
            x: {
              format: "dd/MM/yy HH:mm",
            },
          },
        },
      },
      radialOptions: {
        series: [67],
        chart: {
          type: "radialBar",
          background: "transparent",
        },
        plotOptions: {
          radialBar: {
            hollow: {
              size: "50%",
            },
            startAngle: -90,
            endAngle: 90,
            track: {
              background: "rgba(255, 255, 255, 0.1)",
            },
            dataLabels: {
              name: {
                show: false, // ✅ Hides "Median Ratio"
              },
              value: {
                formatter: function (val) {
                  return val + "$";
                },
                fontSize: "20px", // ✅ Adjust size of "67"
                fontWeight: "bold",
                color: "#ffffff", // ✅ Adjust color if needed
                show: true, // ✅ Shows only the value
                offsetY: 0,
              },
            },
          },
        },
        fill: {
          type: "gradient",
          gradient: {
            type: "horizontal", // Can be "horizontal" or "vertical"
            shadeIntensity: 1,
            gradientToColors: ["#27AE60", "#ffd166", "#ff8548", "#C0392B"],
            inverseColors: false,
            opacityFrom: 1,
            opacityTo: 1,
            stops: [0, 50, 75, 100], // Defines color transition points
            colorStops: [
              { offset: 0, color: "#27AE60", opacity: 1 }, // Green
              { offset: 50, color: "#ffd166", opacity: 1 }, // Yellow
              { offset: 75, color: "#ff8548", opacity: 1 }, // Orange
              { offset: 100, color: "#C0392B", opacity: 1 }, // Red
            ],
          },
        },
        stroke: {
          dashArray: 3,
        },
        annotations: {
          position: "back",
          texts: [
            {
              text: "Low", // Start label
              x: "15%",
              y: "50%",
              textAnchor: "middle",
              foreColor: "#fff",
            },
            {
              text: "High", // End label
              x: "85%",
              y: "50%",
              textAnchor: "middle",
              foreColor: "#fff",
            },
          ],
        },
      },
      radialOptions2: {
        series: [78],
        chart: {
          type: "radialBar",
          background: "transparent",
        },
        plotOptions: {
          radialBar: {
            hollow: {
              size: "50%",
            },
            startAngle: -90,
            endAngle: 90,
            track: {
              background: "rgba(255, 255, 255, 0.1)",
            },
            dataLabels: {
              name: {
                show: false, // ✅ Hides "Median Ratio"
              },
              value: {
                formatter: function (val) {
                  return val + "MW";
                },
                fontSize: "20px", // ✅ Adjust size of "67"
                fontWeight: "bold",
                color: "#ffffff", // ✅ Adjust color if needed
                show: true, // ✅ Shows only the value
                offsetY: 0,
              },
            },
          },
        },
        fill: {
          type: "gradient",
          gradient: {
            type: "horizontal", // Can be "horizontal" or "vertical"
            shadeIntensity: 1,
            gradientToColors: ["#27AE60", "#ffd166", "#ff8548", "#C0392B"],
            inverseColors: false,
            opacityFrom: 1,
            opacityTo: 1,
            stops: [0, 50, 75, 100], // Defines color transition points
            colorStops: [
              { offset: 0, color: "#27AE60", opacity: 1 }, // Green
              { offset: 50, color: "#ffd166", opacity: 1 }, // Yellow
              { offset: 75, color: "#ff8548", opacity: 1 }, // Orange
              { offset: 100, color: "#C0392B", opacity: 1 }, // Red
            ],
          },
        },
        stroke: {
          dashArray: 3,
        },
        annotations: {
          position: "back",
          texts: [
            {
              text: "Low", // Start label
              x: "15%",
              y: "50%",
              textAnchor: "middle",
              foreColor: "#fff",
            },
            {
              text: "High", // End label
              x: "85%",
              y: "50%",
              textAnchor: "middle",
              foreColor: "#fff",
            },
          ],
        },
      },
    };
  },
});
</script>

<style lang="scss">
.body-background,
.full-screen-chart {
  background: rgb(0, 60, 126);
  background: radial-gradient(
    circle,
    rgba(0, 60, 126, 1) 0%,
    rgba(48, 115, 167, 1) 0%,
    rgba(0, 60, 126, 1) 100%
  );
  color: #fff;
}
.glass-card {
  background-color: rgba(255, 255, 255, 0.1);
  padding: 20px;
  backdrop-filter: blur(10px); /* Эффект размытия */
  border-radius: 12px; /* Закругленные углы */
}
.sla {
  .q-field--outlined .q-field__control:before {
    border: 1px solid #2e6da4;
  }
}
.analytic-bar {
  background: linear-gradient(
    180deg,
    #004276,
    #0c1d44
  ); /* Темно-синий градиент */
  border-left: 1px solid #438bca;
  .head {
    border-bottom: 1px solid #438bca;
  }
}
.bar-label {
  font-size: 18px;
}
.analytic-table {
  background-color: rgba(255, 255, 255, 0.1);
  color: #fff;
  border-radius: 14px;
}
.q-table thead,
.q-table tr,
.q-table th,
.q-table td {
  border-color: #2e6da4;
}
.block-graph {
  background-color: rgba(255, 255, 255, 0.1);
  padding: 8px;
  border-radius: 14px;
  .graph-holder {
    width: 40%;
  }
  .graph-legend {
    width: 60%;

    span {
      display: flex;
      align-items: center;
    }
  }
}

.block-graph-no-padding {
  background-color: rgba(255, 255, 255, 0.1);
  border-radius: 14px;
  padding-right: 4px;
  padding-top: 8px;
}

.impact {
  height: 100%;
  background-color: rgba(0, 0, 0, 0.1);
  border-radius: 14px;
  padding: 14px;
}

.item-holder {
  background-color: rgba(255, 255, 255, 0.1);
  padding: 14px 8px 8px;
  border-radius: 14px;
  height: 100%;

  &.linear {
    span.linear-title {
      text-align: left;
      font-size: 15px;
    }
  }

  span {
    display: block;
    font-size: 20px;
    text-align: center;
  }
}

.card-holder {
  background-color: rgba(0, 0, 0, 0.15);
  color: #fff;
  padding: 15px;
  border-radius: 12px;

  span {
    font-size: 16px;
  }

  strong {
    font-size: 24px;
  }

  img {
    filter: invert(79%) sepia(79%) saturate(6000%) hue-rotate(1deg)
      brightness(103%) contrast(101%);
    margin-bottom: 5px;
  }
}
.suggestion-card {
  background: linear-gradient(
    180deg,
    rgba(255, 255, 255, 0.1),
    rgba(255, 255, 255, 0.05)
  );
  border-radius: 12px;
  padding: 15px;
  color: #fff;
  box-shadow: 0 4px 10px rgba(0, 0, 0, 0.2);
}
.suggestion-header {
  display: flex;
  align-items: center;
  margin-bottom: 10px;
}

.impact-label {
  background: rgba(255, 200, 0, 0.2);
  padding: 5px 10px;
  border-radius: 6px;
  font-size: 10px;
  margin-right: 5px;

  &.high {
    background: rgba(255, 3, 3, 0.4);
  }

  &.quick-fix {
    background: rgba(47, 169, 36, 0.2);
  }
}
.q-linear-progress__model {
  border-radius: 8px;
}

.meters {
  .meters-holder {
    display: inline-block;
  }
  p {
    display: flex;
  }
  font-size: 16px;
  b {
    margin-left: auto;
    padding-left: 10px;
  }
}

.chart-btns {
  .active {
    background-color: #438bca;
  }
}

.communication {
  b,
  span {
    display: inline-block;
  }
  font-size: 12px;
}

.software {
  font-size: 14px;
  a {
    display: flex;
    color: white;
    text-decoration: none;
    border-bottom: 1px solid #fff;
    margin-bottom: 5px;
    b {
      margin-left: auto;
      padding-left: 10px;
    }
  }
}
</style>
