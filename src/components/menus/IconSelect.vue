<template>
    <v-menu offset-y v-model="menu">
        <template v-slot:activator="{ on, attrs }">
            <v-btn class="pa-0" text v-bind="attrs" v-on="on">
                <v-icon v-text="items[selected]"/>
                <v-icon :class="{'active': menu}">
                    mdi-menu-down
                </v-icon>
            </v-btn>
        </template>
        <v-sheet class="d-flex flex-column">
            <div v-for="(value, key) in items" :key="key">
                <v-btn text class="d-flex" @click="onClickItem(key)">
                    <v-icon v-text="value" class="mr-2"/>{{key}}
                </v-btn>
            </div>
            <slot/>
        </v-sheet>
    </v-menu>
</template>

<script>
    export default {
        props: {
            value: {
                type: String,
                default: () => {
                    return ""
                }
            },
            items: {
                type: Object,
                default: () => {
                    return {}
                }
            },
        },
        data: () => ({
            selected: null,
            menu: null
        }),
        created() {
            this.selected = this.value
        },
        methods: {
            onClickItem(key){
                this.selected = key
                this.$emit('input', key)
            }
        }
    }
</script>

<style lang="scss" scoped>
    .active {
        transform: rotate(-180deg)
    }
</style>
