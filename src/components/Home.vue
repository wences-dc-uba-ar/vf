<template>
  <v-container>

    <v-layout 
      row 
      wrap>
      <v-flex 
        xs12 
        sm6 
        class="text-xs-center text-sm-right">
        <v-btn 
          large 
          color="success" 
          router 
          to="/meetups">Explore Meetups</v-btn>
      </v-flex>
      <v-flex 
        xs12 
        sm6 
        class="text-xs-center text-sm-left">
        <v-btn 
          large 
          color="success" 
          router 
          to="/meetup/new">Organize Meetups</v-btn>
      </v-flex>
    </v-layout>

    <v-layout 
      row 
      wrap>
      <v-flex 
        xs12 
        class="text-xs-center">
        <v-progress-circular
          indeterminate
          color="red"
          :width="7"
          :size="100"
          v-if="loading"
        />
      </v-flex>
    </v-layout>

    <v-layout 
      row 
      wrap 
      class="mt-2" 
      v-if="!loading">
      <v-flex xs12>
        <v-carousel>
          <v-carousel-item
            v-for="meetup in meetups"
            :key="meetup.id"
            :src="meetup.imageUrl"
            @click="onLoadMeetup(meetup.id)"
            style="cursor: pointer">
            <div class="title">
              {{ meetup.title }}
            </div>
          </v-carousel-item>
        </v-carousel>
      </v-flex>
    </v-layout>

    <v-layout 
      row 
      wrap 
      class="mt-2">
      <v-flex 
        xs12 
        class="text-xs-center">
        <p>Join our awesome meetup</p>
      </v-flex>
    </v-layout>

  </v-container>
</template>

<script>
export default {
  computed: {
    meetups() {
      //   return this.$store.getters.loadedMeetups
      return this.$store.getters.featuredMeetups;
    },
    loading() {
      return this.$store.getters.loading;
    }
  },
  data() {
    return {};
  },
  methods: {
    onLoadMeetup(id) {
      console.log(id);
      this.$router.push("/meetup/" + id);
    }
  }
};
</script>

<style>
.title {
  position: absolute;
  bottom: 50px;
  background-color: rgba(0, 0, 0, 0.5);
  color: white;
  font-size: 2em;
  padding: 20px;
  width: 100%;
  text-align: center;
}
</style>
