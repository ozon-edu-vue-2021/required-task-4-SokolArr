<template>
  <div class="form">
    <div class="personal-data" style="display: flex; flex-direction: column">
      <h2>Личные данные</h2>
      <div class="string one">
        <!--      ++++++++++++++++++++++++-->
        <div class="input-wrapper second-name">
          Фамилия
          <input class="myInput second-name" type="text" placeholder="Иванов" v-model="secondName" />
        </div>
        <!--      ++++++++++++++++++++++++-->
        <div class="input-wrapper first-name">
          Имя
          <input class="myInput first-name" type="text" placeholder="Иван" v-model="firstName" />
        </div>
        <!--      ++++++++++++++++++++++++-->
        <div class="input-wrapper patronymic-name">
          Отчество
          <input class="myInput patronymic-name" type="text" placeholder="Иванович" v-model="patronymicName" />
        </div>
        <!--      ++++++++++++++++++++++++-->
      </div>
      <div class="string two">
        <div class="birthday" style="display: flex; flex-direction: column;width: fit-content">
          Дата рождения
          <input class="myInput birthday" placeholder="дд.мм.гггг" v-model="birthdayText" />
        </div>
      </div>
      <div class="string three">
        <div class="email" style="display: flex; flex-direction: column;width: fit-content">
          E-mail
          <input class="myInput email" placeholder="example@email.com" v-model="emailText" />
        </div>
      </div>
    </div>


    <div class="sex" style="display: flex; flex-direction: column;margin-top: 10px">
      <h2>Пол</h2>
      <div class="male-female-wrapper">
        <input type="radio" value="Мужской" id="radio-male" class="radio" v-model="sexText" />
        <label for="radio-male" class="label-radio">Мужской</label>
        <input type="radio" value="Женский" id="radio-female" class="radio" v-model="sexText" />
        <label for="radio-female" class="label-radio">Женский</label>
      </div>
    </div>


    <div class="passport-data" style="display: flex; flex-direction: column;margin-top: 10px">
      <h2>Пасспортные данные</h2>
      <div class="name citizenship" style="display: flex;flex-direction: column; width: 300px">
        Гражданство
        <input class="myInput" v-model="citizenshipText" />
      </div>

      <div
        class="string four"
        v-if="citizenshipText==='Россия'"
      >
        <div class="passport serial">
          Серия пасспорта
          <input class="myInput passSerial" placeholder="1234" v-model="passportSerial" />
        </div>
        <div class="passport number">
          Номер пасспорта
          <input class="myInput passNumber" placeholder="567890" v-model="passportNumber" />
        </div>
        <div class="passport get-date">
          Дата выдачи
          <input class="myInput dateGet" placeholder="дд.мм.гггг" v-model="dateGet" />
        </div>
      </div>

      <div v-else>
        <div class="string four">
          <div class="input-wrapper second-name-latin" style="width: 320px">
            Surname in Latin
            <input class="myInput second-name-latin" placeholder="Ivanov" v-model="secondNameLatin" />
          </div>
          <div class="input-wrapper first-name-latin" style="width: 320px">
            Name in Latin
            <input class="myInput first-name-latin" placeholder="Ivan" v-model="firstNameLatin" />
          </div>
        </div>
        <div class="string four2">
          <div class="input-wrapper passport number-latin">
            Passport number
            <input class="myInput passSerialLatin" placeholder="" v-model="passportNumberLatin" />
          </div>
          <div class="input-wrapper passport country-get">
            Country of issue
            <input class="myInput countryGet" placeholder="" v-model="countryGet" />
          </div>
          <div class="input-wrapper passport type">
            Passport type
            <input class="myInput passType" placeholder="" v-model="passportType" />
          </div>
        </div>
      </div>
    </div>

    <div class="personal-change" style="display: flex; flex-direction: column;margin-top: 10px">
      <h3>Меняли ли фамилию или имя?</h3>
      <div class="line five">
        <input type="radio" value="false" id="radio-no" class="radio" v-model="isChanged" />
        <label for="radio-no" class="label-radio">Нет</label>
        <input type="radio" value="true" id="radio-yes" class="radio" v-model="isChanged" />
        <label for="radio-yes" class="label-radio">Да</label>
      </div>
      <div class="isChanged" v-show="isChanged === 'true'">
        <div class="string six">
          <!--      ++++++++++++++++++++++++-->
          <div class="input-wrapper second-name" style="width: 320px">
            Предыдущая фамилия
            <input class="myInput second-name" placeholder="Иванов" v-model="secondNameChanged" />
          </div>
          <!--      ++++++++++++++++++++++++-->
          <div class="input-wrapper first-name" style="width: 320px">
            Предыдущее имя
            <input class="myInput first-name" placeholder="Иван" v-model="firstNameChanged" />
          </div>
          <!--      ++++++++++++++++++++++++-->
        </div>
      </div>
    </div>
    <div
      v-show="firstName && secondName && patronymicName"
      style="display: flex; justify-content: space-between;align-items: center;"
    >
      <div style="margin-right: 20px;">
        Я, {{ secondName }} {{ firstName }} {{ patronymicName }} соглашаюсь отправить форму
      </div>

      <input type="submit" style="height: 30px" />
    </div>
  </div>
</template>

<script>
import citizenships from "@/assets/data/citizenships.json";

export default {
  data() {
    return {
      citizenshipsData: [],
      firstName: "",
      firstNameChanged: "",
      firstNameLatin: "",
      secondName: "",
      secondNameChanged: "",
      secondNameLatin: "",
      patronymicName: "",
      birthdayText: "",
      emailText: "",
      citizenshipText: "Россия",
      passportSerial: "",
      passportNumber: "",
      passportNumberLatin: "",
      passportType: "",
      countryGet: "",
      dateGet: "",
      sexText: "",
      isChanged: "false"
    };
  },
  mounted() {
    this.citizenshipsData = citizenships;
  },
  methods: {},
  computed: {}
};
</script>

<style scoped>
.form {
  box-sizing: border-box;
  background: white;
  border: 1px solid #aeb7e6;
  border-radius: 6px;
  padding: 20px;
  width: 700px;
  height: fit-content;
  margin-left: auto;
  margin-right: auto;
  box-shadow: 0px 0px 25px 6px rgba(0, 23, 191, 0.1);
}

.string {
  display: flex;
  flex-direction: row;
  justify-content: space-between;
}

input {
  margin-top: 5px;
  margin-bottom: 10px;
  margin-right: 5px;
}

.myInput {
  width: auto;
  font-size: 18px;
  padding: 6px 0 4px 10px;
  border: 2px solid #cecece;
  background: #f8faff;
  border-radius: 6px;
}

.input-wrapper {
  display: flex;
  flex-direction: column;
}

.label-radio {
  margin-right: 20px;
}

h2,
h3 {
  margin-bottom: 8px;
}

.line {
  margin-bottom: 5px;
  margin-top: 5px;
}

.string.six {
  display: flex;
}

</style>
