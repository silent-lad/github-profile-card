<template>
  <div class="container">
    <div style="margin-top:100px;" class="github-card" id="github-card">
      <!-- <img src="../assets/placeholder.png" alt=""> -->
      <div class="outer-backdrop">
        <div class="inner-backdrop">
          <div class="card-header">
            <div class="username">@silentlad</div>
          </div>
          <div class="card-body">
            <div class="stats">
              <div class="rating">A+</div>
              <div class="numerical-stats">
                <div class="num-stat totalPRs">
                  71
                </div>
                <div class="num-stat totalCommits">
                  50
                </div>
                <div class="num-stat totalIssuess">
                  17
                </div>
                <div class="num-stat totalStars">
                  234
                </div>
                <div class="num-stat contributedTos">
                  0
                </div>
              </div>
              <div class="languages">
                
              </div>
            </div>
            <div class="profile-image">
              <img src="" alt="">
            </div>
          </div>
          
        </div>
      </div>
    </div>
    <a href="#" @click="download()">download</a>
  </div>
</template>

<script>
import VanillaTilt from "vanilla-tilt";
import * as htmlToImage from 'html-to-image';
import axios from "axios";

export default {
  name: 'Card',
  data() {
    return {
      msg: String,
      stargazers:0,
      user: Object,
      stats: {
          "name": "Divyansh Tripathi",
          "totalPRs": 71,
          "totalCommits": 50,
          "totalIssues": 17,
          "totalStars": 234,
          "contributedTo": 0,
          "rank": {
              "level": "A+",
              "score": 50.04415509543695
          }
      }
    }
  },
  methods:{
    download:()=>{
      htmlToImage.toPng(document.getElementById('github-card'))
        .then(function (dataUrl) {
          var link = document.createElement('a');
          link.download = 'github-card.jpeg';
          link.href = dataUrl;
          link.click();
        });
    },
     getStars: async function(){
      const repos = await axios.get("https://api.github.com/users/silent-lad/repos")
      console.log(repos);
      // repos.forEach(repo => {
      //     this.stargazers += repo.stargazers_count
      // });
    },
    getUser: async function(){
      const user = await axios.get("https://api.github.com/users/silent-lad");
      console.log(JSON.parse(user.request.response));
    },
    getObject: async function() {
      this.stats = await axios.get("https://github-readme-stats-chi-six-98.vercel.app/api?username=silent-lad");
    }
  },
  mounted() {
    VanillaTilt.init(document.querySelector("img"), {
      max: 15,
      speed: 400,
      reverse: true,
    //   scale: 1.05,
      glare: true,
      "full-page-listening": true,
      "max-glare": 0.6,
    });
    this.getStars();
    this.getUser();
    this.getObject();
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
  @import './Card.css';
</style>