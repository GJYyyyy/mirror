<template>
    <div class="mirror">
        <div class="content">
            <slot></slot>
        </div>
        <div class="mirror-entity" :class="{ gradient: gradient, 'drop-shadow': dropShadow }"
            :style="`--gradientPoint:${_gradientPoint};--blur:${_blur};--opacity:${_opacity};--gap:${_gap};--dropShadowColor:${dropShadowColor};--dropShadowOffsetX:${_dropShadowOffsetX};--dropShadowOffsetY:${_dropShadowOffsetY};`">
            <slot></slot>
        </div>
    </div>
</template>

<script>
export default {
    name: "Mirror",
    props: {
        gradient: {
            type: Boolean,
            default: true,
        },
        gradientPoint: {
            type: Number,
            default: 0.4,
        },
        blur: {
            type: Number,
            default: 1,
        },
        opacity: {
            type: Number,
            default: 0.5,
        },
        gap: {
            type: Number,
            default: 0,
        },
        dropShadow: {
            type: Boolean,
            default: false,
        },
        dropShadowColor: {
            type: String,
            default: "black",
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
        _gradientPoint() {
            let num = this.gradientPoint;
            if (this.gradientPoint < 0) num = 0;
            if (this.gradientPoint > 1) num = 1;
            return `${num * 100}%`;
        },
        _blur() {
            let num = this.blur;
            if (this.blur < 0) num = 0;
            return `${num}px`;
        },
        _gap() {
            let num = this.gap;
            if (this.gap < 0) num = 0;
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
    },
};
</script>

<style scoped>
.mirror {
    position: relative;
}

.mirror>.content {}

.mirror>.mirror-entity {
    position: absolute;
    top: calc(100% + var(--gap));
    left: 0%;
    width: 100%;
    height: 100%;
    transform: rotateZ(180deg) rotateY(180deg);
    pointer-events: none;
    opacity: var(--opacity);
    filter: blur(var(--blur));
}

.mirror>.mirror-entity.gradient {
    mask: linear-gradient(to top, white 0%, transparent var(--gradientPoint)) center/100% 100%;
}

.mirror>.mirror-entity.drop-shadow {
    filter: drop-shadow(var(--dropShadowOffsetX) var(--dropShadowOffsetY) var(--dropShadowColor)) blur(var(--blur));
}
</style>