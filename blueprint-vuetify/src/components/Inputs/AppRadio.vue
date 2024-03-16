<template>
    <v-radio-group
        v-model="inputValue"
        :rules="[required]"
        :label="proprieties.label"
        :disabled="proprieties.disabled"
        :id="proprieties.id"
        :class="proprieties.class"
        :color="proprieties.color"
        :inline="proprieties.inline"
    >
        <v-radio
            v-for="item in items"
            :key="item.value"
            :value="item.value"
            :label="item.label"
        ></v-radio>
    </v-radio-group>
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
            items: Array,
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