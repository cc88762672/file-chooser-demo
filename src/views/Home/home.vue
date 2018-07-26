<template>
 <div class="home">
  <x-header title="文件选择Demo" :left-options="{showBack:false}" ></x-header>
  <view-box ref="viewBox" body-padding-bottom="0px">
   <div class="one-line pad10">
      <div class="w50">
       <input type="file" ref="picFile" accept="image/*" capture="camera" alt="" class="file-input"  @change="chooseFile('pic')"/>
       <div class="big-label">只选图片</div>
      </div>
      <div class="w50 with-left">
       <input type="file" ref="allFile" accept="*" capture="camera" alt="" class="file-input" @change="chooseFile('all')"/>
       <div class="big-label">所有文件</div>
      </div>
   </div>
   <div class="common-list top10">
    <div class="common-item" v-for="(item,index) in fileList" :key="index">
      <img src="../../assets/images/home/no.png" class="delete-icon" @click="deleteFile(index)"/>
      <div class="one-line small-font on-left pad5">
        <div class="inner-text with-min-width">文件名称:</div>
        <div class="inner-text be-break">{{item.name}}</div>
      </div>
      <div class="one-line small-font on-left pad5">
        <div class="inner-text with-min-width">文件类型:</div>
        <div class="inner-text be-break">{{item.type}}</div>
      </div>
      <div class="one-line small-font on-left pad5">
         <div class="inner-text with-min-width">文件大小:</div>
         <div class="inner-text be-break">{{item.size}}</div>
      </div>
    </div> 
   </div>
  </view-box>
 </div>
</template>
<script>
import { ViewBox, XHeader } from "vux";
import portraitA from "../../assets/images/home/a.jpeg";
import portraitB from "../../assets/images/home/b.jpeg";
import portraitC from "../../assets/images/home/c.jpeg";
export default {
  data() {
    return {
      fileList: []
    };
  },
  methods: {
    chooseFile(key) {
      let vm = this;
      let mb = 1024 * 1024;
      let size = 0; //文件大小，以MB为单位
      let currentFile = "";
      if (key == "pic") {
        currentFile = vm.$refs.picFile.files[0];
      } else if (key == "all") {
        currentFile = vm.$refs.allFile.files[0];
      }
      size = currentFile.size / mb;
      size = Number(size.toFixed(2));
      size = size + "MB";
      let temp = {
        name: currentFile.name,
        size: size,
        type: currentFile.type
      };
      vm.fileList.push(temp);
      console.log("文件格式:" + currentFile.type);
      console.log("文件大小:" + size);
    },
    deleteFile(index) {
      let vm = this;
      vm.fileList.splice(index, 1);
    }
  },
  components: {
    ViewBox,
    XHeader
  },
  beforeRouteEnter(to, from, next) {
    next(vm => {
      vm.fileList = [];
    });
  }
};
</script>
<style scoped>
select:focus {
  outline: 0;
}
button:focus {
  outline: 0;
}
textarea:focus {
  outline: 0;
}
.home {
  height: 100%;
}
.title {
  width: 100%;
  color: #1b1b1b;
  text-align: center;
  font-size: 1rem;
  margin-top: 10px;
}
.one-line {
  width: 100%;
  overflow: hidden;
  display: flex;
}
.pad10 {
  padding: 10px;
}
.file-input {
  width: 100%;
  height: 90px;
  position: absolute;
  top: 0;
  left: 0;
  z-index: 100;
  opacity: 0;
}
.w50 {
  width: 49%;
  height: 90px;
  position: relative;
  float: left;
  display: flex;
  justify-content: center;
  align-items: center;
  border: 2px dashed #d2d2d2;
  border-radius: 5px;
}
.with-left {
  margin-left: 2%;
}
.big-label {
  font-size: 1.2rem;
  color: #000000;
}
.small-font {
  font-size: 0.875rem;
  color: #000000;
}
.common-list {
  width: 100%;
  background-color: transparent;
  overflow: hidden;
}
.common-item {
  width: 94%;
  margin-left: 3%;
  margin-bottom: 10px;
  background-color: #ffffff;
  position: relative;
  overflow: hidden;
  padding: 10px;
  border: 2px dashed #ccc;
  transition: opacity ease-in 0.2s;
  border-radius: 5px;
}
.common-item:last-child {
  margin-bottom: 0;
}
.common-item:active {
  opacity: 0.4;
}
.be-break {
  word-break: break-all;
}
.top10 {
  margin-top: 10px;
}
.delete-icon {
  width: 40px;
  height: 40px;
  padding: 10px;
  position: absolute;
  top: 0;
  right: 0;
  transition: transform ease-in 0.1s;
  z-index: 100;
}
.delete-icon:active {
  transform: scale(0.95, 0.95);
}
.on-left {
  text-align: left;
}
.one-line {
  width: 100%;
  overflow: hidden;
  display: flex;
}
.pad5 {
  padding: 5px;
  padding-left: 10px;
  padding-right: 20px;
}
.inner-text {
  font-size: 0.875rem;
  color: #000000;
  float: left;
}
.with-min-width {
  min-width: 70px;
}
</style>
