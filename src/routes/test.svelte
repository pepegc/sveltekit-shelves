<script>
	import * as THREE from 'three';
	import * as SC from 'svelte-cubed';
    import Shelf from '../components/shelf.svelte';

    let width = 1050;
	let height = 1800;
	let depth = 500;

    let shelves = 4;

	let spin = 0;

    let GRID_COLOR = 0x999999;
    let SKY_COLOR = 0xf8f1f8;
    let FLOOR_COLOR = 0xc8c1c8;

    let SCALE = 1000;

</script>

<SC.Canvas
    antialias
    background={new THREE.Color(SKY_COLOR)}
    fog={new THREE.FogExp2(SKY_COLOR, 0.1)}
    shadows
>
    <SC.Group position={[0, -height/2/SCALE, 0]}>
        <SC.Mesh
            geometry={new THREE.PlaneGeometry(500, 500)}
            material={new THREE.MeshStandardMaterial({ color: FLOOR_COLOR })}
            rotation={[-Math.PI / 2, 0, 0]}
            receiveShadow
        />
        <SC.Primitive
            object={new THREE.GridHelper(100, 100, GRID_COLOR, GRID_COLOR)}
            position={[0, 0.001, 0]}
        />
        <SC.Primitive
            object={new THREE.GridHelper(1, 1, 0xff0000, 0xff0000)}
            position={[0, 0.001, 0]}
        />
    </SC.Group>

    <Shelf {width} {height} {depth} {shelves} angle_z=0 scale={SCALE}></Shelf>

    <SC.PerspectiveCamera position={[-2, 2.0, 3]} />
    <SC.OrbitControls enableZoom={false} maxPolarAngle={Math.PI * 0.56} />
    <SC.AmbientLight intensity={0.5} />
    <SC.DirectionalLight intensity={0.6} position={[-2, 3, 2]} shadow={{ mapSize: [2048, 2048] }} />
</SC.Canvas>

<div class="controls">
    <label>Largo<input type="range" bind:value={width} min={400} max={1200} step={10} />{ width/10 } cm</label>
    <label>Fondo<input type="range" bind:value={depth} min={200} max={800} step={10} />{ depth/10 } cm</label>
    <label>Alto<input type="range" bind:value={height} min={500} max={2500} step={10} />{ height/10 } cm</label>
    <label>Niveles<input type="range" bind:value={shelves} min={3} max={14} step={1} color={0xFF0000}/>{ shelves }</label>
</div>

<style>
	.controls {
        width:100%;
		position: absolute;
		left: 1em;
		top: 1em;
	}

	label {
		display: flex;
		width: 100%;
		gap: 0.5em;
		align-items: center;
	}

	input {
		margin: 0;
	}
</style>



