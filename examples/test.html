var camera, scene, renderer, projector;
var triangle;
var wall;
var allPoints = [];
var mouse;

var selectionMeshes = [];
var palette;

var geoTri;
var matDefault;
var matSelection;

var materials;

var init = function () {

	renderer = new THREE.CanvasRenderer();
	renderer.setSize( window.innerWidth, window.innerHeight );
	document.body.appendChild( renderer.domElement );

	camera = new THREE.PerspectiveCamera( 75, window.innerWidth / window.innerHeight, 1, 1000 );
	projector = new THREE.Projector();
	camera.position.z = 500;

	scene = new THREE.Scene();

	// Load Palettes
	palette = [];
  paletteImages = [
    "https://s3-us-west-2.amazonaws.com/s.cdpn.io/108947/18.png",
    "https://s3-us-west-2.amazonaws.com/s.cdpn.io/108947/1.png",
    "https://s3-us-west-2.amazonaws.com/s.cdpn.io/108947/6.png",
    "https://s3-us-west-2.amazonaws.com/s.cdpn.io/108947/12.png",
    "https://s3-us-west-2.amazonaws.com/s.cdpn.io/108947/16.png",
    "https://s3-us-west-2.amazonaws.com/s.cdpn.io/108947/17.png",
    "https://s3-us-west-2.amazonaws.com/s.cdpn.io/108947/15.png",
    "https://s3-us-west-2.amazonaws.com/s.cdpn.io/108947/21.png",
    "https://s3-us-west-2.amazonaws.com/s.cdpn.io/108947/20.png"
    ];

	for (var i = 0; i < paletteImages.length; i++) {
		var path = paletteImages[i];
		var texture = THREE.ImageUtils.loadTexture( path );

		palette.push ( new THREE.MeshPhongMaterial( { transparent:true, map: texture, side: THREE.DoubleSide} ));

	};

	registerListeners();

	// Make wall for mouse intersection
	wall = new THREE.Mesh(new THREE.PlaneGeometry(2000,2000), new THREE.MeshBasicMaterial({color:0x89898900, wireframe:true}));

	// Set Default objects
	triangle = new THREE.Shape([
		new THREE.Vector2 (-50,  0),
		new THREE.Vector2 (50, 0),
		new THREE.Vector2 (0,  75)
	]);

//	geoTri = new THREE.ExtrudeGeometry(triangle, { amount: 10 });
	geoTri = triangle.makeGeometry();
	geoTri.computeFaceNormals();
	// 1 2 0
	geoTri.faceVertexUvs[0][0][0] = new THREE.Vector2( 0, 0 );
	geoTri.faceVertexUvs[0][0][2] = new THREE.Vector2( 1, 1 );
	geoTri.faceVertexUvs[0][0][1] = new THREE.Vector2( 0, 1 );
	matDefault = new THREE.MeshBasicMaterial( { color: "rgb(0,200,200)", wireframe: false, transparent:true, side: THREE.DoubleSide } );
  	matDefault.opacity = 0.5;

  	matSelection = new THREE.MeshBasicMaterial( { color: 0xffffff, wireframe:true, side: THREE.DoubleSide } );

	createFirstObjects();
}

function registerListeners(){
	mouse = {x:0,y:0};

	document.addEventListener( 'mousemove', onDocumentMouseMove, false );
	document.addEventListener( 'touchmove', onDocumentMouseMove, false );
	document.addEventListener( 'mousedown', onDocumentMouseDown, false );
	document.addEventListener( 'touchstart', onDocumentMouseDown, false );
  
}

function createFirstObjects() {

	var firstTriMesh = new THREE.Mesh( geoTri.clone(), getRandomMaterial() );
	scene.add( firstTriMesh );

	allPoints.push( geoTri.vertices[0]);
	allPoints.push( geoTri.vertices[1]);
	allPoints.push( geoTri.vertices[2]);

	var numSelectionsToMake = 2;
	// Create and Add all selection meshes
	for ( var i = 0; i < numSelectionsToMake; i++ ) {
		var mesh = new THREE.Mesh( geoTri.clone(), matSelection.clone() );
		mesh.geometry.dynamic = true;
		selectionMeshes.push( mesh );
		scene.add( mesh );
	}

}

var animate = function () {
  	
  	for (var i = selectionMeshes.length - 1; i >= 0; i--) {
  		selectionMeshes[i].geometry.verticesNeedUpdate = true;
  	};

	requestAnimationFrame( animate );
	renderer.render( scene, camera );
}

