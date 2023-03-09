<template>
    <h1>This is Child Component!</h1>
    <!-- <h3>{{ person }}</h3> -->
    <ul>
        <li v-for="user in users">
            {{ user.name }} - {{ user.Job }}
        </li>
    </ul>
</template>


<script>
    export default {
        name: 'Child',
        props: ['users']
    }
</script>


<style>

</style>