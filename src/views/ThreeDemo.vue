<template>
  <div></div>
</template>

<script>
import * as Three from "three";

export default {
  name: "ThreeDemo1",
  mounted() {
    this.initThree();
  },
  methods: {
    initThree() {
      // 场景
      let scene = new Three.Scene();
      let geometry = new Three.BoxGeometry(100, 100, 100);
      let material = new Three.MeshLambertMaterial({ color: 0x0000ff });
      let mesh = new Three.Mesh(geometry, material);
      scene.add(mesh);

      // 光源
      let point = new Three.PointLight(0xffffff);
      point.position.set(400, 200, 300);
      scene.add(point);
      let ambient = new Three.AmbientLight(0x444444);
      scene.add(ambient);

      // 相机
      let width = window.innerWidth - 100;
      let height = window.innerHeight - 100;
      let k = width / height;
      let s = 200;
      let camera = new Three.OrthographicCamera(-s * k, s * k, s, -s, 1, 1000);
      camera.position.set(200, 300, 200);
      camera.lookAt(scene.position);

      // 渲染器
      let renderer = new Three.WebGLRenderer();
      renderer.setSize(width, height);
      renderer.setClearColor(0xb9d3ff, 1);

      document.body.appendChild(renderer.domElement);

      const render = () => {
        renderer.render(scene, camera);
        mesh.rotateY(0.01);
        requestAnimationFrame(render);
      };

      render();
    },
  },
};
</script>

<style scoped></style>
