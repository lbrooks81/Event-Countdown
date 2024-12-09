<!-- Works like the template property, it's where the HTML will go-->
<template>
  <div id="events">
    <ul>
      <li v-for="event in events" :key="event.id">
        <Event :event="event" :daysLeft="daysLeft(event)"/>
      </li>
    </ul>
  </div>
</template>

<!-- Data, methods, events go here -->
<script>

import {defineComponent} from "vue";
import Event from "@/components/Event.vue";

export default defineComponent({
  components: {Event},
  data(){
    return{
      events: eventData
    }
  },
  methods:{
    daysLeft(event){
      const eventDate = Date.parse(event.date);
      const millisecsUntilEvent = eventDate - Date.now();
      const daysRemaining = millisecsUntilEvent / (1000 * 60 * 60 * 24);
      return Math.ceil((daysRemaining));
    }
  }
})

const eventData = [
  {
    id: 1,
    name: "Graduation",
    details: "wooohoo!!!",
    date: "2025-06-02",
    background: "#F34949",
  },
  {
    id: 2,
    name: "Holidays",
    details: "Break time!",
    date: "2024-12-24",
    background: "#f9f970",
  },
  {
    id: 3,
    name: "Birthday",
    details: "My birthday party",
    date: "2025-01-08",
    background: "#F07AEC",
  },
  {
    id: 4,
    name: "Next Christmas",
    details: "ho ho ho",
    date: "2025-12-25",
    background: "#165b33",
  },
  {
    id: 5,
    name: "Thanksgiving",
    details: "Turkey time",
    date: "2024-11-28",
    background: "#EB9A0F",
  },
  {
    id: 6,
    name: "Conference Talk",
    details: "dont flop",
    date: "2025-02-28",
    background: "#68EE94",
  },
];

</script>


<!-- scoped makes it isolated CSS; it only applies to this template and nothing else -->
<style scoped>
ul
{
  padding: 0;
}

li
{
  list-style: none;
  cursor: pointer;
}

#events
{
  font-family: Helvetica, Arial, sans-serif;
  max-width: 800px;
  margin: 0 auto;
}
</style>