<template>
    <div class="todoBox" id="todoBox">
        <p class="title">Lac's TODO:</p>
        <input type="text" v-model="item" @keyup.enter="addItem">
        <button @click="addItem" class="addBtn">submit</button>
        <!--<div class="text-item">{{item}}</div>-->
        <button class="delAll" @click="delAll">delAll</button>
        <hr>
        <div class="todoList">
            <span class="title">List:</span>
            <p class="tip" v-show="!itemArr.length">啥都木有~</p>
            <ul>
                <li v-for="(k,index) in itemArr" class="itemContent" :class="{finished:k.did}"><span>{{k.item}}</span>
                    <button v-show="!itemArr.length==0" class="listBtn" @click="doIt(k)">{{k.did?'todo':'done'}}</button>
                    <button v-show="!itemArr.length==0" @click="delIt(index)">del</button>
                </li>
            </ul>
        </div>
    </div>
</template>

<script>
    export default {
        name: 'todoBox',
        data() {
            return {
                item: '',
                itemArr: []
            }
        },
        methods: {
            addItem() {
                // console.log(this.item);
                this.itemArr.push({
                    item: this.item,
                    did: false
                });
                this.item = '';
            },
            doIt(item) {
                item.did = !item.did;
            },
            delIt(index) {
                this.itemArr.splice(index, 1);
            },
            delAll() {
                this.itemArr = null;
            }
        }
    }
</script>

<style>
    * {
        margin: 0;
        padding: 0;
        list-style: none;
    }

    p.title {
        font-size: 20px;
    }

    .text-item {
        margin-bottom: 20px;
    }

    hr {
        margin-top: 30px;
    }

    .todoList {
        margin-top: 20px;
    }

    .itemContent {
        color: red;
        margin: 10px;
    }

    .listBtn {
        margin-left: 50px;
    }

    .finished {
        text-decoration: line-through;
    }

    .delAll {
        display: block;
        margin-top: 20px;
        color: red;
    }
    .tip{
        color: deepskyblue;
    }
</style>