<script>
export default {
    data() {
        return {
            errors: [],
            isSubmitting: false,
            formData: StorageHub.formData
        }
    },

    methods: {
        FormSubmit(event) {
            this.isSubmitting = true

            axios({
                method: event.target.method,
                url: event.target.action,
                data: new FormData(event.target)
            }).then((res) => {

                this.errors = []

                console.clear()

                EventHub.fire('showNotif', {
                    title: 'Success',
                    body: 'All Good',
                    type: 'success',
                    duration: 3,
                    icon: false,
                    onClose() {
                        // what to do on notification close
                    }
                })

            }).catch((error) => {
                this.isSubmitting = false

                if (error.response) {
                    this.errors = error.response.data.errors
                } else {
                    EventHub.fire('showNotif', {
                        title: 'Error',
                        body: error.message,
                        type: 'danger'
                    })
                }
            })
        }
    },
    render () {}
}
</script>
