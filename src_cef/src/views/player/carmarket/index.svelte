<script>
    import { translateText } from 'lang'
    import './main.sass'
    
    let CarStats = {
        name: "Elegy Super FT",
        descr: "Timeless classic",
        owner: "Vitaliy Zdobich",
        number: 2281337,
        gosprice: 50000,
        tune: [
            "Engine Level 4",
            "Brakes Level 4",
            "Wheels Level 4",
            "Windows Level 4",
            "Exhaust Level 4"
        ],
        price: 100000
    }
</script>

<div id="carmarket">
    <div class="carmarket__panel">
        <div class="carmarket__header">{translateText('player', 'Vehicle Purchase')}</div>
        <div class="carmarket__mainmenu">
            <div class="carmarket__mainmenu_center left">
                <div class="carmarket__rielt_info left">
                    <div class="carmarket__rielt_header">{CarStats.name}</div>
                    <div class="carmarket__gray">{CarStats.descr}</div>
                    <div class="carmarket__rielt_stat">
                        <div class="carmarket__rielt_element">
                            <div class="carmarket__gray">{translateText('player', 'Owner')}:</div>
                            <div>{CarStats.owner}</div>
                        </div>
                        <div class="carmarket__rielt_element">
                            <div class="carmarket__gray">{translateText('player', 'Phone Number')}:</div>
                            <div>{CarStats.number}</div>
                        </div>
                        <div class="carmarket__rielt_element">
                            <div class="carmarket__gray">{translateText('player', 'Government Price')}:</div>
                            <div>{CarStats.gosprice}$</div>
                        </div>
                        <div class="carmarket__rielt_element">
                            <div class="carmarket__gray">{translateText('player', 'Tuning')}:</div>
                            <div class="box-column">
                                {#each CarStats.tune as detail, index}
                                    <div>{detail}</div>
                                {/each}
                            </div>
                        </div>
                    </div>
                    <div class="box-column">
                        <div class="carmarket__rielt_price">${CarStats.price}</div>
                        <div class="carmarket__gray">{translateText('player', 'Approximate tuned price')}:</div>
                    </div>
                </div>
            </div>
            <div class="carmarket__mainmenu_block"></div>
        </div>

        <div class="box-between">
            <div class="house_bottom_buttons back">
                <div>{translateText('player', 'Buy')}</div>
                <div class="house_bottom_button">Enter</div>
            </div>
            <div class="house_bottom_buttons esc">
                <div>{translateText('player', 'Exit')}</div>
                <div class="house_bottom_button">ESC</div>
            </div>
        </div>
    </div>
</div>
