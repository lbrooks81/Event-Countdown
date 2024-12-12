<!-- Works like the template property, it's where the HTML will go-->
<template>
  <button @click="darkModeSet = !darkModeSet">
    Toggle Dark Mode
  </button>

  <div id="events">
    <teleport to="#modal">
      <!--
           v-if is like display: none, v-show is like visibility: hidden.
           v-if doesn't reserve room on the DOM for the element, while v-show does
           when v-if is false, it is unmounted from the application
       -->
      <AddUpdateForm v-if="showForm" @close-form="showForm = !showForm"/>
    </teleport>

    <div class="options">
      <button @click="showPastEvents = !showPastEvents">
        Show Past Events
      </button>
      <button class="add-new" @click="showForm = !showForm">
        &#43;
      </button>
    </div>

    <ul>
      <li v-for="event in orderEvents" :key="event.id">
        <Event
            :event="event"
            :daysLeft="daysLeft(event)"
            :showPastEvents="showPastEvents"
        />
      </li>
    </ul>
  </div>
</template>

<!-- Data, methods, events go here -->
<script>

import {defineComponent} from "vue";
import Event from "@/components/Event.vue";
import AddUpdateForm from "@/components/AddUpdateForm.vue";

export default defineComponent({
  components: {AddUpdateForm, Event},
  data(){
    return{
      events: eventData,
      darkModeSet: false,
      showPastEvents: false,
      showForm: false
    }
  },
  methods:{
    daysLeft(event){
      const eventDate = Date.parse(event.date);

      //* This ensures that if the event was set to today, any second after midnight won't be counted as yesterday
      const today = new Date();
      today.setHours(0, 0, 0, 0);
      const millisecsUntilEvent = eventDate - today;

      const daysRemaining = millisecsUntilEvent / (1000 * 60 * 60 * 24);
      return Math.ceil((daysRemaining));
    }
  },
  //* Fires when changes on properties with the same name are made
  //* Watchers won't fire by default on changes for values in reference types
  watch:{
    //* First param always has the new value, second param always has the old value
    darkModeSet(newVal, oldVal) {
      console.log(newVal, oldVal);
    }
  },
  computed:{
    orderEvents(){
      const eventsToSort = this.events;
      //* We are passing in a comparison function of two dates
      //* This returns a negative number if the first date is earlier, 0 if they're the same, and positive if it's later
      return eventsToSort.sort((a, b) => Date.parse(a.date) - Date.parse(b.date));
    }
  }
});

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