<template>
  <div>
<!--    <page-header/>-->
    <p> Modal dialog with activator</p>
    <b-modal close-btn size="xs" title="My title" @click:outside="showModal = false">
      <template slot="title" slot-scope="scope">{{scope.title}} {{scope.visible}}</template>
      <template #footer="scope">
        <button class="btn btn-primary" @click="scope.close">Close</button>
      </template>
      Modal with activator
      <template #activator="{on}">
        <button class="btn btn-primary" @click="on">Open</button>
      </template>
    </b-modal>
    <hr>


    <p> Modal dialog with model</p>
    <b-modal v-model="showModal" close-btn size="xs" title="My title" @click:outside="showModal = false">
      Modal with model
    </b-modal>

    <button type="button" class="btn btn-primary" @click="showModal = !showModal">
      Launch demo modal
    </button>

    <div>
      <b-alert
          :type="alertConfig.type"
          :duration="alertConfig.duration"
          :visible="showAlert"
          :can-close="alertConfig.canHideNotification"
          @close="changeAlertVisibility(false)"
          @beforeClose="beforeAlertClose"
      >
        <h1>SOM ALERT TExt</h1>
      </b-alert>
      <button @click="showInfoAlert">show info</button>
      <button @click="showSuccessAlert">show success</button>
      <button @click="showWarningAlert">show warning</button>
    </div>

  </div>
</template>

<script>
  import BModal from "../../components/bootstrap/BModal";
  import BAlert
  ,{ALERT_TYPE}
    from "../../components/bootstrap/BAlert";

  export default {
    name: "Home",
    components: {
      // PageHeader,
      BModal,
      BAlert
    },
    data() {
      return {
        showModal: false,
        showAlert: false,
        alertConfig: {
          type:
          ALERT_TYPE.SUCCESS,
          duration: 1000,
          canHideNotification: true
        }
      }
    },

    methods: {
      changeAlertVisibility(visible) {
        this.showAlert = !!visible
      },
      changeAlertType(type){
        this.alertConfig.type = type
      },
      beforeAlertClose() {
        alert("Next act: b-alert will closed")
      },
      showInfoAlert() {
       this.changeAlertType(ALERT_TYPE.INFO)
       this.showAlert = true
      },
      showSuccessAlert() {
        this.changeAlertType(ALERT_TYPE.SUCCESS)
        this.showAlert = true
      },
      showWarningAlert() {
        this.changeAlertType(ALERT_TYPE.WARNING)
        this.showAlert = true
      }
    }
  }
</script>

