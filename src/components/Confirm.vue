<template>
    <transition name="fade">
        <div class="d-f jc-c ac-c ai-fs pt-10 p-fx z-fixed t-0 l-0 r-0 b-0 bg-opq-dark-sm" v-if="show">
            <div class="confirm-box bdr-5 bgc-white mt-10" style="min-width: 300px">

                <div class="confirm-msg p-4 bdB" v-html="message"></div>

                <div class="confirm-btns d-f jc-sb pl-4 pr-4 pt-3 pb-3">

                    <button type="button"
                            @click="notAccepted()"
                            v-text="cancelText"
                            class="btn btn-secondary py-2 px-4 bdr-full label ls-16 d-f ai-c">Cancel
                    </button>

                    <button type="button"
                            @click="accepted()"
                            v-text="confirmText"
                            class="btn btn-primary py-2 px-4 bdr-full label ls-16 d-f ai-c">
                    </button>
                </div>
            </div>
        </div>
    </transition>
</template>

<script>
    export default {
        name: "vue-confirm",

        data() {
            return {
                message: null,
                show: null,
                cancelText: 'Cancel',
                confirmText: 'Confirm',
                data: {}
            }
        },

        mounted() {
            Event.listen('confirm', this.showWindow);

            this.$watch('show', val => !val ? this.data = {} : '');

            document.addEventListener("keydown", (e) => {
                if (this.show && e.keyCode === 27) {
                    this.show = false
                }
            });
        },

        methods: {

            showWindow(data) {
                this.message = data.message;
                this.data.resolve = data.resolve;
                this.data.reject = data.reject;
                this.cancelText = data.cancelText ? data.cancelText : this.cancelText;
                this.confirmText = data.confirmText ? data.confirmText : this.confirmText;
                this.show = true;
            },

            accepted() {
                this.data.resolve('accepted');
                this.show = false;
            },

            notAccepted() {
                this.data.reject('not accepted');
                this.show = false;
            }

        }
    }
</script>