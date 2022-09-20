<script setup>

import BlogPost from './components/BlogPost.vue';
import { computed, ref,onMounted } from 'vue';
import ButtonGroup from './components/ButtonGroup.vue';
import LoadingSpinner from './components/LoadingSpinner.vue';
const posts=ref([
])
const fav=ref("")
const loading=ref(true)
const postXpage=10
const init=ref(0)
const end=ref(postXpage)
const maxLength=computed(()=>posts.value.length)
const addFav=(title)=>{
  fav.value=title
}

onMounted (async()=>{
loading.value=true
try{
const res=await fetch("https://jsonplaceholder.typicode.com/posts")
posts.value=await res.json()
}catch(error){console.log(error)}
finally{
  setTimeout(()=>(loading.value=false),1500)
}
})

const next=()=>{
  init.value=init.value+postXpage
  end.value=end.value+postXpage
}
const prev=()=>{
  init.value=init.value-postXpage
  end.value=end.value-postXpage
}
</script>

<template>
  <LoadingSpinner v-if="loading"/>
  <div class="container" v-else>
<h1>Blog</h1>
<h2>My favorite:{{fav || "No fav"}}</h2>
<ButtonGroup
:init="init"
:end="end"
:maxLength="maxLength"
@paginateNext="next"
@paginatePrev="prev"
 class="mb-2"></ButtonGroup>
<BlogPost 
v-for="post in posts.slice(init,end)"
:key="post.title"
:title="post.title"
:id="post.id"
:body="post.body"
:colorText="post.colorText"
class="mb-2"
@myfav="addFav"></BlogPost>
</div>
</template>

