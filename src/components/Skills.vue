<template>
  <div class="hello">
      <div class="holder">
          <form action="" @submit.prevent="addSkill">
              <input type="text" placeholder="Enter a skip you have" v-model="skill" v-validate="'min: 5'" name="skill">
              <transition name="alert-in" enter-active-class="animated flipInX" leave-active-class="animated flipOutX">
                  <p class="alert" v-if="errors.has('skill')">{{ errors.first('skill') }}</p>
                  <p v-if="generalError">{{ generalError }}</p>
              </transition>
          </form>
          <ul>
              <transition-group name="list" enter-active-class="animated bounceInUp" leave-active-class="animated bounceOutUp">
              <li v-for="(data, index) in skills" :key='index'>
                  {{ data.skill }}
                  <i class="fa fa-minus-circle" v-on:click="remove(index)"></i>
              </li>
              </transition-group>
          </ul>

          <p>These are the skills you posses</p>
      </div>
  </div>
</template>

<script>
export default {
  name: 'Skills',
  data () {
    return {
      generalError: '',
      skill: '',
      skills: [
        {
          'skill': 'Vue.js',
        },
        {
          'skill': 'Frontend developer',
        },
      ],
    };
  },
  methods: {
    addSkill () {
      this.$validator.validateAll().then((result) => {
        if (result) {
          this.skills.push({skill: this.skill});
          this.skill = '';
          this.generalError = '';
        }
        else {
          this.generalError = 'Input data is not valid';
        }
      });
    },
    remove(id) {
      this.skills.splice(id, 1)
    }
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
@import "https://cdn.jsdelivr.net/npm/animate.css@3.5.1";
@import "https://maxcdn.bootstrapcdn.com/font-awesome/4.7.0/css/font-awesome.min.css";

.holder {
      background: #fff;
  }

  ul {
      margin: 0;
      padding: 0;
      list-style-type: none;
  }

  ul li {
      padding: 20px;
      font-size: 1.3em;
      background-color: #E0EDF4;
      border-left: 5px solid #3EB3F6;
      margin-bottom: 2px;
      color: #3E5252;
  }

  p {
      text-align: center;
      padding: 30px 0;
      color: gray;
  }

  .container {
      box-shadow: 0 0 40px lightgray;
  }

  input {
      width: calc(100% - 40px);
      border: 0;
      padding: 20px;
      font-size: 1.3em;
      background-color: #323333;
      color: #687F7F;
  }

  .alert {
      background: #fdf2ce;
      font-weight: bold;
      display: inline-block;
      padding: 5px;
      margin-top: -20px;
  }
    i {
        float: right;
        cursor: pointer;
    }

</style>
