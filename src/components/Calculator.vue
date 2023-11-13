<template>
  <div>
    <div v-for="shape, index in shapes" :key="index">

      <!-- shape form wrapper -->

      <div>
        <div class="form-wrapper-header">

          <h1>Kształt {{ index + 1 }}</h1>
          <div>

            <span @click="shape.visible=!shape.visible">
              {{ shape.visible ? "-" : "+" }}
            </span>
            <button v-if="shapes.length>1" @click="removeShape(index)">Usuń</button>
          </div>
        </div>

        <!-- shape form container -->

        <div v-if="shape.visible">

          <!-- shape select -->

          <div>

            <label for="rectangle">Kwadrat lub prostokąt</label>
            <input type="radio" value="rectangle" v-model="shape.type" name="shape" id="rectangle"
              @change="handleVolume(shape)">
            <label for="triangle">Trójkąt prostokątny</label>

            <input type="radio" value="triangle" v-model="shape.type" name="shape" id="triangle"
              @change="handleVolume(shape)">
            <label for="circle">Wycinek kołowy</label>
            <input type="radio" value="circle" v-model="shape.type" name="shape" id="circle"
              @change="handleVolume(shape)">
          </div>

          <!-- rectangle / triangle form -->

          <div v-if="shape.type === 'rectangle' || shape.type === 'triangle'">

            <!-- length -->

            <label>Długość:</label>
            <div>
              <input type="number" v-model="shape.length.value" @input="handleVolume(shape)">
              <select v-model="shape.length.unit" @change="handleVolume(shape)">
                <option value="1">Metrów</option>
                <option value="1000">Kilometrów</option>
              </select>
            </div>

            <!-- height -->

            <label>Wysokość:</label>
            <div>
              <input type="number" v-model="shape.height.value" @input="handleVolume(shape)">
              <select v-model="shape.height.unit" @change="handleVolume(shape)">
                <option value="1">Metrów</option>
                <option value="1000">Kilometrów</option>
              </select>
            </div>

            <!-- width -->

            <label>Szerokość:</label>
            <div>
              <input type="number" v-model="shape.width.value" @input="handleVolume(shape)">
              <select v-model="shape.width.unit" @change="handleVolume(shape)">
                <option value="1">Metrów</option>
                <option value="1000">Kilometrów</option>
              </select>
            </div>
          </div>

          <!-- circle form -->

          <div v-else>
            <!-- radius -->
            <label>Promień:</label>
            <div>
              <input type="number" v-model="shape.radius.value" @input="handleVolume(shape)">
              <select v-model="shape.radius.unit" @change="handleVolume(shape)">
                <option value="1">Metrów</option>
                <option value="1000">Kilometrów</option>
              </select>
            </div>
            <!-- height -->
            <label>Wysokość:</label>
            <div>
              <input type="number" v-model="shape.height.value" @input="handleVolume(shape)">
              <select v-model="shape.height.unit" @change="handleVolume(shape)">
                <option value="1">Metrów</option>
                <option value="1000">Kilometrów</option>
              </select>
            </div>
            <!-- angle -->
            <label>Kąt:</label>
            <div>
              <input type="number" v-model="shape.angle" @input="handleVolume(shape)">
              <span>°</span>
            </div>
          </div>
        </div>

      </div>

      <!-- add new shape -->
      <button v-if="shape.visible" class="btn-add" @click="addNewShape(shape)">Dodaj kolejny kształt</button>
    </div>

    <!-- list of types + volume -->

    <div v-for="shape in shapes" :key="index">
      <p>{{ shape.type }}</p>
      <p>{{ shape.volume.toFixed(2) }} m³</p>
    </div>
    <div>
      <label>Zapas:</label>
      <input type="number" v-model="stock">
      <span>m³</span>
    </div>
    <div class="total">
      <p>
        Całkowita objętość: {{ stock ? (total + stock).toFixed(2) : total.toFixed(2) }} m³
      </p>
    </div>


  </div>
</template>

<script setup>
import { computed, ref } from 'vue';
const stock = ref(0)
const shapes = ref([
  {
    type: 'rectangle',
    width: {
      value: 0,
      unit: 1,
    },
    height: {
      value: 0,
      unit: 1,
    },
    length: {
      value: 0,
      unit: 1,
    },
    radius: {
      value: 0,
      unit: 1,
    },
    angle: 0,
    volume: 0,
    visible: true
  }
])


const total = computed(() => {
  return shapes.value.reduce((sum, value) => sum + value.volume, 0)
}
)

const addNewShape = (shape) => {
  shape.visible = false
  shapes.value.push({
    type: 'rectangle',
    width: {
      value: 0,
      unit: 1,
    },
    height: {
      value: 0,
      unit: 1,
    },
    length: {
      value: 0,
      unit: 1,
    },
    radius: {
      value: 0,
      unit: 1,
    },
    angle: 0,
    volume: 0,
    visible:true
  })
}

const removeShape = (idx) =>{
  shapes.value.splice(idx,1);
  
}

const handleVolume = (shape) => {
  if (shape.type === 'rectangle') {
    shape.volume = (shape.length.value * shape.length.unit) * (shape.height.value * shape.height.unit) * (shape.width.value * shape.width.unit)
  }
  else if (shape.type === 'triangle') {
    shape.volume = 0.5 * (shape.length.value * shape.length.unit) * (shape.height.value * shape.height.unit) * (shape.width.value * shape.width.unit)
  }
  else if (shape.type === 'circle') {
    shape.volume = Math.PI * Math.pow((shape.radius.value * shape.radius.unit), 2) * (shape.height.value * shape.length.unit) * (shape.angle / 360);
  }
}

</script>

<style scoped>
input[type="radio"]{
  display: block;
}
input::-webkit-outer-spin-button,
input::-webkit-inner-spin-button {
  -webkit-appearance: none;
  margin: 0;
}

input[type=number] {
  -moz-appearance: textfield;
}

.btn-add {
  display: block;
  margin: 2rem;
  padding: 1rem 0.5rem;
}
.form-wrapper-header{
  display: flex;
  align-items:center;
  justify-content: space-between;
}
.form-wrapper-header span{
  font-size: 1.75rem;
  padding:1rem;
  text-align: center;
  min-width:20px;
  margin-right:0.5rem;
}
.form-wrapper-header span:hover{
  cursor: pointer;
}
.total p{
  font-weight:800;
  font-size:1.25rem;
}
@media(min-width:650px){
  input[type="radio"]{
  display: inline;
}
}
</style>