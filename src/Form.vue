<template></template>

<script>
    export default {
        data() {
            return {
                errors: [],
                isSubmit: false,
                formData: StorageHub.formData
            }
        },

        methods: {
            FormSubmit(event) {
                this.isSubmit = true;

                axios({
                    method: event.target.method,
                    url: event.target.action,
                    data: this.formData
                }).then(({data}) => {

                    this.errors = [];

                    console.clear()

                    const status = data.status ? data.status : 'Thank You';

                    EventHub.fire('showNotif',{
                        title: 'Success',
                        body: status,
                        type: 'success',
                        duration: 1,
                        onClose(){
                            // window.location.replace('/')
                        }
                    });

                }).catch(error => {
                    this.isSubmit = false;

                    if (error.response) {
                        this.errors = error.response.data
                    } else {
                        EventHub.fire('showNotif',{
                            title: 'Error',
                            body: error.message,
                            type: 'danger'
                        });
                    }
                })
            }
        }
    }
</script>
