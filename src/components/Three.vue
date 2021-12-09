<template>
  <div>
      
      <div id="container"></div>
      <button  v-on:click="moveup">Haut</button></br>
      <button id="gauche" v-on:click="moveleft">Gauche</button><button  id="reset" v-on:click="reset">RESET</button><button v-on:click="moveright">Droite</button></br>
      <button v-on:click="movedown">Bas</button></br></br></br>
      <button v-on:click="sizeplus">Zoom ++</button>
      <button v-on:click="sizemoins">Zoom --</button></br></br></br>
      <button v-on:click="rotationplus">Rotation ++</button>

  </div>
</template>

<script>
let size = 2;
let up = '';
let right = '';
import * as three from 'three'
export default {
    name:'TreeJS',
    data(){
        return{
            scene:null,
            camera:null,
            renderer:null,
            mesh:null,
        }
    },
     methods: {

    init: function() {
        let container = document.getElementById('container');
        let tailleTab = 16
        this.camera = new three.PerspectiveCamera(70, container.clientWidth/container.clientHeight, 0.01, 50);
        this.camera.position.z = 19;
        this.camera.position.x = 0;
        this.camera.position.y = 0;
        this.scene = new three.Scene();
        let geometry = new three.BoxGeometry(size, size, size);
        let terre = new three.MeshBasicMaterial( {color: 0x00ff00} );
        this.mesh = new three.Mesh( geometry, terre )
         this.scene.add(this.mesh);
       this.renderer = new three.WebGLRenderer({antialias: true});
        this.renderer.setSize(container.clientWidth, container.clientHeight);
        container.appendChild(this.renderer.domElement);
},
    animate: function() {
        requestAnimationFrame(this.animate);
        this.mesh.rotation.x += 0.0008;
        this.mesh.rotation.y += 0.0008;
        this.renderer.render(this.scene, this.camera);
    },
    

    moveup : function(event){
     let up2 = up++
     this.mesh.position.y = up2;
     console.log(up)
    },

    movedown : function(event){
        let down2 = up--
        this.mesh.position.y = down2;
        console.log(up)
    },

     moveright : function(event){
        let right2 = right++
        this.mesh.position.x = right2;
    },

    moveleft : function(event){
        let left2 = right--
        this.mesh.position.x = left2;
    },

    reset : function(event){
        this.mesh.position.x = 0;
        this.mesh.position.y = 0;
        up = 0;
        right = 0;
    },

    sizeplus : function(event){
        this.mesh.scale.x += 1;
         this.mesh.scale.y += 1;
         this.mesh.scale.z += 1;
    },

    sizemoins : function(event){
        this.mesh.scale.x -= 1;
         this.mesh.scale.y -= 1;
         this.mesh.scale.z -= 1;
    },

    rotationplus : function(event){
        this.mesh.rotation.x += 1;
        this.mesh.rotation.y += 1;
        this.mesh.rotation.z += 1;
    }

  },
    mounted(){
        /*const container = document.querySelector('#scene-container');
        const fov = 70; 
        const aspect = container.clientWidth / container.clientHeight;
        const near = 0.1; 
        const far = 100;
        this.camera = new three.PerspectiveCamera(fov, aspect, near, far);
        this.scene = new three.Scene();
        this.camera.position.set(0, 0, 15);
        const geometry = new three.BoxBufferGeometry(2, 2, 2); 
        const material = new three.MeshBasicMaterial()
        const cube = new three.Mesh(geometry, material);
        this.scene.add(cube);
        const geometrye = new three.PlaneGeometry( 1, 1 );
        const terre = new three.MeshBasicMaterial( {color: 0x32CD32, side: three.DoubleSide} );
        const mech = new three.Mesh( geometrye, terre )
        this.scene.add(mech)



        this.renderer = new three.WebGLRenderer();
        this.renderer.setSize(container.clientWidth, container.clientHeight);
        this.renderer.setPixelRatio(window.devicePixelRatio);
        container.append(this.renderer.domElement);
        this.renderer.render(this.scene, this.camera);*/
        this.init();
        this.animate();
    },
}

</script>
<style>

#gauche {
    margin-right : 15%
}

#scene-container {
  width: 60%;
  height: 60%;
  background-color: skyblue;
}
#container{
    width: 1000px;
    height: 700px;
    margin-left: auto;
    margin-right: auto;
  }

#reset {
    margin-right:16%;
}
</style>