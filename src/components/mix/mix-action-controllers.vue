<template>
  <div :class="`actionControllers${isActived ? '': ' is-hidden'}`">
    <div class="actionContent">
      <ul class="actionContent__list">
        <li
          class="actionContent__item"
          v-for="(action, index) of actions"
          :key="index"
          @click="action.event">
            {{action.name}}
        </li>
      </ul>
    </div>
    <add-button
      :isShown="buttons.add"
      :isActived="isActived"
      @click.native="toggleState"/>
    <delete-button
      :isShown="buttons.del"
      @click.native="fire(delAction)"
    />
  </div>
</template>

<script>
import { fire } from "~/plugins/util";
import AddButton from "~/components/single/add-button";
import DeleteButton from "~/components/single/delete-button";
import { mapState } from 'vuex';

export default {
  components: {
    AddButton,
    DeleteButton
  },
  props: {
    actions: Array,
    delAction: Function,
  },
  computed: {
    ...mapState('mix-action-controllers', [
      'isActived',
      'buttons',
    ]),
  },
  methods: {
    fire, // import from plugins/util
    toggleState() {
      this.$store.commit('mix-action-controllers/isActived');
    },
  },
};
</script>

<style lang="scss" scoped>
.actionControllers {
  position: fixed;
  bottom: 0;
  left: 0;
  z-index: 80;
  width: 100%;
  transform: translate(0, 0);
  transition: .3s;
  &.is-hidden {
    transform: translate(0, 100%);
  }
}
.actionContent {
  background-color: $app-color;

  &__list {
    list-style: none;
  }
  &__item {
    display: flex;
    justify-content: center;
    align-items: center;
    color: #fff;
    font-size: 14px;
    width: 100%;
    height: 56px;
  }

  &__item + .actionContent__item {
    border-top: 1px solid #ac3318;
  }
}

.actionControllers {
  /deep/ .addButton,
  /deep/ .deleteButton {
    position: absolute;
    top: -70px;
    transition: .3s;
  }
  &.is-hidden /deep/ .addButton,
  &.is-hidden /deep/ .deleteButton {
    top: -122px;
  }
}
</style>

