<template>
  <CalculatorComponent />
</template>

<script lang="ts">
import CalculatorComponent from "@/components/CalculatorComponent.vue";
import { defineComponent } from "vue";

export default defineComponent({
  setup() {
    return {};
  },
  components: { CalculatorComponent },
});
</script>
