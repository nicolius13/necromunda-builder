<template>
  <div>
    <b-container class="main">
      <b-row>
        <b-col>
          <h1 class="text-primary text-center">
            A character planner for Necromunda Underhive Wars
          </h1>
          <h2 class="text-center">
            Select a profile and plan your character
          </h2>
          <h3 class="text-primary text-center">Gangs of the Underhive</h3>
        </b-col>
      </b-row>
      <b-row>
        <b-col>
          <b-img fluid src="~/assets/img/goliath.jpg"></b-img>
          <ClassesLinks :house="'goliath'" :landing="true" />
        </b-col>
        <b-col>
          <b-img fluid src="~/assets/img/esher.jpg"></b-img>
          <ClassesLinks :house="'esher'" :landing="true" />
        </b-col>
        <b-col>
          <b-img fluid src="~/assets/img/orlock.jpg"></b-img>
          <ClassesLinks :house="'orlock'" :landing="true" />
        </b-col>
      </b-row>
    </b-container>
  </div>
</template>

<script>
import ClassesLinks from '../components/navigation/ClassesLinks';

export default {
  components: {
    ClassesLinks,
  },
};
</script>

<style lang="scss"></style>
