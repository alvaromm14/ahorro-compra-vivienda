<script>
    export let xScale;
    export let yScale;
    export let hoveredDate;
    export let data;
    export let innerWidth;

    const getYValue = (date) =>
        data.filter((d) => d.Fecha >= date)[0]?.Esfuerzo

</script>

<circle
    cx={xScale(hoveredDate)}
    cy={yScale(getYValue(hoveredDate))}
    r="5"
    fill="steelblue"
    stroke="white"
    pointer-events="none"
/>

<text
    x={xScale(hoveredDate) + 55 > innerWidth ? xScale(hoveredDate) - 16 : xScale(hoveredDate)}
    dx="8"
    y={yScale(getYValue(hoveredDate))}
    pointer-events="none"
    fill="steelblue"
    stroke="white"
    stroke-width="3"
    paint-order="stroke"
    text-anchor={xScale(hoveredDate) + 55 > innerWidth ? "end" : "start"}
    dominant-baseline="middle"
    font-weight="600"
    font-size="12px"
>
    <tspan class="dato">
        {Math.round(getYValue(hoveredDate)).toString().replace(/\B(?=(\d{3})+(?!\d))/g, ".") + " años"}
    </tspan>
    <tspan class="fecha"
        x={xScale(hoveredDate) + 55 > innerWidth ? xScale(hoveredDate) - 10 : xScale(hoveredDate) + 8} dy="1.1em">
        ({new Date(hoveredDate).toLocaleString('default', { year: 'numeric' })})
    </tspan>
</text>

<style>

    .dato {
        font-size: 0.9rem;
    }
    .fecha {
        fill:black;
        font-weight: 400;
        font-size: 0.8rem;
    }
</style>

