<script lang="ts">
  import { getContext, onMount } from "svelte";
  import { Grid } from "ag-grid-community";
  import "ag-grid-enterprise";
  import { CalendarSheet, options } from "../../components/sheets/calendar-sheet";
  import { Cache } from "../../services/course/cache";
  import { MetricsService } from "../../services/analytics/metrics-service";
  import Icon from "../../components/iconography/Icon.svelte";

  let calendar;
  let calendarGrid;
  let calendarHeight = 1600;
  let calendarSheet = new CalendarSheet();

  const cache: Cache = getContext("cache");

  onMount(async () => {
    calendarGrid = new Grid(calendar, { ...options });
    const calendarData = cache.course.calendar;
    let userMap = await cache.course.metricsService.fetchAllUsers();
    calendarSheet.populateCols(calendarData);
    for (const user of userMap.values()) {
      calendarSheet.populateRow(user, calendarData);
    }
    calendarSheet.render(calendarGrid);
  });

  let exportExcel = function() {
    calendarGrid.gridOptions.api.exportDataAsExcel();
  };
</script>

<div class="flex justify-around justify-center p-1">
  <div class="w-1/2">
    <div class="text-base font-light text-gray-900"> Time online this semester</div>
  </div>
  <div class="w-1/4">
    <button on:click={exportExcel}>
      <Icon type="timeExport" toolTip="Export this sheet to excel" scale="1.5" />
    </button>
  </div>
</div>
<div style="height:{calendarHeight}px">
  <div bind:this={calendar} style="height: 100%; width:100%" class="ag-theme-balham" />
</div>
