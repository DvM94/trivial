<template>
  <div class="about center">
    <div class="avatares">
      <div class="avatar">
        <img alt="Nuria" src="/img/nuria.png" class="logo" />
        <div class="link">
          <a href="https://github.com/nurimartinez" target="_blank">
            <i class="fab fa-github"></i>
            <p>@nurimartinez</p>
          </a>
        </div>
      </div>
      <div class="avatar">
        <img alt="Dani" src="/img/dani.png" class="logo" />
        <div class="link">
          <a href="https://github.com/DvM94" target="_blank">
            <i class="fab fa-github"></i>
            <p>@DvM94</p>
          </a>
        </div>
      </div>
    </div>
    <div class="card">
      <p class="about-title">About us</p>
      <p class="about-text">
        We are Daniel and Nuria, two colleagues of a Full Stack course who are
        passionate about Web Development. We are working with HTML5, CSS3, JS,
        Vue, Node and MongoDB, but we also use tools and principles that make
        our projects more reliable, such as Git, Agile methodologies and
        Responsive Design.
      </p>
    </div>
    <router-link to="/game"
      ><img
        alt="Vue logo"
        src="/img/play.png"
        @mouseover="hover($event, '/img/play2.png')"
        @mouseout="hover($event, '/img/play.png')"
    /></router-link>
  </div>
</template>

<script>
export default {
  name: "About",
  components: {},
  setup() {
    const hover = (e, link) => (e.target.src = link);

    return {
      hover,
    };
  },
};
</script>

<style lang="scss" scoped>
.about {
  width: 60%;
  max-width: 900px;
}
.avatares {
  width: 100%;
  display: flex;
  justify-content: center;
  align-items: center;
}
.avatar {
  width: 47%;
  max-width: 250px;
  position: relative;

  .link {
    cursor: pointer;
    width: 85%;
    position: absolute;
    padding: 6px 10px 4px 10px;
    border-radius: 10px;
    border: 1px solid black;
    background-color: #36b39e;
    bottom: 0;
    left: 50%;
    transform: translateX(-50%);

    a {
      text-decoration: none;
      display: flex;
      justify-content: center;
      align-items: center;

      .fa-github {
        margin: 0 5px 0 0;
        color: white;
        font-size: 1.5rem;
      }

      p {
        color: white;
      }
    }
  }
}

.card {
  width: 75%;
  background-color: rgb(136, 135, 135);
  box-shadow: 3px 3px 5px gray;
  border: 1px solid black;
  border-radius: 10px;
  margin: 20px auto;
  padding: 25px 15px;
}

.about-title {
  font-size: 2rem;
  font-weight: 700;
  color: white;
  text-shadow: 1px 0 0 #000, -1px 0 0 #000, 0 1px 0 #000, 0 -1px 0 #000,
    1px 1px #000, -1px -1px 0 #000, 1px -1px 0 #000, -1px 1px 0 #000;
  text-align: center;
  letter-spacing: 4px;
}

.about-text {
  margin: 10px;
  text-align: center;
  font-weight: 500;
  color: white;
  line-height: 20px;
}

@media (max-width: 600px) {
  .about {
    width: 85%;
  }

  .link {
    font-size: 0.8rem;
  }

  .card {
    width: 90%;
    padding: 15px 10px;
  }

  .about-title {
    font-size: 2rem;
  }

  .about-text {
    color: white;
    line-height: 17px;
    font-size: 0.8rem;
  }
}
</style>