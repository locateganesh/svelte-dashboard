<script>
    // import { onMount } from 'svelte';
    import Card from "../components/Atoms/Card.svelte";
    // import ColumnBar from "../charts/column-bar.svelte";
    import Bar from "../charts/bar.svelte";
    import StackedBar from "../charts/stackedBar.svelte"; 
    import ChartHeader from "../components/Molecules/chartHeader.svelte";
    
</script>
<main id="main-content" class="main-cards flex-1 flex flex-wrap">
    <!-- <div class="chart-sections">
        <Card>
            <h3 class="pl-[10px] mb-[10px]">Column Bar</h3>
            <ColumnBar />
        </Card>
    </div> -->
    <div class="chart-sections">
        <Card customClass="charts">
            <ChartHeader title="Children's enrolment in school" text="Percentage of respondent's whose children have been enrolled at an educational institution" />
            <div class="pt-[15px] pb-[15px]">
                <Bar />
            </div>
            <div class="text-right">N=1,894</div>
        </Card>
    </div>
    <div class="chart-sections">
        <Card customClass="charts">
            <ChartHeader title="Discrimination in host countries" text="percentage of respondents who have experienced unfair or unequal treatment in the country of survey:" />
            <div class="flex mt-[15px]">
                <div class="flex items-center mr-[20px]"><div class="bg-[#03369a] preference"></div> No</div>
                <div class="flex items-center mr-[20px]"><div class="bg-[#ff671f] preference"></div> Yes</div>
                <div class="flex items-center"><div class="bg-[#5b5b5b] preference"></div> Prefer not to answer</div>
            </div>
            <div class="pt-[15px] pb-[15px]">
                <StackedBar />
            </div>
            <div class="text-right">N=10,934</div>
        </Card>
    </div>
</main>
<style>
    .chart-sections {
        width: 100%;
        height: 100%;
    }
    .preference {
        width:15px;
        height: 15px;
        border-radius: 100%;
        margin-right: 10px;
    }
</style>