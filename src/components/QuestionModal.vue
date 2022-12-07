<template>
    <div>
        <b-modal id="modal-center" centered title="Form Veri Ekle" v-if=showTurkish okTitle="Kaydet" cancelTitle="İptal Et"  @ok="saveQuestion" hide-header-close=true>
            <p class="my-4">{{questionTitleTurkish}}</p>
            <label class="mr-sm-2" for="inline-form-custom-select-pref">Veri Tipi</label>
            <b-form-select
                v-model="selected"
                :options="options"
                class="mb-3 w-100"
                value-field="item"
                text-field="name"
                disabled-field="notEnabled"
            ></b-form-select>
         
            <b-form-group label="Zorunlu mu?" v-slot="{ ariaDescribedby }" v-if=selected>
                <b-form-radio v-model="requiredSelected" :aria-describedby="ariaDescribedby" name="some-radios" value="A"> Evet</b-form-radio>
                <b-form-radio v-model="requiredSelected" :aria-describedby="ariaDescribedby" name="some-radios" value="B"> Hayir</b-form-radio>
            </b-form-group>

            <b-form-input v-if=requiredSelected class="w-100 m-2" v-model="questionModal" placeholder="Lütfen sorunuzu giriniz"></b-form-input>
            <b-form-input v-if=requiredSelected class="w-100 m-2" v-model="description" placeholder="Lütfen açıklama giriniz"></b-form-input>
            <label v-if=questionModal class="mr-sm-2" for="inline-form-custom-select-pref">Secenekler</label>
            <div v-if=questionModal v-for="(option, index) in optionsQuestion">
                <b-form-input class="w-50 m-1 d-inline" v-model="temp[index]" :key="index" @change="setOption(index)" placeholder="Lütfen soru seçeneğini giriniz"></b-form-input>
                <b-button class="m1 d-inline" variant="primary" @click="deleteOption(index);"><b-icon icon="x"></b-icon></b-button>
            </div>
            <b-button v-if=questionModal class="m-1" variant="primary" @click="addOption();"><b-icon icon="plus" ></b-icon> Seçenek Ekle</b-button>
        </b-modal>
        <b-modal id="modal-center" centered title="Add Form Input" v-if=showEnglish okTitle="Save" cancelTitle="Cancel" @ok="saveQuestion" hide-header-close=true>
            <p class="my-4">{{questionTitleEnglish}}</p>
            <label class="mr-sm-2" for="inline-form-custom-select-pref">Input Type</label>
            <b-form-select
                v-model="selected"
                :options="optionsEN"
                class="mb-3 w-100"
                value-field="item"
                text-field="name"
                disabled-field="notEnabled"
            ></b-form-select>
            <b-form-group label="Is required?" v-slot="{ ariaDescribedby }" v-if=selected>
                <b-form-radio v-model="requiredSelected" :aria-describedby="ariaDescribedby" name="some-radios" value="A"> Yes</b-form-radio>
                <b-form-radio v-model="requiredSelected" :aria-describedby="ariaDescribedby" name="some-radios" value="B"> No</b-form-radio>
            </b-form-group>

            <b-form-input v-if=requiredSelected class="w-100 m-2" v-model="questionModal" placeholder="Please enter the question"></b-form-input>
            <b-form-input v-if=requiredSelected class="w-100 m-2" v-model="description" placeholder="Please enter the description"></b-form-input>
            <label v-if=questionModal class="mr-sm-2" for="inline-form-custom-select-pref">Options</label>
            <div v-if=questionModal v-for="(option, index) in optionsQuestion">
                <b-form-input class="w-50 m-1 d-inline" v-model="option.text" :key="index" placeholder="Please enter the option"></b-form-input>  
                <b-button class="m-1 d-inline" variant="primary" ><b-icon icon="x" @click="deleteOption(index);"></b-icon></b-button>    
            </div>
            <b-button v-if=questionModal class="m-1" variant="primary" @click="addOption();"><b-icon icon="plus" ></b-icon> Add Option</b-button>
     
        </b-modal>
    </div>    
</template>
  
  <script>
  export default {
   
    name: 'QuestionModal',
    data () {
      return {
        msg: 'Welcome to Your Vue.js App',
        optionsQuestion: [],
        selected: null,
        options: [
            { item: null, name: 'Lütfen soru tipini seçiniz', notEnabled: true  },
            { item: 'selectBox', name: 'Select Box' },
        ],
        optionsEN: [
            { item: null, name: 'Please select question type', notEnabled: true  },
            { item: 'selectBox', name: 'Select Box' },
        ],
        requiredSelected: '',
        questionModal: '',
        description: '',
        temp: []
      }
    },
    props: {
        questionTitleTurkish: String,
        questionTitleEnglish: String,
        showTurkish: Boolean,
        showEnglish: Boolean,
        questionList: Array ,
    },
    methods:{
        addOption(){
            this.optionsQuestion.push({value: '', text: ''});
        },
        setOption(index){
            this.optionsQuestion[index] = {value: this.index, text: this.temp[index]}
        },
        deleteOption(index) {
            this.optionsQuestion.splice(index, 1);
        },
        saveQuestion(event){
            if(this.showTurkish){
                this.questionList.push({
                    title: this.questionTitleTurkish,
                    language: 'tr' ,
                    question: this.questionModal,
                    description: this.description,
                    selected: null,
                    options: this.optionsQuestion
                });
            }

            if(this.showEnglish){
                this.questionList.push({
                    title: this.questionTitleEnglish,
                    language: 'en' ,
                    question: this.questionModal,
                    description: this.description,
                    selected: null,
                    options: this.optionsQuestion
                });
            }
            this.questionTitleTurkish='';
            this.questionTitleEnglish='';
            this.questionModal= '';
            this.description='';
            this.optionsQuestion=[];
            this.selected= null;
            this.requiredSelected= null;
        }
    }
  }
  </script>
  
  <style >

  </style>
  