<template>
    <div id="app">
        <div class="table">
            <div class="board">
                <div class="center">
                    <div class="community-chest-deck">
                        <h2 class="label">Community Chest</h2>
                        <div class="deck"></div>
                    </div>
                    <h1 class="title">MONOPOLY</h1>
                    <div class="chance-deck">
                        <h2 class="label">Chance</h2>
                        <div class="deck"></div>
                    </div>
                </div>

                <div v-for="side in board"
                     v-bind:key="side.hash"
                     v-bind:class="side.classes">
                    <div v-for="cell in side.cells"
                         v-bind:key="cell.index"
                         v-bind:class="cell.classes"
                         :id="'cell-' + cell.index">
                        <div class="container">
                            <div v-for="cont in cell.container_entries"
                                 v-bind:key="cont.hash">
                                <div v-if="cont.icon" v-bind:class="cont.classes">
                                    <font-awesome-icon :icon="cont.icon"/>
                                </div>
                                <div v-else v-bind:class="cont.classes">
                                    {{ cont.content }}
                                </div>
                            </div>
                        </div>
                        <div v-bind:class="cell.postdiv_classes"></div>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>
<script>
var genPropertySquare = function (index, color, name, price) {
  return {
    'index': index,
    'classes': ['space', 'property'],
    'container_entries': [
      {
        'classes': ['color-bar', color],
        'content': ''
      },
      {
        'classes': ['name'],
        'content': name
      },
      {
        'classes': ['price'],
        'content': 'Price $' + price
      }
    ]
  }
}

var genChanceSquare = function (index) {
  return {
    'index': index,
    'classes': ['space', 'chance'],
    'container_entries': [
      {
        'classes': ['name'],
        'content': 'Chance'
      },
      {
        'classes': ['drawing'],
        'icon': 'question'
      }
    ]
  }
}

var genSpecialSquare = function (index, name, price, icon, classes) {
  return {
    'index': index,
    'classes': ['space', classes],
    'container_entries': [
      {
        'classes': ['name'],
        'content': name
      },
      {
        'classes': ['drawing'],
        'icon': icon
      },
      {
        'classes': ['price'],
        'content': 'Price $' + price
      }
    ]
  }
}

var genTaxSquare = function (index) {
  return {
    'index': index,
    'classes': ['space', 'income-tax'],
    'container_entries': [
      {
        'classes': ['name'],
        'content': 'Income Tax'
      },
      {
        'classes': ['diamond'],
        'content': ''
      },
      {
        'classes': ['instructions'],
        'content': 'Pay 10% or $200'
      },
    ]
  }
}

var genLuxTaxSquare = function (index) {
  return {
    'index': index,
    'classes': ['space', 'fee', 'luxury-tax'],
    'container_entries': [
      {
        'classes': ['name'],
        'content': 'Luxury Tax'
      },
      {
        'classes': ['drawing'],
        'icon': 'gem'
      },
      {
        'classes': ['instructions'],
        'content': 'Pay $75.00'
      },
    ]
  }
}



var genCommunityChest = function (index) {
  return {
    'index': index,
    'classes': ['space', 'community-chest'],
    'container_entries': [
      {
        'classes': ['name'],
        'content': 'Community Chest'
      },
      {
        'classes': ['drawing'],
        'icon': 'cube'
      },
      {
        'classes': ['instructions'],
        'content': 'Follow instructions on top card'
      },
    ]
  }
}

var genFreeParking = function (index) {
  return {
    'index': index,
    'classes': ['space', 'corner', 'free-parking'],
    'container_entries': [
      {
        'classes': ['name'],
        'content': 'Free'
      },
      {
        'classes': ['drawing'],
        'icon': 'car'
      },
      {
        'classes': ['name'],
        'content': 'Parking'
      },
    ]
  }
}

var genGoToJail = function (index) {
  return {
    'index': index,
    'classes': ['space', 'corner', 'go-to-jail'],
    'container_entries': [
      {
        'classes': ['name'],
        'content': 'Go To'
      },
      {
        'classes': ['drawing'],
        'icon': 'gavel'
      },
      {
        'classes': ['name'],
        'content': 'Jail'
      },
    ]
  }
}

