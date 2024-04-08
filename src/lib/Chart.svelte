
<script lang="ts" context="module">
  // import * as echarts from 'echarts';
  // import { BarChart } from 'echarts/charts';
  import * as echarts from 'echarts/core';
  import {
    PieChart,
    TreemapChart,
    LineChart,
  } from 'echarts/charts';
  import {
    //TitleComponent,
    TooltipComponent,
    //GridComponent,
    LegendComponent,
    // Dataset
    DatasetComponent,
    // Built-in transform (filter, sort)
    TransformComponent
  } from 'echarts/components';
  import { LabelLayout, UniversalTransition } from 'echarts/features';
  import { CanvasRenderer } from 'echarts/renderers';

  import type {
    // The series option types are defined with the SeriesOption suffix
    BarSeriesOption, 
    LineSeriesOption,
  } from 'echarts/charts';

  import type {
    // The component option types are defined with the ComponentOption suffix
    LegendComponentOption,
    //TitleComponentOption, 
    //TooltipComponentOption,
    //GridComponentOption,
    //DatasetComponentOption
  } from 'echarts/components';

  import type { 
    ComposeOption, 
  } from 'echarts/core';

  type EChartsOption = ComposeOption<
    | BarSeriesOption
    | LineSeriesOption
    | LegendComponentOption
    // | TitleComponentOption
    // | TooltipComponentOption
    // | GridComponentOption
    // | DatasetComponentOption
  >;

  echarts.use([
      //TitleComponent,
      TooltipComponent,
      //GridComponent,
      DatasetComponent,
      TransformComponent,
      LegendComponent,
      PieChart,
      TreemapChart,
      //BarChart,
      LineChart,
      LabelLayout,
      UniversalTransition,
      CanvasRenderer
  ]);

  export type EChartsOptions = echarts.EChartsCoreOption
  export type EChartsTheme = string | object
  export type EChartsRenderer = 'canvas' | 'svg'

  export type ChartOptions = {
    theme?: EChartsTheme
    renderer?: EChartsRenderer
    options: EChartsOptions
  }

  const DEFAULT_OPTIONS: Partial<ChartOptions> = {
    theme: undefined,
    renderer: 'svg',
  }

  export function chartable(element: HTMLElement, echartOptions: ChartOptions) {
    const { theme, renderer, options } = {
      ...DEFAULT_OPTIONS,
      ...echartOptions,
    }
    
    console.log('is it rebuilding');
    const echartsInstance = echarts.init(element, theme, { renderer })
    echartsInstance.setOption(options)

    function handleResize() {
      echartsInstance.resize()
    }

    window.addEventListener('resize', handleResize)

    return {
      destroy() {
        // console.log('destroyed');
        echartsInstance.dispose()
        window.removeEventListener('resize', handleResize)
      },
      update(newOptions: ChartOptions) {
        console.log('on update', newOptions);
        echartsInstance.setOption({
          ...echartOptions.options,
          ...newOptions.options,
        })
      },
    }
  }
</script>

<script lang="ts">
  export let options: echarts.EChartsCoreOption
  export let { theme, renderer } = DEFAULT_OPTIONS
</script>

<div class="chart" use:chartable={{ renderer, theme, options }} />

<style>
  .chart {
    height: 100%;
    width: 100%;
  }
</style>
