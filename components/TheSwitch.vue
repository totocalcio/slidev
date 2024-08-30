<script setup>
/*
 *   This content is licensed according to the W3C Software License at
 *   https://www.w3.org/Consortium/Legal/2015/copyright-software-and-document
 *
 *   File:  switch.js
 *
 *   Desc:  Switch widget that implements ARIA Authoring Practices
 */

import { ref, onMounted } from "vue";

const isChecked = ref(false);

const toggleStatus = () => {
  isChecked.value = !isChecked.value;
};

const handleKeydown = (event) => {
  if (event.key === "Enter" || event.key === " ") {
    event.preventDefault();
    toggleStatus();
  }
};

onMounted(() => {
  // DOM の読み込み完了後に必要な初期化処理を行う
  document
    .querySelector("[role=switch]")
    .setAttribute("aria-checked", isChecked.value);
});
</script>

<template>
  <div
    role="switch"
    class="mx-auto"
    :aria-checked="isChecked"
    tabindex="0"
    @click="toggleStatus"
    @keydown="handleKeydown"
  >
    <span class="label">LT発表</span>
    <span class="switch mr-2 mt-4">
      <span></span>
    </span>
    <span class="on" aria-hidden="true">おわり</span>
    <span class="off" aria-hidden="true">かいし</span>
  </div>
</template>

<style scoped>
[role="switch"] {
  padding: 4px 4px 8px 8px;
  border: 0 solid #005a9c;
  border-radius: 5px;
  width: 18em;
  user-select: none;
}

[role="switch"] .label {
  display: inline-block;
  width: 6em;
}

[role="switch"] .switch {
  position: relative;
  display: inline-block;
  top: 6px;
  border: 2px solid black;
  border-radius: 12px;
  height: 20px;
  width: 40px;
}

[role="switch"] .switch span {
  position: absolute;
  top: 2px;
  left: 2px;
  display: inline-block;
  border: 2px solid black;
  border-radius: 8px;
  height: 12px;
  width: 12px;
  background: black;
}

[role="switch"][aria-checked="true"] .switch span {
  left: 21px;
  background: green;
  border-color: green;
}

[role="switch"] .on {
  display: none;
}

[role="switch"] .off {
  display: inline;
}

[role="switch"][aria-checked="true"] .on {
  display: inline;
}

[role="switch"][aria-checked="true"] .off {
  display: none;
}

[role="switch"]:focus,
[role="switch"]:hover {
  padding: 2px 2px 6px 6px;
  border-width: 2px;
  outline: none;
  background-color: #def;
  cursor: pointer;
}

[role="switch"]:focus span.switch {
  background-color: white;
}
</style>
