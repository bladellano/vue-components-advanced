<template>
    <div>

        <h2>Lista de posts</h2>

        <PostsListIten
            v-for="post in posts"
            :key="post.id"
            :post="post">
                <slot :meuPost="post"></slot> <!-- passagem da prop para o slot -->
        </PostsListIten>

    </div>
</template>

<script>

    import PostsListIten from '@/components/PostListIten.vue'

    export default {
        components:{
            PostsListIten
        },
        props:{
            posts:{
                type:Array,
                required: true
            }
        }
    }
</script>
