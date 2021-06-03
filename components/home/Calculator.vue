<template>
  <div class="calculator">
    <header class="text-center header">
      <h1 class="text-uppercase">
        Calculator
      </h1>
    </header>
    <div class="inputs-wrapper">
      <div class="row">
        <div class="col-md-6 col-12 mx-auto px-5">
          <div class="calculator-card card">
            <div class="card-body">
              <div class="form-wrapper text-center col-md-6 mx-auto">
                <form @submit.prevent="calculate">
                  <p>Enter the numbers</p>
                  <div class="form-group">
                    <input
                      v-model="inputs.number1"
                      type="number"
                      class="form-control"
                      :class="{ 'is-invalid':errors.number1.show}"
                      placeholder="Number 1"
                    >
                    <div class="invalid-feedback">
                      {{ errors.number1.message }}
                    </div>
                  </div>

                  <div class="form-group">
                    <input
                      v-model="inputs.number2"
                      type="number"
                      class="form-control"
                      :class="{ 'is-invalid':errors.number2.show}"
                      placeholder="Number 2"
                    >
                    <div class="invalid-feedback">
                      {{ errors.number2.message }}
                    </div>
                  </div>
                  <button :disabled="loading" type="submit" class="btn btn-block calculate-btn">
                    Calculate
                  </button>
                </form>
              </div>
              <hr class="divider" :class="{ 'animate-divider': loading}">

              <div class="col-md-6 text-center mx-auto">
                <p>Results</p>
                <input v-model="answer" type="text" disabled class="form-control result-value">
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'Calculator',
  data: () => ({
    inputs: {
      number1: '',
      number2: ''
    },
    loading: false,
    answer: '',

    errors: {
      number1: {
        message: 'Number 1 is requires a number',
        show: false
      },
      number2: {
        message: 'Number 2 is requires a number',
        show: false
      }
    }
  }),
  watch: {
    inputs: {
      deep: true,
      handler () {
        this.answer = ''
      }
    }
  },

  methods: {
    inputAreValid () {
      let isValid = true
      Object.keys(this.inputs).forEach((key) => {
        this.errors[key].show = !(this.inputs[key] && !isNaN(this.inputs[key]))
        if (this.errors[key].show) {
          isValid = false
        }
      })
      return isValid
    },
    async calculate () {
      if (this.inputAreValid()) {
        this.loading = true
        try {
          const { data: { data } } = await this.$axios.get('/calculator/add', {
            params: this.inputs
          })
          this.answer = data.sum
        } catch (e) {
          console.error(e)
        } finally {
          this.loading = false
        }
      }
    }
  }
}
</script>

<style scoped>
p{
  font-size: 16px;
  color: #A4A4A4 ;
}
.header h1{
  font-size: 18px;
  color: #ffffff;
  letter-spacing: 0.54px;
}

.header{
  background:var(--primary-color);
  padding: 20px 0;
}
.inputs-wrapper{
  margin-top: 100px;
}

.calculate-btn{
  background-color:var(--primary-color) ;
  color: #ffffff;
}

.divider{
  background-color: var(--primary-color) ;
  margin: 50px auto;
}

.animate-divider{
  animation: breath .5s infinite;
}

.result-value{
  background-color: #ffffff;
  border-color: var(--primary-color);
}

@keyframes breath {
  from {
    width: 5%;
  }

  to{
    width: 100%;
  }
}

</style>
