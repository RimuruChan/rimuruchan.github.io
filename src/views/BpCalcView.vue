<template>
  <div class="bpCalc">
    <h1>进行蜡烛计算</h1>
    <el-row gutter="16" justify="center">
      <el-card>
        <el-row gutter="16" justify="center">
          <el-col :span="8">
            <span>起始等级</span>
            <el-input v-model="levelStart" placeholder="起始等级"/>
          </el-col>
          <el-col :span="8">
            <span>目标等级</span>
            <el-input v-model="levelEnd" placeholder="目标等级"/>
          </el-col>
        </el-row>
        <el-row gutter="16" justify="center">
          <el-col :span="8">
            <span>蜡烛单位数量</span>
            <el-input v-model="bpNum" placeholder="蜡烛单位数量"/>
          </el-col>
          <el-col :span="8">
            <span>蜡烛单位价格</span>
            <el-input v-model="bpCost" placeholder="蜡烛单位价格"/>
          </el-col>
        </el-row>
        <h3>需要的蜡烛</h3>
        <p class="number">{{ calculateToken }} 蜡烛</p>
        <h3>推荐价格</h3>
        <p class="number">{{ calculateCost }} 元</p>
      </el-card>
    </el-row>
  </div>
</template>

<script lang="ts">
import {Vue} from "vue-class-component";

