<template>
  <form @submit.prevent="someAction()">
    <div>   
        <div>
        <label for="surname">Фамилия*</label>
        <input id="surname" type="text" v-model="surname">
        <span class="errorMsg" v-if="!$v.surname.valid">
            В фамилии недопустимые символы
        </span>
        </div>
        <div>
            <label for="name">Имя*</label>
            <input id="name" type="text" v-model="name">
            <span class="errorMsg" v-if="!$v.name.valid">
                    В имени недопустимые символы
            </span>
        </div>
        <div>
            <label for="secondName">Отчество</label>
            <input id="secondName" type="text" v-model="secondName">

        </div>
        <div>
            <label for="dateBirth">Дата рождения*</label>
            <input id="dateBirth" type="date" v-model="dateBirth" @blur="$v.dateBirth.$touch()">
            <span class="errorMsg" v-if="!$v.dateBirth.valid && $v.dateBirth.$model">
                Дата рождения не может быть больше текущей
            </span>
        </div>
        <div>
            <label for="phone">Номер телефона*</label>
            <input id="phone" type="tel" v-model="phone">
            <span class="errorMsg" v-if="!$v.phone.phoneValid && $v.phone.$model">
                Некорректно введен номер
            </span>
        </div>
        <div>
            <label for="gender">Пол</label>
            <input id="gender" type="text" v-model="gender">
        </div>
        <div>
            <label for="groupClients">Группа клиентов</label>            
            <select id="groupClients" required multiple v-model="groupClients" size="3">
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
            <input id="sendSms" type="checkbox" v-model="sendSms">
            <label for="sendSms">Не отправлять СМС.</label>
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
            <label for="city">Город*</label>
            <input id="city" type="text" v-model="city">
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
    </div>
    <div>
        <h2>Паспорт:</h2>  
        <div>
            <label for="typeDoc">Тип документа*.</label>
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
            <label for="dateIssued">Дата выдачи*</label>
            <input id="dateIssued" type="date" v-model="dateIssued" @blur="$v.dateIssued.$touch()">
            <span class="errorMsg" v-if="!$v.dateIssued.valid && $v.dateIssued.$model">
                Дата выдачи не может быть больше текущей
            </span>
        </div>  
    </div> 
    <button type="submit" :disabled="$v.$invalid">Отправить</button>
  </form>
  
</template>

<script>
import { required, minValue } from 'vuelidate/lib/validators';

export default {
    name: 'App',
    data() {
        return {
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
            valid: val => moment(val) < new Date(),
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
            valid: val => moment(val) < new Date(),
        },
    },
    methods: {
        someAction() {
            alert('Форма отправлена');
        },
    },
}
</script>
      
<style scoped>

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

.errorMsg {
    color: red;
}
</style>
