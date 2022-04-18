<template>
  <div class="hello-three">
    <div ref="container"></div>
  </div>
</template>

<script>
import * as Three from "three";
import { OrbitControls } from "three/examples/jsm/controls/OrbitControls";
import img11 from "../assets/img/skybox_mx.png";
import img12 from "../assets/img/skybox_px.png";
import img13 from "../assets/img/skybox_my.png";
import img21 from "../assets/img/skybox_py.png";
import img22 from "../assets/img/skybox_mz.png";
import img23 from "../assets/img/skybox_pz.png";

const scene = new Three.Scene();

export default {
  name: "HelloThree",
  data() {
    return {};
  },
  mounted() {
    this.init3dScene();
  },
  methods: {
    init3dScene() {
      this.whole = new Three.Group();
      this.yuanQuGroup = new Three.Group();
      this.yuanQuBuildGroup = new Three.Group();

      this.initRender();
      this.initScene();
      this.initCamera();
      this.initLight();
      this.startAnimate();
    },
    // 初始化渲染器
    initRender() {
      this.renderer = new Three.WebGLRenderer({
        antialias: true,
        precision: "highp",
        logarithmicDepthBuffer: true,
        preserveDrawingBuffer: true,
      });

      this.renderer.setClearColor(0x000000, 0);
      this.renderer.setSize(window.innerWidth - 100, window.innerHeight - 100);
      this.renderer.setPixelRatio(window.devicePixelRatio);

      this.$refs.container.appendChild(this.renderer.domElement);
    },
    // 初始化场景
    initScene() {
      scene.matrixAutoUpdate = false;

      let axes = new Three.AxesHelper(100);
      scene.add(axes);

      const skyBox = [img11, img12, img13, img21, img22, img23];

      scene.background = new Three.CubeTextureLoader().load(skyBox);
    },
    // 初始化相机
    initCamera() {
      this.camera = new Three.PerspectiveCamera(
        30,
        window.innerWidth / window.innerHeight,
        1,
        10000
      );
      this.camera.position.x = 697.1343985659603;
      this.camera.position.y = 1784.0457888299613;
      this.camera.position.z = 1566.095679557605;

      this.camera.up.x = 0;
      this.camera.up.y = 1;
      this.camera.up.z = 0;

      this.camera.lookAt({
        x: 0,
        y: 0,
        z: 0,
      });

      this.controls = new OrbitControls(this.camera, this.renderer.domElement);
      this.controls.target = new Three.Vector3(0, 1, 0);
      this.controls.enableZoom = true;
      this.controls.autoRotate = false;
      this.controls.maxPolarAngle = Math.PI / 2;
      this.controls.enablePan = true;
      this.controls.rotateSpeed = 1;
      this.controls.enableDamping = true;
      this.controls.minDistance = 1;
      this.controls.maxDistance = 20000;
    },
    // 初始化光源
    initLight() {
      let ambientLight = new Three.AmbientLight(0xf1e2e2, 1.25);
      scene.add(ambientLight);

      let pointLight = new Three.PointLight(0xbfbfbf, 0.6);
      pointLight.position.set(0, 40, 80);
      scene.add(pointLight);
    },
    // 动画帧
    startAnimate() {
      this.renderer.render(scene, this.camera);
      requestAnimationFrame(this.startAnimate);
    },
  },
};
</script>

<style scoped></style>
