<template>
    <form @submit.prevent="someAction()" @submit="action()">
        <transition name="appearance" appear>  
        <div v-if="!successfulIsTrue">
            <div class="container">
                <div> 
                    <h2>Данные</h2>  
                    <div>
                    <label for="surname">Фамилия<span class="red">*</span></label>
                    <input id="surname" type="text" v-model="defaultState.surname" placeholder="Иванов">
                    <span class="errorMsg" v-if="!$v.defaultState.surname.valid && $v.defaultState.surname.required">
                        В фамилии недопустимые символы
                    </span>
                    <span class="errorMsg" v-if="!$v.defaultState.surname.required">
                        Необходимо заполнить поле
                    </span>
                    </div>
                    <div>
                        <label for="name">Имя<span class="red">*</span></label>
                        <input id="name" type="text" v-model="defaultState.name" placeholder="Иван">
                        <span class="errorMsg" v-if="!$v.defaultState.name.valid && $v.defaultState.name.required">
                                В имени недопустимые символы
                        </span>
                        <span class="errorMsg" v-if="!$v.defaultState.name.required">
                        Необходимо заполнить поле
                        </span>
                    </div>
                    <div>
                        <label for="secondName">Отчество</label>
                        <input id="secondName" type="text" v-model="defaultState.secondName">

                    </div>
                    <div>
                        <label for="dateBirth">Дата рождения<span class="red">*</span></label>
                        <input id="dateBirth" type="date" v-model="defaultState.dateBirth" @blur="$v.defaultState.dateBirth.$touch()" placeholder="01.01.2000">
                        <span class="errorMsg" v-if="!$v.defaultState.dateBirth.valid && $v.defaultState.dateBirth.$model">
                            Дата рождения не может быть больше текущей
                        </span>
                        <span class="errorMsg" v-if="!$v.defaultState.dateBirth.required">
                        Необходимо заполнить поле
                        </span>
                    </div>
                    <div>
                        <label for="phone">Номер телефона<span class="red">*</span></label>
                        <input id="phone" type="tel" v-model="defaultState.phone" placeholder="790000000">
                        <span class="errorMsg" v-if="!$v.defaultState.phone.phoneValid && $v.defaultState.phone.$model">
                            Некорректно введен номер
                        </span>
                        <span class="errorMsg" v-if="!$v.defaultState.phone.required">
                        Необходимо заполнить поле
                        </span>
                    </div>
                    <div>
                        <label for="gender">Пол</label>
                        <input id="gender" type="text" v-model="defaultState.gender">
                    </div>
                    <div>
                        <label for="groupClients">Группа клиентов<span class="red">*</span></label>        
                        <select id= "groupClients" multiple v-model="defaultState.groupClients" size="3">
                            <option value="vip">VIP</option>
                            <option value="problem">Проблемные</option>
                            <option value="omc">ОМС</option>
                        </select>  
                        <span class="errorMsg" v-if="$v.defaultState.groupClients.$invalid && $v.defaultState.groupClients.$model">
                            Необходимо выбрать группу
                        </span>
                    </div>
                    <div>
                        <label for="doctor">Лечащий врач</label>
                        <select v-model="defaultState.doctor">
                            <option value="null" disabled selected>Выберите врача</option>
                            <option value="Иванов">Иванов</option>
                            <option value="Захаров">Захаров</option>
                            <option value="Чернышева">Чернышева</option>
                        </select>
                    </div>
                    <div>
                        <label>Не&nbsp;отправлять СМС</label>
                        <input id="sendSms" type="checkbox" v-model="defaultState.sendSms" class="customCheckbox">
                        <label for="sendSms"></label>
                        <span></span>
                    </div>
                    <div style="max-width: 310px;
                                margin-top: 15px;">
                    <span class="red">*</span> 
                    <span>Поле обязательное для заполнения</span>
                    </div>  
                </div>
                <div>
                    <h2>Адрес:</h2>   
                    <div>
                        <label for="index">Индекс</label>
                        <input id="index" type="text" v-model="defaultState.index">
                    </div>
                    <div>
                        <label for="country">Страна</label>
                        <input id="country" type="text" v-model="defaultState.country">
                    </div>
                    <div>
                        <label for="region">Область</label>
                        <input id="region" type="text" v-model="defaultState.region">
                    </div>
                    <div>
                        <label for="city">Город<span class="red">*</span></label>
                        <input id="city" type="text" v-model="defaultState.city" placeholder="Москва">
                        <span class="errorMsg" v-if="!$v.defaultState.city.required">
                                Необходимо заполнить поле
                        </span>
                        <span class="errorMsg" v-if="!$v.defaultState.city.valid && $v.defaultState.city.$model">
                                Недопустимые символы
                        </span>
                    </div>
                    <div>
                        <label for="street">Улица</label>
                        <input id="street" type="text" v-model="defaultState.street">
                    </div>
                    <div>
                        <label for="house">Дом</label>
                        <input id="house" type="text" v-model="defaultState.house">
                    </div>
                
                    <h2>Паспорт:</h2>  
                    <div>
                        <label for="typeDoc">Тип документа<span class="red">*</span></label>
                        <select id="typeDoc" v-model="defaultState.typeDoc">
                            <option disabled value="null">Выберите тип документа</option>
                            <option selected value="Паспорт">Паспорт</option>
                            <option value="Свидетельство о рождении"> Свидетельство о рождении</option>
                            <option value="Вод. удостоверение">Вод. удостоверение</option>
                        </select>
                        <span class="errorMsg" v-if="!$v.defaultState.typeDoc.required">
                                Необходимо выбрать документ
                        </span>
                    </div>
                    <div>
                        <label for="series">Серия</label>
                        <input type="text" v-model="defaultState.series">
                    </div>
                    <div>
                        <label for="number">Номер</label>
                        <input type="text" v-model="defaultState.number">
                    </div>
                    <div>
                        <label for="whoIssued">Кем выдан </label>
                        <input type="text" v-model="defaultState.whoIssued">
                    </div>
                    <div>
                        <label for="dateIssued">Дата выдачи<span class="red">*</span></label>
                        <input id="dateIssued" type="date" v-model="defaultState.dateIssued" @blur="$v.defaultState.dateIssued.$touch()">
                        <span class="errorMsg" v-if="!$v.defaultState.dateIssued.valid && $v.defaultState.dateIssued.$model">
                            Дата выдачи не может быть больше текущей
                        </span>
                        <span class="errorMsg" v-if="!$v.defaultState.dateIssued.required">
                        Необходимо заполнить поле
                        </span>
                    </div>  
                </div> 
            </div>
            <button type="submit" 
                    :disabled="$v.$invalid" 
                    @click="successfulIsTrue = !successfulIsTrue"              
            >Отправить
            </button>
            
            <!-- <button type="submit"
                    @click="successfulIsTrue = !successfulIsTrue"         
            > Отправить
            </button> 
            -->
                        
        </div> 
        </transition>  
            
        <transition name="slide">
            <div class="msgSuccessful" v-if="successfulIsTrue">
            <span>
                Новый клиент успешно создан
            </span>
            
            <button class="closeBtn" @click="successfulIsTrue = !successfulIsTrue">Закрыть</button>
            <div class="close" @click="successfulIsTrue = !successfulIsTrue">&times;</div>
            
            </div> 
        </transition>     
    </form>
    
