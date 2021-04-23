<template>
  <main>
    <section v-if="posts.length">
    <div class="parent">
      <post-item v-for="(post, index) in posts.slice(0, 7)" :key="post.id" :post="post" :class="'div' + ++index"/>
      </div>
      <pagination v-if="totalPages > 1" :total="totalPages" :current="page" />
    </section>
  </main>
</template>

<script>
import PostItem from '@/components/template-parts/PostItem'
import Pagination from '@/components/template-parts/Pagination'

export default {
  name: 'Home',
  components: {
    PostItem,
    Pagination
  },
  props: {
    page: {
      type: Number,
      required: true
    }
  },
  data() {
    return {
      holder: 0,
      request: {
        type: 'posts',
        params: { 
          per_page: this.$store.state.site.posts_per_page,
          page: this.page
        }, 
        showLoading: true 
      },
      totalPages: 0
    }
  },
  computed: {
    posts() {
      return this.$store.getters.requestedItems(this.request)
    }
  },
  methods: {
    increment() {
      this.holder = this.holder + 1;
      return this.holder;
    },
    getPosts() {
      return this.$store.dispatch('getItems', this.request)
    },
    setTotalPages() {
      this.totalPages = this.$store.getters.totalPages(this.request)
    }
  },
  created() {
    this.getPosts().then(() => this.setTotalPages())
  }
}
</script>
