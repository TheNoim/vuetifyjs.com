<template>
  <v-layout column>
    <v-flex xs12>
      <div class="resultContainer">
        <v-layout v-bind="layoutAttributes">
          <div class="item elevation-5"></div>
          <div class="item elevation-5"></div>
          <div class="item elevation-5"></div>
        </v-layout>
      </div>
    </v-flex>
    <v-flex xs12>
      <v-layout column xs12>
        <div>
          <v-layout row>
            <v-flex xs12 md4>
              <v-radio-group v-model="alignment">
                <v-radio
                  v-for="n in alignmentsAvailable"
                  :key="n"
                  :label="n === '' ? 'Nothing' : n"
                  :value="n"/>
              </v-radio-group>
            </v-flex>
            <v-flex xs12 md4>
              <v-radio-group v-model="justify">
                <v-radio
                  v-for="n in justifyAvailable"
                  :key="n"
                  :label="n === '' ? 'Nothing' : n"
                  :value="n"/>
              </v-radio-group>
            </v-flex>
            <v-flex xs12 md4>
              <v-layout column>
                <v-radio-group v-model="flexDirection">
                  <v-checkbox
                    label="reverse"
                    v-model="reverse"
                    hide-details/>
                  <v-checkbox
                    label="fill-height"
                    v-model="fillHeight"
                    hide-details/>
                  <v-radio
                    v-for="n in flexDirectionAvailable"
                    :key="n"
                    :label="n"
                    :value="n"/>
                </v-radio-group>
              </v-layout>
            </v-flex>
          </v-layout>
        </div>
      </v-layout>
    </v-flex>
    <v-flex xs12>
      <h5>Output:</h5>
      <code>{{formatAttributes(layoutAttributes)}}</code>
    </v-flex>
  </v-layout>
</template>

<script>
  export default {
    data() {
      return {
        alignmentsAvailable: ['align-center', 'align-end', 'align-space-around', 'align-space-between', 'align-start', ''],
        alignment: 'align-center',
        justifyAvailable: ['justify-center', 'justify-end', 'justify-space-around', 'justify-space-between', 'justify-start', ''],
        justify: 'justify-center',
        reverse: false,
        flexDirectionAvailable: ['row', 'column'],
        flexDirection: 'row',
        fillHeight: true
      };
    },
    computed: {
      layoutAttributes() {
        return {
          [this.alignment]: true,
          [this.justify]: true,
          [this.flexDirection]: true,
          reverse: this.reverse,
          ['fill-height']: this.fillHeight
        };
      }
    },
    methods: {
      formatAttributes(attributes) {
        const attributeArray = [];
        for (const Key in attributes) {
          if (!attributes.hasOwnProperty(Key) || Key === '' || attributes[Key] === false) continue;
          attributeArray.push(Key.trim());
        }
        return `<v-layout ${attributeArray.join(' ')}/>`;
      }
    }

  }
</script>

<style scoped>
  .resultContainer {
    height: 350px;
  }

  .item {
    min-height: 50px;
    min-width: 100px;
    margin: 10px;
  }
</style>
