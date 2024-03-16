<template>
    <v-main>
        <AppTextField
            @inputValue="handleValueChange"
            :proprieties="proprieties"
            :rules="rules"
        />
        <v-btn @click="logValue">Button</v-btn>
    </v-main>
</template>

<script>

    export default {
        data: () => (
            {
                value: null,
                proprieties: {
                    label: 'Text'
                },
                rules: {
                    validRegex: {
                        value: '\\d'
                    }
                }
            }
        ),
        methods: {
            handleValueChange(newValue) {
                this.value = newValue;
            },
            logValue() {
                console.log('teste');
            }
        }
    }
</script>