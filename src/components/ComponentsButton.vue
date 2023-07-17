<template>
  <button class="button"
        @click="$emit('onClick', label)"
        :class="{ double, triple, operation }">
        {{ label }}
    </button>
</template>

<script>
export default {
  props: {
    label: {},
    operation: { type: Boolean },
    double: { type: Boolean },
    triple: { type: Boolean }
  }

}
</script>

<style>
:root {
  --bg-button: #48bc79;
  --border-button: solid 1px #888;
}

.button {
  font-size: 1.4em;
  background: var(--bg-button);
  border: none;
  border-right: var(--border-button);
  border-bottom: var(--border-button);
  outline: none;
  color: white;
}

.button:active {
  background-color: #ccc;
}

.button.double {
  grid-column: span 2;
  color: white;
}

.button.triple {
  grid-column: span 3;
  color: white;
}

.button.operation {
  background-color: #4a5568;
  color: #fff
}

.button.operation:active {
  background-color: #4a5568;
}

</style>