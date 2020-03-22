<template>
    <Component
        :is="tag ? tag : tabByTypo[typo]"
        :class="typoClass"
        class="WText"
    >
        <slot />
    </Component>
</template>

<script>
import VueTypes from 'vue-types'

const fontSizes = [8, 10, 12, 14, 16, 20, 24, 30, 36, 48, 60]
const typos = ['h1', 'h2', 'h3', 'h4', 'h5', 'h6', 'body', 'p', 'span']

export default {
    name: 'WText',
    props: {
        typo: VueTypes.oneOf(typos).def('p'),
        tag: VueTypes.oneOf(['p', 'h1', 'h2', 'h3', 'h4', 'h5', 'h6', 'span', 'label']).optional,
        color: VueTypes.oneOf(
            [
                'primary',
                'secondary',
                'white',
                'black',
                'yellow',
                'red',
                'grey01',
                'grey02',
                'grey03',
                'grey04',
                '',
            ],
        ).optional,
        align: VueTypes.oneOf(['left', 'center', 'right', '']).def('left'),
        size: VueTypes.oneOf([...fontSizes, ...fontSizes.map(String)]).optional,
        weight: VueTypes.oneOf(['light', 'medium', 'semi', 'bold', '']).def(''),
        capitalize: VueTypes.bool.def(false),
        uppercase: VueTypes.bool.def(false),
        underline: VueTypes.bool.def(false),
        italic: VueTypes.bool.def(false),
        ellipsis: VueTypes.bool.def(false),
    },
    data () {
        return {
            tabByTypo: {
                h1: 'h1',
                h2: 'h2',
                h3: 'h3',
                h4: 'h4',
                h5: 'h5',
                h6: 'h6',
                p: 'p',
                span: 'span',
                body: 'p',
            },
        }
    },
    computed: {
        typoClass () {
            return [
                this.typo,
                this.color,
                this.align,
                this.size ? `fs${this.size}` : undefined,
                this.weight,
                {
                    capitalize: this.capitalize,
                    uppercase: this.uppercase,
                    underline: this.underline,
                    italic: this.italic,
                    ellipsis: this.ellipsis,
                },
            ]
        },
    },
}
</script>

<style scoped lang="scss">
@import '@/theme/theme.scss';

.WText {
    &.p {
        color: $grey-01;
        font-family: $font-family-sans-serif;
        font-size: $font-size;
        font-weight: $font-weight-normal;
        line-height: 1.4;
    }

    &.span {
        color: $grey-01;
        font-family: $font-family-sans-serif;
        font-size: $font-size;
        font-weight: $font-weight-normal;
        line-height: 1.4;
    }

    &.h1,
    &.h2,
    &.h3,
    &.h4,
    &.h5,
    &.h6 {
        margin-bottom: $headings-margin-bottom;
        color: $black;
        font-family: $headings-font-family;
        font-weight: $headings-font-weight;
        line-height: 1.2;
    }

    &.h1 {
        font-size: 24px;
        line-height: 24px;
    }
    &.h2 {
        font-size: 18px;
    }
    &.h3 {
        font-size: 16px;
        line-height: 15px;
    }
    &.h4 {
        font-size: 14px;
    }
    &.h5 {
        font-size: 12px;
        letter-spacing: 1px;
    }
    &.h6 {
        letter-spacing: 1px;
        font-size: 10px;
    }

    &.p, &.span, &.label {
        $font-sizes: ('8', '10', '12', '14', '16', '18', '20', '24', '30', '36', '48', '60');
        @for $i from 0 to length($font-sizes) {
            $size: unquote(nth($font-sizes, $i+1));
            &.fs#{$size} {
                font-size: #{$size}px;
            }
        }
    }

	// Colors
    &.white {
        color: $white;
    }
    &.primary {
        color: $primary;
    }
    &.secondary {
        color: $secondary;
    }
    &.yellow {
        color: $warning;
    }
    &.red {
        color: $danger;
    }
    &.black {
        color: $black;
    }
    &.grey01 {
        color: $grey-01;
    }
    &.grey02 {
        color: $grey-02;
    }
	&.grey03 {
        color: $grey-03;
	}
	&.grey04 {
        color: $grey-04;
	}

	// Weight
    &.light {
        font-weight: $font-weight-light;
    }
    &.medium {
        font-weight: $font-weight-normal;
    }
    &.semi {
        font-weight: $font-weight-semibold;
    }
    &.bold {
        font-weight: $font-weight-bold;
    }

	// Align
    &.left {
        text-align: left;
    }
    &.center {
        text-align: center;
    }
    &.right {
        text-align: right;
    }

	// Other styling
    &.uppercase {
        text-transform: uppercase;
    }
    &.italic {
        font-style: italic;
    }
    &.underline {
        text-decoration: underline;
    }
    &.capitalize {
        text-transform: capitalize;
    }

    &.ellipsis {
        white-space: nowrap;
        overflow: hidden;
        text-overflow: ellipsis;
    }
}
</style>
