<template>
    <div id="app">
        <div class="nav">
            id:<input type="text" v-model="id">
            name:<input type="text" v-model="name" @keyup.enter="add()">
            <input type="button" value="添加" @click="add()" class="button">
            <input type="button" class="search" value="搜索">
            <input type="text" v-model="keywords" value="关键字" v-focus v-color="'red'">
        </div>
        <input type="reset" class="reset" @click="reset">
        <div class="container">
            <table>
                <tr>
                    <th>id</th>
                    <th>name</th>
                    <th>time</th>
                    <th>operate</th>
                </tr>
                <!--通过关键字查找对象数组的方法-->
                <tr v-for="item in search(keywords)" :key="item.id">
                    <td>{{item.id}}</td>
                    <td>{{item.name}}</td>
                    <td>{{item.time | timeFormat }}</td>
                    <td>
                        <a href="" @click.prevent="del(item.id)">删除</a>
                    </td>
                </tr>
            </table>
        </div>
    </div>
</template>

<script>
export default {
    name: 'Form',
    data(){
        return {
            id:'',
            name:'',
            keywords:'',
            list:[
                {id:1,name:'宝马',time:new Date()},
                {id:2,name:'奔驰',time:new Date()},
                {id:3,name:'法拉利',time:new Date()}
            ]
        }
    },
    filters:{
        timeFormat:function (time) {
            var dt = new  Date(time);
            var year = dt.getFullYear();
            var month =(dt.getMonth()+1);
            var day = dt.getDay();
            if (month <10) {
                month = '0'+month;
            }
            if (day<10){
                day = '0'+day;
            }
            return year+'-'+month+'-'+day;
        }
    },
    methods:{
        add(){
            var car = {id:this.id,name:this.name,time:new Date()};
            this.list.push(car);
            this.id = '';
            this.name = '';
        },
        del(id){
            //findIndex的用法是查找指定的id在哪一个索引里产生，然后返回这个索引值
            // var index = this.list.findIndex(item => {
            //     if (item.id == id) {
            //         return true;
            //     }
            // });
            //console.log(index)
            //this.list.splice(index,1);

            //this.list.forEach((item,index) => {
            //    if (item.id == id) {
            //        this.list.splice(index,1);
            //    }
            //})

            this.list.filter((item,i) => {
                if (item.id == id) {
                    this.list.splice(i,1)
                }
            })
        },
        search(keywords){
            var newlist = [];
            this.list.forEach(item =>{
                if (item.name.indexOf(keywords) != -1) {
                    // console.log(keywords);
                    newlist.push(item);
                }
            });
            //在这里includes()方法并不存在呢，但是这确实是一个方法
            // newlist = this.list.filter(item => {
            //    if (this.item.includes(keywords)) {
            //        return item;
            //    }
            // });
            return newlist;
        },
        reset() {
            var newList = [
                {id: 1, name: '宝马', time: new Date()},
                {id: 2, name: '奔驰', time: new Date()},
                {id: 3, name: '法拉利', time: new Date()}
            ];
            if (this.list.length != 3) {
                this.list = newList;
                //alert(this.list.length)
            }
            if (this.keywords.length != 0) {
                //这里是当keywords的长度不为0的时候首先将Keywords清空同时给list添加一个新的newList
                this.keywords = '';
                this.list = newList;
            }
        }
    }
}
</script>

<style>
    * {
        padding: 0;
        margin: 0;
        font-family: sans-serif;
        font-size: 18px;
    }
    #app {
        margin: 50px auto;
        width: 500px;
        height: 500px;
        background-color: #a29bfe;
        padding-top: 5px;
        position: relative;
        cursor: pointer;
    }
    #app .container {
        width: 400px;
        margin: 10px auto;
    }
    #app .container table {
        width: 398px;
        border: 1px solid yellow;
        border-collapse: collapse;
    }
    #app .container tr,#app .container table th {
        border: 1px solid yellow;
        border-collapse: collapse;
        padding: 10px;
        width: 25%;
    }
    #app .container td {
        border: 1px solid yellow;
        border-collapse: collapse;
        padding: 10px;
        text-align: center;
    }
    .nav {
        text-align: center;
        width: 500px;
        /* background-color: yellow;*/
    }
    input {
        width: 80px;
        text-align: center;
        padding: 1px;
    }
    input:link {
        -webkit-box-shadow: 0 0 2px darkseagreen;
    }
    .search {
        width: 50px;
        padding: 1px;
    }
    .reset {
        width: 40px;
        font-size: 14px;
        padding: 1px;
        position: absolute;
        top: 50px;
        left: 5px;
    }
    .reset:hover,.button:hover,.search {
        background-color: aquamarine;
    }
</style>