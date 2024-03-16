<template>
    <v-autocomplete
        v-model="inputValue"
        :rules="[required,minSelected,maxSelected]"
        :items="items"
        :label="proprieties.label"
        :placeholder="proprieties.placeholder"
        :disabled="proprieties.disabled"
        :id="proprieties.id"
        :class="proprieties.class"
        :type="proprieties.type"
        :hint="proprieties.hint"
        :clearable="proprieties.clearable"
        :chips="proprieties.chips"
        :multiple="proprieties.multiple"
        :color="proprieties.color"
        :loading="proprieties.loading"
    ></v-autocomplete>
</template>
<script>
    export default {
        data: () => (
            {
                inputValue: null
            }
        ),
        props: {
            proprieties: {
                type: Object,
                default: () => ({})
            },
            items: Array,
            rules: Object
        },
        methods: {
            required (v) {
                if(this.rules && this.rules.required){
                    const msg = this.rules.required.msg ? this.rules.required.msg : 'This field is required'
                    return !!v || msg
                }
                return true
            },
            minSelected (v) {
                if(this.rules && this.rules.minSelected && this.rules.minSelected.value){
                    const msg = this.rules.minSelected.msg ? this.rules.minSelected.msg : 'Min '+this.rules.minSelected.value+' selections'
                    return (v && v.length >= this.rules.minSelected.value) || msg
                }
                return true
            },
            maxSelected (v) {
                if(this.rules && this.rules.maxSelected && this.rules.maxSelected.value){
                    const msg = this.rules.maxSelected.msg ? this.rules.maxSelected.msg : 'Max '+this.rules.maxSelected.value+' selections'
                    return (v && v.length <= this.rules.maxSelected.value) || msg
                }
                return true
            },
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