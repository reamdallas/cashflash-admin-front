<template>
  <div>
    <base-header class="pb-6">
      <div class="row align-items-center py-4">
        <div class="col-lg-6 col-7">
          <h6 class="h2 d-inline-block mb-0">
            Dashboard
          </h6>
          <nav
            aria-label="breadcrumb"
            class="d-none d-md-inline-block ml-md-4"
          >
            <route-breadcrumb />
          </nav>
        </div>
        <!--        <div class="col-lg-6 col-5 text-right">-->
        <!--          <base-button-->
        <!--            size="sm"-->
        <!--            type="neutral"-->
        <!--          >-->
        <!--            New-->
        <!--          </base-button>-->
        <!--          <base-button-->
        <!--            size="sm"-->
        <!--            type="neutral"-->
        <!--          >-->
        <!--            Filters-->
        <!--          </base-button>-->
        <!--        </div>-->
      </div>
      <!-- Card stats -->
      <div class="row">
        <div class="col-xl-4 col-md-6">
          <stats-card
            title="Users"
            type="gradient-red"
            sub-title="350,897"
            icon="ni ni-single-02"
          >
            <template slot="footer">
              <span class="text-success mr-2"><i class="fa fa-arrow-up" /> 3.48%</span>
              <span class="text-nowrap">Since last month</span>
            </template>
          </stats-card>
        </div>
        <div class="col-xl-4 col-md-6">
          <stats-card
            title="amount of CFT"
            type="gradient-info"
            sub-title="2,356"
            icon="ni ni-money-coins"
          >
            <template slot="footer">
              <span class="text-success mr-2"><i class="fa fa-arrow-up" /> 12.18%</span>
              <span class="text-nowrap">Since last month</span>
            </template>
          </stats-card>
        </div>
        <div class="col-xl-4 col-md-6">
          <stats-card
            title="amount of EOS"
            type="gradient-info"
            sub-title="924"
            icon="ni ni-money-coins"
          >
            <template slot="footer">
              <span class="text-danger mr-2"><i class="fa fa-arrow-down" /> 5.72%</span>
              <span class="text-nowrap">Since last month</span>
            </template>
          </stats-card>
        </div>
        <div class="col-xl-4 col-md-6">
          <stats-card
            title="Total balance (USD)"
            type="gradient-info"
            sub-title="350,897"
            icon="ni ni-money-coins"
          >
            <template slot="footer">
              <span class="text-success mr-2"><i class="fa fa-arrow-up" /> 3.48%</span>
              <span class="text-nowrap">Since last month</span>
            </template>
          </stats-card>
        </div>
        <div class="col-xl-4 col-md-6">
          <stats-card
            title="Referrals"
            type="gradient-red"
            sub-title="2,356"
            icon="ni ni-single-02"
          >
            <template slot="footer">
              <span class="text-success mr-2"><i class="fa fa-arrow-up" /> 12.18%</span>
              <span class="text-nowrap">Since last month</span>
            </template>
          </stats-card>
        </div>
        <div class="col-xl-4 col-md-6">
          <stats-card
            title="Referral CFT"
            type="gradient-info"
            sub-title="924"
            icon="ni ni-money-coins"
          >
            <template slot="footer">
              <span class="text-danger mr-2"><i class="fa fa-arrow-down" /> 5.72%</span>
              <span class="text-nowrap">Since last month</span>
            </template>
          </stats-card>
        </div>
      </div>
    </base-header>

    <!--Charts-->
    <div class="container-fluid mt--6">
      <card>
        <div
          slot="header"
          class="row align-items-center"
        >
          <div class="col">
            <h6 class="text-uppercase ls-1 mb-1">
              Overview
            </h6>
            <h5 class="h3 mb-0">
              Total balance
            </h5>
          </div>
          <div class="col">
            <ul class="nav nav-pills justify-content-end">
              <li class="nav-item mr-2 mr-md-0">
                <a
                  class="nav-link py-2 px-3"
                  href="#"
                  :class="{active: bigLineChart.activeIndex === 0}"
                  @click.prevent="initBigChart(0)"
                >
                  <span class="d-none d-md-block">Month</span>
                  <span class="d-md-none">M</span>
                </a>
              </li>
              <li class="nav-item">
                <a
                  class="nav-link py-2 px-3"
                  href="#"
                  :class="{active: bigLineChart.activeIndex === 1}"
                  @click.prevent="initBigChart(1)"
                >
                  <span class="d-none d-md-block">Year</span>
                  <span class="d-md-none">Y</span>
                </a>
              </li>
            </ul>
          </div>
        </div>
        <line-chart
          ref="bigChart"
          :height="350"
          :chart-data="bigLineChart.chartData"
          :extra-options="bigLineChart.extraOptions"
        />
      </card>
      <!-- End charts-->
    </div>
  </div>
</template>
<script>
// Charts
import * as chartConfigs from '@/components/argon-core/Charts/config';
import LineChart from '@/components/argon-core/Charts/LineChart';
import BarChart from '@/components/argon-core/Charts/BarChart';

// Components
import BaseProgress from '@/components/argon-core/BaseProgress';
import RouteBreadCrumb from '@/components/argon-core/Breadcrumb/RouteBreadcrumb';
import StatsCard from '@/components/argon-core/Cards/StatsCard';

// Lists
import ActivityFeed from '@/components/pages/dashboard/ActivityFeed.vue';
import TaskList from '@/components/pages/dashboard/TaskList.vue';
import UserList from '@/components/pages/dashboard/UserList.vue';
import ProgressTrackList from '@/components/pages/dashboard/ProgressTrackList.vue';

// Tables
import LightTable from '@/components/pages/dashboard/LightTable.vue';
import SocialTrafficTable from '@/components/pages/dashboard/SocialTrafficTable.vue';
import PageVisitsTable from '@/components/pages/dashboard/PageVisitsTable.vue';

export default {
  middleware: 'auth',
  layout: 'DashboardLayout',
  components: {
    ActivityFeed,
    LineChart,
    BarChart,
    BaseProgress,
    RouteBreadCrumb,
    StatsCard,
    TaskList,
    PageVisitsTable,
    SocialTrafficTable,
    LightTable,
    UserList,
    ProgressTrackList,
  },
  data() {
    return {
      bigLineChart: {
        allData: [
          [0, 20, 10, 30, 15, 40, 20, 60, 60],
          [0, 20, 5, 25, 10, 30, 15, 40, 40],
        ],
        activeIndex: 0,
        chartData: {
          datasets: [
            {
              label: 'Performance',
              data: [0, 20, 10, 30, 15, 40, 20, 60, 60],
            },
          ],
          labels: ['May', 'Jun', 'Jul', 'Aug', 'Sep', 'Oct', 'Nov', 'Dec'],
        },
        extraOptions: chartConfigs.blueChartOptions,
      },
      redBarChart: {
        chartData: {
          labels: ['Jul', 'Aug', 'Sep', 'Oct', 'Nov', 'Dec'],
          datasets: [{
            label: 'Sales',
            data: [25, 20, 30, 22, 17, 29],
          }],
        },
      },
    };
  },
  mounted() {
    this.initBigChart(0);
  },
  methods: {
    initBigChart(index) {
      const chartData = {
        datasets: [
          {
            label: 'Performance',
            data: this.bigLineChart.allData[index],
          },
        ],
        labels: ['May', 'Jun', 'Jul', 'Aug', 'Sep', 'Oct', 'Nov', 'Dec'],
      };
      this.bigLineChart.chartData = chartData;
      this.bigLineChart.activeIndex = index;
    },
  },
};
</script>
<style></style>
