<template>
  <!-- only shows future dates-->
  <article v-show="Math.sign(daysLeft) !== -1 || showPastEvents"
    :style="{
    background: event.background,
    color: changeContrast ? '#454544' : 'whitesmoke'
  }">
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
          {{ daysLeftAsString }}
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
  props: ["event", "daysLeft", "showPastEvents"],
  //* Computed properties are automatically called when reactive data is updated
  computed: {
    daysLeftAsString() {
        const dayText = this.daysLeft === 1 ? "day" : "days";
        const leftOrAgo = Math.sign(this.daysLeft) === 1 ? "left" : "ago";
        return `${dayText} ${leftOrAgo}`;
    },
    //// Returns a bool representing whether the event has a low-contrast background
    changeContrast() {
      //* Hexcode without #
      const c = this.event.background.substring(1);
      //* parseInt in base 16
      const rgb = parseInt(c, 16);

      //* >> bitshifts the 1's and 0's 16 positions to the right
      //* & 0xff is an and-ing mask that states that we only want the first byte after the bitshift
      //* 0x is the prefix stating it is in base 16, ff represents 255
      const r = (rgb >> 16) & 0xff;
      const g = (rgb >> 8) & 0xff;
      const b = (rgb >> 0) & 0xff;

      //* ITU-R BT.709 Standard to determine how bright something is
      //* 0 to 255, 0 being darkest and 255 being brightest
      const luma = 0.2126 * r + 0.7152 * g + 0.0722 * b;

      return luma >= 128;
    }
  }

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