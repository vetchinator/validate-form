<template>
    <form @submit.prevent="someAction()" @submit="action">
        <transition name="scale" appear>  
        <div v-if="!successfulIsTrue">
            <div class="container">
                <div> 
                    <h2>Данные</h2>  
                    <div>
                    <label for="surname">Фамилия<span class="red">*</span></label>
                    <input id="surname" type="text" v-model="surname" placeholder="Иванов">
                    <p class="errorMsg" v-if="!$v.surname.valid">
                        В фамилии недопустимые символы
                    </p>
                    </div>
                    <div>
                        <label for="name">Имя<span class="red">*</span></label>
                        <input id="name" type="text" v-model="name" placeholder="Иван">
                        <span class="errorMsg" v-if="!$v.name.valid">
                                В имени недопустимые символы
                        </span>
                    </div>
                    <div>
                        <label for="secondName">Отчество</label>
                        <input id="secondName" type="text" v-model="secondName">

                    </div>
                    <div>
                        <label for="dateBirth">Дата рождения<span class="red">*</span></label>
                        <input id="dateBirth" type="date" v-model="dateBirth" @blur="$v.dateBirth.$touch()">
                        <span class="errorMsg" v-if="!$v.dateBirth.valid && $v.dateBirth.$model">
                            Дата рождения не может быть больше текущей
                        </span>
                    </div>
                    <div>
                        <label for="phone">Номер телефона<span class="red">*</span></label>
                        <input id="phone" type="tel" v-model="phone" placeholder="790000000">
                        <span class="errorMsg" v-if="!$v.phone.phoneValid && $v.phone.$model">
                            Некорректно введен номер
                        </span>
                    </div>
                    <div>
                        <label for="gender">Пол</label>
                        <input id="gender" type="text" v-model="gender">
                    </div>
                    <div>
                        <label for="groupClients">Группа клиентов<span class="red">*</span></label>        
                        <select id="groupClients" multiple v-model="groupClients" size="3">
                            <option value="vip">VIP</option>
                            <option value="problem">Проблемные</option>
                            <option value="omc">ОМС</option>
                        </select>  
                        <span class="errorMsg" v-if="$v.groupClients.$invalid && $v.groupClients.$model">
                            Необходимо выбрать группу
                        </span>
                    </div>
                    <div>
                        <label for="doctor">Лечащий врач</label>
                        <select v-model="doctor">
                            <option disabled>Выберите врача</option>
                            <option selected value="Иванов">Иванов</option>
                            <option value="Захаров">Захаров</option>
                            <option value="Чернышева">Чернышева</option>
                        </select>
                    </div>
                    <div>
                        <label for="sendSms">Не&nbsp;отправлять СМС</label>
                        <input id="sendSms" type="checkbox" v-model="sendSms">
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
                        <input id="index" type="text" v-model="index">
                    </div>
                    <div>
                        <label for="country">Страна</label>
                        <input id="country" type="text" v-model="country">
                    </div>
                    <div>
                        <label for="region">Область</label>
                        <input id="region" type="text" v-model="region">
                    </div>
                    <div>
                        <label for="city">Город<span class="red">*</span></label>
                        <input id="city" type="text" v-model="city" placeholder="Москва">
                        <span class="errorMsg" v-if="!$v.city.valid && $v.city.$model">
                                Недопустимые символы
                        </span>
                    </div>
                    <div>
                        <label for="street">Улица</label>
                        <input id="street" type="text" v-model="street">
                    </div>
                    <div>
                        <label for="house">Дом</label>
                        <input id="house" type="text" v-model="house">
                    </div>
                
                    <h2>Паспорт:</h2>  
                    <div>
                        <label for="typeDoc">Тип документа<span class="red">*</span></label>
                        <select id="typeDoc" v-model="typeDoc">
                            <option disabled>Выберите тип документа</option>
                            <option selected value="Паспорт">Паспорт</option>
                            <option value=" Свидетельство о рождении"> Свидетельство о рождении</option>
                            <option value="Вод. удостоверение">Вод. удостоверение</option>
                        </select>
                    </div>
                    <div>
                        <label for="series">Серия </label>
                        <input type="text">
                    </div>
                    <div>
                        <label for="number">Номер</label>
                        <input type="text">
                    </div>
                    <div>
                        <label for="whoIssued">Кем выдан </label>
                        <input type="text">
                    </div>
                    <div>
                        <label for="dateIssued">Дата выдачи<span class="red">*</span></label>
                        <input id="dateIssued" type="date" v-model="dateIssued" @blur="$v.dateIssued.$touch()">
                        <span class="errorMsg" v-if="!$v.dateIssued.valid && $v.dateIssued.$model">
                            Дата выдачи не может быть больше текущей
                        </span>
                    </div>  
                </div> 
            </div>
            <button type="submit" 
                    :disabled="$v.$invalid"                
            >Отправить
            </button>
            <button  type="submit"
                    @click="successfulIsTrue = !successfulIsTrue"
            > Отправить
            </button>
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
            successfulIsTrue: false,
            surname: null,
            name: null,
            secondName: null,
            dateBirth: null,
            phone: null,
            gender: null,
            groupClients: [],
            doctor: "Иванов",
            sendSms: false,

            index: null,
            country: null,
            region: null,
            city: null,
            street: null,
            house: null,

            typeDoc: 'Паспорт',
            series: null,
            number: null,
            whoIssued: null,
            dateIssued: null,
        };
    },

    validations: {
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
        doctor: {
            required,    
        },
        city: {
            required,
            valid: val => /^[a-zA-Zа-яёА-ЯЁ\s\-]+$/.test(val),
        },
        dateIssued: {
            required,
            valid: val => new Date(val) < new Date(),
        },
    },
    methods: {
        someAction() {
            
        },
        action() {
            console.log('Клиент создан');
        }
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
    padding-top: 30px;
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
    margin-bottom: 10px;
    flex-wrap: wrap;
}

h2 {
    margin-bottom: 20px;
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
    padding: 5px 10px;
    border-radius: 10px;
    border: 1px solid black;
    overflow-y: hidden;
    width: 65%;
}

select {
    box-sizing: content-box;    
}

input:focus, select:focus {
    background-color: cornsilk;
    outline: none;
}

option {
    padding: 3px;
}

.errorMsg {
    color: red;
    flex-grow: 1;
    text-align: right;
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
    height: 200px;
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
    transition: all .5s ease;
    
}
.slide-enter, .slide-leave-to {
    transform: translateY(-100vh);
}

.scale-enter-active, .slide-leave-active {
    transition: all 1s ease;
}

.scale-enter  {
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
        width: 100%;
    }

      
}

</style>
