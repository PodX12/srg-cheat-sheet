<template>
  <div style="margin-bottom: 50px;" >
    <label>Raw Data</label>
    <input type="text" :value="rawData" />
  </div>
  <div class="main">
    <div class="overworld">
      <div class="item-title">Overworld</div>
      <div class="item">
        <div class="img"><img :src="icons.flint" /></div>
        <div class="note">
          First Flint - {{ this.info.flint }}
        </div>
      </div>
      <div class="item">
        <div class="img"><img :src="icons.iron" /></div>
        <div class="note">
          Golem - 4
        </div>
      </div>
    </div>

    <div class="fortress">
      <div class="item-title">Fortress</div>
      <div class="item">
        <div class="img"><img :src="icons.blaze" /></div>
        <div class="note">
          5 - {{ this.info.fort["5"] }} Blazes
        </div>
      </div>
      <div class="item">
        <div class="img">
          <img :src="icons.blaze" />
        </div>
        <div class="note">
          6 - {{ this.info.fort["6"] }} Blazes
        </div>
      </div>
    </div>

    <div class="clear"></div>
    <div class="bastion">
      <div class="item-title">Bastion Barters</div>
      <div class="block-group" v-for="g in this.info.gold" v-bind:key="g.goldBlocks">
        <div class="item">
          <div class="img"><img :src="icons.gold" /></div>
          <div class="note">
            {{ g.goldBlocks }} Blocks
          </div>
        </div>
        <div class="trade">
          <div class="img"><img :src="icons.pearl" /></div>
          <div class="note">
            {{ g.pearls }}
          </div>
        </div>
        <div class="trade">
          <div class="img"><img :src="icons.string" /></div>
          <div class="note">
            {{ g.string }}
          </div>
        </div>
        <div class="trade">
          <div class="img"><img :src="icons.obi" /></div>
          <div class="note">
            {{ g.obi }}
          </div>
        </div>
        <div class="trade">
          <div class="img"><img :src="icons.res" /></div>
          <div class="note">
            {{ g.res }}
          </div>
        </div>
      </div>
      <div class="clear"></div>
    </div>

    <div class="stronghold">
      <div class="item-title">Portal Room #1: <span class="sh1">{{ this.info.stronghold["1"].eyes }} eye</span></div>
      <div>Nether: <span class="sh1">{{ this.info.stronghold["1"].pos }}</span></div>
    </div>
    <div class="stronghold">
      <div class="item-title">Portal Room #2: <span class="sh2">{{ this.info.stronghold["2"].eyes }} eye</span></div>
      <div>Nether: <span class="sh2">{{ this.info.stronghold["2"].pos }}</span></div>
    </div>

    <div class="stronghold">
      <div class="item-title">Portal Room #3: <span class="sh3">{{ this.info.stronghold["3"].eyes }} eye</span></div>
      <div>Nether: <span class="sh3">{{ this.info.stronghold["3"].pos }}</span></div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'HelloWorld',
  data() {
    return {
      icons: {
        flint: "https://static.wikia.nocookie.net/minecraftpocketedition/images/2/2e/Flint.png",
        blaze: "https://static.wikia.nocookie.net/minecraft_gamepedia/images/8/87/Blaze_Rod_JE1_BE1.png",
        gold: "https://static.wikia.nocookie.net/minecraft_gamepedia/images/7/72/Block_of_Gold_JE6_BE3.png",
        pearl: "https://static.wikia.nocookie.net/minecraft_gamepedia/images/f/f6/Ender_Pearl_JE3_BE2.png",
        string: "https://oyster.ignimgs.com/mediawiki/apis.ign.com/minecraft/f/fa/Grid_String.png",
        obi: "https://static.wikia.nocookie.net/minecraft_gamepedia/images/9/99/Obsidian_JE3_BE2.png",
        res: "https://static.wikia.nocookie.net/minecraft_gamepedia/images/1/1f/Fire_Resistance_JE2_BE2.png",
        eye: "https://static.wikia.nocookie.net/minecraft_gamepedia/images/7/7a/Eye_of_Ender_JE2_BE2.png",
        iron: "https://static.wikia.nocookie.net/minecraft_gamepedia/images/f/fc/Iron_Ingot_JE3_BE2.png",
        endPortal: "https://static.wikia.nocookie.net/minecraft/images/4/44/EndPortal.png"
      },
      rawData: "5	6	12	12	28	2	4	19	28	6	4	19	43	8	4	19	63	11	8	0	121 183	5	-299 19	3	158 -217",
      info: null
    }
  },
  created() {
    this.parseData();
  },
  methods: {
    parseData() {
      var split = this.rawData.split("\t");

      this.info = {
        flint: split[0],
        fort: {
          "5": split[1],
          "6": split[2]
        },
        gold: [
          {
            goldBlocks: 4,
            pearls: split[3],
            string: split[4],
            obi: split[5],
            res: split[6]
          },
          {
            goldBlocks: 6,
            pearls: split[7],
            string: split[8],
            obi: split[9],
            res: split[10]
          },
          {
            goldBlocks: 8,
            pearls: split[11],
            string: split[12],
            obi: split[13],
            res: split[14]
          },
          {
            goldBlocks: 10,
            pearls: split[15],
            string: split[16],
            obi: split[17],
            res: split[18]
          }
        ],
        stronghold: {
          "1": {
            eyes: split[19],
            pos: split[20]
          },
          "2": {
            eyes: split[21],
            pos: split[22]
          },
          "3": {
            eyes: split[23],
            pos: split[24]
          }
        }
      }
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style>
body {
  background-color: #333;
  color: #eee;
  margin: 20px !important;
  text-shadow: 1px 1px 1px #000000ee;
}

.item {
  padding: 5px 0;
}

.item:after {
  content: "";
  display: block;
  clear: both;
}

.item-title {
  font-size: 110%;
}

.item .img {
  float: left;
  padding-right: 5px;
}

.item .note {
  float: left;
}

.clear {
  clear: both;
}

.item .img img {
  height: 20px;
}

.block-group {
  margin-bottom: 15px;
}

.block-group,
.overworld,
.fortress {
  width: 195px;
  float: left;
}

.block-group .item:first-child {
  margin-left: 0;
}

.sh:after {
  content: "";
  display: block;
  clear: both;
}

.sh .item {
  float: left;
  width: 120px;
}

.sh .item .img {}

.sh .item .note {
  width: 70px;
  padding-left: 2px;
}

.trade {
  width: 40px;
  float: left;
}

.trade .img {
  height: 20px;
  text-align: center;
}

.trade .note {
  margin-top: 5px;
  text-align: center;
}

.trade .img img {
  height: 100%;
}



.overworld {
  width: 180px;
}

.fortress {
  width: 180px;
}

.bastion {
  width: 390px;
}

.stronghold {
  width: 390px;
}

.overworld,
.fortress,
.bastion,
.stronghold {
  margin: 5px;
  padding: 5px;
  background-color: rgba(50, 50, 50, 0.5);
  border: 5px solid rgba(0, 0, 0, 0.5);
}


.main {
  width: 420px;
  background-image: url("../assets/image-2.png");
  background-size: 130%;
  padding-bottom: 5px;
}

.sh1 {
  color: rgb(255, 100, 100);
}

.sh2 {
  color: rgb(100, 255, 100);
}

.sh3 {
  color: rgb(100, 100, 255);
}
</style>
