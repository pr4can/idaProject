<template>
    <transition name="fade">
        <div class="dialog" v-if="show" @click="hideDialog">
            <div @click.stop class="dialog__content">
                <slot></slot>
            </div>
        </div>
    </transition>
</template>

<script>
export default {
    name: "my-dialog",
    props: {
        show: {
            type: Boolean,
            default: false
        }
    },
    methods: {
        hideDialog() {
            this.$emit('update:show', false);
        }
    }
}
</script>

<style lang="scss" scoped>
.dialog {
    position: fixed;
    left: 0;
    top: 0;
    display: flex;
    align-items: center;
    justify-content: center;
    width: 100%;
    height: 100%;
    background-color: rgba(0, 0, 0, 0.5);
    z-index: 100;
    &__content {
        padding: 20px;
        background-color: #ffffff;
        border-radius: 12px;
        min-width: 300px;
    }
}
.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.5s ease;
}

.fade-enter-from,
.fade-leave-to {
  opacity: 0;
}
</style>