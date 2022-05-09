<template>
    <button class="button">
        <slot></slot>
    </button>
</template>

<script>
export default {
    name: "my-button",
};
</script>

<style lang="scss" scoped>
.button {
    font-family: Inter-SemiBold;
    font-size: 12px;
    line-height: 15px;
    color: #ffffff;
    text-align: center;
    width: 100%;
    padding: 10px;
    border-radius: 10px;
    border: none;
    background-color: #7bae73;
    box-shadow: 0 2px 4px 0 rgba(0, 0, 0, 0.1);
    cursor: pointer;
    transition: 0.3s background, 0.3s color, 0.3s box-shadow;
    &:hover {
        background-color: #489f3a;
    }
    &:disabled {
        color: #b4b4b4;
        background-color: #eeeeee;
        box-shadow: none;
        cursor: not-allowed;
    }
}
</style>
