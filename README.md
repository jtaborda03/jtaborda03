E html>
<html>
    <head>
        <title> AAAaAAA</title>
        <style>canvas{ width: 100%; height: 100%;}</style>
    </head>
    <body>
        <script src="three.js"></script>
        <script src="cannon.js"></script>
        <script src="orbitControls.js"></script>

        <script>
            window.onload= function(){
                init();
                render();
                animate(0);
            }
            var angulo=0;
            var angulo2=22;
            var angulo3=44;
            //en la funcion init, inicializo las variables
            function init(){
                scene = new THREE.Scene();
                camera = new THREE.PerspectiveCamera( 75, window.innerWidth / window.innerHeight, 1, 10000 )
                camera.position.set(200,100,200)

                //luz ambiente
                const light = new THREE.AmbientLight( 0x8D36E3, 1.0 )
                scene.add( light )
                const light2 = new THREE.PointLight( 0xffffff, 5, 500 );
            light2.position.set( 250, 200, 250 );
            light2.castShadow = true; // default false
            scene.add( light2 );

            light2.shadow.mapSize.width = 1080; // default
            light2.shadow.mapSize.height = 1080; // default
            light2.shadow.camera.near = 0.5; // default
            light2.shadow.camera.far = 500;



                controls = new THREE.OrbitControls( camera );// mover camaraaa
                controls.maxDistance = 5000.0 //distancia maximaaa
                
                renderer = new THREE.WebGLRenderer()
                //

                renderer.shadowMap.enabled = true;
                renderer.shadowMap.type = THREE.PCFSoftShadowMap;
                //

                renderer.setSize( window.innerWidth, window.innerHeight )
                controls.update();//actualizar la direccion del puntero en el plano
                document.body.appendChild( renderer.domElement )
                //creando grid como cuadricula nose jijijiji
                const gridHelper = new THREE.GridHelper( 1000, 20 )//tamaño del plano
                scene.add( gridHelper )
                const axisHelper = new THREE.AxisHelper( 1000 )
                scene.add( axisHelper )

                //la caja
                const geometrya = new THREE.BoxGeometry();
                const materiala = new THREE.MeshToonMaterial( {color: 0x429FB8} );
                cube = new THREE.Mesh( geometrya, materiala );
                cube.castShadow = false; //default is false
                cube.receiveShadow = true;
                scene.add( cube );

                cube.position.set(0,-60,0);
                cube.scale.set(1000,10,1000);

                //esfera 1
                const geometry = new THREE.SphereGeometry( 0.1, 32 , 16 );
                const material = new THREE.MeshBasicMaterial( { color: 0xffff00 } );
                sphere = new THREE.Mesh( geometry, material );
                sphere.castShadow = true; //default is false
                sphere.receiveShadow = true;
                scene.add( sphere );

                sphere.position.set(50,20,100);
                sphere.scale.set(80,50,80);
                //esfera 2
                sphere2 = new THREE.Mesh( geometry, material );
                sphere2.castShadow = true; //default is false
                sphere2.receiveShadow = true;
                scene.add( sphere2 );

                sphere2.position.set(50,20,100);
                sphere2.scale.set(80,50,80);
                //esfera 3
                sphere3 = new THREE.Mesh( geometry, material );
                sphere3.castShadow = true; //default is false
                sphere3.receiveShadow = true;
                scene.add( sphere3 );

                sphere3.position.set(50,20,100);
                sphere3.scale.set(80,50,80);

                renderer.render( scene, camera );
            }
            function render(){
                renderer.render(scene, camera );
            }
            function animate(time){
                requestAnimationFrame(animate);
                controls.update();

                angulo = angulo + 0.09;
                var x = 20* Math.cos(angulo);
                var y = 20* Math.sin(angulo);

                sphere.position.set ( x, y, 0);

                angulo2 = angulo2 +0.02;
                var x2 = sphere.position.x*5 + 2*Math.cos(angulo2);
                var y2 = sphere.position.y*5 + 8*Math.cos(angulo2);
                var z = 20* Math.cos(angulo)* sphere.position.y;
                

         sphere2.position.set ( x2, y2, z);

            angulo3 = angulo3 + 0.10;
            var x3 = 20* Math.cos(angulo3);
            var y3 = 20* Math.sin(angulo3);

            sphere3.position.set ( x3, y3, 0);
                
                renderer.render( scene, camera);//

            }
        </script>
    </body>
</html>
