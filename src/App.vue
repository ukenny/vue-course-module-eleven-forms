<template>
  <b-container>
    <b-form>
      <b-form-row>
        <h1>File a Complaint</h1>
        <hr />
      </b-form-row>

      <b-form-group
        id="fieldset-horizontal-1"
        label-cols-sm="2"
        description="Please provide your email address."
        label="Enter your email:"
        label-for="email"
      >
        <b-form-input
          v-model="userData.email"
          type="email"
          id="emal"
        ></b-form-input>
      </b-form-group>
      <b-form-group
        id="fieldset-horizontal-2"
        label-cols-sm="2"
        description="Please provide your password."
        label="Enter your password:"
        label-for="password"
      >
        <b-form-input
          v-model.lazy="userData.password"
          type="password"
          id="password"
        ></b-form-input>
      </b-form-group>
      <b-form-group
        id="fieldset-horizontal-3"
        label-cols-sm="2"
        description="Please provide your age."
        label="Enter your age:"
        label-for="age"
      >
        <b-form-input
          min="18"
          max="120"
          v-model.number="userData.age"
          type="number"
          id="age"
        ></b-form-input>
      </b-form-group>
      <b-form-group
        id="fieldset-horizontal-4"
        label-cols-sm="2"
        description="Please provide a escription of the problem."
        label="Message:"
        label-for="message"
      >
        <b-textarea
          maxlength="200"
          rows="2"
          max-rows="3"
          no-resize
          :placeholder="messagePlaceholder"
          id="message"
          v-model.lazy="message"
        ></b-textarea>
      </b-form-group>
      <div class="col-xs-12 col-sm-8 col-sm-offset-2 col-md-6 col-md-offset-3">
        <b-form-group>
          <b-form-checkbox
            id="sendemail"
            v-model="sendMail"
            name="SendMail"
            value="send_email"
            unchecked-value="do_not_send_email"
            >Send Mail</b-form-checkbox
          >
          <b-form-checkbox
            id="sendInfoMail"
            v-model="sendMail"
            name="SendInfoMail"
            value="send_info_mail"
            unchecked-value="do_not_send_info_mail"
            >Send Info Mail</b-form-checkbox
          >
        </b-form-group>
      </div>
      <b-form-row>
        <div
          class="col-xs-12 col-sm-8 col-sm-offset-2 col-md-6 col-md-offset-3"
        >
          <b-form-group label="Select your gender:">
            <b-form-radio-group
              id="gender-radio-selection"
              v-model="genderSelection"
              :options="options"
              name="gender-selection"
            ></b-form-radio-group>
          </b-form-group>
        </div>
        <div class="col-xs-3" style="text-align:right;">
          <b-dropdown
            id="priority"
            variant="primary"
            text="Priority Level"
            class="m-md-2"
          >
            <b-dropdown-item @click="priorityClicked($event)" active
              >Low</b-dropdown-item
            >
            <b-dropdown-item @click="priorityClicked($event)"
              >Medium</b-dropdown-item
            >
            <b-dropdown-item @click="priorityClicked($event)"
              >High</b-dropdown-item
            >
            <b-dropdown-divider></b-dropdown-divider>
            <b-dropdown-item @click="priorityClicked($event)"
              >Critical</b-dropdown-item
            >
          </b-dropdown>
        </div>
      </b-form-row>
      <app-switch v-model="dataSwitch"></app-switch>
      <div class="col-xs-12" style="text-align:center;">
        <button
          class="btn btn-success"
          @click.prevent="complaintSubmitted($event)"
        >
          Submit!
        </button>
      </div>
      <hr />
      <div
        v-if="isSubmitted"
        class="col-xs-12 col-sm-8 col-sm-offset-2 col-md-6 col-md-offset-3"
      >
        <div class="panel panel-default">
          <div class="panel-heading">
            <h4>Your Data</h4>
          </div>
          <div class="panel-body" style="align: text-align: center">
            <p>Mail: {{ userData.email }}</p>
            <p>Password: {{ userData.password }}</p>
            <p>Age: {{ userData.age }}</p>
            <p style="white-space: pre">
              Message:
              <i style="text-align: right">
                {{ message }}
              </i>
            </p>
            <p>
              <strong>Send Mail?</strong>
            </p>
            <ul>
              <li v-for="item in sendMail" v-bind:key="item">
                {{ item }}
              </li>
            </ul>
            <p>Gender: {{ genderSelection }}</p>
            <p>Priority: {{ priorityLevel }}</p>
            <p>Switched: {{ dataSwitch }}</p>
          </div>
        </div>
      </div>
    </b-form>
  </b-container>
</template>

<script>
import Switch from "./components/Switch.vue";

export default {
  name: "app",
  components: {
    "app-switch": Switch
  },
  data: function() {
    return {
      userData: {
        email: "",
        password: "",
        age: 18
      },
      message: "",
      messagePlaceholder: "My problem is that...",
      sendMail: [],
      priorityLevel: "Low",
      genderSelection: "other",
      options: [
        { text: "Male", value: "male" },
        { text: "Female", value: "female" },
        { text: "Prefer Not To Say", value: "other" }
      ],
      dataSwitch: true,
      isSubmitted: false
    };
  },
  methods: {
    priorityClicked(event) {
      this.priorityLevel = event.target.text;
    },
    complaintSubmitted() {
      this.isSubmitted = true;
    }
  }
};
</script>

<style>
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
input[type="number"] {
  -webkit-appearance: textfield;
  -moz-appearance: textfield;
  appearance: textfield;
}
input[type="number"]::-webkit-inner-spin-button,
input[type="number"]::-webkit-outer-spin-button {
  -webkit-appearance: none;
}
.panel-body {
  font-size: 1.4vw;
}
</style>
