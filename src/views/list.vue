<!--
 * @Description: 
 * @Version: 1.0
 * @Autor: Li Cheng
 * @Date: 2024-06-24 14:34:13
 * @LastEditors: Li Cheng
 * @LastEditTime: 2024-06-24 15:01:55
-->
<template>
  <div class="list-comp">
    <h1>同学列表</h1>
    <div class="tool-bar">
      <button class="add-btn" type="primary" @click="showFlag = true">新增</button>
    </div>
    <ul>
      <li>
        <span class="No">序号</span>
        <span class="study-code">学号</span>
        <span class="name">姓名</span>
        <span class="year">年龄</span>
        <div class="operation">操作</div>
        <!-- <button @click="deleteUser(index)">删除</button>
        <button @click="editUser(index)">编辑</button>
        <button @click="getYourName(item.id)">问名字</button> -->
      </li>
      <li v-for="(item, index) in list" :key="item.id">
        <span class="No">{{ index + 1 }}.</span>
        <span class="study-code">{{ item.id }}</span>
        <span class="name">{{ item.userName }}</span>
        <span class="year">{{ item.age }}</span>
        <div class="operation">
          <button @click="deleteUser(index)">删除</button>
          <button @click="editUser(index)">编辑</button>
          <button @click="getYourName(item.id)">问名字</button>
        </div>
      </li>
    </ul>

    <div class="pop-blank" v-if="showFlag">
      <h2>{{isEdit ? '编辑同学' : '新增同学'}}</h2>
      <div class="blank-body">
        <div class="blank-item">
          <span>学号</span>
          <input type="text" v-model="studyNum">
        </div>
        <div class="blank-item">
          <span>姓名</span>
          <input type="text" v-model="name">
        </div>
        <div class="blank-item">
          <span>年龄</span>
          <input type="text" v-model="year">
        </div>
      </div>
      <div class="footer">
        <button type="primary" @click="showFlag = false">取消</button>
        <button type="primary" @click="submitFn">确定</button>
      </div>
    </div>
  </div>
</template>

<script setup>
import { reactive, ref } from 'vue';

let showFlag = ref(false);
let isEdit = ref(false);
let curIdx = ref(0);

let studyNum = ref(0);
let name = ref('');
let year = ref(0);
let list = reactive([
  {
    id: 220812022,
    userName: '刘淑文',
    age: 18
  },
  {
    id: 220812008,
    userName: '蔡欣怡',
    age: 18
  },
  {
    id: 220812030,
    userName: '龙依',
    age: 18
  }
]);

const deleteUser = index => {
  list.splice(index, 1);
};

const editUser = index => {
  isEdit.value = true;
  curIdx.value = index;
  const item = list[index];
  // item.age = 22;
  // todo: 拿到的item信息填入弹窗对应的输入框里
  studyNum.value = item.id;
  name.value = item.userName;
  year.value = item.age;
  showFlag.value = true;
};

const submitFn = () => {
  if (isEdit.value) { // 编辑
    list.splice()
    list[curIdx.value] = {
      id: studyNum.value,
      userName: name.value,
      age: year.value
    }
  } else { // 新增
    list = [{
      id: studyNum.value,
      userName: name.value,
      age: year.value
    }, ...list];
  }
  showFlag.value = false;
  // alert(`新增的同学学号是：${studyNum.value};姓名是：${name.value};年龄是：${year.value}`);
}

const getYourName = id => {
  const student = list.find(item => item.id === id);
  alert(student.userName);
};
</script>

<style lang="less" scoped>
.list-comp {
  text-align: left;
}
h1 {
  text-align: center;
}
.tool-bar {
  display: flex;
  justify-content: flex-end;
  .add-btn {
    background-color: rgba(42, 46, 54, 0.48);
    color: #ffffff;
    width: 90px;
    margin-right: 24px;
  }
}
ul {
  padding-left: 0;
  padding: 0 24px;
  text-align: center;
}
.pop-blank {
  position: absolute;
  background-color: #ffffff;
  border-radius: 8px;
  left: 50%;
  top: 50%;
  width: 50%;
  height: 50vh;
  transform: translate(-50%, -50%);
  padding: 24px;
  border: 1px solid rgba(0, 0, 0, 0.4);
    display: flex;
    flex-direction: column;
  h2 {
    text-align: center;
  }
  .blank-body {
    flex-grow: 1;
    flex-shrink: 1;
    display: flex;
    flex-direction: column;
    justify-content: center;
    .blank-item {
      height: 72px;
      font-size: 24px;
      display: flex;
      span {
        margin-right: 12px;
        width: 60px;
      }
      input {
        height: 36px;
        flex-grow: 1;
        flex-shrink: 1;
        font-size: 16px;
        // width: 100%;
      }
    }
  }
  .footer {
    // position: absolute;
    display: flex;
    justify-content: flex-end;
    width: 100%;
    button {
      background-color: #1677FF;
      color: #ffffff;
    }
    & > button:nth-child(1) {
      margin-right: 12px;
      background-color: #ffffff;
      border: 1px solid #1677FF;
      color: #1677FF;
    }
  }
}
li {
  list-style: none;
  display: flex;
  justify-content: flex-start;
  align-items: center;
  // margin-bottom: 24px;
  height: 64px;
  border-bottom: 1px solid rgba(0, 0, 0, 0.4);
  &:nth-child(1) {
    color: aliceblue;
    background-color: rgba(42, 46, 54, 0.48);
  }
  .No {
    width: 18%;
  }
  .study-code {
    width: 18%;
  }
  .name {
    width: 18%;
  }
  .year {
    width: 18%;
  }
  .operation {
    flex-grow: 1;
    display: flex;
    justify-content: space-around;
    & > button {
      background-color: #314659;
      color: #ffffff;
      width: 90px;
    }
  }
}
</style>
