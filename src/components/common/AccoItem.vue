<template>
    <div class="box-acco-list" :class="type">
        <div
            v-for="(item, index) in list"
            :key="`acco-item-${index}`"
            :class="['box-acco-item', { active: index === currentIndex }]"
        >
            <button
                type="bubton"
                class="acco-anchor"
                :aria-controls="`acco-item-${index}`"
                :aria-expanded="index === currentIndex ? 'true' : 'false'"
                @click="onClick(index)"
            >
                <span
                    v-if="item.category"
                    class="category"
                    >{{ item.category }}</span
                >
                <strong class="tit">{{ item.title }}</strong>
            </button>
            <div :id="`acco-item-${index}`" class="acco-cont">
                <div class="acco-cont-inner">
                    {{ item.desc }}
                </div>
            </div>
        </div>
    </div>
</template>

<script lang="ts">
import { Component, Prop, Vue } from "vue-property-decorator";

export interface AccordionListItem {
    category?: string;
    title: string;
    desc: string;
}

@Component
export default class AccoItem extends Vue {
    @Prop({ type: Array, default: () => [], required: true })
    readonly list!: AccordionListItem[];

    @Prop({ type: String, default: "" })
    readonly type!: string;

    private currentIndex = -1;

    onClick(index: number) {
        this.currentIndex = this.currentIndex === index ? -1 : index;
    }
}
</script>

<style lang="scss" scoped src="./AccoItem.scss"></style>
