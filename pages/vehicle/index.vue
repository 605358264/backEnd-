<


<template>
  <a-layout id="components-layout-demo-custom-trigger">
    <a-layout-sider :trigger="null" collapsible v-model="collapsed">
      <div class="logo" />
      <a-menu   theme="dark" mode="inline"  @click="handleClick" >
        <a-menu-item key="1">
          <a-icon type="user" />
          <span>重点车辆</span>
        </a-menu-item>
        <a-menu-item key="2">
          <a-icon type="video-camera" />
          <span>重点人员</span>
        </a-menu-item>
        <a-menu-item key="3">
          <a-icon type="upload" />
          <span>一车一档</span>
        </a-menu-item>
        <a-menu-item key="4">
          <a-icon type="upload" />
          <span>辑查布控</span>
        </a-menu-item>
        <a-menu-item key="5">
          <a-icon type="upload" />
          <span>地点管理</span>
        </a-menu-item>
        <a-menu-item key="6">
          <a-icon type="upload" />
          <span>设备管理</span>
        </a-menu-item>
        <a-menu-item key="7">
          <a-icon type="upload" />
          <span>权限管理</span>
        </a-menu-item>
        <a-menu-item key="8">
          <a-icon type="upload" />
          <span>字典管理</span>
        </a-menu-item>
        <a-menu-item key="9">
          <a-icon type="upload" />
          <span>用户管理</span>
        </a-menu-item>
        <a-menu-item key="10">
          <a-icon type="upload" />
          <span>操作日志</span>
        </a-menu-item>
      </a-menu>
    </a-layout-sider>
    <a-layout>
      <a-layout-header style="background: #fff; padding: 0">
        <a-icon
          class="trigger"
          :type="collapsed ? 'menu-unfold' : 'menu-fold'"
          @click="() => (collapsed = !collapsed)"
        />
      </a-layout-header>
      <a-layout-content
        :style="{ margin: '24px 16px', padding: '24px', background: '#fff', minHeight: '280px' }"
      >
      <a-row class="row"> 
        <span class="carType"> 车辆类型：</span>
        <a-select defaultValue="lucy" style="width: 120px" @change="handleChange">
              <a-select-option value="jack">Jack</a-select-option>
              <a-select-option value="lucy">Lucy</a-select-option>
              <a-select-option value="disabled" disabled>Disabled</a-select-option>
              <a-select-option value="Yiminghe">yiminghe</a-select-option>
        </a-select>
          <span class="carType"> 布控状态：</span>
        <a-select defaultValue="lucy" style="width: 120px" @change="handleChange">
              <a-select-option value="jack">Jack</a-select-option>
              <a-select-option value="lucy">Lucy</a-select-option>
              <a-select-option value="disabled" disabled>Disabled</a-select-option>
              <a-select-option value="Yiminghe">yiminghe</a-select-option>
        </a-select> 
         <span class="carType"> 车辆分类：</span>
        <a-select defaultValue="lucy" style="width: 120px" @change="handleChange">
              <a-select-option value="jack">Jack</a-select-option>
              <a-select-option value="lucy">Lucy</a-select-option>
              <a-select-option value="disabled" disabled>Disabled</a-select-option>
              <a-select-option value="Yiminghe">yiminghe</a-select-option>
        </a-select>   
        <a-button type="primary" icon="search" class="search">查询</a-button> 
      </a-row>
      <a-row class="row">
        <a-button type="primary" icon="add" class="add" style="margin-left:10px" @click="add(type)">新增类型</a-button>
        <a-button type="primary" icon="edit" class="edit" style="margin-left:10px" @click="edit(type)">修改类型</a-button>
        <a-button type="primary" icon="delete" class="delete" style="margin-left:10px" @click="showModal">删除信息</a-button>
        <a-button type="primary" icon="car" class="car" style="margin-left:10px" @click="car">车型布控</a-button>
      </a-row> 
      <a-table :columns="columns" :dataSource="datas" class="action-table"  
       :rowSelection="{selectedRowKeys: selectedRowKeys, onChange:onSelectChange,type:'radio'}"
         rowKey='id' 
      >
        <a slot="name" slot-scope="text">{{ text }}</a>
      </a-table>
      <a-row>
        <div class="pagenation">
          <span> 共8条</span>  
            <div id="components-pagination-demo-mini">
              <a-pagination size="small" :total="8" />
            </div>
        </div> 
      </a-row> 
      <!--增加修改弹框-->
      <div class="addDialog" v-show="addShow">
        <span class="title">{{types}}</span>
        <span class="icon" @click=shutAdd>x</span>  
        <div class="addContent">
          <a-row>
            <span class="carType"> 车辆类型：</span>
              <a-select defaultValue="lucy" style="width: 320px" @change="handleChange">
                <a-select-option value="jack">Jack</a-select-option>
                <a-select-option value="lucy">Lucy</a-select-option>
                <a-select-option value="disabled" disabled>Disabled</a-select-option>
                <a-select-option value="Yiminghe">yiminghe</a-select-option>
              </a-select>
          </a-row>
          <a-row style="margin:24px;display:flex">
            <span>车辆分类</span>
             <div style="margin-left:24px">
              <a-radio-group :options="plainOptions" @change="onChange" :defaultValue="value1" />
            </div> 
          </a-row>
          <a-row style="margin:24px;display:flex">
            <span>布控状态</span>
             <div style="margin-left:24px">
              <a-radio-group :options="plainOptions1" @change="onChange1" :defaultValue="value3" />
            </div> 
          </a-row>
          <a-row>
             <div class="addMark">
                <span>备注信息:</span>                
                  <a-input class="markPlace" placeholder="请填写备注信息"></a-input>
              </div>  
          </a-row> 
          <a-row>
            <div class="addFooter">
              <div class="buttonGroup">
                <a-button  icon="delete" class="delete" style="margin-left:10px" @click="cancle">取消</a-button>
                <a-button type="primary" icon="car" class="car" style="margin:10px" @click="ok">确认</a-button>
              </div> 
              
            </div> 
          </a-row>    
        </div>  
      </div> 
      <!--对话框-->
      <div>
    <a-modal     
      :visible="visible"
      @ok="handleOk"
      :confirmLoading="confirmLoading"
      @cancel="handleCancel"
    >
      <p>{{ ModalText }}</p>
    </a-modal>
  </div>
   <!--车型布控-->
   <div class="carDialog" v-show="carShow">
        <span class="title">车型布控</span>
        <span class="icon" @click=shutCar>x</span>  
        <div class="addContent">
          <a-row>
            <span class="carType"> 车辆类型：</span>
            <span></span>
          </a-row>
          <a-row style="margin:24px;display:flex">
            <span>车辆分类</span>
             <div style="margin-left:24px">
              <a-radio-group :options="plainOptions" @change="onChange" :defaultValue="value1" />
            </div> 
          </a-row>
          <a-row style="margin:24px;display:flex">
            <span>布控状态</span>
             <div style="margin-left:24px">
              <a-radio-group :options="plainOptions1" @change="onChange1" :defaultValue="value3" />
            </div> 
          </a-row>
          <a-row>
             <div class="addMark">
                <span>备注信息:</span>                
                  <a-input class="markPlace" placeholder="请填写备注信息"></a-input>
              </div>  
          </a-row> 
          <a-row>
            <div class="addFooter">
              <div class="buttonGroup">
                <a-button  icon="delete" class="delete" style="margin-left:10px" @click="cancle">取消</a-button>
                <a-button type="primary" icon="car" class="car" style="margin:10px" @click="okCar">确认</a-button>
              </div> 
              
            </div> 
          </a-row>    
        </div>  
      </div> 
      </a-layout-content>
    </a-layout>
  </a-layout>
