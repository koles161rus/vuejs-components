<template>
  <div class="main">
    <select v-model="selectValue" class="main__select">
      <option
        v-for="(option, index) in options"
        :key="index"
        :value="option.value"
      >
        {{ option.name }}
      </option>
    </select>
    <div>
      <ValidateComponent :componentId="1" :selectedOption="selectValue">
        <SomeComponent>
          <div>
            <ValidateComponent :componentId="2" :selectedOption="selectValue" />
          </div>
        </SomeComponent>
        <SomeComponent>
          <ValidateComponent :componentId="3" :selectedOption="selectValue">
            <ValidateComponent :componentId="4" :selectedOption="selectValue" />
          </ValidateComponent>
        </SomeComponent>
        <ValidateComponent :componentId="5" :selectedOption="selectValue" />
      </ValidateComponent>
    </div>
  </div>
</template>

<script>
import ValidateComponent from "./ValidateComponent";
import SomeComponent from "./SomeComponent";

export default {
  name: "MainComponent",
  components: {
    ValidateComponent,
    SomeComponent,
  },
  data() {
    return {
      selectValue: "all",
      options: [
        {
          name: "Вызывать проверку всех вложенных компонентов",
          value: "all",
        },
        {
          name: "Вызывать проверку только первых вложенных компонентов",
          value: "first",
        },
      ],
    };
  },
};
</script>

<style scoped lang="scss">
.main {
  display: block;
  margin: auto;
  width: 700px;

  &__select {
    font-size: 20px;
    border: none;
    outline: none;
    cursor: pointer;
    margin: auto;
  }
}
</style>
