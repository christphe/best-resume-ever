<template>
  <div class="resume" v-if="person" id="resume2">
    <div class="left-column">
      <div>
        <div class="headline">
          <span> {{ person.name.first }} {{ person.name.middle }} </span>
          <span class="uppercase"> {{ person.name.last }} </span>
        </div>

        <p>
          <span class=""> {{ person.position }} </span>
          <br />
          <span v-if="person.contact.location">
            {{ person.contact.location }}
          </span>
        </p>
      </div>

      <div class="mugshot">
        <img src="../../resume/id.jpg" />
      </div>
      <div class="multi-line-txt" v-html="person.about"></div>

      <div class="multi-line-txt">
        {{ person.knowledge }}
      </div>

      <a v-if="contactLinks.email" :href="contactLinks.email">
        <div class="block-marged">
          <i class="contact-icon far fa-envelope"></i> {{ person.contact.email }}
        </div>
      </a>

      <div v-if="contactLinks.phone"  class="block-marged">
        <i class="contact-icon fa fa-phone"></i>{{ person.contact.phone }}
      </div>

      <div class="social-container">
        <a v-if="person.contact.website" :href="person.contact.website">
          <div class="block-marged">
            <i class="fa fa-globe contact-icon"></i>
            {{ person.contact.website }}
          </div>
        </a>

        <a
          v-if="person.contact.github"
          :href="contactLinks.github"
          class="external-link"
        >
          <i class="fab fa-github contact-icon"></i>
          <span class="block-marged">
            {{ person.contact.github }}
          </span>
        </a>

        <a
          v-if="person.contact.codefights"
          :href="contactLinks.codefights"
          class="external-link"
        >
          <svg
            width="20"
            height="20"
            viewBox="0 0 24 24"
            class="contact-icon-svg"
          >
            <path
              d="M12 15.2L9.2 4.8 0 3.2l1.7 2.6 5.7.7.7 2.3-3.7-.4 1.3 2 3 .3L12 20.8l3.3-10.1 3-.3 1.3-2-3.7.4.7-2.3 5.7-.7L24 3.2l-9.2 1.6"
            ></path>
          </svg>

          <span class="block-marged">
            {{ person.contact.codefights }}
          </span>
        </a>

        <a
          v-if="person.contact.medium"
          :href="contactLinks.medium"
          class="external-link"
        >
          <i class="fab fa-medium contact-icon"></i>
          <span class="block-marged">
            {{ person.contact.medium }}
          </span>
        </a>
      </div>

      <div class="hobbies-container">
        <!-- <span class="subheadline">Hobbies</span> -->
        <div class="hobbies-content">
          <a
            v-for="(hobby, index) in person.hobbies"
            :key="index"
            class="hobby-item"
            :href="hobby.url"
          >
            <i
              v-if="hobby.iconClass"
              :class="hobby.iconClass + ' hobby-item__icon'"
            ></i>
            <span class="hobby-item__icon-label"> {{ hobby.name }} </span>
          </a>
        </div>
      </div>
    </div>

    <div class="left-column-bg"></div>

    <div class="right-column">
      <div class="experience-section section">
        <div class="icon">
          <i class="material-icons small-icon">work</i>
          <span class="section-headline">{{ lang.experience }}</span>
        </div>

        <div class="section-content">
          <a
            v-for="(experience, index) in person.experience"
            :key="index"
            class="section-content__item"
            :href="experience.website"
          >
            <div class="row">
              <span class="col col-8 section-content__header">
                {{ experience.position }}
              </span>
              <span
                class="col col-4 section-content__text text-right timeperiod"
              >
                {{ experience.timeperiod }}
              </span>
            </div>
            <span class="section-content__subheader">
              {{ experience.company }}</span
            >
            <span
              class="section-content__text description"
              v-html="experience.description"
            >
            </span>
          </a>
        </div>
      </div>

      <div v-if="person.projects" class="projects-section section">
        <div class="icon">
          <i class="material-icons">code</i>
          <span class="section-headline"> {{ lang.projects }} </span>
        </div>

        <div class="section-content">
          <a
            v-for="(project, index) in person.projects"
            :key="index"
            class="section-content__item"
            :href="project.url"
          >
            <span class="section-content__header"> {{ project.name }} </span>
            <span class="section-content__subheader">{{
              project.platform
            }}</span>
            <span class="section-content__text">
              {{ project.description }}
            </span>
            <span class="section-content__text--light">
              {{ project.url }}
            </span>
          </a>
        </div>
      </div>

      <div v-if="person.skills" class="skills-section section">
        <div class="icon">
          <i class="material-icons">done_all</i>
          <span class="section-headline"> {{ lang.skills }} </span>
        </div>

        <div class="section-content row">
          <div
            v-for="(skill, index) in person.skills"
            :key="index"
            class="col col-4"
          >
            <div>
              <a :href="skill.url">
                <i
                  v-if="skill.iconClass"
                  :class="'lang-icon ' + skill.iconClass"
                ></i>

                <span v-else class=""> {{ skill.name }} </span>
              </a>
            </div>
            <div class="skill-bar">
              <div
                class="skill-bar-content"
                :style="{ width: skill.level + '%' }"
              ></div>
            </div>
          </div>
        </div>
      </div>

      <div v-if="person.contributions" class="contributions-section section">
        <div class="icon">
          <i class="fa fa-heart font-awesome-icons"></i>
          <span class="section-headline"> {{ lang.contributions }} </span>
        </div>

        <div class="section-content-grid">
          <a
            v-for="(contribution, index) in person.contributions"
            :key="index"
            :href="contribution.url"
            class="section-content__item-grid"
          >
            <span class="section-content__header">
              {{ contribution.name }}
            </span>
            <span class="section-content__text">
              {{ contribution.description }}
            </span>
            <span
              class="section-content__text--light"
              style="word-break: break-all;"
            >
              {{ contribution.url }}
            </span>
          </a>
        </div>
      </div>

      <div class="education-section section">
        <div class="icon">
          <i class="material-icons">school</i>
          <span class="section-headline">{{ lang.education }}</span>
        </div>

        <div class="section-content">
          <a
            v-for="(education, index) in person.education"
            :key="index"
            class="section-content__item"
            :href="education.website"
          >
            <span class="section-content__header">
              {{ education.school }}
            </span>
            <span class="section-content__subheader">{{
              education.degree
            }}</span>
            <span class="section-content__text">
              {{ education.timeperiod }}
            </span>
            <span class="section-content__text--light">
              {{ education.description }}
            </span>
          </a>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import Vue from 'vue';
