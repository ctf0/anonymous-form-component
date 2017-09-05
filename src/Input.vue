<script>
import FormErrors from './Errors.vue'

export default {
    components: {FormErrors},
    props: ['getErrors'],
    data() {
        return {
            input: '',
            newError: false
        }
    },
    computed: {
        // to show/hide the errors
        showErrors() {
            if (this.input) {
                if (this.newError) {
                    return this.getErrors
                }
                return null
            }
            return this.getErrors
        },
        // to change the input class according to error/input
        classObject() {
            return {
                'is-danger': this.showErrors && !this.input || this.newError,
                'is-success': this.input && !this.showErrors
            }
        }
    },
    mounted() {
        if (this.$el.type == 'hidden') {
            StorageHub.formData[this.$el.name] = this.input = this.$el.value
        }
    },
    methods: {
        getName(event) {
            StorageHub.formData[event.target.name] = this.input
        }
    },
    watch: {
        getErrors(val, oldVal) {
            // we have old & new, but are diff
            if (val !== undefined && oldVal !== undefined && val !== oldVal) {
                return this.newError = true
            }

            // we have old only
            if (val == undefined && oldVal !== undefined) {
                return this.newError = false
            }

            // we have new only
            if (val !== undefined && oldVal == undefined) {
                // fire only when we have input & new error
                if (this.input) {
                    return this.newError = true
                }
            }
        }
    },
    render () {}
}
</script>
