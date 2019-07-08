<template>
    <div>
        <ul>
            <li v-for="todoItem in todoItems" v-bind:key="todoItem">
            <!-- <li v-for="todoItem in todoItems" v-bind:key="todoItems"> -->
                {{todoItem}}
            </li>
            <li></li>
            <li></li>
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
    created: function(){
        // console.log("Created");
        if(localStorage.length > 0){
            for(var i=0;i<localStorage.length;i++){
                if(localStorage.key(i) !=="loglevel:webpack-dev-server"){
                this.todoItems.push(localStorage.key(i));
                }
            }
        }

    }

}
</script>

<style>

</style>
