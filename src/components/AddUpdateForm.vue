<template>
  <div class="form-wrapper">
    <form>
      <!-- $prefix means we are referring to a property of a Vue component
           In this instance, we can use it to emit one of the events specified
      -->
      <span class="close"
            @click="this.$emit('close-form')">
        &#10060;</span>
      <div>
        <label for="name">Name:</label>
        <input type="text" id="name" v-model="event.name" />
      </div>
      <div>
        <label for="details">Details:</label>
        <input type="text" id="details" v-model="event.details">
      </div>
      <div>
        <label for="date">Date:</label>
        <input type="date" id="date" v-model="event.date">
      </div>
      <div>
        <label for="background">Background:</label>
        <select id="background">
          <option value="#F34949">Red</option>
          <option value="#F07AEC">Pink</option>
          <option value="#997AF0">Purple</option>
          <option value="#7AD3F0">Blue</option>
          <option value="#68EE94">Green</option>
          <option value="#F9F970">Yellow</option>
          <option value="#FFBF00">Orange</option>
        </select>
      </div>
      <div>
        <button>Add</button>
      </div>
    </form>
  </div>
</template>

<script>
export default {
  name: "AppUpdateForm",
  //* This is where we can specify the types of custom events that we can emit from this component
  emits: ["close-form"],
  data(){
    return{
      event: {}
    }
  },
}
</script>


<style scoped>
.form-wrapper
{
  background-color: rgba(0, 0, 0, 0.7);
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  display: flex;
  /* flex allows us to center the form
   horizontally and vertically */
  justify-content: center;
  align-items: center;
}

form
{
  background: white;
  min-width: 60vw;
  min-height: 40vh;
  padding: 2rem;
  border-radius: 0.3rem;
  display: flex;
  flex-direction: column;
}

form > div
{
  display: flex;
  flex-direction: column;
  margin: 1rem 0;
  font-size: 1.6rem;
}

form input, select
{
  margin: 0.6rem 0;
  padding: 0.6rem 1rem;
  border: 1px lightgrey solid;
  border-radius: 0.3rem;
  font-size: 16px;
}

form button
{
  background: rgb(123, 194, 123);
  width: 100px;
  border: none;
  padding: 0.6rem;
  border-radius: 0.3rem;
  font-size: 16px;
}

.close
{
  align-self: flex-end;
  cursor: pointer;
}
</style>