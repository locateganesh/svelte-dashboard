<script>
    import { LayerCake, Svg, flatten, stack, Html } from 'layercake';
    // import { stack } from 'd3-shape';
    import { scaleBand, scaleOrdinal } from 'd3-scale';
    // import { format } from 'd3-format';
  
    import BarStacked from '../_components/BarStacked.svelte';
    // import Labels from '../_components/Labels.html.svelte';
    import AxisX from '../_components/AxisX.svelte';
    import AxisY from '../_components/AxisY.svelte';
  
    // This example loads csv data as json using @rollup/plugin-dsv
    // import data from './_data/fruitOrdinal.csv';
    const data = [
      {contries: 'All Surveyed countries (Average)', no: 90, yes: 8, preferNotToAnswer: 2},
      {contries: 'Slovakia', no: 85, yes: 12, preferNotToAnswer: 3},
      {contries: 'Poland', no: 85, yes: 12, preferNotToAnswer: 3},
      {contries: 'Hungary', no: 90, yes: 8, preferNotToAnswer: 2},
      {contries: 'Latvia', no: 92, yes: 8, preferNotToAnswer: 0},
      {contries: 'Republic of Moldova', no: 94, yes: 6, preferNotToAnswer: 0},
      {contries: 'Romania', no: 95, yes: 5, preferNotToAnswer: 0},
    ];
  
    const xKey = [0, 1];
    const yKey = 'contries';
    const zKey = 'key';
  
    const seriesNames = Object.keys(data[0]).filter(d => d !== yKey);
    //const seriesColors = ['#00bbff', '#8bcef6', '#c4e2ed', '#f7f6e3'];
    const seriesColors = ['#03369a', '#ff671f', '#5b5b5b'];
    // const formatLabelX = d => format(`~s`)(d);  
    const stackedData = stack(data, seriesNames);

    const longestString = data.reduce((prev, current) => {
      return prev[yKey].length > current[yKey].length ? prev : current;
    });


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
        />
        <!-- <Labels class='labels' 
              values={(data, xGet, yGet) => data.map(d => ({...d, x: xGet(d), y: yGet(d)}))} 
              x={(d) => d.x} 
              y={(d) => d.y} 
              label={(d) => d.value}>
          {(props) => props.label}
        </Labels> -->
      </Svg>
      <Html>
        <!-- <Labels
          values={(data, xGet, yGet) => data.map(d => ({...d, x: xGet(d), y: yGet(d)}))} 
          x={(d) => d.x} 
          y={(d) => d.y} 
          label={(d) => d.value}
        /> -->
      </Html>
    </LayerCake>
  </div>