var genStartSquare = function (index) {
  return {
    'index': index,
    'classes': ['space', 'corner', 'go'],
    'container_entries': [
      {
        'classes': ['instructions'],
        'content': 'Collect $200.00 salary as you pass.'
      },
      {
        'classes': ['go-word'],
        'content': 'go'
      }
    ],
    'postdiv_classes': ['arrow', 'fa', 'fa-long-arrow-left']
  }
}

export default {
  name: 'App',
  data: function () {
    return {
      board: [
        {
          'classes': [],
          'cells': [
            genStartSquare(0)
          ]
        },
        {
          'classes': ['row', 'horizontal-row', 'bottom-row'],
          'cells': [
            genPropertySquare(9, 'light-blue', 'Connecticut Avenue', 120),
            genPropertySquare(8, 'light-blue', 'Vermont Avenue', 100),
            genChanceSquare(7),
            genPropertySquare(6, 'light-blue', 'Oriental Avenue', 100),
            genSpecialSquare(5, 'Reading Railroad', 200, 'subway', ['railroad']),
            genTaxSquare(4),
            genPropertySquare(3, 'dark-purple', 'Baltic Avenue', 50),
            genCommunityChest(2),
            genPropertySquare(1, 'dark-purple', 'Mediterranean Avenue', 50)
          ]
        },
        {
            // TODO: JAIL
            /*
            <div class="space corner jail" id="cell10">
                <div class="just">Just</div>
                <div class="drawing">
                    <div class="container">
                        <div class="name">In</div>
                        <div class="window">
                            <div class="bar"></div>
                            <div class="bar"></div>
                            <div class="bar"></div>
                            <i class="person fa fa-frown-o"></i>
                        </div>
                        <div class="name">Jail</div>
                    </div>
                </div>
                <div class="visiting">Visiting</div>
            </div>
            */
          'classes': [],
          'cells': [
            genFreeParking(10)
          ]
        },
        {
          'classes': ['row', 'vertical-row', 'left-row'],
          'cells': [
            genPropertySquare(19, 'orange', 'New York Avenue', 200),
            genPropertySquare(18, 'orange', 'Tennesee Avenue', 180),
            genCommunityChest(17),
            genPropertySquare(16, 'orange', 'St. James Avenue', 180),
            genSpecialSquare(15, 'Pennsylvania Railroad', 200, 'subway', ['railroad']),
            genPropertySquare(14, 'purple', 'Virginia Avenue', 160),
            genPropertySquare(13, 'purple', 'States Avenue', 140),
            genSpecialSquare(12, 'Electric Company', 150, 'lightbulb', ['utility', 'electric-company']),
            genPropertySquare(11, 'purple', 'St. Charles Place', 160),
          ]
        },
        {
          'classes': [],
          'cells': [
            genFreeParking(20)
          ]
        },
        {
          'classes': ['row', 'horizontal-row', 'top-row'],
          'cells': [
            genPropertySquare(21, 'red', 'Kentucky Avenue', 220),
            genChanceSquare(22),
            genPropertySquare(23, 'red', 'Indiana Avenue', 220),
            genPropertySquare(24, 'red', 'Illinois Avenue', 200),
            genSpecialSquare(25, 'B & O Railroad', 200, 'subway', ['railroad']),
            genPropertySquare(26, 'yellow', 'Atlantic Avenue', 260),
            genPropertySquare(27, 'yellow', 'Ventnor Avenue', 260),
            genSpecialSquare(28, 'Waterworks', 120, 'tint', ['utility', 'waterworks']),
            genPropertySquare(29, 'yellow', 'Marvin Gardens', 280),
          ]
        },
        {
          'classes': [],
          'cells': [
            genGoToJail(30)
          ]
        },
        {
          'classes': ['row', 'vertical-row', 'right-row'],
          'cells': [
            genPropertySquare(31, 'green', 'Pacific Avenue', 300),
            genPropertySquare(32, 'green', 'North Carolina Avenue', 300),
            genCommunityChest(33),
            genPropertySquare(34, 'green', 'Pennsylvania Avenue', 320),
            genSpecialSquare(35, 'Short Line', 200, 'subway', ['railroad']),
            genChanceSquare(36),
            genPropertySquare(37, 'dark-blue', 'Park Place', 350),
            genLuxTaxSquare(38),
            genPropertySquare(39, 'dark-blue', 'Boardwalk', 400),
          ]
        },
      ]
    }
  }
}
</script>

