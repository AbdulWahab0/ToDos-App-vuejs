<template>
  <transition name="modal">
    <div class="amodal" v-show="value">
      <transition name="zoom">
        <div class="amodal__container" v-if="value" :style="{ width: width }">
          <div class="amodal__header">
            <div class="aspace-between">
              <div class="amodal__title">{{ title }}</div>
              <div @click="$emit('input', false)" class="amodal__close">
                &times;
              </div>
            </div>
          </div>

          <div class="amodal__body">
            <slot></slot>
          </div>

          <div class="amodal__footer"></div>
        </div>
      </transition>
    </div>
  </transition>
</template>

<script>
export default {
  data() {
    return {};
  },
  props: {
    value: {
      type: Boolean,
      default: false
    },
    width: {
      type: String,
      default: "960px"
    },

    title: {
      type: String,
      default: "Modal title"
    }
  },

  watch: {
    value: function(newValue, oldValue) {
      // this.$eb.$emit("toggleOverlay", this.value);
    }
  }
};
</script>

<style>
.aspace-between {
  display: flex;
  justify-content: space-between;
}

.amodal {
  position: fixed;
  z-index: 999;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  display: flex;
  justify-content: center;
  align-items: center;
  background: rgba(0, 0, 0, 0.6);
}

.amodal__container {
  box-shadow: 0 0 15px 10px #5656566b;
  min-height: 22px;
  background: #fff;
  border-radius: 3px;
  max-width: 95%;
}

.amodal__header {
  background: #ececec;
  border-bottom: 1px solid #e6e6e6;
  border-radius: 3px 3px 0 0;
}

.amodal__title {
  padding: 11px 22px;
}

.amodal__close {
  cursor: pointer;
  padding: 0px 15px;
  font-size: 28px;
}

.amodal__close:hover {
  color: red;
}

.amodal__body {
  padding: 44px 33px;
  max-height: 88vh;
  overflow-y: auto;
}

.zoom-enter-active,
.zoom-leave-active {
  transition: all 0.25s;
  /* transform: scale(1); */
}
.zoom-enter,
.zoom-leave-to {
  transform: scale(0.5);
  opacity: 0;
}

.modal-enter-active,
.modal-leave-active {
  transition: all 0.25s;
}
.modal-enter,
.modal-leave-to {
  background-color: none;
  opacity: 0;
}
</style>
