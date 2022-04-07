<template>
  <label>
    {{ labelName }}
    <input
      :value="value"
      :type="type"
      :name="type"
      @input="$emit('input', $event.target.value)"
    />
  </label>
</template>

<script>
export default {
  name: "LabelAndInput",
  props: {
    value: String,
    labelName: String,
    type: String,
  },
};
</script>
