<template>
  <v-card elevation="2" class="mt-4 " width="230">
    <v-img :src="currentImg" height="150" contain>
    </v-img>
    <v-divider class="mx-1"></v-divider>
    <v-card-title> {{ name }} </v-card-title>
    <v-card-text class="type">
      <p :class="type">
        {{ pokemon.type }}
      </p>
    </v-card-text>
  </v-card>
</template>

<script>
import axios from "axios";

export default {
  name: "HelloWorld",

  created: function () {
    axios.get(this.url).then((res) => {
      (this.pokemon.type = res.data.types[0].type.name),
        (this.pokemon.front = res.data.sprites.front_default);
      this.type = this.pokemon.type;
      this.pokemon.back = res.data.sprites.back_default;
      this.currentImg = this.pokemon.front;
    });
  },

  props: {
    num: String,
    name: String,
    url: String,
  },

  data() {
    return {
      isFront: true,
      currentImg: "",
      type: "",
      pokemon: {
        type: "",
        front: "",
        back: "",
      },
    };
  },

  methods: {},
};
</script>

<style scoped>
.grass {
  color: #28a745;
}
.fire {
  color: darkorange;
}

.water {
  color: #007bff;
}

.electric {
  color: #ffc107;
}

.ice {
  color: #00c1cf;
}

.poison {
  color: purple;
}

</style>