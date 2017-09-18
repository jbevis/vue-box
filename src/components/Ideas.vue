<template>
  <section class='idea-card'>
    <article v-for='(idea, index) in ideas'>
      <h1 contenteditable="true" @blur='updateTitle($event, index)'>
        {{ idea.title }}
      </h1>
      <h2 contenteditable="true" @blue='updateBody($event, index)'>
        {{ idea.body }}
      </h2>
      <h3>{{ idea.quality }}</h3>
      <button @click='deleteIdea(index)'>Delete</button>
      <hr>
    </article>
  </section>
</template>

<script>
export default {
  props: ['ideas', 'deleteIdea', 'updateTitle', 'updateBody']
}
</script>