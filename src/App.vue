<template>
  <div id="app">
    <router-view />
  </div>
</template>
<script>

</script>
<style lang="scss">
body {
  font-family: "Roboto", sans-serif;
}
*,
*::before,
*::after {
  margin: 0;
  padding: 0;
  box-sizing: border-box !important;
}
h1,
h2,
h3,
h4,
h5,
h6,
label {
  text-transform: capitalize;
  > span {
    text-transform: lowercase;
  }
}
p {
  cursor: default;
  font-size: 1.1rem;
  line-height: 1.6;
}
li,
a {
  text-decoration: none;
  list-style-type: none;
}
.input {
  display: block;
  width:100%;
  height: 100%;
  padding: .5rem 1rem;
  border-radius: .75rem;
  appearance: none;
  border:none;
  outline:none;
  box-shadow: none;
  background: #FFF;
  color: #313131;
  transition: all .2s ease-in-out;
  &:focus {
    box-shadow: .1rem .2rem 1rem rgba(0,0,0,.25) ;
  }
}
$breakpoints-up: (
  "sm": "567px",
  "md": "768px",
  "lg": "992px",
  "xl": "1200px",
  "xxl": "1400px",
);
$breakpoints-down: (
  "xs": "566px",
  "sm": "767px",
  "md": "991px",
  "lg": "1199px",
  "xl": "1399px",
);
$container: (
  "xs": "460px",
  "sm": "720px",
  "md": "940px",
  "lg": "1024px",
  "xl": "1300px",
);

@mixin breakpoint-up($size) {
  @media (min-width: map-get($breakpoints-up, $size)) {
    @content;
  }
}
@mixin breakpoint-down($size) {
  @media (max-width: map-get($breakpoints-down, $size)) {
    @content;
  }
}
.container {
  width: 100%;
  padding-right: var(--bs-gutter-x, 0.75rem);
  padding-left: var(--bs-gutter-x, 0.75rem);
  margin-right: auto;
  margin-left: auto;
  @include breakpoint-up(sm) {
    max-width: 540px;
  }
  @include breakpoint-up(md) {
    max-width: 720px;
  }
  @include breakpoint-up(lg) {
    max-width: 960px;
  }
  @include breakpoint-up(xl) {
    max-width: 1140px;
  }
  @include breakpoint-up(xxl) {
    max-width: 1320px;
  }
}
</style>
