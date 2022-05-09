<template>
    <form class="form" @submit.prevent>
        <div class="form__inputs">
            <my-input
                class="form__input"
                :id="'name-id'"
                :label="'Наименование товара'"
                :placeholder="'Введите наименование товара'"
                :required="true"
                v-model="post.title"
            ></my-input>
            <my-textarea
                class="form__input"
                :id="'desc-id'"
                :label="'Описание товара'"
                :placeholder="'Введите описание товара'"
                :required="false"
                v-model="post.desc"
            ></my-textarea>
            <my-input
                class="form__input"
                :id="'img-id'"
                :label="'Ссылка на изображение товара'"
                :placeholder="'Введите ссылку'"
                :required="true"
                v-model="post.img"
            ></my-input>
            <my-input
                class="form__input"
                :id="'cost-id'"
                :label="'Цена товара'"
                :placeholder="'Введите цену'"
                :required="true"
                v-model="post.cost"
                @input="numberDivide"
            ></my-input>
        </div>
        <my-button @click="createPost" class="form__button" :disabled="disabledForm">Добавить товар</my-button>
    </form>
</template>

<script>
export default {
    data() {
        return {
            post: {
                id: "",
                title: "",
                desc: "",
                img: "",
                cost: ""
            },
            disabledForm: true
        }
    },
    methods: {
        numberDivide(event) {
            const res = event.target.value.replace(/[^\d.]/g,"");
            this.post.cost = res.replace(/\d{1,3}(?=(\d{3})+(?!\d))/g, "$& ");
        },
        createPost() {
            this.post.id = Date.now();
            this.$emit('create', this.post);

            this.post = {
                id: "",
                title: "",
                desc: "",
                img: "",
                cost: ""
            }
        },
        validateForm() {
            if (this.post.title && this.post.img && this.post.cost) {
                this.disabledForm = false;
                return;
            }
            this.disabledForm = true;
        }
    },
    watch: {
        post: {
            handler() {
                this.validateForm();
            },
            deep: true
        }
    }
};
</script>

<style lang="scss" scoped>
.form {
    padding: 24px;
    border-radius: 4px;
    background-color: #fffefb;
    box-shadow: 0 20px 30px 0 rgba(0, 0, 0, 0.04),
        0 6px 10px 0 rgba(0, 0, 0, 0.02);
    &__inputs {
        margin-bottom: 24px;
        & > *:not(:last-child) {
            margin-bottom: 16px;
        }
    }
}
</style>
