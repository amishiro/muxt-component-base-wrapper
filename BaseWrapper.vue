<template>
  <component :is="tag" class="base-wrapper" :class="[addClassColor]">
    <div
      class="base-wrapper__inner"
      :class="[addClassSize, addClassPadding, addClassPaddingTop]"
    >
      <slot />
    </div>
  </component>
</template>

<script>
export default {
  props: {
    // 利用するタグ
    tag: {
      type: String,
      default: 'div',
    },

    // 背景色
    color: {
      type: String,
      default: undefined,
      validator(val) {
        return ['white'].includes(val)
      },
    },

    // 横幅のサイズ
    size: {
      type: String,
      default: 'medium',
      validator(val) {
        return ['full', 'large', 'medium', 'small'].includes(val)
      },
    },

    // 上下パディングのサイズ
    padding: {
      type: String,
      default: 'medium',
      validator(val) {
        return ['none', 'large', 'medium', 'small'].includes(val)
      },
    },

    // 上方のみパッディングのサイズ
    paddingTop: {
      type: String,
      default: undefined,
      validator(val) {
        return ['none', 'small'].includes(val)
      },
    },
  },

  computed: {
    /**
     * 背景色指定用のclassを生成
     * @returns {( String | undefined )} - class名 || undefinedを返す
     */
    addClassColor() {
      return this.color ? `is-color-${this.color}` : undefined
    },

    /**
     * 横幅のサイズ用のclassを生成
     * @returns {( String | undefined )} - class名 || undefinedを返す
     */
    addClassSize() {
      return this.size ? `is-size-${this.size}` : undefined
    },

    /**
     * 上下のpadding用のclassを生成
     * @returns {( String | undefined )} - class名 || undefinedを返す
     */
    addClassPadding() {
      return this.padding ? `is-padding-${this.padding}` : undefined
    },

    /**
     * 上のpadding用のclassを生成
     * @returns {( String | undefined )} - class名 || undefinedを返す
     */
    addClassPaddingTop() {
      return this.paddingTop ? `is-padding-top-${this.paddingTop}` : undefined
    },
  },
}
</script>

<style lang="scss" scoped>
//-------------------- ベースマージンの設定

// $gap: 8px; //ベースに8pxは計算しやすい
// $gap-s: $gap * 2; //16px
// $gap-m: $gap * 3; //24px
// $gap-l: $gap * 5; //40px
// $gap-xl: $gap * 8; //64px

//-------------------- 横幅の設定

// $width-xs: 320px; // iOSSE専用
// $width-s: 560px; // mobileサイズ最大
// $width-m: 800px; // tabletサイズ最大
// $width-l: 964px; // desktopサイズ最大
// $width-xl: 1160px; // メインビジュアルやヘッダフッタ用

//-------------------- breakpoint

// @mixin mobile-xs {
//   @media screen and (max-width: $width-xl) {
//     @content;
//   }
// }

// @mixin mobile {
//   @media screen and (max-width: $width-s) {
//     @content;
//   }
// }

// @mixin tablet {
//   @media screen and (min-width: $width-s + 1) {
//     @content;
//   }
// }

// @mixin tablet-only {
//   @media screen and (min-width: $width-s + 1) and (max-width: $width-m) {
//     @content;
//   }
// }

// @mixin desktop {
//   @media screen and (min-width: $width-m + 1) {
//     @content;
//   }
// }

.base-wrapper {
  // 背景色指定
  &.is-color-white {
    background-color: white;
  }

  // .base-wrapper__inner

  &__inner {
    // 横幅のサイズ
    width: 100%;
    &:not(.is-size-full) {
      padding-right: $gap-m;
      padding-left: $gap-m;
      @include tablet {
        padding-right: $gap-l;
        padding-left: $gap-l;
      }
      @include desktop {
        margin-right: auto;
        margin-left: auto;

        &.is-size-small {
          max-width: $width-m;
        }

        &.is-size-medium {
          max-width: $width-l;
        }

        &.is-size-large {
          max-width: $width-xl;
        }
      }
    }

    // 上下のpadding
    &.is-padding {
      // .is-padding-none
      &-none {
        padding-top: none;
        padding-bottom: none;
      }
      
      // .is-padding-large
      &-large {
        padding-top: $gap-xl;
        padding-bottom: $gap-xl;
      }
      
      // .is-padding-medium
      &-medium {
        padding-top: $gap-xl;
        padding-bottom: $gap-xl;
      }
      
      // .is-padding-small
      &-small {
        padding-top: $gap-s;
        padding-bottom: $gap-s;
      }
    }

    // 上方のみpadding関連
    &.is-padding-top {
    
      // .is-padding-top-none
      &-none {
        padding-top: none;
      }
      
      // .is-padding-top-small
      &-small {
        padding-top: $gap-s;
      }
    }
  }
}
</style>
