<template>
  <div>
    <b-container class="container">
      <!-- Section: Team v.1 -->
      <section class="team-section text-center my-5">
        <!-- Section heading -->
        <h2 class="h1-responsive font-weight-bold my-3">Michal & Roi Team</h2>
        <!-- Section description -->
        <p
          class="grey-text w-responsive mx-auto mb-5"
          style="font-size: 1.2em;"
        >
          Enjoy our amazing website. <br/>
          
        </p>

        <!-- Grid row -->
        <div class="row">
          <!-- Grid column -->
          <div class="col-lg-6 col-md-6 mb-lg-0 mb-5">
            <div class="avatar mx-auto">
              <!-- <img
                src="../images/‏‏avitalImage.jpg"
                class="rounded-circle z-depth-1"
                alt="Sample avatar"
                width="250px"
                height="170px"
              /> -->
            </div>
            <h5 class="font-weight-bold mt-4 mb-6">Roi Katz</h5>
            <p class="text-uppercase blue-text">
            </p>
            <p class="grey-text" style="text-align:left;font-size: 1.2em;">
              Loves chewing on hummus chocolate chips cookies. <br />
              In her spare time, a student of information systems engineering at
              Ben Gurion University of the Negev. Specializes in NodeJS and
              VueJS. <br />
              You can contact me via gmail or facebook.
              <br />
            </p>
            <ul class="list-unstyled mb-0">
              <link
                rel="stylesheet"
                href="https://use.fontawesome.com/releases/v5.7.0/css/all.css"
                integrity="sha384-lZN37f5QGtY3VHgisS14W3ExzMWZxybE1SJSEsQp9S+oqd12jhcu+A56Ebc1zFSJ"
                crossorigin="anonymous"
              />
              <!-- Facebook -->
              <a href="https://www.facebook.com/avital.zehavi.9'">
                <i
                  class="fab fa-facebook-f fa-lg white-text mr-md-10 mr-3 fa-2x"
                ></i
              ></a>

              <!-- gmail -->
              <a class="p-4 fa-lg ins-ic">
                <a href="mailto:avitalz57@gmail.com">
                  <i class="fab fa-google-plus black-text p-4 fa-lg fb-ic"></i
                ></a>
              </a>
            </ul>
          </div>
          <!-- Grid column -->

          <!-- Grid column -->
          <div class="col-lg-6 col-md-6 mb-lg-0 mb-5">
            <div class="avatar mx-auto">
              <!-- <img
                src="../images/orImage.jpeg"
                class="rounded-circle z-depth-1"
                alt="Sample avatar"
                width="250px"
                height="170px"
              /> -->
            </div>
            <h5 class="font-weight-bold mt-4 mb-6">Michal Talmor</h5>
            <p class="text-uppercase blue-text">
            </p>
            <p class="grey-text" style="text-align:left;font-size: 1.2em;">
              The worlds best hummus chocolate chips cookies baker. <br />
              In her spare time, she is a student of information systems
              engineering at Ben Gurion University of the Negev. Specializes in
              NodeJS and VueJS. <br />You can contact me via gmail or facebook.
            </p>
            <ul class="list-unstyled mb-0">
              <!-- Facebook -->
              <a href="https://www.facebook.com/OrAlfasi">
                <i
                  class="fab fa-facebook-f fa-lg white-text mr-md-10 mr-3 fa-2x"
                ></i
              ></a>
              <!-- gmail -->
              <a class="p-4 fa-lg ins-ic">
                <a href="mailto:oralfasi09@gmail.com">
                  <i class="fab fa-google-plus black-text p-4 fa-lg fb-ic"></i
                ></a>
              </a>
            </ul>
          </div>
          <!-- Grid column -->
        </div>
        <!-- Grid row -->

        <div class="projectStory">
          The website developed by us using Node.js in the back side and Vue.js in the front side. <br/>
        </div>

        <div class="projectLinks">
          <!-- style="text-align:left;margin-bottom:30px;" -->
          <ul class="list-unstyled mb-0">
            
              <a
                href=" https://app.swaggerhub.com/apis/avitalze/recipeWebUpdate/1.9"
                >Part 1 - API</a
              >
             |
            
              <a
                href="https://github.com/SISE-Web-Development-Environments/assignment-3-2-or_avital"
                >Part 2 - backend</a
              >
            |
            
              <a
                href="https://github.com/SISE-Web-Development-Environments/assignment-3-3-or_avital"
                >Part 3- fronted</a
              >
            
          </ul>
        </div>
      </section>
    </b-container>
  </div>
</template>
<script>
export default {
 
};
</script>

<style lang="scss" scoped>
.container {
  min-height: 400px;
}
// .row {
//   padding: 10 px;
//   align-items: center;
// }
.col {
  float: left;
  width: 50%;
  margin-bottom: 16px;
  padding: 0 8px;
}
.p {
  font-size: 16px;
}
.card {
  box-shadow: 0 4px 8px 0 rgba(0, 0, 0, 0.2);
  margin: 8px;
}
.bg-1 {
  background-color: #1ac6f1; /* Green */
  color: #ffffff;
}
.bg-2 {
  background-color: #474e5d; /* Dark Blue */
  color: #ffffff;
}
.bg-3 {
  background-color: #ffffff; /* White */
  color: #555555;
}
.fa-clickable {
  cursor: pointer;
  outline: none;
}
.projectLinks {
  padding-bottom: 30px;
}
</style>