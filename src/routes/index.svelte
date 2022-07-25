<!-- npn run dev -->

<script>
	import * as THREE from 'three';
	import * as SC from 'svelte-cubed';
    import Shelf from '../components/shelf.svelte';

    let room_x = 2000;
    let room_y = 2000;
    let room_z = 2000;

    let GRID_COLOR = 0x999999;
    let SKY_COLOR = 0xf8f1f8;
    let FLOOR_COLOR = 0xc8c1c8;

    let SCALE = 1000;

    let vars = {
        width:{
            label:'Width',
            min:400,
            max:1200,
            step:50,
            scale:1/10,
            suffix:' cm',
            value:1000,
        },
        depth:{
            label:'Depth',
            min:200,
            max:800,
            step:50,
            scale:1/10,
            suffix:' cm',
            value:400,
        },
        height:{
            label:'Height',
            min:500,
            max:3500,
            step:50,
            scale:1/10,
            suffix:' cm',
            value:1800,
        },
        shelves:{
            label:'Shelve count',
            min:3,
            max:14,
            step:1,
            scale:1,
            suffix:'',
            value:5,
        }
    } 
</script>

<SC.Canvas
    antialias
    background={new THREE.Color(SKY_COLOR)}
    fog={new THREE.FogExp2(SKY_COLOR, 0.1)}
    shadows
>
    <SC.Group position={[0, -vars.height.value/2/SCALE, 0]}>
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
        <SC.Primitive
            object={new THREE.EdgesGeometry(new THREE.BoxBufferGeometry(room_x/SCALE, room_z/SCALE, room_y/SCALE), 1)}
            position={[0, 1, 0]}
        />
    </SC.Group>

    <Shelf width={vars.width.value} height={vars.height.value} depth={vars.depth.value} shelves={vars.shelves.value} angle_z=0 scale={SCALE}></Shelf>

    <SC.PerspectiveCamera position={[-2, 2.0, 3]} />
    <SC.OrbitControls enableZoom={false} maxPolarAngle={Math.PI * 0.56} />
    <SC.AmbientLight intensity={0.5} />
    <SC.DirectionalLight intensity={0.6} position={[-2, 3, 2]} shadow={{ mapSize: [2048, 2048] }} />
</SC.Canvas>

<div class="controls">
    {#each Object.entries(vars) as [_, v]}
    <label>{v.label}<input type="range" bind:value={v.value} min={v.min} max={v.max} step={v.step} />{ v.value*v.scale }{v.suffix}</label>
    {/each}
    <!--
    <label>E Largo<input type="number" bind:value={room_x} min={400} max={1200} step={10} />{ room_x/10 } cm</label>
    <label>E Ancho<input type="number" bind:value={room_y} min={400} max={1200} step={10} />{ room_y/10 } cm</label>
    <label>Largo<input type="range" bind:value={width} min={400} max={1200} step={10} />{ width/10 } cm</label>
    <label>Fondo<input type="range" bind:value={depth} min={200} max={800} step={10} />{ depth/10 } cm</label>
    <label>Alto<input type="range" bind:value={height} min={500} max={2500} step={10} />{ height/10 } cm</label>
    <label>Niveles<input type="range" bind:value={shelves} min={3} max={14} step={1} color={0xFF0000}/>{ shelves }</label>
    -->
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



