<template>
    <div>
        <ul>
            <li v-for="(todoItem, index) in todoItems" v-bind:key="todoItem.item" class="shadow">
            <!-- <li v-for="todoItem in todoItems" v-bind:key="todoItems"> -->
                <i class="fas fa-check" v-bind:class="{checkBtnCompleted:todoItem.completed}"
                 v-on:click="toggleComplete(todoItem, index)"></i>
                <span v-bind:class="{textCompleted:todoItem.completed}">
                    {{ todoItem.item }}
                </span>
                <span class="removeBtn" v-on:click="removeTodo(todoItem, index)">
                    <i class="fas fa-trash"></i>
                </span>
            </li>
        </ul>

    </div>
</template>

<script>
export default {
    data: function(){
        return {
            todoItems: []
        }
    },
    // 인스턴스가 생성되자마자 호출됨
    created: function callwhencreated(){
        // console.log("Created");
        if(localStorage.length > 0){
            for(var i=0;i<localStorage.length;i++){
                if(localStorage.key(i) !=="loglevel:webpack-dev-server"){
                this.todoItems.push(JSON.parse(localStorage.getItem(localStorage.key(i))));
                // this.todoItems.push(localStorage.key(i));
                }
            }
        }
    },
    methods: {
        removeTodo: function(todoItem, index){
            //console.log(todoItem + " " +  index);
            localStorage.removeItem(todoItem.item);
            this.todoItems.splice(index, 1);
        },
        toggleComplete: function(todoItem, index){
            todoItem.completed = !todoItem.completed;
            // console.log(todoItem, index);
            localStorage.removeItem(todoItem.item);
            localStorage.setItem(todoItem.item, JSON.stringify(todoItem));

        }
    }

}
</script>

<style scoped>
ul{
    list-style-type: none;
    padding-left: 0px;
    margin-top: 0;
    text-align: left;
}
li{
    display:flex;
    min-height: 50px;
    height: 50px;
    line-height: 0.5rem 0;
    margin: 0 0.9rem;
    padding: 0 0.9rem;
    background: white;
    border-radius: 5px;
}
.checkBtn{
    line-height: 45px;
    color: #62acd6;
    margin-right: 5px;
}
.checkBtnCompleted{
    color: #b3adad;

}
.textCompleted{
    text-decoration: line-through;
    color: #b3adad;
}
.removeBtn{
    margin-left: auto;
    color: #de4343;
}
</style>
