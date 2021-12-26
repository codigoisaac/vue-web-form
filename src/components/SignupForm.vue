<template>
  <form>
    <label>Email</label>
    <input type="email" v-model="email" required />

    <label>Password</label>
    <input type="password" v-model="password" required />

    <label>Role:</label>
    <select v-model="role">
      <option value="developer">Web Developer</option>
      <option value="designer">Web Designer</option>
    </select>

    <label>Skills</label> <br />
    <div class="skills">
      <span
        v-for="skill in skills"
        :key="skill"
        class="pill"
        @click="deleteSkill(skill)"
        >{{ skill }}</span
      >
    </div>
    <input
      type="text"
      v-model="tempSkill"
      @keyup="addSkill"
      placeholder="Add Skill (Enter or Comma to add)"
    />

    <div class="terms">
      <input type="checkbox" v-model="terms" required />
      <label>Accept terms and conditions</label>
    </div>
  </form>

  <p>Email: {{ email }}</p>
  <p>Password: {{ password }}</p>
  <p>Role: {{ role }}</p>
  <p>Terms accepted: {{ terms }}</p>
</template>

<script>
export default {
  data() {
    return {
      email: "",
      password: "",
      role: "",
      terms: false,
      tempSkill: "",
      skills: [],
    };
  },
  methods: {
    addSkill(e) {
      if ((e.key === "," || e.key === "Enter") && this.tempSkill) {
        const val =
          e.key === "," ? this.tempSkill.slice(0, -1) : this.tempSkill;

        if (!this.skills.includes(val) && val) {
          this.skills.push(val);
        }
        this.tempSkill = "";
      }
    },
    deleteSkill(skill) {
      this.skills.splice(this.skills.indexOf(skill), 1);
    },
  },
};
</script>

<style>
form {
  max-width: 420px;
  margin: 30px auto;
  background: white;
  text-align: left;
  padding: 40px;
  border-radius: 10px;
}
label {
  color: #aaa;
  display: inline-block;
  margin: 25px 0 15px;
  font-size: 0.6rem;
  text-transform: uppercase;
  letter-spacing: 1px;
  font-weight: bold;
}
input,
select {
  display: block;
  padding: 10px 6px;
  width: 100%;
  box-sizing: border-box;
  border: none;
  border-bottom: 1px solid #ddd;
  color: #555;
}
input[type="checkbox"] {
  display: inline-block;
  width: 16px;
  margin: 0 10px 0 0;
  position: relative;
  top: 2px;
}
.pill {
  display: inline-block;
  padding: 6px 12px;
  background: #eee;
  border-radius: 20px;
  font-size: 12px;
  letter-spacing: 1px;
  font-weight: bold;
  color: #777;
  cursor: pointer;
  margin: 1px;
}
.skills {
  margin: 0 0 10px 0;
}
</style>
