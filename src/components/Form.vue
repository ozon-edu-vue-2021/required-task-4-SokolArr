<template>
  <div class="form">
    <div class="personal-data" style="display: flex; flex-direction: column">
      <h2>Личные данные</h2>
      <div class="string one">
        <!--      ++++++++++++++++++++++++-->
        <div class="input-wrapper second-name">
          Фамилия
          <input
            class="myInput second-name"
            type="text"
            placeholder="Иванов"
            v-model="secondName"
          />
        </div>
        <!--      ++++++++++++++++++++++++-->
        <div class="input-wrapper first-name">
          Имя
          <input
            class="myInput first-name"
            type="text"
            placeholder="Иван"
            v-model="firstName"
          />
        </div>
        <!--      ++++++++++++++++++++++++-->
        <div class="input-wrapper patronymic-name">
          Отчество
          <input
            class="myInput patronymic-name"
            type="text"
            placeholder="Иванович"
            v-model="patronymicName"
          />
        </div>
        <!--      ++++++++++++++++++++++++-->
      </div>
      <div class="string two">
        <div
          class="birthday"
          style="display: flex; flex-direction: column; width: fit-content"
        >
          Дата рождения
          <input
            class="myInput birthday"
            placeholder="дд.мм.гггг"
            v-model="birthdayText"
          />
        </div>
      </div>
      <div class="string three">
        <div
          class="email"
          style="display: flex; flex-direction: column; width: fit-content"
        >
          E-mail
          <input
            class="myInput email"
            placeholder="example@email.com"
            v-model="emailText"
          />
        </div>
      </div>
    </div>

    <div
      class="sex"
      style="display: flex; flex-direction: column; margin-top: 10px"
    >
      <h2>Пол</h2>
      <div class="male-female-wrapper">
        <input
          type="radio"
          value="Мужской"
          id="radio-male"
          class="radio"
          v-model="sexText"
        />
        <label for="radio-male" class="label-radio">Мужской</label>
        <input
          type="radio"
          value="Женский"
          id="radio-female"
          class="radio"
          v-model="sexText"
        />
        <label for="radio-female" class="label-radio">Женский</label>
      </div>
    </div>

    <div
      class="passport-data"
      style="display: flex; flex-direction: column; margin-top: 10px"
    >
      <h2>Пасспортные данные</h2>
      Гражданство
      <div
        class="name citizenship"
        style="display: flex; flex-direction: column; width: 300px"
        v-click-outside="hideDropdownCitizenship"
      >
        <div>

        </div>
        <div
          class="dropdown-wrapper"
          @click="isDropdownCitizenshipOpen=true"
        >
          <input
            class="myInput dropdown citizenship"
            v-model="citizenshipText"
            @focus="isDropdownCitizenshipOpen=true"
            ref="citizenship"
            style="border: 0px; margin: 0"
            @input="inputCitizenshipHandler(citizenshipText)"
          />
          <div class="triangle"></div>

        </div>

        <div
          class="dropdown"
          v-if="isDropdownCitizenshipOpen"
        >
          <ul class="dropdown-content">
            <li
              v-for="citizenship in filteredCitizenship"
              :key="citizenship.id"
              class="li-in-content"
              @click="clickHandlerOnCitizenship(citizenship)"
            >
              {{citizenship.nationality}}
            </li>
          </ul>
        </div>

      </div>



      <div class="string four" v-if="citizenshipText === 'Россия' || citizenshipText === 'Russia'">
        <div class="passport serial">
          Серия пасспорта
          <input
            class="myInput passSerial"
            placeholder="1234"
            v-model="passportSerial"
          />
        </div>
        <div class="passport number">
          Номер пасспорта
          <input
            class="myInput passNumber"
            placeholder="567890"
            v-model="passportNumber"
          />
        </div>
        <div class="passport get-date">
          Дата выдачи
          <input
            class="myInput dateGet"
            placeholder="дд.мм.гггг"
            v-model="dateGet"
          />
        </div>
      </div>

      <div v-else>
        <div class="string four">
          <div class="input-wrapper second-name-latin" style="width: 320px">
            Surname in Latin
            <input
              class="myInput second-name-latin"
              placeholder="Ivanov"
              v-model="secondNameLatin"
            />
          </div>
          <div class="input-wrapper first-name-latin" style="width: 320px">
            Name in Latin
            <input
              class="myInput first-name-latin"
              placeholder="Ivan"
              v-model="firstNameLatin"
            />
          </div>
        </div>
        <div class="string four2">
          <div class="input-wrapper passport number-latin">
            Passport number
            <input
              class="myInput passSerialLatin"
              placeholder=""
              v-model="passportNumberLatin"
            />
          </div>
          <div class="input-wrapper passport country-get" v-click-outside="hideDropdownCountryGet">
            Country of issue

            <div
              class="dropdown-wrapper"
              @click="isDropdownCountryGetOpen=true"
            >
              <input
                class="myInput dropdown countryGet"
                placeholder=""
                v-model="countryGet"
                @focus="isDropdownCountryGetOpen=true"
              />

              <div class="triangle"></div>
            </div>

            <div
              class="dropdown"
              v-if="isDropdownCountryGetOpen"
            >
              <ul class="dropdown-content">
                <li
                  v-for="citizen in citizenshipsData"
                  :key="citizen.id"
                  class="li-in-content"
                  @click="clickHandlerOnCountryGetOpen(citizen.flag)"
                >
                  {{citizen.flag}}
                </li>
              </ul>
            </div>

          </div>

          <div
            class="input-wrapper passport type"
            v-click-outside="hideDropdownPassType"
          >
            Passport type

            <div
              class="dropdown-wrapper"
              @click="isDropdownPassTypeOpen=true"
            >
              <input
                class="myInput dropdown passType"
                placeholder=""
                v-model="passportTypeText"
                @focus="isDropdownPassTypeOpen=true"
              />
              <div class="triangle"></div>
            </div>

            <div
              class="dropdown"
              v-if="isDropdownPassTypeOpen"
            >
              <ul class="dropdown-content">
                <li
                  v-for="passport in passportTypesData"
                  :key="passport.id"
                   class="li-in-content"
                  @click="clickHandlerOnPassportType(passport.type)"
                >
                  {{passport.type}}
                </li>
              </ul>
            </div>

          </div>
        </div>
      </div>
    </div>

    <div
      class="personal-change"
      style="display: flex; flex-direction: column; margin-top: 10px"
    >
      <h3>Меняли ли фамилию или имя?</h3>
      <div class="line five">
        <input
          type="radio"
          value="false"
          id="radio-no"
          class="radio"
          v-model="isChanged"
        />
        <label for="radio-no" class="label-radio">Нет</label>
        <input
          type="radio"
          value="true"
          id="radio-yes"
          class="radio"
          v-model="isChanged"
        />
        <label for="radio-yes" class="label-radio">Да</label>
      </div>
      <div class="isChanged" v-show="isChanged === 'true'">
        <div class="string six">
          <!--      ++++++++++++++++++++++++-->
          <div class="input-wrapper second-name" style="width: 320px">
            Предыдущая фамилия
            <input
              class="myInput second-name"
              placeholder="Иванов"
              v-model="secondNameChanged"
            />
          </div>
          <!--      ++++++++++++++++++++++++-->
          <div class="input-wrapper first-name" style="width: 320px">
            Предыдущее имя
            <input
              class="myInput first-name"
              placeholder="Иван"
              v-model="firstNameChanged"
            />
          </div>
          <!--      ++++++++++++++++++++++++-->
        </div>
      </div>
    </div>
    <div
      v-show="firstName && secondName && patronymicName"
      style="display: flex; justify-content: space-between; align-items: center"
    >
      <div style="margin-right: 20px">
        Я, {{ secondName }} {{ firstName }} {{ patronymicName }} соглашаюсь
        отправить форму
      </div>

      <input type="submit" @click="formSubmit" style="height: 30px" />

    </div>
  </div>
