<template>
<!-- eslint-disable -->
<div id="app">

    <!--==========================
    Header
  ============================-->
    <header id="header">
        <div class="container">

            <div id="logo" class="pull-left">
                <img src="static/img/logo.png" alt="">
                <!-- <h1><a href="#body" class="scrollto">DOWNPAYMENT<span>LOOKUP</span></a></h1> -->
            </div>

        </div>
    </header>
    <!-- #header -->

    <!--==========================
    Intro Section
  ============================-->
    <section id="intro">

        <div class="intro-content">
            <h2>Making <span>your ideas</span><br>happen!</h2>
            <div>
                <a href="#about" class="btn-get-started scrollto">Get Started</a>
            </div>
        </div>

        <div id="intro-carousel" class="owl-carousel">
            <div class="item" style="background-image: url('/static/img/intro-carousel/1.jpg');"></div>
            <div class="item" style="background-image: url('/static/img/intro-carousel/2.jpg');"></div>
            <div class="item" style="background-image: url('/static/img/intro-carousel/3.jpg');"></div>
            <div class="item" style="background-image: url('/static/img/intro-carousel/4.jpg');"></div>
            <div class="item" style="background-image: url('/static/img/intro-carousel/5.jpg');"></div>
        </div>

    </section>
    <!-- #intro -->

    <main id="main">

        <!--==========================
      About Section
    ============================-->
        <section id="about" class="wow fadeInUp">
            <router-view/>
        </section>
        <!-- #about -->


    </main>

    <!--==========================
    Footer
  ============================-->
    <footer id="footer">
        <div class="container">
            <div class="copyright">
                 Copyright &copy; 2018 <strong>DOWNPAYMENTLOOKUP</strong>. All Rights Reserved
            </div>
        </div>
    </footer>
    <!-- #footer -->

</div>

</template>

<script>

export default {
    name: 'App',
    data() {
        return {
        }
    },
}

</script>

<style>

#app {
    font-family: 'Avenir', Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    text-align: center;
    color: #2c3e50;
    margin-top: 60px;
}

</style>