</template>
<script>
const columns = [
  {
    title: '车辆分类',
    dataIndex: 'name',
 
    width:250,    
    scopedSlots: { customRender: 'name' },
  },
  {
    title: '车辆类型',
    dataIndex: 'carType',
  
    width: 250,
  },
  {
    title: '添加日期',
    dataIndex: 'date',
 
    ellipsis: true,
    width:250
  },
  {
    title: '布控状态',
    dataIndex: 'state',
 
    ellipsis: true,
    width:250
  },
  {
    title: '备注信息',
    dataIndex: 'mark',
  
    ellipsis: true,
    width:250
  },
  {
    title: '操作人员',
    dataIndex: 'actionPeople',
    
    ellipsis: true,
    width:250
  },
];

const datas = [
  {
    id:1,
    name: '一类车',
    carType:'皮卡车',
    date:'2010-1-1',
    state:'未布控',
    mark: '皮卡车',
    actionPeople:'超级管理员'
  },
  {
    id:2,
    name: '一类车',
    carType: '商务车',
    date:'2010-1-1',
    state:'未布控',
    mark: '皮卡车',
    actionPeople:'超级管理员'
  },
  {
    id:3,
    name: '一类车',
    carType: '越野车',
    date:'2010-1-1',
    state:'未布控',
    mark: '皮卡车',
    actionPeople:'超级管理员'
  },
  {
    id:4,
   name: '一类车',
    carType: '小轿车',
    date:'2010-1-1',
    state:'未布控',
    mark: '皮卡车',
    actionPeople:'超级管理员'
  },
  {
    id:5,
    name: '一类车',
    carType: '小轿车',
    date:'2010-1-1',
    state:'未布控',
    mark: '皮卡车',
    actionPeople:'超级管理员'
  },
  {
    id:6,
    name: '一类车',
    carType:'小轿车',
    date:'2010-1-1',
    state:'未布控',
    mark: '皮卡车',
    actionPeople:'超级管理员'
  },
  {
    id:7,
    name: '一类车',
    carType: '越野车',
    date:'2010-1-1',
    state:'未布控',
    mark: '皮卡车',
    actionPeople:'超级管理员'
  },
  {
    id:8,
    name: '一类车',
    carType: '越野车',
    date:'2010-1-1',
    state:'未布控',
    mark: '皮卡车',
    actionPeople:'超级管理员'
  },
];
const rowSelection = {
  onChange: (selectedRowKeys, selectedRows) => {
    console.log(`selectedRowKeys: ${selectedRowKeys}`, 'selectedRows: ', selectedRows);
  },

};
const plainOptions = ['一类车', '二类车',];

