<template>
  <div>
    <h1>Event #{{ $route.params.id }}</h1>

    <div>
      {{ event }}
    </div>
  </div>
</template>

<script>
import { mapState } from 'vuex';

export default {
  async fetch({ store, error, params }) {
    try {
      await store.dispatch('events/fetchEvent', params.id);
    } catch (e) {
      error(e);
    }
  },
  head() {
    return {
      title: 'Event #' + this.event.id
    };
  },
  computed: {
    ...mapState({ event: (state) => state.events.event })
  }
};
</script>