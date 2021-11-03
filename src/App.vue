<template>
  <div id="app">
    <canvas ref="canvas" id="canvas"/>
  </div>
</template>

<script>
import * as THREE from 'three';
import { OrbitControls } from 'three/examples/jsm/controls/OrbitControls.js';
import { FBXLoader } from 'three/examples/jsm/loaders/FBXLoader.js';

export default {
  name: 'App',
  components: {
  },
  mounted() {
    const canvas = this.$refs.canvas

    let scene, camera, renderer;
    function init() {
      camera = new THREE.PerspectiveCamera( 45, window.innerWidth / window.innerHeight, 0.1, 20000);
      camera.position.set( 0, 5000, 5500);
      // camera.rotateOnAxis('z', 45)

      scene = new THREE.Scene();
      scene.background = new THREE.Color( 0xFFFFFF );

      const hlight = new THREE.AmbientLight (0xFFFFFF);
      scene.add(hlight);

      const light = new THREE.PointLight(0xeeeeee,0.4);
      light.position.set(0,2000,0);
      scene.add(light);

      const light2 = new THREE.PointLight(0xeeeeee,0.4);
      light.position.set(0,-2000,0);
      scene.add(light2);

      const light3 = new THREE.PointLight(0xeeeeee,0.4);
      light.position.set(0,4000,4000);
      scene.add(light3);

      renderer = new THREE.WebGLRenderer({antialias:true, canvas});
      renderer.setSize(window.innerWidth,window.innerHeight);

      const controls = new OrbitControls(camera, renderer.domElement);
      controls.enableZoom = false
      controls.rotateSpeed = 0.4

      let loader = new FBXLoader();
      loader.load('legion_base.fbx', function(object){
        scene.add(object);
        animate();
      });
    }

    function animate() {
      renderer.render(scene,camera);
      requestAnimationFrame(animate);
    }
    init();
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  margin-top: 60px;
}
</style>
