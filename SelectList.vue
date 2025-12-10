<template>
  <!-- S: Dropdown 유형 1, 2, 3 -->
  <div
    v-if="!typeImg"
    class="sc-list sc-select__list mark"
    :class="typeOverflow ? '' : 'full'"
  >
    <div class="select-list__group">
      <div
        v-for="(item, i) in items"
        :key="`check-${i}`"
        class="select-list__item"
      >
        <BasicCard
          class="select-card select-card__check"
          variant="solid"
          :disabled="item.disabled"
          @contentClick="toggleMark(item)"
          :selected="setMark(item)"
        >
          <ListItem
            class="select-cardlist__item"
            align="centered"
            label-orientation="column"
            :left="{
              mainText: item.main,
              subText: item.sub,
              direction: 'column',
            }"
            :class="{ 'disabled-item': item.disabled }"
          >
            <template #leftIcon>
              <ScIcon
                v-if="item.iconName"
                :iconName="item.iconName"
                :size="iconSize"
              />
              <img
                v-else-if="item.image"
                :src="item.image"
                class="symbol-thumb"
                alt=""
              />
            </template>
            <template #rightControl>
              <div v-if="item.rightText">
                <div class="sv-list__text__main__body-m">
                  {{ item.rightText }}
                </div>
              </div>
              <Checkbox
                v-else
                :value="item.value"
                :disabled="item.disabled"
                variant="mark"
                align="left"
                class="select-card__checkbox"
                :model-value="setMark(item)"
                @update:model-value="onMark(item.value, $event)"
                @click.stop
              >
                <template #label></template>
              </Checkbox>
            </template>
          </ListItem>
          <div
            v-if="item.metaLeft || item.metaRight"
            class="select-cardlist__foot"
          >
            <ListItem
              :right="{
                mainText: item.metaRight,
                subText: item.metaLeft,
                direction: 'row-reverse',
              }"
            />
          </div>
        </BasicCard>
      </div>
    </div>
  </div>
  <!-- E: Dropdown 유형 1, 2, 3 -->
  <!-- S: Dropdown 유형 4, 4-1 -->
  <div v-else-if="typeImg" class="sc-select__list min-h-130">
    <div class="select-list__group select-list__image">
      <SelectBoxGroup
        v-bind="selectedValue"
        :items="items"
        orientation="vertical"
        variant="outline"
        as="div"
      >
        <template #contents="{ item }">
          <ListItem
            :left="{
              mainText: item.main,
              subText: item.sub,
            }"
            :class="{ 'disabled-item': item.disabled }"
          >
            <template #leftIcon>
              <img
                v-if="item.image"
                :src="item.image"
                :alt="item.main"
                class="thumb"
              />
              <Icon v-else name="sample-icon" :size="24" aria-hidden="true" />
            </template>
            <template #leftSubText v-if="item.disabled && item.showWarning">
              <div class="sub-icon__text">
                <Icon name="Circle_alert" :size="16" class="sub-icon" />
                <span class="sub-text">{{ item.subIconText }}</span>
              </div>
            </template>
          </ListItem>
        </template>
      </SelectBoxGroup>
    </div>
  </div>
  <!-- E: Dropdown 유형 4, 4-1 -->
</template>

<script setup>
import { ScIcon } from "@shc-nss/ui/shc";
import {
  BasicCard,
  Checkbox,
  Icon,
  ListItem,
  SelectBoxGroup,
} from "@shc-nss/ui/solid";
import { ref } from "vue";

const marks = ref("");
function onMark(value, checked) {
  if (checked) {
    marks.value = value;
  } else if (marks.value === value) {
    marks.value = null;
  }
}
function toggleMark(item) {
  if (item?.disabled) return;
  if (marks.value === item.value) {
    return;
  }
  marks.value = item.value;
}
function setMark(item) {
  if (marks.value == "" && item.selected) {
    return item.selected;
  } else if (marks.value !== null && marks.value !== "") {
    return marks.value === item.value;
  }
  return false;
}

const props = defineProps({
  items: {
    type: Array,
  },
  // 유형 2
  typeOverflow: {
    type: Boolean,
    default: false,
  },
  // 유형 4, 4-1
  typeImg: {
    type: Boolean,
    default: false,
  },
  selectedValue: {
    type: Boolean,
    default: false,
  },
  iconSize: {
    type: Number,
    default: 28,
  },
});
</script>
