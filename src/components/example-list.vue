<template>
  <list>
    <cell v-for="item in items" append="tree">
      <example-list-item :title="item.title" :url="item.url"></example-list-item>
    </cell>
  </list>
</template>

<script>
  var getBaseURL = require('utils').getBaseURL
  module.exports = {
    props: {
      dir: {
        default: 'examples'
      }, // examples, test ...
      items: {
        default: [
          {name: 'hello', title: 'Hello World', url: ''}
        ]
      }
    },
    components: {
      exampleListItem: require('./example-list-item.vue')
    },
    created: function() {
      var base = getBaseURL(weex)
      for (var i in this.items) {
        var item = this.items[i];
        if (!item.url) {
          item.url = base + item.name + '.js';
          console.log('item.url='+item.url);
        }
      }
    }
  }
</script>
