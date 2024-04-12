<script>
    import { LayerCake, Svg, flatten, stack, Html } from 'layercake';
    // import { stack } from 'd3-shape';
    import { scaleBand, scaleOrdinal } from 'd3-scale';
    // import { format } from 'd3-format';
  
    import BarStacked from '../_components/BarStacked.svelte';
    import Labels from '../_components/Labels.svelte';
    // import AxisX from '../_components/AxisX.svelte';
    import AxisY from '../_components/AxisY.svelte';
    import Tooltip from '../_components/Tooltip.html.svelte';
  
    // This example loads csv data as json using @rollup/plugin-dsv
    // import data from './_data/fruitOrdinal.csv';
    const data = [
      {countries: 'All Surveyed countries (Average)', no: 90, yes: 8, preferNotToAnswer: 2, counts: {no:28394, yes:1099, preferNotToAnswer:250}},
      {countries: 'Slovakia', no: 85, yes: 12, preferNotToAnswer: 3, counts: {no:2394, yes:199, preferNotToAnswer:40}},
      {countries: 'Poland', no: 85, yes: 12, preferNotToAnswer: 3, counts: {no:2090, yes:109, preferNotToAnswer:150}},
      {countries: 'Hungary', no: 90, yes: 8, preferNotToAnswer: 2, counts: {no:2394, yes:299, preferNotToAnswer:150}},
      {countries: 'Latvia', no: 92, yes: 8, preferNotToAnswer: 0, counts: {no:2834, yes:199, preferNotToAnswer:25}},
      {countries: 'Republic of Moldova', no: 94, yes: 6, preferNotToAnswer: 0, counts: {no:2394, yes:109, preferNotToAnswer:20}},
      {countries: 'Romania', no: 95, yes: 5, preferNotToAnswer: 0, counts: {no:2344, yes:123, preferNotToAnswer:20}},
    ];
  
    const xKey = [0, 1];
    const yKey = 'countries';
    const zKey = 'key';
  
    const seriesNames = Object.keys(data[0]).filter(d => d !== yKey && d !== 'counts');
    //const seriesColors = ['#00bbff', '#8bcef6', '#c4e2ed', '#f7f6e3'];
    const seriesColors = ['#03369a', '#ff671f', '#5b5b5b'];
    // const formatLabelX = d => format(`~s`)(d);  
    const stackedData = stack(data, seriesNames);

    const longestString = data.reduce((prev, current) => {
      return prev[yKey].length > current[yKey].length ? prev : current;
    });

    let evt;
    let hideTooltip = false;


    const yScale = scaleBand()
    .domain(data.map(d => d.name))
    .range([0, 50])  // adjust this to change the height of the bars
    .padding(0.09);
    // console.log("longestString", longestCountry[yKey].length);

  

    // console.log("stackData", stackedData);
  </script>
  
  <style>
    .chart-container {
        width:100%;
        height:450px;
    }


  </style>
  
  <div class="chart-container">
    <!-- flatData={flatten(series)} -->
    <LayerCake
      padding={{ top: 30, bottom: 0 }}
      x={xKey}
      y={d => d.data[yKey]}
      z={zKey}
      yScale={yScale}
      zScale={scaleOrdinal()}
      zDomain={seriesNames}
      zRange={seriesColors}
      yDomainSort={false}
      flatData={flatten(stackedData)}
      data={stackedData}
    >
      <Svg>
        <AxisY 
          labelPosition={"above"}
          dx={longestString[yKey].length * 7.25}
          dy={-32}
          ticks={false}
          gridlines={false}
        />
        <BarStacked
          separator
          on:mousemove={event => evt = hideTooltip = event}
          on:mouseout={() => (hideTooltip = true)}
        />
        <Labels
          labels={stackedData}
        />
      </Svg>
      <Html pointerEvents={false}>
        {#if hideTooltip !== true}
          <Tooltip
            {evt}
            let:detail
          >
          {@const tooltipData = { ...detail.props }}
            <div>
                <div><span class="text-slate-500">Country of Survey: </span> {tooltipData.data[yKey]}</div>
                {#each Object.keys(tooltipData.data) as key}
                  {#if tooltipData.data[key] === tooltipData["1"] - tooltipData["0"]}
                    <div><span class="text-slate-500">Report "{key == 'no' && "No" || key == 'yes' && "Yes" || key == 'preferNotToAnswer' && "No Answer"}": </span> Percentage = {tooltipData.data[key]}% &lcub;N = {tooltipData.data.counts[key].toLocaleString()}&rcub;</div>
                  {/if}
                {/each}
            </div>
          </Tooltip>
        {/if}
      </Html>
    </LayerCake>
  </div>
