<template>
  <div>
    <table class="table table-striped table bordered">
      <tr>
        <th>Last Name</th>
        <td>
          <input type="text" v-model="currentMember.lname" class="form-control">
        </td>
      </tr>
      <tr>
        <th>First Name</th>
        <td>
          <input type="text" v-model="currentMember.fname"v>
        </td>
      </tr>
      <tr>
        <th>Address</th>
        <td>
          <textarea v-model="currentMember.address" rows="3" class="form-control"></textarea>
        </td>
      </tr>
      <tr>
        <th>Phone</th>
        <td>
          <input type="text" v-model="currentMember.phone" class="form-control">
        </td>
      </tr>
      <tr>
        <th>Points Earned</th>
        <td>
          <input type="text" v-model="currentMember.points" class="form-control">
        </td>
      </tr>

    </table>
  </div>
</template>


<script>
export default {
  props: {
    member: {}
  },

  computed: {
    currentMember() {
      return this.member
    }
  },
  created() {
    this.currentMember = this.member
    console.log(this.currentMember)
  }
}
</script>
