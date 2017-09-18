<script>
import Ideas from './components/Ideas.vue';
import Input from './components/Input.vue';
import Lspi from 'lspi';

const lspi = new Lspi();

const loadIdeas = () => {
  const ideas = lspi.getRecord('ideas');

  if (ideas) {
    return ideas;
  } else {
    lspi.setRecord('ideas', [])
    return lspi.getRecord('ideas');
  }
};

export default {
  data() {
    return {
      ideas: loadIdeas()
    }
  },
  methods: {
    setIdeas() {
      lspi.setRecord('ideas', this.ideas)
    },
    addIdea(obj) {
      this.ideas.unshift(obj)
      this.seIdeas()
    },
    deleteIdea(index) {
      this.ideas = this.ideas.filter((el, i) => i !== index)
      this.setIdeas()
    },
    updateBody(event, index) {
      this.updateIdea('body', event.target.textContent, index)
    },
    updateTitle(event, index) {
      this.updateIdea('title', event.target.textContent, index)
    },
    updateIdea(type, value, index) {
      this.ideas[index][type] = value
      this.setIdeas()
    }
  },
  components: {
    'ideas': Ideas,
    'idea-input': Input
  }
}
</script>

<template>
  <main id='app'>
    <idea-input
      :addIdea='addIdea' >
    </idea-input>
    <ideas
      :ideas='ideas'
      :deleteIdea='deleteIdea'
      :updateBody='updateBody'
      :updateTitle='updateTitle' >
    </ideas>
  </main>
</template>t

<style>
  body {
    font-family: Helvetica, sans-serif;
  }
</style>