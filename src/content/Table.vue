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
                <td v-for="item in numberOfPallets" :key=item.id>
                    <input type="text" :value="item">
                </td>
                <td>total <span>{{ totalPallets() }}</span></td>
            </tr>
            <tr>
                <td>Dimensions,cm</td>
                <td><input type="text"></td>
                <td><input type="text"></td>
                <td><input type="text"></td>
                <td><input type="text"></td>
                <td>total <span></span></td>
            </tr>
            <tr>
                <td>Levels of stackability</td>
                <td><input type="text"></td>
                <td><input type="text"></td>
                <td><input type="text"></td>
                <td><input type="text"></td>
            </tr>
            <tr>
                <td>LDM</td>
                <td><input type="text"></td>
                <td><input type="text"></td>
                <td><input type="text"></td>
                <td><input type="text"></td>
                <td>total <span></span></td>
            </tr>
            <tr>
                <td>Weight,kg</td>
                <td><input type="text"></td>
                <td><input type="text"></td>
                <td><input type="text"></td>
                <td><input type="text"></td>
                <td>total <span></span></td>
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
                <td><input type="text"></td>
                <td><input type="text"></td>
                <td><input type="text"></td>
                <td><input type="text"></td>
                <td>total <span></span></td>
            </tr>
            <tr>
                <td>Additional costs</td>
                <td><input type="text"></td>
                <td><input type="text"></td>
                <td><input type="text"></td>
                <td><input type="text"></td>
                <td>total <span></span></td>
            </tr>
            <tr>
                <td>Income,EUR</td>
                <td><input type="text"></td>
                <td><input type="text"></td>
                <td><input type="text"></td>
                <td><input type="text"></td>
                <td>total <span></span></td>
            </tr>
        </table>   
    </div>
</template>

<script>
export default {
    data: function(){
        return {
            numberOfPallets: [5,5,0,0],
            totalPallets: 0
        }
    },
    computed: {
        totalPallets(){
            return this.numberOfPallets.forEach((item)=>{
                this.totalPallets += item;
            })
        }
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
            height: 50px;

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
    }
</style>
