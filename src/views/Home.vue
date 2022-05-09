<template>

    <div class="home">
        <my-dialog class="home__dialog" v-model:show="dialogVisible">
            <span>Товар успешно добавлен!</span>
        </my-dialog>
        <div class="home__container container">
            <div class="home__row">
                <div class="home__left">
                    <h1 class="home__title">Добавление товара</h1>
                    <post-form 
                        @create="createPost"
                        class="home__form"
                    ></post-form>
                </div>
                <div class="home__right">
                    <my-select 
                        :options="sortOptions"
                        @select="selectOption"
                        class="home__select"
                    ></my-select>
                    <post-list 
                        :posts="sortedPosts"
                        @remove="removePost"
                        class="home__list-item"
                    ></post-list>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
import PostForm from "@/components/PostForm";
import PostList from "@/components/PostList";

export default {
    components: {
        PostForm,
        PostList
    },
    data() {
        return {
            dialogVisible: false,
            posts: JSON.parse(localStorage.getItem("products")) ?? [],
            sortOptions: [
                {name: "По наименованию", value: "title"},
                {name: "По возрастанию цены", value: "price-up"},
                {name: "По убыванию цены", value: "price-down"}
            ],
            selectedSort: ""
        }
    },
    methods: {
        selectOption(option) {
            this.selectedSort = option.value;
        },
        createPost(post) {
            this.posts.push(post);
            localStorage.setItem("products", JSON.stringify(this.posts));
            this.dialogVisible = true;
            setTimeout(() => {
                this.dialogVisible = false;
            }, 2000);
        },
        removePost(post) {
            this.posts = this.posts.filter(p => p.id !== post.id);
            localStorage.setItem("products", JSON.stringify(this.posts));
        },
    },
    computed: {
        sortedPosts() {
            switch(this.selectedSort) {
                case "price-up":
                    return [...this.posts].sort((post_1, post_2) => {
                        const cost_1 = +post_1.cost.split(' ').join(''),
                            cost_2 = +post_2.cost.split(' ').join('');
                        return cost_1 - cost_2;
                    });
                case "price-down":
                    return [...this.posts].sort((post_1, post_2) => {
                        const cost_1 = +post_1.cost.split(' ').join(''),
                            cost_2 = +post_2.cost.split(' ').join('');
                        return cost_2 - cost_1;
                    });
                default:
                    return [...this.posts].sort((post_1, post_2) => post_1[this.selectedSort]?.localeCompare(post_2[this.selectedSort]));
            }
            
        }
    },
}
</script>

<style lang="scss" scoped>
.home {
    padding: 32px 0;
    &__dialog {
        & span {
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 18px;
            line-height: 20px;
            color: #3F3F3F;
            text-align: center;
            &::before {
                content: "";
                display: inline-block;
                width: 15px;
                height: 15px;
                mask-image: url("@/assets/img/circle-check-solid.svg");
                mask-size: contain;
                mask-position: center;
                mask-repeat: no-repeat;
                background-color: #489f3a;
                margin-right: 10px;
            }
        }
    }
    &__row {
        display: flex;
        align-items: flex-start;
        justify-content: space-between;
        @media screen and (max-width: 676px) {
            flex-wrap: wrap;
        }
    }
    &__left {
        position: sticky;
        top: 32px;
        width: 332px;
        @media screen and (max-width: 676px) {
            position: static;
            width: 100%;
            margin-bottom: 16px;
        }
    }
    &__right {
        display: flex;
        flex-direction: column;
        width: calc((100% - 348px));
        @media screen and (max-width: 676px) {
            width: 100%;
        }
    }
    &__title {
        font-family: SourceSansPro-SemiBold;
        font-size: 28px;
        line-height: 35px;
        color: #3F3F3F;
        margin: 0 0 16px;
    }
    &__select {
        margin: 0 0 16px auto;
    }
}
</style>