<!--

  Take this template as base for your own application.

  For real modularization, all pages are extracted to their own page component in /pages folder.
  You can define the initial page for each view with the URL attribute.
  Initial pages should not require a login (to configure in package.json file).

  Read more about application layouts: https://framework7.io/vue/app-layout.html

-->

<template>

  <!-- Will replace app container -->
  <div id="app">

    <!-- Statusbar -->
    <f7-statusbar></f7-statusbar>

    <!-- Left panel -->
    <f7-panel left reveal layout="dark">
      <f7-view id="left-panel-view" navbar-through :dynamic-navbar="true" url="panel-left"></f7-view>
    </f7-panel>

    <!-- Right panel -->
    <f7-panel right cover layout="dark">
      <f7-view id="right-panel-view" navbar-through :dynamic-navbar="true" url="panel-right"></f7-view>
    </f7-panel>

    <!-- Main view -->
    <f7-views navbar-through>
      <f7-view main url="/home/" :dynamic-navbar="true"></f7-view>
    </f7-views>

  </div>

</template>

<script>
  require('./kitchen-sink-ios.css')
  require('./kitchen-sink-material.css')
  let iosKitchenSinkCode = require('./kitchen-sink-ios.js')
  let materialKitchenSinkCode = require('./kitchen-sink-material.js')
  let iosKitchenSinkHtml = require('./kitchen-sink-ios-html.js')
  let materialKitchenSinkHtml = require('./kitchen-sink-material-html.js')
  module.exports = {
    data: function () {
      return {
        user: {
          name: 'Vladimir',
          lastName: 'Kharlampidi',
          age: 30
        },
        popupOpened: false,
        loginScreenOpened: false,
        pickerOpened: false,
        actionsOpened: false
      }
    },
    computed: {
      themeColor: function () {
        return this.$root.color
      }
    },
    watch: {
      themeColor: function (newColor) {
        this.$root.statusbarBackgroundColor = this.$root.theme === 'material' ? this.$root.colors[this.$root.theme][newColor] : this.$root.config.statusbarBackgroundColor
      }
    },
    methods: {
      onF7Init: function () {
        if (this.$root.theme === 'ios') {
          iosKitchenSinkCode(this.$root)
        } else {
          materialKitchenSinkCode(this.$root)
        }
        this.$$(document).on('page:beforeinit', function (e) {
          if (e.detail.page.url && e.detail.page.url.indexOf('f7ios/index') > -1) {
            this.$$('.popup, .popover, .login-screen, .picker-modal').remove()
            this.$$('#app').append(iosKitchenSinkHtml)
          } else if (e.detail.page.url && e.detail.page.url.indexOf('f7material/index') > -1) {
            this.$$('.popup, .popover, .login-screen, .picker-modal').remove()
            this.$$('#app').append(materialKitchenSinkHtml)
          }
        }.bind(this))
        window.Dom7('.ks-color-theme').on('click', function () {
          window.Dom7('.statusbar-overlay').css('background-color', '')
        })
      }
    }
  }
</script>

<style>
  /* Icon sizes */
  .item-media .fa,
  .swipeout-actions-left .fa,
  .swipeout-actions-right .fa  {
    font-size: 20px;
  }
  .item-media i.icon,
  .item-media i.f7-icons  {
    width: 29px;
    font-size: 29px;
    height: 29px;
    text-align: center;
  }
  .item-media i.f7-icons {
    color: gray;
  }
</style>