</template>

<script>
import { required, minValue } from 'vuelidate/lib/validators';

export default {
    name: 'App', 
    data() {
        return {
            defaultState: {
                surname: null,
                name: null,
                secondName: null,
                dateBirth: null,
                phone: null,
                gender: null,
                groupClients: [],
                doctor: null,
                sendSms: false,

                index: null,
                country: null,
                region: null,
                city: null,
                street: null,
                house: null,

                typeDoc: null,
                series: null,
                number: null,
                whoIssued: null,
                dateIssued: null,

                newState: null,
            },
            successfulIsTrue: false,
        }
    },

    validations: {
        defaultState: {
            surname: {
                required,
                valid: val => /^[a-zA-Zа-яёА-ЯЁ\s\-]+$/.test(val),
            },
            name: {
                required,
                valid: val => /^[a-zA-Zа-яёА-ЯЁ\s\-]+$/.test(val),
            },
            dateBirth: {
                required,
                valid: val => new Date(val) < new Date(),
            },
            phone: {
                required,
                phoneValid: val => /^((8|\+7)[\- ]?)?(\(?\d{3}\)?[\- ]?)?[\d\- ]{7,10}$/.test(val),
            },
            groupClients: {
                required,    
            },
            city: {
                required,
                valid: val => /^[a-zA-Zа-яёА-ЯЁ\s\-]+$/.test(val),
            },
            typeDoc: {
                required,
            },
            dateIssued: {
                required,
                valid: val => new Date(val) < new Date(),
            },
        }
    },
    methods: {
        someAction() {
            
        },

        action() {
            this.defaultState = Object.assign({}, this.newState);
        },

        clear(){
            
        },
    },
    created: function () {
        this.newState = Object.assign({}, this.defaultState);
        
    },
}
</script>
      
<style>

* {
    margin: 0;
    padding: 0;
}

#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  max-width: 1920px;
  margin: 0 auto;
}

body {
    background-color: #ea3d1f;
    margin: 0!important;
}

.container {
    display: flex;
    flex-direction: row;
    justify-content: space-evenly;
    padding-top: 10px;
}

.container > div {
    display: flex;
    flex-direction: column;
    width: 35%;
    max-width: 650px;
    background-color: rgb(117,30,13, 0.9);
    padding: 10px 20px;
    border-radius: 10px;
    color: wheat;
    font-size: 20px;
    
}

.container > div > div {
    display: flex;
    justify-content: space-between;
    margin-bottom: 5px;
    flex-wrap: wrap;
    box-shadow: inset 0px 0px 10px rgba(0,0,0,0.5);
    padding: 8px 10px;
    border-radius: 5px;
}

