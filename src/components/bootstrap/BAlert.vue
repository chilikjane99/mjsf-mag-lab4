<template>
  <div
      class="alert alert-primary"
      :class="{
        'alert-primary':type === ALERT_TYPE.INFO,
        'alert-warning':type === ALERT_TYPE.WARNING,
        'alert-success':type === ALERT_TYPE.SUCCESS,
      }"
      role="alert"
      v-if="visible"
  >
    <slot #default></slot>
    <button
        v-if="canClose"
        class="close"
        data-dismiss="alert"
        aria-label="Close"
        @click="close"
    >
      <span aria-hidden="true">&times;</span>
    </button>
  </div>
</template>
<script>
export const ALERT_TYPE = {
  INFO: "primary",
  WARNING: "warning",
  SUCCESS: "success"
}
export default {
  model: {
    prop: 'visible',
    event: 'change'
  },
  props: {
    type: {
      type: String,
      default: () => ALERT_TYPE.INFO
    },
    duration: {
      type: Number,
      default: 2000
    },
    canClose: {
      type: Boolean,
      default: false,
    },

    visible: {
      type: Boolean,
      default: false
    },
  },
  emits: [
    "beforeShow",
    "beforeClose",
  ],
  data() {
    return {
      ALERT_TYPE,
      timer: null,
    }
  },
  mounted() {
    this.initAlert()
  },
  methods: {
    initAlert() {
      if (!this.visible) {
        return;
      }

      clearTimeout(this.timer)
      this.timer = setTimeout(() => {
        this.close()
        clearTimeout(this.timer)
      }, this.duration)

      this.$emit("beforeShow")
    },
    close() {
      this.$emit("beforeClose")
      this.$emit("close")
    }
  },
  watch: {
    visible() {
      if (!this.visible) {
        return;
      }

      this.initAlert()
    },
    type() {
      this.initAlert()
    }
  }
}
</script>
