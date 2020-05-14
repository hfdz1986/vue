<template>
  <div>
    
    <table v-if='list.length > 0'>
        <thead>
           <tr>
             <td>序号</td>
             <td>商品名称</td>
             <td>商品单价</td>
             <td>商品数量</td>
             <td>操作</td>
           </tr>
        </thead>
        <tbody>
          <tr 
            v-for='(item,index) in list'
          >
            <td>
              {{item.id}}
            </td>
            <td>
              {{item.name}}
            </td>
            <td>
              {{item.price}}
            </td>
            <td>
              
              <button 
                @click='reduce(index)' 
                :disabled='item.count===1'
              >-</button>

              {{item.count}}

              <button @click='add(index)'>+</button>

            </td>
            <td>
              <button @click='remove(index)'>删除</button>
            </td>
          </tr>
        </tbody>
        <h1>总价：{{totalPrice}}</h1>
    </table>
    <div v-else>暂无数据...</div>
  </div>
</template>

<script>
export default{
  data () {
    return {
      list:[
        {
          id:0,
          name:"足球",
          price:200,
          count:1
        },
        {
          id:1,
          name:"上衣",
          price:109,
          count:1
        },
        {
          id:2,
          name:"鞋",
          price:1500,
          count:1
        },
        {
          id:3,
          name:"充电宝",
          price:70,
          count:1
        }
      ]
    }
  },
  methods:{
    add(index){
      this.list[index].count++;
    },
    reduce(index){
       if(this.list[index].count === 1) return;
       this.list[index].count--;
    },
    remove(index){
      this.list.splice(index,1)
    }
  },
  computed:{
     totalPrice(){
       let total = 0;
       for(let i=0;i<this.list.length;i++){
        total+= this.list[i].price*this.list[i].count;
       }
       return total;
     }
  }
}
</script>

<style>
table{
  border:1px solid #f5f5f5;
  border-spacing: 0;
  border-collapse: collapse;
}
tr,td{
  padding:15px;
  border:1px solid #e9e9e9;
}
</style>