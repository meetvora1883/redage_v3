<script>
    import { translateText } from 'lang'
    import { executeClient } from 'api/rage'
    import { format } from 'api/formatter'    
    import { charBankMoney } from 'store/chars';

    import './css/main.css'

    import Business from './elements/business.svelte'
    import Input from './elements/input.svelte'
    import Menu from './elements/menu.svelte'

    export let viewData;

    let SelectViews = "Menu";

    const Views = {
        Menu,
        Input,
        Business
    }

    const menuItem = [
        {
            "title": translateText('player', 'Deposit funds'),
            "icon": "ic-user-shared-fill"
        },
        {
            "title": translateText('player', 'Withdraw funds'),
            "icon": "ic-user-received-fill"
        },
        {
            "title": translateText('player', 'Pay property tax'),
            "icon": "ic-home-fill"
        },
        {
            "title": translateText('player', 'Pay business tax'),
            "icon": "ic-store-fill"
        },
        {
            "title": translateText('player', 'Transfer to another account'),
            "icon": "ic-article-fill"
        }
    ];

    let
        type = 1,
        subdata = '',   
        number = viewData.number,
        activeMain = 0,
        holder = viewData.holder,
        placeholder = "";


    window.atm = {
        open: (data) => {
            window.atm.reset();
            placeholder = data[2];
            subdata = data[1];
            type = data[0];            

            if (type === 1) SelectViews = "Menu";
            else if (type === 2) SelectViews = "Input";
            else if (type === 3) SelectViews = "Business";
        },
        reset: () => {
            subdata = [];
            type = 1;
            SelectViews = "Menu";
        }
    }

    const onSelectMain = (index) => {
        activeMain = index;

        executeClient("atmCB", type, index);
    }
</script>

<div class="rd-body-inventory-u">
    <div class="module_atm page">
        <div class="banner">
            <div class="head">
                <div class="title">
                    <div>
                        {translateText('player', 'ATM')} <span class="bold">ATM</span>
                    </div>
                    <span class="logo" />
                </div>
                <p>
                    {translateText(
                        'player',
                        'The fastest and most reliable “ATM” machines work 24/7 and are located all across the state!'
                    )}
                </p>
                <div class="prevButton">
                    {translateText('player', 'No fee')}
                </div>
            </div>
        </div>
        <div class="cont">
            <ul class="info_atm">
                <li id="number">
                    <span class="ib bank-card"></span>
                    <span class="info_head">{translateText('player', 'Account number')}</span>
                    <span class="info_val">{number}</span>
                </li>
                <li id="holder">
                    <span class="ib bank-user"></span>
                    <span class="info_head">{translateText('player', 'Account holder')}</span>
                    <span class="info_val">{holder}</span>
                </li>
                <li id="balance">
                    <span class="ib bank-fill"></span>
                    <span class="info_head">{translateText('player', 'Bank account balance')}</span>
                    <span class="info_val">{format("money", $charBankMoney)}$</span>
                </li>
            </ul>
            <svelte:component
                this={Views[SelectViews]}
                {menuItem}
                {type}
                {subdata}
                {activeMain}
                {placeholder}
                {onSelectMain}
            />
        </div>
    </div>
</div>
