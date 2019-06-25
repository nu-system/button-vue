<template>
    <component
            :is="attr.is"
            v-bind="{ ...$attrs, ...attr }"
            v-on="$listeners">
        <span><slot/></span>
    </component>
</template>

<script>
    const _classMap = {
        baseClass: "nu_btn",
        default: "_default",
        primary: "_primary",
        secondary: "_secondary",
        warning: "_warning",
        success: "_success",
        danger: "_danger",
        fill: "_fill",
        ghost: "_ghost",
        link: "_link",
        disabled: "_disabled",
        loading: "_loading",
        large: "_large",
        middle: "_middle",
        small: "_small",
        capsule: "_capsule",
        block: "_block",
    };

    export default {
        name: "NuButton",
        props: {
            color: {
                type: String,
                default: 'default',
                validator: function (value) {
                    // 这个值必须匹配下列字符串中的一个
                    return ['default', 'primary', 'secondary', 'success', 'warning', 'danger'].indexOf(value) !== -1
                }
            },
            primary: Boolean,
            secondary: Boolean,
            warning: Boolean,
            success: Boolean,
            danger: Boolean,
            variant: {
                type: String,
                default: 'fill',
                validator: function (value) {
                    // 这个值必须匹配下列字符串中的一个
                    return ['fill', 'ghost', 'link'].indexOf(value) !== -1
                }
            },
            fill: Boolean,
            ghost: Boolean,
            link: Boolean,
            large: Boolean,
            middle: Boolean,
            small: Boolean,
            capsule: Boolean,
            block: Boolean,
            disabled: Boolean,
            loading: Boolean,
        },
        computed: {
            attr() {
                // 取出所有属性
                const {
                    color,
                    primary,
                    secondary,
                    warning,
                    success,
                    danger,
                    /* variant */
                    variant,
                    fill,
                    link,
                    ghost,
                    /* size */
                    large,
                    middle,
                    small,
                    /* others */
                    capsule,
                    block,
                    disabled,
                    loading,
                } = this;

                const classObjects = {
                    [_classMap.baseClass]: true,
                    [_classMap.primary]: primary,
                    [_classMap.secondary]: secondary,
                    [_classMap.warning]: warning,
                    [_classMap.success]: success,
                    [_classMap.danger]: danger,
                    [_classMap.large]: large,
                    [_classMap.middle]: middle,
                    [_classMap.small]: small,
                    [_classMap.disabled]: disabled,
                    [_classMap.loading]: loading,
                    [_classMap.ghost]: ghost,
                    [_classMap.capsule]: capsule,
                    [_classMap.link]: link,
                    [_classMap.block]: block,
                    [_classMap.fill]: fill,
                    // 设置默认颜色
                    [_classMap[color]]: !primary && !secondary && !warning && !success && !danger,
                    // 设置默认变体
                    [_classMap[variant]]: !fill && !ghost && !link
                };

                const attr = {
                    class: classObjects
                };

                // 当有 href 属性当时候表示这个按钮是个 a 标签
                if (this.$attrs.href) {
                    attr.is = "a";
                } else {
                    attr.disabled = disabled;
                    attr.type = "button";
                    attr.is = "button";
                }
                return attr;
            }
        }
    };
</script>
