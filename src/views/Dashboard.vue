<template>
  <div class="dashboard">
    <h1 class="subheading grey--text">Dashboard</h1>

    <v-container class="py-5">
      <v-layout row class="mb-3">
        <v-tooltip top>
          <v-btn slot="activator" color="primary">
            <v-btn small flat color="white" @click="sortBy('title')">
              <v-icon left small>folder</v-icon>
              <span class="caption text-lowercase">By Project Name</span>
            </v-btn>
          </v-btn>
          <span>Sorted By projects Name</span>
        </v-tooltip>
        <v-tooltip top>
          <v-btn slot="activator" color="primary">
            <v-btn small flat color="white" @click="sortBy('person')">
              <v-icon left small>person</v-icon>
              <span class="caption text-lowercase">By Person Name</span>
            </v-btn>
          </v-btn>
          <span>Sorted By Person Name</span>
        </v-tooltip>
      </v-layout>

      <v-card flat v-for="project in projects" :key="project.id">
        <v-layout row wrap :class="`pa-3 project ${project.status}`">
          <v-flex xs12 md6>
            <div class="caption gray--text">Project title</div>
            <div>{{project.title}}</div>
          </v-flex>
          <v-flex xs6 sm4 md2>
            <div class="caption gray--text">Person</div>
            <div>{{project.person}}</div>
          </v-flex>
          <v-flex xs6 md2 sm4>
            <div class="caption gray--text">Due by</div>
            <div>{{project.due}}</div>
          </v-flex>
          <v-flex xs2 sm4 md2>
            <div class="right">
              <v-chip
                small
                :class="`${project.status} white--text caption my-2}`"
              >{{project.status}}</v-chip>
            </div>
          </v-flex>
        </v-layout>
        <v-divider></v-divider>
      </v-card>
    </v-container>
  </div>
</template>

<script>
import db from '@/fb'

export default {
  data() {
    return {
      projects: []
       
    };
  },
  methods: {
    sortBy(props) {
      this.projects.sort((a, b) => (a[props] < b[props] ? -1 : 1));
    }
  },
  created(){
    db.collection('projects').onSnapshot(res => {
      const changes = res.docChanges();
      changes.forEach(change =>{
        if(change.type === 'added'){
          this.projects.push({
            ...change.doc.data(),
            id:change.doc.id
          })
        }
      })
    })
  }
};
</script>
<style>
.project.complete {
  border-left: 4px solid #3cd1c3;
}
.project.ongoing {
  border-left: 4px solid #3cd148;
}
.project.overdue {
  border-left: 4px solid #f80830;
}
.v-chip.complete {
  background: #3cd1c3;
}
.v-chip.ongoing {
  background: #3cd148;
}
.v-chip.overdue {
  background: #f80830;
}
</style>
