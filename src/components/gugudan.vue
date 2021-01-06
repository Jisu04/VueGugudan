<template>
  <div id="wrap">
    <header>
        <p id="title">구구단 계산기</p>
    </header>
    <div id="content">
      <input type="number" id="inputNumber"
      v-model="inputNumber"
      v-on:keyup.enter="createResult()"
      >

      <div id="resultList">
        <div id="listHeader">
          <h5>결과</h5>
          <button id="listReset" @click="ResetList()">Reset</button>
        </div>
        <div class="resultBox" v-for="(num,idx) in RList" :key="idx">
          <h5>검색 : {{num.num}}단</h5>
          <p><span>{{num.num}}</span> <span>x</span> <span>1</span> <span>=</span> <span>{{num.num*1}}</span></p>
          <p><span>{{num.num}}</span> <span>x</span> <span>2</span> <span>=</span> <span>{{num.num*2}}</span></p>
          <p><span>{{num.num}}</span> <span>x</span> <span>3</span> <span>=</span> <span>{{num.num*3}}</span></p>
          <p><span>{{num.num}}</span> <span>x</span> <span>4</span> <span>=</span> <span>{{num.num*4}}</span></p>
          <p><span>{{num.num}}</span> <span>x</span> <span>5</span> <span>=</span> <span>{{num.num*5}}</span></p>
          <p><span>{{num.num}}</span> <span>x</span> <span>6</span> <span>=</span> <span>{{num.num*6}}</span></p>
          <p><span>{{num.num}}</span> <span>x</span> <span>7</span> <span>=</span> <span>{{num.num*7}}</span></p>
          <p><span>{{num.num}}</span> <span>x</span> <span>8</span> <span>=</span> <span>{{num.num*8}}</span></p>
          <p><span>{{num.num}}</span> <span>x</span> <span>9</span> <span>=</span> <span>{{num.num*9}}</span></p>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
  export default{
    data(){
      return{
        inputNumber:null,
        RList:new Array()
      }
    },
    methods:{
      createResult(){        
        let number = parseInt(this.inputNumber);
        this.inputNumber = null;

        if(isNaN(number)) return alert("숫자만 입력해주세요!");
        if(number < 1) return alert("1이상의 숫자를 입력해주세요!");

        this.RList.unshift({num:number});
      },
      ResetList(){
        this.RList = [];
      }
    }
  }
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

header{
  background-color: #f2f2f2;
  width: 100%;
}

#title{
  padding: 20px;
  font-weight: bold;
  font-size: 25px;
}

#content{
  width: 100%;
  display: flex;
  justify-content: flex-start;
  flex-wrap: wrap;
}

#inputNumber{
  padding: 10px;
  border: 2px solid #ddd;
  border-radius: 5px;
  margin: 10px;
  width: 100px;
  height: 20px;
}

#listHeader{
  width: 100%;
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 10px;
}

#listHeader > h5{
  font-size: 20px;
}

#listReset{
  background-color: #333;
  border: none;
  border-radius: 5px;
  color: #fff;
  padding: 10px;
  transition: .3s all;
  cursor: pointer;
}

#listReset:hover{opacity: 0.8;}

#resultList{
  width: 200px;
  padding: 10px;
  display: flex;
  flex-direction: column;
}

.resultBox{
  padding: 10px 20px;
  margin-bottom: 20px;
  background-color: #555;
  border-radius: 5px;
  width: 150px;
  transition: 0.3s all;
  cursor: pointer;
}

.resultBox:hover{box-shadow: 5px 5px 10px #ddd;}

.resultBox  *{color: #fff;}
.resultBox > h5{
  font-size: 17px;
  margin-bottom: 10px;
}

.resultBox > p{
  display: flex;
  justify-content: space-between;
}

</style>
