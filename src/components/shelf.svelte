<script>
	import * as SC from 'svelte-cubed';
	import {range} from '../utils/range.js';
	import Angle from '../components/angle.svelte';
    import Level from '../components/level.svelte';

    export let width;
    export let depth;
    export let height;
    export let angle_z;
    export let scale;
    export let shelves;

    let level = {
        thickness:3,
        height:30,
        color:0xaaaaaa,
    }

    let angle = {
        thickness:3,
        side:40,
        color:0x555555,
    }
</script>

<SC.Group
        rotation={[0, angle_z, 0]}
        scale={[1/scale, 1/scale, 1/scale]}
    >
        {#each range(0, shelves) as n}
            <Level width={width-angle.thickness*2-10}
                depth={depth-angle.thickness*2-level.thickness}
                z={height/2-height/shelves*n}
                {...level}
            />
        {/each}
        <Angle x={width/2} y={depth/2} angle={Math.PI} height={height} {...angle}/>
        <Angle x={-width/2} y={depth/2} angle={Math.PI/2} height={height} {...angle}/>
        <Angle x={-width/2} y={-depth/2} angle={0} height={height} {...angle}/>
        <Angle x={width/2} y={-depth/2} angle={-Math.PI/2} height={height} {...angle}/>
        
</SC.Group>