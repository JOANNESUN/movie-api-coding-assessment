<template>
  <div id="app">
    <section class="navigation">
      <div class="nav-container">
        <div class="brand">
          <a href="#!">Martin's Movie</a>
        </div>
        <nav>
          <div class="nav-mobile">
            <a id="nav-toggle" href="#!"><span></span></a>
          </div>
          <ul class="nav-list">
            <li>
              <a href="#!">Home</a>
              <ul class="nav-dropdown"></ul>
            </li>
            <li>
              <a href="#!">Pages</a>
              <ul class="nav-dropdown"></ul>
            </li>
            <li>
              <a href="#!">Movies & Shows</a>
              <ul class="nav-dropdown"></ul>
            </li>
            <li>
              <a href="#!">Blog</a>
              <ul class="nav-dropdown"></ul>
            </li>
            <li>
              <a href="#!">Contact US</a>
              <ul class="nav-dropdown"></ul>
            </li>
            <li>
              <button>&#128100; LOGIN</button>
            </li>
          </ul>
        </nav>
      </div>
    </section>
    <section class="hero">
      <div class="titleSection">
        <h1 style="padding: 1em">Movie Grid</h1>
      </div>
      <div class="titleSection">
        <h5 style="padding: 0 0 0 2em">Home | Movie Grid</h5>
      </div>
    </section>

    <ContentPage />
  </div>
</template>

<script>
import ContentPage from "./components/ContentPage";

export default {
  name: "App",
  components: {
    ContentPage,
  },
  data() {
    return {
      burgerVisibility: false,
    };
  },
  methods: {
    changeVisibility() {
      this.burgerVisibility = !this.burgerVisibility;
    },
  },
};
</script>

<style>
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

/* nav bar */
.navigation {
  height: 70px;
  background: white;
}
.brand {
  position: absolute;
  padding-left: 10px;
  float: left;
  line-height: 70px;
  text-transform: uppercase;
  font-size: 1.4em;
}
.brand a,
.brand a:visited {
  color: purple;
  text-decoration: none;
}
.nav-container {
  max-width: 1200px;
  margin: 0 auto;
}
nav {
  float: right;
}
nav ul {
  list-style: none;
  margin: 0;
  padding: 0;
}
nav ul li {
  float: left;
  position: relative;
}
nav ul li a,
nav ul li a:visited {
  display: block;
  padding: 0 20px;
  line-height: 70px;
  /* background: #262626; */
  color: #545557;
  font-size: 17px;
  text-decoration: none;
}
/* nav ul li a:hover,
nav ul li a:visited:hover {
 
  color: #fff;
} */
nav ul li a:not(:only-child):after,
nav ul li a:visited:not(:only-child):after {
  padding-left: 4px;
  content: "▾";
}
nav ul li ul li {
  min-width: 190px;
}
nav ul li ul li a {
  padding: 15px;
  line-height: 20px;
}
.nav-dropdown {
  position: absolute;
  display: none;
  z-index: 1;
  box-shadow: 0 3px 12px rgba(0, 0, 0, 0.15);
}
/* Mobile navigation */
.nav-mobile {
  display: none;
  position: absolute;
  top: 0;
  right: 0;
  background: #262626;
  height: 70px;
  width: 70px;
}
@media only screen and (max-width: 798px) {
  .nav-mobile {
    display: block;
  }
  nav {
    width: 100%;
    padding: 70px 0 15px;
  }
  nav ul {
    display: none;
  }
  nav ul li {
    float: none;
  }
  nav ul li a {
    padding: 15px;
    line-height: 20px;
  }
  nav ul li ul li a {
    padding-left: 30px;
  }
  .nav-dropdown {
    position: static;
  }
}
@media screen and (min-width: 799px) {
  .nav-list {
    display: block !important;
  }
}
#nav-toggle {
  position: absolute;
  left: 18px;
  top: 22px;
  cursor: pointer;
  padding: 10px 35px 16px 0px;
}
#nav-toggle span,
#nav-toggle span:before,
#nav-toggle span:after {
  cursor: pointer;
  border-radius: 1px;
  height: 5px;
  width: 35px;
  background: #fff;
  position: absolute;
  display: block;
  content: "▾";
  transition: all 300ms ease-in-out;
}
#nav-toggle span:before {
  top: -10px;
}
#nav-toggle span:after {
  bottom: -10px;
}
#nav-toggle.active span {
  background-color: transparent;
}
#nav-toggle.active span:before,
#nav-toggle.active span:after {
  top: 0;
}
#nav-toggle.active span:before {
  transform: rotate(45deg);
}
#nav-toggle.active span:after {
  transform: rotate(-45deg);
}
article {
  max-width: 1000px;
  margin: 0 auto;
  padding: 10px;
}

.hero {
  height: 200px;
  background-image: linear-gradient(
    to right top,
    #d16ba5,
    #d75fad,
    #db53b7,
    #dc45c2,
    #dc37cf,
    #cb2dcc,
    #ba23c8,
    #a81ac5,
    #8714ae,
    #670d97,
    #49067f,
    #2c0167
  );
}

.titleSection {
  text-align: left;
  color: white;
}
.title {
  margin: 5em;
}

button {
  background-color: #a903fc;
  color: white;
  font-weight: 600;
  border-radius: 5px;
  margin-top: 1em;
  width: 100px;
  height: 40px;
  border-color: #ba23c8;
}
</style>
