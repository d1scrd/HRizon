<script>
    import ApexCharts from 'apexcharts';
    import { onMount, onDestroy } from 'svelte';
  
    let radarChart, pieChart, barChart, growthChart, timeSeriesChart;
  
    onMount(() => {
      // Radar Chart
      radarChart = new ApexCharts(document.querySelector("#radarChart"), {
        chart: {
          type: 'radar',
        },
        series: [{
          name: 'Cost to Company',
          data: [20, 40, 25, 50],
        }],
        labels: ['Employee Type 1', 'Employee Type 2', 'Employee Type 3', 'Employee Type 4'],
      });
      radarChart.render();
  
      // Pie Chart
      pieChart = new ApexCharts(document.querySelector("#pieChart"), {
        chart: {
          type: 'pie',
        },
        series: [44, 55, 41],
        labels: ['Male', 'Female', 'Other'],
      });
      pieChart.render();
  
      // Total Employee Bar Chart
      barChart = new ApexCharts(document.querySelector("#barChart"), {
        chart: {
          type: 'bar',
        },
        series: [{
          name: 'Total Employees',
          data: [50, 60, 70, 80],
        }],
        xaxis: {
          categories: ['Q1', 'Q2', 'Q3', 'Q4'],
        },
      });
      barChart.render();
  
      // Growth Line Chart
      growthChart = new ApexCharts(document.querySelector("#growthChart"), {
        chart: {
          type: 'line',
        },
        series: [{
          name: 'Employee Growth',
          data: [100, 200, 300, 400],
        }],
        xaxis: {
          categories: ['2019', '2020', '2021', '2022'],
        },
      });
      growthChart.render();
  
      // Time Series Line Chart
      timeSeriesChart = new ApexCharts(document.querySelector("#timeSeriesChart"), {
        chart: {
          type: 'line',
        },
        series: [
          { name: 'Employee Type 1', data: [10, 20, 30, 40] },
          { name: 'Employee Type 2', data: [15, 25, 35, 45] },
          { name: 'Employee Type 3', data: [20, 30, 40, 50] },
          { name: 'Employee Type 4', data: [25, 35, 45, 55] },
        ],
        xaxis: {
          categories: ['2019', '2020', '2021', '2022'],
        },
      });
      timeSeriesChart.render();
    });
  
    onDestroy(() => {
      radarChart.destroy();
      pieChart.destroy();
      barChart.destroy();
      growthChart.destroy();
      timeSeriesChart.destroy();
    });
  </script>
  
  <style>
    .container {
      padding: 2rem;
      font-size: 1.5rem;
      color: #333;
      display: flex;
      flex-wrap: wrap;
      gap: 2rem;
    }
  
    .chart-container {
      flex: 1 1 calc(50% - 2rem);
      min-width: 300px;
      max-width: 500px;
    }
  
    h2 {
      font-size: 1.2rem;
      margin-bottom: 1rem;
    }
  
    @media (max-width: 768px) {
      .chart-container {
        flex: 1 1 100%;
      }
    }
  </style>
  
  <div class="container">
    <div class="chart-container">
      <h2>Cost to Company</h2>
      <div id="radarChart"></div>
    </div>
    <div class="chart-container">
      <h2>Employee Gender</h2>
      <div id="pieChart"></div>
    </div>
    <div class="chart-container">
      <h2>Total Employees</h2>
      <div id="barChart"></div>
    </div>
    <div class="chart-container">
      <h2>Growth Chart</h2>
      <div id="growthChart"></div>
    </div>
    <div class="chart-container">
      <h2>Employee Type Over Time</h2>
      <div id="timeSeriesChart"></div>
    </div>
  </div>
  