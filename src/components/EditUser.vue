<template>
  <div class="details">
    <div class="input-group flex-nowrap">
      <span class="input-group-text" id="addon-wrapping"> name</span>
      <input
          v-model="user.name"
          type="text" class="form-control"
          placeholder="Username"
          aria-label="Username"
          aria-describedby="addon-wrapping"
          :disabled="!editability"
      >
    </div>
    <br>
    <div class="input-group flex-nowrap">
      <span class="input-group-text" id="addon-wrapping">phone</span>
      <input
          v-model="user.phone"
          type="text"
          class="form-control"
          placeholder="Username"
          aria-label="Username"
          aria-describedby="addon-wrapping"
          :disabled="!editability"
      >
    </div>
    <br>
    <div class="buttons">
      <button class="btn" v-show="!editability" @click="editInfo">Edit</button>
      <button class="btn" v-show="editability" @click="cancelChanges">Cancel</button>
      <button class="btn" @click="hideDetails">Done</button>
    </div>
  </div>
</template>

<script>
export default {
  name: "EditUser",
  props: ['user'],
  data() {
    return {
      editability: false,
      originalInfo: {}
    };
  },
  methods: {
    hideDetails() {
      this.$emit("hideDetails", this.user.id);
      this.editability = false;

      if (this.isChanged(this.originalInfo, this.user)) {
        const unparsed = JSON.parse(localStorage.getItem("contacts"));
        unparsed[this.user.id] = this.user;
        const updated = JSON.stringify(unparsed);
        localStorage.setItem("users", updated);
      }
    },
    editInfo() {
      Object.assign(this.originalInfo, this.user);
      this.editability = true;
    },
    cancelChanges() {
      Object.assign(this.user, this.originalInfo);
      this.editability = false;
      this.hideDetails();
    },
    isChanged(obj1, obj2) {
      return JSON.stringify(obj1) !== JSON.stringify(obj2);
    }
  }
}
</script>

<style scoped>

</style>