<template lang="jade">
  .component
    .ui.grid.four.column.padded.doubling.emptyable
      .box.column(v-for="t in list")
        // .inner
        router-link.topic(:to="'/topic/' + t.routeName")

          img(:src ="t.cover || 'http://lorempixel.com/320/240/sports'")
          // .null
          h3.header {{ t.title }}
            // .sub.header {{ t.owner }} 

          .progress_bar
            .progress(v-bind:style="{ width: (t.progress / t.total * 100) + '%' }")
          .progress_text(v-if="t.status==='討論中'") 還有{{Math.floor(t.total - t.progress)}}天
          .progress_text(v-else) 討論已結束
          
</template>

<script>
  export default {
    name: 'box',
    props: ['list'],
    data() {
      return {
        //...
      }
    }
  }
</script>

<style lang="scss" scoped>
  @import "../sass/global.scss";

  @keyframes spin { 100% { -webkit-transform: rotate(360deg); transform:rotate(360deg); } }
  .emptyable:empty::after {
    margin: 1em auto;
    content: "";
    width: 50px;
    height: 50px;
    color: lightcoral;
    animation:spin 3s linear infinite;
    background: url(data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAADIAAAAyCAMAAAAp4XiDAAABfVBMVEUAAADd3d3d3d3d3d3d3d3d3d3d3d3d3d3d3d3d3d3d3d3d3d3d3d3d3d3d3d3d3d3d3d3d3d3d3d3d3d3d3d3d3d3d3d3d3d3d3d3d3d3d3d3d3d3d3d3d3d3d3d3d3d3d3d3d3d3d3d3d3d3d3d3d3d3d3d3d3d3d3d3d3d3d3d3d3d3d3d3d3d3d3d3d3d3d3d3d3d3d3d3d3d3d3d3d3d3d3d3d3d3d3d3d3d3d3d3d3d3d3d3d3d3d3d3d3d3d3d3d3d3d3d3d3d3d3d3d3d3d3d3d3d3d3d3d3d3d3d3d3d3d3d3d3d3d3d3d3d3d3d3d3d3d3d3d3d3d3d3d3d3d3d3d3d3d3d3d3d3d3d3d3d3d3d3d3d3d3d3d3d3d3d3d3d3d3d3d3d3d3d3d3d3d3d3d3d3d3d3d3d3d3d3d3d3d3d3d3d3d3d3d3d3d3d3d3d3d3d3d3d3d3d3d3d3d3d3d3d3d3d3d3d3d3d3d3d3d3d3d3d3d3d3leqQ3AAAAfnRSTlMAAQIDBAUGBwgJCgsMDQ8QERQVFxkaHB4fISIjJCYnKywtLzAxMzc4OTs/QEFCQ0dJSktMTU5PUFFSVFVWW1xeX2FiY2RnaGlscXN3eYWGiIuOj5GSmpueoKKlpqiqq62vsLK1t7rAwcPIzNHX2d7g4uTm6evt7/Hz9ff5+/0C5wS+AAAByklEQVQYGe3BaVsSUQAG0PeOkywSGhK2r6YhlZRtlmWGLRaVJqZl0p6ZlSgKYsz7270wk15mrug8ffUc7HOLXMx+WqoUFqYfnW3FHhipBSrmzmE3yVW6/O5GM8HP1MgHIF07AI3DJdpWcplbN0cm/tC21gUxxavwOmmxpnQ/Ckfb4ArrknlyBh5dFmtGDSjEHYuOqoBLuEyp0AmX9l90dMLlO6XFADzMH7TdQKPrlIphaLygbRYNzApJKwaNV3RYAqohSiPQyHJLHKplkssGNPpmK3QMQhGnNIAdtJ1+MLdB8gkU9yiF0UzkTNqE4h3JefhSJvkcfghKA/CjhdIx+NIaCgXQlAiFQgK+zJB8DF/KJIfhRwulS/AjRikBRbz3kEAzDymZ2GZYJOfHejoEdrBE8gtU63R8exqExnlKl6HKcUsMXkaBZNWEKkWHdQoaY5QyaNBOm3UUGv2UVk00KtGWgtcF1nTDZZyODNzusiYLtyT/+doBVfQDa94LuB0keTvPutwRAUdinHUfDXgV2QsxQdvG9Gi6rz/zpkLbpIBGzwlIV/5SI41mgq/p9jaCXUSfrXNb9WUMeyASQ5M/i9ba4tTwcQP7/tsmD17vR2+KlQEAAAAASUVORK5CYII=) no-repeat;
  }

  .box {
    display: flex !important;
  }

  a {
    // border: 1px solid #DDD;
    box-shadow: 0 3px 1em hsla(0,0,0%,0.1);
    // flex: 1 1 20%;
    display: flex;
    flex-flow: column nowrap;
    @include transition(all .1s ease);
    &:hover {
      margin: 3px -3px -3px 3px;
    }
    img {
      flex: 1 1;
      max-width: 100%;
      height: auto;
    }
    // .null {
    //   flex: 1 1;
    // }
    h3 {
      // flex: 1 1;
      color: black;
      font-family: $main_font;
      // font-size: .8rem;
      margin: .5em;
      // margin-top: .5em;
      // flex: 1;
      // text-align: left;
      .sub.header {
        color: #999;
        font-size: .5em;
      }
    }
    .progress_bar {
      // flex: 0 1;
      background-color: #CCC;
      padding: 0;
      // margin: 3px 0;
      .progress {
        height: 5px;
        background-color: lightcoral;
        // border-radius: 0 5px 0 0;
      }
      margin-bottom: 4px;
    }
    .progress_text {
      font-size: .8rem;
      text-align: right;
    }
  }
  
</style>
