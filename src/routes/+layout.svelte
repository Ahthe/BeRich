    <script>
        import Navbar from '../components/Navbar.svelte'
        import '../style.css'
    </script>
<script context="module">

    export const prerender = true

</script>
<style>
    /*:global(body) {*/
    /*    overflow: hidden;*/
    /*    overscroll-behavior: none;*/
    /*}*/
</style>
<div class="container mx-auto max-w-screen-md md:border-l md:border-r md:h-screen  border-gray-100 bg-background">
    <Navbar subPath='Stock Trader'/>
    <slot/>
</div>