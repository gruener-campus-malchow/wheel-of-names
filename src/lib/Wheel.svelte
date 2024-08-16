<script>
    export let fields, wheel_angle
    const TAU = Math.PI * 2
</script>

<svg viewBox="-1.1 -1.1 2.2 2.2" class="drop-shadow-xl">
    <g style:transform={`rotate(${wheel_angle * 360/TAU}deg)`} style:transition="transform 4s cubic-bezier(0,0,.25,1)">
        {#if fields.length < 2}
            <circle cx="0" cy="0" r="1" stroke="black" stroke-width=".01" class="fill-gray-400" />
        {:else}
            {#each fields as field, i}
                <path d={`M0,0
								  L${Math.cos(field.start_angle)},${Math.sin(field.start_angle)}
								  A1,1 0 0 1 ${Math.cos(field.end_angle)},${Math.sin(field.end_angle)}
								  Z`}
                      stroke="black"
                      stroke-width=".01"
                      class={field.color} />
                <text x="0" y="0"
                      transform={`rotate(${field.label_angle * 360/TAU}) translate(.6)`}
                      text-anchor="middle" dominant-baseline="central"
                      fill="white" font-size={Math.min(1.5/field.label.length, .1)} class="font-sans font-bold">{field.label}</text>
            {/each}
        {/if}
    </g>

    <path d="M1.05,-.1 A.2,.1 0 0 1 .85,0 .2,.1 0 0 1 1.05,.1"
          fill="none" stroke="black" stroke-width=".02" stroke-linecap="round" stroke-linejoin="round" />
</svg>
