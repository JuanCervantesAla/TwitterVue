<template>
  <q-page>
    <div class="q-py-lg q-px-md row items-end q-col-gutter-md">

      <div class="col">
        <q-input bottom-slots v-model="newQweetContent"  class="new-qweet" placeholder="What's happening?" counter maxlength="280" autogrow>
          <template v-slot:before>
            <q-avatar size="xl">
              <img src="https://cdn.donmai.us/sample/d5/a5/__alice_lendrott_and_bocchan_shinigami_bocchan_to_kuro_maid_drawn_by_inoue_koharu__sample-d5a50cecc522523315df0e1245022b67.jpg">
            </q-avatar>
          </template>
        </q-input>
      </div>

      <div class="col col-shrink">
        <q-btn @click="addNewQweet" :disable="!newQweetContent" class="q-mb-lg" unelevated rounded color="primary" label="Emitt" no-caps/>
      </div>

    </div>

    <q-separator size="10px" color="grey-2" class="divider" />

    <q-list separator>
    <transition-group appear enter-active-class="animated fadeIn slow" leave-active-class="animated fadeOut slow">
      <q-item class="q-py-md" v-for="qweet in qweets" :key="qweet.date" >
        <q-item-section avatar top>
          <q-avatar size="xl">
              <img src="https://cdn.donmai.us/sample/d5/a5/__alice_lendrott_and_bocchan_shinigami_bocchan_to_kuro_maid_drawn_by_inoue_koharu__sample-d5a50cecc522523315df0e1245022b67.jpg">
            </q-avatar>
        </q-item-section>

        <q-item-section>
          <q-item-label class="text-subtitle1">
            <strong>Juan Jose Emiliano</strong>
            <span class="text-grey-7">@elgrueson <br class="lt-md">&bull; {{ relativeDate(qweet.date) }}</span>
          </q-item-label>
          <q-item-label class="qweet-content text-body1">{{qweet.content}}
          </q-item-label>

          <div class="qweet-icons row justify-between q-mt-sm">
            <q-btn flat round color="grey" size="sm" icon="far fa-comment"/>
            <q-btn flat round color="grey" size="sm" icon="fas fa-retweet"/>
            <q-btn flat round color="grey" size="sm" icon="far fa-heart"/>
            <q-btn @click="deleteQweet(qweet)" flat round color="grey" size="sm" icon="fas fa-trash"/>
          </div>
        </q-item-section>

      </q-item>
    </transition-group>
    </q-list>
  </q-page>
</template>

<script setup>
import { formatDistance } from 'date-fns';
defineOptions({
  name: 'PageHome',
  data(){
    return{
    newQweetContent: '',
    qweets:[
        {
          content: 'El capibara, conocido como el roedor más grande del mundo, es a menudo considerado como el mejor amigo por varias razones que destacan su naturaleza amistosa, sociabilidad y características únicas. ',
          date: 1727770022372

        },
        {
          content: 'El oso hormiguero, a pesar de ser un animal fascinante, a menudo no recibe la misma atención o cariño que otras especies más populares.  ',
          date: 1727770056045

        },
        {
          content: 'Hola gente esto en un Emeett no un tweet Porque pues uno siempre original la verdad Arriba los raiders /n ~Espresso',
          date: 1727771156045
        },
      ]
    }
  },
  methods: {
    addNewQweet(){
      let newQweet = {
        content: this.newQweetContent,
        date: Date.now()
      }
      this.qweets.unshift(newQweet)
      this.newQweetContent = '' 
    },

    deleteQweet(qweet){
      let dateToDelete = qweet.date
      let index = this.qweets.findIndex(qweet => qweet.date === dateToDelete)
      this.qweets.splice(index, 1)
    },

    relativeDate(value){
      const dateValue = new Date(value);
      return formatDistance(dateValue, new Date(), { addSuffix: true });
    }


  }
});
</script>

<style lang="sass">
.new-qweet
  textarea
    font-size: 19px
    line-height: 1.4

.divider 
  border-top: 1px solid
  border-bottom: 1px solid
  border-color: $grey-4

.qweet:not(:first-child)
  border-top: 1px solid rgba(0,0,0,0.12)

.qweet-content
  white-space: pre-line

.qweet-icons
  margin-left: -5px

</style>
