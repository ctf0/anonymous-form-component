<template></template>

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
            }).then(({data}) => {

                this.errors = []

                console.clear()

                const status = data.status ? data.status : 'Thank You'

                EventHub.fire('showNotif', {
                    title: 'Success',
                    body: status,
                    type: 'success',
                    duration: 3,
                    icon: false,
                    onClose() {
                        window.location.replace('/')
                    }
                })

            }).catch((error) => {
                this.isSubmitting = false

                if (error.response) {
                    this.errors = error.response.data
                } else {
                    EventHub.fire('showNotif', {
                        title: 'Error',
                        body: error.message,
                        type: 'danger'
                    })
                }
            })
        }
    }
}
</script>
