<script>
    import { selectChar } from './../store.js';
    import { format } from 'api/formatter'
    import fraction from 'json/fraction.js'

    import Spawn from './spawn.svelte'
</script>

<Spawn {...$selectChar.Data} isBan={$selectChar.ban} />

<div class="auth__stats">
    <div class="auth__stat">
        <div class="gray">Cash on hand</div>
        <div>${format("money", $selectChar.Data.Money)}</div>
    </div>
    <div class="auth__stat">
        <div class="gray">Money in bank</div>
        <div>${format("money", $selectChar.Data.BankMoney)}</div>
    </div>
    <div class="auth__stat">
        <div class="gray">Faction</div>
        <div>{fraction[$selectChar.Data.FractionID]}</div>
    </div>
    {#if $selectChar.ban && $selectChar.ban.Reason}
        <div class="auth__stat">
            <div class="gray">Reason</div>
            <div>{$selectChar.ban.Reason}</div>
        </div>
        <div class="auth__stat">
            <div class="gray">Banned by</div>
            <div>{$selectChar.ban.Admin}</div>
        </div>
        <div class="auth__stat">
            <div class="gray">Ban date</div>
            <div>{$selectChar.ban.Time}</div>
        </div>
        <div class="auth__stat">
            <div class="gray">Unban date</div>
            <div>{$selectChar.ban.Until}</div>
        </div>
    {/if}
</div>