</template>

<script>
import citizenships from "@/assets/data/citizenships.json";
import passportTypes from "@/assets/data/passport-types.json";
import {debounce} from "@/helpers/debounce";
import ClickOutside from "vue-click-outside";

export default {
  directives:{
    ClickOutside
  },
  data() {
    return {
      citizenshipsData: [],
      filteredCitizenship:[],
      passportTypesData:[],
      citizenshipsArr:[
        {country:"Россия"},
        {country:"Другое"},
      ],
      submitDataRus:{},
      submitDataInt:{},
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
      passportTypeText: "",
      countryGet: "",
      dateGet: "",
      sexText: "",
      isChanged: "false",
      isDropdownPassTypeOpen: false,
      isDropdownCountryGetOpen:false,
      isDropdownCitizenshipOpen:false,
      debouncedSearch: null,
    };
  },
  created() {
    this.debouncedSearch = debounce(this.filterCitizenships,500);
  },
  mounted() {
    this.citizenshipsData = citizenships;
    this.passportTypesData = passportTypes;
  },
  methods: {
    hideDropdownPassType(){
      this.isDropdownPassTypeOpen=false;
    },
    hideDropdownCountryGet(){
      this.isDropdownCountryGetOpen = false;
    },
    hideDropdownCitizenship(){
      this.isDropdownCitizenshipOpen = false;
    },
    clickHandlerOnPassportType(type){
      this.passportTypeText = type;
      this.isDropdownPassTypeOpen = false;
    },
    clickHandlerOnCountryGetOpen(country){
      this.countryGet = country;
      this.isDropdownCountryGetOpen = false;
    },
    clickHandlerOnCitizenship(citizenship){
      if(citizenship){
        this.citizenshipText = citizenship.nationality;
        this.countryGet = citizenship.flag;
      }
      else {
        this.citizenshipText = "";
        let el = this.$refs.citizenship;
        el.focus();
      };
      this.isDropdownCitizenshipOpen = false;
    },
    inputCitizenshipHandler(citizenshipText){

      //this.filterCitizenships(citizenshipText);

      this.debouncedSearch(citizenshipText);

      this.isDropdownCitizenshipOpen = true;
    },
    filterCitizenships(element){
      console.log("Searching " + element + " in citizenships...")

      // this.filteredCitizenship = citizenshipData.map(el => {
      //   if ((element === el.nationality)||(el.nationality.includes(element))) {
      //     return el;
      //   }else return "";
      // })

      this.filteredCitizenship = this.citizenshipsData.filter(el => (element === el.nationality)||(el.nationality.includes(element)))

      //console.log(this.filteredCitizenship);
    },
    formSubmit: function() {
      let json;
      if (this.citizenshipText === "Россия" || this.citizenshipText === "Russia") {
        this.submitDataRus = {
          firstname: this.firstName,
          lastname: this.secondName,
          secondname: this.patronymicName,
          birthday: this.birthdayText,
          email: this.emailText,
          sex: this.sexText,
          citizenship: this.citizenshipText,

          passport_serial: this.passportSerial,
          passport_number: this.passportNumber,
          date_of_issue: this.dateGet,
        };

        if(this.isChanged === "true"){
          this.submitDataRus.is_changed_bio = "true";
          this.submitDataRus.previos_lastname =this.secondNameChanged;
          this.submitDataRus.previos_firstname =this.firstNameChanged;
        } else {this.submitDataRus.is_changed_bio = false };

        json = JSON.stringify(this.submitDataRus);
      } else {
        this.submitDataInt = {
          firstname: this.firstName,
          lastname: this.secondName,
          secondname: this.patronymicName,
          birthday: this.birthdayText,
          email: this.emailText,
          sex: this.sexText,
          citizenship: this.citizenshipText,

          surname_latin: this.secondNameLatin,
          name_latin: this.firstNameLatin,
          passport_number: this.passportNumberLatin,
          country_of_issue: this.countryGet,
          passport_type: this.passportTypeText
        };
        if(this.isChanged === "true"){
          this.submitDataInt.is_changed_bio = "true";
          this.submitDataInt.previos_lastname =this.secondNameChanged;
          this.submitDataInt.previos_firstname =this.firstNameChanged;
        } else {this.submitDataInt.is_changed_bio = false};

        json = JSON.stringify(this.submitDataInt);
      }
      console.log(json);
    }
  },
  computed: {

  },
};
</script>

