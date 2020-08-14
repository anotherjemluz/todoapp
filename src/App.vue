<template lang="pug">
  #app
    transition
      router-view

</template>

<style lang="scss">
@import url('https://cdn.bootcss.com/font-awesome/4.7.0/css/font-awesome.css');
@import url('https://fonts.googleapis.com/css2?family=Baloo+Tamma+2:wght@400;600&display=swap');

* {
  margin: 0;
  padding: 0;
}

a {
  text-decoration: inherit;
}

ul,
ol {
  list-style: none;
}

h1,
h2,
h3,
h4 {
  font: inherit;
}

input,
select,
button {
  font: inherit;
}

html,
body {
  height: 100%;
  -webkit-user-select: none;
  -webkit-touch-callout: none;
  -webkit-tap-highlight-color: transparent;
}

body {
  font-family: 'Baloo Tamma 2', cursive;
}

#app {
  height: 100%;
  overflow: hidden;
}
</style>
