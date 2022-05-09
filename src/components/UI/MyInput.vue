<template>
    <div class="input" 
        :class="{
            'input--required': required,
            'input--invalid': isError
            }
    ">
        <label :for="id">{{label}}</label>
        <input 
            type="text"
            autocomplete="off"
            :id="id"             
            :placeholder="placeholder"
            :value="modelValue" 
            @input="updateInput"
            @blur="checkInput"
        />
        <transition name="fade">
            <p v-if="isError">Поле является обязательным</p>
        </transition>        
    </div>
</template>

<script>
export default {
    name: "my-input",
    props: {
        required: {
            type: Boolean,
            default: false
        },
        id: {
            type: [String, Number],
            required: true
        },
        label: {
            type: String,
            required: true
        },
        placeholder: {
            type: String,
            required: true
        },
        modelValue: [String, Number]
    },
    data() {
        return {
            isError: false
        }
    },
    methods: {
        updateInput(event) {
            this.$emit('update:modelValue', event.target.value)
        },
        checkInput(event) {
            if (!this.required) return;
            if (event.target.value) {
                this.isError = false;
                return;
            }
            this.isError = true;
        }
    }
};
</script>

<style lang="scss" scoped>
.input {
    position: relative;
    display: flex;
    flex-direction: column;
    align-items: flex-start;
    label {
        position: relative;
        font-size: 10px;
        line-height: 13px;
        letter-spacing: -0.02em;
        padding-right: 0.04em;
        color: #49485e;
        margin: 0 0 4px;
        user-select: none;
    }
    &--required label {
        &::after {
            content: "";
            position: absolute;
            left: 100%;
            top: 0;
            width: 4px;
            height: 4px;
            border-radius: 50%;
            background-color: #ff8484;
        }
    }
    input {
        font-size: 12px;
        line-height: 15px;
        color: #3f3f3f;
        width: 100%;
        padding: 8px 14px;
        background-color: #fffefb;
        border-radius: 4px;
        border: 1px solid transparent;
        box-shadow: 0 2px 5px 0 rgba(0, 0, 0, 0.1);
        transition: 0.3s border;
        &::placeholder {
            color: #b4b4b4;
        }
        &:focus {
            border-color: #3f3f3f;
        }
    }
    &--invalid input {
        border-color: #ff8484;
    }
    p {
        position: absolute;
        left: 0;
        top: calc(100% + 4px);
        font-size: 8px;
        line-height: 10px;
        letter-spacing: -0.02em;
        padding-right: 0.04em;
        color: #ff8484;
        margin: 0;
    }
    &--invalid p {
        display: block;
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
