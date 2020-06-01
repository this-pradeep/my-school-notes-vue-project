<template>
  <div>
    <div class="bg-theme-blue py-1 mb-3">
      <div class="container mx-auto">
        <div class="mx-auto -mb-56 ">
          <div class="my-16">
            <h1 class="text-2xl text-blue-300">The Next Generation Notebook For Students</h1>
          </div>
        <form class="bg-white shadow-xl rounded-lg px-8 pt-6 pb-8 mb-4 relative">
          <div class="mb-4">
            <label class="block text-gray-600 text-left font-medium mb-2" for="question">
              Question:
            </label>
            <input v-model="newQuestion" class="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:bg-blue-100 focus:shadow-md" id="question" type="text" placeholder="What is the name of our Prime Minister?, etc.">
          </div>
          <div class="mb-6">
            <label class="block text-gray-600 text-left font-medium mb-2" for="answer">
              Answer:
            </label>
            <textarea v-model="newAnswer" name="answer" class="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 mb-3 leading-tight focus:outline-none focus:bg-blue-100 focus:shadow-md"  cols="30" rows="4"></textarea>
          </div>
          <div class="absolute right-0 bottom-0 mb-5 mr-10 ">
            <button @click ="addQA" class="bg-blue-400 hover:bg-blue-500 text-white font-medium py-1 px-10 rounded focus:outline-none" type="button">
            SAVE
            </button>
          </div>
        </form>
      </div>
    </div>
    </div><br>
    <div class="mt-56">
      <h1 v-show="remaining" class="text-2xl text-center">{{remaining}} Question-Answers are remaining to learn</h1>
      <h1 v-show="!remaining" class="text-2xl text-center">Congratulations! You have learned all the Question &amp; Answers</h1>
      <div class="flex justify-between my-10 mx-32">
        <div>
          <button  class="bg-blue-200 hover:bg-blue-400 hover:text-gray-100 text-blue-600 font-medium py-1 px-16 rounded-l-full focus:outline-none" :class="{'active:bg-red-400 active:text-gray-100': filter === 'all' }" @click="filter = 'all'" type="button">
            ALL
        </button>
        <button class="bg-blue-200 hover:bg-blue-400 hover:text-gray-100 text-blue-600 font-medium py-1 px-8 focus:outline-none" :class="{'active:bg-red-900 active:text-gray-100': filter == 'active' }" @click="filter = 'active'" type="button">
            Active
        </button>
        <button class="bg-blue-200 hover:bg-blue-400 hover:text-gray-100 text-blue-600 font-medium py-1 px-8 rounded-r-full focus:outline-none" :class="{'active:bg-red-400 active:text-gray-100': filter == 'completed' }" @click="filter = 'completed'" type="button">
            Completed
        </button>
        </div>
        <div>
          <button v-if="showClearCompletedButton" @click="clearCompleted" class="bg-gray-300 hover:bg-gray-400 hover:text-gray-800 text-gray-600 font-medium py-1 px-8 rounded-full focus:outline-none"  type="button">
           Clear Completed
        </button>
        </div>
      </div>
      <div v-for="( QA, index ) in QAfiltered" :key="QA.id" class="container mx-auto mt-10 pb-8 border-b-2">
        <div class="flex flex-row justify-between">
          <div class="flex">
            <span class="mr-2 text-lg font-medium text-gray-600">Question {{QA.id}} </span>
            <h3 :class="{'line-through bg-gray-300': QA.completed}" class="ml-4 text-lg font-medium text-gray-600">{{QA.question}}</h3>
          </div>
          <div class="flex">
            <button @click="editQA(index)" class="font-medium text-gray-600 mx-4 focus:outline-none">
              <svg class="fill-current text-gray-600 inline-block mx-1 mb-1" width="17.491" height="17.491" viewBox="0 0 17.491 17.491">
              <path  data-name="006-edit" d="M16.225,1.288a4.366,4.366,0,0,0-6.178-.017l-.007.007-.005.006L.884,10.43a.683.683,0,0,0-.2.4L.005,16.728a.683.683,0,0,0,.758.757l5.86-.683a.683.683,0,0,0,.4-.195l.013-.013.007-.006.006-.006L16.21,7.455a4.369,4.369,0,0,0,.015-6.166Zm-5.7,1.439,1.639,1.639L3.975,12.553l-1.64-1.64Zm-9.061,13.3.422-3.635L5.1,15.6Zm5.1-.888L4.942,13.519l8.187-8.186,1.635,1.634Zm9.111-9.194L11.545,1.817a3,3,0,0,1,4.129,4.129Zm0,0" transform="translate(0 0)" fill=""/>
            </svg>
            <span class="text-lg font-medium text-gray-600">EDIT</span>
            </button>
            <button @click="removeQA(index)" class="font-medium text-gray-600 mx-4 focus:outline-none">
              <svg class="fill-current text-gray-600 inline-block mx-1 mb-1" width="15.036" height="17" viewBox="0 0 15.036 17">
                <path id="_019-garbage" data-name="019-garbage" d="M14.9,2.523H11.19V.664A.65.65,0,0,0,10.555,0H5.48a.65.65,0,0,0-.634.664V2.523H1.134a.665.665,0,0,0,0,1.328H2.308V16.336A.65.65,0,0,0,2.942,17H13.093a.65.65,0,0,0,.634-.664V3.852H14.9a.665.665,0,0,0,0-1.328Zm-8.787-1.2H9.921v1.2H6.115Zm6.344,14.344H3.577V3.852h8.882Zm-5.5-9.961v8.1a.635.635,0,1,1-1.269,0v-8.1a.635.635,0,1,1,1.269,0Zm3.383,0v8.1a.635.635,0,1,1-1.269,0v-8.1a.635.635,0,1,1,1.269,0Zm0,0" transform="translate(-0.5)"/>
              </svg>
            <span class="text-lg font-medium text-gray-600">DELETE</span>
            </button>
            <button @click="completedCheck(index)" :class="{'text-green-500': QA.completed}" class="font-medium text-gray-600 mx-4 focus:outline-none">
               <svg  class="fill-current inline-block mx-1 mb-1" width="25"  viewBox="0 0 512 512" ><path d="m369.164062 174.769531c7.8125 7.8125 7.8125 20.476563 0 28.285157l-134.171874 134.175781c-7.8125 7.808593-20.472657 7.808593-28.285157 0l-63.871093-63.875c-7.8125-7.808594-7.8125-20.472657 0-28.28125 7.808593-7.8125 20.472656-7.8125 28.28125 0l49.730468 49.730469 120.03125-120.035157c7.8125-7.808593 20.476563-7.808593 28.285156 0zm142.835938 81.230469c0 141.503906-114.515625 256-256 256-141.503906 0-256-114.515625-256-256 0-141.503906 114.515625-256 256-256 141.503906 0 256 114.515625 256 256zm-40 0c0-119.394531-96.621094-216-216-216-119.394531 0-216 96.621094-216 216 0 119.394531 96.621094 216 216 216 119.394531 0 216-96.621094 216-216zm0 0"/></svg>
            </button>
          </div>
        </div>
        <div class="flex">
          <span class="mr-2 text-lg font-medium text-gray-600">Answer</span>
          <p :class="{'line-through bg-gray-300': QA.completed}" class="text-left ml-10 text-lg  text-gray-600">{{QA.answer}}</p>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'QuestionAnswerList',
  props: {},
  data() {
    return {
      newQuestion: '',
      newAnswer: '',
      idforQA: 4,
      filter: 'all',
      questionAnswers: [
        {
          id: 1,
          question: 'What are you doing these days?',
          answer: 'Yes, please sit down. Here is Shipras monthly progress report. She has failed in two subject.Yes, please sit down. Here is Shipra monthly progress report. She has failed in two subject.Yes, please sit down. Here is Shipra monthly progress report. She has failed in two subject.Yes, please sit down. Here is Shipras monthly progress report. She has failed in two subject.Yes, please sit down. Here is Shipras monthly progress report. She has failed in two subject.',
          completed: false,
        },
        {
          id: 2,
          question: 'What 2 are you doing these days?',
          answer: 'Yes, 2 please sit down. Here is Shipras monthly progress report. She has failed in two subject.Yes, please sit down. Here is Shipra monthly progress report. She has failed in two subject.Yes, please sit down. Here is Shipra monthly progress report. She has failed in two subject.Yes, please sit down. Here is Shipras monthly progress report. She has failed in two subject.Yes, please sit down. Here is Shipras monthly progress report. She has failed in two subject.',
          completed: false,
        },
        {
          id: 3,
          question: 'What 3 are you doing these days?',
          answer: 'Yes, 3 please sit down. Here is Shipras monthly progress report. She has failed in two subject.Yes, please sit down. Here is Shipra monthly progress report. She has failed in two subject.Yes, please sit down. Here is Shipra monthly progress report. She has failed in two subject.Yes, please sit down. Here is Shipras monthly progress report. She has failed in two subject.Yes, please sit down. Here is Shipras monthly progress report. She has failed in two subject.',
          completed: false,
        },
      ],
    };
  },
  computed: {
    remaining() {
      return this.questionAnswers.filter((QA) => !QA.completed).length;
    },
    showClearCompletedButton() {
      return this.questionAnswers.filter((QA) => QA.completed).length > 0;
    },
    QAfiltered() {
      if (this.filter === 'active') {
        return this.questionAnswers.filter((QA) => !QA.completed);
      }
      if (this.filter === 'completed') {
        return this.questionAnswers.filter((QA) => QA.completed);
      }
      return this.questionAnswers;
    },
  },

  methods: {
    addQA() {
      if (this.newQuestion.trim().length === 0 || this.newAnswer.trim().length === 0) {
        return;
      }
      this.questionAnswers.push({
        id: this.idforQA,
        question: this.newQuestion,
        answer: this.newAnswer,
        completed: false,
      });
      this.newQuestion = '';
      this.newAnswer = '';
      this.idforQA += 1;
    },

    editQA(index) {
      const arr = [this.newQuestion = this.questionAnswers[index].question, this.newAnswer = this.questionAnswers[index].answer];
      return arr;
    },

    removeQA(index) {
      this.questionAnswers.splice(index, 1);
    },

    completedCheck(index) {
      const t = true;
      const f = false;
      this.questionAnswers[index].completed = !this.questionAnswers[index].completed ? t : f;
    },

    clearCompleted() {
      this.questionAnswers = this.questionAnswers.filter((QA) => !QA.completed);
    },
  },
};
</script>

<style scoped lang="scss">

</style>