<style>
* {
  box-sizing: border-box;
}

body {
  margin: 0;
  background-position: center;
  background-repeat: repeat;
  background-size: 100px;
  font-family: "Oswald", sans-serif;
  font-weight: 400;
  font-size: 10px;
  color: #080808;
  text-transform: uppercase;
}

h1, h2, h3, h4, h5, h6 {
  margin: 0;
}

.dark-purple {
  background: #5e3577;
}

.light-blue {
  background: #d2eaf5;
}

.purple {
  background: #b02f7c;
}

.orange {
  background: #fa811d;
}

.red {
  background: #f50c2b;
}

.yellow {
  background: #ffed20;
}

.green {
  background: #41994e;
}

.dark-blue {
  background: #5a6dba;
}

.table {
  padding-left: 50px;
  padding-right: 50px;
}

.board {
  display: grid;
  grid-template-columns: 125px repeat(9, 80px) 125px;
  grid-template-rows: 125px repeat(9, 80px) 125px;
  grid-gap: 2px;
  margin: 50px auto;
  width: 994px;
  height: 994px;
  background: #080808;
  border: 2px solid #080808;
}

.center {
  grid-column: 2/11;
  grid-row: 2/11;
  background: #fafaf8;
  display: grid;
  grid-template-columns: repeat(7, 1fr);
  grid-template-rows: repeat(7, 1fr);
  justify-items: center;
  align-items: center;
}

.title {
  grid-column: 1/9;
  grid-row: 4;
  font-size: 90px;
  font-weight: 400;
  letter-spacing: 12px;
}

.community-chest-deck {
  grid-column: 2/4;
  grid-row: 2/4;
  transform: rotate(135deg);
  margin-bottom: 60px;
  margin-right: 60px;
}

.chance-deck {
  grid-column: 5/7;
  grid-row: 5/7;
  transform: rotate(315deg);
  margin-top: 60px;
  margin-left: 60px;
}

.label {
  text-align: center;
  font-weight: 500;
  letter-spacing: 3px;
  padding-bottom: 10px;
}

.deck {
  border: 2px dashed #080808;
  width: 160px;
  height: 120px;
}

.row {
  display: grid;
  grid-gap: 2px;
}

.horizontal-row {
  grid-template-columns: repeat(9, 80px);
  grid-template-rows: 125px;
}

.vertical-row {
  grid-template-columns: 125px;
  grid-template-rows: repeat(9, 80px);
}
.vertical-row .container {
  top: 50%;
  left: 50%;
}

.bottom-row {
  grid-column: 2/11;
  grid-row: 11;
}

.left-row {
  grid-column: 1;
  grid-row: 2/11;
}
.left-row .container {
  transform: translate(-50%, -50%) rotate(90deg);
}

.top-row {
  grid-column: 2/11;
  grid-row: 1;
}
.top-row .container {
  transform: rotate(180deg);
}

.right-row {
  grid-column: 11;
  grid-row: 2/11;
}
.right-row .container {
  transform: translate(-50%, -50%) rotate(270deg);
}

.space {
  background: #fafaf8;
  text-align: center;
}
.space .container {
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  position: relative;
  transform-origin: center;
  height: 125px;
  width: 80px;
}
.space .name,
.space .instructions {
  padding-left: 15px;
  padding-right: 15px;
}
.space .price {
  font-size: 7px;
  font-weight: 400;
  padding-bottom: 5px;
}

.corner .container {
  justify-content: space-around;
  height: 100%;
  width: 100%;
}
.corner .name {
  padding: 0;
}

