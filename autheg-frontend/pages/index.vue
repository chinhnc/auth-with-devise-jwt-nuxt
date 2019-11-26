<template>
  <v-layout>
    <v-flex>
      <v-list>
        <v-list-item-group color="primary">
          <v-list-item
            v-for="example in examples"
            :key="example.id"
            :class="example.colour"
          >
            <v-list-item-content>
              <v-list-item-title v-text="example.name"></v-list-item-title>
            </v-list-item-content>
          </v-list-item>
        </v-list-item-group>
      </v-list>
    </v-flex>
  </v-layout>
</template>

<script>
export default {
  middleware: 'auth',
  data () {
    return {
      examples: []
    }
  },
  methods: {
    async updateExamples() {
      this.examples = await this.$axios.$get('/examples')
    }
  },
  mounted () {
    this.updateExamples()
  }
}
</script>
