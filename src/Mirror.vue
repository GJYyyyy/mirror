<template>
    <div class="mirror">
        <div class="content">
            <slot></slot>
        </div>
        <div class="mirror-entity"
            :style="`--endPoint:${_endPoint};--blur:${_blur};--opacity:${_opacity};--dropShadowColor:${dropShadowColor};--dropShadowOffsetX:${_dropShadowOffsetX};--dropShadowOffsetY:${_dropShadowOffsetY};`">
            <slot></slot>
        </div>
    </div>
</template>

<script>
export default {
    name: 'Mirror',
    props: {
        endPoint: {
            type: Number,
            default: 0.4,
        },
        blur: {
            type: Number,
            default: 1,
        },
        opacity: {
            type: Number,
            default: 0.5
        },
        dropShadowColor: {
            type: String,
            default: 'black',
        },
        dropShadowOffsetX: {
            type: Number,
            default: 0,
        },
        dropShadowOffsetY: {
            type: Number,
            default: 0,
        },
    },
    computed: {
        _endPoint() {
            let num = this.endPoint;
            if (this.endPoint < 0) num = 0;
            if (this.endPoint > 1) num = 1;
            return `${num * 100}%`;
        },
        _blur() {
            let num = this.blur;
            if (this.blur < 0) num = 0;
            return `${num}px`;
        },
        _opacity() {
            let num = this.opacity;
            if (this.opacity < 0) num = 0;
            if (this.opacity > 1) num = 1;
            return num;
        },
        _dropShadowOffsetX() {
            let num = this.dropShadowOffsetX;
            if (this.dropShadowOffsetX < 0) num = 0;
            return `${num}px`;
        },
        _dropShadowOffsetY() {
            let num = this.dropShadowOffsetY;
            if (this.dropShadowOffsetY < 0) num = 0;
            return `${num}px`;
        },
    }
}
</script>

<style scoped>
.mirror {
    position: relative;
}

.mirror>.content {}

.mirror>.mirror-entity {
    position: absolute;
    top: 100%;
    left: 0%;
    width: 100%;
    height: 100%;
    transform: rotateZ(180deg) rotateY(180deg);
    mask: linear-gradient(to top, white 0%, transparent var(--endPoint)) center/100% 100%;
    filter: drop-shadow(var(--dropShadowOffsetX) var(--dropShadowOffsetY) var(--dropShadowColor)) blur(var(--blur));
    opacity: var(--opacity);
    pointer-events: none;
}
</style>