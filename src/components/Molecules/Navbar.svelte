<script>
    import {page} from '$app/stores';
    // console.log('page', $page.route.id);
    const _routes = {
        index: '/',
        demographicProfile: "/demographic-profile"
    };
</script>

<nav>
    <ul class="flex justify-between nav-list text-md font-medium mt-[20px]" data-page={$page.route.id}>
        <li><a href={_routes.index} class:is-active={$page.route.id === _routes.index}>Overview</a></li>
        <li><a href={_routes.demographicProfile} class:is-active={$page.route.id === _routes.demographicProfile}>Demographic profile</a></li>
        <li><a href="./">Reasons of return</a></li>
        <li><a href="./">Return Condition</a></li>
        <li><a href="./">Need, challenges and assistace</a></li>
    </ul>
</nav>
<!-- class:is-active={currentRoute === "/demographic-profile"} -->
<style>
    .nav-list a {
        display: block;
        padding: 10px 20px;
        border-bottom: 3px solid transparent;
    }
    .nav-list a.is-active {
        border-color:#fff;
    }
</style>