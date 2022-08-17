<script setup>
  import { reactive, ref } from 'vue'
  import { ElMessageBox } from 'element-plus'

  const tableData = reactive([
    { name: "daniel01", link: "http://www.google.com" ,comment: "handsome boy01" },
    { name: "daniel02", link: "http://www.google.com" ,comment: "handsome boy02" },
    { name: "daniel03", link: "http://www.google.com" ,comment: "handsome boy03" },
    { name: "daniel04", link: "http://www.google.com" ,comment: "handsome boy04" },
    { name: "daniel05", link: "http://www.google.com" ,comment: "handsome boy05" },
    { name: "daniel06", link: "http://www.google.com" ,comment: "handsome boy06" },
    { name: "daniel07", link: "http://www.google.com" ,comment: "handsome boy07" },
    { name: "daniel08", link: "http://www.google.com" ,comment: "handsome boy08" },
    { name: "daniel09", link: "http://www.google.com" ,comment: "handsome boy09" },
    { name: "daniel10", link: "http://www.google.com" ,comment: "handsome boy10" },
  ])
  const form = reactive({
    index:"",
    name:"",
    comment:""
  })

  const dialogVisible = ref(null)

  function handleEdit(index){
    dialogVisible.value = true
    form.index = index
    form.name = tableData[index].name
    form.comment = tableData[index].comment
  }

  function handleDelete(index){
    const message = "Do you want Delete?"
    ElMessageBox.confirm(message)
      .then(()=>tableData.splice(index,1))
      .catch(()=>{})    
    
  }

  function handleSubmit(){
    const { index, name, comment } = form
    const data = { name, comment }
    const message = "Do you want to submit?"

    ElMessageBox.confirm(message)
      .then(()=>{
        tableData.splice(index , 1 , data)
        dialogVisible.value = false
      }).catch(()=>{})
    
  }
</script>
<template>
  <div class="color-[#fff] w-[900px] mx-[auto]">
    <div class="w-[443px] h-[199px] mx-[auto]">
      <img src="./assets/notarmory_logo.gif" class="w-[100%]"  alt="median xl">
    </div>
    <h3>Aahz Snapshot List</h3>
    <el-table :data="tableData" class="w-[800px]" stripe>
      <el-table-column label="Name">
        <template #default="{ row }">
          <a class="no-underline" :href="row.link" target="_blank" >{{row.name}}</a>
        </template>

      </el-table-column>
      <el-table-column prop="comment" label="Description"/>
      <el-table-column label="action">
        <template #default="{ $index }">
          <el-button type="info" @click="handleEdit($index)">Edit</el-button>
          <el-button type="info" @click="handleDelete($index)">Delete</el-button>
        </template>
      </el-table-column>
    </el-table>


    <el-dialog v-model="dialogVisible" title="Edit Snapshot"  width="600px">
      <el-form :model="form" label-width="100px">
        <el-form-item label="name">
          <el-input v-model="form.name"/>
        </el-form-item>
        <el-form-item label="description">
          <el-input v-model="form.comment" type="textarea" :rows="5" maxlength="200" show-word-limit />
        </el-form-item>        
        <el-form-item>
          <el-button class="ml-[auto]" type="danger" @click="dialogVisible = false" >cancel</el-button>
          <el-button class="ml-[auto]" type="primary" @click="handleSubmit" >submit</el-button>
        </el-form-item>
      </el-form>      
    </el-dialog>
  </div>
</template>