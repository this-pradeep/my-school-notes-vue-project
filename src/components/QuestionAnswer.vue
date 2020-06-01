<template>
  <div class="container mx-auto mt-10 pb-8 border-b-2">
        <div class="flex flex-row justify-between">
          <div class="flex">
            <span class="mr-2 text-lg font-medium text-gray-600">Question {{id}} </span>
            <h3 :class="{'line-through bg-gray-300': completed}" class="ml-4 text-lg font-medium text-gray-600">{{question}}</h3>
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
          <p :class="{'line-through bg-gray-300': completed}" class="text-left ml-10 text-lg  text-gray-600">{{answer}}</p>
        </div>
      </div>
</template>

<script>
export default {
  name: 'QuestionAnswer',
  props: {
    QA: {
      type: Object,
      required: true,
    },
    index: {
      type: Number,
      required: true,
    },
  },
  data() {
    return {
      id: this.QA.id,
      question: this.QA.question,
      answer: this.QA.answer,
      completed: this.QA.completed,
    };
  },

  methods: {
    removeQA(index) {
      this.$emit('removedQA', index);
    },

    editQA(index) {
      this.$emit('editedQA', index);
    },

    completedCheck(index) {
      this.$emit('completeCheck', index);
      if (!this.completed) {
        this.completed = true;
      } else {
        this.completed = false;
      }
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style lang="scss">

</style>
