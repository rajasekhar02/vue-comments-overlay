<template>
  <div>
    <comments-overlay
        v-for="target in targets"
        :target="target"
        @create="handleCreate"
        :key="target.id">
    </comments-overlay>
  </div>

</template>

<script>
import CommentsOverlay from "./CommentsOverlay";

export default {
  components: { CommentsOverlay },
  data:function(){
    return{
      ownerData:{},
    }
  },
  computed: {
    targets() {
      return this.$root.targets;
    }
  },
  async mounted(){
    const response = await this.$root.axiosObj.get('/user');
    // console.log(response)
    this.ownerData = response.data;
  },
  methods:{
    async handleCreate(params){
      const response = await this.$root.axiosObj.post(`/repos/${this.ownerData.login}/${this.$root.github_repo}/issues`,{title:'kajdsjfkaj;dslf',body:JSON.stringify({title:'asdfasdf',body:params,title:'Vue Component Overlay'})});
      console.log(response)
    }
  }
};
</script> 