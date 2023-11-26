<template>
    <div>
        <div class="d-flex align-items-center justify-content-center almar-calculator">
            <div class="container">
                <div class="d-flex align-items-center justify-content-center text-primary text-center section-label">
                    <i class="as as-minus"></i>
                    <p class="label">Kalkulator betonu</p>
                </div>
                <h2 class="text-center section-title medium dark">Oblicz dokładną ilość betonu potrzebną do Twojego projektu
                </h2>
                <div class="calculator">
                    <div class="row">
                        <div class="col-12 col-xl-9 " v-for="shape,index in shapes" :key="index">
                            <div class="calculator-items">
                                <div class="calculator-item" data-index="1">
                                    <h4 class="d-flex align-items-center justify-content-between shape-label">
                                        <span data-bs-toggle="collapse"
                                        data-bs-target="#calculatorItem1"
                                            aria-expanded="true" aria-controls="calculatorItem1"
                                            >Kształt {{ index+1 }}</span><span
                                            v-show="shapes.length>1"
                                            class="d-flex align-items-center justify-content-end"
                                            @click="shape.visible=!shape.visible">
                                            <i class="me-3 as as-trash text-danger" @click="removeShape(shape)">Remove</i>
                                            <i class="as as-angle-up"
                                                
                                                data-bs-toggle="collapse" data-bs-target="#calculatorItem1"
                                                aria-expanded="true" aria-controls="calculatorItem1">Expand</i></span>
                                    </h4>
                                    <div class="collapse show" v-show="shape.visible" id="calculatorItem1" >
                                        <div class="calculator-item-content">
                                            <!-- shape form -->
                                            <ul class="nav nav-tabs border-0 d-flex justify-content-between"
                                                id="calculatorTabs1" role="tablist">
                                                <li class="nav-item" role="presentation">
                                                    <button class="border-0 w-100 nav-link active" id="calculatorSquareTab1"
                                                        data-bs-toggle="tab" data-bs-target="#calculatorSquare1"
                                                        type="button" role="tab" aria-controls="calculatorSquare1"
                                                        aria-selected="true" data-shape="square"
                                                        data-shape-name="Kwadrat lub prostokąt"
                                                        @click="handleVolume(shape,'square')">
                                                        <span class="d-block w-100 image square"></span>
                                                        <span>Kwadrat lub prostokąt</span>
                                                    </button>
                                                </li>

                                                <li class="nav-item" role="presentation">
                                                    <button class="border-0 w-100 nav-link" id="calculatorTriangleTab1"
                                                        data-bs-toggle="tab" data-bs-target="#calculatorTriangle1"
                                                        type="button" role="tab" aria-controls="calculatorTriangle1"
                                                        aria-selected="false" data-shape="triangle"
                                                        data-shape-name="Trójkąt prostokątny"
                                                        @click="handleVolume(shape,'triangle')">
                                                        <span class="d-block w-100 image triangle"></span>
                                                        <span>Trójkąt prostokątny</span>
                                                    </button>
                                                </li>

                                                <li class="nav-item" role="presentation">
                                                    <button class="border-0 w-100 nav-link" id="calculatorCircleTab1"
                                                        data-bs-toggle="tab" data-bs-target="#calculatorCircle1"
                                                        type="button" role="tab" aria-controls="calculatorCircle1"
                                                        aria-selected="false" data-shape="circle"
                                                        data-shape-name="Wycinek kołowy" @click="handleVolume(shape,'circle')">
                                                        <span class="d-block w-100 image circle"></span>
                                                        <span>Wycinek kołowy</span>
                                                    </button>
                                                </li>


                                            </ul>
                                            <!-- shape form -->



                                            <div class="tab-content">
                                                <!-- square calc -->
                                                <div class="tab-pane active" id="calculatorSquare1" role="tabpanel"
                                                    aria-labelledby="calculatorSquareTab1" tabindex="0"
                                                    v-if="shape.type === 'square'">
                                                    <div class="d-lg-flex align-items-lg-center justify-content-between">
                                                        <!-- square width -->
                                                        <div class="mb-3 mb-lg-0 form-group">
                                                            <p class="mb-2">Szerokość</p>
                                                            <div
                                                                class="d-flex align-items-center justify-content-between justify-content-lg-start parameters-wrap">
                                                                <input class="form-control" type="text"
                                                                    name="calculator_square_width" placeholder="0" v-model="shape.width.value" @input="handleVolume(shape,'square')"/>
                                                                <select class="form-select"
                                                                    name="calculator_square_width_unit" v-model="shape.width.unit" @change="handleVolume(shape,'square')">
                                                                    <option value=1>Metry</option>
                                                                    <option value=1000>Kilometry</option>
                                                                </select>
                                                            </div>
                                                        </div>
                                                        <!-- square width -->

                                                        <!-- square length -->
                                                        <div class="mb-3 mb-lg-0 form-group">
                                                            <p class="mb-2">Długość</p>
                                                            <div
                                                                class="d-flex align-items-center justify-content-between justify-content-lg-start parameters-wrap">
                                                                <input class="form-control" type="text"
                                                                    name="calculator_square_length" placeholder="0" v-model="shape.length.value" @input="handleVolume(shape,'square')"/>
                                                                <select class="form-select"
                                                                    name="calculator_square_length_unit" v-model="shape.length.unit" @change="handleVolume(shape,'square')">
                                                                    <option value=1>Metry</option>
                                                                    <option value=1000>Kilometry</option>
                                                                </select>
                                                            </div>
                                                        </div>
                                                        <!-- square length -->

                                                        <!-- square height -->
                                                        <div class="mb-3 mb-lg-0 form-group">
                                                            <p class="mb-2">Wysokość</p>
                                                            <div
                                                                class="d-flex align-items-center justify-content-between justify-content-lg-start parameters-wrap">
                                                                <input class="form-control" type="text"
                                                                    name="calculator_square_height" placeholder="0" v-model="shape.height.value" @input="handleVolume(shape,'square')"/>
                                                                <select class="form-select"
                                                                    name="calculator_square_height_unit" v-model="shape.height.unit" @change="handleVolume(shape,'square')">
                                                                    <option value=1>Metry</option>
                                                                    <option value=1000>Kilometry</option>
                                                                </select>
                                                            </div>
                                                        </div>
                                                        <!-- square height -->
                                                    </div>
                                                </div>
                                                <!-- square calc -->

                                                <!-- triangle calc -->
                                                <div class="tab-pane" id="calculatorTriangle1" role="tabpanel"
                                                    aria-labelledby="calculatorTriangleTab1" tabindex="0"
                                                    v-if="shape.type === 'triangle'">
                                                    <div class="d-lg-flex align-items-lg-center justify-content-between">
                                                        <!-- triangle width -->
                                                        <div class="mb-3 mb-lg-0 form-group">
                                                            <p class="mb-2">Szerokość</p>
                                                            <div
                                                                class="d-flex align-items-center justify-content-between justify-content-lg-start parameters-wrap">
                                                                <input class="form-control" type="text"
                                                                    name="calculator_triangle_width" placeholder="0" v-model="shape.width.value" @input="handleVolume(shape,'triangle')"/>
                                                                <select class="form-select"
                                                                    name="calculator_triangle_width_unit" v-model="shape.width.unit" @change="handleVolume(shape,'triangle')">
                                                                    <option value=1>Metry</option>
                                                                    <option value=1000>Kilometry</option>
                                                                </select>
                                                            </div>
                                                        </div>
                                                        <!-- triangle width -->

                                                        <!-- triangle length -->
                                                        <div class="mb-3 mb-lg-0 form-group">
                                                            <p class="mb-2">Długość</p>
                                                            <div
                                                                class="d-flex align-items-center justify-content-between justify-content-lg-start parameters-wrap">
                                                                <input class="form-control" type="text"
                                                                    name="calculator_triangle_length" placeholder="0" v-model="shape.length.value" @input="handleVolume(shape,'triangle')"/>
                                                                <select class="form-select"
                                                                    name="calculator_triangle_length_unit"
                                                                    v-model="shape.length.unit" @change="handleVolume(shape,'triangle')">
                                                                    <option value=1>Metry</option>
                                                                    <option value=1000>Kilometry</option>
                                                                </select>
                                                            </div>
                                                        </div>
                                                        <!-- triangle length -->

                                                        <!-- triangle height -->
                                                        <div class="mb-3 mb-lg-0 form-group">
                                                            <p class="mb-2">Wysokość</p>
                                                            <div
                                                                class="d-flex align-items-center justify-content-between justify-content-lg-start parameters-wrap">
                                                                <input class="form-control" type="text"
                                                                    name="calculator_triangle_height" placeholder="0" v-model="shape.height.value" @input="handleVolume(shape,'triangle')"/>
                                                                <select class="form-select"
                                                                    name="calculator_triangle_height_unit" 
                                                                    v-model="shape.height.unit" @change="handleVolume(shape,'triangle')">
                                                                    <option value=1>Metry</option>
                                                                    <option value=1000>Kilometry</option>
                                                                </select>
                                                            </div>
                                                        </div>
                                                        <!-- triangle height -->
                                                    </div>
                                                </div>
                                                <!-- triangle calc -->

                                                <!-- circle calc -->
                                                <div class="tab-pane" id="calculatorCircle1" role="tabpanel"
                                                    aria-labelledby="calculatorCircleTab1" tabindex="0"
                                                    v-if="shape.type === 'circle'">
                                                    <div class="d-lg-flex align-items-lg-center justify-content-between">

                                                        <!-- circle radius -->
                                                        <div class="mb-3 mb-lg-0 form-group">
                                                            <p class="mb-2">Promień</p>
                                                            <div
                                                                class="d-flex align-items-center justify-content-between justify-content-lg-start parameters-wrap">
                                                                <input class="form-control" type="text"
                                                                    name="calculator_circle_width" placeholder="0" v-model="shape.radius.value" @input="handleVolume(shape,'circle')"/>
                                                                <select class="form-select"
                                                                    name="calculator_circle_width_unit"
                                                                    v-model="shape.radius.unit" @change="handleVolume(shape,'circle')">
                                                                    <option value=1>Metry</option>
                                                                    <option value=1000>Kilometry</option>
                                                                </select>
                                                            </div>
                                                        </div>
                                                        <!-- circle radius -->

                                                        <!-- circle angle -->
                                                        <div class="mb-3 mb-lg-0 form-group">
                                                            <p class="mb-2">Kąt</p>
                                                            <div
                                                                class="d-flex align-items-center justify-content-between justify-content-lg-start parameters-wrap">
                                                                <input class="form-control" type="text"
                                                                    name="calculator_circle_length" placeholder="0" v-model="shape.angle" @input="handleVolume(shape,'circle')"/>
                                                            </div>
                                                        </div>
                                                        <!-- circle angle -->

                                                        <!-- circle height -->
                                                        <div class="mb-3 mb-lg-0 form-group">
                                                            <p class="mb-2">Wysokość</p>
                                                            <div
                                                                class="d-flex align-items-center justify-content-between justify-content-lg-start parameters-wrap">
                                                                <input class="form-control" type="text"
                                                                    name="calculator_circle_height" placeholder="0" v-model="shape.height.value" @input="handleVolume(shape,'circle')"/>
                                                                <select class="form-select"
                                                                    name="calculator_circle_height_unit" v-model="shape.radius.unit" @change="handleVolume(shape,'circle')">
                                                                    <option value=1>Metry</option>
                                                                    <option value=1000>Kilometry</option>
                                                                </select>
                                                            </div>
                                                        </div>
                                                        <!-- circle height -->

                                                    </div>
                                                </div>
                                                <!-- square calc -->

                                            </div>
                                        </div>
                                    </div>
                                </div>
                            </div>
                            <button type="button" id="addShapeBtn"
                            v-show="!shape.added"
                            @click="addNewShape(shape)"
                                class="mb-4 mb-xl-0 d-flex align-items-center justify-content-center btn btn-outline-primary">
                                <i class="me-1 as as-plus"></i>
                                Kolejny kształt
                            </button>
                        </div>
                        <div class="col-12 col-xl-3">
                            <div class="calculator-summary">
                                <div class="d-flex align-items-center justify-content-between top">
                                    <p>Kształt</p>
                                    <p class="text-end">Objętość</p>
                                </div>
                                <table class="items-list">
                                    <tr data-index="1" v-for="shape,index in shapes" :key="index">
                                        <td><strong class="index">{{index+1}}</strong></td>
                                        <td>
                                            <div class="image square"></div>
                                        </td>
                                        <td class="shape">{{
                                            shape.type === 'square' ? "Kwadrat lub prostokąt" : 
                                            shape.type === 'triangle' ? "Trójkąt prostokątny" : 
                                            shape.type === 'circle' ? "Wycinek kołowy" : null }}</td>
                                        <td class="text-end"><span class="value"></span>{{ shape.volume.toFixed(2) }}<span
                                                class="unit">m</span><sup>3</sup></td>
                                    </tr>
                                </table>
                                <div class="reserve">
                                    <label for="#reserve" class="d-block">Zapas betonu</label>
                                    <div class="d-flex align-items-center justify-content-between">
                                        <input id="reserve" type="text" class="form-control w-auto" placeholder="0" v-model="stock"/>
                                        <p class="mb-0">+ <span class="value">{{ stock }}</span> m<sup>3</sup></p>
                                    </div>
                                </div>
                                <div class="d-flex align-items-center justify-content-between bottom">
                                    <p>Całkowita objętość</p>
                                    <p><span class="summary-value">{{ stock>0 ? (parseFloat(total)+parseFloat(stock)).toFixed(2) : total.toFixed(2) }}</span> m<sup>3</sup></p>
                                </div>
                                <button type="button"
                                    class="d-flex align-items-center justify-content-center btn btn-primary text-white">
                                    Poproś o wycenę
                                    <i class="as as-arrow-right"></i>
                                </button>
                            </div>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>

<script setup>
import { computed, ref } from 'vue';
const stock = ref(null);
const shapes = ref([
    {
        type:'square',
        added:false,
        width: {
            value: null,
            unit: 1,
        },
        height: {
            value: null,
            unit: 1,
        },
        length: {
            value: null,
            unit: 1,
        },
        radius: {
            value: null,
            unit: 1,
        },
        angle: null,
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
    shape.added = true
    shapes.value.push({
        type:'square',
        width: {
            value: null,
            unit: 1,
        },
        height: {
            value: null,
            unit: 1,
        },
        length: {
            value: null,
            unit: 1,
        },
        radius: {
            value: null,
            unit: 1,
        },
        angle: null,
        volume: 0,
        visible: true
    })
}

const removeShape = (idx) => {
    shapes.value.splice(idx, 1);
}

const handleVolume = (shape,figure) => {
    shape.type = figure
    if (shape.type === 'square') {
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

<style scoped></style>