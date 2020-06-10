<template>
  <div class="ruler-container">

    <ul class="notes">
      <div
        @mousedown="startDrag($event)"
        @mousemove="doDrag($event)"
        @mouseup="stopDrag($event)"
        class="ruler"
      >
        <span v-for="n in 12" :key="n">
          <div v-if="scale[n - 1] == 0" class="filled"
            :style="{'margin-left': (n - 1)*5 +'em'}">
          </div>
          <div v-if="scale[n - 1] != 0" class="empty"
            :style="{'margin-left': (n - 1)*5 +'em'}">
          </div>
        </span>
      </div>
      <li v-for="n in notes" :key="n.order">
        <div class=n-container>
          <span class="n-names">
            {{ n.names[0] }}
          </span>
          <span v-if="n.names[1]" class="n-names">
            {{ n.names[1] }}
          </span>
        </div>
      </li>
    </ul>
    <button @click="setMajor">
      Major
    </button>
    <button @click="setMinor">
      Minor
    </button>
  </div>
</template>

<script>
import { NOTES } from '../js/constants/notes';
import {
  MAJOR,
  MINOR
} from '../js/constants/scales';
export default {
  name: 'Ruler',
  data() {
    return {
      notes: [
        ...NOTES,
        ...NOTES,
        ...NOTES
      ],
      scales: {
        major: MAJOR
      },
      scale: MAJOR,
      ruler: {
        isDragging: false,
        offset: 0
      }
    }
  },
  methods: {
    startDrag(e) {
      let ruler = document.getElementsByClassName("ruler")[0];
      this.ruler.offset = ruler.offsetLeft - e.clientX;
      this.ruler.isDragging = true;
    },
    stopDrag() {
      this.ruler.isDragging = false;
    },
    doDrag(e) {
      if(this.ruler.isDragging){
        let ruler = document.getElementsByClassName("ruler")[0];
        ruler.style.left = ((this.ruler.offset + e.clientX)) + 'px';
      }
    },
    setMajor() {
      this.scale = MAJOR;
    },
    setMinor() {
      this.scale = MINOR;
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