h2 {
    margin-bottom: 5px;
}

.red {
    color: red;
}

label {
    margin: auto 0;
    width: 25%;    
    text-align: right;
    margin-right: 10px;
}

input, select {
    padding: 10px 10px;
    border-radius: 10px;
    border: 1px solid black;
    width: 65%;
}

input[type='checkbox'] {
    margin: auto;   
}

select {
    box-sizing: content-box;    
}

select[multiple='multiple'] {
    overflow-y: hidden;    
}

option[disabled] { 
    display: none; 
} 

input:focus, select:focus {
    background-color: cornsilk;
    outline: none;
}

option {
    padding: 3px 3px;
}

.customCheckbox {
    position: absolute;
    z-index: -1;
    opacity: 0;    
}

.customCheckbox+label {
  display: inline-flex;
  align-items: center;
  user-select: none;
  flex-direction: column;
  margin: auto;
}
.customCheckbox+label::before {
  content: '';
  display: inline-block;
  width: 1.5em;
  height: 1.5em;
  flex-shrink: 0;
  flex-grow: 0;
  border: 1px solid #adb5bd;
  border-radius: 0.25em;
  background-repeat: no-repeat;
  background-position: center center;
  background-size: 50% 50%;
}

.customCheckbox:checked+label::before {
  border-color: #d35426;
  background-color: #d35426;
  background-image: url("data:image/svg+xml,%3csvg xmlns='http://www.w3.org/2000/svg' viewBox='0 0 8 8'%3e%3cpath fill='%23fff' d='M6.564.75l-3.59 3.612-1.538-1.55L0 4.26 2.974 7.25 8 2.193z'/%3e%3c/svg%3e");
}

/* стили при наведении курсора на checkbox */
.customCheckbox:not(:disabled):not(:checked)+label:hover::before {
  border-color: #b3d7ff;
}
/* стили для активного состояния чекбокса (при нажатии на него) */
.customCheckbox:not(:disabled):active+label::before {
  background-color: #47494b;
  border-color: #b3d7ff;
}
/* стили для чекбокса, находящегося в фокусе */
.customCheckbox:focus+label::before {
  box-shadow: 0 0 0 0.2rem rgba(0, 123, 255, 0.25);
}
/* стили для чекбокса, находящегося в фокусе и не находящегося в состоянии checked */
.customCheckbox:focus:not(:checked)+label::before {
  border-color: #80bdff;
}
/* стили для чекбокса, находящегося в состоянии disabled */
.customCheckbox:disabled+label::before {
  background-color: #e9ecef;
}

.errorMsg {
    color: red;
    flex-grow: 1;
    text-align: right;
    padding-top: 3px;
}

button {
    margin-top: 30px;
    display: block;
    background-color: #fc9202;
    color: #fffcff;
    padding: 10px;
    margin: 25px auto;
    border-radius: 10px;
    box-shadow: 3px 3px 5px 0px rgba(0,0,0,0.75);
    border: none;
    outline: none;
}

button[disabled] {
    opacity: .7;
}

button:active {
    border: none;
    box-shadow: none;
}

button:hover {
    background-color: #fcae0c;
}

.msgSuccessful {
    text-align: center;
    align-items: center;
    display: flex;
    width: 400px;
    height: 300px;
    background-color: yellowgreen;
    border-radius: 15px;
    position: absolute;
    top: 0;
    left: 0;
    right: 0;
    bottom: 0;
    margin: auto;
    z-index: 3;
}

.msgSuccessful span {
    width: 100%;
    margin: auto;
    font-size: 25px;
}

.closeBtn {
    position: absolute;
    font-size: 20px;
    bottom: 0;
    left: 0;
    right: 0;
    margin-bottom: 20px;
}

.close {
    position: absolute;
    right: -22px;
    top: -22px;
    width: 44px;
    height: 44px;
    opacity: 0.3;
    font-size: 38px;
    background-color: white;
    border-radius: 50%;
    color: red;
    opacity: 1;
    padding: 0px;
    cursor: pointer;
    box-shadow: 3px 3px 5px 0px rgba(0,0,0,0.75);
}

.close:hover {
    background-color: blanchedalmond;
}

.close:active {
    box-shadow: none;
}

.slide-enter-active, .slide-leave-active {
    transition: all 1s ease;
    
}
.slide-enter, .slide-leave-to {
    transform: translateY(-100vh);
}

.appearance-enter-active, .appearance-leave-active {
    transition: all 1s ease;  
}

.appearance-enter, .appearance-leave-to {
    opacity: 0;
}

@media screen and (max-width: 1050px) {
    .container {
        flex-direction: column;
    }

    .container > div {
        width: 70%;
        margin: 20px auto;
    }   
}

@media screen and (max-width: 500px) {
    label {
        width: 100%;
        text-align: left;
    }

    input, select {
        width: -webkit-fill-available;
    }

    .msgSuccessful {
        width: 75%;
        height: 250px;
        padding: 5px;
    }    
}

</style>
