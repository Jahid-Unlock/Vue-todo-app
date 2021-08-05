<template>
  <div class="main-wrapper">
    <div class="form-wrap">
      <input type="text" v-model="newItem" @keyup.enter="itemAdded" placeholder="Add Items"/>
      <button @click="itemAdded">Add Item</button>
    </div>

    <ul v-if="items.length !== 0">
        <li v-for="item in items" :key="item.id" class="single-item">
            <span @click="taskDone(item)" :class="{taskdone : item.taskdone} ">{{item.title}}</span> <button class="remove-btn" @click="removeItem(item)">delete</button>
        </li>
    </ul>
    <h3 v-if="items.length === 0">Congratulations! Your todo's are done!</h3>

    <div class="functionalities">
        <h3>Functionalities</h3>
        <ol>
            <li>You can add items either clicking <strong>Add items</strong> button or pressing <strong>Enter Key.</strong></li>
            <li>You can add any kind of data except empty string.</li>
            <li>You can delete delete item by clicking <strong>delete button.</strong></li>
            <li>You can mark done any item by clicking item itself.</li>
        </ol>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      newItem : '',
      items: [
        { id: 1, title: "Mouse", taskdone : false},
        { id: 2, title: "Keybord", taskdone : false },
        { id: 3, title: "Power Supply", taskdone : false },
      ],
    };
  },
  methods: {
      itemAdded(){

          if(this.newItem === ''){
              alert('input is empty')
          } else{
              this.items.push(
              {
                  id : this.items.length +1,
                  title : this.newItem
              }
          )
          this.newItem = ''
          }
          
      },
      removeItem(data){
          this.items = this.items.filter(item => item !== data)
      },

      taskDone(data){
          this.items.map(cv => cv === data ? (cv.taskdone === false ? cv.taskdone = true : cv.taskdone = false) : null)
      }
  },
};
</script>

<style scoped>

.main-wrapper{
    max-width: 600px;
    margin: 0 auto;
}
.form-wrap {
  display: flex;
  justify-content: center;
}
.form-wrap input {
  height: 45px;
  width: 400px;
  border-radius: 6px;
  padding: 0 20px;
  border: 2px solid chartreuse;
  font-size: 18px;
}
.form-wrap input:focus{
    border: 2px solid rgb(106, 211, 1);
    outline: none;
}
.form-wrap button {
  background: chartreuse;
  font-weight: 500;
  padding: 12px 30px;
  font-size: 16px;
  border: none;
  border-radius: 6px;
  margin-left: 10px;
  cursor: pointer;
}
.functionalities{
    margin-top: 40px;
}
.functionalities ol li{
    text-align: start;
    margin-bottom: 10px;
}
ul{
    max-width: 500px;
    margin: 0 auto;
    margin-top: 60px;
    list-style: none;
    padding: 30px;
    border: 1px solid chartreuse;
    border-radius: 10px;
    box-shadow: rgba(0, 0, 0, 0.1) 0px 1px 2px 0px;
}

ul li{
    text-align: start;
    padding: 8px 20px;
    box-shadow: rgba(0, 0, 0, 0.05) 0px 6px 24px 0px, rgba(0, 0, 0, 0.08) 0px 0px 0px 1px;
    margin-top: 12px;
    display: flex;
    justify-content: space-between;
    align-items: center;
}

ul li span{
    font-size: 16px;
    font-weight: 600;
    color: darkblue;
}
ul li:first-child{
    margin-top: 0;
}

button.remove-btn{
    border: none;
    background: #eee;
    padding: 6px 10px;
    border-radius: 5px;
    cursor: pointer;
}
.taskdone{
    text-decoration: line-through;
    color: #ddd;
}
</style>