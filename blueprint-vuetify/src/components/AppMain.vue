<template>
    <v-main>
        <v-btn @click="logValue">Button</v-btn>
    </v-main>
</template>

<script>
    export default {
        data: () => (
            {
                value: ''
            }
        ),
        methods: {
            handleValueChange(newValue) {
                this.value = newValue;
            },
            logValue() {
                console.log(this.value);
            }
        }
    }
</script>