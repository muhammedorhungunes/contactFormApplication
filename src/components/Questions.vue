<template>
  <div>
      <b-card title="Card Title" no-body>
        <b-card-header stlye="width: 500px;" header-tag="nav">
          <b-nav card-header pills>
            <b-nav-item active style="margin:10px;" @click="changeLanguage('tr')">TR</b-nav-item>
            <b-nav-item active style="margin:10px;" @click="changeLanguage('en')">EN</b-nav-item>
          </b-nav>
        </b-card-header>

        <b-card-body class="text-center" v-if=showTurkish>
          <label class="mr-sm-2" for="inline-form-custom-select-pref">Başlık TR</label>
          <b-form-input class="w-100 m-2" v-model="questionTitleTurkish" placeholder="Lütfen soru başlığını giriniz."></b-form-input>

          <b-button v-if=questionTitleTurkish v-b-modal.modal-center class="m-2" variant="outline-primary" @click="showDetails();"><b-icon icon="plus"></b-icon> Soru Ekle</b-button>
        </b-card-body>
        <b-card-body class="text-center" v-if=showEnglish>
          <label class="mr-sm-2" for="inline-form-custom-select-pref">Title EN</label>
          <b-form-input class="w-100 m-2" v-model="questionTitleEnglish" placeholder="Enter your question title"></b-form-input>
          <b-button v-if=questionTitleEnglish v-b-modal.modal-center class="m-2" variant="outline-primary" @click="showDetails();"><b-icon icon="plus"></b-icon> Add Question</b-button>
        </b-card-body>
      </b-card>
      <QuestionModal v-show="showModal" :question-title-english=questionTitleEnglish :question-title-turkish=questionTitleTurkish :show-english=showEnglish :show-turkish=showTurkish :question-list=questionList></QuestionModal>
      <draggable v-model="questionList" :options="{group:'people'}" @start="drag=true" @end="drag=false">
          <div v-for="(item,index) in questionList" :key="item.question">
            <div v-if=questionList >
              <b-card-group deck >
                <b-card
                  :header=item.language
                  style="width: 20rem; margin: 20px;display: inline-block;"
                  header-tag="header"
                  footer=" "
                  footer-tag="footer"
                  :title=item.question
                  :key=index 
                >
                  <b-card-text>{{item.description}}</b-card-text>
                  <b-form-select v-bind:v-model="item.selected" v-bind:options="item.options"></b-form-select>
                </b-card>
              </b-card-group>
              <b-col lg="4" class="pb-2 m-1 d-inline"><b-button size="sm"><b-icon icon="x" @click="deleteQuestion(index);"></b-icon></b-button></b-col>
              <!-- <b-button class="m-1 d-inline" variant="primary" ><b-icon icon="x" @click="deleteQuestion(index);"></b-icon></b-button> -->
            </div>
          </div>
        </draggable>
    </div>
  
</template>

<script>

import QuestionModal from './QuestionModal.vue'
import draggable from 'vuedraggable'

export default {
  
  name: 'Questions',
 
  components: {
    QuestionModal,
    draggable,
  },
  data () {
    return {
      msg: 'Welcome to Your Vue.js App',
      showTurkish: true,
      showEnglish: false,
      showModal: false,
      questionTitleEnglish: '',
      questionTitleTurkish: '',
      questionList: [{
        title: 'title',
        language: 'en',
        question: 'What is your gender?',
        description: 'Description',
        selected: null,
        options: [
          { value: 'Female', text: 'Female' },
          { value: 'Male', text: 'Male' },
          { value: 'Other', text: 'Other' },
        ]
      }]
    }
  },
  methods: {
    changeLanguage(language){
      if(language === 'en'){
        this.showTurkish=false;
        this.showEnglish=true;
      }else{
        this.showTurkish=true;
        this.showEnglish=false;
      }
    },
    showDetails(){
        this.showModal = true
    },
    deleteQuestion(index) {
      this.questionList.splice(index, 1);
    },
  }
}
</script>


<style scoped>

</style>
