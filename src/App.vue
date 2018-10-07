<template>
  <v-app>
    <v-jumbotron class="login-jumbotron" height="100%">
      <v-container fluid fill-height>
    <v-layout row>
        <v-flex xs12 sm6 offset-sm3>
          <v-card>
            <v-img
              :src="require('@/assets/mike.jpg')"
              height="300px"
            >
              <v-layout
                column
                fill-height
              >
                <v-card-title>
                  <v-btn dark icon>
                    <v-icon medium @click="categoryChange('General')">person</v-icon>
                  </v-btn>

                  <v-btn dark icon>
                    <v-icon medium @click="categoryChange('Socials')">message</v-icon>
                  </v-btn>

                  <v-spacer></v-spacer>

                  <v-btn dark icon class="mr-3">
                    <v-icon medium @click="categoryChange('Contact')">phone</v-icon>
                  </v-btn>

                  <v-btn dark icon>
                    <v-icon medium @click="categoryChange('Skills')">local_library</v-icon>
                  </v-btn>

                  <v-btn dark icon>
                    <v-icon medium @click="categoryChange('Education')">school</v-icon>
                  </v-btn>

                  <v-btn dark icon>
                    <v-icon medium @click="categoryChange('Experience')">domain</v-icon>
                  </v-btn>
                  
                </v-card-title>

                <v-spacer></v-spacer>

                <v-card-title class="white--text pl-5 pt-5">
                  <div class="display-1 pl-5 pt-5"><br> <v-icon large dark>local_cafe</v-icon>  Michael Awad: Developer<br> {{ category }}</div>
                </v-card-title>
              </v-layout>
            </v-img>

            <v-list two-line>
              <v-list-tile v-show="category === 'Contact' " v-for ="item in cvData.categories.contact" v-bind:key="item.value">
                <v-list-tile-action>
                  <v-icon color="primary" medium>{{item.icon}}</v-icon>
                </v-list-tile-action>

                <v-list-tile-content>
                  <v-list-tile-title>{{item.value}}</v-list-tile-title>
                  <v-list-tile-sub-title>{{item.type}}</v-list-tile-sub-title>
                </v-list-tile-content>

                <v-list-tile-action>
                  <v-icon medium color="primary">done</v-icon>
                </v-list-tile-action>
              </v-list-tile>

                <v-list-tile v-if="category === 'General'" v-for="item in cvData.categories.general" v-bind:key="item.value">
                <v-list-tile-action>
                  <v-icon medium color="primary">{{item.icon}}</v-icon>
                </v-list-tile-action>

                <v-list-tile-content>
                  <v-list-tile-title>{{item.value}}</v-list-tile-title>
                  <v-list-tile-sub-title>{{item.type}}</v-list-tile-sub-title>
                </v-list-tile-content>

                <v-list-tile-action>
                  <v-icon medium color="primary">done</v-icon>
                </v-list-tile-action>
              </v-list-tile>

              <v-list-tile v-if="category === 'Skills'" v-for="item in cvData.categories.skills" v-bind:key="item.name">
                <v-list-tile-action>
                  <v-icon medium color="primary">local_library</v-icon>
                </v-list-tile-action>

                <v-list-tile-content>
                  <v-list-tile-title>{{item.name}}</v-list-tile-title>
                  <v-list-tile-sub-title>
                    {{item.language}}
                </v-list-tile-sub-title>
            
                </v-list-tile-content>

                <v-list-tile-action>
                  <v-progress-circular
                    :rotate="360"
                    :size="40"
                    :width="4"
                    :value="item.skill"
                    color=#1eff38
                  >
                    {{ item.skill }}
                  </v-progress-circular>
                </v-list-tile-action>
              </v-list-tile>

              <v-list-tile v-if="category === 'Education'" v-for="item in cvData.categories.education" v-bind:key="item.instance">
                <v-list-tile-action>
                  <v-icon medium color="primary">school</v-icon>
                </v-list-tile-action>

                <v-list-tile-content>
                  <v-list-tile-title>{{item.instance}}</v-list-tile-title>
                  <v-list-tile-sub-title>{{item.degree}}</v-list-tile-sub-title>
                </v-list-tile-content>

                <v-list-tile-action>
                  {{item.year}}
                </v-list-tile-action>
              </v-list-tile>

              <v-list-tile v-if="category === 'Experience'" v-for="item in cvData.categories.experience" v-bind:key="item.employer">
                <v-list-tile-action>
                  <v-icon medium color="primary">domain</v-icon>
                </v-list-tile-action>

                <v-list-tile-content>
                  <v-list-tile-title>{{item.employer}}</v-list-tile-title>
                  <v-list-tile-sub-title>{{item.role}}</v-list-tile-sub-title>
                </v-list-tile-content>

                <v-list-tile-action>
                  {{item.when}}
                </v-list-tile-action>
              </v-list-tile>

              <v-list-tile v-if="category === 'Socials'" v-for="item in cvData.categories.social" v-bind:key="item.type">
              <v-list-tile-action>
                  <v-avatar v-for="image in socialImages" v-bind:key="image.twitter">
                  <img v-show="item.type === 'Twitter'" :src="image.twitter">
                  <img v-show="item.type === 'Google'" :src="image.google">
                  <img v-show="item.type === 'Github'" :src="image.github">
                  <img v-show="item.type === 'linkedIn'" :src="image.linkedin">
                  </v-avatar>
              </v-list-tile-action>

              <v-list-tile-content>
                <v-list-tile-title>{{item.type}}</v-list-tile-title>
                <v-list-tile-sub-title>{{item.value}}</v-list-tile-sub-title>
              </v-list-tile-content>

                <v-list-tile-action>
                  <v-icon medium color="primary">whatshot</v-icon>
                </v-list-tile-action>
            </v-list-tile>
            </v-list>
          </v-card>
        </v-flex>
      </v-layout>
      </v-container>
    </v-jumbotron>
  </v-app>
</template>

<script>
import cvData from './assets/cvData.json'

export default {
  name: 'App',
  data () {
    return {
      socialImages:[{
        twitter: require('@/assets/twitter.png'),
        google: require('@/assets/google.png'),
        github: require('@/assets/github.png'),
        linkedin: require('@/assets/linkedin.png'),
      }],
      category: 'Contact',
      cvData: cvData,
      clipped: false,
      drawer: true,
      fixed: false,
      items: [{
        icon: 'bubble_chart',
        title: 'Inspire'
      }]
    }
  },
  methods: {
    categoryChange(category) {
      this.category = category
    }
  }
}
</script>
<style scoped>
.login-jumbotron {
  background-image: url("assets/deskbg.jpeg");
}
</style>