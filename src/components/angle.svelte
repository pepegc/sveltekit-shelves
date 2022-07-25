<script>
	import * as THREE from 'three';
	import * as SC from 'svelte-cubed';

    export let x = 1;
    export let y = 1 ;
	export let angle = 0;
	export let height = 1000;

    export let side;
    export let thickness;
    export let color;

    let leg_extra = 8;
</script>


<SC.Group
    position={[x, 0, y]}
    rotation={[0, angle, 0]}
>
    <SC.Mesh
        geometry={new THREE.BoxGeometry(side, height, thickness)}
        position={[side/2, 0, thickness/2]}
        material={new THREE.MeshStandardMaterial({ color: color })}
        castShadow
    /> 
    <SC.Mesh
        geometry={new THREE.BoxGeometry(thickness, height, side)}
        position={[thickness/2, 0, side/2]}
        material={new THREE.MeshStandardMaterial({ color: color })}
        castShadow
    /> 
    <SC.Mesh
        geometry={new THREE.BoxGeometry(side+leg_extra, 30, thickness+leg_extra)}
        position={[side/2, -height/2, thickness/2]}
        material={new THREE.MeshStandardMaterial({ color: 0x000000 })}
        castShadow
    /> 
    <SC.Mesh
        geometry={new THREE.BoxGeometry(thickness+leg_extra, 30, side+leg_extra)}
        position={[thickness/2, -height/2, side/2]}
        material={new THREE.MeshStandardMaterial({ color: 0x000000 })}
        castShadow
    /> 
</SC.Group>