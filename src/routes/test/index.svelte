<script>
  import { onMount } from "svelte";
  import { Engine } from "@babylonjs/core/Engines/engine";
  import { Scene } from "@babylonjs/core/scene";
  import { Vector3 } from "@babylonjs/core/Maths/math";
  import { DirectionalLight } from "@babylonjs/core/Lights/directionalLight";
  import { ArcRotateCamera } from "@babylonjs/core/Cameras/arcRotateCamera";

  import { SceneLoader } from "@babylonjs/core/Loading/sceneLoader";
  import "@babylonjs/loaders/glTF/2.0/glTFLoader";

  onMount(() => {
    const canvas = document.getElementById("render-canvas");
    const engine = new Engine(canvas, true, null, true);
    const scene = new Scene(engine);

    const camera = new ArcRotateCamera(
      "ArcRotateCamera",
      2,
      1.45,
      4,
      new Vector3(0, 0, 0),
      scene
    );
    camera.panningSensibility = 0;
    scene.activeCamera.attachControl(canvas, false);

    new DirectionalLight("dir01", new Vector3(0.25, -1, 0), scene);

    engine.runRenderLoop(() => scene.render());

    SceneLoader.ImportMesh(
      "",
      "./",
      "capelina_crusader.gltf",
      scene,
      function (meshes) {
        console.log(meshes);
      }
    );
  });
</script>

<svelte:head>
  <title>Test</title>
</svelte:head>
<canvas id="render-canvas" width="800" height="600" />
