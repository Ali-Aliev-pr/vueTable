<template>
  <div>
    <button @click="show">Start</button>
    <div class="startBlock" :class="{show: active}">
      <h2>Press "Add Input" to write new header name</h2>
      <div class="strokeInput">
        <input class="strokes" type="number" placeholder="Enter count of strokes" v-model="strokes">
      </div>
      <hr>
      <div class="inputs" v-for="i in count" :key="i">
        <input class="inputHeader" type="text" placeholder="Enter field name">
      </div>
      <div class="addInput"><button @click="addInput">Add Input</button></div>
      <div class="finish">
        <button @click="createTable">Create Table</button>
      </div>
    </div>
    <div class="tables" v-for="item in tableHead" :key="item.id">
      <table border="1">
        <thead>
          <tr>
            <th v-for="i in item.value" :key="i">{{i}}</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="i in item.strokes" :key="i">
            <td v-for="i in item.value.length" :key="i">
              <input class="tableInput" type="text">
            </td>
          </tr>
        </tbody>
        <div class="tableButtons">
          <button @click="strokeMinus" class="strokeMinus">-</button>
          <button @click="strokePlus" class="strokePlus">+</button>
        </div>
      </table>
    </div>
    <p>{{strokes}}</p>
  </div>
</template>

<script>


export default {
  name: 'App',
  components: {
  },
  data() {
    return {
      count: 1,
      tableHead: [],
      active: true,
      strokes: 0
     }
  },
  methods: {
    addInput() {
      this.count += 1
    },
    show() {
      this.active = !this.active
      console.log(this.active)
    },
    createTable() {
      let headers = document.querySelectorAll('.inputHeader');
      let headersArray = []
      headers.forEach(item => {
        headersArray.push(item.value)
      })
      let tableElem = {
        id: this.tableHead.length+1,
        value: headersArray,
        strokes: +this.strokes
      }
      this.tableHead.push(tableElem)
      console.log(this.tableHead)
    },
    strokeMinus() {
      if (this.strokes) {
        this.strokes -= 1
      }
      console.log(this.strokes)
    },
    strokePlus() {
      this.strokes = this.strokes + 1
      console.log(this.strokes, typeof(this.strokes))
    }
  }
}
</script>

<style>
* {
  margin: 0;
  padding: 0;
  font-family: Avenir, Helvetica, Arial, sans-serif;
}

.show {
  display: none;
}

.startBlock {
  border: 1px solid #000;
  width: 600px;
  /* height: 300px; */
  padding: 30px 0 30px 0;
}

h2 {
  display: flex;
  justify-content: center;
  margin-top: 20px;
}

.inputs {
  display: flex;
  flex-direction: column;
  margin-top: 10px;
}

.inputHeader {
  width: 200px;
  margin: 0 auto;
  outline: none;
  margin-top: 5px;
}

.addInput {
  display: flex;
  justify-content: center;
  margin-top: 5px;
}

.finish {
  display: flex;
  justify-content: center;
  margin-top: 10px;
}

.strokeInput {
  display: flex;
  justify-content: center;
  margin: 10px 0;
}

.tableInput {
  outline: none;
}
</style>