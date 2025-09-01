<template>
  <div id="cesiumContainer"></div>
  
  
  
  
</template>

 
<script setup lang='ts'>
import * as Cesium from 'cesium';
import { onMounted } from 'vue';
import {
  Cesium3DTile,
  Cartesian3,
  Matrix4,
  Transforms,
  Math as CesiumMath 
} from 'cesium'


onMounted(async () =>{
  Cesium.Ion.defaultAccesssToken = 'eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJqdGkiOiJlMDZjNzk2YS05ZDI5LTQxNDQtOWQyZi1lZTExYzk5OTIxM2UiLCJpZCI6MjM5ODg0LCJpYXQiOjE3MjU3Nzc1MTB9.16MVVV-m6ndRsZ1k6Vli0b4Xv2mNFKcYO04qDorcuqk'
  //viewer是
  


  const viewer = new Cesium.Viewer('cesiumContainer',{
    //timeline: false,//时间轴
    //animation: false,//动画
    //geocoder: false,//搜索
    //homeButton: false,//主页
    //sceneModePicker: false,//投影方式
    //baseLayer: false,//图层选择
    //navigationHelpButton: false,//帮助
    //fullscreenButton: false,//全屏
  });
  viewer.camera.flyTo({
    destination:Cesium.Cartesian3.fromDegrees(118.93611520,32.1109622,800),
    //方向，俯仰角度
    duration: 5,
    orientation:{
      heading:Cesium.Math.toRadians(0),
      pitch:Cesium.Math.toRadians(-40),
      roll: (0),
    }
  })

  const label = viewer.entities.add({
    position: Cesium.Cartesian3.fromDegrees(118.93611520,32.1199922),
    label: {
      text:"光纤振动强度：a",
    }
  })
  viewer.zoomTo(label)

  

  const polyline = viewer.entities.add({
    polyline: {
      positions:Cesium.Cartesian3.fromDegreesArray([118.93911520,32.120140,118.93601520,32.120140]),
      width: 10,
      material: Cesium.Color.YELLOW
    
    }
  })
  viewer.zoomTo(polyline)
  
  

  const tileset = await Cesium.Cesium3DTileset.fromUrl('../node_modules/YANGSAHN/Data/tileset.json')
  viewer.scene.primitives.add(tileset)
  viewer.zoomTo(tileset)  
  viewer.entities.add(polyline)

  
})
</script>



    
    

