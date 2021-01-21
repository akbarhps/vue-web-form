<template>
  <form @submit.prevent="onFormSubmitted">
    <label>Email:</label>
    <input v-model="email" type="email" required />

    <label>Password:</label>
    <input v-model="password" type="password" required />
    <div class="error" v-if="passwordError">{{ passwordError }}</div>

    <label>Role: </label>
    <select v-model="role">
      <option value="developer">Web Developer</option>
      <option value="designer">Web Designer</option>
    </select>

    <label>Skills: </label>
    <input
      type="text"
      v-model="tempSkill"
      @keyup="addSkills"
      placeholder="Type skill and enter to add more."
    />
    <div class="skills">
      <div
        class="skill"
        v-for="skill in skills"
        :key="skill"
        @click="deleteSkill(skill)"
      >
        {{ skill }}
      </div>
    </div>

    <div class="terms">
      <input v-model="terms" type="checkbox" required />
      <label>Accept terms and conditions</label>
    </div>

    <div class="submit">
      <button>Create Account</button>
    </div>
  </form>
</template>

<script>
export default {
  data() {
    return {
      email: "",
      password: "",
      role: "developer",
      terms: false,
      tempSkill: "",
      skills: [],
      passwordError: "",
    };
  },
  methods: {
    addSkills(e) {
      if (e.key == "Enter" && this.tempSkill) {
        if (!this.skills.includes(this.tempSkill)) {
          this.skills.push(this.tempSkill);
        }
        this.tempSkill = "";
      }
    },
    deleteSkill(selectedSkill) {
      const skillIndex = this.skills.indexOf(selectedSkill);
      this.skills.splice(skillIndex, 1);
    },
    onFormSubmitted() {
      this.passwordError =
        this.password.length < 5
          ? "Password must be at least 5 characters long"
          : "";
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
  color: #aaaaaa;
  display: inline-block;
  margin: 25px 0 15px;
  font-size: 0.6em;
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
  border-bottom: 1px solid #dddddd;
  color: #555555;
}
input[type="checkbox"] {
  display: inline-block;
  width: 16px;
  margin: 0 10px 0 0;
  position: relative;
  top: 2px;
}
.skill {
  margin-top: 20px;
  margin-right: 8px;
  display: inline-block;
  padding: 6px 12px;
  background: #eeeeee;
  border-radius: 20px;
  font-size: 12px;
  letter-spacing: 1px;
  font-weight: bold;
  color: #777777;
  cursor: pointer;
}
.submit {
  text-align: center;
}
button {
  background: #0b6dff;
  border: 0;
  padding: 10px 20px;
  margin-top: 20px;
  color: white;
  border-radius: 20px;
  cursor: pointer;
}
.error {
  margin-top: 10px;
  color: #ff0062;
  font-size: 0.8em;
  font-weight: bold;
}
</style>