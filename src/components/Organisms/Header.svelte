<script>
    import SectionWrapper from '../Atoms/SectionWrapper.svelte';
    import Navbar from '../Molecules/Navbar.svelte'
</script>

<header class="bg-green text-white pt-[5px]">
    <SectionWrapper>
     <div class="flex justify-between items-center">
        <div>Logo</div>
        <div class="text-center">
            <h1>Dashboard</h1>
        </div>
        <div>6 Countries</div>
     </div>
     <Navbar />
    </SectionWrapper>
</header>