<script>
import { LayerCake, Svg, Html } from 'layercake';
import { scaleBand } from 'd3-scale';
// import { onMount } from 'svelte';
// import { hoverData } from 'layercake/src/Component.Hover.svelte';

import Bar from '../_components/Bar.svelte';
// import AxisX from '../_components/AxisX.svelte';
import AxisY from '../_components/AxisY.svelte';
import Labels from '../_components/Labels.html.svelte';
import Tooltip from '../_components/Tooltip.html.svelte';
// import Annotations from '../_components/Annotations.html.svelte';

// This example loads csv data as json using @rollup/plugin-dsv
// import data from './_data/groups.csv';

const data = [
    { age: "Local School", value: 37 },
    { age: "Attend classes online", value: 34 },
    { age: "Local and online school", value: 21 },
    { age: "Don't attend school", value: 1 }
];

const xKey = 'value';
const yKey = 'age';

const allValues = data.map(item => item.value);
const hightNumber = Math.max(...allValues);
// console.log(hightNumber);

let evt;
let hideTooltip = false;

const longestString = data.reduce((prev, current) => {
    return prev[yKey].length > current[yKey].length ? prev : current;
});

// let tooltip = '';

// onMount(() => {
//     hoverData.subscribe(value => {
//       if (value.length > 0) {
//         tooltip = `Name: ${value[0].name}, Value: ${value[0].value}`;
//       } else {
//         tooltip = '';
//       }
//     });
// });

// const zKey = 'gender';
// const seriesNames = Object.keys(data[0]).filter(d => d !== xKey);

// data.forEach(d => {
//     d[xKey] = typeof d[xKey] === 'string' ? xKeyCast(d[xKey]) : d[xKey];
//     seriesNames.forEach(name => {
//       d[name] = +d[name];
//     });
// });

// const groupedData = groupLonger(data, seriesNames, {
//     groupTo: zKey,
//     valueTo: yKey
// });

// const annotations = [{
//         text: 'Age',
//         top: '-22px',
//         left:'-10px',
//     }
// ];

</script>

<style>
.chart-container {
    width: 100%;
    height: 350px;
}

</style>

<div class="chart-container">
    <!-- xDomain={[0, (hightNumber + 8 || 100)]} percentRange -->
    <LayerCake
        padding={{ top: 50, right: 0, bottom: 20, left: 0 }} 
        x={xKey}
        y={yKey}
        yScale={scaleBand().paddingInner(0.6)}
        xDomain={[0, (hightNumber ? hightNumber + 8 : null)]}
        yDomainSort={false}
        debug={false}
        data={data}
    >
        <Svg>
            <AxisY
                labelPosition={"above"}
                dx={longestString[yKey].length * 7.25}
                dy={-23}
                ticks={false}
                gridlines={false}
            />
            
            <Bar 
                fill="#0D369A"
                on:mousemove={event => evt = hideTooltip = event}
                on:mouseout={() => (hideTooltip = true)}
            />
        </Svg>
        <Html pointerEvents={false}>
         <svelte:fragment>   
            <Labels
                labels={data}
                getLabelName={(d) => d.value} 
                formatLabelName={(d) => d.toString() + "%"}
            />
            {#if hideTooltip !== true}
              <Tooltip
                {evt}
                let:detail
              >
              {@const tooltipData = { ...detail.props }}
                <div>
                    <div><span class="text-slate-500">Enrolment status:</span> {tooltipData.age}</div>
                    <div><span class="text-slate-500">Percentage:</span> {tooltipData.value}%</div>
                </div>
              </Tooltip>
            {/if}
        </svelte:fragment>
        </Html>
    </LayerCake>
</div>
