<script lang="ts">
    import { formatDollars } from '../utils/strings'
    import { tweened } from 'svelte/motion'
    import { PaperTradingUtils } from '../logic/game'
    import { numberEasingProps } from '../logic/utils'
    import PriceMovementBadge from './PriceMovementBadge.svelte'
    import StockChart from './StockChart.svelte'

    export let priceData: number[] = []
    export let tick = priceData.length - 1
    export let holdsPosition = false
    let cl: string
    export { cl as class }

    $: beanPriceMovementPercentage = PaperTradingUtils.priceMovementPercentage({ priceData, tick })

    const animatedTickerPrice = tweened(priceData[tick], numberEasingProps)
    $:  {
        animatedTickerPrice.set(priceData[tick])
    }
</script>
<div
        class="self-stretch flex flex-col -m-1 {cl} {holdsPosition ? 'bg-gradient-to-b' : undefined } from-yellow-50 to-white rounded px-1">
    <span class='font-semibold text-gray-500'>$APPLE</span>
    <div class="flex items-start">
        <span class='font-semibold text-4xl tabular-nums'>${formatDollars($animatedTickerPrice)}</span>
        <PriceMovementBadge delta={beanPriceMovementPercentage} class='mt-1'/>
    </div>

    <StockChart {priceData} {tick} {holdsPosition} class=""/>
</div>