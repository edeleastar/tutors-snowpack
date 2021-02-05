<script lang="typescript">
  import { onMount, setContext } from "svelte";
  import Router from "svelte-spa-router";
  import Sidebar from "./components/navigators/Sidebar.svelte";
  import Blank from "./pages/support/Blank.svelte";
  import Course from "./pages/Course.svelte";
  import Topic from "./pages/Topic.svelte";
  import Talk from "./pages/Talk.svelte";
  import Video from "./pages/Video.svelte";
  import Wall from "./pages/Wall.svelte";
  import Lab from "./pages/Lab.svelte";
  import AllCourses from "./pages/AllCourses.svelte";
  import NotFound from "./pages/support/NotFound.svelte";
  import MainNavigator from "./components/navigators/MainNavigator.svelte";
  import Logout from "./pages/support/Logout.svelte";
  import { Cache } from "./services/course/cache";
  import { handleAuthentication } from "./services/analytics/auth-service";
  import { AnalyticsService } from "./services/analytics/analytics-service";


  let count: number = 0;
  onMount(() => {
    const interval = setInterval(() => count++, 1000);
    return () => {
      clearInterval(interval);
    };
  });
</script>

<div class="App">
<h1 class="p-4 border"> test </h1>
</div>

<style global>
  @import 'tailwindcss/base';
  @import 'tailwindcss/components';

  .tooltip .tooltip-text {
    @apply invisible p-1 absolute z-50 inline-block mt-12 text-sm rounded-lg border border-gray-900 bg-white text-gray-900;
  }

  .tooltip:hover .tooltip-text {
    @apply visible;
  }

  @import 'tailwindcss/utilities';
</style>
