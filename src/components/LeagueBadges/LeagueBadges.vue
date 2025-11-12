<script setup>
import { ref, watch, onMounted, onBeforeUnmount } from "vue";

const props = defineProps({
  url: { type: String, default: null },
});
const emit = defineEmits(["close"]);

const show = ref(false);

function open() {
  if (props.url) {
    show.value = true;
    document.body.style.overflow = "hidden";
  }
}
function close() {
  show.value = false;
  document.body.style.overflow = "";
  emit("close"); 
}

watch(
  () => props.url,
  (val) => {
    if (val) open();
    else close();
  },
  { immediate: true }
);

function onKey(e) {
  if (e.key === "Escape") close();
}
onMounted(() => window.addEventListener("keydown", onKey));
onBeforeUnmount(() => window.removeEventListener("keydown", onKey));
</script>

<template>
  <teleport to="body">
    <div
      v-if="props.url"
      class="cardBackDrop"
      :class="show ? 'fadeIn' : 'fadeOut'"
      @click.self="close"
    >
      <div
        class="cardContent"
        :class="show ? 'slideUp' : 'slideDown'"
        @click.stop
      >
        <button class="cardClose" @click="close">×</button>

        
        <img :src="props.url" alt="league badge" class="cardImage" />
      </div>
    </div>
  </teleport>
</template>

<style scoped>
.cardBackDrop {
  position: fixed;
  inset: 0;
  background: rgba(0, 0, 0, 0.6);
  display: flex;
  justify-content: center;
  align-items: center;
  backdrop-filter: blur(3px);
  z-index: 9999;
  opacity: 0;
  transition: opacity 0.3s ease;
  
}
.fadeIn { opacity: 1; }
.fadeOut { opacity: 0; }

.cardContent {
  position: relative;
  text-align: center;
  background: #181818;
  padding: 25px;
  border-radius: 12px;
  width: 520px;
  max-width: 90vw;
  max-height: 80vh;
  overflow-y: auto;
  color: #fff;
  transform: translateY(20px);
  opacity: 0;
  transition: 0.3s ease;
  
}
.slideUp { transform: translateY(0); opacity: 1; }
.slideDown { transform: translateY(20px); opacity: 0; }

.cardClose {
  position: absolute;
  top: 10px;
  right: 10px;
  background: crimson;
  border: none;
  color: white;
  font-size: 18px;
  padding: 5px 10px;
  border-radius: 6px;
  cursor: pointer;
  transition: background 0.2s ease;
}
.cardClose:hover { background: #ff2f2f; }

.cardImage {
  width: 300px;
  height: auto;
  border-radius: 10px;
  box-shadow: 0 0 20px rgba(255,255,255,0.15);
}
</style>
