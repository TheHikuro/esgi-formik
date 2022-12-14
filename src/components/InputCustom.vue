<script>
export default {
    name: "Field",
    props: {
        as: { type: [Object, String], required: true },
        name: { type: String, required: true },
    },
    inject: ["formik"],
    methods: {
        isSpecialInput() {
            if (this.as == "textarea" || this.as == "select")
                return true;
            return false;
        },
        isCheckbox() {
            if (this.as == "checkbox") return true;
            return false;
        },
        isSelect() {
            if (this.as == "select") return true;
            return false;
        },
        hasValue() {
            if (this.as == "select" || this.as == "checkbox")
                return false;
            return true;
        },
        createElementFromVNode(vnode, createElement, fieldValue) {
            let children = [];
            let elementConf = {
                domProps: {
                    name: this.name,
                    value: vnode.data.attrs.value
                },
            };
            // Put only inner text as children
            // todo : recursive dom element
            if (vnode.children.length > 0 && !vnode.children[0].tag) {
                children.push(vnode.children[0].text);
            }
            if (vnode.data.staticClass) elementConf.class = vnode.data.staticClass;
            if (vnode.componentOptions) elementConf.on = (vnode.componentOptions.listeners || {});
            if (vnode.data.attrs.value == fieldValue) elementConf.domProps.selected = true;
            return createElement(vnode.tag, elementConf, children);
        }
    },
    render(createElement) {
        const { values, change } = this.formik;
        const fieldValue = get(values, this.name);
        let elementConf = {
            domProps: {
                name: this.name
            },
            on: {
                input: change
            }
        };
        let children = [];
        if (this.$slots.default) {
            children = this.$slots.default.map(vnode => {
                return this.createElementFromVNode(vnode, createElement, fieldValue);
            });
        }
        if (!this.isSpecialInput()) elementConf.domProps.type = this.as;
        if (this.isCheckbox()) elementConf.domProps.checked = !!fieldValue;
        if (this.hasValue()) elementConf.domProps.value = fieldValue;
        return createElement(
            this.isSpecialInput() ? this.as : "input",
            elementConf,
            children
        );
    }
};
</script>
