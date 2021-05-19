<template>
  <div id="cover">
    <!-- <img id="cover-img" src="@/assets/images/shoes.jpg" alt="" /> -->
    <h1 id="cover-title">最新潮流款式</h1>
    <a href="#" v-scroll-to="'h3'">
      <button id="jump">立即購買</button>
    </a>
  </div>
</template>

<script>
export default {};
</script>

<style>
#cover {
  width: 100%;
  height: 95vh;
  overflow: hidden;
  position: relative;
  background: url(../assets/images/shoes.jpg);
  background-size: cover;
  background-position: 25%;
  margin-bottom: 5rem;
}
#cover-img {
  width: 100%;
  height: 100%;
}
#jump {
  position: absolute;
  top: 45%;
  left: 17%;
  z-index: 1;
  border: none;
  background-color: #517563;
  border-radius: 10px;
  font-size: 1.5rem;
  font-weight: 600;
  color: #fff;
  padding: 1rem 1.2rem;
}
#cover-title {
  position: absolute;
  top: 20%;
  left: 5%;
  font-weight: 700;
  font-size: 5rem;
  color: black;
}
@media screen and (max-width: 991px) {
  #cover-title {
    font-size: 3.5rem;
  }
  #jump {
    font-size: 1.2rem;
  }
}
@media screen and (max-width: 768px) {
  #cover-title {
    font-size: 3.5rem;
  }
  #jump {
    font-size: 1.2rem;
  }
  #cover {
    background-position: 55%;
    height: 80vh;
  }
}
@media screen and (max-width: 576px) {
  #cover {
    height: 70vh;
    background-position: right 25% bottom 35%;
    display: flex;
    flex-direction: column;
    justify-content: space-between;
    align-items: center;
    position: static;
  }
  #cover-title {
    font-size: 3rem;
    position: static;
    margin-top: 4rem;
  }
  #jump {
    font-size: 1rem;
    position: static;
    margin-bottom: 4rem;
  }
}
</style>
