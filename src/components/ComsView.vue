<template>
  <div class="obs-main">
    <div class="main-title">
      Couples Counselling Tournament
    </div>
    <div class="sub-title">
      {{ info.subTitle }}
    </div>
    <div class="casters" v-if="info.people"
      :class="{ two: info.people.length == 2, three: info.people.length == 3, four: info.people.length == 4 }">
      <div class="person" v-for="p in info.people" v-bind:key="p.twitter">
        <div class="role">{{ p.role }}</div>
        <div class="green-space"></div>
        <div class="name">{{ p.name }}</div>
        <div class="twitter">{{ p.twitter }}</div>
      </div>
    </div>
  </div>
  <div style="margin-top: 50px;">Edit Link</div>
  <textarea style="width: 500px; height: 500px;" v-model="rawData"></textarea>
  <button @click="parseData()">Parse</button>
  <input type="text" v-model="urlOut" />

  <br>
  <a href="/srg-cheat-sheet/#/coms/?data=%7B%22subTitle%22:%22Pre-game:%20SEED%20IS%20BEING%20Scouted...%22,%22people%22:%5B%7B%22role%22:%22Commentator%22,%22name%22:%22PodX12%20(He/Him)%22,%22twitter%22:%22PodX12%22%7D,%7B%22role%22:%22Commentator%22,%22name%22:%22Skyro%20(He/Him)%22,%22twitter%22:%22skyro%22%7D%5D%7D">Two Perspectives</a>
  <br>
  <a href="/srg-cheat-sheet/#/coms/?data=%7B%22subTitle%22:%22Pre-game:%20SEED%20IS%20BEING%20Scouted...%22,%22people%22:%5B%7B%22role%22:%22Commentator%22,%22name%22:%22PodX12%20(He/Him)%22,%22twitter%22:%22PodX12%22%7D,%7B%22role%22:%22Commentator%22,%22name%22:%22Skyro%20(He/Him)%22,%22twitter%22:%22skyro%22%7D,%7B%22role%22:%22Runner%22,%22name%22:%22Player%201(He/Him)%22,%22twitter%22:%22-%22%7D%5D%7D">Three Perspectives</a>
  <br>
  <a href="/srg-cheat-sheet/#/coms/?data=%7B%22subTitle%22:%22Pre-game:%20SEED%20IS%20BEING%20Scouted...%22,%22people%22:%5B%7B%22role%22:%22Commentator%22,%22name%22:%22PodX12%20(He/Him)%22,%22twitter%22:%22PodX12%22%7D,%7B%22role%22:%22Commentator%22,%22name%22:%22Skyro%20(He/Him)%22,%22twitter%22:%22skyro%22%7D,%7B%22role%22:%22Runner%22,%22name%22:%22Player%201%20(He/Him)%22,%22twitter%22:%22-%22%7D,%7B%22role%22:%22Runner%22,%22name%22:%22Player%202%20(He/Him)%22,%22twitter%22:%22-%22%7D%5D%7D">Four Perspectives</a>
</template>
<!-- http://localhost:8080/srg-cheat-sheet/#/coms/?data=%7B%22subTitle%22:%22test%22,%22people%22:%5B%7B%22role%22:%22Commentator%22,%22name%22:%22PodX12%20(He/Him)%22,%22twitter%22:%22PodX12%22%7D,%7B%22role%22:%22Commentator%22,%22name%22:%22Katherine%20(She/Her)%22,%22twitter%22:%22Queenkac_%22%7D%5D%7D -->
<script>
export default {
  name: 'ComsView',
  data() {
    return {
      rawData: `{
    "subTitle": "Pre-game: SEED IS BEING Scouted...",
    "people": [
        {
            "role": "Commentator",
            "name": "PodX12 (He/Him)",
            "twitter": "PodX12"
        },
        {
            "role": "Commentator",
            "name": "Skyro (He/Him)",
            "twitter": "skyro"
        },
        {
            "role": "Runner",
            "name": "Player 1 (He/Him)",
            "twitter": "-"
        },
        {
            "role": "Runner",
            "name": "Player 2 (He/Him)",
            "twitter": "-"
        }
    ]
}`,
      info: {},
      urlOut: ""
    }
  },
  created() {
    let dataSplit = window.location.href.split("/?data=");

    if (dataSplit[1]) {
      this.info = JSON.parse(decodeURI(dataSplit[1]))
      this.rawData = JSON.stringify(this.info, undefined, 4);
      this.parseData();
    }
  },
  methods: {
    parseData() {
      var data = JSON.parse(this.rawData);
      console.log(data);
      console.log(encodeURI(JSON.stringify(data)));
      this.urlOut = "http://localhost:8080/srg-cheat-sheet/#/coms/?data=" + encodeURI(JSON.stringify(data));
    }
  }
}
</script>
<style>
.main-title {
  padding: 20px 0;
  font-size: 112px;
  text-align: center;
}

.sub-title {
  text-align: center;
  font-size: 45px;
}

.casters {
  padding: 80px 0;
  text-align: center;
}

.person {
  width: 500px;
  display: inline-block;
  padding: 0 70px;
}

.role {
  font-size: 45px;
  margin-bottom: 10px;
  text-align: left;
}

.green-space {
  width: 500px;
  height: 500px;
  background-color: rgb(0, 255, 0);
}

.name {
  font-size: 40px;
  text-align: left;
}

.twitter {
  font-size: 30px;
  text-align: left;
}

.casters.four .green-space {
  width: 400px;
  height: 400px;
}

.casters.four .person {
  width: 400px;
  padding: 0 40px;
}
</style>