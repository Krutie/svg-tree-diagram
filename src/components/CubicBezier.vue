<template>
    <g>
        <text :x="xPosition" :y="bottomHeight + 60">
            {{ item }}
        </text>

        <path
            :d="
                'M' +
                    halfSize +
                    ',' +
                    (topHeight + radius) +
                    ' ' +
                    'C' +
                    halfSize +
                    ',' +
                    halfSize +
                    ' ' +
                    xPosition +
                    ',' +
                    halfSize +
                    ' ' +
                    xPosition +
                    ',' +
                    bottomHeight
            "
        />
        <circle fill="#FFC107" r="10" :cx="xPosition" :cy="bottomHeight + 15">
        </circle>
    </g>
</template>
<script>
export default {
    props: [
        "index",
        "halfSize",
        "topHeight",
        "bottomHeight",
        "radius",
        "distance",
        "item"
    ],
    computed: {
        xPosition() {
            return this.distance * this.index + this.distance * 0.5
        }
    }
}
</script>
