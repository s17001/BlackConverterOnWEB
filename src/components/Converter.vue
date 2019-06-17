<template>
    <div>
        <div>ここは説明文です</div>
        <div><textarea v-model="input" onchange="" name="" id="input" cols="30" rows="10"></textarea></div>
        <div><textarea name="" id="output" cols="30" rows="10"></textarea></div>
        <p>{{input}}</p>
    </div>
</template>

<script>
    export default {
        name: "Converter",
        data() {
            return {
                input:''
            }
        },
        methods:{

        }
    }
</script>

<style scoped>

</style>