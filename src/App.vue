<template>
  <div class="wrapper">
    <div class="wrapper-content">
      <section>
        <div class="container">
          <div v-if="calculated">
            <p>Зарплата на руки: {{ result }}</p>
          </div>
          <div v-else>
            <p>Зарплата не рассчитана</p>
          </div>

          <form @submit.prevent="calculate">
            <div>
              <label for="salary">Оклад</label>
              <input required type="text" name="salary" v-model="salary" />
            </div>
            <div>
              <label for="prize">Премия</label>
              <input required type="text" name="prize" v-model="prize" />
            </div>
            <div>
              <label for="districtCoefficient">Районный коэффициент</label>
              <input
                type="text"
                name="districtCoefficient"
                v-model="districtCoefficient"
              />
            </div>
            <div>
              <label for="workingDays">Количество рабочих дней в месяце </label>
              <input
                required
                type="text"
                name="workingDays"
                v-model="workingDays"
              />
            </div>
            <div>
              <label for="workedDays"
                >Количество отработанных дней в месяце
              </label>
              <input
                required
                type="text"
                name="workedDays"
                v-model="workedDays"
              />
            </div>
            <div>
              <button @click="calculate">Расчитать зарплату</button>
            </div>
          </form>
        </div>
      </section>
    </div>
  </div>
</template>

<script>
export default {
  name: "App",
  data() {
    return {
      salary: null,
      prize: null,
      districtCoefficient: null,
      workingDays: null,
      workedDays: null,
      fullSalaries: null,
      NDFL: null,
      handSalary: null,
      result: null,
      calculated: false
    }
  },
  methods: {
    calculate() {
      this.fullSalaries =
        (this.salary * this.districtCoefficient * this.workedDays) /
          this.workingDays +
        this.prize

      this.NDFL = this.fullSalaries * 0.13
      this.result = Math.floor(this.fullSalaries - this.NDFL)
      this.calculated = true
    }
  }
}
</script>

<style lang="css">
body {
  font-family: "Montserrat", sans-serif;
  background-color: #2e2e2e;
}
.wrapper {
  padding: 0 10%;
  margin-top: 30px;
}

p {
  color: #ffffff;
}

.wrapper-content {
  display: grid;
  grid-template-columns: 1fr;
  align-content: center;
  justify-items: center;
}
.container {
  display: grid;
  grid-template-columns: 1fr;
  align-content: center;
  justify-items: center;
}
label {
  display: block;
  font-size: 16px;
  margin-bottom: 10px;
  text-align: left;
  color: #ffffff;
}
input {
  width: 100%;
  border: none;
  padding: 5px 10px;
  margin-bottom: 20px;
  max-width: 600px;
  border-radius: 20px;
}
form {
  padding: 30px;
  background-color: #040113;
  border-radius: 20px;
}

button {
  border: none;
  display: block;
  padding: 0.8em 2em;
  line-height: 1;
  text-transform: uppercase;
  cursor: pointer;
  border-radius: 20px;
  background-color: #ffffff;
}
</style>
