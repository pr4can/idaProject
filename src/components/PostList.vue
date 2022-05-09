<template>
    <div class="post-list">
        <transition-group name="post-animate-list">
            <post 
                v-for="post in posts"
                :post="post"
                :key="post.id"
                @remove="$emit('remove', post)"
                class="post-list__item"
            ></post>
        </transition-group>
    </div>
</template>

<script>
import Post from "@/components/Post";

export default {
    components: {
        Post
    },
    props: {
        posts: {
            type: Array,
            required: true
        }
    }
};
</script>

<style lang="scss" scoped>
.post-list {
    display: grid;
    grid-template-columns: repeat(3, 1fr);
    column-gap: 16px;
    row-gap: 16px;
    @media screen and (max-width: 1200px) {
        grid-template-columns: repeat(2, 1fr);
    }
    @media screen and (max-width: 991px) {
        grid-template-columns: repeat(1, 1fr);
    }
}
.post-animate-list-enter-active,
.post-animate-list-leave-active {
    transition: all 0.5s ease;
}
.post-animate-list-enter-from,
.post-animate-list-leave-to {
    opacity: 0;
    transform: translateY(30px);
}
.post-animate-list-move {
  transition: transform 0.3s ease;
}
</style>
