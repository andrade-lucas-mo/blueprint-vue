<template>
    <v-text-field
        v-model="inputValue"
        :rules="[required,minCaracter,maxCaracter,validEmail,validRegex]"
        :label="proprieties.label"
        :placeholder="proprieties.placeholder"
        :disabled="proprieties.disabled"
        :id="proprieties.id"
        :class="proprieties.class"
        :type="proprieties.type"
        :hint="proprieties.hint"
        :clearable="proprieties.clearable"
        :color="proprieties.color"
        :loading="proprieties.loading"
    ></v-text-field>
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
            minCaracter(v){
                if(this.rules && this.rules.minCaracter && this.rules.minCaracter.value){
                    const msg = this.rules.minCaracter.msg ? this.rules.minCaracter.msg : 'Min '+this.rules.minCaracter.value+' characters'
                    return (v && v.length >= this.rules.minCaracter.value) || msg
                }
                return true
            },
            maxCaracter(v){
                if(this.rules && this.rules.maxCaracter && this.rules.maxCaracter.value){
                    const msg = this.rules.maxCaracter.msg ? this.rules.maxCaracter.msg : 'Max '+this.rules.maxCaracter.value+' characters'
                    return (v && v.length <= this.rules.maxCaracter.value) || msg
                }
                return true
            },
            validEmail(v){
                if(this.rules && this.rules.validEmail){
                    const regex = /^[^\s@]+@[^\s@]+\.[^\s@]+$/;
                    const msg = this.rules.validEmail.msg ? this.rules.validEmail.msg : 'Invalid email'
                    return regex.test(v) || msg;
                }
                return true
            },
            validRegex(v){
                if(this.rules && this.rules.validRegex && this.rules.validRegex.value){
                    const regex = new RegExp(this.rules.validRegex.value);
                    const msg = this.rules.validRegex.msg ? this.rules.validRegex.msg : 'Invalid format'
                    return regex.test(v) || msg;
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