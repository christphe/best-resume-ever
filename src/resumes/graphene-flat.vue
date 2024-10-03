<template>
  <div class="resume">
    <div class="row header">
      <div class="name col-12">
        <span class="uppercase">{{ person.name.first }} {{ person.name.middle }} {{ person.name.last }} </span>
      </div>
      <div class="position col-12">
        <span class="uppercase">{{ person.position }}</span>
      </div>
    </div>
    <div class="mugshot">
      <img src="../../resume/id.jpg" />
    </div>
    <div class="content">
      <div class="row contact-row">
        <div><i class="contact-icon far fa-envelope"></i> {{ person.contact.email }}</div>
        <div><i class="contact-icon fa fa-phone"></i>&nbsp;{{ person.contact.phone }}</div>
        <div><i class="contact-icon fa fa-home"></i>&nbsp;{{ person.location }}</div>
      </div>
      <div class="about-section section">
        <div class="section-title headline"><i class="fas fa-user"></i> {{ lang.about }}</div>
        <div class="section-content"><span v-html="person.about"></span></div>
      </div>
      <div v-if="person.skills" class="skills-section section">
        <div class="section-title headline">
          <i class="fa fa-flask"></i> {{ lang.skills }}
        </div>
        <div class="section-content row">
          <div v-for="(skill, index) in person.skills" :key="index" class="section-content__item col col-4">
            <div>
              {{ skill.name }}
            </div>
          </div>
        </div>
      </div>
      <div class="section experience-section">
        <div class="section-title headline"><i class="fas fa-history"></i> {{ lang.experience }}</div>
        <div class="section-content">
          <div v-for="(experience, index) in person.experience" :key="index" class="section-content__item">
            <div class="row section-title">
              <span class="col col-8 position">
                {{ experience.company }} - {{ experience.position }}
              </span>
              <span class="col col-4 text-right timeperiod">
                {{ experience.timeperiod }}
              </span>
            </div>
            <div class="section-content__text description" v-html="experience.description"></div>
          </div>
        </div>
      </div>
      <div class="education-section section">
        <div class="section-title headline"><i class="fas fa-graduation-cap"></i> {{ lang.education }}</div>
        <div class="section-content">
          <div v-for="(education, index) in person.education" :key="index" class="section-content__item">
            <div class="row section-title">
              <div class="col col-8 degree">
                {{ education.school }} - {{ education.degree }}
              </div>
              <div class="col col-4 text-right timeperiod">
                {{ education.timeperiod }}
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<style lang="less" scoped>
@gunmetal: #022b3aff;
@teal: #1f7a8cff;
@columbia-blue: #bfdbf7ff;
@lavender-web: #e1e5f2ff;
@white: #ffffffff;
@accent-color: #294466;

.resume {
  display: flex;
  flex-direction: column;
  position: relative;

  font-family: 'Roboto' !important;
  font-size: 0.9em;
  box-sizing: border-box;
  page-break-after: auto;
}

.header {
  width: 100%;
  height: 128px;
  color: @gunmetal;
  background-color: @lavender-web;
  padding: 0.5cm 1cm;
  margin-top: 0.5cm;
  margin-left: 0 !important;
  margin-right: 0 !important;

  .name {
    font-size: 3em;
  }

  .position {
    font-size: 1.5em;
  }
}

.mugshot {
  margin: -90px 1cm -1cm auto;

  img {
    border-radius: 50%;
    width: 128px;
  }
}

.contact-row {
  >div {
    padding: 0 0.3cm;
  }
}

.content {
  padding: 0 0.5cm 1cm 0.5cm;
  font-weight: 300;

  .section-title {
    font-weight: 500;
    font-size: 1.2em;
    margin-bottom: 0.3cm;
    margin-top: 0.5cm;
  }

  .section-content {
    margin-left: 0.5cm;
  }
}

.experience-section {
  .position {
    color: @accent-color;
    font-weight: bold;
  }

  .timeperiod {
    color: @accent-color;
    font-weight: bold;
  }

  .section-content__text {
    margin-left: 0.5cm;
  }

  .section-title {
      margin-bottom: -0.1cm;
    }

  .section-content__item {
    padding-top: 0.5cm;
    padding-bottom: 0.5cm;
    page-break-after: auto;
    page-break-before: auto;
    page-break-inside: avoid;

    .section-title {
      margin-top: 0;
      margin-bottom: 0.3cm;
    }
  }

  ::v-deep ul {
    padding-left: 0.7cm;
    margin: 0;
    padding-top: 0.1cm;
    padding-bottom: 0.1cm;
  }

  ::v-deep strong {
    font-weight: 500;
  }
}

.education-section {
  .degree {
    color: @accent-color;
    font-weight: bold;
  }

  .timeperiod {
    color: @accent-color;
    font-weight: bold;
  }

  .section-content__item {
    margin-bottom: 1cm;
    page-break-after: auto;
    page-break-before: auto;
    page-break-inside: avoid;
  }
}

.headline {
  color: @accent-color;
  font-size: 1.3em;
  font-weight: bold;
}

.text-right {
  text-align: right;
}

.text-left {
  text-align: left;
}

.row {
  flex-direction: row;
  flex-wrap: wrap;
  display: flex;
  box-sizing: border-box;

  margin-right: -4px;
  margin-left: -4px;

  .col {
    box-sizing: border-box;
    padding-left: 4px;
    padding-right: 4px;
    width: 100%;
  }

  .col-1 {
    flex: 0 0 8.333333333%;
    max-width: 8.333333333%;
  }

  .col-2 {
    flex: 0 0 16.666666667%;
    max-width: 16.666666667%;
  }

  .col-3 {
    flex: 0 0 25%;
    max-width: 25%;
  }

  .col-4 {
    flex: 0 0 33.333333333%;
    max-width: 33.333333333%;
  }

  .col-5 {
    flex: 0 0 41.666666667;
    max-width: 41.666666667;
  }

  .col-6 {
    flex: 0 0 50%;
    max-width: 50%;
  }

  .col-7 {
    flex: 0 0 58.333333333%;
    max-width: 58.333333333%;
  }

  .col-8 {
    flex: 0 0 66.666666667%;
    max-width: 66.666666667%;
  }

  .col-9 {
    flex: 0 0 75%;
    max-width: 75%;
  }

  .col-10 {
    flex: 0 0 83.333333333%;
    max-width: 83.333333333%;
  }

  .col-11 {
    flex: 0 0 91.666666667;
    max-width: 91.666666667;
  }

  .col-12 {
    flex: 0 0 100%;
    max-width: 100%;
  }
}

.material-icons {
  //  color: @accent-color;
  position: relative;
  top: 5px;
}

.font-awesome-icons {
  //  color: @accent-color;
  font-size: 1.3em;
  margin-right: 6px;
}

.small-icon {
  top: 2.5px;
  font-size: 1.4em;
}

.uppercase {
  text-transform: uppercase;
}
</style>

<script>
import Vue from 'vue';
import { getVueOptions } from './options';

const name = 'graphene-flat';

export default Vue.component(name, getVueOptions(name));
</script>
