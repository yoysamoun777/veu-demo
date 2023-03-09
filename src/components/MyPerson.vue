<template>
    
    <div class="container">
        <ul>
            <li v-for="person in persons" v-on:click="person.show = !person.show">
                <h4> {{ person.name }} </h4>
                <h6 v-show="person.show">{{ person.Job }}</h6>
            </li>
        </ul>
    </div>

</template>


<script>
    export default {
        data() {
            return {
                persons: [
                    {name: 'Y.SAMOUN', Job: 'Web Developer', show: false},
                    {name: 'ETHELANO', Job: 'Web Developer', show: false},
                    {name: 'SHISCO', Job: 'Web Developer', show: false},
                    {name: 'TANOUN', Job: 'Web Developer', show: false},
                    {name: 'RUINSI', Job: 'Web Developer', show: false},
                    {name: 'AMORU', Job: 'Web Developer', show: false}
                ]
            }
        }
    }
</script>

<style scoped>
    div {
        padding: 20px;
        display: flex;
        justify-content: center;
        align-items: center;
        flex-direction: none;
        
    }

    ul li {
        list-style: none;
        display: inline-block;
        padding: 30px 20px;
        margin: 10px 20px;
        color:black;
        border: 2px solid #feee;
        background-color: blueviolet;
        width:90px;
        text-align: center;

    }
    h6 {
        color:white;
        text-align: center;
        padding: 0 auto;
    }
</style>