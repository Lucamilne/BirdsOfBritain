<template>
  <v-container>
    <v-row>
      <v-col
        cols="12"
        md="6"
        lg="4"
        xl="3"
        v-for="bird in sliceOfBirdList"
        :key="birds[bird].name"
      >
        <v-card tile>
          <v-list-item three-line>
            <v-list-item-content>
              <div class="overline mb-4">
                {{ birds[bird].population.type }}
              </div>
              <v-list-item-title class="headline mb-1">
                {{ birds[bird].name }}
              </v-list-item-title>
              <v-list-item-subtitle>{{
                birds[bird].scientificName
              }}</v-list-item-subtitle>
            </v-list-item-content>
            <v-list-item-avatar tile size="120" color="grey lighten-4">
              <img
                :src="require(`../assets/birds/${birds[bird].images[0]}`)"
                :alt="birds[bird].name"
              />
            </v-list-item-avatar>
          </v-list-item>
          <v-card-actions>
            <v-btn
              text
              color="primary"
              @click.stop="
                $router.push({
                  name: 'birds',
                  params: { id: toKebabCase(bird) },
                })
              "
              >Learn more</v-btn
            >
          </v-card-actions>
        </v-card>
      </v-col>
    </v-row>
    <div class="text-center">
      <v-pagination v-model="page" :length="numberOfPages"></v-pagination>
    </div>
  </v-container>
</template>

<script>
import birds from "@/common/birds.js";

export default {
  name: "Birds",
  data: () => ({
    page: 1,
    resultsPerPage: 24,
    birds: birds.data,
  }),
  computed: {
    sliceOfBirdList() {
      const start = (this.page - 1) * this.resultsPerPage;
      const end = this.page * this.resultsPerPage;

      return Object.keys(birds.data).slice(start, end);
    },
    numberOfPages() {
      return Math.ceil(Object.keys(birds.data).length / this.resultsPerPage);
    },
  },
  methods: {
    toKebabCase(bird) {
      return bird.toLowerCase().replaceAll(" ", "-");
    },
  },
};
</script>

<style scoped>
.v-avatar img {
  object-fit: cover;
}
.position-absolute {
  position: absolute;
}
.bottom {
  bottom: 0;
}
.right {
  right: 0;
}
</style>