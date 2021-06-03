<template>
  <div class="calculator">
    <header class="text-center header">
      <h1 class="text-uppercase">
        Calculator
      </h1>
    </header>
    <div class="inputs-wrapper">
      <div class="row">
        <div class="col-md-4 col-12 mx-auto px-5">
          <div class="calculator-card card">
            <div class="card-body">
              <div class="form-wrapper text-center col-md-6 mx-auto">
                <form>
                  <p>Enter the numbers</p>
                  <div class="form-group">
                    <input type="number" class="form-control" placeholder="Number 1">
                  </div>

                  <div class="form-group">
                    <input type="number" class="form-control" placeholder="Number 2">
                  </div>
                  <button type="button" class="btn btn-block calculate-btn">
                    Calculate
                  </button>
                </form>
              </div>
              <hr class="divider">

              <div class="col-md-6 text-center mx-auto">
                <p>Results</p>
                <input type="text" disabled class="form-control result-value">
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
  name: 'Calculator'
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
  margin: 50px 10px;
}

.result-value{
  background-color: #ffffff;
  border-color: var(--primary-color);
}
</style>
