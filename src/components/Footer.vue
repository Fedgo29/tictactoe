<template>
    <footer>
        <h5>Created by Fedgo</h5>
    </footer>
</template>

<script>
    export default {
        name: "AppFooter",
    };
</script>

<style scoped>
    * {
        margin: 0;
        padding: 0;
        box-sizing: border-box;
    }

    html, body {
        height: 100%; /* Asegura que el documento ocupe toda la altura */
    }
    footer{
        background-color: blue;
        color: white;
        box-shadow:  1px 2px black;
        /*margin: 0;*/
        padding: 25px;
    }
</style>