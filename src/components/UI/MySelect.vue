<template>
    <div class="select">
        <span 
            class="select__current"
            @click="isVisible = !isVisible"
            :class="{'select__current--active': isVisible}"
        >{{ currentSelect }}</span>
        <transition name="fade">
            <ul 
                v-if="isVisible"
                class="select__options">
                <li
                    v-for="option in options"
                    :key="option.value"
                    @click="selectOption(option)"
                >
                    {{ option.name }}
                </li>
            </ul>
        </transition>
    </div>
</template>

<script>
export default {
    name: "my-select",
    props: {
        options: {
            type: Array,
            default() {
                return []
            }
        }
    },
    data() {
        return {
            currentSelect: "По умолчанию",
            isVisible: false
        }
    },
    methods: {
        selectOption(option) {
            this.$emit("select", option);
            this.currentSelect = option.name;
            this.isVisible = false;
        },
        hideSelect(event) {
            if (!document.querySelector(".select__current").contains(event.target)) {
                this.isVisible = false;
            }            
        }
    },
    mounted() {
        document.addEventListener("click", this.hideSelect.bind(this), true);
    },
    beforeDestroy() {
        document.removeEventListener("click", this.hideSelect, true);
    }
}
</script>

<style lang="scss" scoped>
.select {
    position: relative;
    display: flex;
    user-select: none;
    z-index: 99;
    &__current {
        display: flex;
        align-items: center;
        font-size: 12px;
        line-height: 15px;
        color: #B4B4B4;
        padding: 10px 16px;
        border-radius: 4px;
        background-color: #FFFEFB;
        box-shadow: 0 2px 5px 0 rgba(0, 0, 0, 0.1);
        cursor: pointer;
        transition: 0.3s box-shadow;
        &:hover {
            box-shadow: 0 2px 20px 0 rgba(0, 0, 0, 0.1);
        }
        &::after {
            content: "";
            display: block;
            width: 4.59px;
            height: 4.59px;
            border-left: 1px solid #B4B4B4;
            border-bottom: 1px solid #B4B4B4;
            transform: rotate(-45deg);
            margin-left: 5px;
            transition: 0.3s transform;
        }
        &.select__current--active {
            &::after {
                transform: rotate(135deg) translate(1px, -2px);
            }
        }
    }
    &__options {
        position: absolute;
        right: 0;
        top: calc(100% + 10px);
        min-width: 100%;
        margin: 0;        
        padding: 0;
        box-shadow: 0 2px 5px 0 rgba(0, 0, 0, 0.1);
        & > li {
            list-style: none;
            font-size: 12px;
            line-height: 15px;
            color: #3F3F3F;
            background-color: #FFFEFB;
            padding: 10px 16px;
            cursor: pointer;
            transition: 0.3s background;
            &:hover {
                background-color: #ebebeb;
            }
            &:first-child {
                border-radius: 4px 4px 0 0;
            }
            &:last-child {
                border-radius: 0 0 4px 4px;
            }
        }
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