const plainOptions1=['已布控','未布控']
export default {
  data() {
    return {
      collapsed: false,
      datas,
      columns,
       rowSelection,
       addShow:false,
       plainOptions,    
       value1:['一类车'],
       value2:['二类车'],
       plainOptions1,
       value3:'已布控',
       value4:'未布控',
       mark:'请填写备注日期',
       types:'新增类型',
       ModalText: '确定要删除吗？',
       visible: false,
       confirmLoading: false,
       carShow:false,
       selectedRowKeys: [],
      
    };

  },
  methods: {
    handleChange(value) {
      console.log(`selected ${value}`);
    },
    add(type){
      
      this.addShow=true;
    },
    shutAdd(){
      this.addShow=false;
    },
    delete(){
    
    },
    edit(type){
      this.types='修改类型',
      this.addShow=true;

    },
    car(){
      this.carShow=true
    },
    onChange(){

    },
    ok(){
       this.addShow=false;
    },
    showModal() {
      this.visible = true;
    },
    handleOk(e) {
      this.ModalText = 'The modal will be closed after two seconds';
      this.confirmLoading = true;
      setTimeout(() => {
        this.visible = false;
        this.confirmLoading = false;
      }, 2000);
    },
    handleCancel(e) {
      console.log('Clicked cancel button');
      this.visible = false;
    },
    cancle(){

    },
    okCar(){
      this.carShow=false
    },
    shutCar(){
      this.carShow=false
    },
    
      //选中行的事件
       onSelectChange(selectedRowKeys) {
        console.log('selectedRowKeys changed: ', selectedRowKeys);
        this.selectedRowKeys = selectedRowKeys;
        
      },
     onChange1(){

     },
     handleClick(e){
       console.log(e)
     }
  },
  watch: {
    $route() {
    this.activeKey =  this.$route.xxx;
  }
},
};
</script>
<style>
#components-layout-demo-custom-trigger .trigger {
  font-size: 18px;
  line-height: 64px;
  padding: 0 24px;
  cursor: pointer;
  transition: color 0.3s;
}

#components-layout-demo-custom-trigger .trigger:hover {
  color: #1890ff;
}

#components-layout-demo-custom-trigger .logo {
  height: 32px;
  background: rgba(255, 255, 255, 0.2);
  margin: 16px;
}
.carType{
  margin-left:20px;
}
.search{
  margin-left:20px;  
}
.row{
  margin-top:24px;
  margin-left:24px;
}
.action-table{
  height:600px;
  margin-top:24px;
}
.pagenation{
  display: flex;
  align-items: center;
  justify-content: center
}
.addDialog{
  width:520px;
  height:467px;
  background: white;
  position:fixed;
  left:300px;
  top:200px;
  padding-top:12px;
}
.icon{
  float:right;
  width:56px;
  height: 56px;
}
.title{
  font-size: 18px;
  margin:12px 12px;
}
.addContent{
  height:360px;
  width:100%;
  border-top:1px solid gray;
  padding-top:24px;
}
.addMark{
  display: flex;
  margin:24px;
}
.markPlace{
  width:320px;
  height:60px;
  border:1px solid gray;
  margin-left:24px;
}
.addFooter{
  border-top:1px solid gray;
  margin:24px;
}
.buttonGroup{
  float:right;
  margin-top:24px;
}
.carDialog{
  width:520px;
  height:467px;
  background: white;
  position:fixed;
  left:300px;
  top:200px;
  padding-top:12px;
}
</style>