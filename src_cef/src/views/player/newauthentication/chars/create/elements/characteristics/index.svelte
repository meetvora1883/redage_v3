<script>
    import { data } from 'store/customization';
    import ListButton from './listbutton.svelte';
    import Selector from './selector/index.svelte';
    import { gender, customization, updateCharacteristic } from 'store/customization';

    import characteristics from './characteristics.js';

    let isUse = false;
    let refCallback = null;
    let refCallbackPoint = null;
    let activeItem = 0;

    const componentsData = [
        {
            name: 'Forehead',
            dataname: 'brow',
            preset: 0,
            gridType: false,

            xgrid: ['Flat', 'Convex'],
            ygrid: ['High', 'Low'],
        },
        {
            name: 'Eyes',
            dataname: 'eyes',
            preset: 0,
            gridType: true,

            xgrid: ['Narrow', 'Wide'],
            ygrid: [],
        },
        {
            name: 'Nose',
            dataname: 'nose',
            preset: 0,
            gridType: false,

            xgrid: ['Narrow', 'Wide'],
            ygrid: ['Upturned', 'Low'],
        },
        {
            name: 'Nose profile',
            dataname: 'noseprofile',
            preset: 0,
            gridType: false,

            xgrid: ['Small', 'Large'],
            ygrid: ['With hump', 'Curved'],
        },
        {
            name: 'Nose tip',
            dataname: 'nosetip',
            preset: 0,
            gridType: false,

            xgrid: ['Slant left', 'Slant right'],
            ygrid: ['Tip up', 'Tip down'],
        },
        {
            name: 'Cheekbones',
            dataname: 'cbones',
            preset: 0,
            gridType: false,

            xgrid: ['Thin', 'Full'],
            ygrid: ['High', 'Low'],
        },
        {
            name: 'Cheeks',
            dataname: 'cheeks',
            preset: 0,
            gridType: true,

            xgrid: ['Thin', 'Full'],
            ygrid: [],
        },
        {
            name: 'Lips',
            dataname: 'lips',
            preset: 0,
            gridType: true,

            xgrid: ['Thin', 'Thick'],
            ygrid: [],
        },
        {
            name: 'Jaw',
            dataname: 'jaw',
            preset: 0,
            gridType: false,

            xgrid: ['Narrow', 'Wide'],
            ygrid: ['Round', 'Square'],
        },
        {
            name: 'Chin profile',
            dataname: 'chinprofile',
            preset: 0,
            gridType: false,

            xgrid: ['Short', 'Long'],
            ygrid: ['High', 'Low'],
        },
        {
            name: 'Chin shape',
            dataname: 'chinform',
            preset: 0,
            gridType: false,

            xgrid: ['Square', 'Pointed'],
            ygrid: ['Round', 'With dimple'],
        }
    ];

    const OnPresetChanged = (index, change) => {
        activeItem = index;

        const key = componentsData[activeItem].dataname;
        let preset = $customization[key].preset;
        preset += change;

        if (preset >= 3) preset = 0;
        else if (preset < 0) preset = 2;

        let presetSettings = characteristics[key][preset];
        updateCharacteristic($gender, key, preset, presetSettings.x, presetSettings.y);
    }
    
    const OnCustomPresetChanged = (key, x, y) => {
        updateCharacteristic($gender, key, 3, x, y);
    }
    
    const handleKeyUp = (event) => {
        const { keyCode } = event;
        switch (keyCode) {
            case 38: // up
                if(--activeItem < 0)
                    activeItem = componentsData.length - 1;
                break;
            case 40: // down
                if(++activeItem >= componentsData.length)
                    activeItem = 0;
                break;
        }
    }
</script>

<svelte:window on:keyup={handleKeyUp} />

<div class="auth__customization_elements">
    {#each componentsData as item, index}
    {#if $customization[item.dataname]}
    <div class="auth__customization_element" class:active={activeItem === index} on:click={() => activeItem = index}>
        <div class="auth__customization_leftside">{item.name}</div>

        <ListButton
            on:click={e => activeItem = index}
            key={item.dataname}
            active={activeItem === index}
            preset={$customization[item.dataname].preset}
            onChange={(change) => OnPresetChanged (index, change)} />
    </div>
    {/if}
    {/each}
</div>
<div class="auth__scroll" />
<div class="title margin-top-20">{componentsData[activeItem].name}:</div>
{#if $customization[componentsData[activeItem].dataname]}
<Selector
    isLine={componentsData[activeItem].gridType}
    key={componentsData[activeItem].dataname}
    x={$customization[componentsData[activeItem].dataname].x}
    y={$customization[componentsData[activeItem].dataname].y}
    xLeftName={componentsData[activeItem].xgrid[0]}
    xRightName={componentsData[activeItem].xgrid[1]}
    yTopName={componentsData[activeItem].ygrid[0]}
    yBottomName={componentsData[activeItem].ygrid[1]}
    onChange={OnCustomPresetChanged} />

{/if}
