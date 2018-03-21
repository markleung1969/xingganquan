<template>
  <div id="app">
    <router-view/>
  </div>
</template>

<script>
export default {
  name: 'App'
}
</script>

<style>
html,body,div,dl,dt,dd,ul,ol,li,h1,h2,
h3,h4,h5,h6,pre,code,form,fieldset,
legend,input,textarea,p,blockquote,th,td{
    margin:0;
    padding:0;
}

html {
    -webkit-text-size-adjust:none;
    -webkit-appearance:none;
}

body {
    font:14px/2.0 Helvetica,'Microsoft Yahei',serif,sans-serif;
}

a {
    text-decoration:none;
}

table{
    border-collapse:collapse;
    border-spacing:0;
}

fieldset,img{
    border:0;
}

img {
    vertical-align:bottom;
}

address,caption,cite,code,dfn,em,strong,th,var{
    font-style:normal;
    font-weight:normal;
}

ul{
    list-style:none;
}
ol{
    list-style-position:inside;
}

caption,th{
    text-align:left;
}

h1,h2,h3,h4,h5,h6{
    font-size:100%;
    font-weight:normal;
}

/*--某些浏览器中，q或者blockquote前后会出现引号--*/
q:before,
q:after{
    content:'';
}

abbr,acronym{
    border:0;
    font-variant:normal;
}

sup{
    vertical-align:text-top;
}

sub{
    vertical-align:text-bottom;
}

input,textarea,select{
    font-family:inherit;
    font-size:inherit;
    font-weight:inherit;
}

 /*--ie6不支持inherit--*/
input,textarea,select{
    *font-size:100%;
}

legend{
    color:#000;
}

/* 防止注入iframe */
iframe {
    display:none !important;
}

/*- 通用样式 -*/
.clearfix {
    *zoom:1;
}
.clearfix:after,
.clearfx:before {
    content:"";
    display:table;
    line-height:0;
}
.clearfix:after {
  clear: both;
}
.text-center {
    text-align:center;
}
.text-left {
    text-align:left;
}
.text-right {
    text-align:right;
}
.hide {
    display:none;
}
.show {
    display:block;
}
.hidden {
    visibility:hidden;
}
.visibile {
    visibility:visible;
}
.fl {
    float:left;
}
.fr {
    float:right;
}
.inline-block {
    display:inline-block;
}
.block {
    display:block;
}
.inline {
    display:inline;
}
.relative {
    position:relative;
}
.unstyle {
    padding:0;
    margin:0;
    list-style:none;
    text-decoration:none;
}
</style>
