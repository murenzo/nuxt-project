<template>
  <div>
    <h2>Events</h2>
    <EventCard
      v-for="(event, index) in events"
      :key="index"
      :event="event"
      :data-index="index"
    />
  </div>
</template>
<script>
import EventCard from '@/components/EventCard'
export default {
  components: {
    EventCard
  },
  async asyncData({ $axios, error }) {
    try {
      const { data } = await $axios.get('http://localhost:3001/events')
      return {
        events: data
      }
    } catch (e) {
      error({
        statusCode: 503,
        message: 'Unable to fetch event list from server at this time'
      })
    }
  },
  head() {
    return {
      title: 'Event Listing',
      meta: [
        {
          hid: 'description',
          name: 'description',
          content:
            'Where you can find all the events taken place in your neighbourhood'
        }
      ]
    }
  }
}
</script>
