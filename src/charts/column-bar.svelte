<script>
    // import { onMount } from 'svelte';
    import { LayerCake, Svg, Html } from 'layercake';
    import { scaleBand } from 'd3-scale';
    // import { onMount } from 'svelte';

    import Column from '../_components/Column.svelte';
    // import Bar from '../_components/Bar.svelte';
    import AxisX from '../_components/AxisX.percent-range.html.svelte';
    import AxisY from '../_components/AxisY.percent-range.html.svelte';
    import Annotations from '../_components/Annotations.html.svelte';
    
    const data = [
        { gender: "Male", value: "79" },
        { gender: "Female", value: "20" },
        { gender: "Prefer Not to Answer", value: "1" }
    ];
    const xKey = 'gender';
    const yKey = 'value';

    data.forEach(d => {
      d[yKey] = +d[yKey];
    });

    // const annotations = [{
    //     text: 'Gender',
    //     top: '-22px',
    //     left:'-10px',
    //     }
    // ];

    
</script>

<div class="chart-container">
    <!-- yDomain={[0, null]}-->
    <LayerCake
        padding={{ top: 20, right: 20, bottom: 20, left: 20 }}
        x={xKey}
        y={yKey}
        xScale={scaleBand().paddingInner(0.05)}
        yDomain={[0, null]}
        
        {data}
    >
        <Svg>
            <AxisX
                tickMarks
                baseline
                snapLabels
            />
            <AxisY
                tickMarks
                gridlines={false}
            />
            <Column fill="#0D369A" />
            <!-- <Bar fill="#0D369A" /> -->
        </Svg>
        <Html>
            <!-- <Annotations {annotations}/> -->
        </Html>
    </LayerCake>
</div>


<style>
    .chart-container {
        width: 100%;
        height: 400px;
        /* border: 1px solid red; */
    }
</style>