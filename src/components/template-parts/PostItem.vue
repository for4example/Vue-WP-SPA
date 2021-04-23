<template>

  <a :href="post.link">
    <responsive-image
      v-if="post.featured_media"    
      :media-id="post.featured_media"
    />
      <h3 class="blog-title">{{post.title.rendered}}</h3>
    

  </a>
</template>

<script>
import ResponsiveImage from '@/components/utility/ResponsiveImage'
import PostMeta from '@/components/utility/PostMeta'
import PostTaxonomies from '@/components/utility/PostTaxonomies'

export default {
  
  name: 'PostItem',
  components: {
    ResponsiveImage,
    PostMeta,
    PostTaxonomies
  },
  props: {
    post: {
      type: Object,
      required: true
    }
  },
  data() {
    return {
    }
  },



}
</script>

<style>

</style>
