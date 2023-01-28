<template>
  <div class="app">
    <h1 class="title">
      帕拉丁助手
    </h1>
    <div class="table-container">
      <el-table :data="characters">
        <el-table-column prop="name" label="Name" width="180" />
        <el-table-column prop="staff" label="权杖" width="180" />
        <el-table-column prop="sword" label="巨剑" width="180" />
        <el-table-column prop="shield" label="盾牌" width="180" />
      </el-table>
    </div>
    <div class="validator">
      <el-select v-model="select1" class="m-2" placeholder="请选择玩家1" size="large">
        <el-option
          v-for="item in characters"
          :key="item.name"
          :label="item.name"
          :value="item.name"
        />
      </el-select>
      <el-select v-model="select2" class="m-2" placeholder="请选择玩家2" size="large">
        <el-option
          v-for="item in characters"
          :key="item.name"
          :label="item.name"
          :value="item.name"
        />
      </el-select>
      <el-select v-model="select3" class="m-2" placeholder="请选择玩家3" size="large">
        <el-option
          v-for="item in characters"
          :key="item.name"
          :label="item.name"
          :value="item.name"
        />
      </el-select>
      <el-select v-model="placeSelected" class="m-2" placeholder="请选择任务地点" size="large">
        <el-option
          v-for="item in places"
          :key="item.name"
          :label="item.name"
          :value="item.name"
        />
      </el-select>
    </div>
    <div class="validate-text">
      <p v-show="select1 && placeSelected">
        {{ diceNeededText }} <br>
        {{ resultsText }}
      </p>
    </div>
    <div class="generate-text">
      <el-button :disabled="!(placeSelected && select1)" @click="generateText" type="primary">话术生成</el-button>
        {{ generatedText }}
      <el-button @click="copytext">
        复制
      </el-button>
    </div>
  </div>
</template>

