<template>
  <v-container>
    <v-item-group v-model="selected">
      <v-row>
        <v-col v-for="(family, i) in families" :key="i" cols="6" md="3">
          <v-item v-slot="{ active, toggle }">
            <v-card
              tile
              :color="active ? 'primary' : 'white'"
              class="d-flex align-center"
              :dark="active ? true : false"
              @click="
                toggle;
                $router.push({
                  name: 'families',
                  params: { id: toKebabCase(family) },
                });
              "
            >
              <v-responsive :aspect-ratio="4 / 3" class="d-flex align-center">
                <div class="overline text-center">
                  {{ family }}
                </div>
              </v-responsive>
            </v-card>
          </v-item>
        </v-col>
      </v-row>
    </v-item-group>
  </v-container>
</template>

<script>
import birds from "@/common/birds.js";

export default {
  name: "Families",
  data: function () {
    return {
      selected: null,
      birds: birds.data,
      families: Object.keys(birds.birdsByFamily),
      birdsByFamily: birds.birdsByFamily,
    };
  },
  methods: {
    toKebabCase(family) {
      return family.toLowerCase().replaceAll(" ", "-");
    },
  },
};
</script>
