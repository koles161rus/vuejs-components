<template>
  <div class="validate-component">
    <span class="validate-component__title"
      >Проверочный компонент {{ componentId }}</span
    >
    <span v-if="parentId" class="validate-component__info"
      >Проверка вызвана из компонента {{ parentId }}</span
    >
    <button @click="validateAll()" class="validate-component__button">
      Проверить
    </button>
    <button @click="parentId = null" class="validate-component__button">
      Очистить
    </button>
    <button
      v-if="$children.length"
      @click="resetAll()"
      class="validate-component__button"
    >
      Очистить всё
    </button>
    <slot />
  </div>
</template>

<script>
export default {
  name: "ValidateComponent",
  props: {
    componentId: Number,
    selectedOption: {
      type: String,
      default: "all",
    },
  },
  data() {
    return {
      parentId: null,
    };
  },
  watch: {
    selectedOption() {
      this.resetAll();
    },
  },
  methods: {
    validateAll(componentId = this.componentId, component = this) {
      this.parentId = componentId;
      component.$children.forEach((childrenComponent) => {
        return childrenComponent.$options.name === "ValidateComponent"
          ? this.selectedOption === "all"
            ? childrenComponent.validateAll(this.componentId)
            : childrenComponent.validateFirst(componentId)
          : this.validateAll(componentId, childrenComponent);
      });
    },
    validateFirst(componentId = this.componentId) {
      this.parentId = componentId;
    },
    resetAll(component = this) {
      this.parentId = null;
      component.$children.forEach((childrenComponent) => {
        return childrenComponent.$options.name === "ValidateComponent"
          ? childrenComponent.resetAll()
          : this.resetAll(childrenComponent);
      });
    },
  },
};
</script>

<style scoped lang="scss">
.validate-component {
  display: block;
  border: 5px solid #be687b;
  margin: 10px;
  padding: 10px;

  &__title {
    display: block;
    font-size: 20px;
    color: #be687b;
    font-weight: 800;
  }

  &__info {
    display: block;
    font-size: 14px;
    font-weight: 600;
    color: #7bbe68;
  }

  &__button {
    outline: none;
    margin: 5px 2px;
    border: 2px solid #687bbe;
    color: #687bbe;
    background-color: #e0e4f2;
    cursor: pointer;
    font-weight: 600;
    font-size: 14px;
    padding: 8px;
  }
}
</style>
