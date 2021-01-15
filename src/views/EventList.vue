<template>
  <h1>Events for {{ user.user.name }}</h1>
  <div class="events">
    <EventCard v-for="event in event.events" :key="event.id" :event="event" />
    <div class="pagination">
      <router-link
        id="page-prev"
        :to="{ name: 'EventList', query: { page: page - 1 } }"
        rel="prev"
        v-if="page > 1"
      >
        &#60; Previous
      </router-link>
      <router-link
        id="page-next"
        :to="{ name: 'EventList', query: { page: page + 1 } }"
        rel="next"
        v-if="hasNextPage"
      >
        Next &#62;
      </router-link>
    </div>
    <div id="nav">
      <router-link :to="{ name: 'EventCreate' }">New Event</router-link>
    </div>
  </div>
</template>

<script>
// @ is an alias to /src
import EventCard from '@/components/EventCard.vue'
import { mapActions, mapState } from 'vuex'
import { watchEffect } from 'vue'

export default {
  name: 'EventList',
  props: ['page'],
  components: {
    EventCard
  },
  created() {
    watchEffect(() => {
      this.fetchEvents({ perPage: 3, page: this.page })
    })
  },
  computed: {
    hasNextPage() {
      return this.event.eventsTotal > this.page * 3
    },
    ...mapState(['event', 'user'])
  },
  methods: mapActions('event', ['fetchEvents'])
}
</script>

<style scoped>
.events {
  display: flex;
  flex-direction: column;
  align-items: center;
}
.pagination {
  display: flex;
  width: 290px;
}
.pagination a {
  flex: 1;
  text-decoration: none;
  color: #2c3e50;
}
#page-prev {
  text-align: left;
}
#page-next {
  text-align: right;
}
</style>
