<template lang="jade">
  .component    
    .ui.container
      h1.ui.huge.header {{article.title}}
      // h4.ui.medium.header {{article.status}}
      NextStage(:article="article")
      br
      br
      Slide(v-if = "article.id !== undefined", :article="article")
      // video(:style="{'background-image': 'url('+article.cover+')'}")
      br
      .tab_container
        input#tab1(type='radio', name='tabs', checked='')
        label(for='tab1')
          i.fa.fa-info-circle
          span 詳細內容
        input#tab2(type='radio', name='tabs')
        label(for='tab2')
          i.fa.fa-calendar
          span 議題時間軸
        input#tab3(type='radio', name='tabs')
        label(for='tab3')
          i.fa.fa-users
          span 參與討論
        // input#tab4(type='radio', name='tabs')
        // label(for='tab4')
        //   i.fa.fa-arrow-circle-right
        //   span 下一階段
        section#content1.tab-content(v-if = "article.id !== undefined")
          Description(:article="article")
        section#content2.tab-content(v-if = "article.id !== undefined")
          Timeline(:article="article")
        section#content3.tab-content(v-if = "article.id !== undefined")
          Discussion(:article="article")  
        // section#content4.tab-content(v-if = "article.id !== undefined")
        //   NextStage(:article="article")
</template>

<script>


import axios from 'axios'
import Slide from './Detail_Topic_Slide.vue'
import Description from './Detail_Topic_Description.vue'
import Discussion from './Detail_Topic_Discussion.vue'
import Timeline from './Detail_Topic_Timeline.vue'
import NextStage from './Detail_Topic_NextStage.vue'

export default {
  name: 'Detial_Topic',
  props: ['allTopics'],
  components: {
      Description,
      Discussion,
      Timeline,
      NextStage,
      Slide
  },
  data () {
    return {
      article:{}, // title & status
      timeline:[], // 時間軸
      polis_link:[], // polis連結
    }
  },
  computed: {
    article:function(){
      var rtName = this.$route.params.tRouteName;
      var t = this.allTopics.filter( (o)=> {
        return o.routeName == rtName;
      })[0];
      if(t===undefined){return new Object()}
      else{return t};
    }
  }
}

</script>

<style scoped lang="scss">
.component {
  position: relative;
  top: 66px;
}

p {
  text-align: center;
}

video {
  min-width: 75%;
  min-height: 50vh;
  background-color: #ccc;
  background-size: cover;
}
.ui.medium.header{
  color:#db2828;
}
.event-list {
  display: flex;
  flex-flow: column nowrap;
  .item {
    display: flex;
    text-align: left;
    padding: 1em;
    font-size: 1.2rem;
    &.dark { background-color: #ccc }
    &.gloom { background-color: #ddd }
    &.light { background-color: #eee }
    .big {
      display: flex;
      align-items: center;
      flex: 1 0 6em;
    }
    .small {
      flex: 2 0 6em;
      font-size: 1.0em;
    }
    .null {
      flex: 4 2;
    }
  }
}

/*
.clickDeselectsHull {
  display: none !important;
}*/

@import url('https://maxcdn.bootstrapcdn.com/font-awesome/4.7.0/css/font-awesome.min.css');

*,
*:after,
*:before {
	-webkit-box-sizing: border-box;
	-moz-box-sizing: border-box;
	box-sizing: border-box;
}

.clearfix:before,
.clearfix:after {
	content: " ";
	display: table;
}

.clearfix:after {
	clear: both;
}

body {
	font-family: sans-serif;
	background: #f6f9fa;
}

h1 {
	color: #ccc;
	text-align: center;
}

a {
  color: #ccc;
  text-decoration: none;
  outline: none;  
}

/*Fun begins*/
.tab_container {
	width: 90%;
	margin: 0 auto;
	padding-top: 25px;
	position: relative;
}

input, section {
  clear: both;
  padding-top: 10px;
  display: none;
}

label {
  font-weight: 700;
  font-size: 18px;
  display: block;
  float: left;
  width: 33.33%;
  padding: 1.5em;
  color: #1b1c1d;
  cursor: pointer;
  text-decoration: none;
  text-align: center;
  background: #f0f0f0;
}

#tab1:checked ~ #content1,
#tab2:checked ~ #content2,
#tab3:checked ~ #content3,
#tab4:checked ~ #content4, {
  display: block;
  padding: 20px;
  background: rgba(204,114,0,0.28);
  color: #1b1c1d;
  border-bottom: 2px solid #f0f0f0;
}
.tab_container .tab-content,
.tab_container .tab-content p,
.tab_container .tab-content h3 {
  -webkit-animation: fadeInScale 0.7s ease-in-out;
  -moz-animation: fadeInScale 0.7s ease-in-out;
  animation: fadeInScale 0.7s ease-in-out;
}
.tab_container .tab-content h3  {
  text-align: center;
}

.tab_container [id^="tab"]:checked + label { // icon bar 
  background: rgba(204,114,0,0.28);
  box-shadow: inset 0 3px #f2711c;
}

.tab_container [id^="tab"]:checked + label .fa { // icon color
  color: #f2711c;
}

label .fa {
  font-size: 1.3em;
  margin: 0 0.4em 0 0;
}

/*Media query*/
@media only screen and (max-width: 900px) {
  label {
    // display: none;
    span {
      font-size: 12px;
    }
    .fa {
      display: block;
      margin: 0;
    }
  }
  
  .tab_container {
    width: 98%;
  }
}

/*Content Animation*/
@keyframes fadeInScale {
  0% {
  	transform: scale(0.9);
  	opacity: 0;
  }
  
  100% {
  	transform: scale(1);
  	opacity: 1;
  }
}

.no_wrap {
  text-align:center;
  color: #0ce;
}
.link {
  text-align:center;
}


</style>
