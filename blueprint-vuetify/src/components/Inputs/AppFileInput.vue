<template>
    <v-file-input
        v-model="file"
        :rules="[required,minFiles,maxFiles]"
        :accept="proprieties.accept"
        :show-size="proprieties.showSize"
        :chips="proprieties.chips"
        :multiple="proprieties.multiple"
        :label="proprieties.label"
        :placeholder="proprieties.placeholder"
        :disabled="proprieties.disabled"
        :id="proprieties.id"
        :class="proprieties.class"
        :hint="proprieties.hint"
        :clearable="proprieties.clearable"
        :color="proprieties.color"
        :loading="proprieties.loading"
    ></v-file-input>
</template>
<script>
    export default {
        data: () => (
            {
                file: ''
            }
        ),
        props: {
            proprieties: {
                type: Object,
                default: () => ({})
            },
            rules: Object
        },
        methods: {
            required (v) {
                if(this.rules && this.rules.required){
                    const msg = this.rules.required.msg ? this.rules.required.msg : 'This field is required'
                    return (Array.isArray(v) && v.length > 0) || msg;
                }
                return true
            },
            minFiles(v){
                if(this.rules && this.rules.minFiles && this.rules.minFiles.value){
                    const msg = this.rules.minFiles.msg ? this.rules.minFiles.msg : 'Min '+this.rules.minFiles.value+' files'
                    return (Array.isArray(v) && v.length >= this.rules.minFiles.value) || msg
                }
                return true
            },
            maxFiles(v){
                if(this.rules && this.rules.maxFiles && this.rules.maxFiles.value){
                    const msg = this.rules.maxFiles.msg ? this.rules.maxFiles.msg : 'Max '+this.rules.maxFiles.value+' files'
                    return (Array.isArray(v) && v.length <= this.rules.maxFiles.value) || msg
                }
                return true
            }
        },
        watch: {
            file(newValue) {
                this.$emit('inputValue', newValue);
            }
        },
        mounted() {
            if (this.proprieties.value !== undefined) {
                this.file = this.proprieties.value;
            }
        }
    }
</script>