function onDocumentMouseMove( event ) {

	event.preventDefault();

	mouse.x = ( event.clientX / renderer.domElement.width ) * 2 - 1;
	mouse.y = - ( event.clientY / renderer.domElement.height ) * 2 + 1;
//	mouse.z = getRandomArbitrary(-1, 1);
	mouse.z = 0;

	var position = getWorldPosition( mouse.x, mouse.y );
	if( position ) {

		for (var i = selectionMeshes.length - 1; i >= 0; i--) {
			var mesh = selectionMeshes[i];

			// set third vertex to cursor position
			var vertex = mesh.geometry.vertices[2];
			var isEven = (i % 2 == 0);

			if( isEven ) {
				var middle = window.innerWidth / 2;
				var isRightSide = (position.x > 0);
				var offset = Math.abs( position.x);
				if( isRightSide ) {
					// Flip to Left Side
					vertex.x = -offset;
				} else {
					// Flip to Right Side
					vertex.x = offset;
				}
			} else {
				vertex.x = position.x;
			}

			var sortedPoints = [];

			allPoints.forEach( function( point ) {
				sortedPoints.push( { x:point.x, y:point.y, d:point.distanceTo( vertex )} );
			});

			sortByKey( sortedPoints, "d");

			vertex.y = position.y;
			vertex.z = mouse.z;

			vertex = mesh.geometry.vertices[0];
			vertex.x = sortedPoints[0].x;
			vertex.y = sortedPoints[0].y;

			// Make sure picked points have some space between them
			var secondPointIndex = 1;
			var tooSmall = true;
			while( tooSmall ) {
				var secondPoint = sortedPoints[ secondPointIndex ];
				var innerDistance = new THREE.Vector2( secondPoint.x, secondPoint.y ).distanceTo( sortedPoints[0]);
				tooSmall = ( innerDistance < 2 );
				secondPointIndex ++;
			}

			targetVertex = mesh.geometry.vertices[1];
			targetVertex.x = sortedPoints[ secondPointIndex ].x;
			targetVertex.y = sortedPoints[ secondPointIndex ].y;

		};

	}
  
}

function getRandomMaterial() {
	return palette[ Math.floor( Math.random() * palette.length  )];
}

function onDocumentMouseDown( event ) {

	// set mouse data
	mouse.x = ( event.clientX / renderer.domElement.width ) * 2 - 1;
	mouse.y = - ( event.clientY / renderer.domElement.height ) * 2 + 1;

	event.preventDefault();
  
	var position = getWorldPosition( mouse.x, mouse.y );
	if( position ) {

		for (var i = selectionMeshes.length - 1; i >= 0; i--) {
			var mesh = selectionMeshes[i];

			// add new Mesh to scene
			var meshClone = new THREE.Mesh( mesh.geometry.clone(), getRandomMaterial() );
			meshClone.overdraw = true;
			scene.add( meshClone );

			allPoints.push( meshClone.geometry.vertices[0]);
			allPoints.push( meshClone.geometry.vertices[1]);
			allPoints.push( meshClone.geometry.vertices[2]);

			// remove duplicate points from allPoints
			allPoints = allPoints.filter( function( item, index, inputArray ) {
		           return inputArray.indexOf(item) == index;
		    });

			// update selection mesh using points from newly made geometry
			mesh.geometry.vertices[0] = meshClone.geometry.vertices[1].clone();
			mesh.geometry.vertices[1] = meshClone.geometry.vertices[2].clone();
			mesh.geometry.vertices[2] = meshClone.geometry.vertices[2].clone();
			};

	}
}

function getWorldPosition( x, y ) {
	var vector = new THREE.Vector3(  x, y, 0.5 );
	projector.unprojectVector( vector, camera );

	var raycaster = new THREE.Raycaster( camera.position, vector.sub( camera.position ).normalize() );
	var intersects = raycaster.intersectObjects( [wall] );

	if ( intersects.length > 0 ){
		return( intersects[0].point );
	} else {
		return false;
	}
}

function sortByKey(array, key) {
    return array.sort(function(a, b) {
        var x = a[key]; var y = b[key];
        return ((x < y) ? -1 : ((x > y) ? 1 : 0));
    });
}

// Returns a random number between min and max
function getRandomArbitrary(min, max) {
  return Math.random() * (max - min) + min;
}

init();
animate();