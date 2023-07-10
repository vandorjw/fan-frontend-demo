<script setup lang="ts">
import { RouterLink, RouterView } from 'vue-router'
</script>

<template>
  <!-- -------------------------------------------------- START Skip Link --------------------------------------------------- -->
  <nav class="skip-links" aria-label="Skip to main content">
    <a href="#main" class="skip-to-link">Skip to main content</a>
  </nav>
  <!-- -------------------------------------------------- END Skip Link  --------------------------------------------------- -->

  <!-- -------------------------------------------------- START HEADER --------------------------------------------------- -->

  <header>
    <!-- START SALTIRE NS MOTHERSHIP RIBBON w FR -->
    <nav id="navigation" class="ribbon" role="navigation" aria-label="Main navigation">
      <div class="container">
        <div class="row">
          <div class="col-xs-6">
            <a href="/" hreflang="en"><img class="ribbon-img"
                src="https://novascotia.ca/clf/ignition/img/nsvip-en-white-flag.svg" alt="Government of Nova Scotia"></a>
          </div>
          <div class="col-xs-6">

          </div>
        </div>
      </div>
    </nav>
    <!-- END SALTIRE NS MOTHERSHIP RIBBON w FR -->
  </header>


  <!-- -------------------------------------------------- END HEADER --------------------------------------------------- -->

  <div id="nav-placeholder4">
    <!-- START Primary NAV -->
    <nav id="topheader" class="navbar navbar-expand-lg ns-navbar-light">
      <div class="container ns-nav-container">
        <button class="navbar-toggler" type="button" data-toggle="collapse" data-target="#navbarNavDropdown"
          aria-controls="navbarNavDropdown" aria-expanded="false" aria-label="Toggle navigation">
          <i class="fa fa-bars fa-2 ns-toggle-icon" aria-hidden="true"></i>
        </button>
        <div class="collapse navbar-collapse" id="navbarNavDropdown">
          <ul class="navbar-nav mt-0">
            <li class="nav-item">
              <RouterLink to="/" class="nav-link">Home</RouterLink>
            </li>
            <li class="nav-item">
              <RouterLink to="/about" class="nav-link">About</RouterLink>
            </li>

          </ul>
        </div>
      </div>
    </nav>
    <!-- End Primary NAV -->
  </div>



  <!--A basic page has a primary content area and an optional column for secondary information like related content.-->
  <div class="container Site-content">
    <main id="main"><!-- SEMANTIC MAIN TAG TO INDICATE PAGE CONTENT-->
      <article><!-- SEMANTIC ARTICLE TAG TO GROUP RELATED CONTENT-->
        <div class="row">
          <RouterView />
        </div><!--/row-->
      </article>
    </main>
  </div><!-- /container -->

  <!-- START FOOTER -->
  <footer id="footer" class="footer" role="contentinfo">
    <div class="container">
      <ul class="remove-underline">
        <li><a href="#/privacy/">Privacy</a></li>
        <li><a href="#/terms/">Terms</a></li>
        <li><a href="#/cookies/">Cookies</a></li>
      </ul>
    </div>
  </footer>
  <!-- END FOOTER -->
</template>
