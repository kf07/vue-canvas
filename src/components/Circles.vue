<template>
  <div>
    <v-stage :config="configKonva">
      <v-layer>
        <v-circle :config="configCircle"></v-circle>
      </v-layer>
    </v-stage>
    <p>{{ colorResult }}</p>
    <p>{{ colorHex }}</p>
  </div>
</template>

<script>
import tinycolor from "tinycolor2";

export default {
  name: "Circles",
  data() {
    return {
      configKonva: {
        width: 200,
        height: 200
      },
      configCircle: {
        x: 100,
        y: 100,
        radius: 70,
        fill: ""
      },
      colorsRgb: {
        r: 255,
        g: 0,
        b: 0
      },
      colorsHsl: {
        h: 0,
        s: 100,
        l: 50
      },
      colorHex: ""
    };
  },
  computed: {
    colorResult: function() {
      const colorList = this.colorsHsl;
      const color2 = tinycolor(
        `hsl(${colorList.h},${colorList.s},${colorList.l}`
      );
      this.colorHex = color2.toHexString();
      this.colorsRgb.r = Math.floor(color2._r);
      this.colorsRgb.g = Math.floor(color2._g);
      this.colorsRgb.b = Math.floor(color2._b);
      this.configCircle.fill = `rgb(${this.colorsRgb.r},${this.colorsRgb.g},${
        this.colorsRgb.b
      })`;
      return `rgb(${this.colorsRgb.r},${this.colorsRgb.g},${
        this.colorsRgb.b
      })、hsl(${this.colorsHsl.h},${this.colorsHsl.s},${this.colorsHsl.l})`;
    }
  },
  mounted() {
    setInterval(() => {
      if (this.colorsHsl.h <= 360) {
        this.colorsHsl.h = this.colorsHsl.h + 1;
      } else {
        this.colorsHsl.h = 0;
      }
    }, 100);
  }
};
</script>

<style scoped></style>
