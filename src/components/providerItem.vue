<!--Вывод одного поставщика в списке поставщиков-->
<template>
  <!--catalogItem.vue-->
  <transition name="vue-fade" mode="out-in"
              enter-active-class="animated zoomIn"
              leave-active-class="animated zoomOut">
    <div class="row catalog-list-r">
      <div class="col-12 catalog-list-c">
        <div class="catalog-list-i">
          <div class="catalog-h">
            <div class="title-cat">
              <div class="title">
                <div class="txt-link">
                  {{name}}
                </div>
              </div>
            </div>
            <div class="conf-panel">
              <!--<div class="item" v-if="isActive">-->
                <!--<button data-toggle="tooltip" data-placement="left" data-original-title="Активен">-->
                  <!--<div class="svg-c">-->
                    <!--<svg-->
                      <!--xmlns="http://www.w3.org/2000/svg"-->
                      <!--xmlns:xlink="http://www.w3.org/1999/xlink"-->
                      <!--width="10px" height="17px">-->
                      <!--<path fill-rule="evenodd"  fill="rgb(255, 229, 130)"-->
                            <!--d="M7.685,0.632 L5.598,7.629 L9.425,7.629 L2.119,16.631 L4.206,9.630 L0.384,9.630 L7.685,0.632 Z"/>-->
                    <!--</svg>-->
                  <!--</div>-->
                <!--</button>-->
              <!--</div>-->
              <div class="item">
                <button class="time-btn" data-toggle="tooltip" data-placement="top" data-original-title="Последнее обновление">
                  <div class="svg-c">
                    <svg
                      xmlns="http://www.w3.org/2000/svg"
                      xmlns:xlink="http://www.w3.org/1999/xlink"
                      width="17px" height="17px">
                      <path fill-rule="evenodd"  fill="rgb(131, 147, 167)"
                            d="M8.821,16.912 C4.403,16.912 0.821,13.330 0.821,8.912 C0.821,4.493 4.403,0.912 8.821,0.912 C13.239,0.912 16.821,4.493 16.821,8.912 C16.821,13.330 13.239,16.912 8.821,16.912 ZM8.821,2.999 C5.555,2.999 2.908,5.646 2.908,8.912 C2.908,12.177 5.555,14.825 8.821,14.825 C12.087,14.825 14.734,12.177 14.734,8.912 C14.734,5.646 12.087,2.999 8.821,2.999 ZM12.300,9.955 L8.821,9.955 C8.245,9.955 7.778,9.489 7.778,8.912 L7.778,5.434 C7.778,4.858 8.245,4.390 8.821,4.390 C9.397,4.390 9.865,4.858 9.865,5.434 L9.865,7.869 L12.300,7.869 C12.875,7.869 13.343,8.336 13.343,8.912 C13.343,9.489 12.875,9.955 12.300,9.955 Z"/>
                    </svg>
                  </div>
                  <span class="time-txt">
                    {{lastUpdate}}
                  </span>
                </button>
              </div>
              <div class="item">
                <button @click="$emit('configToogle')" data-toggle="tooltip" data-placement="top" data-original-title="Настройки">
                  <div class="svg-c">
                    <svg
                      xmlns="http://www.w3.org/2000/svg"
                      xmlns:xlink="http://www.w3.org/1999/xlink"
                      width="17px" height="17px">
                      <path fill-rule="evenodd"  fill="rgb(131, 147, 167)"
                            d="M16.039,9.965 L14.539,9.965 C14.387,10.629 14.115,11.244 13.765,11.805 L14.834,12.874 C15.095,13.135 15.095,13.557 14.834,13.817 L13.892,14.760 C13.631,15.020 13.209,15.020 12.949,14.760 L11.885,13.696 C11.324,14.051 10.708,14.326 10.039,14.478 L10.039,15.965 C10.039,16.333 9.741,16.632 9.373,16.632 L8.040,16.632 C7.671,16.632 7.373,16.333 7.373,15.965 L7.373,14.478 C6.705,14.326 6.088,14.051 5.527,13.696 L4.464,14.760 C4.203,15.020 3.781,15.020 3.521,14.760 L2.578,13.817 C2.318,13.557 2.318,13.135 2.578,12.874 L3.647,11.805 C3.297,11.244 3.025,10.629 2.874,9.965 L1.373,9.965 C1.004,9.965 0.706,9.666 0.706,9.299 L0.706,7.965 C0.706,7.597 1.004,7.298 1.373,7.298 L2.874,7.298 C3.025,6.634 3.297,6.019 3.647,5.459 L2.578,4.389 C2.318,4.128 2.318,3.707 2.578,3.446 L3.521,2.503 C3.781,2.243 4.203,2.243 4.464,2.503 L5.527,3.567 C6.088,3.212 6.705,2.938 7.373,2.785 L7.373,1.299 C7.373,0.930 7.671,0.632 8.040,0.632 L9.373,0.632 C9.741,0.632 10.039,0.930 10.039,1.299 L10.039,2.785 C10.708,2.938 11.324,3.212 11.885,3.567 L12.949,2.503 C13.209,2.243 13.631,2.243 13.892,2.503 L14.834,3.446 C15.095,3.707 15.095,4.128 14.834,4.389 L13.765,5.459 C14.115,6.019 14.387,6.634 14.539,7.298 L16.039,7.298 C16.408,7.298 16.706,7.597 16.706,7.965 L16.706,9.299 C16.706,9.666 16.408,9.965 16.039,9.965 ZM8.706,4.632 C6.497,4.632 4.706,6.423 4.706,8.632 C4.706,10.841 6.497,12.632 8.706,12.632 C10.915,12.632 12.706,10.841 12.706,8.632 C12.706,6.423 10.915,4.632 8.706,4.632 ZM8.706,10.632 C7.602,10.632 6.706,9.736 6.706,8.632 C6.706,7.527 7.602,6.631 8.706,6.631 C9.811,6.631 10.706,7.527 10.706,8.632 C10.706,9.736 9.811,10.632 8.706,10.632 Z"/>
                    </svg>
                  </div>
                </button>
              </div>
              <div class="item">
                <button :class="{isOnTr: isOn}" class="trIsOnB" @click="$emit('isOnToogle')" data-toggle="tooltip" data-placement="top" :data-original-title="isOn ? 'Выключить':'Включить'" >
                  <div class="svg-c">
                    <svg
                      xmlns="http://www.w3.org/2000/svg"
                      xmlns:xlink="http://www.w3.org/1999/xlink"
                      width="17px" height="17px">
                      <path fill-rule="evenodd"  fill="rgb(3, 189, 91)"
                            d="M8.973,16.632 C4.555,16.632 0.974,13.193 0.974,8.951 C0.974,6.143 2.546,3.692 4.888,2.353 C5.168,2.198 5.406,2.166 5.495,2.165 C6.073,2.165 6.541,2.615 6.541,3.169 C6.538,3.577 6.320,3.821 6.171,3.941 C6.149,3.956 6.063,4.019 5.977,4.066 C4.234,5.053 3.060,6.867 3.060,8.951 C3.060,12.086 5.708,14.628 8.973,14.628 L8.973,14.632 C12.239,14.632 14.886,12.095 14.886,8.965 C14.886,6.885 13.713,5.074 11.970,4.089 C11.884,4.042 11.797,3.980 11.777,3.964 C11.627,3.845 11.409,3.601 11.406,3.194 C11.406,2.641 11.874,2.192 12.452,2.192 C12.541,2.193 12.779,2.225 13.059,2.380 C15.402,3.716 16.974,6.163 16.974,8.965 C16.974,13.199 13.392,16.632 8.973,16.632 ZM8.973,8.632 C8.397,8.632 7.930,8.184 7.930,7.632 L7.930,1.632 C7.930,1.079 8.397,0.632 8.973,0.632 C9.550,0.632 10.017,1.079 10.017,1.632 L10.017,7.632 C10.017,8.184 9.550,8.632 8.973,8.632 Z"/>
                    </svg>
                  </div>
                </button>
              </div>
            </div>
          </div>
          <transition name="vue-fade" mode="out-in"
                      enter-active-class="animated fadeIn"
                      leave-active-class="animated fadeOut">
            <div v-show="showConfig" class="catalog-b">
              <div class="row">
                <div class="col-4 " v-for="(elem, index) in inputsArr" >
                  <appInput class="appInputLabel"
                            :key="index"
                            :validFeedback="elem.validFeedback"
                            :invalidFeedback="elem.invalidFeedback"
                            :placeholder="elem.placeholder"
                            :required="elem.required"
                            :pattern="elem.pattern"
                            :type="elem.type"
                            :value="elem.value"
                            :isValid="elem.isValid"
                            :showError="elem.showError"
                            @changedata="onChangeData(index, $event)"
                  >
                  </appInput>
                </div>
              </div>
              <div class="row align-items-end provider-config-r">
                <div class="col-6">
                  <div class="upload-t">
                    <div class="upload-i">
                      <div class="txt-lbl">
                        Частота обновления
                      </div>
                      <div class="btn-group" role="group" aria-label="update buttons">
                        <button v-for="(btn, index) in uploadBtnArr"
                                @click="$emit('uploadTime', {'value': btn.value, 'id': id})"
                                :class="{'active': btn.value === uploadTime}"
                                type="button" class="btn btn-outline-secondary">
                          {{btn.btnTxt}}
                        </button>
                      </div>
                    </div>
                  </div>
                </div>
                <div class="col-6">
                  <div class="btn-c">
                    <button v-if="catalogFileUrl" type="button" class="btn btn-outline-secondary">
                      <a :href="catalogFileUrl" target="_blank">
                        <span class="svg-c">
                          <svg
                            xmlns="http://www.w3.org/2000/svg"
                            xmlns:xlink="http://www.w3.org/1999/xlink"
                            width="25px" height="19px">
                            <path fill-rule="evenodd"  fill="rgb(131, 147, 167)"
                                  d="M19.315,18.507 C19.314,18.507 19.313,18.507 19.312,18.507 L19.312,18.507 L12.847,18.507 C13.118,18.511 13.390,18.424 13.596,18.217 L16.496,15.306 C16.903,14.899 16.903,14.237 16.496,13.829 C16.089,13.421 15.431,13.421 15.024,13.829 L13.796,15.062 L13.796,9.507 L11.803,9.507 L11.803,15.062 L10.575,13.829 C10.169,13.421 9.510,13.421 9.104,13.829 C8.697,14.237 8.697,14.899 9.104,15.306 L12.003,18.217 C12.213,18.428 12.490,18.515 12.763,18.507 L7.312,18.507 L7.312,18.507 C3.724,18.505 0.815,15.596 0.815,12.007 C0.815,8.742 3.230,6.065 6.367,5.603 C7.531,2.622 10.422,0.507 13.815,0.507 C18.104,0.507 21.595,3.884 21.796,8.124 C23.580,9.033 24.815,10.867 24.815,13.007 C24.815,16.045 22.353,18.507 19.315,18.507 Z"/>
                          </svg>
                        </span>
                        Скачать
                      </a>
                    </button>
                    <button @click="$emit('saveProvider')" type="button" class="btn btn-success">
                      Сохранить
                    </button>
                  </div>
                </div>
              </div>
            </div>
          </transition>
        </div>
      </div>
    </div>
  </transition>
</template>

<script>
  import appSwitcher from './switcher'
  import appInput from './inputValid'
	export default {
		name: "providerItem",
    data () {
      return {
        msg: 'providerItem'
      }
    },
    props: [
      'name', //имя поставщика
      'lastUpdate', // последнее обновление, приходит с сервера в виде строки
      'showConfig',// Тригер для отображения параметров переключателя(шестерёнка)
      'isOn', // Тригер для включения/отключения провайдера, если каталог отключён, то пользователи его не видят
      'id', //идентификатор
      'inputsArr', // массив инпатов
      'uploadTime', // частота обновления
      'uploadBtnArr', // массив кнопок (частота обновления)
      'catalogFileUrl', // файл для скачивания
    ],
    components: {
      appSwitcher,
      appInput
    },
    methods: {
      // для компонента input
      onChangeData(index, data){
        data.id = this.id;
        data.inputIndex = index;
        this.$emit('changeData', data);
        // this.inputsArr[index].value = data.value;
        // this.inputsArr[index].isValid = data.valid;
      }
    }
	}
</script>

<style >

</style>
