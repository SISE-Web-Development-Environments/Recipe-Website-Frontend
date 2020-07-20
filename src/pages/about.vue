<template>
  <div>
    <b-container>
      <section class="text-center my-5">
        <h2>
          <b>Michal & Roi Team</b>
        </h2>
        <p>
          Enjoy our amazing website!
          <br />
        </p>
        <div class="inline-block">
          <div class="images">
            <h5>Michal Talmor</h5>
             <img
                src="../assets/Michal-Profile.jpeg"                
                alt="Sample avatar"
                width="150px"
                height="200px"
              />    
          </div>         
          <div class = "images">          
            <h5>Roi Katz</h5> 
            <img
                src="../assets/Roi-Profile.jpeg"                
                alt="Sample avatar"
                width="150px"
                height="200px"
              />    
          </div>         
        </div>
        <br>

        <div>
          The website developed by us using Node.js in the back side and Vue.js in the front side.
          <br />
        </div>

        <div>
          <a href="https://app.swaggerhub.com/apis-docs/roikatz16/recepies_API/1.0.0"><b>Part 1 : API</b></a>
          |
          <a
            href="https://github.com/SISE-Web-Development-Environments/assignment-3-2-roi_michal"
          ><b>Part 2 : Backend</b></a>
          |
          <a
            href="https://github.com/SISE-Web-Development-Environments/assignment-3-3-roi_michal"
          ><b>Part 3 : Fronted</b></a>
        </div>
      </section>
    </b-container>
  </div>
</template>
<script>
export default {};
</script>

<style lang="scss" scoped>
.inline-block {
  display: block;
}
.images{
  margin-right: 20px;
  display:inline-block
}
</style>