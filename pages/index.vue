<template>
  <div class="container">

    <b-modal title="View Member" id="memberViewModal" size="lg" ok-title="Save Changes" @ok="onSave" >
      <MemberView :member="selectedMember" />
    </b-modal>

    <h1>List of Members</h1>
    <div class="row">
      <div class="col-md-7">
        <table class="table table-striped table-bordered">
          <thead>
            <tr>
              <th>Last Name</th>
              <th>First Name</th>
              <th>Points</th>
              <th>&nbsp;</th>
            </tr>
          </thead>
          <tbody>
            <tr v-for="member in members" :key="member.id">
              <td>{{member.lname}}</td>
              <td>{{member.fname}}</td>
              <td class="text-right">{{member.points}}</td>
              <td>
                <button class="btn btn-secondary btn-sm" @click="onViewMember(member)">
                  Open
                </button>
              </td>
            </tr>
          </tbody>
        </table>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      members: [],
      selectedMember: {}
    }
  },
  methods: {
    async getMembers() {
      await this.$axios.get('http://localhost:8000/api/members')
      .then(res=>{
        if(res.status==200) {
          this.members = res.data.members
        }
      })
    },
    onViewMember(member) {
      this.$bvModal.show('memberViewModal')
      this.selectedMember = member
    },
    async onSave() {
      await this.$axios.put('http://localhost:8000/api/members/'+ this.selectedMember.id, this.selectedMember)
      .then(res=>{
        if(res.status==202) {
          alert(res.data.message)
        }
      })
    }
  },
  created() {
    this.getMembers()
  }
}
</script>

<style>

</style>
