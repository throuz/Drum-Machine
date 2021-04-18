<template>
  <div id="drum-machine">
    <h1 id="title">Drum Machine</h1>
    <h2 id="display">{{ describeText }}</h2>
    <div id="bracket">
      <div
        v-for="(item, index) in bankData"
        :key="item.keyCode"
        class="drum-pad"
        :class="{ active: isActive[index] }"
        :id="item.id"
        @click="playSound(item.url, item.id, index)"
      >
        {{ item.keyTrigger }}
      </div>
    </div>
  </div>
</template>

<script lang="ts">
import { defineComponent, reactive, ref } from "vue";
export default defineComponent({
  name: "HelloWorld",
  setup: () => {
    const bankData = reactive([
      {
        keyCode: 81,
        keyTrigger: "Q",
        id: "Heater-1",
        url: "https://s3.amazonaws.com/freecodecamp/drums/Heater-1.mp3",
      },
      {
        keyCode: 87,
        keyTrigger: "W",
        id: "Heater-2",
        url: "https://s3.amazonaws.com/freecodecamp/drums/Heater-2.mp3",
      },
      {
        keyCode: 69,
        keyTrigger: "E",
        id: "Heater-3",
        url: "https://s3.amazonaws.com/freecodecamp/drums/Heater-3.mp3",
      },
      {
        keyCode: 65,
        keyTrigger: "A",
        id: "Heater-4",
        url: "https://s3.amazonaws.com/freecodecamp/drums/Heater-4_1.mp3",
      },
      {
        keyCode: 83,
        keyTrigger: "S",
        id: "Clap",
        url: "https://s3.amazonaws.com/freecodecamp/drums/Heater-6.mp3",
      },
      {
        keyCode: 68,
        keyTrigger: "D",
        id: "Open-HH",
        url: "https://s3.amazonaws.com/freecodecamp/drums/Dsc_Oh.mp3",
      },
      {
        keyCode: 90,
        keyTrigger: "Z",
        id: "Kick-n'-Hat",
        url: "https://s3.amazonaws.com/freecodecamp/drums/Kick_n_Hat.mp3",
      },
      {
        keyCode: 88,
        keyTrigger: "X",
        id: "Kick",
        url: "https://s3.amazonaws.com/freecodecamp/drums/RP4_KICK_1.mp3",
      },
      {
        keyCode: 67,
        keyTrigger: "C",
        id: "Closed-HH",
        url: "https://s3.amazonaws.com/freecodecamp/drums/Cev_H2.mp3",
      },
    ]);
    const describeText = ref("Drum Name");
    const isActive = reactive([
      false,
      false,
      false,
      false,
      false,
      false,
      false,
      false,
      false,
    ]);

    const playSound = (soundUrl: string, text: string, index: number) => {
      if (soundUrl) {
        isActive[index] = true;
        describeText.value = text;
        const audio = new Audio(soundUrl);
        audio.addEventListener("ended", function () {
          isActive[index] = false;
        });
        audio.play();
      }
    };

    document.addEventListener("keypress", async (e) => {
      bankData.forEach((el, index) => {
        if (e.key.toUpperCase() === el.keyTrigger) {
          playSound(el.url, el.id, index);
        }
      });
    });

    return { bankData, describeText, playSound, isActive };
  },
});
</script>

<style scoped>
#title {
  text-align: center;
}
#display {
  text-align: center;
}
#bracket {
  display: grid;
  grid-template-columns: auto auto auto;
  grid-template-rows: auto auto auto;
  grid-gap: 10px;
}
.drum-pad {
  background: #abc;
  text-align: center;
  width: 150px;
  line-height: 150px;
  cursor: pointer;
}
.active {
  background: #789;
}
</style>
