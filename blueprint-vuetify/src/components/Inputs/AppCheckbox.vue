<template>
    <v-checkbox
        v-model="inputValue"
        :rules="[required]"
        :label="proprieties.label"
        :disabled="proprieties.disabled"
        :indeterminate="proprieties.indeterminate"
        :id="proprieties.id"
        :class="proprieties.class"
        :color="proprieties.color"
    ></v-checkbox>
</template>
<script>
    export default {
        data: () => (
            {
                inputValue: ''
            }
        ),
        props: {
            proprieties: {
                type: Object,
                default: () => ({})
            },
            rules: Object,
        },
        methods: {
            required (v) {
                if(this.rules && this.rules.required){
                    const msg = this.rules.required.msg ? this.rules.required.msg : 'This field is required'
                    return !!v || msg
                }
                return true
            }
        },
        watch: {
            inputValue(newValue) {
                this.$emit('inputValue', newValue);
            }
        },
        mounted() {
            if (this.proprieties.value !== undefined) {
                this.inputValue = this.proprieties.value;
            }
        }
    }
</script>