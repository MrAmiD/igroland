<!--Список всех каталогов-->

<!--todo: API - Добавить каталог-->
<!--todo: API - Удалить каталог-->
<!--todo: API - Скопировать каталог-->
<!--todo: API - Список каталогов, запрашивается несколько(10) каталогов, в зависимости от страницы, в этом же запросе возвращать данные для пагинации-->
<!--todo: API - блокировать/разблокировать каталог-->

<!--todo: API - Сохранить каталог (после редактирования)-->
<!--todo: API - Запрос списка пользователей(для селекта), для всех каталогов он один-->


<template>
  <!--catalogList.vue-->
  <div class="catalogComp">
    <div class="row">
      <div class="col-12">
        <div class="btn-c">
          <button @click="addNewCatalog" type="button" class="btn btn-outline-secondary">Новый каталог</button>
        </div>
      </div>
      <div class="col-12 mt-3">

      </div>
    </div>
    <!--todo: вынести в отдельный компонент-->

      <!--<template v-for="(catalogItem, index) in catalogList">-->
        <!--{{catalogItem.switcherActive}} {{index}} // <br>-->
      <!--</template>-->

      <!--
          todo: Доделать пагинацию
          todo: Загрузка фото
          todo: Добавить редактирование имени каталога, справа от названия добавить кнопку с карандашиком. при нажатии на кнопку, заменять название на инпат(???)
          todo: добавить массив со страницами в состояние
      -->

      <div class="row" v-if="Object.keys(catalogList).length == 0">
        <div class="col-12">
          <div class="white-block-r ">
            <h4 class="mb-0">
              Список каталогов пуст, для создания нового каталога, используйте кнопку "Новый каталог"
            </h4>
          </div>
        </div>
      </div>

      <appCatalogItem v-else v-for="(catalogItem, index) in catalogList"
        :key="index"
        :selected="catalogItem.selected"
        :switcherActive="catalogItem.switcherActive"
        :showConfig="catalogItem.showConfig"
        :userList="catalogItem.userList"
        :catalogName="catalogItem.catalogName"
        :catalogId="index"
        :isActive="catalogItem.isActive"
        :isOn="catalogItem.isOn"
        :description="catalogItem.description"
        :selectedUsers="catalogItem.selectedUsers"
        @configToogle = "onConfigToogle(index)"
        @switchToogle = "onSwitchToogle(index)"
        @isOnToogle = "onIsOnToogle(index)"
        @changeDescr = "onChangeDescr(index, $event)"
        @copyCatalog = "onCopyCatalog(index)"
        @saveCatalog = "onSaveCatalog(index)"
        @changeSelect = "onChangeSelect(index)"
        @removeCatalog = "onRemoveCatalog(index)">
      </appCatalogItem>

      <appPagination v-if="Object.keys(catalogList).length != 0" :countPage = "pagination.countPage"
        :routerLink="/catalog/"
        :routerOn="pagination.routerOn"
        @pageChange = "onPageChange()">
      </appPagination>

    <!--<div class="row">-->
      <!--<div class="col-12">-->
        <!--<nav aria-label="Page navigation example">-->
          <!--<ul class="pagination">-->
            <!--<li class="page-item">-->
              <!--<a class="page-link" href="#" aria-label="Previous">-->
                <!--<span aria-hidden="true">&laquo;</span>-->
                <!--<span class="sr-only">Предыдущая</span>-->
              <!--</a>-->
            <!--</li>-->
            <!--<li class="page-item is-active"><a class="page-link" href="#">1</a></li>-->
            <!--<li class="page-item dots-pag"><a class="page-link" href="#">...</a></li>-->
            <!--<li class="page-item"><a class="page-link" href="#">2</a></li>-->
            <!--<li class="page-item"><a class="page-link" href="#">3</a></li>-->
            <!--<li class="page-item"><a class="page-link" href="#">4</a></li>-->
            <!--<li class="page-item dots-pag"><a class="page-link" href="#">...</a></li>-->
            <!--<li class="page-item"><a class="page-link" href="#">15</a></li>-->
            <!--<li class="page-item">-->
              <!--<a class="page-link" href="#" aria-label="Next">-->
                <!--<span aria-hidden="true">&raquo;</span>-->
                <!--<span class="sr-only">Следующая</span>-->
              <!--</a>-->
            <!--</li>-->
          <!--</ul>-->
        <!--</nav>-->
      <!--</div>-->
    <!--</div>-->

    <!-- Modal -->
    <div class="modal fade warning-modal" id="confirmDeleteModal" tabindex="-1" role="dialog" aria-labelledby="exampleModalCenterTitle" aria-hidden="true">
      <div class="modal-dialog modal-dialog-centered" role="document">
        <div class="modal-content">
          <div class="modal-header">
            <h5 class="modal-title" id="exampleModalCenterTitle">
              <div class="svg-c">
                <svg
                  xmlns="http://www.w3.org/2000/svg"
                  xmlns:xlink="http://www.w3.org/1999/xlink"
                  width="23px" height="23px">
                  <path fill-rule="evenodd"  fill="rgb(131, 147, 167)"
                        d="M11.500,23.000 C5.149,23.000 0.000,17.851 0.000,11.500 C0.000,5.149 5.149,-0.000 11.500,-0.000 C17.851,-0.000 23.000,5.149 23.000,11.500 C23.000,17.851 17.851,23.000 11.500,23.000 ZM11.500,5.000 C10.672,5.000 10.000,5.671 10.000,6.500 C10.000,7.328 10.672,8.000 11.500,8.000 C12.328,8.000 13.000,7.328 13.000,6.500 C13.000,5.671 12.328,5.000 11.500,5.000 ZM13.000,10.500 C13.000,9.671 12.328,9.000 11.500,9.000 C10.672,9.000 10.000,9.671 10.000,10.500 L10.000,16.500 C10.000,17.328 10.672,18.000 11.500,18.000 C12.328,18.000 13.000,17.328 13.000,16.500 L13.000,10.500 Z"/>
                </svg>
              </div>
              <div class="txt">
                Подтвердите удаление каталога
              </div>
            </h5>
            <button type="button" class="close" data-dismiss="modal" aria-label="Close">
              <span aria-hidden="true">&times;</span>
            </button>
          </div>
          <div class="modal-body">
            <appInput v-for="(elem, index) in inputsArr" :key="index"
                      :validFeedback="elem.validFeedback"
                      :invalidFeedback="elem.invalidFeedback"
                      :placeholder="elem.placeholder"
                      :required="elem.required"
                      :pattern="elem.pattern"
                      :type="elem.type"
                      :value="elem.value"
                      :isValid="elem.isValid"
                      :showError="elem.showError"
                      @changedata="onChangeData(index, $event)">
            </appInput>
          </div>
          <div class="modal-footer">
            <button type="button" class="btn btn-secondary" data-dismiss="modal">Отмена</button>
            <button type="button" class="btn btn-danger" data-dismiss="modal" @click="removeCatalog(removeCatalogIndex)">Удалить каталог</button>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>

  import appCatalogItem from './catalogItem'
  import appInput from './inputValid';
  import appPagination from './pagination'
  import {API_URL} from '../constants'
  import axios from 'axios'

  import {mapGetters} from 'vuex';
  import {mapMutations} from 'vuex';

  export default {
    name: 'catalogList',
    data () {
      return {
        // catalogList["123"]
        catalogList: { // ассоциативный массив объектов
            123: { // Идентификатор каталога
              selected: null, // выбранные элементы в селекте
              switcherActive: false, // активность переключателя (Доступен для всех)
              showConfig: false, // Тригер для отображения параметров переключателя(шестерёнка)
              catalogName: 'Игрушки', // Наименование каталога
              isActive: true, // каталог активен(значёе молнии), один или несколько пользователей используют его
              isOn: true, // Тригер для включения/отключения каталога, если каталог отключён, то пользователи его не видят
              description: 'Краткое описание каталога', // краткое описание каталога
              catalogImg: '', // Изображение каталога
              catalogSaved: true,//каталог сохранён, при внесении изменений или копирывании каталога ставим в false... если каталог не сохранён, то его нельзя скопировать и выводится ошибка(предупреждение) для пользователя
              userList: [ // пользователи для селекта
                {name: 'user@gmail.com', id: '1234'},
                {name: 'goner@gmail.com', id: '4453'},
                {name: '2user2@gmail.com', id: '8489'}
              ],
              selectedUsers: [ // выбранные пользователи в селекте
                {name: 'user@gmail.com', id: '1234'},
              ]
            },
            1232: { // Идентификатор каталога
              selected: null, // выбранные элементы в селекте
              switcherActive: false, // активность переключателя
              showConfig: false, // Тригер для отображения параметров переключателя
              catalogName: 'Игрушки2', // Наименование каталога
              isActive: false, // каталог активен(значёе молнии), один или несколько пользователей используют его
              isOn: false, // Тригер для включения/отключения каталога, если каталог отключён, то пользователи его не видят
              description: '', // краткое описание каталога
              catalogImg: '', // Изображение каталога
              catalogSaved: true,//каталог сохранён, при внесении изменений или копирывании каталога ставим в false... если каталог не сохранён, то его нельзя скопировать и выводится ошибка(предупреждение) для пользователя
              userList: [ // пользователи для селекта
                {name: 'user@gmail.com'},
                {name: 'goner@gmail.com'},
                {name: '2user2@gmail.com'}
              ]
            }
        },
        inputsArr:[
          {
            id: 'confirmDelete',
            showError: '',
            validFeedback: "",
            invalidFeedback: "Имя введено неверно",
            placeholder: "Введите имя каталога, который хотите удалить",
            type: "text",
            required: "true",
            pattern: /[^]*/,
            value: '',
            isValid: false
          }
        ],
        removeCatalogIndex: 0, // индекс каталога, который надо удалить,
        //pagination, при переключении страницы, делаем запрос к серверу
        pagination:{
          countPage: 12, // общее колличество страниц, делаем запрос к базе
          countItemsPage: 12, // колличество элементов на странице
          routerOn: true // // отключение роутера, если включить, то надо настроить роутер
        },
      }
    },
    computed: {
      ...mapGetters('alerts',
        {
          succesAlert: 'succesAlert',
          errorAlert: 'errorAlert'
        }),
      ...mapGetters('progress', {
        progStateWidth: 'progStateWidth',
        progShow: 'progShow'
      })
    },
    methods: {
      ...mapMutations('alerts',{
        setSuccesAlertShow: 'setSuccesAlertShow',
        setErrorAlertShow: 'setErrorAlertShow',
        setSuccesAlertMsg: 'setSuccesAlertMsg',
        setErrorAlertMsg: 'setErrorAlertMsg'
      }),
      ...mapMutations('progress',{
        setProgStateWidth: 'setProgStateWidth',
        setProgShow: 'setProgShow',
        stepOneActive: 'stepOneActive',
        stepTwoActive: 'stepTwoActive',
        stepLastActive: 'stepLastActive',
      }),
      //переключение каталога в режим не сохранён
      falseCatalogSave(index){
        this.catalogList[index].catalogSaved = false;
      },
      // переключение шестерёнки (настройки каталога)
      onConfigToogle(index){
        this.catalogList[index].showConfig = !this.catalogList[index].showConfig;
      },
      // включение/отключение каталога
      onIsOnToogle(index){
        this.catalogList[index].isOn = !this.catalogList[index].isOn;
        this.falseCatalogSave(index);
      },
      // переключение "Доступен для всех"
      onSwitchToogle(index){
        this.catalogList[index].switcherActive = !this.catalogList[index].switcherActive;
        this.falseCatalogSave(index);
      },
      // изменение описания
      onChangeDescr(index, e){
        this.catalogList[index].description = e.value;
        this.falseCatalogSave(index);
      },
      // копирование каталога
      onCopyCatalog(index){
        //копируем, создаём новый каталог на основе существующего, на стороне клиента
        //далее, только при нажатии на кнопку 'сохранить' отправляем этот каталог на сервер, на сервере каталогу присвается новый ид, этот ид приходит в ответе на операцию сохранения

        let indRand = (new Date).getTime();//unixtime in mileseconds
        this.$set(this.catalogList, indRand, Object.assign({}, this.catalogList[index]));

        $("html, body").animate({ scrollTop: $('.pagination').offset().top - 120}, 600);

        // this.catalogList.splice(indRand, 1, this.catalogList[indRand]);

        this.catalogList[indRand].catalogName = this.catalogList[index].catalogName + ' (копия)';
        this.falseCatalogSave(indRand);
      },
      // сохранение каталога
      onSaveCatalog(index){
        if(this.catalogList[index].catalogSaved){
          this.setSuccesAlertShow(true);
          this.setSuccesAlertMsg('Каталог сохранён');
        }else {
          let payload = this.catalogList[index];
          this.stepOneActive(); // прогрессбар
          axios({url: API_URL + '/saveCatalog', data: payload, method: 'POST' })
            .then(resp => {
              const error = resp.data.error;
              this.stepLastActive(); // прогрессбар
              if(error){
                let errorTxt = resp.data.data.msgClient;
                this.setErrorAlertShow(true);
                this.setErrorAlertMsg('Ошибка при сохранении каталога: ' + errorTxt);
              }else {
                this.catalogList[index].catalogSaved = true;
                this.setSuccesAlertShow(true);
                this.setSuccesAlertMsg('Каталог сохранён');
              }
            })
            .catch(err => {
              this.setErrorAlertShow(true);
              this.setErrorAlertMsg('Ошибка при сохранении каталога');
              this.stepLastActive(); // прогрессбар
              console.log(err);
            });
        }
        // let indRand = (new Date).getTime();//unixtime in mileseconds
        // this.$set(this.catalogList, indRand, Object.assign({}, this.catalogList[index]));
        // this.catalogList[indRand].catalogName = this.catalogList[index].catalogName + ' (копия)';

      },
      // удаление каталога, открытие окна подтверждения
      onRemoveCatalog(index){
        this.removeCatalogIndex = index;
        $('#confirmDeleteModal').modal();
      },
      //выполняется при переключении страницы
      onPageChange(){
        console.log('onPageChange');
      },
      // удаление каталога
      removeCatalog(index){

        if(this.inputsArr[0].value === this.catalogList[index].catalogName){
          let payload = this.catalogList[index];
          this.stepOneActive(); // прогрессбар
          axios({url: API_URL + '/removeCatalog', data: payload, method: 'POST' })
            .then(resp => {
              const error = resp.data.error;
              this.stepLastActive(); // прогрессбар
              if(error){
                let errorTxt = resp.data.data.msgClient;
                this.setErrorAlertShow(true);
                this.setErrorAlertMsg('Ошибка при удалении каталога: ' + errorTxt);
              }else{
                this.$delete(this.catalogList, index, this.catalogList[index]);
                this.setSuccesAlertShow(true);
                this.setSuccesAlertMsg('Каталог удалён');
              }
            })
            .catch(err => {
              this.setErrorAlertShow(true);
              this.setErrorAlertMsg('Ошибка при удалении каталога ');
              this.stepLastActive(); // прогрессбар
              console.log(err);
            });
        }else{
          this.setErrorAlertShow(true);
          this.setErrorAlertMsg('Ошибка при удалении каталога: имена не совпадают');
        }
      },
      //выполняется при  изменении селекта
      onChangeSelect(index){
        //Делать запрос на сервер для копирования?
        console.log('onChangeSelect');
        this.falseCatalogSave(index);
      },
      // для компонента input
      onChangeData(index, data){
        this.inputsArr[index].value = data.value;
        this.inputsArr[index].isValid = data.valid;
      },
      //Добавить новый каталог
      addNewCatalog(){
        let payload = {};
        this.stepOneActive(); // прогрессбар
        axios({url: API_URL + '/addCatalog', data: payload, method: 'POST' })
          .then(resp => {
            const error = resp.data.error;
            this.stepLastActive(); // прогрессбар
            if(error){
              let errorTxt = resp.data.data.msgClient;
              this.setErrorAlertShow(true);
              this.setErrorAlertMsg('Ошибка при добавлении каталога: ' + errorTxt);
            }else{
              this.$delete(this.catalogList, index, this.catalogList[index]);
              this.setSuccesAlertShow(true);
              this.setSuccesAlertMsg('Каталог добавлен');
            }
          })
          .catch(err => {
            this.setErrorAlertShow(true);
            this.setErrorAlertMsg('Ошибка при добавлении каталога ');
            this.stepLastActive(); // прогрессбар
            console.log(err);
          });

      }
    },
    components: {
      appCatalogItem,
      appInput,
      appPagination
    },
    mounted(){
      $('[data-toggle="tooltip"]').tooltip();
    }
  }
</script>

<style lang="sass">
  @import '../../node_modules/vue-multiselect/dist/vue-multiselect.min.css'
  /*@import 'assets/sass/main.sass';*/
</style>