<script>
export default{
  data(){
    return{
      select1: null,
      select2: null,
      select3: null,
      placeSelected: null,
      generatedText: '',
      characters: [
        {
          name: '圣枪骑士',
          staff: 2,
          sword: 3,
          shield: 4,
        },
        {
          name: '海辰先知',
          staff: 4,
          sword: 2,
          shield: 3,
        },
        {
          name: '云灵勇士',
          staff: 3,
          sword: 5,
          shield: 1,
        },
        {
          name: '暮星战士',
          staff: 3,
          sword: 4,
          shield: 2,
        },
        {
          name: '言灵巫师',
          staff: 5,
          sword: 1,
          shield: 3,
        },
        {
          name: '光竹祭祀',
          staff: 4,
          sword: 3,
          shield: 2,
        },
      ],
      places:[
        {
          name: '犹希洞窟',
          boss: '骷髅王-李奥瑞克',
          requirement: 'sword',
          requirement1: 'sword',
          requirement1Amount: 2,
        },
        {
          name: '霞光洞穴',
          boss: '地穴领主-阿努巴拉克',
          requirement: 'sword',
          requirement1: 'sword',
          requirement1Amount: 2,
        },
        {
          name: '海底洞窟',
          boss: '海神',
          requirement: 'staff',
          requirement1: 'shield',
          requirement1Amount: 3,
        },
        {
          name: '誓言之花',
          boss: '来自东方的妖怪-彼岸花',
          requirement: 'shield',
          requirement1: 'sword',
          requirement1Amount: 2,
        },
        {
          name: '龙之洞窟',
          boss: '巨龙-昆图库塔卡提考特苏瓦西拉松',
          requirement: 'sword',
          requirement1: 'sword',
          requirement1Amount: 2,
        },
        {
          name: '索奇亚神庙',
          boss: '德古拉男爵',
          requirement: 'staff',
          requirement1: 'shield',
          requirement1Amount: 3,
        },
        {
          name: '远古沉船',
          boss: '海盗之王-德雷克',
          requirement: 'staff',
          requirement1: 'sword',
          requirement1Amount: 4,
        },
        {
          name: '梦洛克遗迹',
          boss: '魔王-梦洛克',
          requirement: 'shield',
          requirement1: 'staff',
          requirement1Amount: 2,
        },
        {
          name: '吉芬古城',
          boss: '死灵',
          requirement: 'sword',
          requirement1: 'shield',
          requirement1Amount: 2,
        },
        {
          name: '圣鸟祭坛',
          boss: '鸟人希尔队长',
          requirement: 'staff',
          requirement1: 'sword',
          requirement1Amount: 3,
        },
        {
          name: '北方冰原',
          boss: '寒冰龙',
          requirement: 'shield',
          requirement1: 'staff',
          requirement1Amount: 1,
        },
        {
          name: '拉和墓穴',
          boss: '幽暗梦魇',
          requirement: 'sword',
          requirement1: 'shield',
          requirement1Amount: 4,
        },
        {
          name: '基脉沼泽',
          boss: '史莱姆之王',
          requirement: 'shield',
          requirement1: 'shield',
          requirement1Amount: 3,
          requirement2: 'sword',
          requiremen2Amount: 1,
        },
        {
          name: '费沃冰库',
          boss: '暗·十字刺客-艾勒梅斯',
          requirement: 'staff',
          requirement1: 'staff',
          requirement1Amount: 3,
          requirement2: 'shield',
          requiremen2Amount: 1,
        },
        {
          name: '阿巫荒漠',
          boss: '沙漠皇帝-阿兹尔',
          requirement: 'sword',
          requirement1: 'sword',
          requirement1Amount: 2,
          requirement2: 'staff',
          requiremen2Amount: 2,
        },
        {
          name: '神木幻境',
          boss: '宇智波斑',
          requirement: 'shield',
          requirement1: 'shield',
          requirement1Amount: 3,
          requirement2: 'sword',
          requiremen2Amount: 2,
        },
        {
          name: '勒尼山脉',
          boss: '蜂后',
          requirement: 'staff',
          requirement1: 'staff',
          requirement1Amount: 3,
          requirement2: 'shield',
          requiremen2Amount: 1,
        },
        {
          name: '迷藏之森',
          boss: '魔王-巴风特',
          requirement: 'sword',
          requirement1: 'sword',
          requirement1Amount: 2,
          requirement2: 'staff',
          requiremen2Amount: 3,
        },
        {
          name: '精灵密泉',
          boss: '月之女祭司-泰兰德·语风暗',
          requirement: 'staff',
          requirement1: 'staff',
          requirement1Amount: 4,
          requirement2: 'sword',
          requiremen2Amount: 1,
        },
        {
          name: '帕蓝钟塔',
          boss: '斯佩夏尔',
          requirement: 'sword',
          requirement1: 'sword',
          requirement1Amount: 2,
          requirement2: 'staff',
          requiremen2Amount: 3,
        },
        {
          name: '龙骨之地',
          boss: '邪恶之龙-迪塔勒泰晤勒斯',
          requirement: 'shield',
          requirement1: 'shield',
          requirement1Amount: 2,
          requirement2: 'staff',
          requiremen2Amount: 3,
        },
        {
          name: '流行山丘',
          boss: '山丘之王穆拉丁铜须',
          requirement: 'sword',
          requirement1: 'sword',
          requirement1Amount: 4,
          requirement2: 'staff',
          requiremen2Amount: 2,
        },
        {
          name: '奥汀峡谷',
          boss: '魔剑士达纳托斯',
          requirement: 'staff',
          requirement1: 'staff',
          requirement1Amount: 3,
          requirement2: 'shield',
          requiremen2Amount: 3,
        },
        {
          name: '克特森林',
          boss: '犬妖首领',
          requirement: 'shield',
          requirement1: 'shield',
          requirement1Amount: 2,
          requirement2: 'sword',
          requiremen2Amount: 4,
        },
      ]
    }
  },
  computed:{
    player1(){
      let player1 = this.characters.find((character) => character.name === this.select1);
      if(!player1){
        player1 = {
          name: '',
          staff: 0,
          sword: 0,
          shield: 0,
        }
      }
      return player1;
    },
    player2(){
      let player1 = this.characters.find((character) => character.name === this.select2);
      if(!player1){
        player1 = {
          name: '',
          staff: 0,
          sword: 0,
          shield: 0,
        }
      }
      return player1;
    },
    player3(){
      let player1 = this.characters.find((character) => character.name === this.select3);
      if(!player1){
        player1 = {
          name: '',
          staff: 0,
          sword: 0,
          shield: 0,
        }
      }
      return player1;
    },
    place(){
      return this.places.find((place) => place.name === this.placeSelected);
    },
    diceNeededText(){
      const player2 = this.select2 === null ?  '' : ` 和 ${this.select2}`;
      const player3 = this.select3 === null ? '' : ` 和 ${this.select3}`;
      const text = this.select1 + player2 + player3 + ` 去 ${this.placeSelected} 可以用 ${this.diceNeeded} 个 骰子`;
      return text;
    },
    resultsText(){
      const req1 = this.place?.requirement1Amount + ' 个 ' + this.place?.requirement1;
      const req2 = this.place?.hasOwnProperty('requiremen2Amount') ? this.place?.requiremen2Amount + ' 个 ' + this.place?.requirement2 : '';
      const text = `胜利需要 ${req1} ${req2 ? ' 和 ' + req2 : ''}`;
      return text;
    },
    diceNeeded(){
      switch(this.place?.requirement){
        case 'shield':
          return this.player1.shield + this.player2?.shield + this.player3?.shield;
        case 'sword':
          return this.player1.sword + this.player2?.sword + this.player3?.sword;
        case 'staff':
          return this.player1.sword + this.player2?.sword + this.player3?.sword;
        default:
          return 0;
      }
    },
  },
  methods:{
    generateText(){
      const player2 = this.select2 === null ?  '' : ` 与 ${this.select2}`;
      const player3 = this.select3 === null ? '' : ` 与 ${this.select3}`;
      this.generatedText = this.select1 + player2 + player3 + ` 在 ${this.placeSelected} 击败了 ${this.place.boss}，到了无比丰厚的宝物与装备！哇！真的是羡煞旁人！`;
    },
    copytext(){
      navigator.clipboard.writeText(this.generatedText);
    }
  }
}
</script>

<style scoped>
.app{
  margin: 0 auto;
}
.title{
  margin-top: 20px;
  text-align: center;
}

.table-container{
  margin: 0 auto;
}

.validator{
  margin: 20px 0;
}
.m-2{
  margin: 0 20px;
}
.validate-text{
  margin-left: 30px;
}

.generate-text{
  margin-top: 40px;
  margin-left: 60px;
}
</style>