.property .color-bar {
  height: 25px;
  border-bottom: 2px solid #080808;
}
.property .name {
  padding-bottom: 50px;
}

.railroad .name {
  padding-top: 10px;
}
.railroad .drawing {
  font-size: 60px;
  color: #080808;
}

.utility .name {
  padding-top: 10px;
}
.utility .drawing {
  font-size: 70px;
}

.fee .name {
  padding-top: 10px;
  font-size: 14px;
}
.fee .instructions {
  font-size: 10px;
}

.go {
  grid-column: 11;
  grid-row: 11/12;
  position: relative;
}
.go .container {
  justify-content: flex-start;
  transform: rotate(315deg);
}
.go .instructions {
  padding: 0 30px;
}
.go .go-word {
  font-size: 60px;
  color: #f50c2b;
}
.go .arrow {
  font-size: 45px;
  color: #f50c2b;
  position: absolute;
  bottom: -10px;
  left: 5px;
}

.jail {
  grid-column: 1;
  grid-row: 11/12;
  display: grid;
  grid-template-columns: repeat(10, 12.5px);
  grid-template-rows: repeat(10, 12.5px);
  justify-content: center;
  align-items: center;
}
.jail .drawing {
  grid-column: 4/11;
  grid-row: 1/8;
  width: 87.5px;
  height: 87.5px;
  background: #fa811d;
  border-bottom: 2px solid #080808;
  border-left: 2px solid #080808;
}
.jail .just {
  grid-column: 3;
  grid-row: 4;
  transform: rotate(90deg);
  padding-top: 5px;
}
.jail .visiting {
  grid-column: 6;
  grid-row: 8;
  padding-top: 5px;
}
.jail .container {
  align-items: center;
  transform: rotate(45deg);
}
.jail .name {
  font-size: 14px;
}
.jail .window {
  display: flex;
  justify-content: space-around;
  align-items: center;
  position: relative;
  width: 55px;
  height: 55px;
  background: #fafaf8;
  border: 2px solid #080808;
}
.jail .person {
  position: absolute;
  transform: translate(-50%, -50%);
  top: 50%;
  left: 50%;
  font-size: 40px;
}
.jail .bar {
  height: 55px;
  width: 2px;
  background: #080808;
}

.free-parking {
  grid-column: 1;
  grid-row: 1/2;
}
.free-parking .container {
  justify-content: center;
  transform: rotate(135deg);
}
.free-parking .name {
  font-size: 16px;
}
.free-parking .drawing {
  font-size: 60px;
  color: #f50c2b;
  padding-top: 5px;
  padding-bottom: 5px;
}

.go-to-jail {
  grid-column: 11;
  grid-row: 1/1;
}
.go-to-jail .container {
  justify-content: center;
  transform: rotate(225deg);
}
.go-to-jail .name {
  font-size: 16px;
}
.go-to-jail .drawing {
  font-size: 60px;
  color: #640303;
  padding-top: 5px;
  padding-bottom: 5px;
}

.chance .container {
  justify-content: center;
}
.chance .drawing {
  font-size: 90px;
  color: #f50c2b;
}
.chance .blue {
  color: #5a6dba;
}

.community-chest .container {
  justify-content: space-around;
}
.community-chest .drawing {
  font-size: 50px;
  color: #d2eaf5;
}
.community-chest .instructions {
  font-size: 8px;
}

.electric-company .drawing {
  color: #ffed20;
}

.waterworks .drawing {
  color: #5a6dba;
}

.income-tax .container {
  justify-content: center;
  align-items: center;
}
.income-tax .name {
  padding-bottom: 5px;
}
.income-tax .gem {
  width: 5px;
  height: 5px;
  background: #080808;
  transform: rotate(45deg);
  display: inline-block;
}
.income-tax .instructions {
  padding-top: 5px;
  padding-bottom: 5px;
}

.luxury-tax .drawing {
  font-size: 50px;
}
.luxury-tax .instructions {
  padding-bottom: 5px;
}

.long-name {
  padding-left: 0 !important;
  padding-right: 0 !important;
}

.three-line-name {
  position: relative;
  top: 5px;
}
</style>
