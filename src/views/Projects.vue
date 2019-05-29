<template>
  <div class="project">
    <h1 class="subheading grey--text">Project</h1>

    <v-container class="my-5">
      <v-expansion-panel>
        <v-expansion-panel-content v-for="project in myProjects" :key="project.title">
          <div slot="header">{{project.title}}</div>
          <v-card>
            <v-card-text class="px-4 grey--text" >
              <div class="font-weight-bold">
                {{project.due}}
              </div>
                {{project.content}}
            </v-card-text>
          </v-card>
        </v-expansion-panel-content>
      </v-expansion-panel>
    </v-container>
  </div>
</template>

<script>
export default {
  data(){
    return{
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
    }
  },
  computed:{
    myProjects(){
      return this.projects.filter(project =>{
        return project.person === 'Ninja'
      })
    }
  }
};
</script>
