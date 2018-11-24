<template>
<div class="container">
    <h1 class="text-white text-uppercase">Vapelator</h1>
    <h4>Kalkulaator e-sigareti vedeliku tegemiseks</h4>
    <form class="mt-4 col-md-6 mx-auto">
    <div class="form-group">
        <div class="input-group">
            <div class="input-group-prepend">
                <span class="input-group-text" id="inputGroup-sizing-sm">Kogus:</span>
                <b-btn class="btn-dark" v-b-popover.hover="'Sisesta siia kogus palju sa tahad vedelikku valmistada.'">?</b-btn>

            </div>
            <input name="batch" type="number" class="form-control" min="0" v-model="formula.batch" v-bind="calculate()">
            <div class="input-group-append ">
                <span class="input-group-text">ml</span>
            </div>
        </div>
        
    </div>
    <div class="form-group">
        <div class="input-group">
            <div class="input-group-prepend">
                <span class="input-group-text" id="inputGroup-sizing-sm">Nikotiini kangus:</span>
                <b-btn class="btn-dark" v-b-popover.hover="'Sisesta siia kui kange on nikotiin millest vedelikku valmistad.'">?</b-btn>
            </div>
            <input name="strength" type="number" class="form-control" min="0"  v-model="formula.strength" v-bind="calculate()" >
            <div class="input-group-append">
                <span class="input-group-text">mg/ml</span>
            </div>
        </div>
        
    </div>
    <div class="form-group">
        <div class="input-group">
            <div class="input-group-prepend">
                <span class="input-group-text" id="inputGroup-sizing-sm">Tahetud koguse kangus:</span>
                <b-btn class="btn-dark" v-b-popover.hover="'Sisesta siia kui kange sa tahad, et vedelik lõpuks oleks.'">?</b-btn>
                </div>
            <input name="target" type="number" class="form-control shadow" min="0"  v-model="formula.target" v-bind="calculate()" >
            <div class="input-group-append">
                <span class="input-group-text">mg/ml</span>
            </div>
        </div>
        </div>
        <div class="form-group">
            <div class="input-group">
                <div class="input-group-prepend">
                    <span class="input-group-text" id="inputGroup-sizing-sm">Maitse protsent:</span>
                    <b-btn class="btn-dark" v-b-popover.hover="'Sisesta siia kui suur on osakaal maitsel lõppvedelikus (tavaliselt kuskil vahemikus 5-15%).'">?</b-btn>
                </div>
                <input name="flavour" type="number" class="form-control" min="0" v-model="formula.flavour" v-bind="calculate()" >
                <div class="input-group-append">
                    <span class="input-group-text">%</span>
                </div>
            </div>
        </div>
    </form>
    <div class="result mt-4">
        <h4>{{formula.batch}} ml koguse valmistamiseks läheb vaja {{formula.nicotine}} ml nikotiini, maitset läheb {{formula.finalFlavour}} ml ja baasvedelikku läheb {{formula.result}} ml.</h4>
    </div>
</div>
</template>
<script>
export default {
  data() {
    return {
      formula: {batch: 10, strength: 20, target: 6, flavour: 10},
      init:''
    };
  },

  methods: {
    calculate() {
      this.init = true;
      this.formula.nicotine = (
        (this.formula.batch * this.formula.target) /
        this.formula.strength
      ).toFixed(2);
      this.formula.finalFlavour =
        (this.formula.flavour * this.formula.batch) / 100;
      this.formula.result = (
        this.formula.batch -
        this.formula.nicotine -
        this.formula.finalFlavour
      ).toFixed(2);

      if (this.formula.target === 0) {
        this.formula.nicotine = 0;
        this.formula.result = (
          this.formula.batch - this.formula.finalFlavour
        ).toFixed(2);
      }
      if (this.formula.strength === 0) {
        this.formula.nicotine = 0;
        this.formula.result = (
          this.formula.batch - this.formula.finalFlavour
        ).toFixed(2);
      }
    }
  }
};
</script>
<style scoped>
    label{
        display:block;
    }
    h1{
        font-size: 4em;
        text-shadow: 4px 4px 5px rgba(0, 0, 0, 0.5);
    }
    h4{
        font-size: 1.8em;
        color: whitesmoke;
    }

    

    h1,h4{
        color: #3A0F38;
        /* text-shadow: 4px 4px 5px rgba(0, 0, 0, 0.5); */
    }

    .result{
        font-size: 1em;
        background: #3A0F38;
        border-radius: 5px;
    }
    .result h4{
        color: white;
        padding: 1em;
        font-size: 1.3em;
    }

    .shadow{
        box-shadow: 4px 4px 5px rgba(0, 0, 0, 0.5);
    }

</style>