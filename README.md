# bender-router-builder

## Description
Simple express router builder.
Use it if you don`t want to think about the routing of your server application.

![bender](http://dl4.joxi.net/drive/2020/02/19/0014/4067/983011/11/b102f8abb4.jpg "bender")

## Features

1) GET
2) POST
3) Upload file (in development)

## Use

**project**

```
├── features
|   ├── index.js
|   └── users.js
├── ...
├── server.js
└── front.vue
```

**index.js**

```
const buider = require('bender-router-builder')

const path = `${__dirname}`

module.exports = buider({ path: path })
```

> path - path to your api

**users.js**

```
function getUsers (id) {
  const users = [
    { id: 1, name: 'Tom' },
    { id: 2, name: 'Jack' },
    { id: 3, name: 'Max' },
  ]
  
  return users.find(u => u.id === id)
}

module.exports = {
  getUsers
}
```

**or**

**users.js**

```
function getUsers (id) {
  const users = [
    { id: 1, name: 'Tom' },
    { id: 2, name: 'Jack' },
    { id: 3, name: 'Max' },
  ]
  
  return users.find(u => u.id === id)
}

module.exports = getUsers
```

**server.js**

```
const express = require('express')
const app = express()

...

app.use('/', require('../features'))
app.use(express.static(`${__dirname}/../features`))

...
```

**front.vue**

```
<template>
 ...
</template>

<script>
  import axios from 'axios'

  export default {
    async mounted () {
      const users = await axios({
        method: 'get',
        url: '/users.getUsers',
        params: id,
      })
      .then(r => r.data)
    }
  }
</script>
```
