<template>
  <span>
    <transition name="mu-bottom-sheet" @after-enter="show()" @after-leave="hide()">
      <div class="mu-bottom-sheet" ref="popup" v-show="open" :style="{'z-index': zIndex}">
        <slot></slot>
      </div>
    </transition>
  </span>
</template>

<script>
import Popup from '../internal/popup'
export default {
  name: 'mu-bottom-sheet',
  mixins: [Popup],
  methods: {
    overlayClick () {
      this.$emit('close', 'overlay')
    },
    escPress () {
      this.$emit('close', 'esc')
    },
    show () {
      this.$emit('show')
    },
    hide () {
      this.$emit('hide')
    }
  }
}
</script>

<style lang="less">
@import "../styles/import.less";
.mu-bottom-sheet {
  background-color: @dialogBackgroundColor;
  position: fixed;
  left: 0;
  right: 0;
  bottom: 0;
}

.mu-bottom-sheet-enter-active,
.mu-bottom-sheet-leave-active{
  transition: transform .45s @easeOutFunction;
  backface-visibility: hidden;
}

.mu-bottom-sheet-enter,
.mu-bottom-sheet-leave-active{
  transform: translate3d(0, 100%, 0);
}
</style>
