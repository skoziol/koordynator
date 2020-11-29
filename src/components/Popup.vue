<template>
  <div class="popup">
    <header>
      <span class="title">Dokumentacja Jakaśtam </span>
      <span class="subtitle">
        Dodano przez {{creator}}, wyznaczony ekspert:  {{expert}}, koordynator: {{coordinator}}
      </span>
      <div class="slider-section">A <Slider :height="30" style="margin: 0 10px;"/>B</div>
    </header>
    <div class="body">
      <div class="column section_40">
        <TaskSection/>
        <RequirementsSection/>
      </div>
      <div class="column">
        <CommentSection/>
      </div>
      <div class="column">
        <button class="sample">-> Odeślij do projektu</button>
        <button class="sample">Zakończ i zaakceptuj</button>
        <button class="sample">Zakończ i odrzuć</button>
        <button class="sample">Sample</button>
        <button class="sample">Sample</button>

        <FilesSection/>
      </div>
    </div>
  </div>
</template>

<script>
import RequirementsSection from './RequirementsSection.vue'
import Slider from './Slider'
import TaskSection from './TaskSection'
import CommentSection from './CommentSection'
import FilesSection from './FilesSection.vue'

export default {
  name: 'Popup',
  components: {
    TaskSection,
    Slider,
    RequirementsSection,
    CommentSection,
    FilesSection
  },
  data () {
    return {
      creator: 'Stanisław Kozioł - HURT',
      expert: 'Siemason Stugała - HURT',
      coordinator: 'Aaaaa Bsade - HURT'
    }
  }
}
</script>

<style scoped lang='scss'>
  .popup{
    display:flex;
    align-items: center;
    justify-content: center;
    flex-direction: column;
    background:white;

    header{
      flex-basis: 50px;
      width: 100%;
      display:flex;
      align-items: center;
      justify-content: start;

      .title{
        font-size: 30px;
        margin-right: 20px;
      }

      .slider-section {
        margin:10px;
        font-size: 20px;
      }
    }

    .body{
      display:flex;
      align-items: center;
      justify-content: center;
      flex-grow:1;
      width:100%;

      .column{
        display:flex;
        flex-direction: column;
        flex-basis: 30%;
        border: 1px lightgrey solid;
        height:100%;

        &+.column{
          margin-left:5px;
        }

        &.section_40{
          flex-basis: 40% !important;
        }
      }
    }
  }
</style>
