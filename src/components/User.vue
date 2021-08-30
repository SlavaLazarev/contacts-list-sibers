<template>
  <div>
  <ul class="list-group">
    <li class="list-group-item" aria-current="true">
      <img
          :src="user.avatar"
          @click="showDetails"
          style="border-radius: 50%; height: 30px; width: 30px"
          @error="replaceAvatarByDefault"
      />
      <p style="display: inline-block; padding-left: 20px">{{user.name}}</p>
      <br>
      <EditUser
          v-if="detailsVisability"
          :user="user"
          @hideDetails="hideDetails"
      />
      <div>
      </div>
    </li>
  </ul>
  </div>
</template>

<script>
import EditUser from "@/components/EditUser";
export default {
  data() {
    return {
      detailsVisability: false,
      nameVisability: true
    };
  },
  props: ["user", "users"],
  components: {
    EditUser,
  },
  methods: {
    replaceAvatarByDefault(error) {
      error.target.src = require("./../assets/img/photo6.jpeg");
    },
    showDetails() {
      this.detailsVisability = true;
      this.nameVisability = false;
    },
    hideDetails() {
      this.detailsVisability = false;
    }
  }
};
</script>

<style scoped>

</style>