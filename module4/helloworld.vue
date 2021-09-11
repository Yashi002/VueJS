<template><div>
   <h1>Indexed Db</h1>
  <!-- <button @click="createDb">Create db</button> -->
  <!-- <button @click="addData">add data</button> -->
  <button @click="retriveData">read all</button>
  <!-- <button @click="read">read</button> -->
  <!-- <button @click="remove">remove</button> -->
  <!-- <h1>{{productData}}</h1> -->
  <h1>{{aryofObjects}}</h1>

  </div>
</template>

<script>
import axios from 'axios';
export default {
   name:'indexedDb',
   data(){
      return{
         db:"",
         request:"",
         productData:"",
         aryofObjects:[]
      }
   },
   created(){
       window.IDBTransaction = window.IDBTransaction || 
         window.webkitIDBTransaction || window.msIDBTransaction;
         window.IDBKeyRange = window.IDBKeyRange || window.webkitIDBKeyRange || 
         window.msIDBKeyRange
         if(!window.indexedDB){
            window.alert("Your browser does not support a indexed Db");
         }
         // const employeeData = [ 
         //    { id: "00-01", name: "shashank", age: 23, email: "shashank@gmail.com" },
         //    { id: "00-02", name: "utkarsh;", age: 32, email: "utk@gamil.com.com" }
         // ];
          var url = "https://fakestoreapi.com/products/category/"+"jewelery" ;
          axios.get(url)
          .then((resp)=>{
              this.request = window.indexedDB.open("myDb",1);
         this.request.onerror = function(){
            console.log("error");
         }
         // this.request.onsuccess = function(){
         //     this.db= this.request.result;
           
         //    // console.log("success: " +this.db);
         // }
         this.request.onupgradeneeded = function (event) {
             var db1= event.target.result;
            var objectStore = db1.createObjectStore("Products",{keyPath: "id"});
             
            this.productData=resp.data; 
            console.log(this.productData);   
             for(var i in this.productData){
               objectStore.add(this.productData[i]);
            }
         }
         console.log("data stored sucessfully");
        console.log("created sucessfully")
         console.log(this.db);
        })
        
        
           
   },
   methods:{
      retriveData(){
          window.IDBTransaction = window.IDBTransaction || 
         window.webkitIDBTransaction || window.msIDBTransaction;
         
 window.IDBKeyRange = window.IDBKeyRange || window.webkitIDBKeyRange || 
         window.msIDBKeyRange
         this.db = this.request.result;
         // var transcation = this.db.tansaction("employee");
         // var objectStore = this.db.tansaction("employee").objectStore("employee");
         this.request = this.db.transaction(["Products"],"readwrite")
         .objectStore("Products").openCursor();
         this.request.onsuccess = function(event){
            console.log(event);
            var cursor = event.target.result;
            if(cursor){
               alert("Name for id " + cursor.key + "is" + cursor.value.title+ "Age:" + cursor.value.category + "description :" + cursor.value.description) + "image : "+ cursor.value.image + "price :"+cursor.value.price;
               cursor.continue();
            }
         }
         
         alert("Read All Method")
      },      
   }
   
}
</script>

<style>
</style>