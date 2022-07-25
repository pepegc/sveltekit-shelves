<script>
	import * as THREE from 'three';
	import * as SC from 'svelte-cubed';

    export let width;
    export let depth;
    export let z;

    export let thickness;
    export let height;
    export let color;

   

</script>


<SC.Group
    position={[0, z, 0]}
>
    <SC.Mesh
        geometry={new THREE.BoxGeometry(width, thickness, depth)}
        position={[0, -thickness/2, 0]}
        material={new THREE.MeshStandardMaterial({ color: color })}
        castShadow
    /> 
    <SC.Mesh
        geometry={new THREE.BoxGeometry(width, height, thickness)}
        position={[0, -height/2, depth/2]}
        material={new THREE.MeshStandardMaterial({ color: color })}
        castShadow
    /> 
    <SC.Mesh
        geometry={new THREE.BoxGeometry(width, height, thickness)}
        position={[0, -height/2, -depth/2]}
        material={new THREE.MeshStandardMaterial({ color: color })}
        castShadow
    /> 
</SC.Group>