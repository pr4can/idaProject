<template>
    <div class="post">
        <a href="" @click.prevent="$emit('remove', post)" class="post__delete"><img src="@/assets/img/delete.svg" alt=""/></a>
        <div class="post__img"><img :src="post.img" alt="" /></div>
        <div class="post__info">
            <h4 class="post__name">{{ post.title }}</h4>
            <p class="post__desc">{{ post.desc }}</p>
            <p class="post__cost">{{ post.cost }} руб.</p>
        </div>
    </div>
</template>

<script>
export default {
  props: {
    post: {
      type: Object,
      required: true,
    }
  }
}
</script>

<style lang="scss" scoped>
.post {
    position: relative;
    display: flex;
    flex-direction: column;
    height: auto;
    box-shadow: 0 20px 30px 0 rgba(0, 0, 0, 0.04),
        0 6px 10px 0 rgba(0, 0, 0, 0.02);
    border-radius: 4px;
    background-color: #fffefb;
    &__delete {
        position: absolute;
        right: -8px;
        top: -8px;
        display: flex;
        align-items: center;
        justify-content: center;
        width: 32px;
        height: 32px;
        background-color: #ff8484;
        border-radius: 10px;
        box-shadow: 0 2px 4px 0 rgba(0, 0, 0, 0.1);
        opacity: 0;
        transition: 0.3s opacity, 0.3s background;
        z-index: 2;
        &:hover {
            background-color: #ff3737;
        }
    }
    &:hover .post__delete {
        opacity: 1;
    }
    &__img {
        position: relative;
        padding-top: 60%;
        border-radius: 4px 4px 0 0;
        overflow: hidden;
        & > img {
            position: absolute;
            left: 0;
            top: 0;
            width: 100%;
            height: 100%;
            object-fit: cover;
            object-position: center;
        }
    }
    &__info {
        display: flex;
        flex-direction: column;
        align-posts: flex-start;
        height: auto;
        padding: 16px 16px 24px;
    }
    &__name {
        font-family: SourceSansPro-SemiBold;
        font-size: 20px;
        line-height: 25px;
        color: #3f3f3f;
        margin: 0 0 16px;
    }
    &__desc {
        font-size: 16px;
        line-height: 20px;
        color: #3f3f3f;
        margin: 0 0 32px;
    }
    &__cost {
        font-family: SourceSansPro-SemiBold;
        font-size: 24px;
        line-height: 30px;
        color: #3f3f3f;
        margin: auto 0 0;
    }
}
</style>