<style scoped>
.form {
  box-sizing: border-box;
  background: #f9f9f9;
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
  font-size: 15px;
  padding: 6px 0 4px 10px;
  border: 2px solid #cecece;
  background: #fcfcfc;
  border-radius: 6px;
  margin-right: 0;
  margin-top: 10px;
  margin-bottom: 10px;
}
.dropdown-wrapper{
  display: flex;
  flex-direction: row;
  align-items: center;
  border: 2px solid #cecece;
  width: auto;
  border-radius: 6px;
  justify-content: space-between;
  margin-bottom: 5px;
  margin-top: 10px;
  background: white;
}
.string.four{
  margin-top: 5px;
}
.myInput.dropdown{
  width: 100%;
  border: 0px;
}
.myInput.dropdown:focus{
  outline: none
}

.input-wrapper {
  display: flex;
  flex-direction: column;
  min-width: 200px;
  /*color: #cecece;*/
}

.label-radio {
  margin-right: 20px;
}
h1,
h2,
h3 {
  margin-bottom: 8px;
  margin-top: 2px;
}


.line {
  margin-bottom: 5px;
  margin-top: 5px;
}

.string.six {
  display: flex;
}

.dropdown {
  position: relative;
  display: inline-block;
  margin: 0;
}

.dropdown-content {
  position: absolute;
  list-style: none;
  background-color: white;
  min-width: 100%;
  max-height: 150px;
  border-radius: 6px;
  padding: 0 ;
  z-index: 1;
  margin:0;
  overflow: auto;

}
.li-in-content{
  box-shadow: 0px 0px 5px 1px rgba(0, 23, 191, 0.1);
  border: 1px solid #aeb7e6;
  background: white;
  border-radius: 6px;
  padding-left: 5px;
  min-height: 30px;
  display: flex;
  align-items: center;
  font-size:15px;
}
.li-in-content:hover{
  border-radius: 6px;
  background-color: #eef0ff;
  cursor: pointer;
}

/*.dropdown:hover .dropdown-content {*/
/*  display: block;*/
/*}*/
.triangle {
  width: 0;
  height: 0;
  border-left: 5px solid transparent;
  border-right: 5px solid transparent;
  border-top: 10px solid #bebebe;
  margin-right: 5px;
}
.triangle:hover{
  cursor: pointer;
}

</style>
