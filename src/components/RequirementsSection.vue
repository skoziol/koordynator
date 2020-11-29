<template>
    <div class="requirements-section">
      <h3>Wymagania</h3>
      <span v-if="requirementsList.length > 0">{{completedRequirements/requirementsList.length * 100}}%</span> <progress :max="requirementsList.length" :value="completedRequirements" v-if="requirementsList.length > 0"></progress>
      <div class="requirement" v-for="requirement in requirementsList" :key="requirement">
        <div class="requirement-info">
          <input type="checkbox" v-model="requirement.status" @change="RequirementCompleted(requirement.status)">
          <span :class="{'line-through': requirement.status}">{{requirement.name}}</span>
        </div>
        <div class="requirement-detail">
          Dodano przez {{requirement.addedBy}}, {{requirement.time}}
        </div>
      </div>
      <div class="addRequirements">
        <input type="text" v-model="newRequirement">
        <button @click="addRequirements()">Add</button>
      </div>
  </div>
</template>

<script>
import moment from 'moment'
export default {
  name: 'requirements',
   data () {
    return {
      completedRequirements: 0,
      newRequirement:'',
      requirementsList: []
    }
  },
  methods: {
    addRequirements() {
      if(this.newRequirement.length === 0) return
      this.requirementsList.push({
          name: this.newRequirement,
          status: false,
          addedBy: 'Stanisław Kozioł - partner HURT',
          time: moment().locale('pl').format('DD-MM-YYYY, HH:mm:ss ')
        })
      this.newRequirement = ''
    },
    RequirementCompleted(){
      this.completedRequirements = 0
      this.requirementsList.map(requirement => {
        if(requirement.status) this.completedRequirements ++
      })
    }
  }
}
</script>

<style lang="scss" scoped>
.requirements-section{
  flex-grow:1;

  .requirement{
    display:flex;
    align-items: start;
    justify-content: center;
    flex-direction: column;
    font-size: 15px;
    height: 50px;

    .line-through{
      text-decoration: line-through;
    }

    .requirement-info{
      display:flex;
      align-items: center;
      justify-content: start;
    }
    .requirement-detail{
      display:flex;
      align-items: center;
      justify-content: start;
    }
  }

  .addRequirements{
  display:flex;
  } 
}
</style>