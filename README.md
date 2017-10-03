vuejs-storage
==============
*vue.js and vuex plugin to persistence data with localStorage/sessionStorage*
--------------

[example code](https://github.com/maple3142/vuejs-storage/blob/master/example.html)
```html
<!DOCTYPE html>
<html lang="en">

<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <meta http-equiv="X-UA-Compatible" content="ie=edge">
  <title>example</title>
  <script src="dist/vuejs-storage.js"></script>
  <!--import from cdn-->
  <!--script src="https://unpkg.com/vuejs-storage"></script-->
  <script src="https://unpkg.com/vue"></script>
  <script src="https://unpkg.com/vuex"></script>
</head>

<body>
  <div id="app">
    <div>
      <span>Vue counter: {{count}}</span>
      <button @click="add">add</button>
    </div>
    <div>
      <span>Vuex counter: {{vuexcount}}</span>
      <button @click="vuexadd">add</button>
    </div>
  </div>
  <div id="app2">
    <div>
      <span>sessionStorage counter: {{count}} {{message}}</span>
      <button @click="add">add</button>
    </div>
  </div>
  <script>
    Vue.use(Vuex)
    Vue.use(vuejsStorage)

    const store = new Vuex.Store({
      state: {
        count: 0
      },
      mutations: {
        increment(state) {
          state.count++
        }
      },
      plugins: [new vuejsStorage.Storage({ namespace: 'vuex-app' }).plugin()]
    })

    var app = new Vue({
      el: '#app',
      storage: new vuejsStorage.Storage({
        data: {
          count: 0
        },
        namespace: 'app'
      }),
      methods: {
        add: function () {
          this.count++
        },
        vuexadd: function () {
          store.commit('increment')
        }
      },
      computed: {
        vuexcount() {
          return store.state.count
        }
      }
    })

    //advanced example
    var app2 = new Vue({
      el: '#app2',
      data: {
        message: 'Hello'
      },
      storage: function () { //function syntax is ok
        return new vuejsStorage.Storage({
          data: {
            count: 0
          },
          storage: sessionStorage,
          namespace: 'app2'
        })
      },
      methods: {
        add: function () {
          this.count++
        }
      }
    })
  </script>
</body>

</html>
```

[codepen example](https://codepen.io/maple3142/full/eGNMBK/)
[simple todo list](https://codepen.io/maple3142/full/MEagWw/)
-----------