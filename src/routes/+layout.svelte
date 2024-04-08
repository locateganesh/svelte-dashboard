<script>
  import "../app.css";
  import Header from "../components/Organisms/Header.svelte";
  import Sidebar from "../components/Organisms/Sidebar.svelte";
  import Footer from "../components/Organisms/Footer.svelte";
</script>

<div class="flex flex-col min-h-[100vh]">
    <Header />
    <div class="flex flex-1 p-[10px]">
        <Sidebar />
        <slot />
    </div>
    <Footer />
</div>




<!---
Atomic Desing components:

Atoms
Malecules
Orgamisms

-->