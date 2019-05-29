<template>
  <div class="dashboard">
    <h1 class="subheading grey--text">Dashboard</h1>

    <v-container class="my-5">
      <v-layout row class="mb-3">
        <!--按键提示-->
        <v-tooltip top>
          <v-btn small flat color="grey" @click="sortBy('title')" slot="activator">
            <v-icon left small>folder</v-icon>
            <span class="caption text-lowercase">By project</span>
          </v-btn>
          <span>sort project by title</span>
        </v-tooltip>

        <v-tooltip top>
          <v-btn small flat color="grey" @click="sortBy('person')" slot="activator">
            <v-icon left small>person</v-icon>
            <span class="caption text-lowercase">By person</span>
          </v-btn>
          <span>sort projects by person</span>
        </v-tooltip>
      </v-layout>

      <!--卡片内容-->
      <v-card flat class="pa-3" v-for="project in projects" :key="project.id">
        <v-layout row wrap :class="`pa-3 project.${project.title}`">
          <v-flex xs12 md6>
            <div class="caption grey--text">title</div>
            <div>{{project.title}}</div>
          </v-flex>

          
          <v-flex xs6 sm4 md2>
            <div class="caption grey--text">preson</div>
            <div>{{project.guestInfo}}</div>
          </v-flex>

          <v-flex xs6 sm4 md2>
            <div class="caption grey--text">Dua by</div>
            <div>{{project.due}}</div>
          </v-flex>

          <v-flex xs6 sm4 md2>
            <div>
              <v-chip small :class="`dark--text caption`">{{project.status}}</v-chip>
            </div>
          </v-flex>
        </v-layout>
      </v-card>
    </v-container>

    <!--测试项-->
    <v-layout>
      <v-flex xs12 sm6 offset-sm3>
        <v-card>
          <v-img
            class="white--text"
            height="200px"
            src="https://cdn.vuetifyjs.com/images/cards/docks.jpg"
          >
            <v-container fill-height fluid>
              <v-layout fill-height>
                <v-flex xs12 align-end flexbox>
                  <span class="headline">{{this.projects[0].title}}</span>
                </v-flex>
              </v-layout>
            </v-container>
          </v-img>
          <v-card-title>
            <div>
              <span class="grey--text">Number 10</span>
              <br>
              <span>{{this.projects[0].guestInfo}}</span>
              <br>
              <span>{{this.projects[0].content}}</span>
            </div>
          </v-card-title>
          <v-card-actions>
            <v-btn flat color="orange">Share</v-btn>
            <v-btn flat color="orange">Explore</v-btn>
          </v-card-actions>
        </v-card>
      </v-flex>
    </v-layout>

    <span>-------------------------------------------------------------------</span>

    <p
      class="red white--text"
    >Lorem ipsum dolor sit, amet consectetur adipisicing elit. Omnis suscipit corrupti possimus eligendi culpa fugit quo, dicta hic voluptates cupiditate temporibus est, nobis consequatur ipsa dolorum iure quam et. Eaque.</p>
    <p
      class="red lighten-4 red--text text--darken-4"
    >Lorem ipsum dolor sit, amet consectetur adipisicing elit. Omnis suscipit corrupti possimus eligendi culpa fugit quo, dicta hic voluptates cupiditate temporibus est, nobis consequatur ipsa dolorum iure quam et. Eaque.</p>
    <h1 class="display-4">massive display</h1>
    <h4 class="display-1">Hello world</h4>
    <p class="headline">This is a headline</p>
    <v-btn depressed class="pink white--text">
      <v-icon left>email</v-icon>
      <span>click me</span>
    </v-btn>

    <v-btn depressed small class="pink white--text">
      <v-icon left>email</v-icon>
      <span>click me</span>
    </v-btn>

    <v-btn depressed large class="pink white--text">
      <span>click me</span>
      <v-icon right>email</v-icon>
    </v-btn>

    <v-btn fab depressed large dark color="purple">
      <v-icon>favorite</v-icon>
    </v-btn>
  </div>
</template>

<script>
import { constants } from "crypto";
export default {
  mounted: function() {
    this.axios
      .get(
        "http://ec2-15-164-103-237.ap-northeast-2.compute.amazonaws.com:3000/board/getGuestList"
      )
      .then(response => {
        console.log(response.data);
        this.boards = response.data;
      });
  },
  data() {
    return {
      boards: [],
      projects: [
        {
          title: "Design a new webside",
          person: "Ninja",
          due: "20190307",
          status: "ongoing",
          content:
            "尝试Vue.js 最简单的方法是使用JSFiddle 上的Hello World 例子。你可以在浏览器新标签页中打开它，跟着例子学习一些基础用法。或者你也可以创建一个 .html 文件，"
        },
        {
          title: "Code up the sign page",
          person: "chun li",
          due: "20190408",
          status: "complete",
          content:
            "尝试Vue.js 最简单的方法是使用JSFiddle 上的Hello World 例子。你可以在浏览器新标签页中打开它，跟着例子学习一些基础用法。或者你也可以创建一个 .html 文件，"
        },
        {
          title: "Design a new webside",
          person: "Ninja",
          due: "20190307",
          status: "ongoing",
          content:
            "尝试Vue.js 最简单的方法是使用JSFiddle 上的Hello World 例子。你可以在浏览器新标签页中打开它，跟着例子学习一些基础用法。或者你也可以创建一个 .html 文件，"
        },
        {
          title: "create a community for formu",
          person: "khalil",
          due: "20190307",
          status: "overdue",
          content:
            "尝试Vue.js 最简单的方法是使用JSFiddle 上的Hello World 例子。你可以在浏览器新标签页中打开它，跟着例子学习一些基础用法。或者你也可以创建一个 .html 文件，"
        }
      ]
    };
  },
  methods: {
    sortBy(prop) {
      this.projects.sort((a, b) => (a[prop] < b[prop] ? -1 : 1));
    }
  }
};
</script>

<style>
.project.ongoing {
  border-left: 4px solid green;
}
.project.ongoing {
  border-left: 4px solid blue;
}
.project.overdue {
  border-left: 4px solid red;
}
</style>
