<template>
  <div class="=container">
          <div class="nav">
    <div class="main">
    </div>
    <div class="right">
      <el-button @click="signout" >SIGN OUT</el-button>
    </div>
  </div>
  
  <div class="container shifted">

    <h1 class="h1">
      FILE BANK
    </h1>
      
    <el-button>
      <label for="file">
        Upload
        <input type="file" @change="upload" id="file" style="display:none;">
      </label>
    </el-button>
    <el-button @click="refresh" class="el-icon-refresh-left"></el-button>
    <el-table 
      :data="s3Data"
      style="width: 100%">
      <el-table-column
        prop="key"
        label="Key"
        sortable>
      </el-table-column>
      <el-table-column
        prop='lastModified'
        label="LastModified"
        sortable>
      </el-table-column>
      <el-table-column
        prop="size"
        label="Size"
        sortable>
      </el-table-column>
      <el-table-column>
        <template slot-scope="scope">
          <el-button
            @click="download(scope.row)">Download</el-button>
          <el-button type="danger" @click="openDeleteDialog(scope.row)">Delete</el-button>
        </template>
      </el-table-column>    
    </el-table>
    <el-dialog
      title="Delete objects"
      :visible.sync="dialogVisible"
      width="30%"
      :before-close="handleClose">
      <span>{{ deleteObject }} Objects will be deleted</span>
      <span slot="footer" class="dialog-footer">
        <el-button @click="dialogVisible = false">Cancel</el-button>
        <el-button type="primary" @click="deleteOK()">Confirm</el-button>
      </span>
    </el-dialog>
  </div>
  </div>
</template>

<script>
import Vue from 'vue'
import { Auth, Storage } from 'aws-amplify';
import ElementUI from 'element-ui'
import 'element-ui/lib/theme-chalk/index.css'
import locale from 'element-ui/lib/locale/lang/en'

Vue.use(ElementUI, { locale })

export default {
  name: 'Home',
  data () {
    return {
      s3Data: [],
      dialogVisible: false,
      selectedRow: "",
      deleteObject: "",
      uploadFile: ""
    }
  },
  created () {
    this.refresh()  
  },
  methods: {
    refresh () {
      Storage.list('', { level: 'private' })
        .then(result => this.s3Data = JSON.parse(JSON.stringify(result)))
        .catch(err => console.log(err));
    },
    upload(e) {
      var files = e.target.files || e.dataTransfer.files;
      console.log(files)
      Storage.put(files[0].name, files[0], {level: "private"})
        .then(result => {
          console.log(result)
          this.refresh() 
          })
        .catch(err => console.log(err));
    },
    download (row) {
      Storage.get(row['key'], { level: "private", download: true })
        .then(result => {
          console.log(result)
          const url = URL.createObjectURL(new Blob([result.Body]));
          const link = document.createElement('a')
          link.href = url
          link.download = row['key']
          console.log(link)
          link.click()
        })
        .catch(err => console.log(err));
    },
    openDeleteDialog(row) {
      this.selectedRow = row;
      console.log(row)
      this.deleteObject = row['key'];
      this.dialogVisible = true
    },
    deleteOK () {
      this.dialogVisible = false
      Storage.remove(this.selectedRow['key'])
        .then(result => {
          console.log(result)
          this.refresh() 
          }
        )
        .catch(err => console.log(err));
    },      
    handleClose(done) {
        this.$confirm('Are you sure to close this dialog?')
          .then(done())
          .catch();
    },
    signout: async function() {
      try {
        await Auth.signOut();
    } catch (error) {
        console.log('error signing out: ', error);
    }
    },
  }
}

</script>

<style>
label {
  color: #606266;  
  background-color:white;
  padding: 10px;
}
</style>