import { getVueOptions } from './options';

const name = 'graphene';

export default Vue.component(name, getVueOptions(name));
</script>

<style lang="less" scoped>
@gunmetal: #022b3aff;
@teal: #1f7a8cff;
@columbia-blue: #bfdbf7ff;
@lavender-web: #e1e5f2ff;
@white: #ffffffff;
@accent-color: @gunmetal;

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
  align-items: center;
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

.resume {
  display: flex;
  position: relative;

  font-family: 'Roboto' !important;
  font-size: 0.9em;
}

.left-column {
  width: 30%;
  height: 100%;
  padding: 30px;
  padding-top: 45px;
  text-align: left;

  color: @gunmetal;
  background-color: @lavender-web;
  overflow: hidden;
  display: block;
  z-index: 2;

  opacity: 1; // lower this value (0.7 approx.) to see the cover image
  position: absolute;
}

// Background cover displayed on the left-column side
// ------------
.left-column-bg {
  // You can put your own cover image in the url path
  // --------------------------------------
  // background: url('../assets/cover.jpg');
  background-repeat: no-repeat;
  background-size: cover;
  background-position: 25% 25%;
  opacity: 0.4; // up this value to contrast the cover image

  height: 100%;
  width: 35%;
  padding: 30px;
  padding-top: 45px;

  display: block;
  overflow: hidden;
  position: relative;
  top: 0;
  z-index: 1;
}

