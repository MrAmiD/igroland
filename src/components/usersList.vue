<!--Список пользователей-->
<template>
  <!--usersList.vue-->

  <!--todo: API - блокировка пользователя
      todo: API - список незаблокированных пользователей
      todo: API - список всех пользователей (заблокированные и активные)
      todo: API - список активных пользователей
      todo: API - поиск пользователей по подстроке
  -->

  <!--
    todo: переделать ассециативный массив, на обычный usersList
  -->

  <div class="container">
    <div class="white-block-r">
      <div class="row align-items-center">
        <div class="col-6">
          <div class="user-cntr-bar">
            <appSwitcher  txt="Все пользователи"
                          :switcherActive="switcherActive"
                          @switchToogle="onSwitchToogle">
            </appSwitcher>
            <div class="new-usr-i" >
              <button type="button" @click="showRegPanel(true)" class="btn btn-outline-secondary" v-if="!showSignup">Новый пользователь</button>
              <button type="button" @click="showRegPanel(false)" class="btn btn-outline-secondary" v-else>Скрыть панель регистрации</button>
            </div>
          </div>
        </div>
        <div class="col-6">
          <div class="find-b justify-content-end d-flex">
            <div class="input-group ">
              <input v-model.lazy="findUserStr" v-on:keyup.enter="findUser" type="text" class="form-control" placeholder="Найти" aria-label="Recipient's username" aria-describedby="button-addon2">
              <div class="input-group-append">
                <button class="btn btn-outline-secondary" type="button" @click="findUser">
                  <svg
                    xmlns="http://www.w3.org/2000/svg"
                    xmlns:xlink="http://www.w3.org/1999/xlink"
                    width="17px" height="17px">
                    <path fill-rule="evenodd"  fill="rgb(131, 147, 167)"
                          d="M15.919,15.813 C15.525,16.207 14.887,16.207 14.494,15.813 L11.403,12.723 C10.235,13.594 8.792,14.117 7.223,14.117 C3.357,14.117 0.223,10.983 0.223,7.117 C0.223,3.251 3.357,0.117 7.223,0.117 C11.088,0.117 14.222,3.251 14.222,7.117 C14.222,8.686 13.700,10.130 12.828,11.298 L15.919,14.388 C16.312,14.782 16.312,15.420 15.919,15.813 ZM7.223,2.117 C4.461,2.117 2.222,4.355 2.222,7.117 C2.222,9.879 4.461,12.117 7.223,12.117 C9.984,12.117 12.223,9.879 12.223,7.117 C12.223,4.355 9.984,2.117 7.223,2.117 Z"/>
                  </svg>
                </button>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>

    <transition name="vue-fade" mode="out-in"
                enter-active-class="animated fadeIn"
                leave-active-class="animated fadeOut">
      <div class="row" v-if="showSignup" >
          <div class="col-4">
            <div class="white-block-r">
              <div class="hideRegQuest">
                <appSignup :regBtnTxt="regBtnTxt"></appSignup>
              </div>
            </div>
          </div>
      </div>
    </transition>

    <template v-for="(userItem, index) in usersList">
      <transition name="vue-fade" mode="out-in"
                  enter-active-class="animated zoomIn"
                  leave-active-class="animated zoomOut">
        <div class="row catalog-list-r">
          <div class="col-12 catalog-list-c">
            <div class="catalog-list-i">
              <div class="catalog-h">
                <div class="title-cat">
                  <div class=" ava-c" data-placement="bottom">
                    <img :src="userItem.avatar" :alt="userItem.name">
                  </div>
                  <div class="user-info">
                    <div class="h-user-name">
                      {{userItem.name + ' ' + userItem.surname}}
                    </div>
                    <div class="h-user-role">
                      {{userItem.email}}
                    </div>
                  </div>
                </div>
                <div class="conf-panel">
                  <div class="item">
                    <button  class="" data-dismiss="modal" @click="openRemoveModal(userItem.id)" data-toggle="tooltip" data-placement="top" data-original-title="Удалить пользователя" >
                      <div class="svg-c">
                        <svg
                          xmlns="http://www.w3.org/2000/svg"
                          xmlns:xlink="http://www.w3.org/1999/xlink"
                          width="16px" height="17px">
                          <path fill-rule="evenodd"  fill="rgb(131, 147, 167)"
                                d="M14.309,6.310 L13.309,6.310 L13.309,15.977 C13.309,16.529 12.861,16.977 12.309,16.977 L3.643,16.977 C3.090,16.977 2.642,16.529 2.642,15.977 L2.642,6.310 L1.642,6.310 C1.090,6.310 0.642,5.862 0.642,5.310 C0.642,4.758 1.090,4.310 1.642,4.310 L3.643,4.310 L4.643,4.310 C4.643,2.469 6.135,0.977 7.976,0.977 C9.817,0.977 11.309,2.469 11.309,4.310 L12.309,4.310 L14.309,4.310 C14.862,4.310 15.309,4.758 15.309,5.310 C15.309,5.862 14.862,6.310 14.309,6.310 ZM7.309,14.977 L8.643,14.977 L8.643,6.977 L7.309,6.977 L7.309,14.977 ZM4.643,6.977 L4.643,14.977 L5.976,14.977 L5.976,6.977 L4.643,6.977 ZM7.976,2.310 C6.872,2.310 5.976,3.205 5.976,4.310 L9.976,4.310 C9.976,3.205 9.080,2.310 7.976,2.310 ZM11.309,6.977 L9.976,6.977 L9.976,14.977 L11.309,14.977 L11.309,6.977 Z"/>
                        </svg>
                      </div>
                    </button>
                  </div>
                  <div class="item">
                    <button :class="{isOnTr: !userItem.blocked}" class="trIsOnB" @click="isOnToogle(userItem.id)" data-toggle="tooltip" data-placement="top" :data-original-title="userItem.blocked ? 'Разблокировать':'Заблокировать'" >
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
            </div>
          </div>
        </div>
      </transition>
    </template>

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
                Подтвердите удаление пользователя
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
            <button type="button" class="btn btn-danger" data-dismiss="modal" @click="deleteUser(removeUserIndex)">Удалить пользователя</button>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
  import appSwitcher from './switcher';
  import {API_URL} from '../constants';
  import axios from 'axios';
  import {mapGetters} from 'vuex';
  import {mapMutations} from 'vuex';
  import appInput from './inputValid';
  import appSignup from './SignUp.vue';
  export default {
    name: 'usersList',
    data () {
      return {
        usersList: {
          123: {
            name: 'MrAmiD', // Имя пользователя
            role: 'Ninja',//'права' пользователя
            avatar: 'src/assets/img/avatar.png',//аватарка
            email: 'someMail@gmail.com', // email
            site: 'site.ru', //какой-то сайт
            phone: '+7(953)345-34-54', // телефон
            surname: 'Surname', // фамилия
            lastName: 'lastName', // отчество
            login: 'someMail@gmail.com', // login
            id: 123, // id
            blocked: false // заблокирован
          }
        },
        switcherActive: true, // все пользователи
        findUserStr: '', // Подстрока для поиска пользователя
        removeUserIndex: '', // Ид пользователя для удаления
        inputsArr:[
          {
            id: 'confirmDelete',
            showError: '',
            validFeedback: "",
            invalidFeedback: "Email введен неверно",
            placeholder: "Введите Email пользователя, которого хотите удалить",
            type: "text",
            required: "true",
            pattern: /[^]*/,
            value: '',
            isValid: false
          }
        ],
        regBtnTxt: 'Зарегистрировать нового пользователя',// текст кнопки регистрации
        showSignup: false, // показывать окно для регистрации нового пользователя
      }
    },
    computed: {
      ...mapGetters('alerts', {
        succesAlert: 'succesAlert',
        errorAlert: 'errorAlert'
      }),
      ...mapGetters('progress', {
        progStateWidth: 'progStateWidth',
        progShow: 'progShow'
      }),
      currentPage(){ // текущая страница, передаётся в url в качестве параметра
        return this.$route.params.page || 1;
      }
    },
    components: {
      appSwitcher,
      appInput,
      appSignup
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
      onSwitchToogle(){// переключение "Все пользователи"

        let payload = this.switcherActive;
        this.stepOneActive(); // прогрессбар

        axios({url: API_URL + '/user/userlist', data: payload, method: 'POST' })
          .then(resp => {
            const error = resp.data.error;
            this.stepLastActive(); // прогрессбар
            if(error){
              this.stepLastActive();
              let errorTxt = resp.data.data.msgClient;
              this.setErrorAlertShow(true);
              this.setErrorAlertMsg('Ошибка при фильтрации пользователей: ' + errorTxt);
            }else {
              this.stepLastActive();
              this.switcherActive = !this.switcherActive;
              this.usersList[index].blocked = !this.usersList[index].blocked;
              this.setSuccesAlertShow(true);
              this.setSuccesAlertMsg('Пользователи отфильтрованы');
            }
          })
          .catch(err => {
            this.setErrorAlertShow(true);
            this.setErrorAlertMsg('Ошибка при фильтрации пользователей');
            console.log(err);
            this.stepLastActive();
          });
      },
      isOnToogle(index){ // заблокировать/разблокировать пользователя
        let payload = this.usersList[index];

        this.stepOneActive(); // прогрессбар

        axios({url: API_URL + '/blockuser', data: payload, method: 'POST' })
          .then(resp => {
            const error = resp.data.error;
            this.stepLastActive(); // прогрессбар
            if(error){
              let errorTxt = resp.data.data.msgClient;
              this.setErrorAlertShow(true);
              this.setErrorAlertMsg('Ошибка при блокировке пользователя: ' + errorTxt);
            }else {
              this.usersList[index].blocked = !this.usersList[index].blocked;
              this.setSuccesAlertShow(true);
              this.setSuccesAlertMsg('Пользователь заблокирован');
            }
          })
          .catch(err => {
            this.setErrorAlertShow(true);
            this.setErrorAlertMsg('Ошибка при блокировке пользователя');
            this.stepLastActive(); // прогрессбар
            console.log(err);
          });

      },
      findUser(){
        let payload = this.findUserStr;

        this.stepOneActive(); // прогрессбар

        axios({url: API_URL + '/user/finduser', data: payload, method: 'POST' })
          .then(resp => {
            const error = resp.data.error;
            this.stepLastActive(); // прогрессбар
            if(error){
              let errorTxt = resp.data.data.msgClient;
              this.setErrorAlertShow(true);
              this.setErrorAlertMsg(`Ошибка при поиске пользователя по запросу '${this.findUserStr}'; ${errorTxt}`);
            }else {
              this.setSuccesAlertShow(true);
              this.setSuccesAlertMsg(`Пользователи по запросу '${this.findUserStr}'`);
            }
          })
          .catch(err => {
            this.setErrorAlertShow(true);
            this.setErrorAlertMsg(`Ошибка при поиске пользователя по запросу '${this.findUserStr}'`);
            this.stepLastActive(); // прогрессбар
            console.log(err);
          });
      },
      deleteUser(index){
        console.log('delete user', index);
        if(this.inputsArr[0].value === this.usersList[index].email){
          let payload = this.usersList[index];
          this.stepOneActive(); // прогрессбар
          axios({url: API_URL + '/login', data: payload, method: 'POST' })
            .then(resp => {
              const error = resp.data.error;
              this.stepLastActive(); // прогрессбар
              if(error){
                let errorTxt = resp.data.data.msgClient;
                this.setErrorAlertShow(true);
                this.setErrorAlertMsg('Ошибка при удалении пользователя: ' + errorTxt);
              }else{
                this.$delete(this.usersList, index, this.usersList[index]);
                this.setSuccesAlertShow(true);
                this.setSuccesAlertMsg('Пользователь удалён');
              }
            })
            .catch(err => {
              this.setErrorAlertShow(true);
              this.setErrorAlertMsg('Ошибка при удалении пользователя ');
              this.stepLastActive(); // прогрессбар
              console.log(err);
            });
        }else{
          this.setErrorAlertShow(true);
          this.setErrorAlertMsg('Ошибка при удалении пользователя: имена не совпадают');
        }
      },
      openRemoveModal(index){ // открытие окна подтверждения для удаления пользователя
        this.removeUserIndex = index;
        $('#confirmDeleteModal').modal();
      },
      onChangeData(index, data){ // для компонента input
        this.inputsArr[index].value = data.value;
        this.inputsArr[index].isValid = data.valid;
      },
      showRegPanel(showPanel){
        this.showSignup = showPanel;
      }
    }
  }
</script>

<style lang="sass">
  /*@import 'assets/sass/main.sass';*/
</style>
