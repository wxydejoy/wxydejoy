### Hi there 👋

Here is wxydejoy

As you can see code is my joy

You can get more information  [here](https://c.undf.top)

Here are some repos to get you started:

![Top Langs](https://github-readme-stats.vercel.app/api/top-langs/?username=wxydejoy&langs_count=10&layout=compact)



| Machine(C & C++)                                             | Python                                                       | Npm Package                                                  |
| ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ |
| 平面三杆机械臂模拟 [DrawPath](https://github.com/wxydejoy/DrawPath) | 又拍云备份工具 [upyun-backup-server ](https://github.com/wxydejoy/upyun-backup-server) | [luoxiaohei](https://www.npmjs.com/package/live2d-widget-model-luoxiaohei) |
| 智能路边喷淋系统 [EMC](https://github.com/wxydejoy/EMC)      | 叶片 or 物块视觉识别[visual_identity_](https://github.com/wxydejoy/visual_identity_) | Not original, but modified                                   |
| 笔记 [doc-page](https://github.com/wxydejoy/doc-page)        | 一个友好的 HEXO 工具 [HexoDaily](https://github.com/wxydejoy/HexoDaily) | [abbrlink](https://www.npmjs.com/package/hexo-mod-abbrlink)  |

 Oh, I almost forgot to tell you that my major is mechanical engineering and intelligent manufacturing

 <img src="https://user-images.githubusercontent.com/81625961/147847145-e01a6c89-a917-4495-96d0-c94f0aadcc3b.gif"  />

<body>

		<script type="module">

      import * as THREE from './build/three.module.js';

      import Stats from './build/stats.js';

      import { STLLoader } from './build/stl.js';

			let container, stats;

			let camera, cameraTarget, scene, renderer;

			init();
			animate();

			function init() {

				container = document.createElement( 'div' );
				document.body.appendChild( container );

				camera = new THREE.PerspectiveCamera( 35, window.innerWidth / window.innerHeight, 1, 30 );
				camera.position.set( 0, 0.85, 0 );

				cameraTarget = new THREE.Vector3( 0, - 0.25, 0 );

				scene = new THREE.Scene();
				scene.background = new THREE.Color( 0x72645b );
				scene.fog = new THREE.Fog( 0x72645b, 2, 15 );

				// Ground

				const plane = new THREE.Mesh(
					new THREE.PlaneGeometry( 40, 40 ),
					new THREE.MeshPhongMaterial( { color: 0x999999, specular: 0x101010 } )
				);
				plane.rotation.x = - Math.PI / 2;
				plane.position.y = - 0.5;
				scene.add( plane );

				plane.receiveShadow = true;


				// ASCII file

				const loader = new STLLoader();
				

				// Binary files

				const material = new THREE.MeshPhongMaterial( { color: 0xAAAAAA, specular: 0x111111, shininess: 200 } );

				loader.load( './model/bysj.stl', function ( geometry ) {

					const mesh = new THREE.Mesh( geometry, material );

					mesh.position.set( 0, - 0.18, - 0.1 );
					mesh.rotation.set( - Math.PI / 2, 0, 0 );
					mesh.scale.set( 0.008, 0.008, 0.008 );

					mesh.castShadow = true;
					mesh.receiveShadow = true;

					scene.add( mesh );

				} );

				

				
				scene.add( new THREE.HemisphereLight( 0x443333, 0x111122 ) );

				addShadowedLight( 1, 1, 1, 0xffffff, 1.35 );
				addShadowedLight( 0.5, 1, - 1, 0xffaa00, 1 );
				// renderer

				renderer = new THREE.WebGLRenderer( { antialias: true } );
				renderer.setPixelRatio( window.devicePixelRatio );
				renderer.setSize( window.innerWidth, window.innerHeight );
				renderer.outputEncoding = THREE.sRGBEncoding;

				renderer.shadowMap.enabled = true;

				container.appendChild( renderer.domElement );

				// stats

				stats = new Stats();
				container.appendChild( stats.dom );

				//

				window.addEventListener( 'resize', onWindowResize );

			}

			function addShadowedLight( x, y, z, color, intensity ) {

				const directionalLight = new THREE.DirectionalLight( color, intensity );
				directionalLight.position.set( x, y, z );
				scene.add( directionalLight );

				directionalLight.castShadow = true;

				const d = 1;
				directionalLight.shadow.camera.left = - d;
				directionalLight.shadow.camera.right = d;
				directionalLight.shadow.camera.top = d;
				directionalLight.shadow.camera.bottom = - d;

				directionalLight.shadow.camera.near = 1;
				directionalLight.shadow.camera.far = 4;

				directionalLight.shadow.bias = - 0.002;

			}

			function onWindowResize() {

				camera.aspect = window.innerWidth / window.innerHeight;
				camera.updateProjectionMatrix();

				renderer.setSize( window.innerWidth, window.innerHeight );

			}

			function animate() {

				requestAnimationFrame( animate );

				render();
				stats.update();

			}

			function render() {

				const timer = Date.now() * 0.0005;

				camera.position.x = Math.cos( timer ) * 3;
				camera.position.z = Math.sin( timer ) * 3;

				camera.lookAt( cameraTarget );

				renderer.render( scene, camera );

			}

		</script>
	</body>