.right-column {
  display: flex;
  flex-direction: column;
  padding: 30px;

  height: 100%;
  width: 70%;
}

a {
  color: inherit;
  cursor: pointer;
  text-decoration-line: none;

  &:visited {
    color: inherit;
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

.contact-icon {
  color: #294466;
  font-size: 1.5em;
  margin-right: 10px;

  top: 2px;
  position: relative;
}

.contact-icon-svg {
  margin-top: -2.5px;
  margin-right: 10px;

  transform: scale(1);

  top: 5px;
  position: relative;
}

.contact-icon-svg path {
  fill: #294466;
}

.external-link {
  display: block;
  margin-bottom: 5px;
}

.block-marged {
  margin-top: 15px;
  margin-bottom: 15px;
}

.multi-line-txt {
  margin-top: 30px;
  margin-bottom: 20px;
}

.social-container {
  margin-top: 30px;
  margin-bottom: 30px;
}

.headline {
  color: #294466;
  font-size: 1.3em;
  font-weight: bold;
}

.mugshot {
  img {
    width: 75%;
  }
}

.uppercase {
  text-transform: uppercase;
}

.section-headline {
  display: inline-block;
  font-size: 1.2em;
  margin-left: 5px;
}

.section-content {
  margin-top: 10px;
  padding-left: 32px;
}

.section-content__item {
  display: block;
  margin-bottom: 20px;
}

.section-content__item-grid {
  flex: 1 1 0;

  margin-bottom: 10px;
  padding-right: 10px;
}

.section-content-grid {
  display: flex;
  flex-wrap: wrap;
  justify-content: space-between;

  margin-top: 10px;
  margin-bottom: 10px;
  padding-left: 32px;
}

.grid-item {
  padding-right: 20px;
}

.section-content__header {
  display: block;

  font-size: 1.1em;
  font-weight: 500;
}

.squarred-grid-item {
  display: block;

  border: 1px solid @accent-color;

  background-color: @accent-color;
  color: #294466;

  margin-top: 5px;
  padding: 5px;

  transition: 0.5s;

  &:hover {
    background-color: transparent;
    color: @accent-color;
    transition: 0.5s;
  }
}

.section-content__subheader {
  display: block;
  font-weight: 400;
}

.section-content__text {
  display: block;
  font-weight: 300;

  &.timeperiod {
    font-weight: 500;
    color: @accent-color;
  }

  &.description ::v-deep strong {
    font-style: oblique;
    font-weight: 500;
  }
}

.skill-bar {
  background-color: @gunmetal;
  .skill-bar-content {
    height: 10px;
    background-color: @columbia-blue;
  }
}

.section-content__text--light {
  color: rgba(0, 0, 0, 0.42);
  font-weight: 300;
}

.section-content__subheader,
.section-content__text--light,
.section-content__header {
  line-height: 1.5em;
}

.section {
  margin-top: 10px;
  margin-bottom: 10px;
}

.lang-icon {
  color: rgba(0, 0, 0, 0.72);
  font-size: 3em;

  &:hover {
    color: @accent-color;
  }
}

.hobbies-container {
  margin-top: 30px;
}

.hobbies-content {
  display: flex;
  flex-direction: column;
}

.hobby-item {
  display: grid;
  grid-template-columns: 30px auto;

  margin-right: 25px;
  margin-bottom: 10px;
}

.hobby-item__icon {
  font-size: 1.3em;
}

.hobby-item__icon-label {
  top: 2.5px;
  position: relative;
}

.subheadline {
  color: rgba(255, 255, 255, 0.8);
  font-size: 1.2em;

  display: block;
  margin-bottom: 10px;
}
</style>
