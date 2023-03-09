<template>
    <div>
        <header class="header">
            <slot name="header"></slot>
        </header>

        <main class="main">
            <slot name="main"></slot>
        </main>

        <footer class="footer">
            <slot class="footer"></slot>
        </footer>
    </div>
</template>


<script>
    export default {
        name: 'BaseLayout'
    }
</script>

<style>

</style>