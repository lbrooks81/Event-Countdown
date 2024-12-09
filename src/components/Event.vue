<template>
  <!-- only shows future dates-->
  <article v-show="Math.sign(daysLeft) !== -1"
    :style="{background: event.background}">
    <div class="data">
      <h3 class="name">{{ event.name }}</h3>
      <p class="details">{{ event.details }}</p>
    </div>
    <div class="countdown">
      <div class="remove-btn-wrapper">
        <button class="remove-btn">&#10060;</button>
      </div>
      <p v-if="daysLeft === 0" style="text-align: center">
        Today
      </p>
      <p v-else style="text-align: center">
        {{ Math.abs(daysLeft) }}
        <br />
        <small>
          {{ daysLeft === 1 ? "day" : "days" }}
           {{ Math.sign(daysLeft) === 1 ? "left" : "ago"}}
        </small>
      </p>
    </div>
  </article>
</template>

<script>
//* Exporting allows it to be used in other components
export default {
  //* This name does not define the tag name for using the components, it's mainly for debugging
  name: "Event",
  props: ["event", "daysLeft"]
}
</script>

<style scoped>
article
{
  background: lightslategray;
  display: flex;
  align-items: center;
  border-radius: 1rem;
  margin: 1rem 0;
  padding: 0.2rem 1rem;
  color: whitesmoke;
  font-weight: 300;
}

.data
{
  flex: 3;
}

.countdown
{
  flex: 1;
  text-align: center;
  font-size: 1.6rem;
  border-left: 1px solid;
}

.name
{
  font-size: 1.8rem;
}

.details
{
  font-size: 1.6rem;
}

/* remove event button: */
.remove-btn
{
  background: transparent;
  border: none;
  font-size: 14px;
  cursor: pointer;
}

.remove-btn-wrapper
{
  text-align: right;
}
</style>