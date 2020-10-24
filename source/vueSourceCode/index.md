---
title: Vue2.x源码
date: 2020-10-23 13:21:00
type: 'vue'
comments: false

---

# [响应式原理](/vue2.x源码/响应式原理/)

<style>
  .layout_page h1 {
    position: relative;
    width: 25%;
    padding: 0;
    border-radius: 10px;
    transition-duration: .3s;
    margin-bottom: 1rem;
    margin-left: 16px;
    display: block;
    float: left;
    box-shadow: 0 2px 6px 0 rgba(0,0,0,.12);
    background-image: linear-gradient(to right, #eea2a2 0%, #bbc1bf 19%, #57c6e1 42%, #b49fda 79%, #7ac5d8 100%);
      background-size: 400% 400%;
    animation: gradientBG 10s ease infinite;
    overflow: hidden;
    font-size: 20px;
    text-align: center;
  }
  .layout_page h1 a {
    color: #fff !important;
  }
  .layout_page h1:hover:before, .card:focus:before, .card:active:before {
    -webkit-transform: scale(1);
    transform: scale(1);
  }

  .layout_page h1:before {
    content: "";
    position: absolute;
    z-index: -1;
    top: 0;
    left: 0;
    right: 0;
    bottom: 0;
    background-image: linear-gradient(to right, #23a6d5 0%, #23a6d5 1%, #a1c4fd 100%);
    -webkit-transform: scale(0);
    transform: scale(0);
    -webkit-transition-property: transform;
    transition-property: transform;
    -webkit-transition-duration: 0.15s;
    transition-duration: all 0.15s;
    -webkit-transition-timing-function: ease-out;
    transition-timing-function: ease-out;
  }
  .layout_page h1:hover {
    transform:scale(1);
  }
  .layout_page h1:hover a {
    color: #fff !important;
  }
  #article-container a:last-child {
    display: inline-block;
    width: 100%;
  }
</style>