export default class BpCalc extends Vue {
  bpData = [
    {
      id: "bp_level_1",
      level: 1,
      tokenNum: 200,
      nextTokenNum: 400,
      itemID: "4001",
      itemType: "GOLD",
      itemCount: 20000,
      isGoodPrize: false,
      isGrandPrize: false,
    },
    {
      id: "bp_level_2",
      level: 2,
      tokenNum: 400,
      nextTokenNum: 600,
      itemID: "2004",
      itemType: "CARD_EXP",
      itemCount: 10,
      isGoodPrize: false,
      isGrandPrize: false,
    },
    {
      id: "bp_level_3",
      level: 3,
      tokenNum: 600,
      nextTokenNum: 800,
      itemID: "31043",
      itemType: "MATERIAL",
      itemCount: 10,
      isGoodPrize: false,
      isGrandPrize: false,
    },
    {
      id: "bp_level_4",
      level: 4,
      tokenNum: 800,
      nextTokenNum: 1000,
      itemID: "3301",
      itemType: "MATERIAL",
      itemCount: 30,
      isGoodPrize: false,
      isGrandPrize: false,
    },
    {
      id: "bp_level_5",
      level: 5,
      tokenNum: 1000,
      nextTokenNum: 1200,
      itemID: "31054",
      itemType: "MATERIAL",
      itemCount: 3,
      isGoodPrize: false,
      isGrandPrize: false,
    },
    {
      id: "bp_level_6",
      level: 6,
      tokenNum: 1200,
      nextTokenNum: 1400,
      itemID: "4001",
      itemType: "GOLD",
      itemCount: 20000,
      isGoodPrize: false,
      isGrandPrize: false,
    },
    {
      id: "bp_level_7",
      level: 7,
      tokenNum: 1400,
      nextTokenNum: 1600,
      itemID: "2004",
      itemType: "CARD_EXP",
      itemCount: 10,
      isGoodPrize: false,
      isGrandPrize: false,
    },
    {
      id: "bp_level_8",
      level: 8,
      tokenNum: 1600,
      nextTokenNum: 1800,
      itemID: "31053",
      itemType: "MATERIAL",
      itemCount: 10,
      isGoodPrize: false,
      isGrandPrize: false,
    },
    {
      id: "bp_level_9",
      level: 9,
      tokenNum: 1800,
      nextTokenNum: 2000,
      itemID: "3302",
      itemType: "MATERIAL",
      itemCount: 10,
      isGoodPrize: false,
      isGrandPrize: false,
    },
    {
      id: "bp_level_10",
      level: 10,
      tokenNum: 2000,
      nextTokenNum: 2200,
      itemID: "31044",
      itemType: "MATERIAL",
      itemCount: 3,
      isGoodPrize: false,
      isGrandPrize: false,
    },
    {
      id: "bp_level_11",
      level: 11,
      tokenNum: 2200,
      nextTokenNum: 2400,
      itemID: "4001",
      itemType: "GOLD",
      itemCount: 20000,
      isGoodPrize: false,
      isGrandPrize: false,
    },
    {
      id: "bp_level_12",
      level: 12,
      tokenNum: 2400,
      nextTokenNum: 2625,
      itemID: "2004",
      itemType: "CARD_EXP",
      itemCount: 10,
      isGoodPrize: false,
      isGrandPrize: false,
    },
    {
      id: "bp_level_13",
      level: 13,
      tokenNum: 2625,
      nextTokenNum: 2850,
      itemID: "31043",
      itemType: "MATERIAL",
      itemCount: 10,
      isGoodPrize: false,
      isGrandPrize: false,
    },
    {
      id: "bp_level_14",
      level: 14,
      tokenNum: 2850,
      nextTokenNum: 3075,
      itemID: "3303",
      itemType: "MATERIAL",
      itemCount: 3,
      isGoodPrize: false,
      isGrandPrize: false,
    },
    {
      id: "bp_level_15",
      level: 15,
      tokenNum: 3075,
      nextTokenNum: 3300,
      itemID: "31054",
      itemType: "MATERIAL",
      itemCount: 3,
      isGoodPrize: false,
      isGrandPrize: false,
    },
    {
      id: "bp_level_16",
      level: 16,
      tokenNum: 3300,
      nextTokenNum: 3525,
      itemID: "4001",
      itemType: "GOLD",
      itemCount: 20000,
      isGoodPrize: false,
      isGrandPrize: false,
    },
    {
      id: "bp_level_17",
      level: 17,
      tokenNum: 3525,
      nextTokenNum: 3750,
      itemID: "2004",
      itemType: "CARD_EXP",
      itemCount: 10,
      isGoodPrize: false,
      isGrandPrize: false,
    },
    {
      id: "bp_level_18",
      level: 18,
      tokenNum: 3750,
      nextTokenNum: 3975,
      itemID: "31044",
      itemType: "MATERIAL",
      itemCount: 3,
      isGoodPrize: false,
      isGrandPrize: false,
    },
    {
      id: "bp_level_19",
      level: 19,
      tokenNum: 3975,
      nextTokenNum: 4200,
      itemID: "3301",
      itemType: "MATERIAL",
      itemCount: 30,
      isGoodPrize: false,
      isGrandPrize: false,
    },
    {
      id: "bp_level_20",
      level: 20,
      tokenNum: 4200,
      nextTokenNum: 4450,
      itemID: "30145",
      itemType: "MATERIAL",
      itemCount: 1,
      isGoodPrize: true,
      isGrandPrize: false,
    },
    {
      id: "bp_level_21",
      level: 21,
      tokenNum: 4450,
      nextTokenNum: 4700,
      itemID: "4001",
      itemType: "GOLD",
      itemCount: 30000,
      isGoodPrize: false,
      isGrandPrize: false,
    },
    {
      id: "bp_level_22",
      level: 22,
      tokenNum: 4700,
      nextTokenNum: 4950,
      itemID: "31034",
      itemType: "MATERIAL",
      itemCount: 3,
      isGoodPrize: false,
      isGrandPrize: false,
    },
    {
      id: "bp_level_23",
      level: 23,
      tokenNum: 4950,
      nextTokenNum: 5200,
      itemID: "2004",
      itemType: "CARD_EXP",
      itemCount: 15,
      isGoodPrize: false,
      isGrandPrize: false,
    },
    {
      id: "bp_level_24",
      level: 24,
      tokenNum: 5200,
      nextTokenNum: 5450,
      itemID: "30044",
      itemType: "MATERIAL",
      itemCount: 3,
      isGoodPrize: false,
      isGrandPrize: false,
    },
    {
      id: "bp_level_25",
      level: 25,
      tokenNum: 5450,
      nextTokenNum: 5700,
      itemID: "char_4025_aprot2",
      itemType: "CHAR",
      itemCount: 1,
      isGoodPrize: false,
      isGrandPrize: true,
    },
    {
      id: "bp_level_26",
      level: 26,
      tokenNum: 5700,
      nextTokenNum: 5950,
      itemID: "4001",
      itemType: "GOLD",
      itemCount: 30000,
      isGoodPrize: false,
      isGrandPrize: false,
    },
    {
      id: "bp_level_27",
      level: 27,
      tokenNum: 5950,
      nextTokenNum: 6200,
      itemID: "30135",
      itemType: "MATERIAL",
      itemCount: 1,
      isGoodPrize: true,
      isGrandPrize: false,
    },
    {
      id: "bp_level_28",
      level: 28,
      tokenNum: 6200,
      nextTokenNum: 6475,
      itemID: "2004",
      itemType: "CARD_EXP",
      itemCount: 15,
      isGoodPrize: false,
      isGrandPrize: false,
    },
    {
      id: "bp_level_29",
      level: 29,
      tokenNum: 6475,
      nextTokenNum: 6750,
      itemID: "30024",
      itemType: "MATERIAL",
      itemCount: 3,
      isGoodPrize: false,
      isGrandPrize: false,
    },
    {
      id: "bp_level_30",
      level: 30,
      tokenNum: 6750,
      nextTokenNum: 7025,
      itemID: "p_char_4025_aprot2",
      itemType: "MATERIAL",
      itemCount: 1,
      isGoodPrize: true,
      isGrandPrize: false,
    },
    {
      id: "bp_level_31",
      level: 31,
      tokenNum: 7025,
      nextTokenNum: 7300,
      itemID: "4001",
      itemType: "GOLD",
      itemCount: 30000,
      isGoodPrize: false,
      isGrandPrize: false,
    },
    {
      id: "bp_level_32",
      level: 32,
      tokenNum: 7300,
      nextTokenNum: 7575,
      itemID: "30014",
      itemType: "MATERIAL",
      itemCount: 3,
      isGoodPrize: false,
      isGrandPrize: false,
    },
    {
      id: "bp_level_33",
      level: 33,
      tokenNum: 7575,
      nextTokenNum: 7850,
      itemID: "2004",
      itemType: "CARD_EXP",
      itemCount: 15,
      isGoodPrize: false,
      isGrandPrize: false,
    },
    {
      id: "bp_level_34",
      level: 34,
      tokenNum: 7850,
      nextTokenNum: 8125,
      itemID: "31024",
      itemType: "MATERIAL",
      itemCount: 3,
      isGoodPrize: false,
      isGrandPrize: false,
    },
    {
      id: "bp_level_35",
      level: 35,
      tokenNum: 8125,
      nextTokenNum: 8400,
      itemID: "p_char_4025_aprot2",
      itemType: "MATERIAL",
      itemCount: 1,
      isGoodPrize: true,
      isGrandPrize: false,
    },
    {
      id: "bp_level_36",
      level: 36,
      tokenNum: 8400,
      nextTokenNum: 8700,
      itemID: "4001",
      itemType: "GOLD",
      itemCount: 30000,
      isGoodPrize: false,
      isGrandPrize: false,
    },
    {
      id: "bp_level_37",
      level: 37,
      tokenNum: 8700,
      nextTokenNum: 9000,
      itemID: "30125",
      itemType: "MATERIAL",
      itemCount: 1,
      isGoodPrize: true,
      isGrandPrize: false,
    },
    {
      id: "bp_level_38",
      level: 38,
      tokenNum: 9000,
      nextTokenNum: 9300,
      itemID: "2004",
      itemType: "CARD_EXP",
      itemCount: 15,
      isGoodPrize: false,
      isGrandPrize: false,
    },
    {
      id: "bp_level_39",
      level: 39,
      tokenNum: 9300,
      nextTokenNum: 9600,
      itemID: "30094",
      itemType: "MATERIAL",
      itemCount: 3,
      isGoodPrize: false,
      isGrandPrize: false,
    },
    {
      id: "bp_level_40",
      level: 40,
      tokenNum: 9600,
      nextTokenNum: 9900,
      itemID: "p_char_4025_aprot2",
      itemType: "MATERIAL",
      itemCount: 1,
      isGoodPrize: true,
      isGrandPrize: false,
    },
    {
      id: "bp_level_41",
      level: 41,
      tokenNum: 9900,
      nextTokenNum: 10200,
      itemID: "4001",
      itemType: "GOLD",
      itemCount: 50000,
      isGoodPrize: false,
      isGrandPrize: false,
    },
    {
      id: "bp_level_42",
      level: 42,
      tokenNum: 10200,
      nextTokenNum: 10500,
      itemID: "30064",
      itemType: "MATERIAL",
      itemCount: 3,
      isGoodPrize: false,
      isGrandPrize: false,
    },
    {
      id: "bp_level_43",
      level: 43,
      tokenNum: 10500,
      nextTokenNum: 10825,
      itemID: "2004",
      itemType: "CARD_EXP",
      itemCount: 20,
      isGoodPrize: false,
      isGrandPrize: false,
    },
    {
      id: "bp_level_44",
      level: 44,
      tokenNum: 10825,
      nextTokenNum: 11150,
      itemID: "30104",
      itemType: "MATERIAL",
      itemCount: 3,
      isGoodPrize: false,
      isGrandPrize: false,
    },
    {
      id: "bp_level_45",
      level: 45,
      tokenNum: 11150,
      nextTokenNum: 11475,
      itemID: "p_char_4025_aprot2",
      itemType: "MATERIAL",
      itemCount: 1,
      isGoodPrize: true,
      isGrandPrize: false,
    },
    {
      id: "bp_level_46",
      level: 46,
      tokenNum: 11475,
      nextTokenNum: 11800,
      itemID: "4001",
      itemType: "GOLD",
      itemCount: 50000,
      isGoodPrize: false,
      isGrandPrize: false,
    },
    {
      id: "bp_level_47",
      level: 47,
      tokenNum: 11800,
      nextTokenNum: 12200,
      itemID: "30115",
      itemType: "MATERIAL",
      itemCount: 1,
      isGoodPrize: true,
      isGrandPrize: false,
    },
    {
      id: "bp_level_48",
      level: 48,
      tokenNum: 12200,
      nextTokenNum: 12600,
      itemID: "2004",
      itemType: "CARD_EXP",
      itemCount: 20,
      isGoodPrize: false,
      isGrandPrize: false,
    },
    {
      id: "bp_level_49",
      level: 49,
      tokenNum: 12600,
      nextTokenNum: 13000,
      itemID: "30054",
      itemType: "MATERIAL",
      itemCount: 3,
      isGoodPrize: false,
      isGrandPrize: false,
    },
    {
      id: "bp_level_50",
      level: 50,
      tokenNum: 13000,
      nextTokenNum: 13400,
      itemID: "p_char_4025_aprot2",
      itemType: "MATERIAL",
      itemCount: 1,
      isGoodPrize: true,
      isGrandPrize: false,
    },
    {
      id: "bp_level_51",
      level: 51,
      tokenNum: 13400,
      nextTokenNum: 13800,
      itemID: "4001",
      itemType: "GOLD",
      itemCount: 50000,
      isGoodPrize: false,
      isGrandPrize: false,
    },
    {
      id: "bp_level_52",
      level: 52,
      tokenNum: 13800,
      nextTokenNum: 14200,
      itemID: "2004",
      itemType: "CARD_EXP",
      itemCount: 20,
      isGoodPrize: false,
      isGrandPrize: false,
    },
    {
      id: "bp_level_53",
      level: 53,
      tokenNum: 14200,
      nextTokenNum: 14600,
      itemID: "30074",
      itemType: "MATERIAL",
      itemCount: 3,
      isGoodPrize: false,
      isGrandPrize: false,
    },
    {
      id: "bp_level_54",
      level: 54,
      tokenNum: 14600,
      nextTokenNum: 15000,
      itemID: "3301",
      itemType: "MATERIAL",
      itemCount: 30,
      isGoodPrize: false,
      isGrandPrize: false,
    },
    {
      id: "bp_level_55",
      level: 55,
      tokenNum: 15000,
      nextTokenNum: 15400,
      itemID: "30145",
      itemType: "MATERIAL",
      itemCount: 1,
      isGoodPrize: true,
      isGrandPrize: false,
    },
    {
      id: "bp_level_56",
      level: 56,
      tokenNum: 15400,
      nextTokenNum: 15800,
      itemID: "4001",
      itemType: "GOLD",
      itemCount: 50000,
      isGoodPrize: false,
      isGrandPrize: false,
    },
    {
      id: "bp_level_57",
      level: 57,
      tokenNum: 15800,
      nextTokenNum: 16200,
      itemID: "2004",
      itemType: "CARD_EXP",
      itemCount: 20,
      isGoodPrize: false,
      isGrandPrize: false,
    },
    {
      id: "bp_level_58",
      level: 58,
      tokenNum: 16200,
      nextTokenNum: 16600,
      itemID: "avatar_activity_RL1_1",
      itemType: "PLAYER_AVATAR",
      itemCount: 1,
      isGoodPrize: false,
      isGrandPrize: true,
    },
    {
      id: "bp_level_59",
      level: 59,
      tokenNum: 16600,
      nextTokenNum: 17000,
      itemID: "3302",
      itemType: "MATERIAL",
      itemCount: 10,
      isGoodPrize: false,
      isGrandPrize: false,
    },
    {
      id: "bp_level_60",
      level: 60,
      tokenNum: 17000,
      nextTokenNum: 17400,
      itemID: "30084",
      itemType: "MATERIAL",
      itemCount: 3,
      isGoodPrize: false,
      isGrandPrize: false,
    },
    {
      id: "bp_level_61",
      level: 61,
      tokenNum: 17400,
      nextTokenNum: 17800,
      itemID: "4001",
      itemType: "GOLD",
      itemCount: 50000,
      isGoodPrize: false,
      isGrandPrize: false,
    },
    {
      id: "bp_level_62",
      level: 62,
      tokenNum: 17800,
      nextTokenNum: 18200,
      itemID: "2004",
      itemType: "CARD_EXP",
      itemCount: 20,
      isGoodPrize: false,
      isGrandPrize: false,
    },
    {
      id: "bp_level_63",
      level: 63,
      tokenNum: 18200,
      nextTokenNum: 18600,
      itemID: "30135",
      itemType: "MATERIAL",
      itemCount: 1,
      isGoodPrize: true,
      isGrandPrize: false,
    },
    {
      id: "bp_level_64",
      level: 64,
      tokenNum: 18600,
      nextTokenNum: 19000,
      itemID: "3303",
      itemType: "MATERIAL",
      itemCount: 3,
      isGoodPrize: false,
      isGrandPrize: false,
    },
    {
      id: "bp_level_65",
      level: 65,
      tokenNum: 19000,
      nextTokenNum: 19400,
      itemID: "avatar_activity_RL1_2",
      itemType: "PLAYER_AVATAR",
      itemCount: 1,
      isGoodPrize: false,
      isGrandPrize: true,
    },
    {
      id: "bp_level_66",
      level: 66,
      tokenNum: 19400,
      nextTokenNum: 19800,
      itemID: "4001",
      itemType: "GOLD",
      itemCount: 50000,
      isGoodPrize: false,
      isGrandPrize: false,
    },
    {
      id: "bp_level_67",
      level: 67,
      tokenNum: 19800,
      nextTokenNum: 20200,
      itemID: "2004",
      itemType: "CARD_EXP",
      itemCount: 20,
      isGoodPrize: false,
      isGrandPrize: false,
    },
    {
      id: "bp_level_68",
      level: 68,
      tokenNum: 20200,
      nextTokenNum: 20600,
      itemID: "31014",
      itemType: "MATERIAL",
      itemCount: 3,
      isGoodPrize: false,
      isGrandPrize: false,
    },
    {
      id: "bp_level_69",
      level: 69,
      tokenNum: 20600,
      nextTokenNum: 21000,
      itemID: "3301",
      itemType: "MATERIAL",
      itemCount: 30,
      isGoodPrize: false,
      isGrandPrize: false,
    },
    {
      id: "bp_level_70",
      level: 70,
      tokenNum: 21000,
      nextTokenNum: 21400,
      itemID: "30125",
      itemType: "MATERIAL",
      itemCount: 1,
      isGoodPrize: true,
      isGrandPrize: false,
    },
    {
      id: "bp_level_71",
      level: 71,
      tokenNum: 21400,
      nextTokenNum: 21800,
      itemID: "4001",
      itemType: "GOLD",
      itemCount: 50000,
      isGoodPrize: false,
      isGrandPrize: false,
    },
    {
      id: "bp_level_72",
      level: 72,
      tokenNum: 21800,
      nextTokenNum: 22200,
      itemID: "2004",
      itemType: "CARD_EXP",
      itemCount: 20,
      isGoodPrize: false,
      isGrandPrize: false,
    },
    {
      id: "bp_level_73",
      level: 73,
      tokenNum: 22200,
      nextTokenNum: 22600,
      itemID: "30034",
      itemType: "MATERIAL",
      itemCount: 3,
      isGoodPrize: false,
      isGrandPrize: false,
    },
    {
      id: "bp_level_74",
      level: 74,
      tokenNum: 22600,
      nextTokenNum: 23000,
      itemID: "3302",
      itemType: "MATERIAL",
      itemCount: 10,
      isGoodPrize: false,
      isGrandPrize: false,
    },
    {
      id: "bp_level_75",
      level: 75,
      tokenNum: 23000,
      nextTokenNum: 23400,
      itemID: "31054",
      itemType: "MATERIAL",
      itemCount: 3,
      isGoodPrize: false,
      isGrandPrize: false,
    },
    {
      id: "bp_level_76",
      level: 76,
      tokenNum: 23400,
      nextTokenNum: 23800,
      itemID: "4001",
      itemType: "GOLD",
      itemCount: 50000,
      isGoodPrize: false,
      isGrandPrize: false,
    },
    {
      id: "bp_level_77",
      level: 77,
      tokenNum: 23800,
      nextTokenNum: 24200,
      itemID: "2004",
      itemType: "CARD_EXP",
      itemCount: 20,
      isGoodPrize: false,
      isGrandPrize: false,
    },
    {
      id: "bp_level_78",
      level: 78,
      tokenNum: 24200,
      nextTokenNum: 24600,
      itemID: "30115",
      itemType: "MATERIAL",
      itemCount: 1,
      isGoodPrize: true,
      isGrandPrize: false,
    },
    {
      id: "bp_level_79",
      level: 79,
      tokenNum: 24600,
      nextTokenNum: 25000,
      itemID: "3303",
      itemType: "MATERIAL",
      itemCount: 3,
      isGoodPrize: false,
      isGrandPrize: false,
    },
    {
      id: "bp_level_80",
      level: 80,
      tokenNum: 25000,
      nextTokenNum: 25400,
      itemID: "uni_set_castle_1",
      itemType: "UNI_COLLECTION",
      itemCount: 1,
      isGoodPrize: false,
      isGrandPrize: true,
    },
    {
      id: "bp_level_81",
      level: 81,
      tokenNum: 25400,
      nextTokenNum: 25800,
      itemID: "4001",
      itemType: "GOLD",
      itemCount: 50000,
      isGoodPrize: false,
      isGrandPrize: false,
    },
    {
      id: "bp_level_82",
      level: 82,
      tokenNum: 25800,
      nextTokenNum: 26200,
      itemID: "2004",
      itemType: "CARD_EXP",
      itemCount: 20,
      isGoodPrize: false,
      isGrandPrize: false,
    },
    {
      id: "bp_level_83",
      level: 83,
      tokenNum: 26200,
      nextTokenNum: 26600,
      itemID: "31044",
      itemType: "MATERIAL",
      itemCount: 3,
      isGoodPrize: false,
      isGrandPrize: false,
    },
    {
      id: "bp_level_84",
      level: 84,
      tokenNum: 26600,
      nextTokenNum: 27000,
      itemID: "3301",
      itemType: "MATERIAL",
      itemCount: 30,
      isGoodPrize: false,
      isGrandPrize: false,
    },
    {
      id: "bp_level_85",
      level: 85,
      tokenNum: 27000,
      nextTokenNum: 27400,
      itemID: "30145",
      itemType: "MATERIAL",
      itemCount: 1,
      isGoodPrize: true,
      isGrandPrize: false,
    },
    {
      id: "bp_level_86",
      level: 86,
      tokenNum: 27400,
      nextTokenNum: 27800,
      itemID: "4001",
      itemType: "GOLD",
      itemCount: 50000,
      isGoodPrize: false,
      isGrandPrize: false,
    },
    {
      id: "bp_level_87",
      level: 87,
      tokenNum: 27800,
      nextTokenNum: 28200,
      itemID: "2004",
      itemType: "CARD_EXP",
      itemCount: 20,
      isGoodPrize: false,
      isGrandPrize: false,
    },
    {
      id: "bp_level_88",
      level: 88,
      tokenNum: 28200,
      nextTokenNum: 28600,
      itemID: "31034",
      itemType: "MATERIAL",
      itemCount: 3,
      isGoodPrize: false,
      isGrandPrize: false,
    },
    {
      id: "bp_level_89",
      level: 89,
      tokenNum: 28600,
      nextTokenNum: 29000,
      itemID: "3302",
      itemType: "MATERIAL",
      itemCount: 10,
      isGoodPrize: false,
      isGrandPrize: false,
    },
    {
      id: "bp_level_90",
      level: 90,
      tokenNum: 29000,
      nextTokenNum: 29400,
      itemID: "30044",
      itemType: "MATERIAL",
      itemCount: 3,
      isGoodPrize: false,
      isGrandPrize: false,
    },
    {
      id: "bp_level_91",
      level: 91,
      tokenNum: 29400,
      nextTokenNum: 29800,
      itemID: "4001",
      itemType: "GOLD",
      itemCount: 50000,
      isGoodPrize: false,
      isGrandPrize: false,
    },
    {
      id: "bp_level_92",
      level: 92,
      tokenNum: 29800,
      nextTokenNum: 30200,
      itemID: "2004",
      itemType: "CARD_EXP",
      itemCount: 20,
      isGoodPrize: false,
      isGrandPrize: false,
    },
    {
      id: "bp_level_93",
      level: 93,
      tokenNum: 30200,
      nextTokenNum: 30600,
      itemID: "30135",
      itemType: "MATERIAL",
      itemCount: 1,
      isGoodPrize: true,
      isGrandPrize: false,
    },
    {
      id: "bp_level_94",
      level: 94,
      tokenNum: 30600,
      nextTokenNum: 31000,
      itemID: "3303",
      itemType: "MATERIAL",
      itemCount: 3,
      isGoodPrize: false,
      isGrandPrize: false,
    },
    {
      id: "bp_level_95",
      level: 95,
      tokenNum: 31000,
      nextTokenNum: -1,
      itemID: "char_250_phatom@sale#4",
      itemType: "CHAR_SKIN",
      itemCount: 1,
      isGoodPrize: false,
      isGrandPrize: true,
    },
  ];
  levelStart = 0;
  levelEnd = 95;
  bpNum = 200;
  bpCost = 1;

  /**
   * calculate token number for level up
   */
  public get calculateToken(): number {
    // check levelStart and levelEnd is not float
    if (this.levelStart % 1 !== 0 || this.levelEnd % 1 !== 0) {
      return -1;
    }

    // check levelStart and levelEnd between 0 and 95 and levelStart is bigger then levelEnd
    if (
        this.levelStart < 0 ||
        this.levelStart > 95 ||
        this.levelEnd < 0 ||
        this.levelEnd > 95 ||
        this.levelStart > this.levelEnd
    ) {
      return -1;
    }
    let tokenStart = 0;
    let tokenEnd = 0;
    if (this.levelStart != 0)
      tokenStart = this.bpData[this.levelStart - 1].tokenNum;
    if (this.levelEnd != 0)
      tokenEnd = this.bpData[this.levelEnd - 1].tokenNum;
    return tokenEnd - tokenStart;
  }

  public get calculateCost(): number {
    return this.bpCost * this.calculateToken / this.bpNum;
  }
}
</script>

<style>
.el-row {
  margin-bottom: 20px;
}

.number {
  font-size: 2em;
  color: #397f4b;
}
</style>