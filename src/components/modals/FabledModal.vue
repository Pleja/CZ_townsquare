<template>
  <Modal v-if="modals.fabled && fabled.length" @close="toggleModal('fabled')">
    <h3>
      Přidat postavu Proslulého nebo Lorika do hry
    </h3>
    <ul class="tokens" v-if="tab === 'fabled'">
      <li v-for="role in fabled" :key="role.id" @click="setFabled(role)">
        <Token :role="role" />
      </li>
    </ul>
    <ul class="tokens" v-else-if="tab === 'loric'">
      <li v-for="role in loric" :key="role.id" @click="setFabled(role)">
        <Token :role="role" />
      </li>
    </ul>
    <div class="button-group">
      <span
        class="button"
        :class="{ townsfolk: tab === 'fabled' }"
        @click="tab = 'fabled'"
        >Proslulí</span
      >
      <span
        class="button"
        :class="{ townsfolk: tab === 'loric' }"
        @click="tab = 'loric'"
        >Lorici</span
      >
    </div>
  </Modal>
</template>

<script>
import { mapMutations, mapState } from "vuex";
import Modal from "./Modal";
import Token from "../Token";

export default {
  components: { Token, Modal },
  computed: {
    ...mapState(["modals", "grimoire"]),
    fabled() {
      const fabled = [];
      this.$store.state.fabled.forEach(role => {
        // don't show fabled that are already in play
        if (
          !this.$store.state.players.fabled.some(fable => fable.id === role.id)
        ) {
          fabled.push(role);
        }
      });
      return fabled;
    },
    loric() {
      const loric = [];
      this.$store.state.loric.forEach(role => {
        // don't show loric that are already in play
        if (
          !this.$store.state.players.loric.some(fable => fable.id === role.id)
        ) {
          loric.push(role);
        }
      });
      return loric;
    }
  },
  data() {
    return {
      tab: "fabled"
    };
  },
  methods: {
    setFabled(role) {
      this.$store.commit("players/setFabled", {
        fabled: role
      });
      this.$store.commit("toggleModal", "fabled");
    },
    ...mapMutations(["toggleModal"])
  }
};
</script>

<style scoped lang="scss">
@import "../../vars.scss";

ul.tokens li {
  border-radius: 50%;
  width: 8vw;
  margin: 0.5%;
  transition: transform 500ms ease;

  &.townsfolk {
    box-shadow: 0 0 10px $townsfolk, 0 0 10px #004cff;
  }
  &:hover {
    transform: scale(1.2);
    z-index: 10;
  }
}
</style>
