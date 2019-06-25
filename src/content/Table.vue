<template>
    <div>
        <table>
            <tr>
                <td>Customer</td>
                <td contenteditable="true"></td>
                <td contenteditable="true"></td>
                <td contenteditable="true"></td>
                <td contenteditable="true"></td>
            </tr>
            <tr>
                <td>Loading place</td>
                <td><input type="text"></td>
                <td><input type="text"></td>
                <td><input type="text"></td>
                <td><input type="text"></td>
            </tr>
            <tr>
                <td>Customs</td>
                <td><input type="text"></td>
                <td><input type="text"></td>
                <td><input type="text"></td>
                <td><input type="text"></td>
            </tr>
            <tr>
                <td>Unloading place</td>
                <td><input type="text"></td>
                <td><input type="text"></td>
                <td><input type="text"></td>
                <td><input type="text"></td>
            </tr>
            <tr>
                <td>Number of pallets</td>
                <td v-for="(item,index) in numberOfPallets" :key=item.id>
                    <input type="number" v-model.number="numberOfPallets[index]">
                </td>
                <td>total <span>{{ totalNumber }}</span></td>
            </tr>
            <tr>
                <td>Dimensions,cm</td>
                <td v-for="(item,index) in checkedDimensions" :key="index">
                  <input type="checkbox" id="eur1" value="0.4" v-model="item.a = true ? calcLdm : false">
                    <label for="eur1">120*80</label>
                  <input type="checkbox" id="eur2" value="0.5" v-model="item.b">
                    <label for="eur2">120*100</label>
                  <input type="checkbox" id="eur3" value="0.6" v-model="item.c">
                    <label for="eur3">120*120</label>
                </td>
            </tr>
            <tr>
                <td>Levels of stackability</td>
                <td><input type="text"></td>
                <td><input type="text"></td>
                <td><input type="text"></td>
                <td><input type="text"></td>
            </tr>
            <tr :class="{ 'bgAlert': totalLadometers > 13.6 ? true : false }">
                <td>LDM</td>
                <td v-for="(item,index) in ladometers">
                  <input type="number" v-model.number="ladometers[index] = calcLdm || ladometers[index]">
                </td>
                <td>total <span>{{ totalLadometers = totalLadometers <= 13.60 ? totalLadometers : 'more than 13.6 ldm' }}</span></td>
            </tr>
            <tr ref="w" :class="{ 'bgAlert': totalWeight > 22800 ? true : false }">
                <td>Weight,kg</td>
                <td v-for="(item,index) in weight" :key="item.id">
                  <input type="number" v-model.number="weight[index]">
                </td>
                <td>total <span>{{ totalWeight = totalWeight <= 22800 ? totalWeight : 'more than 22 800 kg' }}</span></td>
            </tr>
            <tr>
                <td>ADR</td>
                <td><input type="text"></td>
                <td><input type="text"></td>
                <td><input type="text"></td>
                <td><input type="text"></td>
            </tr>
            <tr>
                <td>Delivery to warehouse</td>
                <td><input type="text"></td>
                <td><input type="text"></td>
                <td><input type="text"></td>
                <td><input type="text"></td>
            </tr>
            <tr>
                <td>Route length,km</td>
                <td><input type="text"></td>
                <td><input type="text"></td>
                <td><input type="text"></td>
                <td><input type="text"></td>
                <td>total <span></span></td>
            </tr>
            <tr>
                <td>Client price</td>
                <td v-for="(item,index) in clientPrice">
                  <input type="number" v-model.number="clientPrice[index]">
                </td>
                <td>total <span>{{ totalClientPrice }}</span></td>
            </tr>
            <tr>
                <td>Additional costs</td>
                <td v-for="(item,index) in addCosts">
                  <input type="number" v-model.number="addCosts[index]"></td>
                <td>total <span>{{ additionalCosts }}</span></td>
            </tr>
            <tr>
                <td>Income,EUR</td>
                <td v-for="(item,index) in income">
                  <span>{{ income[index] = clientPrice[index] - addCosts[index]}}</span>
                </td>
              <td>total
                <span v-model="finalIncome">{{ finalIncome = totalClientPrice - additionalCosts }}</span>
              </td>
            </tr>
        </table>
    </div>
</template>

<script>
export default {
    data: function(){
        return {
          isActive: false,
          numberOfPallets: [0,0,0,0],
          weight: [0,0,0,0],
          clientPrice: [0,0,0,0],
          ladometers: [0,0,0,0],
          addCosts: [0,0,0,0],
          income: [0,0,0,0],
          finalIncome: 0,
          checked: false,
          checkedDimensions: [
            { a: false, b: false, c: false },
            { a: false, b: false, c: false },
            { a: false, b: false, c: false },
            { a: false, b: false, c: false }
          ]

        }
    },
    computed: {
        totalNumber(){
          return this.numberOfPallets.reduce((accumulator, current) => accumulator + +current)
        },
        totalWeight(){
          return this.weight.reduce((accumulator, current) => accumulator + +current)
          /*Vmodel должен иметь сеттер  меняй на :value (или что у тебя там) или пиши сеттер, если нужно "менять" кампутед*/
        },
        totalClientPrice() {
          return this.clientPrice.reduce((accumulator, current) => accumulator + +current)
        },
        totalLadometers(){
          return this.ladometers.reduce((accumulator, current) => accumulator + +current).toFixed(2);
        },
        additionalCosts(){
          return this.addCosts.reduce((accumulator, current) => accumulator + +current).toFixed(2);
        },
/*        calcLdm(){
          return this.checkedDimensions.map((item,index) => {
            for(let key in item) {
              if(item[key] === true && key === 'a') {
                ladometers[index] = numberOfPallets[index] * 0.4;
              }
              if(item[key] === true && key === 'b') {
                ladometers[index] = numberOfPallets[index] * 0.5;
              }
              if(item[key] === true && key === 'c') {
                ladometers[index] = numberOfPallets[index] * 0.6;
              }
            }
          })
        }*/
/*        ldmCalculation:
          // step 1. get numberOfPallets
            get: function(){
              return this.numberOfPallets.map((item) => {

              })
            }
          // step 2. check dimension of pallets and show an appropriate value
          // step 3. multiply number of pallets and an appropriate value of pallets to get ldm
        }*/

    }
}
</script>

<style lang="scss" scoped>
    table {
        width: 95%;
        outline: 1px dashed black;
        margin: 50px auto;

        tr {
            outline: 1px dotted #ccc;
            //height: 50px;

            td {
                outline: 1px solid lightseagreen;
                width: 200px;
                padding: 5px 8px;
                text-align: center;

                span {
                    width: 20px;
                    height: 10px;
                    border-bottom: 1px solid red;
                }
            }
        }
      tr:hover {
        background-color: #ccc;
      }
    }
  .bgAlert {
    background-color: indianred;
    transition: all ease 2s;
  }
</style>
