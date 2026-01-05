
{% raw %}
```js

<route lang="yaml">
meta:
  id: SSN016A01
  title: 약관동의
  menu: Sign in/up > 약관동의(카드회원)
  layout: SubLayout
  category: Sign in/up
  publish: 김대민
  publishVersion: 0.8
  status: 재작업
  etc: |
    260105: 디자인 동기화 - 약관 체크항목 추가,
    안심 color 변경 blue에서 color=cyan,
    [251027] 마이데이터 서비스 안내 하단 링크 추가
  header:
    fixed: true
    close: true
</route>
<template>
  <!-- 콘텐츠 영역 -->
  <div class="sc-contents__body sc-agree__page">
    <section class="section">
      <div class="sc-agree__list compound" role="region">
        <div class="agree-list__group">
          <div
            class="agree-item item-basic"
            :class="{ 'is-checked': basicAgree4 }"
          >
            <Checkbox
              v-model="basicAgree4"
              class="agree-item__checkbox item-checkbox__basic"
              variant="box"
              align="left"
            >
              <template #label>
                <span class="agree-item__label item-label__basic">{{
                  basicItem4.label
                }}</span>
              </template>
            </Checkbox>
          </div>

          <!-- ======================================== -->
          <!-- 1뎁스 영역: 기본 약관 항목들 -->
          <!-- ======================================== -->
          <div class="agree-sublist" role="group">
            <div
              v-for="item in subItems4"
              :key="item.value"
              class="agree-subitem"
              :class="{ 'agree-subitem__accordion': Boolean(item.accordion) }"
            >
              <template v-if="item.accordion">
                <SolidListAccordion
                  class="agree-subitem__accordion"
                  :rowClickable="false"
                  :value="item.value"
                  v-model:isExpanded="subAccordionState4[item.value]"
                >
                  <template #title>
                    <div
                      class="agree-item agree-item__sub"
                      :class="{
                        'is-checked': subAgrees4.includes(item.value),
                      }"
                    >
                      <Checkbox
                        :value="item.value"
                        variant="box"
                        align="left"
                        :model-value="subAgrees4.includes(item.value)"
                        class="agree-item__checkbox item-checkbox__sub"
                        @update:model-value="onToggleSub4(item.value, $event)"
                        @click.stop
                      >
                        <template #label>
                          <span class="agree-item__label item-label__sub">{{
                            item.label
                          }}</span>
                        </template>
                      </Checkbox>
                    </div>
                  </template>
                  <div class="agree-subitem__panel">
                    <div v-if="item.value === 's4-1'" class="agree-depth">
                      <!-- ======================================== -->
                      <!-- 2뎁스 영역: 서비스 이용약관 -->
                      <!-- ======================================== -->
                      <ul class="agree-sublist agree-sublist__depth2">
                        <li
                          v-for="depth2Item in subItemsDepth2_s4_1"
                          :key="depth2Item.value"
                          class="agree-subitem agree-subitem__depth2"
                        >
                          <!-- 아코디언이 있는 항목 -->
                          <template v-if="depth2Item.accordion">
                            <SolidListAccordion
                              class="agree-subitem__accordion accordion-depth2"
                              :rowClickable="false"
                              :value="depth2Item.value"
                              v-model:isExpanded="
                                subAccordionState4[depth2Item.value]
                              "
                            >
                              <template #title>
                                <div class="agree-item agree-item__sub">
                                  <Checkbox
                                    :value="depth2Item.value"
                                    variant="mark"
                                    align="left"
                                    :model-value="
                                      subAgrees4.includes(depth2Item.value)
                                    "
                                    class="agree-item__checkbox item-checkbox__sub"
                                    @update:model-value="
                                      onToggleSub4(depth2Item.value, $event)
                                    "
                                    @click.stop
                                  >
                                    <template #label>
                                      <span
                                        class="agree-item__label item-label__sub"
                                        >{{ depth2Item.label }}</span
                                      >
                                    </template>
                                  </Checkbox>
                                </div>
                              </template>
                              <div class="agree-subitem__panel">
                                <!-- 3뎁스 영역: 위치기반 서비스 약관동의 -->
                                <div v-if="depth2Item.value === 's4-1-4'">
                                  <ul
                                    class="agree-sublist agree-sublist__depth3"
                                  >
                                    <li
                                      v-for="depth3Item in subItemsDepth3_s4_1_4"
                                      :key="depth3Item.value"
                                      class="agree-subitem agree-subitem__depth3"
                                    >
                                      <!-- 아코디언이 있는 3뎁스 항목 -->
                                      <template v-if="depth3Item.accordion">
                                        <SolidListAccordion
                                          class="agree-subitem__accordion accordion-depth3"
                                          :rowClickable="false"
                                          :value="depth3Item.value"
                                          v-model:isExpanded="
                                            subAccordionState4[depth3Item.value]
                                          "
                                        >
                                          <template #title>
                                            <div
                                              class="agree-item agree-item__sub"
                                            >
                                              <Checkbox
                                                :value="depth3Item.value"
                                                variant="mark"
                                                align="left"
                                                :model-value="
                                                  subAgrees4.includes(
                                                    depth3Item.value
                                                  )
                                                "
                                                class="agree-item__checkbox item-checkbox__sub"
                                                @update:model-value="
                                                  onToggleSub4(
                                                    depth3Item.value,
                                                    $event
                                                  )
                                                "
                                                @click.stop
                                              >
                                                <template #label>
                                                  <span
                                                    class="agree-item__label item-label__sub"
                                                    >{{
                                                      depth3Item.label
                                                    }}</span
                                                  >
                                                </template>
                                              </Checkbox>
                                            </div>
                                          </template>
                                          <div class="agree-subitem__panel">
                                            <!-- 4뎁스 영역: 위치정보 서비스 동의사항 상세 -->
                                            <div
                                              v-if="
                                                depth3Item.value === 's4-1-4-2'
                                              "
                                              class="outline-panel"
                                            >
                                              <Card
                                                variant="solid"
                                                color="gray"
                                                class="agree-details"
                                              >
                                                <ul
                                                  class="agree-sublist"
                                                  role="group"
                                                >
                                                  <li
                                                    v-for="depth4Item in subItemsDepth4_s4_1_4_2"
                                                    :key="depth4Item.value"
                                                    class="agree-subitem agree-subitem__depth4"
                                                  >
                                                    <div
                                                      class="agree-item agree-item__sub"
                                                    >
                                                      <Checkbox
                                                        :value="
                                                          depth4Item.value
                                                        "
                                                        variant="mark"
                                                        align="left"
                                                        :model-value="
                                                          subAgrees4.includes(
                                                            depth4Item.value
                                                          )
                                                        "
                                                        class="agree-item__checkbox item-checkbox__sub"
                                                        @update:model-value="
                                                          onToggleSub4(
                                                            depth4Item.value,
                                                            $event
                                                          )
                                                        "
                                                        @click.stop
                                                      >
                                                        <template #label>
                                                          <span
                                                            class="agree-item__label item-label__sub"
                                                            >{{
                                                              depth4Item.label
                                                            }}</span
                                                          >
                                                        </template>
                                                      </Checkbox>
                                                      <IconButton
                                                        iconName="Chevron_right"
                                                        size="small"
                                                        :aria-label="`${depth4Item.label} 상세 보기`"
                                                        class="agree-subitem__trigger"
                                                      />
                                                    </div>
                                                  </li>
                                                </ul>
                                              </Card>
                                            </div>
                                          </div>
                                        </SolidListAccordion>
                                      </template>

                                      <!-- 일반 3뎁스 항목 -->
                                      <div
                                        v-else
                                        class="agree-item agree-item__sub"
                                      >
                                        <Checkbox
                                          :value="depth3Item.value"
                                          variant="mark"
                                          align="left"
                                          :model-value="
                                            subAgrees4.includes(
                                              depth3Item.value
                                            )
                                          "
                                          class="agree-item__checkbox item-checkbox__sub"
                                          @update:model-value="
                                            onToggleSub4(
                                              depth3Item.value,
                                              $event
                                            )
                                          "
                                          @click.stop
                                        >
                                          <template #label>
                                            <span
                                              class="agree-item__label item-label__sub"
                                              >{{ depth3Item.label }}</span
                                            >
                                          </template>
                                        </Checkbox>
                                        <IconButton
                                          iconName="Chevron_right"
                                          size="small"
                                          :aria-label="`${depth3Item.label} 상세 보기`"
                                          class="agree-subitem__trigger"
                                        />
                                      </div>
                                    </li>
                                  </ul>
                                </div>

                                <!-- 3뎁스 영역: 앱(APP) 알림 수신동의 -->
                                <div v-else-if="depth2Item.value === 's4-1-5'">
                                  <ul
                                    class="agree-sublist agree-sublist__depth3"
                                  >
                                    <li
                                      v-for="depth3Item in subItemsDepth3_s4_1_5"
                                      :key="depth3Item.value"
                                      class="agree-subitem agree-subitem__depth3"
                                    >
                                      <!-- 아코디언이 있는 3뎁스 항목 -->
                                      <template v-if="depth3Item.accordion">
                                        <SolidListAccordion
                                          class="agree-subitem__accordion accordion-depth3"
                                          :rowClickable="false"
                                          :value="depth3Item.value"
                                          v-model:isExpanded="
                                            subAccordionState4[depth3Item.value]
                                          "
                                        >
                                          <template #title>
                                            <div
                                              class="agree-item agree-item__sub"
                                            >
                                              <Checkbox
                                                :value="depth3Item.value"
                                                variant="mark"
                                                align="left"
                                                :model-value="
                                                  subAgrees4.includes(
                                                    depth3Item.value
                                                  )
                                                "
                                                class="agree-item__checkbox item-checkbox__sub"
                                                @update:model-value="
                                                  onToggleSub4(
                                                    depth3Item.value,
                                                    $event
                                                  )
                                                "
                                                @click.stop
                                              >
                                                <template #label>
                                                  <span
                                                    class="agree-item__label item-label__sub"
                                                    >{{
                                                      depth3Item.label
                                                    }}</span
                                                  >
                                                </template>
                                              </Checkbox>
                                            </div>
                                          </template>
                                          <div class="agree-subitem__panel">
                                            <!-- 4뎁스 영역: 마케팅 정보 수신동의 상세 -->
                                            <div
                                              v-if="
                                                depth3Item.value === 's4-1-5-1'
                                              "
                                              class="outline-panel"
                                            >
                                              <Card
                                                variant="solid"
                                                color="gray"
                                                class="agree-details"
                                              >
                                                <UnorderedList>
                                                  <UnorderedListItem
                                                    variant="bullet"
                                                    size="small"
                                                    text="항목 : 앱(APP)을 통한 마케팅 정보 수신동의"
                                                  />
                                                  <UnorderedListItem
                                                    variant="bullet"
                                                    size="small"
                                                    text="이용목적 : 각종 이벤트, 할인, 혜택정보 등의 안내"
                                                  />
                                                  <UnorderedListItem
                                                    variant="bullet"
                                                    size="small"
                                                    text="보유기간 : 별도 동의 철회시까지"
                                                  />
                                                </UnorderedList>
                                              </Card>
                                            </div>
                                          </div>
                                        </SolidListAccordion>
                                      </template>

                                      <!-- 일반 3뎁스 항목 -->
                                      <div
                                        v-else
                                        class="agree-item agree-item__sub"
                                      >
                                        <Checkbox
                                          :value="depth3Item.value"
                                          variant="mark"
                                          align="left"
                                          :model-value="
                                            subAgrees4.includes(
                                              depth3Item.value
                                            )
                                          "
                                          class="agree-item__checkbox item-checkbox__sub"
                                          @update:model-value="
                                            onToggleSub4(
                                              depth3Item.value,
                                              $event
                                            )
                                          "
                                          @click.stop
                                        >
                                          <template #label>
                                            <span
                                              class="agree-item__label item-label__sub"
                                              >{{ depth3Item.label }}</span
                                            >
                                          </template>
                                        </Checkbox>
                                        <IconButton
                                          iconName="Chevron_right"
                                          size="small"
                                          :aria-label="`${depth3Item.label} 상세 보기`"
                                          class="agree-subitem__trigger"
                                        />
                                      </div>
                                    </li>
                                  </ul>
                                </div>
                              </div>
                            </SolidListAccordion>
                          </template>

                          <!-- 일반 항목 -->
                          <div v-else class="agree-item agree-item__sub">
                            <Checkbox
                              :value="depth2Item.value"
                              variant="mark"
                              align="left"
                              :model-value="
                                subAgrees4.includes(depth2Item.value)
                              "
                              class="agree-item__checkbox item-checkbox__sub"
                              @update:model-value="
                                onToggleSub4(depth2Item.value, $event)
                              "
                              @click.stop
                            >
                              <template #label>
                                <span
                                  class="agree-item__label item-label__sub"
                                  >{{ depth2Item.label }}</span
                                >
                              </template>
                            </Checkbox>
                            <IconButton
                              iconName="Chevron_right"
                              size="small"
                              :aria-label="`${depth2Item.label} 상세 보기`"
                              class="agree-subitem__trigger"
                            />
                          </div>
                        </li>
                      </ul>
                    </div>
                    <div v-else-if="item.value === 's4-2'" class="agree-depth">
                      <!-- ======================================== -->
                      <!-- 2뎁스 영역: 신한Pay머니 이용약관 -->
                      <!-- ======================================== -->
                      <ul class="agree-sublist agree-sublist__depth2">
                        <li
                          v-for="depth2Item in subItemsDepth2_s4_2"
                          :key="depth2Item.value"
                          class="agree-subitem agree-subitem__depth2"
                        >
                          <div class="agree-item agree-item__sub">
                            <Checkbox
                              :value="depth2Item.value"
                              variant="mark"
                              align="left"
                              :model-value="
                                subAgrees4.includes(depth2Item.value)
                              "
                              class="agree-item__checkbox item-checkbox__sub"
                              @update:model-value="
                                onToggleSub4(depth2Item.value, $event)
                              "
                              @click.stop
                            >
                              <template #label>
                                <span
                                  class="agree-item__label item-label__sub"
                                  >{{ depth2Item.label }}</span
                                >
                              </template>
                            </Checkbox>
                            <IconButton
                              iconName="Chevron_right"
                              size="small"
                              :aria-label="`${depth2Item.label} 상세 보기`"
                              class="agree-subitem__trigger"
                            />
                          </div>
                        </li>
                        <!-- 동의등급제 안내 -->
                        <li class="agree-subitem agree-subitem__depth2">
                          <Card
                            variant="solid"
                            color="gray"
                            class="agree-info__card card-white"
                          >
                            <div class="info-card__header">
                              <p class="info-card__title">동의등급제 안내</p>
                            </div>
                            <div class="info-card__content">
                              <div class="label-group">
                                <!-- [251016] 안심 color 변경 blue에서 color="cyan" -->
                                <!-- <SolidLabel
                                  color="blue"
                                  title="안심"
                                /> -->
                                <SolidLabel color="cyan" title="안심" />
                                <SolidLabel color="green" title="다소안심" />
                                <SolidLabel color="yellow" title="보통" />
                                <SolidLabel color="orange" title="신중" />
                                <SolidLabel color="red" title="주의" />
                              </div>
                              <UnorderedList>
                                <UnorderedListItem
                                  variant="bullet"
                                  size="small"
                                  text="동의등급제는 개인(신용) 선택적 동의 항목에 대해 사생활의 비밀과 자유를 침해할 위험, 이익이나 혜택, 등의 내용의 명확성 등을 고려하여 5가지 등급을 부여하는 제도입니다."
                                />
                              </UnorderedList>
                            </div>
                          </Card>
                        </li>
                        <!-- 동의등급제 안내 이후 추가 항목들 -->
                        <li
                          v-for="depth2Item in subItemsDepth2_s4_2_after"
                          :key="depth2Item.value"
                          class="agree-subitem agree-subitem__depth2"
                          :class="{
                            'agree-subitem__accordion': Boolean(
                              depth2Item.accordion
                            ),
                          }"
                        >
                          <!-- 아코디언이 있는 항목 -->
                          <template v-if="depth2Item.accordion">
                            <SolidListAccordion
                              class="agree-subitem__accordion accordion-depth2"
                              :rowClickable="false"
                              :value="depth2Item.value"
                              v-model:isExpanded="
                                subAccordionState4[depth2Item.value]
                              "
                            >
                              <template #title>
                                <div class="agree-item agree-item__sub">
                                  <Checkbox
                                    :value="depth2Item.value"
                                    variant="mark"
                                    align="left"
                                    :model-value="
                                      subAgrees4.includes(depth2Item.value)
                                    "
                                    class="agree-item__checkbox item-checkbox__sub"
                                    @update:model-value="
                                      onToggleSub4(depth2Item.value, $event)
                                    "
                                    @click.stop
                                  >
                                    <template #label>
                                      <span
                                        class="agree-item__label item-label__sub"
                                        >{{ depth2Item.label }}</span
                                      >
                                      <template v-if="depth2Item.grade">
                                        <br />
                                        <SolidLabel
                                          :color="depth2Item.grade"
                                          :title="
                                            depth2Item.grade === 'cyan'
                                              ? '안심'
                                              : depth2Item.grade === 'green'
                                                ? '다소안심'
                                                : depth2Item.grade === 'yellow'
                                                  ? '보통'
                                                  : depth2Item.grade ===
                                                      'orange'
                                                    ? '신중'
                                                    : '주의'
                                          "
                                          :aria-label="`동의등급제 ${
                                            depth2Item.grade === 'cyan'
                                              ? '안심'
                                              : depth2Item.grade === 'green'
                                                ? '다소안심'
                                                : depth2Item.grade === 'yellow'
                                                  ? '보통'
                                                  : depth2Item.grade ===
                                                      'orange'
                                                    ? '신중'
                                                    : '주의'
                                          }`"
                                        />
                                      </template>
                                    </template>
                                  </Checkbox>
                                </div>
                              </template>
                              <div class="agree-subitem__panel">
                                <!-- 3뎁스 영역: 카드 및 금융상품 ・ 서비스 안내 및 이용권유를 위한 수집 ・ 이용 -->
                                <div
                                  v-if="depth2Item.value === 's4-2-6'"
                                  class="agree-depth"
                                >
                                  <ul
                                    class="agree-sublist agree-sublist__depth3"
                                  >
                                    <li
                                      v-for="depth3Item in subItemsDepth3_s4_2_6"
                                      :key="depth3Item.value"
                                      class="agree-subitem agree-subitem__depth3"
                                    >
                                      <div class="agree-item agree-item__sub">
                                        <Checkbox
                                          :value="depth3Item.value"
                                          variant="mark"
                                          align="left"
                                          :model-value="
                                            subAgrees4.includes(
                                              depth3Item.value
                                            )
                                          "
                                          class="agree-item__checkbox item-checkbox__sub"
                                          @update:model-value="
                                            onToggleSub4(
                                              depth3Item.value,
                                              $event
                                            )
                                          "
                                          @click.stop
                                        >
                                          <template #label>
                                            <span
                                              class="agree-item__label item-label__sub"
                                              >{{ depth3Item.label }}</span
                                            >
                                          </template>
                                        </Checkbox>
                                      </div>
                                    </li>
                                  </ul>
                                  <!-- 자세히보기 링크 -->
                                  <div class="agree-depth__link">
                                    <TextButton
                                      class="agree-depth__link"
                                      color="secondary"
                                      size="small"
                                      text="자세히보기"
                                      showGoTo
                                    />
                                  </div>
                                </div>

                                <!-- 3뎁스 영역: 카드 및 금융상품 ・ 서비스 이외의 부수서비스 안내 등을 위한 수집 ・ 이용 -->
                                <template
                                  v-else-if="depth2Item.value === 's4-2-7'"
                                >
                                  <ul
                                    class="agree-sublist agree-sublist__depth3"
                                  >
                                    <li
                                      v-for="depth3Item in subItemsDepth3_s4_2_7"
                                      :key="depth3Item.value"
                                      class="agree-subitem agree-subitem__depth3"
                                    >
                                      <div class="agree-item agree-item__sub">
                                        <Checkbox
                                          :value="depth3Item.value"
                                          variant="mark"
                                          align="left"
                                          :model-value="
                                            subAgrees4.includes(
                                              depth3Item.value
                                            )
                                          "
                                          class="agree-item__checkbox item-checkbox__sub"
                                          @update:model-value="
                                            onToggleSub4(
                                              depth3Item.value,
                                              $event
                                            )
                                          "
                                          @click.stop
                                        >
                                          <template #label>
                                            <span
                                              class="agree-item__label item-label__sub"
                                              >{{ depth3Item.label }}</span
                                            >
                                          </template>
                                        </Checkbox>
                                      </div>
                                    </li>
                                  </ul>
                                  <!-- 자세히보기 링크 -->
                                  <div class="agree-depth__link">
                                    <TextButton
                                      class="agree-depth__link"
                                      color="secondary"
                                      size="small"
                                      text="자세히보기"
                                      showGoTo
                                    />
                                  </div>
                                </template>

                                <!-- 3뎁스 영역: 전자적 전송매체를 통한 광고성 정보 수신동의 -->
                                <div
                                  v-else-if="depth2Item.value === 's4-2-8'"
                                  class="agree-depth"
                                >
                                  <Card
                                    variant="solid"
                                    color="gray"
                                    class="agree-details"
                                  >
                                    <ul class="agree-sublist" role="group">
                                      <li
                                        v-for="depth3Item in subItemsDepth3_s4_2_8"
                                        :key="depth3Item.value"
                                        class="agree-subitem agree-subitem__depth3"
                                      >
                                        <div class="agree-item agree-item__sub">
                                          <Checkbox
                                            :value="depth3Item.value"
                                            variant="mark"
                                            align="left"
                                            :model-value="
                                              subAgrees4.includes(
                                                depth3Item.value
                                              )
                                            "
                                            class="agree-item__checkbox item-checkbox__sub"
                                            @update:model-value="
                                              onToggleSub4(
                                                depth3Item.value,
                                                $event
                                              )
                                            "
                                            @click.stop
                                          >
                                            <template #label>
                                              <span
                                                class="agree-item__label item-label__sub"
                                                >{{ depth3Item.label }}</span
                                              >
                                            </template>
                                          </Checkbox>
                                        </div>
                                      </li>
                                    </ul>
                                  </Card>
                                  <!-- 설명 텍스트 -->
                                  <UnorderedList class="mt-md mb-md">
                                    <UnorderedListItem
                                      variant="bullet"
                                      size="small"
                                      text="카드상품과 부수서비스의 안내 및 이용권유에 셨더라도 신용정보의 이용 및 보호에 관한 법률에 따라 이용권유 목적의 연락에 대한 중단을 언제라도 카드사에 요청할 수 있습니다. (대표전화 : 1544-7000 / 홈페이지 : www.shinhancard.com)"
                                    />
                                    <UnorderedListItem
                                      variant="bullet"
                                      size="small"
                                      text="갱신 및 상품서비스 변경 안내 등 필수 고지사항은 상기 동의 대상에서 제외됩니다."
                                    />
                                  </UnorderedList>
                                </div>

                                <!-- 3뎁스 영역: 카드 및 금융상품 ・ 서비스 안내 및 이용권유를 위한 수집 ・ 이용 (s4-2-9) -->
                                <div
                                  v-else-if="depth2Item.value === 's4-2-9'"
                                  class="agree-depth"
                                >
                                  <ul
                                    class="agree-sublist agree-sublist__depth3"
                                  >
                                    <li
                                      v-for="depth3Item in subItemsDepth3_s4_2_9"
                                      :key="depth3Item.value"
                                      class="agree-subitem agree-subitem__depth3"
                                    >
                                      <div class="agree-item agree-item__sub">
                                        <Checkbox
                                          :value="depth3Item.value"
                                          variant="mark"
                                          align="left"
                                          :model-value="
                                            subAgrees4.includes(
                                              depth3Item.value
                                            )
                                          "
                                          class="agree-item__checkbox item-checkbox__sub"
                                          @update:model-value="
                                            onToggleSub4(
                                              depth3Item.value,
                                              $event
                                            )
                                          "
                                          @click.stop
                                        >
                                          <template #label>
                                            <span
                                              class="agree-item__label item-label__sub"
                                              >{{ depth3Item.label }}</span
                                            >
                                          </template>
                                        </Checkbox>
                                      </div>
                                    </li>
                                  </ul>
                                  <!-- 자세히보기 링크 -->
                                  <div class="agree-depth__link">
                                    <TextButton
                                      class="agree-depth__link"
                                      color="secondary"
                                      size="small"
                                      text="자세히보기"
                                      showGoTo
                                    />
                                  </div>
                                </div>
                              </div>
                            </SolidListAccordion>
                          </template>

                          <!-- 일반 항목 -->
                          <div v-else class="agree-item agree-item__sub">
                            <Checkbox
                              :value="depth2Item.value"
                              variant="mark"
                              align="left"
                              :model-value="
                                subAgrees4.includes(depth2Item.value)
                              "
                              class="agree-item__checkbox item-checkbox__sub"
                              @update:model-value="
                                onToggleSub4(depth2Item.value, $event)
                              "
                              @click.stop
                            >
                              <template #label>
                                <span
                                  class="agree-item__label item-label__sub"
                                  >{{ depth2Item.label }}</span
                                >
                                <template v-if="depth2Item.grade">
                                  <br />
                                  <SolidLabel
                                    :color="depth2Item.grade"
                                    :title="
                                      depth2Item.grade === 'cyan'
                                        ? '안심'
                                        : depth2Item.grade === 'green'
                                          ? '다소안심'
                                          : depth2Item.grade === 'yellow'
                                            ? '보통'
                                            : depth2Item.grade === 'orange'
                                              ? '신중'
                                              : '주의'
                                    "
                                    :aria-label="`동의등급제 ${
                                      depth2Item.grade === 'cyan'
                                        ? '안심'
                                        : depth2Item.grade === 'green'
                                          ? '다소안심'
                                          : depth2Item.grade === 'yellow'
                                            ? '보통'
                                            : depth2Item.grade === 'orange'
                                              ? '신중'
                                              : '주의'
                                    }`"
                                  />
                                </template>
                              </template>
                            </Checkbox>
                            <IconButton
                              iconName="Chevron_right"
                              size="small"
                              :aria-label="`${depth2Item.label} 상세 보기`"
                              class="agree-subitem__trigger"
                            />
                          </div>
                          <!-- 서브텍스트: 회원 가입 및 발권신청 동의 -->
                          <div
                            v-if="depth2Item.value === 's4-2-10'"
                            class="agree-subitem padding-lg"
                          >
                            <p class="agree-subtext">
                              본인은 카드 실제 소유자와 동일하며, 위 기재된
                              사실과 다름이 없음을 확인하고 회원가입을
                              신청합니다.
                            </p>
                          </div>
                        </li>
                      </ul>
                    </div>
                    <div v-else-if="item.value === 's4-3'" class="agree-depth">
                      <!-- ======================================== -->
                      <!-- 2뎁스 영역: 온라인 회원 이용약관 -->
                      <!-- ======================================== -->
                      <ul class="agree-sublist agree-sublist__depth2">
                        <li
                          v-for="depth2Item in subItemsDepth2_s4_3"
                          :key="depth2Item.value"
                          class="agree-subitem agree-subitem__depth2"
                        >
                          <div class="agree-item agree-item__sub">
                            <Checkbox
                              :value="depth2Item.value"
                              variant="mark"
                              align="left"
                              :model-value="
                                subAgrees4.includes(depth2Item.value)
                              "
                              class="agree-item__checkbox item-checkbox__sub"
                              @update:model-value="
                                onToggleSub4(depth2Item.value, $event)
                              "
                              @click.stop
                            >
                              <template #label>
                                <span
                                  class="agree-item__label item-label__sub"
                                  >{{ depth2Item.label }}</span
                                >
                              </template>
                            </Checkbox>
                            <IconButton
                              iconName="Chevron_right"
                              size="small"
                              :aria-label="`${depth2Item.label} 상세 보기`"
                              class="agree-subitem__trigger"
                            />
                          </div>
                        </li>
                      </ul>
                    </div>
                    <div v-else-if="item.value === 's4-4'" class="agree-depth">
                      <!-- ======================================== -->
                      <!-- 동의등급제 안내 -->
                      <!-- ======================================== -->
                      <Card
                        variant="solid"
                        color="gray"
                        class="agree-info__card card-white"
                      >
                        <div class="info-card__header">
                          <p class="info-card__title">동의등급제 안내</p>
                        </div>
                        <div class="info-card__content">
                          <div class="label-group">
                            <!-- [251016] 안심 color 변경 blue에서 color="cyan" -->
                            <!-- <SolidLabel
                              color="blue"
                              title="안심"
                            /> -->
                            <SolidLabel color="cyan" title="안심" />
                            <SolidLabel color="green" title="다소안심" />
                            <SolidLabel color="yellow" title="보통" />
                            <SolidLabel color="orange" title="신중" />
                            <SolidLabel color="red" title="주의" />
                          </div>
                          <UnorderedList>
                            <UnorderedListItem
                              variant="bullet"
                              size="small"
                              text="동의등급제는 개인(신용) 선택적 동의 항목에 대해 사생활의 비밀과 자유를 침해할 위험, 이익이나 혜택, 등의 내용의 명확성 등을 고려하여 5가지 등급을 부여하는 제도입니다."
                            />
                          </UnorderedList>
                        </div>
                      </Card>

                      <!-- ======================================== -->
                      <!-- 2뎁스 영역: 신한 슈퍼SOL 이용약관 -->
                      <!-- ======================================== -->
                      <ul class="agree-sublist agree-sublist__depth2">
                        <li
                          v-for="depth2Item in subItemsDepth2_s4_4"
                          :key="depth2Item.value"
                          class="agree-subitem agree-subitem__depth2"
                        >
                          <!-- 아코디언이 있는 항목 -->
                          <template v-if="depth2Item.accordion">
                            <SolidListAccordion
                              class="agree-subitem__accordion accordion-depth2"
                              :rowClickable="false"
                              :value="depth2Item.value"
                              v-model:isExpanded="
                                subAccordionState4[depth2Item.value]
                              "
                            >
                              <template #title>
                                <div class="agree-item agree-item__sub">
                                  <Checkbox
                                    :value="depth2Item.value"
                                    variant="mark"
                                    align="left"
                                    :model-value="
                                      subAgrees4.includes(depth2Item.value)
                                    "
                                    class="agree-item__checkbox item-checkbox__sub"
                                    @update:model-value="
                                      onToggleSub4(depth2Item.value, $event)
                                    "
                                    @click.stop
                                  >
                                    <template #label>
                                      <span
                                        class="agree-item__label item-label__sub"
                                        >{{ depth2Item.label }}</span
                                      >
                                    </template>
                                  </Checkbox>
                                </div>
                              </template>
                              <div class="agree-subitem__panel">
                                <!-- 3뎁스 영역: 전자금융서비스 이용동의(신한은행) -->
                                <div
                                  v-if="depth2Item.value === 's4-4-5'"
                                  class="agree-depth"
                                >
                                  <Card
                                    variant="solid"
                                    color="gray"
                                    class="agree-details"
                                  >
                                    <ul class="agree-sublist" role="group">
                                      <li
                                        v-for="depth3Item in subItemsDepth3_s4_4_5"
                                        :key="depth3Item.value"
                                        class="agree-subitem agree-subitem__depth3"
                                      >
                                        <div class="agree-item agree-item__sub">
                                          <span
                                            class="agree-item__label item-label__sub"
                                            >{{ depth3Item.label }}</span
                                          >
                                          <IconButton
                                            iconName="Chevron_right"
                                            size="small"
                                            :aria-label="`${depth3Item.label} 상세 보기`"
                                            class="agree-subitem__trigger"
                                          />
                                        </div>
                                      </li>
                                    </ul>
                                  </Card>
                                </div>

                                <!-- 3뎁스 영역: 광고성 전자적 수신매체 전송 동의 -->
                                <div
                                  v-else-if="depth2Item.value === 's4-4-10'"
                                  class="agree-depth"
                                >
                                  <Card
                                    variant="solid"
                                    color="gray"
                                    class="agree-details"
                                  >
                                    <ul class="agree-sublist" role="group">
                                      <li
                                        v-for="depth3Item in subItemsDepth3_s4_4_10"
                                        :key="depth3Item.value"
                                        class="agree-subitem agree-subitem__depth3"
                                      >
                                        <div class="agree-item agree-item__sub">
                                          <Checkbox
                                            :value="depth3Item.value"
                                            variant="mark"
                                            align="left"
                                            :model-value="
                                              subAgrees4.includes(
                                                depth3Item.value
                                              )
                                            "
                                            class="agree-item__checkbox item-checkbox__sub"
                                            @update:model-value="
                                              onToggleSub4(
                                                depth3Item.value,
                                                $event
                                              )
                                            "
                                            @click.stop
                                          >
                                            <template #label>
                                              <span
                                                class="agree-item__label item-label__sub"
                                                >{{ depth3Item.label }}</span
                                              >
                                            </template>
                                          </Checkbox>
                                        </div>
                                      </li>
                                    </ul>
                                  </Card>
                                </div>
                              </div>
                            </SolidListAccordion>
                          </template>

                          <!-- 일반 항목 -->
                          <div v-else class="agree-item agree-item__sub">
                            <Checkbox
                              :value="depth2Item.value"
                              variant="mark"
                              align="left"
                              :model-value="
                                subAgrees4.includes(depth2Item.value)
                              "
                              class="agree-item__checkbox item-checkbox__sub"
                              @update:model-value="
                                onToggleSub4(depth2Item.value, $event)
                              "
                              @click.stop
                            >
                              <template #label>
                                <span
                                  class="agree-item__label item-label__sub"
                                  >{{ depth2Item.label }}</span
                                >
                                <template
                                  v-if="
                                    depth2Item.value === 's4-4-8' ||
                                    depth2Item.value === 's4-4-9'
                                  "
                                >
                                  <br />
                                  <SolidLabel
                                    color="cyan"
                                    title="안심"
                                    aria-label="동의등급제 안심"
                                  />
                                </template>
                              </template>
                            </Checkbox>
                            <IconButton
                              iconName="Chevron_right"
                              size="small"
                              :aria-label="`${depth2Item.label} 상세 보기`"
                              class="agree-subitem__trigger"
                            />
                          </div>
                        </li>
                      </ul>
                    </div>
                    <div v-else-if="item.value === 's4-5'" class="agree-depth">
                      <!-- ======================================== -->
                      <!-- 2뎁스 영역: 전자문서 서비스 이용약관 -->
                      <!-- ======================================== -->
                      <ul class="agree-sublist agree-sublist__depth2">
                        <li
                          v-for="depth2Item in subItemsDepth2_s4_5"
                          :key="depth2Item.value"
                          class="agree-subitem agree-subitem__depth2"
                        >
                          <div class="agree-item agree-item__sub">
                            <Checkbox
                              :value="depth2Item.value"
                              variant="mark"
                              align="left"
                              :model-value="
                                subAgrees4.includes(depth2Item.value)
                              "
                              class="agree-item__checkbox item-checkbox__sub"
                              @update:model-value="
                                onToggleSub4(depth2Item.value, $event)
                              "
                              @click.stop
                            >
                              <template #label>
                                <span
                                  class="agree-item__label item-label__sub"
                                  >{{ depth2Item.label }}</span
                                >
                              </template>
                            </Checkbox>
                            <IconButton
                              iconName="Chevron_right"
                              size="small"
                              :aria-label="`${depth2Item.label} 상세 보기`"
                              class="agree-subitem__trigger"
                            />
                          </div>
                        </li>
                      </ul>
                    </div>
                    <div v-else-if="item.value === 's4-6'" class="agree-depth">
                      <!-- ======================================== -->
                      <!-- 2뎁스 영역: 마이데이터 서비스 이용약관 -->
                      <!-- ======================================== -->
                      <ul class="agree-sublist agree-sublist__depth2">
                        <li
                          v-for="depth2Item in subItemsDepth2_s4_6"
                          :key="depth2Item.value"
                          class="agree-subitem agree-subitem__depth2"
                        >
                          <div class="agree-item agree-item__sub">
                            <Checkbox
                              :value="depth2Item.value"
                              variant="mark"
                              align="left"
                              :model-value="
                                subAgrees4.includes(depth2Item.value)
                              "
                              class="agree-item__checkbox item-checkbox__sub"
                              @update:model-value="
                                onToggleSub4(depth2Item.value, $event)
                              "
                              @click.stop
                            >
                              <template #label>
                                <span
                                  class="agree-item__label item-label__sub"
                                  >{{ depth2Item.label }}</span
                                >
                              </template>
                            </Checkbox>
                            <IconButton
                              iconName="Chevron_right"
                              size="small"
                              :aria-label="`${depth2Item.label} 상세 보기`"
                              class="agree-subitem__trigger"
                            />
                          </div>
                        </li>
                      </ul>

                      <!-- 개인정보 처리방침 링크 -->
                      <div class="agree-depth__link">
                        <TextButton
                          class="agree-depth__link"
                          color="secondary"
                          size="small"
                          text="개인정보 처리방침"
                          showGoTo
                        />
                      </div>
                    </div>
                    <div v-else-if="item.value === 's4-7'" class="agree-depth">
                      <!-- ======================================== -->
                      <!-- 2뎁스 영역: 마케팅 동의 이용약관 -->
                      <!-- ======================================== -->
                      <ul class="agree-sublist agree-sublist__depth2">
                        <!-- 동의등급제 안내 -->
                        <li class="agree-subitem agree-subitem__depth2">
                          <Card
                            variant="solid"
                            color="gray"
                            class="agree-info__card card-white"
                          >
                            <div class="info-card__header">
                              <p class="info-card__title">동의등급제 안내</p>
                            </div>
                            <div class="info-card__content">
                              <div class="label-group">
                                <SolidLabel color="cyan" title="안심" />
                                <SolidLabel color="green" title="다소안심" />
                                <SolidLabel color="yellow" title="보통" />
                                <SolidLabel color="orange" title="신중" />
                                <SolidLabel color="red" title="주의" />
                              </div>
                              <UnorderedList>
                                <UnorderedListItem
                                  variant="bullet"
                                  size="small"
                                  text="동의등급제는 개인(신용) 선택적 동의 항목에 대해 사생활의 비밀과 자유를 침해할 위험, 이익이나 혜택, 등의 내용의 명확성 등을 고려하여 5가지 등급을 부여하는 제도입니다."
                                />
                              </UnorderedList>
                            </div>
                          </Card>
                        </li>
                        <!-- 동의등급제 안내 이후 추가 항목들 -->
                        <li
                          v-for="depth2Item in subItemsDepth2_s4_7_after"
                          :key="depth2Item.value"
                          class="agree-subitem agree-subitem__depth2"
                          :class="{
                            'agree-subitem__accordion': Boolean(
                              depth2Item.accordion
                            ),
                          }"
                        >
                          <!-- 아코디언이 있는 항목 -->
                          <template v-if="depth2Item.accordion">
                            <SolidListAccordion
                              class="agree-subitem__accordion accordion-depth2"
                              :rowClickable="false"
                              :value="depth2Item.value"
                              v-model:isExpanded="
                                subAccordionState4[depth2Item.value]
                              "
                            >
                              <template #title>
                                <div class="agree-item agree-item__sub">
                                  <Checkbox
                                    :value="depth2Item.value"
                                    variant="mark"
                                    align="left"
                                    :model-value="
                                      subAgrees4.includes(depth2Item.value)
                                    "
                                    class="agree-item__checkbox item-checkbox__sub"
                                    @update:model-value="
                                      onToggleSub4(depth2Item.value, $event)
                                    "
                                    @click.stop
                                  >
                                    <template #label>
                                      <span
                                        class="agree-item__label item-label__sub"
                                        >{{ depth2Item.label }}</span
                                      >
                                      <template v-if="depth2Item.grade">
                                        <br />
                                        <SolidLabel
                                          :color="depth2Item.grade"
                                          :title="
                                            depth2Item.grade === 'cyan'
                                              ? '안심'
                                              : depth2Item.grade === 'green'
                                                ? '다소안심'
                                                : depth2Item.grade === 'yellow'
                                                  ? '보통'
                                                  : depth2Item.grade ===
                                                      'orange'
                                                    ? '신중'
                                                    : '주의'
                                          "
                                          :aria-label="`동의등급제 ${
                                            depth2Item.grade === 'cyan'
                                              ? '안심'
                                              : depth2Item.grade === 'green'
                                                ? '다소안심'
                                                : depth2Item.grade === 'yellow'
                                                  ? '보통'
                                                  : depth2Item.grade ===
                                                      'orange'
                                                    ? '신중'
                                                    : '주의'
                                          }`"
                                        />
                                      </template>
                                    </template>
                                  </Checkbox>
                                </div>
                              </template>
                              <div class="agree-subitem__panel">
                                <!-- 3뎁스 영역: 카드 및 금융상품 ・ 서비스 안내 및 이용권유를 위한 수집 ・ 이용 -->
                                <div
                                  v-if="depth2Item.value === 's4-2-6'"
                                  class="agree-depth"
                                >
                                  <ul
                                    class="agree-sublist agree-sublist__depth3"
                                  >
                                    <li
                                      v-for="depth3Item in subItemsDepth3_s4_2_6"
                                      :key="depth3Item.value"
                                      class="agree-subitem agree-subitem__depth3"
                                    >
                                      <div class="agree-item agree-item__sub">
                                        <Checkbox
                                          :value="depth3Item.value"
                                          variant="mark"
                                          align="left"
                                          :model-value="
                                            subAgrees4.includes(
                                              depth3Item.value
                                            )
                                          "
                                          class="agree-item__checkbox item-checkbox__sub"
                                          @update:model-value="
                                            onToggleSub4(
                                              depth3Item.value,
                                              $event
                                            )
                                          "
                                          @click.stop
                                        >
                                          <template #label>
                                            <span
                                              class="agree-item__label item-label__sub"
                                              >{{ depth3Item.label }}</span
                                            >
                                          </template>
                                        </Checkbox>
                                      </div>
                                    </li>
                                  </ul>
                                  <!-- 자세히보기 링크 -->
                                  <div class="agree-depth__link">
                                    <TextButton
                                      class="agree-depth__link"
                                      color="secondary"
                                      size="small"
                                      text="자세히보기"
                                      showGoTo
                                    />
                                  </div>
                                </div>

                                <!-- 3뎁스 영역: 카드 및 금융상품 ・ 서비스 이외의 부수서비스 안내 등을 위한 수집 ・ 이용 -->
                                <template
                                  v-else-if="depth2Item.value === 's4-2-7'"
                                >
                                  <ul
                                    class="agree-sublist agree-sublist__depth3"
                                  >
                                    <li
                                      v-for="depth3Item in subItemsDepth3_s4_2_7"
                                      :key="depth3Item.value"
                                      class="agree-subitem agree-subitem__depth3"
                                    >
                                      <div class="agree-item agree-item__sub">
                                        <Checkbox
                                          :value="depth3Item.value"
                                          variant="mark"
                                          align="left"
                                          :model-value="
                                            subAgrees4.includes(
                                              depth3Item.value
                                            )
                                          "
                                          class="agree-item__checkbox item-checkbox__sub"
                                          @update:model-value="
                                            onToggleSub4(
                                              depth3Item.value,
                                              $event
                                            )
                                          "
                                          @click.stop
                                        >
                                          <template #label>
                                            <span
                                              class="agree-item__label item-label__sub"
                                              >{{ depth3Item.label }}</span
                                            >
                                          </template>
                                        </Checkbox>
                                      </div>
                                    </li>
                                  </ul>
                                  <!-- 자세히보기 링크 -->
                                  <div class="agree-depth__link">
                                    <TextButton
                                      class="agree-depth__link"
                                      color="secondary"
                                      size="small"
                                      text="자세히보기"
                                      showGoTo
                                    />
                                  </div>
                                </template>

                                <!-- 3뎁스 영역: 전자적 전송매체를 통한 광고성 정보 수신동의 -->
                                <div
                                  v-else-if="depth2Item.value === 's4-2-8'"
                                  class="agree-depth"
                                >
                                  <Card
                                    variant="solid"
                                    color="gray"
                                    class="agree-details"
                                  >
                                    <ul class="agree-sublist" role="group">
                                      <li
                                        v-for="depth3Item in subItemsDepth3_s4_2_8"
                                        :key="depth3Item.value"
                                        class="agree-subitem agree-subitem__depth3"
                                      >
                                        <div class="agree-item agree-item__sub">
                                          <Checkbox
                                            :value="depth3Item.value"
                                            variant="mark"
                                            align="left"
                                            :model-value="
                                              subAgrees4.includes(
                                                depth3Item.value
                                              )
                                            "
                                            class="agree-item__checkbox item-checkbox__sub"
                                            @update:model-value="
                                              onToggleSub4(
                                                depth3Item.value,
                                                $event
                                              )
                                            "
                                            @click.stop
                                          >
                                            <template #label>
                                              <span
                                                class="agree-item__label item-label__sub"
                                                >{{ depth3Item.label }}</span
                                              >
                                            </template>
                                          </Checkbox>
                                        </div>
                                      </li>
                                    </ul>
                                  </Card>
                                  <!-- 설명 텍스트 -->
                                  <UnorderedList class="mt-md mb-md">
                                    <UnorderedListItem
                                      variant="bullet"
                                      size="small"
                                      text="카드상품과 부수서비스의 안내 및 이용권유에 셨더라도 신용정보의 이용 및 보호에 관한 법률에 따라 이용권유 목적의 연락에 대한 중단을 언제라도 카드사에 요청할 수 있습니다. (대표전화 : 1544-7000 / 홈페이지 : www.shinhancard.com)"
                                    />
                                    <UnorderedListItem
                                      variant="bullet"
                                      size="small"
                                      text="갱신 및 상품서비스 변경 안내 등 필수 고지사항은 상기 동의 대상에서 제외됩니다."
                                    />
                                  </UnorderedList>
                                </div>

                                <!-- 3뎁스 영역: 신한금융 자회사 및 손자회사에 개인(신용)정보를 제공 (s4-2-9) -->
                                <div
                                  v-else-if="depth2Item.value === 's4-2-9'"
                                  class="agree-depth"
                                >
                                  <ul
                                    class="agree-sublist agree-sublist__depth3"
                                  >
                                    <li
                                      v-for="depth3Item in subItemsDepth3_s4_2_9"
                                      :key="depth3Item.value"
                                      class="agree-subitem agree-subitem__depth3"
                                    >
                                      <div class="agree-item agree-item__sub">
                                        <Checkbox
                                          :value="depth3Item.value"
                                          variant="mark"
                                          align="left"
                                          :model-value="
                                            subAgrees4.includes(
                                              depth3Item.value
                                            )
                                          "
                                          class="agree-item__checkbox item-checkbox__sub"
                                          @update:model-value="
                                            onToggleSub4(
                                              depth3Item.value,
                                              $event
                                            )
                                          "
                                          @click.stop
                                        >
                                          <template #label>
                                            <span
                                              class="agree-item__label item-label__sub"
                                              >{{ depth3Item.label }}</span
                                            >
                                          </template>
                                        </Checkbox>
                                      </div>
                                    </li>
                                  </ul>
                                  <!-- 자세히보기 링크 -->
                                  <div class="agree-depth__link">
                                    <TextButton
                                      class="agree-depth__link"
                                      color="secondary"
                                      size="small"
                                      text="자세히보기"
                                      showGoTo
                                    />
                                  </div>
                                </div>
                              </div>
                            </SolidListAccordion>
                          </template>
                        </li>
                      </ul>
                    </div>
                  </div>
                </SolidListAccordion>
              </template>
              <template v-else>
                <div
                  class="agree-item agree-item__sub"
                  :class="{ 'is-checked': subAgrees4.includes(item.value) }"
                >
                  <Checkbox
                    :value="item.value"
                    variant="box"
                    align="left"
                    :model-value="subAgrees4.includes(item.value)"
                    class="agree-item__checkbox item-checkbox__sub"
                    @update:model-value="onToggleSub4(item.value, $event)"
                    @click.stop
                  >
                    <template #label>
                      <span class="agree-item__label item-label__sub">{{
                        item.label
                      }}</span>
                    </template>
                  </Checkbox>
                  <IconButton
                    iconName="Chevron_right"
                    size="small"
                    :aria-label="`${item.label} 상세 보기`"
                    class="agree-subitem__trigger"
                  />
                </div>
              </template>
            </div>
          </div>
        </div>
      </div>
    </section>
  </div>

  <!-- 하단 고정으로 들어가는 부분 위치 수정 -->
  <div class="sc-contents__foot">
    <Divider variant="group" color="tertiary" />
    <div class="sc-bottom-info__inner">
      <h2 class="sc-bottom-info__title">마이데이터 서비스 안내</h2>
      <div class="sc-bottom-info__details">
        <UnorderedList>
          <UnorderedListItem
            variant="bullet"
            text="잘 이용하지 않는 서비스는 탈퇴 후 내 정보를 삭제할 수 있어요."
          />
          <UnorderedListItem
            variant="bullet"
            text="나의 마이데이터 서비스 가입현황은 마이데이터 종합포털에서 확인할 수 있어요."
          />
        </UnorderedList>
      </div>
      <!-- [251027] 마이데이터 서비스 안내 하단 링크 추가 -->
      <div class="agree-depth__link">
        <TextButton
          class="agree-depth__link"
          color="secondary"
          size="small"
          text="종합포털 바로가기"
          showGoTo
        />
      </div>
    </div>
  </div>

  <BottomActionContainer :scrollDim="true">
    <BoxButtonGroup size="xlarge" variant="100">
      <BoxButton text="확인" :disabled="!basicAgree4" />
    </BoxButtonGroup>
  </BottomActionContainer>
</template>

<script setup>
import {
  BottomActionContainer,
  BoxButton,
  BoxButtonGroup,
  Card,
  Checkbox,
  Divider,
  IconButton,
  SolidLabel,
  SolidListAccordion,
  TextButton,
  UnorderedList,
  UnorderedListItem,
} from "@shc-nss/ui/solid";
import { computed, reactive, ref, watch } from "vue";
import { useRoute } from "vue-router";

const route = useRoute();
const bodyTitle = computed(() => route.meta?.title || "");

/**
 * 유형 4 : 약관동의 기본형
 */
const basicItem4 = {
  label: "약관 전체 동의",
};

// JavaScript/TypeScript 호환을 위한 타입 정의 (선택사항)

// JavaScript/TypeScript 호환 배열
const subItems4 = [
  {
    label: "[필수/선택] 서비스 이용약관",
    value: "s4-1",
    accordion: true,
  },
  {
    label: "[필수/선택] 신한Pay머니 이용약관",
    value: "s4-2",
    accordion: true,
  },
  {
    label: "[선택] 온라인 회원 이용약관",
    value: "s4-3",
    accordion: true,
  },
  {
    label: "[선택] 신한 슈퍼SOL 이용약관",
    value: "s4-4",
    accordion: true,
  },
  {
    label: "[선택] 전자문서 서비스 이용약관",
    value: "s4-5",
    accordion: true,
  },
  {
    label: "[선택] 마이데이터 서비스 이용약관",
    value: "s4-6",
    accordion: true,
  },
  {
    label: "[선택] 마케팅 동의 이용약관",
    value: "s4-7",
    accordion: true,
  },
];

// 2뎁스 항목들 - 서비스 이용약관 (s4-1)
const subItemsDepth2_s4_1 = [
  { label: "[필수] 앱카드 서비스 이용약관 동의", value: "s4-1-1" },
  { label: "[필수] 개인(신용)정보의 수집 및 이용동의", value: "s4-1-2" },
  { label: "[필수] 고유식별정보처리 동의", value: "s4-1-3" },
  {
    label: "[선택] 위치기반 서비스 약관동의",
    value: "s4-1-4",
    accordion: true,
  },
  { label: "[선택] 앱(APP) 알림 수신동의", value: "s4-1-5", accordion: true },
];

// 2뎁스 항목들 - 신한Pay머니 이용약관 (s4-2)
const subItemsDepth2_s4_2 = [
  { label: "[필수] 신한Pay머니 이용약관동의", value: "s4-2-1" },
  { label: "[필수] 개인정보 수집 및 이용동의", value: "s4-2-2" },
  { label: "[필수] 고유식별정보처리 동의", value: "s4-2-3" },
  { label: "[필수] 개인(신용)정보 제공동의", value: "s4-2-4" },
  { label: "[필수] 고유식별정보 제공동의", value: "s4-2-5" },
];

// 2뎁스 항목들 - 신한Pay머니 이용약관 동의등급제 이후 항목들 (s4-2)
const subItemsDepth2_s4_2_after = [
  {
    label:
      "[선택] 카드 및 금융상품 ・ 서비스 안내 및 이용권유를 위한 수집 ・ 이용",
    value: "s4-2-6",
    grade: "green", // 다소안심
    accordion: true,
  },
  {
    label:
      "[선택] 카드 및 금융상품 ・ 서비스 이외의 부수서비스 안내 등을 위한 수집 ・ 이용",
    value: "s4-2-7",
    grade: "yellow", // 보통
    accordion: true,
  },
  {
    label: "[선택] 전자적 전송매체를 통한 광고성 정보 수신동의",
    value: "s4-2-8",
    accordion: true,
  },
  {
    label:
      "[선택] 카드 및 금융상품 ・ 서비스 안내 및 이용권유를 위한 수집 ・ 이용",
    value: "s4-2-9",
    grade: "cyan", // 안심
    accordion: true,
  },
  { label: "[필수] 회원 가입 및 발권신청 동의", value: "s4-2-10" },
];

// 2뎁스 항목들 - 마케팅 동의 이용약관 (s4-7)
const subItemsDepth2_s4_7_after = [
  {
    label:
      "[선택] 카드 및 금융상품 ・ 서비스 안내 및 이용권유를 위한 수집 ・ 이용",
    value: "s4-2-6",
    grade: "green", // 다소안심
    accordion: true,
  },
  {
    label:
      "[선택] 카드 및 금융상품 ・ 서비스 이외의 부수서비스 안내 등을 위한 수집 ・ 이용",
    value: "s4-2-7",
    grade: "yellow", // 보통
    accordion: true,
  },
  {
    label: "[선택] 전자적 전송매체를 통한 광고성 정보 수신동의",
    value: "s4-2-8",
    accordion: true,
  },
  {
    label: "[선택] 신한금융 자회사 및 손자회사에 개인(신용)정보를 제공",
    value: "s4-2-9",
    grade: "cyan", // 안심
    accordion: true,
  },
];

// 3뎁스 항목들 - 카드 및 금융상품 ・ 서비스 안내 및 이용권유를 위한 수집 ・ 이용 (s4-2-6)
const subItemsDepth3_s4_2_6 = [
  { label: "고유식별번호 조회 동의", value: "s4-2-6-1" },
  { label: "개인신용정보 제공 동의", value: "s4-2-6-2" },
];

// 3뎁스 항목들 - 카드 및 금융상품 ・ 서비스 안내 및 이용권유를 위한 수집 ・ 이용 (s4-2-9)
const subItemsDepth3_s4_2_9 = [
  { label: "개인신용정보 제공 동의", value: "s4-2-9-1" },
];

// 3뎁스 항목들 - 카드 및 금융상품 ・ 서비스 이외의 부수서비스 안내 등을 위한 수집 ・ 이용 (s4-2-7)
const subItemsDepth3_s4_2_7 = [
  { label: "고유식별번호 조회 동의", value: "s4-2-7-1" },
  { label: "개인신용정보 제공 동의", value: "s4-2-7-2" },
];

// 3뎁스 항목들 - 전자적 전송매체를 통한 광고성 정보 수신동의 (s4-2-8)
const subItemsDepth3_s4_2_8 = [
  { label: "전체", value: "s4-2-8-1" },
  { label: "서면", value: "s4-2-8-2" },
  { label: "이메일", value: "s4-2-8-3" },
  { label: "전화", value: "s4-2-8-4" },
  {
    label: "휴대폰 메세지(카카오톡, 네이버 알림 등 모바일 메세지 포함)",
    value: "s4-2-8-5",
  },
];

// 2뎁스 항목들 - 온라인 회원 이용약관 (s4-3)
const subItemsDepth2_s4_3 = [
  { label: "[필수] 온라인 회원 이용약관동의", value: "s4-3-1" },
  { label: "[필수] 개인정보 필수적 수집・이용동의서", value: "s4-3-2" },
];

// 2뎁스 항목들 - 신한 슈퍼SOL 이용약관 (s4-4)
const subItemsDepth2_s4_4 = [
  { label: "[필수] 신한 모바일 플랫폼 이용약관", value: "s4-4-1" },
  { label: "[필수] 신한금융그룹 통합 포인트 서비스 이용동의", value: "s4-4-2" },
  { label: "[필수] 개인(신용)정보 수집・이용・제공 동의", value: "s4-4-3" },
  {
    label: "[필수] 개인(신용)정보 수집・이용・제공 동의(포인트 서비스 제공)",
    value: "s4-4-4",
  },
  {
    label: "[필수] 전자금융서비스 이용동의(신한은행)",
    value: "s4-4-5",
    accordion: true,
  },
  { label: "[필수] 그룹 로열티 서비스 이용동의(신한은행)", value: "s4-4-6" },
  {
    label: "[필수] 개인(신용)정보 수집・이용・제공 동의(신한은행)",
    value: "s4-4-7",
  },
  {
    label: "[선택] 개인(신용)정보 수집・이용・제공 동의(상품 서비스 안내 등)",
    value: "s4-4-8",
  },
  {
    label:
      "[선택] 개인(신용)정보 수집・이용・제공 동의(상품 서비스 안내 등)(신한은행)",
    value: "s4-4-9",
  },
  {
    label: "[선택] 광고성 전자적 수신매체 전송 동의",
    value: "s4-4-10",
    accordion: true,
  },
];

// 3뎁스 항목들 - 전자금융서비스 이용동의(신한은행) (s4-4-5)
const subItemsDepth3_s4_4_5 = [
  { label: "전자금융거래 기본약관", value: "s4-4-5-1" },
  { label: "신한온라인서비스 이용약관", value: "s4-4-5-2" },
  { label: "전자통지서비스 이용약관", value: "s4-4-5-3" },
  { label: "개인정보 수집 이용동의(비여신 금융거래)", value: "s4-4-5-4" },
];

// 3뎁스 항목들 - 광고성 전자적 수신매체 전송 동의 (s4-4-10)
const subItemsDepth3_s4_4_10 = [
  { label: "문자", value: "s4-4-10-1" },
  { label: "이메일", value: "s4-4-10-2" },
  { label: "전화", value: "s4-4-10-3" },
];

// 3뎁스 항목들 - 위치기반 서비스 약관동의 (s4-1-4)
const subItemsDepth3_s4_1_4 = [
  { label: "신한카드 위치기반 사업자 약관동의", value: "s4-1-4-1" },
  { label: "위치정보 서비스 동의사항", value: "s4-1-4-2", accordion: true },
  { label: "개인정보 수집 및 이용동의", value: "s4-1-4-3" },
  { label: "위치기반 혜택 알림 수신동의", value: "s4-1-4-4" },
  { label: "블루칩 씨엔에스 위치정보사업자약관동의", value: "s4-1-4-5" },
];

// 3뎁스 항목들 - 앱(APP) 알림 수신동의 (s4-1-5)
const subItemsDepth3_s4_1_5 = [
  { label: "마케팅 정보 수신동의", value: "s4-1-5-1", accordion: true },
];

// 4뎁스 항목들 - 위치정보 서비스 동의사항 (s4-1-4-2)
const subItemsDepth4_s4_1_4_2 = [
  { label: "LGU+ 위치정보 사업자 약관 동의", value: "s4-1-4-2-1" },
  { label: "LGU+ 개인정보수집이용 및 제3자 제공동의", value: "s4-1-4-2-2" },
  { label: "로플렛 위치정보 사업자 약관동의", value: "s4-1-4-2-3" },
];

// 2뎁스 항목들 - 전자문서 서비스 (s4-5)
const subItemsDepth2_s4_5 = [
  { label: "[필수] 전자문서 서비스 이용약관 동의", value: "s4-5-1" },
  { label: "[필수] 전자문서 개인정보 수집・이용・동의", value: "s4-5-2" },
  { label: "[필수] 개인정보 제3자 제공 동의", value: "s4-5-3" },
  { label: "[필수] 서비스 유의사항 동의", value: "s4-5-4" },
];

// 2뎁스 항목들 - 마이데이터 서비스 (s4-6)
const subItemsDepth2_s4_6 = [
  { label: "[필수] 마이데이터 서비스 이용약관동의", value: "s4-6-1" },
  {
    label: "[필수] 마이데이터 서비스 개인(신용)정보의 수집 및 이용동의",
    value: "s4-6-2",
  },
];

const basicAgree4 = ref(false);
const subAgrees4 = ref([]);
const subAccordionState4 = reactive({
  "s4-1": false, // 서비스 이용약관 2뎁스 아코디언 상태
  "s4-2": false, // 신한Pay머니 이용약관 2뎁스 아코디언 상태
  "s4-3": false, // 온라인 회원 이용약관 2뎁스 아코디언 상태
  "s4-4": false, // 신한 슈퍼SOL 이용약관 2뎁스 아코디언 상태
  "s4-5": false, // 전자문서 서비스 2뎁스 아코디언 상태
  "s4-6": false, // 마이데이터 서비스 2뎁스 아코디언 상태
  "s4-7": false, // 마케팅 동의 이용약관 2뎁스 아코디언 상태
  "s4-1-4": false, // 위치기반 서비스 약관동의 3뎁스 아코디언 상태
  "s4-1-5": false, // 앱(APP) 알림 수신동의 3뎁스 아코디언 상태
  "s4-1-4-2": false, // 위치정보 서비스 동의사항 4뎁스 아코디언 상태
  "s4-1-5-1": false, // 마케팅 정보 수신동의 4뎁스 아코디언 상태
  "s4-4-5": false, // 전자금융서비스 이용동의(신한은행) 3뎁스 아코디언 상태
  "s4-4-10": false, // 광고성 전자적 수신매체 전송 동의 3뎁스 아코디언 상태
  "s4-2-6": false, // 카드 및 금융상품 ・ 서비스 안내 및 이용권유를 위한 수집 ・ 이용 2뎁스 아코디언 상태
  "s4-2-7": false, // 카드 및 금융상품 ・ 서비스 이외의 부수서비스 안내 등을 위한 수집 ・ 이용 2뎁스 아코디언 상태
  "s4-2-8": false, // 전자적 전송매체를 통한 광고성 정보 수신동의 2뎁스 아코디언 상태
  "s4-2-9": false, // 카드 및 금융상품 ・ 서비스 안내 및 이용권유를 위한 수집 ・ 이용 2뎁스 아코디언 상태
});

/**
 * 동작 로직
 */
function onToggleSub4(value, checked) {
  const set = new Set(subAgrees4.value);
  if (checked) set.add(value);
  else set.delete(value);
  subAgrees4.value = Array.from(set);

  // 전체 항목 수 계산 (1뎁스 + 2뎁스 + 3뎁스 + 4뎁스)
  const totalItems =
    subItems4.length +
    subItemsDepth2_s4_1.length +
    subItemsDepth2_s4_2.length +
    subItemsDepth2_s4_2_after.length +
    subItemsDepth2_s4_3.length +
    subItemsDepth2_s4_4.length +
    subItemsDepth2_s4_5.length +
    subItemsDepth2_s4_6.length +
    subItemsDepth3_s4_1_4.length +
    subItemsDepth3_s4_1_5.length +
    subItemsDepth3_s4_2_6.length +
    subItemsDepth3_s4_2_7.length +
    subItemsDepth3_s4_2_8.length +
    subItemsDepth3_s4_2_9.length +
    subItemsDepth3_s4_4_5.length +
    subItemsDepth3_s4_4_10.length +
    subItemsDepth4_s4_1_4_2.length;
  basicAgree4.value = set.size === totalItems;
}

watch(basicAgree4, (checked) => {
  if (checked) {
    // 1뎁스 항목들 + 아코디언 내부의 모든 하위 항목들 (2뎁스 + 3뎁스 + 4뎁스)
    const allItems = [
      ...subItems4.map((item) => item.value),
      ...subItemsDepth2_s4_1.map((item) => item.value),
      ...subItemsDepth2_s4_2.map((item) => item.value),
      ...subItemsDepth2_s4_2_after.map((item) => item.value),
      ...subItemsDepth2_s4_3.map((item) => item.value),
      ...subItemsDepth2_s4_4.map((item) => item.value),
      ...subItemsDepth2_s4_5.map((item) => item.value),
      ...subItemsDepth2_s4_6.map((item) => item.value),
      ...subItemsDepth3_s4_1_4.map((item) => item.value),
      ...subItemsDepth3_s4_1_5.map((item) => item.value),
      ...subItemsDepth3_s4_2_6.map((item) => item.value),
      ...subItemsDepth3_s4_2_7.map((item) => item.value),
      ...subItemsDepth3_s4_2_8.map((item) => item.value),
      ...subItemsDepth3_s4_2_9.map((item) => item.value),
      ...subItemsDepth3_s4_4_5.map((item) => item.value),
      ...subItemsDepth3_s4_4_10.map((item) => item.value),
      ...subItemsDepth4_s4_1_4_2.map((item) => item.value),
    ];
    subAgrees4.value = allItems;
  } else {
    subAgrees4.value = [];
  }
});
</script>









<route lang="yaml">
meta:
  id: SSN017A01
  title: 약관동의
  menu: Sign in/up > 약관동의(머니회원)
  layout: SubLayout
  category: Sign in/up
  publish: 김대민
  publishVersion: 0.8
  status: 재작업
  etc: |
    260105: 디자인 동기화 - 약관 체크항목 추가,
    안심 color 변경 blue에서 color=cyan,
    [251027] 마이데이터 서비스 안내 하단 링크 추가
  header:
    fixed: true
    close: true
</route>
<template>
  <!-- 콘텐츠 영역 -->
  <div class="sc-contents__body sc-agree__page">
    <section class="section">
      <div class="sc-agree__list compound" role="region">
        <div class="agree-list__group">
          <div
            class="agree-item item-basic"
            :class="{ 'is-checked': basicAgree4 }"
          >
            <Checkbox
              v-model="basicAgree4"
              class="agree-item__checkbox item-checkbox__basic"
              variant="box"
              align="left"
            >
              <template #label>
                <span class="agree-item__label item-label__basic">{{
                  basicItem4.label
                }}</span>
              </template>
            </Checkbox>
          </div>

          <!-- ======================================== -->
          <!-- 1뎁스 영역: 기본 약관 항목들 -->
          <!-- ======================================== -->
          <div class="agree-sublist" role="group">
            <div
              v-for="item in subItems4"
              :key="item.value"
              class="agree-subitem"
              :class="{ 'agree-subitem__accordion': Boolean(item.accordion) }"
            >
              <template v-if="item.accordion">
                <SolidListAccordion
                  class="agree-subitem__accordion"
                  :rowClickable="false"
                  :value="item.value"
                  v-model:isExpanded="subAccordionState4[item.value]"
                >
                  <template #title>
                    <div
                      class="agree-item agree-item__sub"
                      :class="{
                        'is-checked': subAgrees4.includes(item.value),
                      }"
                    >
                      <Checkbox
                        :value="item.value"
                        variant="box"
                        align="left"
                        :model-value="subAgrees4.includes(item.value)"
                        class="agree-item__checkbox item-checkbox__sub"
                        @update:model-value="onToggleSub4(item.value, $event)"
                        @click.stop
                      >
                        <template #label>
                          <span class="agree-item__label item-label__sub">{{
                            item.label
                          }}</span>
                        </template>
                      </Checkbox>
                    </div>
                  </template>
                  <div class="agree-subitem__panel">
                    <div v-if="item.value === 's4-1'" class="agree-depth">
                      <!-- ======================================== -->
                      <!-- 2뎁스 영역: 서비스 이용약관 -->
                      <!-- ======================================== -->
                      <ul class="agree-sublist agree-sublist__depth2">
                        <li
                          v-for="depth2Item in subItemsDepth2_s4_1"
                          :key="depth2Item.value"
                          class="agree-subitem agree-subitem__depth2"
                        >
                          <!-- 아코디언이 있는 항목 -->
                          <template v-if="depth2Item.accordion">
                            <SolidListAccordion
                              class="agree-subitem__accordion accordion-depth2"
                              :rowClickable="false"
                              :value="depth2Item.value"
                              v-model:isExpanded="
                                subAccordionState4[depth2Item.value]
                              "
                            >
                              <template #title>
                                <div class="agree-item agree-item__sub">
                                  <Checkbox
                                    :value="depth2Item.value"
                                    variant="mark"
                                    align="left"
                                    :model-value="
                                      subAgrees4.includes(depth2Item.value)
                                    "
                                    class="agree-item__checkbox item-checkbox__sub"
                                    @update:model-value="
                                      onToggleSub4(depth2Item.value, $event)
                                    "
                                    @click.stop
                                  >
                                    <template #label>
                                      <span
                                        class="agree-item__label item-label__sub"
                                        >{{ depth2Item.label }}</span
                                      >
                                    </template>
                                  </Checkbox>
                                </div>
                              </template>
                              <div class="agree-subitem__panel">
                                <!-- 3뎁스 영역: 위치기반 서비스 약관동의 -->
                                <div v-if="depth2Item.value === 's4-1-4'">
                                  <ul
                                    class="agree-sublist agree-sublist__depth3"
                                  >
                                    <li
                                      v-for="depth3Item in subItemsDepth3_s4_1_4"
                                      :key="depth3Item.value"
                                      class="agree-subitem agree-subitem__depth3"
                                    >
                                      <!-- 아코디언이 있는 3뎁스 항목 -->
                                      <template v-if="depth3Item.accordion">
                                        <SolidListAccordion
                                          class="agree-subitem__accordion accordion-depth3"
                                          :rowClickable="false"
                                          :value="depth3Item.value"
                                          v-model:isExpanded="
                                            subAccordionState4[depth3Item.value]
                                          "
                                        >
                                          <template #title>
                                            <div
                                              class="agree-item agree-item__sub"
                                            >
                                              <Checkbox
                                                :value="depth3Item.value"
                                                variant="mark"
                                                align="left"
                                                :model-value="
                                                  subAgrees4.includes(
                                                    depth3Item.value
                                                  )
                                                "
                                                class="agree-item__checkbox item-checkbox__sub"
                                                @update:model-value="
                                                  onToggleSub4(
                                                    depth3Item.value,
                                                    $event
                                                  )
                                                "
                                                @click.stop
                                              >
                                                <template #label>
                                                  <span
                                                    class="agree-item__label item-label__sub"
                                                    >{{
                                                      depth3Item.label
                                                    }}</span
                                                  >
                                                </template>
                                              </Checkbox>
                                            </div>
                                          </template>
                                          <div class="agree-subitem__panel">
                                            <!-- 4뎁스 영역: 위치정보 서비스 동의사항 상세 -->
                                            <div
                                              v-if="
                                                depth3Item.value === 's4-1-4-2'
                                              "
                                              class="outline-panel"
                                            >
                                              <Card
                                                variant="solid"
                                                color="gray"
                                                class="agree-details"
                                              >
                                                <ul
                                                  class="agree-sublist"
                                                  role="group"
                                                >
                                                  <li
                                                    v-for="depth4Item in subItemsDepth4_s4_1_4_2"
                                                    :key="depth4Item.value"
                                                    class="agree-subitem agree-subitem__depth4"
                                                  >
                                                    <div
                                                      class="agree-item agree-item__sub"
                                                    >
                                                      <Checkbox
                                                        :value="
                                                          depth4Item.value
                                                        "
                                                        variant="mark"
                                                        align="left"
                                                        :model-value="
                                                          subAgrees4.includes(
                                                            depth4Item.value
                                                          )
                                                        "
                                                        class="agree-item__checkbox item-checkbox__sub"
                                                        @update:model-value="
                                                          onToggleSub4(
                                                            depth4Item.value,
                                                            $event
                                                          )
                                                        "
                                                        @click.stop
                                                      >
                                                        <template #label>
                                                          <span
                                                            class="agree-item__label item-label__sub"
                                                            >{{
                                                              depth4Item.label
                                                            }}</span
                                                          >
                                                        </template>
                                                      </Checkbox>
                                                      <IconButton
                                                        iconName="Chevron_right"
                                                        size="small"
                                                        :aria-label="`${depth4Item.label} 상세 보기`"
                                                        class="agree-subitem__trigger"
                                                      />
                                                    </div>
                                                  </li>
                                                </ul>
                                              </Card>
                                            </div>
                                          </div>
                                        </SolidListAccordion>
                                      </template>

                                      <!-- 일반 3뎁스 항목 -->
                                      <div
                                        v-else
                                        class="agree-item agree-item__sub"
                                      >
                                        <Checkbox
                                          :value="depth3Item.value"
                                          variant="mark"
                                          align="left"
                                          :model-value="
                                            subAgrees4.includes(
                                              depth3Item.value
                                            )
                                          "
                                          class="agree-item__checkbox item-checkbox__sub"
                                          @update:model-value="
                                            onToggleSub4(
                                              depth3Item.value,
                                              $event
                                            )
                                          "
                                          @click.stop
                                        >
                                          <template #label>
                                            <span
                                              class="agree-item__label item-label__sub"
                                              >{{ depth3Item.label }}</span
                                            >
                                          </template>
                                        </Checkbox>
                                        <IconButton
                                          iconName="Chevron_right"
                                          size="small"
                                          :aria-label="`${depth3Item.label} 상세 보기`"
                                          class="agree-subitem__trigger"
                                        />
                                      </div>
                                    </li>
                                  </ul>
                                </div>

                                <!-- 3뎁스 영역: 앱(APP) 알림 수신동의 -->
                                <div v-else-if="depth2Item.value === 's4-1-5'">
                                  <ul
                                    class="agree-sublist agree-sublist__depth3"
                                  >
                                    <li
                                      v-for="depth3Item in subItemsDepth3_s4_1_5"
                                      :key="depth3Item.value"
                                      class="agree-subitem agree-subitem__depth3"
                                    >
                                      <!-- 아코디언이 있는 3뎁스 항목 -->
                                      <template v-if="depth3Item.accordion">
                                        <SolidListAccordion
                                          class="agree-subitem__accordion accordion-depth3"
                                          :rowClickable="false"
                                          :value="depth3Item.value"
                                          v-model:isExpanded="
                                            subAccordionState4[depth3Item.value]
                                          "
                                        >
                                          <template #title>
                                            <div
                                              class="agree-item agree-item__sub"
                                            >
                                              <Checkbox
                                                :value="depth3Item.value"
                                                variant="mark"
                                                align="left"
                                                :model-value="
                                                  subAgrees4.includes(
                                                    depth3Item.value
                                                  )
                                                "
                                                class="agree-item__checkbox item-checkbox__sub"
                                                @update:model-value="
                                                  onToggleSub4(
                                                    depth3Item.value,
                                                    $event
                                                  )
                                                "
                                                @click.stop
                                              >
                                                <template #label>
                                                  <span
                                                    class="agree-item__label item-label__sub"
                                                    >{{
                                                      depth3Item.label
                                                    }}</span
                                                  >
                                                </template>
                                              </Checkbox>
                                            </div>
                                          </template>
                                          <div class="agree-subitem__panel">
                                            <!-- 4뎁스 영역: 마케팅 정보 수신동의 상세 -->
                                            <div
                                              v-if="
                                                depth3Item.value === 's4-1-5-1'
                                              "
                                              class="outline-panel"
                                            >
                                              <Card
                                                variant="solid"
                                                color="gray"
                                                class="agree-details"
                                              >
                                                <UnorderedList>
                                                  <UnorderedListItem
                                                    variant="bullet"
                                                    size="small"
                                                    text="항목 : 앱(APP)을 통한 마케팅 정보 수신동의"
                                                  />
                                                  <UnorderedListItem
                                                    variant="bullet"
                                                    size="small"
                                                    text="이용목적 : 각종 이벤트, 할인, 혜택정보 등의 안내"
                                                  />
                                                  <UnorderedListItem
                                                    variant="bullet"
                                                    size="small"
                                                    text="보유기간 : 별도 동의 철회시까지"
                                                  />
                                                </UnorderedList>
                                              </Card>
                                            </div>
                                          </div>
                                        </SolidListAccordion>
                                      </template>

                                      <!-- 일반 3뎁스 항목 -->
                                      <div
                                        v-else
                                        class="agree-item agree-item__sub"
                                      >
                                        <Checkbox
                                          :value="depth3Item.value"
                                          variant="mark"
                                          align="left"
                                          :model-value="
                                            subAgrees4.includes(
                                              depth3Item.value
                                            )
                                          "
                                          class="agree-item__checkbox item-checkbox__sub"
                                          @update:model-value="
                                            onToggleSub4(
                                              depth3Item.value,
                                              $event
                                            )
                                          "
                                          @click.stop
                                        >
                                          <template #label>
                                            <span
                                              class="agree-item__label item-label__sub"
                                              >{{ depth3Item.label }}</span
                                            >
                                          </template>
                                        </Checkbox>
                                        <IconButton
                                          iconName="Chevron_right"
                                          size="small"
                                          :aria-label="`${depth3Item.label} 상세 보기`"
                                          class="agree-subitem__trigger"
                                        />
                                      </div>
                                    </li>
                                  </ul>
                                </div>
                              </div>
                            </SolidListAccordion>
                          </template>

                          <!-- 일반 항목 -->
                          <div v-else class="agree-item agree-item__sub">
                            <Checkbox
                              :value="depth2Item.value"
                              variant="mark"
                              align="left"
                              :model-value="
                                subAgrees4.includes(depth2Item.value)
                              "
                              class="agree-item__checkbox item-checkbox__sub"
                              @update:model-value="
                                onToggleSub4(depth2Item.value, $event)
                              "
                              @click.stop
                            >
                              <template #label>
                                <span
                                  class="agree-item__label item-label__sub"
                                  >{{ depth2Item.label }}</span
                                >
                              </template>
                            </Checkbox>
                            <IconButton
                              iconName="Chevron_right"
                              size="small"
                              :aria-label="`${depth2Item.label} 상세 보기`"
                              class="agree-subitem__trigger"
                            />
                          </div>
                        </li>
                      </ul>
                    </div>
                    <div v-else-if="item.value === 's4-2'" class="agree-depth">
                      <!-- ======================================== -->
                      <!-- 2뎁스 영역: 신한Pay머니 이용약관 -->
                      <!-- ======================================== -->
                      <ul class="agree-sublist agree-sublist__depth2">
                        <li
                          v-for="depth2Item in subItemsDepth2_s4_2"
                          :key="depth2Item.value"
                          class="agree-subitem agree-subitem__depth2"
                        >
                          <div class="agree-item agree-item__sub">
                            <Checkbox
                              :value="depth2Item.value"
                              variant="mark"
                              align="left"
                              :model-value="
                                subAgrees4.includes(depth2Item.value)
                              "
                              class="agree-item__checkbox item-checkbox__sub"
                              @update:model-value="
                                onToggleSub4(depth2Item.value, $event)
                              "
                              @click.stop
                            >
                              <template #label>
                                <span
                                  class="agree-item__label item-label__sub"
                                  >{{ depth2Item.label }}</span
                                >
                              </template>
                            </Checkbox>
                            <IconButton
                              iconName="Chevron_right"
                              size="small"
                              :aria-label="`${depth2Item.label} 상세 보기`"
                              class="agree-subitem__trigger"
                            />
                          </div>
                        </li>
                        <!-- 동의등급제 안내 -->
                        <li class="agree-subitem agree-subitem__depth2">
                          <Card
                            variant="solid"
                            color="gray"
                            class="agree-info__card card-white"
                          >
                            <div class="info-card__header">
                              <p class="info-card__title">동의등급제 안내</p>
                            </div>
                            <div class="info-card__content">
                              <div class="label-group">
                                <SolidLabel color="cyan" title="안심" />
                                <SolidLabel color="green" title="다소안심" />
                                <SolidLabel color="yellow" title="보통" />
                                <SolidLabel color="orange" title="신중" />
                                <SolidLabel color="red" title="주의" />
                              </div>
                              <UnorderedList>
                                <UnorderedListItem
                                  variant="bullet"
                                  size="small"
                                  text="동의등급제는 개인(신용) 선택적 동의 항목에 대해 사생활의 비밀과 자유를 침해할 위험, 이익이나 혜택, 등의 내용의 명확성 등을 고려하여 5가지 등급을 부여하는 제도입니다."
                                />
                              </UnorderedList>
                            </div>
                          </Card>
                        </li>
                        <!-- 동의등급제 안내 이후 추가 항목들 -->
                        <li
                          v-for="depth2Item in subItemsDepth2_s4_2_after"
                          :key="depth2Item.value"
                          class="agree-subitem agree-subitem__depth2"
                          :class="{
                            'agree-subitem__accordion': Boolean(
                              depth2Item.accordion
                            ),
                          }"
                        >
                          <!-- 아코디언이 있는 항목 -->
                          <template v-if="depth2Item.accordion">
                            <SolidListAccordion
                              class="agree-subitem__accordion accordion-depth2"
                              :rowClickable="false"
                              :value="depth2Item.value"
                              v-model:isExpanded="
                                subAccordionState4[depth2Item.value]
                              "
                            >
                              <template #title>
                                <div class="agree-item agree-item__sub">
                                  <Checkbox
                                    :value="depth2Item.value"
                                    variant="mark"
                                    align="left"
                                    :model-value="
                                      subAgrees4.includes(depth2Item.value)
                                    "
                                    class="agree-item__checkbox item-checkbox__sub"
                                    @update:model-value="
                                      onToggleSub4(depth2Item.value, $event)
                                    "
                                    @click.stop
                                  >
                                    <template #label>
                                      <span
                                        class="agree-item__label item-label__sub"
                                        >{{ depth2Item.label }}</span
                                      >
                                      <template v-if="depth2Item.grade">
                                        <br />
                                        <SolidLabel
                                          :color="depth2Item.grade"
                                          :title="
                                            depth2Item.grade === 'cyan'
                                              ? '안심'
                                              : depth2Item.grade === 'green'
                                                ? '다소안심'
                                                : depth2Item.grade === 'yellow'
                                                  ? '보통'
                                                  : depth2Item.grade ===
                                                      'orange'
                                                    ? '신중'
                                                    : '주의'
                                          "
                                          :aria-label="`동의등급제 ${
                                            depth2Item.grade === 'cyan'
                                              ? '안심'
                                              : depth2Item.grade === 'green'
                                                ? '다소안심'
                                                : depth2Item.grade === 'yellow'
                                                  ? '보통'
                                                  : depth2Item.grade ===
                                                      'orange'
                                                    ? '신중'
                                                    : '주의'
                                          }`"
                                        />
                                      </template>
                                    </template>
                                  </Checkbox>
                                </div>
                              </template>
                              <div class="agree-subitem__panel">
                                <!-- 3뎁스 영역: 카드 및 금융상품 ・ 서비스 안내 및 이용권유를 위한 수집 ・ 이용 -->
                                <div
                                  v-if="depth2Item.value === 's4-2-6'"
                                  class="agree-depth"
                                >
                                  <ul
                                    class="agree-sublist agree-sublist__depth3"
                                  >
                                    <li
                                      v-for="depth3Item in subItemsDepth3_s4_2_6"
                                      :key="depth3Item.value"
                                      class="agree-subitem agree-subitem__depth3"
                                    >
                                      <div class="agree-item agree-item__sub">
                                        <Checkbox
                                          :value="depth3Item.value"
                                          variant="mark"
                                          align="left"
                                          :model-value="
                                            subAgrees4.includes(
                                              depth3Item.value
                                            )
                                          "
                                          class="agree-item__checkbox item-checkbox__sub"
                                          @update:model-value="
                                            onToggleSub4(
                                              depth3Item.value,
                                              $event
                                            )
                                          "
                                          @click.stop
                                        >
                                          <template #label>
                                            <span
                                              class="agree-item__label item-label__sub"
                                              >{{ depth3Item.label }}</span
                                            >
                                          </template>
                                        </Checkbox>
                                      </div>
                                    </li>
                                  </ul>
                                  <!-- 자세히보기 링크 -->
                                  <div class="agree-depth__link">
                                    <TextButton
                                      class="agree-depth__link"
                                      color="secondary"
                                      size="small"
                                      text="자세히보기"
                                      showGoTo
                                    />
                                  </div>
                                </div>

                                <!-- 3뎁스 영역: 카드 및 금융상품 ・ 서비스 이외의 부수서비스 안내 등을 위한 수집 ・ 이용 -->
                                <template
                                  v-else-if="depth2Item.value === 's4-2-7'"
                                >
                                  <ul
                                    class="agree-sublist agree-sublist__depth3"
                                  >
                                    <li
                                      v-for="depth3Item in subItemsDepth3_s4_2_7"
                                      :key="depth3Item.value"
                                      class="agree-subitem agree-subitem__depth3"
                                    >
                                      <div class="agree-item agree-item__sub">
                                        <Checkbox
                                          :value="depth3Item.value"
                                          variant="mark"
                                          align="left"
                                          :model-value="
                                            subAgrees4.includes(
                                              depth3Item.value
                                            )
                                          "
                                          class="agree-item__checkbox item-checkbox__sub"
                                          @update:model-value="
                                            onToggleSub4(
                                              depth3Item.value,
                                              $event
                                            )
                                          "
                                          @click.stop
                                        >
                                          <template #label>
                                            <span
                                              class="agree-item__label item-label__sub"
                                              >{{ depth3Item.label }}</span
                                            >
                                          </template>
                                        </Checkbox>
                                      </div>
                                    </li>
                                  </ul>
                                  <!-- 자세히보기 링크 -->
                                  <div class="agree-depth__link">
                                    <TextButton
                                      class="agree-depth__link"
                                      color="secondary"
                                      size="small"
                                      text="자세히보기"
                                      showGoTo
                                    />
                                  </div>
                                </template>

                                <!-- 3뎁스 영역: 전자적 전송매체를 통한 광고성 정보 수신동의 -->
                                <div
                                  v-else-if="depth2Item.value === 's4-2-8'"
                                  class="agree-depth"
                                >
                                  <Card
                                    variant="solid"
                                    color="gray"
                                    class="agree-details"
                                  >
                                    <ul class="agree-sublist" role="group">
                                      <li
                                        v-for="depth3Item in subItemsDepth3_s4_2_8"
                                        :key="depth3Item.value"
                                        class="agree-subitem agree-subitem__depth3"
                                      >
                                        <div class="agree-item agree-item__sub">
                                          <Checkbox
                                            :value="depth3Item.value"
                                            variant="mark"
                                            align="left"
                                            :model-value="
                                              subAgrees4.includes(
                                                depth3Item.value
                                              )
                                            "
                                            class="agree-item__checkbox item-checkbox__sub"
                                            @update:model-value="
                                              onToggleSub4(
                                                depth3Item.value,
                                                $event
                                              )
                                            "
                                            @click.stop
                                          >
                                            <template #label>
                                              <span
                                                class="agree-item__label item-label__sub"
                                                >{{ depth3Item.label }}</span
                                              >
                                            </template>
                                          </Checkbox>
                                        </div>
                                      </li>
                                    </ul>
                                  </Card>
                                  <!-- 설명 텍스트 -->
                                  <UnorderedList class="mt-md mb-md">
                                    <UnorderedListItem
                                      variant="bullet"
                                      size="small"
                                      text="카드상품과 부수서비스의 안내 및 이용권유에 셨더라도 신용정보의 이용 및 보호에 관한 법률에 따라 이용권유 목적의 연락에 대한 중단을 언제라도 카드사에 요청할 수 있습니다. (대표전화 : 1544-7000 / 홈페이지 : www.shinhancard.com)"
                                    />
                                    <UnorderedListItem
                                      variant="bullet"
                                      size="small"
                                      text="갱신 및 상품서비스 변경 안내 등 필수 고지사항은 상기 동의 대상에서 제외됩니다."
                                    />
                                  </UnorderedList>
                                </div>

                                <!-- 3뎁스 영역: 신한금융 자회사 및 손자회사에 개인(신용)정보를 제공 (s4-2-9) -->
                                <div
                                  v-else-if="depth2Item.value === 's4-2-9'"
                                  class="agree-depth"
                                >
                                  <ul
                                    class="agree-sublist agree-sublist__depth3"
                                  >
                                    <li
                                      v-for="depth3Item in subItemsDepth3_s4_2_9"
                                      :key="depth3Item.value"
                                      class="agree-subitem agree-subitem__depth3"
                                    >
                                      <div class="agree-item agree-item__sub">
                                        <Checkbox
                                          :value="depth3Item.value"
                                          variant="mark"
                                          align="left"
                                          :model-value="
                                            subAgrees4.includes(
                                              depth3Item.value
                                            )
                                          "
                                          class="agree-item__checkbox item-checkbox__sub"
                                          @update:model-value="
                                            onToggleSub4(
                                              depth3Item.value,
                                              $event
                                            )
                                          "
                                          @click.stop
                                        >
                                          <template #label>
                                            <span
                                              class="agree-item__label item-label__sub"
                                              >{{ depth3Item.label }}</span
                                            >
                                          </template>
                                        </Checkbox>
                                      </div>
                                    </li>
                                  </ul>
                                  <!-- 자세히보기 링크 -->
                                  <div class="agree-depth__link">
                                    <TextButton
                                      class="agree-depth__link"
                                      color="secondary"
                                      size="small"
                                      text="자세히보기"
                                      showGoTo
                                    />
                                  </div>
                                </div>
                              </div>
                            </SolidListAccordion>
                          </template>

                          <!-- 일반 항목 -->
                          <div v-else class="agree-item agree-item__sub">
                            <Checkbox
                              :value="depth2Item.value"
                              variant="mark"
                              align="left"
                              :model-value="
                                subAgrees4.includes(depth2Item.value)
                              "
                              class="agree-item__checkbox item-checkbox__sub"
                              @update:model-value="
                                onToggleSub4(depth2Item.value, $event)
                              "
                              @click.stop
                            >
                              <template #label>
                                <span
                                  class="agree-item__label item-label__sub"
                                  >{{ depth2Item.label }}</span
                                >
                                <template v-if="depth2Item.grade">
                                  <br />
                                  <SolidLabel
                                    :color="depth2Item.grade"
                                    :title="
                                      depth2Item.grade === 'cyan'
                                        ? '안심'
                                        : depth2Item.grade === 'green'
                                          ? '다소안심'
                                          : depth2Item.grade === 'yellow'
                                            ? '보통'
                                            : depth2Item.grade === 'orange'
                                              ? '신중'
                                              : '주의'
                                    "
                                    :aria-label="`동의등급제 ${
                                      depth2Item.grade === 'cyan'
                                        ? '안심'
                                        : depth2Item.grade === 'green'
                                          ? '다소안심'
                                          : depth2Item.grade === 'yellow'
                                            ? '보통'
                                            : depth2Item.grade === 'orange'
                                              ? '신중'
                                              : '주의'
                                    }`"
                                  />
                                </template>
                              </template>
                            </Checkbox>
                            <IconButton
                              iconName="Chevron_right"
                              size="small"
                              :aria-label="`${depth2Item.label} 상세 보기`"
                              class="agree-subitem__trigger"
                            />
                          </div>
                          <!-- 서브텍스트: 회원 가입 및 발권신청 동의 -->
                          <div
                            v-if="depth2Item.value === 's4-2-10'"
                            class="agree-subitem padding-lg"
                          >
                            <p class="agree-subtext">
                              본인은 카드 실제 소유자와 동일하며, 위 기재된
                              사실과 다름이 없음을 확인하고 회원가입을
                              신청합니다.
                            </p>
                          </div>
                        </li>
                      </ul>
                    </div>
                    <div v-else-if="item.value === 's4-3'" class="agree-depth">
                      <!-- ======================================== -->
                      <!-- 2뎁스 영역: 온라인 회원 이용약관 -->
                      <!-- ======================================== -->
                      <ul class="agree-sublist agree-sublist__depth2">
                        <li
                          v-for="depth2Item in subItemsDepth2_s4_3"
                          :key="depth2Item.value"
                          class="agree-subitem agree-subitem__depth2"
                        >
                          <div class="agree-item agree-item__sub">
                            <Checkbox
                              :value="depth2Item.value"
                              variant="mark"
                              align="left"
                              :model-value="
                                subAgrees4.includes(depth2Item.value)
                              "
                              class="agree-item__checkbox item-checkbox__sub"
                              @update:model-value="
                                onToggleSub4(depth2Item.value, $event)
                              "
                              @click.stop
                            >
                              <template #label>
                                <span
                                  class="agree-item__label item-label__sub"
                                  >{{ depth2Item.label }}</span
                                >
                              </template>
                            </Checkbox>
                            <IconButton
                              iconName="Chevron_right"
                              size="small"
                              :aria-label="`${depth2Item.label} 상세 보기`"
                              class="agree-subitem__trigger"
                            />
                          </div>
                        </li>
                      </ul>
                    </div>
                    <div v-else-if="item.value === 's4-4'" class="agree-depth">
                      <!-- ======================================== -->
                      <!-- 동의등급제 안내 -->
                      <!-- ======================================== -->
                      <Card
                        variant="solid"
                        color="gray"
                        class="agree-info__card card-white"
                      >
                        <div class="info-card__header">
                          <p class="info-card__title">동의등급제 안내</p>
                        </div>
                        <div class="info-card__content">
                          <div class="label-group">
                            <!-- [251016] 안심 color 변경 blue에서 color="cyan" -->
                            <!-- <SolidLabel
                              color="blue"
                              title="안심"
                            /> -->
                            <SolidLabel color="cyan" title="안심" />
                            <SolidLabel color="green" title="다소안심" />
                            <SolidLabel color="yellow" title="보통" />
                            <SolidLabel color="orange" title="신중" />
                            <SolidLabel color="red" title="주의" />
                          </div>
                          <UnorderedList>
                            <UnorderedListItem
                              variant="bullet"
                              size="small"
                              text="동의등급제는 개인(신용) 선택적 동의 항목에 대해 사생활의 비밀과 자유를 침해할 위험, 이익이나 혜택, 등의 내용의 명확성 등을 고려하여 5가지 등급을 부여하는 제도입니다."
                            />
                          </UnorderedList>
                        </div>
                      </Card>

                      <!-- ======================================== -->
                      <!-- 2뎁스 영역: 신한 슈퍼SOL 이용약관 -->
                      <!-- ======================================== -->
                      <ul class="agree-sublist agree-sublist__depth2">
                        <li
                          v-for="depth2Item in subItemsDepth2_s4_4"
                          :key="depth2Item.value"
                          class="agree-subitem agree-subitem__depth2"
                        >
                          <!-- 아코디언이 있는 항목 -->
                          <template v-if="depth2Item.accordion">
                            <SolidListAccordion
                              class="agree-subitem__accordion accordion-depth2"
                              :rowClickable="false"
                              :value="depth2Item.value"
                              v-model:isExpanded="
                                subAccordionState4[depth2Item.value]
                              "
                            >
                              <template #title>
                                <div class="agree-item agree-item__sub">
                                  <Checkbox
                                    :value="depth2Item.value"
                                    variant="mark"
                                    align="left"
                                    :model-value="
                                      subAgrees4.includes(depth2Item.value)
                                    "
                                    class="agree-item__checkbox item-checkbox__sub"
                                    @update:model-value="
                                      onToggleSub4(depth2Item.value, $event)
                                    "
                                    @click.stop
                                  >
                                    <template #label>
                                      <span
                                        class="agree-item__label item-label__sub"
                                        >{{ depth2Item.label }}</span
                                      >
                                    </template>
                                  </Checkbox>
                                </div>
                              </template>
                              <div class="agree-subitem__panel">
                                <!-- 3뎁스 영역: 전자금융서비스 이용동의(신한은행) -->
                                <div
                                  v-if="depth2Item.value === 's4-4-5'"
                                  class="agree-depth"
                                >
                                  <Card
                                    variant="solid"
                                    color="gray"
                                    class="agree-details"
                                  >
                                    <ul class="agree-sublist" role="group">
                                      <li
                                        v-for="depth3Item in subItemsDepth3_s4_4_5"
                                        :key="depth3Item.value"
                                        class="agree-subitem agree-subitem__depth3"
                                      >
                                        <div class="agree-item agree-item__sub">
                                          <span
                                            class="agree-item__label item-label__sub"
                                            >{{ depth3Item.label }}</span
                                          >
                                          <IconButton
                                            iconName="Chevron_right"
                                            size="small"
                                            :aria-label="`${depth3Item.label} 상세 보기`"
                                            class="agree-subitem__trigger"
                                          />
                                        </div>
                                      </li>
                                    </ul>
                                  </Card>
                                </div>

                                <!-- 3뎁스 영역: 광고성 전자적 수신매체 전송 동의 -->
                                <div
                                  v-else-if="depth2Item.value === 's4-4-10'"
                                  class="agree-depth"
                                >
                                  <Card
                                    variant="solid"
                                    color="gray"
                                    class="agree-details"
                                  >
                                    <ul class="agree-sublist" role="group">
                                      <li
                                        v-for="depth3Item in subItemsDepth3_s4_4_10"
                                        :key="depth3Item.value"
                                        class="agree-subitem agree-subitem__depth3"
                                      >
                                        <div class="agree-item agree-item__sub">
                                          <Checkbox
                                            :value="depth3Item.value"
                                            variant="mark"
                                            align="left"
                                            :model-value="
                                              subAgrees4.includes(
                                                depth3Item.value
                                              )
                                            "
                                            class="agree-item__checkbox item-checkbox__sub"
                                            @update:model-value="
                                              onToggleSub4(
                                                depth3Item.value,
                                                $event
                                              )
                                            "
                                            @click.stop
                                          >
                                            <template #label>
                                              <span
                                                class="agree-item__label item-label__sub"
                                                >{{ depth3Item.label }}</span
                                              >
                                            </template>
                                          </Checkbox>
                                        </div>
                                      </li>
                                    </ul>
                                  </Card>
                                </div>
                              </div>
                            </SolidListAccordion>
                          </template>

                          <!-- 일반 항목 -->
                          <div v-else class="agree-item agree-item__sub">
                            <Checkbox
                              :value="depth2Item.value"
                              variant="mark"
                              align="left"
                              :model-value="
                                subAgrees4.includes(depth2Item.value)
                              "
                              class="agree-item__checkbox item-checkbox__sub"
                              @update:model-value="
                                onToggleSub4(depth2Item.value, $event)
                              "
                              @click.stop
                            >
                              <template #label>
                                <span
                                  class="agree-item__label item-label__sub"
                                  >{{ depth2Item.label }}</span
                                >
                                <template
                                  v-if="
                                    depth2Item.value === 's4-4-8' ||
                                    depth2Item.value === 's4-4-9'
                                  "
                                >
                                  <br />
                                  <SolidLabel
                                    color="cyan"
                                    title="안심"
                                    aria-label="동의등급제 안심"
                                  />
                                </template>
                              </template>
                            </Checkbox>
                            <IconButton
                              iconName="Chevron_right"
                              size="small"
                              :aria-label="`${depth2Item.label} 상세 보기`"
                              class="agree-subitem__trigger"
                            />
                          </div>
                        </li>
                      </ul>
                    </div>
                    <div v-else-if="item.value === 's4-5'" class="agree-depth">
                      <!-- ======================================== -->
                      <!-- 2뎁스 영역: 전자문서 서비스 이용약관 -->
                      <!-- ======================================== -->
                      <ul class="agree-sublist agree-sublist__depth2">
                        <li
                          v-for="depth2Item in subItemsDepth2_s4_5"
                          :key="depth2Item.value"
                          class="agree-subitem agree-subitem__depth2"
                        >
                          <div class="agree-item agree-item__sub">
                            <Checkbox
                              :value="depth2Item.value"
                              variant="mark"
                              align="left"
                              :model-value="
                                subAgrees4.includes(depth2Item.value)
                              "
                              class="agree-item__checkbox item-checkbox__sub"
                              @update:model-value="
                                onToggleSub4(depth2Item.value, $event)
                              "
                              @click.stop
                            >
                              <template #label>
                                <span
                                  class="agree-item__label item-label__sub"
                                  >{{ depth2Item.label }}</span
                                >
                              </template>
                            </Checkbox>
                            <IconButton
                              iconName="Chevron_right"
                              size="small"
                              :aria-label="`${depth2Item.label} 상세 보기`"
                              class="agree-subitem__trigger"
                            />
                          </div>
                        </li>
                      </ul>
                    </div>
                    <div v-else-if="item.value === 's4-6'" class="agree-depth">
                      <!-- ======================================== -->
                      <!-- 2뎁스 영역: 마이데이터 서비스 이용약관 -->
                      <!-- ======================================== -->
                      <ul class="agree-sublist agree-sublist__depth2">
                        <li
                          v-for="depth2Item in subItemsDepth2_s4_6"
                          :key="depth2Item.value"
                          class="agree-subitem agree-subitem__depth2"
                        >
                          <div class="agree-item agree-item__sub">
                            <Checkbox
                              :value="depth2Item.value"
                              variant="mark"
                              align="left"
                              :model-value="
                                subAgrees4.includes(depth2Item.value)
                              "
                              class="agree-item__checkbox item-checkbox__sub"
                              @update:model-value="
                                onToggleSub4(depth2Item.value, $event)
                              "
                              @click.stop
                            >
                              <template #label>
                                <span
                                  class="agree-item__label item-label__sub"
                                  >{{ depth2Item.label }}</span
                                >
                              </template>
                            </Checkbox>
                            <IconButton
                              iconName="Chevron_right"
                              size="small"
                              :aria-label="`${depth2Item.label} 상세 보기`"
                              class="agree-subitem__trigger"
                            />
                          </div>
                        </li>
                      </ul>

                      <!-- 개인정보 처리방침 링크 -->
                      <div class="agree-depth__link">
                        <TextButton
                          class="agree-depth__link"
                          color="secondary"
                          size="small"
                          text="개인정보 처리방침"
                          showGoTo
                        />
                      </div>
                    </div>
                    <div v-else-if="item.value === 's4-7'" class="agree-depth">
                      <!-- ======================================== -->
                      <!-- 2뎁스 영역: 마케팅 동의 이용약관 -->
                      <!-- ======================================== -->
                      <ul class="agree-sublist agree-sublist__depth2">
                        <!-- 동의등급제 안내 -->
                        <li class="agree-subitem agree-subitem__depth2">
                          <Card
                            variant="solid"
                            color="gray"
                            class="agree-info__card card-white"
                          >
                            <div class="info-card__header">
                              <p class="info-card__title">동의등급제 안내</p>
                            </div>
                            <div class="info-card__content">
                              <div class="label-group">
                                <SolidLabel color="cyan" title="안심" />
                                <SolidLabel color="green" title="다소안심" />
                                <SolidLabel color="yellow" title="보통" />
                                <SolidLabel color="orange" title="신중" />
                                <SolidLabel color="red" title="주의" />
                              </div>
                              <UnorderedList>
                                <UnorderedListItem
                                  variant="bullet"
                                  size="small"
                                  text="동의등급제는 개인(신용) 선택적 동의 항목에 대해 사생활의 비밀과 자유를 침해할 위험, 이익이나 혜택, 등의 내용의 명확성 등을 고려하여 5가지 등급을 부여하는 제도입니다."
                                />
                              </UnorderedList>
                            </div>
                          </Card>
                        </li>
                        <!-- 동의등급제 안내 이후 추가 항목들 -->
                        <li
                          v-for="depth2Item in subItemsDepth2_s4_7_after"
                          :key="depth2Item.value"
                          class="agree-subitem agree-subitem__depth2"
                          :class="{
                            'agree-subitem__accordion': Boolean(
                              depth2Item.accordion
                            ),
                          }"
                        >
                          <!-- 아코디언이 있는 항목 -->
                          <template v-if="depth2Item.accordion">
                            <SolidListAccordion
                              class="agree-subitem__accordion accordion-depth2"
                              :rowClickable="false"
                              :value="depth2Item.value"
                              v-model:isExpanded="
                                subAccordionState4[depth2Item.value]
                              "
                            >
                              <template #title>
                                <div class="agree-item agree-item__sub">
                                  <Checkbox
                                    :value="depth2Item.value"
                                    variant="mark"
                                    align="left"
                                    :model-value="
                                      subAgrees4.includes(depth2Item.value)
                                    "
                                    class="agree-item__checkbox item-checkbox__sub"
                                    @update:model-value="
                                      onToggleSub4(depth2Item.value, $event)
                                    "
                                    @click.stop
                                  >
                                    <template #label>
                                      <span
                                        class="agree-item__label item-label__sub"
                                        >{{ depth2Item.label }}</span
                                      >
                                      <template v-if="depth2Item.grade">
                                        <br />
                                        <SolidLabel
                                          :color="depth2Item.grade"
                                          :title="
                                            depth2Item.grade === 'cyan'
                                              ? '안심'
                                              : depth2Item.grade === 'green'
                                                ? '다소안심'
                                                : depth2Item.grade === 'yellow'
                                                  ? '보통'
                                                  : depth2Item.grade ===
                                                      'orange'
                                                    ? '신중'
                                                    : '주의'
                                          "
                                          :aria-label="`동의등급제 ${
                                            depth2Item.grade === 'cyan'
                                              ? '안심'
                                              : depth2Item.grade === 'green'
                                                ? '다소안심'
                                                : depth2Item.grade === 'yellow'
                                                  ? '보통'
                                                  : depth2Item.grade ===
                                                      'orange'
                                                    ? '신중'
                                                    : '주의'
                                          }`"
                                        />
                                      </template>
                                    </template>
                                  </Checkbox>
                                </div>
                              </template>
                              <div class="agree-subitem__panel">
                                <!-- 3뎁스 영역: 카드 및 금융상품 ・ 서비스 안내 및 이용권유를 위한 수집 ・ 이용 -->
                                <div
                                  v-if="depth2Item.value === 's4-2-6'"
                                  class="agree-depth"
                                >
                                  <ul
                                    class="agree-sublist agree-sublist__depth3"
                                  >
                                    <li
                                      v-for="depth3Item in subItemsDepth3_s4_2_6"
                                      :key="depth3Item.value"
                                      class="agree-subitem agree-subitem__depth3"
                                    >
                                      <div class="agree-item agree-item__sub">
                                        <Checkbox
                                          :value="depth3Item.value"
                                          variant="mark"
                                          align="left"
                                          :model-value="
                                            subAgrees4.includes(
                                              depth3Item.value
                                            )
                                          "
                                          class="agree-item__checkbox item-checkbox__sub"
                                          @update:model-value="
                                            onToggleSub4(
                                              depth3Item.value,
                                              $event
                                            )
                                          "
                                          @click.stop
                                        >
                                          <template #label>
                                            <span
                                              class="agree-item__label item-label__sub"
                                              >{{ depth3Item.label }}</span
                                            >
                                          </template>
                                        </Checkbox>
                                      </div>
                                    </li>
                                  </ul>
                                  <!-- 자세히보기 링크 -->
                                  <div class="agree-depth__link">
                                    <TextButton
                                      class="agree-depth__link"
                                      color="secondary"
                                      size="small"
                                      text="자세히보기"
                                      showGoTo
                                    />
                                  </div>
                                </div>

                                <!-- 3뎁스 영역: 카드 및 금융상품 ・ 서비스 이외의 부수서비스 안내 등을 위한 수집 ・ 이용 -->
                                <template
                                  v-else-if="depth2Item.value === 's4-2-7'"
                                >
                                  <ul
                                    class="agree-sublist agree-sublist__depth3"
                                  >
                                    <li
                                      v-for="depth3Item in subItemsDepth3_s4_2_7"
                                      :key="depth3Item.value"
                                      class="agree-subitem agree-subitem__depth3"
                                    >
                                      <div class="agree-item agree-item__sub">
                                        <Checkbox
                                          :value="depth3Item.value"
                                          variant="mark"
                                          align="left"
                                          :model-value="
                                            subAgrees4.includes(
                                              depth3Item.value
                                            )
                                          "
                                          class="agree-item__checkbox item-checkbox__sub"
                                          @update:model-value="
                                            onToggleSub4(
                                              depth3Item.value,
                                              $event
                                            )
                                          "
                                          @click.stop
                                        >
                                          <template #label>
                                            <span
                                              class="agree-item__label item-label__sub"
                                              >{{ depth3Item.label }}</span
                                            >
                                          </template>
                                        </Checkbox>
                                      </div>
                                    </li>
                                  </ul>
                                  <!-- 자세히보기 링크 -->
                                  <div class="agree-depth__link">
                                    <TextButton
                                      class="agree-depth__link"
                                      color="secondary"
                                      size="small"
                                      text="자세히보기"
                                      showGoTo
                                    />
                                  </div>
                                </template>

                                <!-- 3뎁스 영역: 전자적 전송매체를 통한 광고성 정보 수신동의 -->
                                <div
                                  v-else-if="depth2Item.value === 's4-2-8'"
                                  class="agree-depth"
                                >
                                  <Card
                                    variant="solid"
                                    color="gray"
                                    class="agree-details"
                                  >
                                    <ul class="agree-sublist" role="group">
                                      <li
                                        v-for="depth3Item in subItemsDepth3_s4_2_8"
                                        :key="depth3Item.value"
                                        class="agree-subitem agree-subitem__depth3"
                                      >
                                        <div class="agree-item agree-item__sub">
                                          <Checkbox
                                            :value="depth3Item.value"
                                            variant="mark"
                                            align="left"
                                            :model-value="
                                              subAgrees4.includes(
                                                depth3Item.value
                                              )
                                            "
                                            class="agree-item__checkbox item-checkbox__sub"
                                            @update:model-value="
                                              onToggleSub4(
                                                depth3Item.value,
                                                $event
                                              )
                                            "
                                            @click.stop
                                          >
                                            <template #label>
                                              <span
                                                class="agree-item__label item-label__sub"
                                                >{{ depth3Item.label }}</span
                                              >
                                            </template>
                                          </Checkbox>
                                        </div>
                                      </li>
                                    </ul>
                                  </Card>
                                  <!-- 설명 텍스트 -->
                                  <UnorderedList class="mt-md mb-md">
                                    <UnorderedListItem
                                      variant="bullet"
                                      size="small"
                                      text="카드상품과 부수서비스의 안내 및 이용권유에 셨더라도 신용정보의 이용 및 보호에 관한 법률에 따라 이용권유 목적의 연락에 대한 중단을 언제라도 카드사에 요청할 수 있습니다. (대표전화 : 1544-7000 / 홈페이지 : www.shinhancard.com)"
                                    />
                                    <UnorderedListItem
                                      variant="bullet"
                                      size="small"
                                      text="갱신 및 상품서비스 변경 안내 등 필수 고지사항은 상기 동의 대상에서 제외됩니다."
                                    />
                                  </UnorderedList>
                                </div>

                                <!-- 3뎁스 영역: 신한금융 자회사 및 손자회사에 개인(신용)정보를 제공 (s4-2-9) -->
                                <div
                                  v-else-if="depth2Item.value === 's4-2-9'"
                                  class="agree-depth"
                                >
                                  <ul
                                    class="agree-sublist agree-sublist__depth3"
                                  >
                                    <li
                                      v-for="depth3Item in subItemsDepth3_s4_2_9"
                                      :key="depth3Item.value"
                                      class="agree-subitem agree-subitem__depth3"
                                    >
                                      <div class="agree-item agree-item__sub">
                                        <Checkbox
                                          :value="depth3Item.value"
                                          variant="mark"
                                          align="left"
                                          :model-value="
                                            subAgrees4.includes(
                                              depth3Item.value
                                            )
                                          "
                                          class="agree-item__checkbox item-checkbox__sub"
                                          @update:model-value="
                                            onToggleSub4(
                                              depth3Item.value,
                                              $event
                                            )
                                          "
                                          @click.stop
                                        >
                                          <template #label>
                                            <span
                                              class="agree-item__label item-label__sub"
                                              >{{ depth3Item.label }}</span
                                            >
                                          </template>
                                        </Checkbox>
                                      </div>
                                    </li>
                                  </ul>
                                  <!-- 자세히보기 링크 -->
                                  <div class="agree-depth__link">
                                    <TextButton
                                      class="agree-depth__link"
                                      color="secondary"
                                      size="small"
                                      text="자세히보기"
                                      showGoTo
                                    />
                                  </div>
                                </div>
                              </div>
                            </SolidListAccordion>
                          </template>
                        </li>
                      </ul>
                    </div>
                  </div>
                </SolidListAccordion>
              </template>
              <template v-else>
                <div
                  class="agree-item agree-item__sub"
                  :class="{ 'is-checked': subAgrees4.includes(item.value) }"
                >
                  <Checkbox
                    :value="item.value"
                    variant="box"
                    align="left"
                    :model-value="subAgrees4.includes(item.value)"
                    class="agree-item__checkbox item-checkbox__sub"
                    @update:model-value="onToggleSub4(item.value, $event)"
                    @click.stop
                  >
                    <template #label>
                      <span class="agree-item__label item-label__sub">{{
                        item.label
                      }}</span>
                    </template>
                  </Checkbox>
                  <IconButton
                    iconName="Chevron_right"
                    size="small"
                    :aria-label="`${item.label} 상세 보기`"
                    class="agree-subitem__trigger"
                  />
                </div>
              </template>
            </div>
          </div>
        </div>
      </div>
    </section>
  </div>

  <!-- 하단 고정으로 들어가는 부분 위치 수정 -->
  <div class="sc-contents__foot">
    <Divider variant="group" color="tertiary" />

    <div class="sc-bottom-info__inner">
      <h2 class="sc-bottom-info__title">마이데이터 서비스 안내</h2>
      <div class="sc-bottom-info__details">
        <UnorderedList>
          <UnorderedListItem
            variant="bullet"
            text="잘 이용하지 않는 서비스는 탈퇴 후 내 정보를 삭제할 수 있어요."
          />
          <UnorderedListItem
            variant="bullet"
            text="나의 마이데이터 서비스 가입현황은 마이데이터 종합포털에서 확인할 수 있어요."
          />
        </UnorderedList>
      </div>
      <!-- [251027] 마이데이터 서비스 안내 하단 링크 추가 -->
      <div class="agree-depth__link">
        <TextButton
          class="agree-depth__link"
          color="secondary"
          size="small"
          text="종합포털 바로가기"
          showGoTo
        />
      </div>
    </div>
  </div>

  <BottomActionContainer :scrollDim="true">
    <BoxButtonGroup size="xlarge" variant="100">
      <BoxButton text="확인" :disabled="!basicAgree4" />
    </BoxButtonGroup>
  </BottomActionContainer>
</template>

<script setup>
import {
  BottomActionContainer,
  BoxButton,
  BoxButtonGroup,
  Card,
  Checkbox,
  Divider,
  IconButton,
  SolidLabel,
  SolidListAccordion,
  TextButton,
  UnorderedList,
  UnorderedListItem,
} from "@shc-nss/ui/solid";
import { computed, reactive, ref, watch } from "vue";
import { useRoute } from "vue-router";

const route = useRoute();
const bodyTitle = computed(() => route.meta?.title || "");

/**
 * 유형 4 : 약관동의 기본형
 */
const basicItem4 = {
  label: "약관 전체 동의",
};

// JavaScript/TypeScript 호환을 위한 타입 정의 (선택사항)

// JavaScript/TypeScript 호환 배열
const subItems4 = [
  {
    label: "[필수/선택] 서비스 이용약관",
    value: "s4-1",
    accordion: true,
  },
  {
    label: "[필수/선택] 신한Pay머니 이용약관",
    value: "s4-2",
    accordion: true,
  },
  {
    label: "[선택] 온라인 회원 이용약관",
    value: "s4-3",
    accordion: true,
  },
  {
    label: "[선택] 신한 슈퍼SOL 이용약관",
    value: "s4-4",
    accordion: true,
  },
  {
    label: "[선택] 전자문서 서비스 이용약관",
    value: "s4-5",
    accordion: true,
  },
  {
    label: "[선택] 마이데이터 서비스 이용약관",
    value: "s4-6",
    accordion: true,
  },
  {
    label: "[선택] 마케팅 동의 이용약관",
    value: "s4-7",
    accordion: true,
  },
];

// 2뎁스 항목들 - 서비스 이용약관 (s4-1)
const subItemsDepth2_s4_1 = [
  { label: "[필수] 앱카드 서비스 이용약관 동의", value: "s4-1-1" },
  { label: "[필수] 개인(신용)정보의 수집 및 이용동의", value: "s4-1-2" },
  { label: "[필수] 고유식별정보처리 동의", value: "s4-1-3" },
  {
    label: "[선택] 위치기반 서비스 약관동의",
    value: "s4-1-4",
    accordion: true,
  },
  { label: "[선택] 앱(APP) 알림 수신동의", value: "s4-1-5", accordion: true },
];

// 2뎁스 항목들 - 신한Pay머니 이용약관 (s4-2)
const subItemsDepth2_s4_2 = [
  { label: "[필수] 신한Pay머니 이용약관동의", value: "s4-2-1" },
  { label: "[필수] 개인정보 수집 및 이용동의", value: "s4-2-2" },
  { label: "[필수] 고유식별정보처리 동의", value: "s4-2-3" },
  { label: "[필수] 개인(신용)정보 제공동의", value: "s4-2-4" },
  { label: "[필수] 고유식별정보 제공동의", value: "s4-2-5" },
];

// 2뎁스 항목들 - 신한Pay머니 이용약관 동의등급제 이후 항목들 (s4-2)
const subItemsDepth2_s4_2_after = [
  {
    label:
      "[선택] 카드 및 금융상품 ・ 서비스 안내 및 이용권유를 위한 수집 ・ 이용",
    value: "s4-2-6",
    grade: "green", // 다소안심
    accordion: true,
  },
  {
    label:
      "[선택] 카드 및 금융상품 ・ 서비스 이외의 부수서비스 안내 등을 위한 수집 ・ 이용",
    value: "s4-2-7",
    grade: "yellow", // 보통
    accordion: true,
  },
  {
    label: "[선택] 전자적 전송매체를 통한 광고성 정보 수신동의",
    value: "s4-2-8",
    accordion: true,
  },
  {
    label: "[선택] 신한금융 자회사 및 손자회사에 개인(신용)정보를 제공",
    value: "s4-2-9",
    grade: "cyan", // 안심
    accordion: true,
  },
  { label: "[필수] 회원 가입 및 발권신청 동의", value: "s4-2-10" },
];

// 2뎁스 항목들 - 온라인 회원 이용약관 (s4-3)
const subItemsDepth2_s4_3 = [
  { label: "[필수] 온라인 회원 이용약관동의", value: "s4-3-1" },
  { label: "[필수] 개인정보 필수적 수집・이용동의서", value: "s4-3-2" },
];

// 2뎁스 항목들 - 신한 슈퍼SOL 이용약관 (s4-4)
const subItemsDepth2_s4_4 = [
  { label: "[필수] 신한 모바일 플랫폼 이용약관", value: "s4-4-1" },
  { label: "[필수] 신한금융그룹 통합 포인트 서비스 이용동의", value: "s4-4-2" },
  { label: "[필수] 개인(신용)정보 수집・이용・제공 동의", value: "s4-4-3" },
  {
    label: "[필수] 개인(신용)정보 수집・이용・제공 동의(포인트 서비스 제공)",
    value: "s4-4-4",
  },
  {
    label: "[필수] 전자금융서비스 이용동의(신한은행)",
    value: "s4-4-5",
    accordion: true,
  },
  { label: "[필수] 그룹 로열티 서비스 이용동의(신한은행)", value: "s4-4-6" },
  {
    label: "[필수] 개인(신용)정보 수집・이용・제공 동의(신한은행)",
    value: "s4-4-7",
  },
  {
    label: "[선택] 개인(신용)정보 수집・이용・제공 동의(상품 서비스 안내 등)",
    value: "s4-4-8",
  },
  {
    label:
      "[선택] 개인(신용)정보 수집・이용・제공 동의(상품 서비스 안내 등)(신한은행)",
    value: "s4-4-9",
  },
  {
    label: "[선택] 광고성 전자적 수신매체 전송 동의",
    value: "s4-4-10",
    accordion: true,
  },
];

// 3뎁스 항목들 - 전자금융서비스 이용동의(신한은행) (s4-4-5)
const subItemsDepth3_s4_4_5 = [
  { label: "전자금융거래 기본약관", value: "s4-4-5-1" },
  { label: "신한온라인서비스 이용약관", value: "s4-4-5-2" },
  { label: "전자통지서비스 이용약관", value: "s4-4-5-3" },
  { label: "개인정보 수집 이용동의(비여신 금융거래)", value: "s4-4-5-4" },
];

// 3뎁스 항목들 - 광고성 전자적 수신매체 전송 동의 (s4-4-10)
const subItemsDepth3_s4_4_10 = [
  { label: "문자", value: "s4-4-10-1" },
  { label: "이메일", value: "s4-4-10-2" },
  { label: "전화", value: "s4-4-10-3" },
];

// 3뎁스 항목들 - 위치기반 서비스 약관동의 (s4-1-4)
const subItemsDepth3_s4_1_4 = [
  { label: "신한카드 위치기반 사업자 약관동의", value: "s4-1-4-1" },
  { label: "위치정보 서비스 동의사항", value: "s4-1-4-2", accordion: true },
  { label: "개인정보 수집 및 이용동의", value: "s4-1-4-3" },
  { label: "위치기반 혜택 알림 수신동의", value: "s4-1-4-4" },
  { label: "블루칩 씨엔에스 위치정보사업자약관동의", value: "s4-1-4-5" },
];

// 3뎁스 항목들 - 앱(APP) 알림 수신동의 (s4-1-5)
const subItemsDepth3_s4_1_5 = [
  { label: "마케팅 정보 수신동의", value: "s4-1-5-1", accordion: true },
];

// 4뎁스 항목들 - 위치정보 서비스 동의사항 (s4-1-4-2)
const subItemsDepth4_s4_1_4_2 = [
  { label: "LGU+ 위치정보 사업자 약관 동의", value: "s4-1-4-2-1" },
  { label: "LGU+ 개인정보수집이용 및 제3자 제공동의", value: "s4-1-4-2-2" },
  { label: "로플렛 위치정보 사업자 약관동의", value: "s4-1-4-2-3" },
];

// 2뎁스 항목들 - 전자문서 서비스 (s4-5)
const subItemsDepth2_s4_5 = [
  { label: "[필수] 전자문서 서비스 이용약관 동의", value: "s4-5-1" },
  { label: "[필수] 전자문서 개인정보 수집・이용・동의", value: "s4-5-2" },
  { label: "[필수] 개인정보 제3자 제공 동의", value: "s4-5-3" },
  { label: "[필수] 서비스 유의사항 동의", value: "s4-5-4" },
];

// 2뎁스 항목들 - 마이데이터 서비스 (s4-6)
const subItemsDepth2_s4_6 = [
  { label: "[필수] 마이데이터 서비스 이용약관동의", value: "s4-6-1" },
  {
    label: "[필수] 마이데이터 서비스 개인(신용)정보의 수집 및 이용동의",
    value: "s4-6-2",
  },
];

// 2뎁스 항목들 - 마케팅 동의 이용약관 (s4-7)
const subItemsDepth2_s4_7_after = [
  {
    label:
      "[선택] 카드 및 금융상품 ・ 서비스 안내 및 이용권유를 위한 수집 ・ 이용",
    value: "s4-2-6",
    grade: "green", // 다소안심
    accordion: true,
  },
  {
    label:
      "[선택] 카드 및 금융상품 ・ 서비스 이외의 부수서비스 안내 등을 위한 수집 ・ 이용",
    value: "s4-2-7",
    grade: "yellow", // 보통
    accordion: true,
  },
  {
    label: "[선택] 전자적 전송매체를 통한 광고성 정보 수신동의",
    value: "s4-2-8",
    accordion: true,
  },
  {
    label: "[선택] 신한금융 자회사 및 손자회사에 개인(신용)정보를 제공",
    value: "s4-2-9",
    grade: "cyan", // 안심
    accordion: true,
  },
];

// 3뎁스 항목들 - 카드 및 금융상품 ・ 서비스 안내 및 이용권유를 위한 수집 ・ 이용 (s4-2-6)
const subItemsDepth3_s4_2_6 = [
  { label: "고유식별번호 조회 동의", value: "s4-2-6-1" },
  { label: "개인신용정보 제공 동의", value: "s4-2-6-2" },
];

// 3뎁스 항목들 - 카드 및 금융상품 ・ 서비스 이외의 부수서비스 안내 등을 위한 수집 ・ 이용 (s4-2-7)
const subItemsDepth3_s4_2_7 = [
  { label: "고유식별번호 조회 동의", value: "s4-2-7-1" },
  { label: "개인신용정보 제공 동의", value: "s4-2-7-2" },
];

// 3뎁스 항목들 - 전자적 전송매체를 통한 광고성 정보 수신동의 (s4-2-8)
const subItemsDepth3_s4_2_8 = [
  { label: "전체", value: "s4-2-8-1" },
  { label: "서면", value: "s4-2-8-2" },
  { label: "이메일", value: "s4-2-8-3" },
  { label: "전화", value: "s4-2-8-4" },
  {
    label: "휴대폰 메세지(카카오톡, 네이버 알림 등 모바일 메세지 포함)",
    value: "s4-2-8-5",
  },
];

// 3뎁스 항목들 - 신한금융 자회사 및 손자회사에 개인(신용)정보를 제공 (s4-2-9)
const subItemsDepth3_s4_2_9 = [
  { label: "개인신용정보 제공 동의", value: "s4-2-9-1" },
];

const basicAgree4 = ref(false);
const subAgrees4 = ref([]);
const subAccordionState4 = reactive({
  "s4-1": false, // 서비스 이용약관 2뎁스 아코디언 상태
  "s4-2": false, // 신한Pay머니 이용약관 2뎁스 아코디언 상태
  "s4-3": false, // 온라인 회원 이용약관 2뎁스 아코디언 상태
  "s4-4": false, // 신한 슈퍼SOL 이용약관 2뎁스 아코디언 상태
  "s4-5": false, // 전자문서 서비스 2뎁스 아코디언 상태
  "s4-6": false, // 마이데이터 서비스 2뎁스 아코디언 상태
  "s4-7": false, // 마케팅 동의 이용약관 2뎁스 아코디언 상태
  "s4-1-4": false, // 위치기반 서비스 약관동의 3뎁스 아코디언 상태
  "s4-1-5": false, // 앱(APP) 알림 수신동의 3뎁스 아코디언 상태
  "s4-1-4-2": false, // 위치정보 서비스 동의사항 4뎁스 아코디언 상태
  "s4-1-5-1": false, // 마케팅 정보 수신동의 4뎁스 아코디언 상태
  "s4-4-5": false, // 전자금융서비스 이용동의(신한은행) 3뎁스 아코디언 상태
  "s4-4-10": false, // 광고성 전자적 수신매체 전송 동의 3뎁스 아코디언 상태
  "s4-2-6": false, // 카드 및 금융상품 ・ 서비스 안내 및 이용권유를 위한 수집 ・ 이용 2뎁스 아코디언 상태
  "s4-2-7": false, // 카드 및 금융상품 ・ 서비스 이외의 부수서비스 안내 등을 위한 수집 ・ 이용 2뎁스 아코디언 상태
  "s4-2-8": false, // 전자적 전송매체를 통한 광고성 정보 수신동의 2뎁스 아코디언 상태
  "s4-2-9": false, // 신한금융 자회사 및 손자회사에 개인(신용)정보를 제공 2뎁스 아코디언 상태
});

/**
 * 동작 로직
 */
function onToggleSub4(value, checked) {
  const set = new Set(subAgrees4.value);
  if (checked) set.add(value);
  else set.delete(value);
  subAgrees4.value = Array.from(set);

  // 전체 항목 수 계산 (1뎁스 + 2뎁스 + 3뎁스 + 4뎁스)
  const totalItems =
    subItems4.length +
    subItemsDepth2_s4_1.length +
    subItemsDepth2_s4_2.length +
    subItemsDepth2_s4_2_after.length +
    subItemsDepth2_s4_3.length +
    subItemsDepth2_s4_4.length +
    subItemsDepth2_s4_5.length +
    subItemsDepth2_s4_6.length +
    subItemsDepth2_s4_7_after.length +
    subItemsDepth3_s4_1_4.length +
    subItemsDepth3_s4_1_5.length +
    subItemsDepth3_s4_2_6.length +
    subItemsDepth3_s4_2_7.length +
    subItemsDepth3_s4_2_8.length +
    subItemsDepth3_s4_2_9.length +
    subItemsDepth3_s4_4_5.length +
    subItemsDepth3_s4_4_10.length +
    subItemsDepth4_s4_1_4_2.length;
  basicAgree4.value = set.size === totalItems;
}

watch(basicAgree4, (checked) => {
  if (checked) {
    // 1뎁스 항목들 + 아코디언 내부의 모든 하위 항목들 (2뎁스 + 3뎁스 + 4뎁스)
    const allItems = [
      ...subItems4.map((item) => item.value),
      ...subItemsDepth2_s4_1.map((item) => item.value),
      ...subItemsDepth2_s4_2.map((item) => item.value),
      ...subItemsDepth2_s4_2_after.map((item) => item.value),
      ...subItemsDepth2_s4_3.map((item) => item.value),
      ...subItemsDepth2_s4_4.map((item) => item.value),
      ...subItemsDepth2_s4_5.map((item) => item.value),
      ...subItemsDepth2_s4_6.map((item) => item.value),
      ...subItemsDepth2_s4_7_after.map((item) => item.value),
      ...subItemsDepth3_s4_1_4.map((item) => item.value),
      ...subItemsDepth3_s4_1_5.map((item) => item.value),
      ...subItemsDepth3_s4_2_6.map((item) => item.value),
      ...subItemsDepth3_s4_2_7.map((item) => item.value),
      ...subItemsDepth3_s4_2_8.map((item) => item.value),
      ...subItemsDepth3_s4_2_9.map((item) => item.value),
      ...subItemsDepth3_s4_4_5.map((item) => item.value),
      ...subItemsDepth3_s4_4_10.map((item) => item.value),
      ...subItemsDepth4_s4_1_4_2.map((item) => item.value),
    ];
    subAgrees4.value = allItems;
  } else {
    subAgrees4.value = [];
  }
});
</script>




<route lang="yaml">
meta:
  id: SSN019A01
  title: 약관동의
  menu: Sign in/up > 약관동의(카드본인확인)
  layout: SubLayout
  category: Sign in/up
  publish: 김대민
  publishVersion: 0.8
  status: 재작업
  etc: |
    260105: 디자인 동기화 - 약관 체크항목 추가,
    안심 color 변경 blue에서 color=cyan,
    [251027] 마이데이터 서비스 안내 하단 링크 추가
  # 네비게이션 상세 옵션
  header:
    fixed: true
    close: true
</route>
<template>
  <!-- 콘텐츠 영역 -->
  <div class="sc-contents__body sc-agree__page">
    <section class="section">
      <div class="sc-agree__list compound" role="region">
        <div class="agree-list__group">
          <div
            class="agree-item item-basic"
            :class="{ 'is-checked': basicAgree4 }"
          >
            <Checkbox
              v-model="basicAgree4"
              class="agree-item__checkbox item-checkbox__basic"
              variant="box"
              align="left"
            >
              <template #label>
                <span class="agree-item__label item-label__basic">{{
                  basicItem4.label
                }}</span>
              </template>
            </Checkbox>
          </div>

          <!-- ======================================== -->
          <!-- 1뎁스 영역: 기본 약관 항목들 -->
          <!-- ======================================== -->
          <div class="agree-sublist" role="group">
            <div
              v-for="item in subItems4"
              :key="item.value"
              class="agree-subitem"
              :class="{ 'agree-subitem__accordion': Boolean(item.accordion) }"
            >
              <template v-if="item.accordion">
                <SolidListAccordion
                  class="agree-subitem__accordion"
                  :rowClickable="false"
                  :value="item.value"
                  v-model:isExpanded="subAccordionState4[item.value]"
                >
                  <template #title>
                    <div
                      class="agree-item agree-item__sub"
                      :class="{
                        'is-checked': subAgrees4.includes(item.value),
                      }"
                    >
                      <Checkbox
                        :value="item.value"
                        variant="box"
                        align="left"
                        :model-value="subAgrees4.includes(item.value)"
                        class="agree-item__checkbox item-checkbox__sub"
                        @update:model-value="onToggleSub4(item.value, $event)"
                        @click.stop
                      >
                        <template #label>
                          <span class="agree-item__label item-label__sub">{{
                            item.label
                          }}</span>
                        </template>
                      </Checkbox>
                    </div>
                  </template>
                  <div class="agree-subitem__panel">
                    <div v-if="item.value === 's4-1'" class="agree-depth">
                      <!-- ======================================== -->
                      <!-- 2뎁스 영역: 서비스 이용약관 -->
                      <!-- ======================================== -->
                      <ul class="agree-sublist agree-sublist__depth2">
                        <li
                          v-for="depth2Item in subItemsDepth2_s4_1"
                          :key="depth2Item.value"
                          class="agree-subitem agree-subitem__depth2"
                        >
                          <!-- 아코디언이 있는 항목 -->
                          <template v-if="depth2Item.accordion">
                            <SolidListAccordion
                              class="agree-subitem__accordion accordion-depth2"
                              :rowClickable="false"
                              :value="depth2Item.value"
                              v-model:isExpanded="
                                subAccordionState4[depth2Item.value]
                              "
                            >
                              <template #title>
                                <div class="agree-item agree-item__sub">
                                  <Checkbox
                                    :value="depth2Item.value"
                                    variant="mark"
                                    align="left"
                                    :model-value="
                                      subAgrees4.includes(depth2Item.value)
                                    "
                                    class="agree-item__checkbox item-checkbox__sub"
                                    @update:model-value="
                                      onToggleSub4(depth2Item.value, $event)
                                    "
                                    @click.stop
                                  >
                                    <template #label>
                                      <span
                                        class="agree-item__label item-label__sub"
                                        >{{ depth2Item.label }}</span
                                      >
                                    </template>
                                  </Checkbox>
                                </div>
                              </template>
                              <div class="agree-subitem__panel">
                                <!-- 3뎁스 영역: 위치기반 서비스 약관동의 -->
                                <div v-if="depth2Item.value === 's4-1-4'">
                                  <ul
                                    class="agree-sublist agree-sublist__depth3"
                                  >
                                    <li
                                      v-for="depth3Item in subItemsDepth3_s4_1_4"
                                      :key="depth3Item.value"
                                      class="agree-subitem agree-subitem__depth3"
                                    >
                                      <!-- 아코디언이 있는 3뎁스 항목 -->
                                      <template v-if="depth3Item.accordion">
                                        <SolidListAccordion
                                          class="agree-subitem__accordion accordion-depth3"
                                          :rowClickable="false"
                                          :value="depth3Item.value"
                                          v-model:isExpanded="
                                            subAccordionState4[depth3Item.value]
                                          "
                                        >
                                          <template #title>
                                            <div
                                              class="agree-item agree-item__sub"
                                            >
                                              <Checkbox
                                                :value="depth3Item.value"
                                                variant="mark"
                                                align="left"
                                                :model-value="
                                                  subAgrees4.includes(
                                                    depth3Item.value
                                                  )
                                                "
                                                class="agree-item__checkbox item-checkbox__sub"
                                                @update:model-value="
                                                  onToggleSub4(
                                                    depth3Item.value,
                                                    $event
                                                  )
                                                "
                                                @click.stop
                                              >
                                                <template #label>
                                                  <span
                                                    class="agree-item__label item-label__sub"
                                                    >{{
                                                      depth3Item.label
                                                    }}</span
                                                  >
                                                </template>
                                              </Checkbox>
                                            </div>
                                          </template>
                                          <div class="agree-subitem__panel">
                                            <!-- 4뎁스 영역: 위치정보 서비스 동의사항 상세 -->
                                            <div
                                              v-if="
                                                depth3Item.value === 's4-1-4-2'
                                              "
                                              class="outline-panel"
                                            >
                                              <Card
                                                variant="solid"
                                                color="gray"
                                                class="agree-details"
                                              >
                                                <ul
                                                  class="agree-sublist"
                                                  role="group"
                                                >
                                                  <li
                                                    v-for="depth4Item in subItemsDepth4_s4_1_4_2"
                                                    :key="depth4Item.value"
                                                    class="agree-subitem agree-subitem__depth4"
                                                  >
                                                    <div
                                                      class="agree-item agree-item__sub"
                                                    >
                                                      <Checkbox
                                                        :value="
                                                          depth4Item.value
                                                        "
                                                        variant="mark"
                                                        align="left"
                                                        :model-value="
                                                          subAgrees4.includes(
                                                            depth4Item.value
                                                          )
                                                        "
                                                        class="agree-item__checkbox item-checkbox__sub"
                                                        @update:model-value="
                                                          onToggleSub4(
                                                            depth4Item.value,
                                                            $event
                                                          )
                                                        "
                                                        @click.stop
                                                      >
                                                        <template #label>
                                                          <span
                                                            class="agree-item__label item-label__sub"
                                                            >{{
                                                              depth4Item.label
                                                            }}</span
                                                          >
                                                        </template>
                                                      </Checkbox>
                                                      <IconButton
                                                        iconName="Chevron_right"
                                                        size="small"
                                                        :aria-label="`${depth4Item.label} 상세 보기`"
                                                        class="agree-subitem__trigger"
                                                      />
                                                    </div>
                                                  </li>
                                                </ul>
                                              </Card>
                                            </div>
                                          </div>
                                        </SolidListAccordion>
                                      </template>

                                      <!-- 일반 3뎁스 항목 -->
                                      <div
                                        v-else
                                        class="agree-item agree-item__sub"
                                      >
                                        <Checkbox
                                          :value="depth3Item.value"
                                          variant="mark"
                                          align="left"
                                          :model-value="
                                            subAgrees4.includes(
                                              depth3Item.value
                                            )
                                          "
                                          class="agree-item__checkbox item-checkbox__sub"
                                          @update:model-value="
                                            onToggleSub4(
                                              depth3Item.value,
                                              $event
                                            )
                                          "
                                          @click.stop
                                        >
                                          <template #label>
                                            <span
                                              class="agree-item__label item-label__sub"
                                              >{{ depth3Item.label }}</span
                                            >
                                          </template>
                                        </Checkbox>
                                        <IconButton
                                          iconName="Chevron_right"
                                          size="small"
                                          :aria-label="`${depth3Item.label} 상세 보기`"
                                          class="agree-subitem__trigger"
                                        />
                                      </div>
                                    </li>
                                  </ul>
                                </div>

                                <!-- 3뎁스 영역: 앱(APP) 알림 수신동의 -->
                                <div v-else-if="depth2Item.value === 's4-1-5'">
                                  <ul
                                    class="agree-sublist agree-sublist__depth3"
                                  >
                                    <li
                                      v-for="depth3Item in subItemsDepth3_s4_1_5"
                                      :key="depth3Item.value"
                                      class="agree-subitem agree-subitem__depth3"
                                    >
                                      <!-- 아코디언이 있는 3뎁스 항목 -->
                                      <template v-if="depth3Item.accordion">
                                        <SolidListAccordion
                                          class="agree-subitem__accordion accordion-depth3"
                                          :rowClickable="false"
                                          :value="depth3Item.value"
                                          v-model:isExpanded="
                                            subAccordionState4[depth3Item.value]
                                          "
                                        >
                                          <template #title>
                                            <div
                                              class="agree-item agree-item__sub"
                                            >
                                              <Checkbox
                                                :value="depth3Item.value"
                                                variant="mark"
                                                align="left"
                                                :model-value="
                                                  subAgrees4.includes(
                                                    depth3Item.value
                                                  )
                                                "
                                                class="agree-item__checkbox item-checkbox__sub"
                                                @update:model-value="
                                                  onToggleSub4(
                                                    depth3Item.value,
                                                    $event
                                                  )
                                                "
                                                @click.stop
                                              >
                                                <template #label>
                                                  <span
                                                    class="agree-item__label item-label__sub"
                                                    >{{
                                                      depth3Item.label
                                                    }}</span
                                                  >
                                                </template>
                                              </Checkbox>
                                            </div>
                                          </template>
                                          <div class="agree-subitem__panel">
                                            <!-- 4뎁스 영역: 마케팅 정보 수신동의 상세 -->
                                            <div
                                              v-if="
                                                depth3Item.value === 's4-1-5-1'
                                              "
                                              class="outline-panel"
                                            >
                                              <Card
                                                variant="solid"
                                                color="gray"
                                                class="agree-details"
                                              >
                                                <UnorderedList>
                                                  <UnorderedListItem
                                                    variant="bullet"
                                                    size="small"
                                                    text="항목 : 앱(APP)을 통한 마케팅 정보 수신동의"
                                                  />
                                                  <UnorderedListItem
                                                    variant="bullet"
                                                    size="small"
                                                    text="이용목적 : 각종 이벤트, 할인, 혜택정보 등의 안내"
                                                  />
                                                  <UnorderedListItem
                                                    variant="bullet"
                                                    size="small"
                                                    text="보유기간 : 별도 동의 철회시까지"
                                                  />
                                                </UnorderedList>
                                              </Card>
                                            </div>
                                          </div>
                                        </SolidListAccordion>
                                      </template>

                                      <!-- 일반 3뎁스 항목 -->
                                      <div
                                        v-else
                                        class="agree-item agree-item__sub"
                                      >
                                        <Checkbox
                                          :value="depth3Item.value"
                                          variant="mark"
                                          align="left"
                                          :model-value="
                                            subAgrees4.includes(
                                              depth3Item.value
                                            )
                                          "
                                          class="agree-item__checkbox item-checkbox__sub"
                                          @update:model-value="
                                            onToggleSub4(
                                              depth3Item.value,
                                              $event
                                            )
                                          "
                                          @click.stop
                                        >
                                          <template #label>
                                            <span
                                              class="agree-item__label item-label__sub"
                                              >{{ depth3Item.label }}</span
                                            >
                                          </template>
                                        </Checkbox>
                                        <IconButton
                                          iconName="Chevron_right"
                                          size="small"
                                          :aria-label="`${depth3Item.label} 상세 보기`"
                                          class="agree-subitem__trigger"
                                        />
                                      </div>
                                    </li>
                                  </ul>
                                </div>
                              </div>
                            </SolidListAccordion>
                          </template>

                          <!-- 일반 항목 -->
                          <div v-else class="agree-item agree-item__sub">
                            <Checkbox
                              :value="depth2Item.value"
                              variant="mark"
                              align="left"
                              :model-value="
                                subAgrees4.includes(depth2Item.value)
                              "
                              class="agree-item__checkbox item-checkbox__sub"
                              @update:model-value="
                                onToggleSub4(depth2Item.value, $event)
                              "
                              @click.stop
                            >
                              <template #label>
                                <span
                                  class="agree-item__label item-label__sub"
                                  >{{ depth2Item.label }}</span
                                >
                              </template>
                            </Checkbox>
                            <IconButton
                              iconName="Chevron_right"
                              size="small"
                              :aria-label="`${depth2Item.label} 상세 보기`"
                              class="agree-subitem__trigger"
                            />
                          </div>
                        </li>
                      </ul>
                    </div>
                    <div v-else-if="item.value === 's4-2'" class="agree-depth">
                      <!-- ======================================== -->
                      <!-- 2뎁스 영역: 신한Pay머니 이용약관 -->
                      <!-- ======================================== -->
                      <ul class="agree-sublist agree-sublist__depth2">
                        <li
                          v-for="depth2Item in subItemsDepth2_s4_2"
                          :key="depth2Item.value"
                          class="agree-subitem agree-subitem__depth2"
                        >
                          <div class="agree-item agree-item__sub">
                            <Checkbox
                              :value="depth2Item.value"
                              variant="mark"
                              align="left"
                              :model-value="
                                subAgrees4.includes(depth2Item.value)
                              "
                              class="agree-item__checkbox item-checkbox__sub"
                              @update:model-value="
                                onToggleSub4(depth2Item.value, $event)
                              "
                              @click.stop
                            >
                              <template #label>
                                <span
                                  class="agree-item__label item-label__sub"
                                  >{{ depth2Item.label }}</span
                                >
                              </template>
                            </Checkbox>
                            <IconButton
                              iconName="Chevron_right"
                              size="small"
                              :aria-label="`${depth2Item.label} 상세 보기`"
                              class="agree-subitem__trigger"
                            />
                          </div>
                        </li>
                        <!-- 동의등급제 안내 -->
                        <li class="agree-subitem agree-subitem__depth2">
                          <Card
                            variant="solid"
                            color="gray"
                            class="agree-info__card card-white"
                          >
                            <div class="info-card__header">
                              <p class="info-card__title">동의등급제 안내</p>
                            </div>
                            <div class="info-card__content">
                              <div class="label-group">
                                <SolidLabel color="cyan" title="안심" />
                                <SolidLabel color="green" title="다소안심" />
                                <SolidLabel color="yellow" title="보통" />
                                <SolidLabel color="orange" title="신중" />
                                <SolidLabel color="red" title="주의" />
                              </div>
                              <UnorderedList>
                                <UnorderedListItem
                                  variant="bullet"
                                  size="small"
                                  text="동의등급제는 개인(신용) 선택적 동의 항목에 대해 사생활의 비밀과 자유를 침해할 위험, 이익이나 혜택, 등의 내용의 명확성 등을 고려하여 5가지 등급을 부여하는 제도입니다."
                                />
                              </UnorderedList>
                            </div>
                          </Card>
                        </li>
                        <!-- 동의등급제 안내 이후 추가 항목들 -->
                        <li
                          v-for="depth2Item in subItemsDepth2_s4_2_after"
                          :key="depth2Item.value"
                          class="agree-subitem agree-subitem__depth2"
                          :class="{
                            'agree-subitem__accordion': Boolean(
                              depth2Item.accordion
                            ),
                          }"
                        >
                          <!-- 아코디언이 있는 항목 -->
                          <template v-if="depth2Item.accordion">
                            <SolidListAccordion
                              class="agree-subitem__accordion accordion-depth2"
                              :rowClickable="false"
                              :value="depth2Item.value"
                              v-model:isExpanded="
                                subAccordionState4[depth2Item.value]
                              "
                            >
                              <template #title>
                                <div class="agree-item agree-item__sub">
                                  <Checkbox
                                    :value="depth2Item.value"
                                    variant="mark"
                                    align="left"
                                    :model-value="
                                      subAgrees4.includes(depth2Item.value)
                                    "
                                    class="agree-item__checkbox item-checkbox__sub"
                                    @update:model-value="
                                      onToggleSub4(depth2Item.value, $event)
                                    "
                                    @click.stop
                                  >
                                    <template #label>
                                      <span
                                        class="agree-item__label item-label__sub"
                                        >{{ depth2Item.label }}</span
                                      >
                                      <template v-if="depth2Item.grade">
                                        <br />
                                        <SolidLabel
                                          :color="depth2Item.grade"
                                          :title="
                                            depth2Item.grade === 'cyan'
                                              ? '안심'
                                              : depth2Item.grade === 'green'
                                                ? '다소안심'
                                                : depth2Item.grade === 'yellow'
                                                  ? '보통'
                                                  : depth2Item.grade ===
                                                      'orange'
                                                    ? '신중'
                                                    : '주의'
                                          "
                                          :aria-label="`동의등급제 ${
                                            depth2Item.grade === 'cyan'
                                              ? '안심'
                                              : depth2Item.grade === 'green'
                                                ? '다소안심'
                                                : depth2Item.grade === 'yellow'
                                                  ? '보통'
                                                  : depth2Item.grade ===
                                                      'orange'
                                                    ? '신중'
                                                    : '주의'
                                          }`"
                                        />
                                      </template>
                                    </template>
                                  </Checkbox>
                                </div>
                              </template>
                              <div class="agree-subitem__panel">
                                <!-- 3뎁스 영역: 카드 및 금융상품 ・ 서비스 안내 및 이용권유를 위한 수집 ・ 이용 -->
                                <div
                                  v-if="depth2Item.value === 's4-2-6'"
                                  class="agree-depth"
                                >
                                  <ul
                                    class="agree-sublist agree-sublist__depth3"
                                  >
                                    <li
                                      v-for="depth3Item in subItemsDepth3_s4_2_6"
                                      :key="depth3Item.value"
                                      class="agree-subitem agree-subitem__depth3"
                                    >
                                      <div class="agree-item agree-item__sub">
                                        <Checkbox
                                          :value="depth3Item.value"
                                          variant="mark"
                                          align="left"
                                          :model-value="
                                            subAgrees4.includes(
                                              depth3Item.value
                                            )
                                          "
                                          class="agree-item__checkbox item-checkbox__sub"
                                          @update:model-value="
                                            onToggleSub4(
                                              depth3Item.value,
                                              $event
                                            )
                                          "
                                          @click.stop
                                        >
                                          <template #label>
                                            <span
                                              class="agree-item__label item-label__sub"
                                              >{{ depth3Item.label }}</span
                                            >
                                          </template>
                                        </Checkbox>
                                      </div>
                                    </li>
                                  </ul>
                                  <!-- 자세히보기 링크 -->
                                  <div class="agree-depth__link">
                                    <TextButton
                                      class="agree-depth__link"
                                      color="secondary"
                                      size="small"
                                      text="자세히보기"
                                      showGoTo
                                    />
                                  </div>
                                </div>

                                <!-- 3뎁스 영역: 카드 및 금융상품 ・ 서비스 이외의 부수서비스 안내 등을 위한 수집 ・ 이용 -->
                                <template
                                  v-else-if="depth2Item.value === 's4-2-7'"
                                >
                                  <ul
                                    class="agree-sublist agree-sublist__depth3"
                                  >
                                    <li
                                      v-for="depth3Item in subItemsDepth3_s4_2_7"
                                      :key="depth3Item.value"
                                      class="agree-subitem agree-subitem__depth3"
                                    >
                                      <div class="agree-item agree-item__sub">
                                        <Checkbox
                                          :value="depth3Item.value"
                                          variant="mark"
                                          align="left"
                                          :model-value="
                                            subAgrees4.includes(
                                              depth3Item.value
                                            )
                                          "
                                          class="agree-item__checkbox item-checkbox__sub"
                                          @update:model-value="
                                            onToggleSub4(
                                              depth3Item.value,
                                              $event
                                            )
                                          "
                                          @click.stop
                                        >
                                          <template #label>
                                            <span
                                              class="agree-item__label item-label__sub"
                                              >{{ depth3Item.label }}</span
                                            >
                                          </template>
                                        </Checkbox>
                                      </div>
                                    </li>
                                  </ul>
                                  <!-- 자세히보기 링크 -->
                                  <div class="agree-depth__link">
                                    <TextButton
                                      class="agree-depth__link"
                                      color="secondary"
                                      size="small"
                                      text="자세히보기"
                                      showGoTo
                                    />
                                  </div>
                                </template>

                                <!-- 3뎁스 영역: 전자적 전송매체를 통한 광고성 정보 수신동의 -->
                                <div
                                  v-else-if="depth2Item.value === 's4-2-8'"
                                  class="agree-depth"
                                >
                                  <Card
                                    variant="solid"
                                    color="gray"
                                    class="agree-details"
                                  >
                                    <ul class="agree-sublist" role="group">
                                      <li
                                        v-for="depth3Item in subItemsDepth3_s4_2_8"
                                        :key="depth3Item.value"
                                        class="agree-subitem agree-subitem__depth3"
                                      >
                                        <div class="agree-item agree-item__sub">
                                          <Checkbox
                                            :value="depth3Item.value"
                                            variant="mark"
                                            align="left"
                                            :model-value="
                                              subAgrees4.includes(
                                                depth3Item.value
                                              )
                                            "
                                            class="agree-item__checkbox item-checkbox__sub"
                                            @update:model-value="
                                              onToggleSub4(
                                                depth3Item.value,
                                                $event
                                              )
                                            "
                                            @click.stop
                                          >
                                            <template #label>
                                              <span
                                                class="agree-item__label item-label__sub"
                                                >{{ depth3Item.label }}</span
                                              >
                                            </template>
                                          </Checkbox>
                                        </div>
                                      </li>
                                    </ul>
                                  </Card>
                                  <!-- 설명 텍스트 -->
                                  <UnorderedList class="mt-md mb-md">
                                    <UnorderedListItem
                                      variant="bullet"
                                      size="small"
                                      text="카드상품과 부수서비스의 안내 및 이용권유에 셨더라도 신용정보의 이용 및 보호에 관한 법률에 따라 이용권유 목적의 연락에 대한 중단을 언제라도 카드사에 요청할 수 있습니다. (대표전화 : 1544-7000 / 홈페이지 : www.shinhancard.com)"
                                    />
                                    <UnorderedListItem
                                      variant="bullet"
                                      size="small"
                                      text="갱신 및 상품서비스 변경 안내 등 필수 고지사항은 상기 동의 대상에서 제외됩니다."
                                    />
                                  </UnorderedList>
                                </div>

                                <!-- 3뎁스 영역: 신한금융 자회사 및 손자회사에 개인(신용)정보를 제공 (s4-2-9) -->
                                <div
                                  v-else-if="depth2Item.value === 's4-2-9'"
                                  class="agree-depth"
                                >
                                  <ul
                                    class="agree-sublist agree-sublist__depth3"
                                  >
                                    <li
                                      v-for="depth3Item in subItemsDepth3_s4_2_9"
                                      :key="depth3Item.value"
                                      class="agree-subitem agree-subitem__depth3"
                                    >
                                      <div class="agree-item agree-item__sub">
                                        <Checkbox
                                          :value="depth3Item.value"
                                          variant="mark"
                                          align="left"
                                          :model-value="
                                            subAgrees4.includes(
                                              depth3Item.value
                                            )
                                          "
                                          class="agree-item__checkbox item-checkbox__sub"
                                          @update:model-value="
                                            onToggleSub4(
                                              depth3Item.value,
                                              $event
                                            )
                                          "
                                          @click.stop
                                        >
                                          <template #label>
                                            <span
                                              class="agree-item__label item-label__sub"
                                              >{{ depth3Item.label }}</span
                                            >
                                          </template>
                                        </Checkbox>
                                      </div>
                                    </li>
                                  </ul>
                                  <!-- 자세히보기 링크 -->
                                  <div class="agree-depth__link">
                                    <TextButton
                                      class="agree-depth__link"
                                      color="secondary"
                                      size="small"
                                      text="자세히보기"
                                      showGoTo
                                    />
                                  </div>
                                </div>
                              </div>
                            </SolidListAccordion>
                          </template>

                          <!-- 일반 항목 -->
                          <div v-else class="agree-item agree-item__sub">
                            <Checkbox
                              :value="depth2Item.value"
                              variant="mark"
                              align="left"
                              :model-value="
                                subAgrees4.includes(depth2Item.value)
                              "
                              class="agree-item__checkbox item-checkbox__sub"
                              @update:model-value="
                                onToggleSub4(depth2Item.value, $event)
                              "
                              @click.stop
                            >
                              <template #label>
                                <span
                                  class="agree-item__label item-label__sub"
                                  >{{ depth2Item.label }}</span
                                >
                                <template v-if="depth2Item.grade">
                                  <br />
                                  <SolidLabel
                                    :color="depth2Item.grade"
                                    :title="
                                      depth2Item.grade === 'cyan'
                                        ? '안심'
                                        : depth2Item.grade === 'green'
                                          ? '다소안심'
                                          : depth2Item.grade === 'yellow'
                                            ? '보통'
                                            : depth2Item.grade === 'orange'
                                              ? '신중'
                                              : '주의'
                                    "
                                    :aria-label="`동의등급제 ${
                                      depth2Item.grade === 'cyan'
                                        ? '안심'
                                        : depth2Item.grade === 'green'
                                          ? '다소안심'
                                          : depth2Item.grade === 'yellow'
                                            ? '보통'
                                            : depth2Item.grade === 'orange'
                                              ? '신중'
                                              : '주의'
                                    }`"
                                  />
                                </template>
                              </template>
                            </Checkbox>
                            <IconButton
                              iconName="Chevron_right"
                              size="small"
                              :aria-label="`${depth2Item.label} 상세 보기`"
                              class="agree-subitem__trigger"
                            />
                          </div>
                          <!-- 서브텍스트: 회원 가입 및 발권신청 동의 -->
                          <div
                            v-if="depth2Item.value === 's4-2-10'"
                            class="agree-subitem padding-lg"
                          >
                            <p class="agree-subtext">
                              본인은 카드 실제 소유자와 동일하며, 위 기재된
                              사실과 다름이 없음을 확인하고 회원가입을
                              신청합니다.
                            </p>
                          </div>
                        </li>
                      </ul>
                    </div>
                    <div v-else-if="item.value === 's4-3'" class="agree-depth">
                      <!-- ======================================== -->
                      <!-- 2뎁스 영역: 온라인 회원 이용약관 -->
                      <!-- ======================================== -->
                      <ul class="agree-sublist agree-sublist__depth2">
                        <li
                          v-for="depth2Item in subItemsDepth2_s4_3"
                          :key="depth2Item.value"
                          class="agree-subitem agree-subitem__depth2"
                        >
                          <div class="agree-item agree-item__sub">
                            <Checkbox
                              :value="depth2Item.value"
                              variant="mark"
                              align="left"
                              :model-value="
                                subAgrees4.includes(depth2Item.value)
                              "
                              class="agree-item__checkbox item-checkbox__sub"
                              @update:model-value="
                                onToggleSub4(depth2Item.value, $event)
                              "
                              @click.stop
                            >
                              <template #label>
                                <span
                                  class="agree-item__label item-label__sub"
                                  >{{ depth2Item.label }}</span
                                >
                              </template>
                            </Checkbox>
                            <IconButton
                              iconName="Chevron_right"
                              size="small"
                              :aria-label="`${depth2Item.label} 상세 보기`"
                              class="agree-subitem__trigger"
                            />
                          </div>
                        </li>
                      </ul>
                    </div>
                    <div v-else-if="item.value === 's4-4'" class="agree-depth">
                      <!-- ======================================== -->
                      <!-- 동의등급제 안내 -->
                      <!-- ======================================== -->
                      <Card
                        variant="solid"
                        color="gray"
                        class="agree-info__card card-white"
                      >
                        <div class="info-card__header">
                          <p class="info-card__title">동의등급제 안내</p>
                        </div>
                        <div class="info-card__content">
                          <div class="label-group">
                            <!-- [251016] 안심 color 변경 blue에서 color="cyan" -->
                            <!-- <SolidLabel
                              color="blue"
                              title="안심"
                            /> -->
                            <SolidLabel color="cyan" title="안심" />
                            <SolidLabel color="green" title="다소안심" />
                            <SolidLabel color="yellow" title="보통" />
                            <SolidLabel color="orange" title="신중" />
                            <SolidLabel color="red" title="주의" />
                          </div>
                          <UnorderedList>
                            <UnorderedListItem
                              variant="bullet"
                              size="small"
                              text="동의등급제는 개인(신용) 선택적 동의 항목에 대해 사생활의 비밀과 자유를 침해할 위험, 이익이나 혜택, 등의 내용의 명확성 등을 고려하여 5가지 등급을 부여하는 제도입니다."
                            />
                          </UnorderedList>
                        </div>
                      </Card>

                      <!-- ======================================== -->
                      <!-- 2뎁스 영역: 신한 슈퍼SOL 이용약관 -->
                      <!-- ======================================== -->
                      <ul class="agree-sublist agree-sublist__depth2">
                        <li
                          v-for="depth2Item in subItemsDepth2_s4_4"
                          :key="depth2Item.value"
                          class="agree-subitem agree-subitem__depth2"
                        >
                          <!-- 아코디언이 있는 항목 -->
                          <template v-if="depth2Item.accordion">
                            <SolidListAccordion
                              class="agree-subitem__accordion accordion-depth2"
                              :rowClickable="false"
                              :value="depth2Item.value"
                              v-model:isExpanded="
                                subAccordionState4[depth2Item.value]
                              "
                            >
                              <template #title>
                                <div class="agree-item agree-item__sub">
                                  <Checkbox
                                    :value="depth2Item.value"
                                    variant="mark"
                                    align="left"
                                    :model-value="
                                      subAgrees4.includes(depth2Item.value)
                                    "
                                    class="agree-item__checkbox item-checkbox__sub"
                                    @update:model-value="
                                      onToggleSub4(depth2Item.value, $event)
                                    "
                                    @click.stop
                                  >
                                    <template #label>
                                      <span
                                        class="agree-item__label item-label__sub"
                                        >{{ depth2Item.label }}</span
                                      >
                                    </template>
                                  </Checkbox>
                                </div>
                              </template>
                              <div class="agree-subitem__panel">
                                <!-- 3뎁스 영역: 전자금융서비스 이용동의(신한은행) -->
                                <div
                                  v-if="depth2Item.value === 's4-4-5'"
                                  class="agree-depth"
                                >
                                  <Card
                                    variant="solid"
                                    color="gray"
                                    class="agree-details"
                                  >
                                    <ul class="agree-sublist" role="group">
                                      <li
                                        v-for="depth3Item in subItemsDepth3_s4_4_5"
                                        :key="depth3Item.value"
                                        class="agree-subitem agree-subitem__depth3"
                                      >
                                        <div class="agree-item agree-item__sub">
                                          <span
                                            class="agree-item__label item-label__sub"
                                            >{{ depth3Item.label }}</span
                                          >
                                          <IconButton
                                            iconName="Chevron_right"
                                            size="small"
                                            :aria-label="`${depth3Item.label} 상세 보기`"
                                            class="agree-subitem__trigger"
                                          />
                                        </div>
                                      </li>
                                    </ul>
                                  </Card>
                                </div>

                                <!-- 3뎁스 영역: 광고성 전자적 수신매체 전송 동의 -->
                                <div
                                  v-else-if="depth2Item.value === 's4-4-10'"
                                  class="agree-depth"
                                >
                                  <Card
                                    variant="solid"
                                    color="gray"
                                    class="agree-details"
                                  >
                                    <ul class="agree-sublist" role="group">
                                      <li
                                        v-for="depth3Item in subItemsDepth3_s4_4_10"
                                        :key="depth3Item.value"
                                        class="agree-subitem agree-subitem__depth3"
                                      >
                                        <div class="agree-item agree-item__sub">
                                          <Checkbox
                                            :value="depth3Item.value"
                                            variant="mark"
                                            align="left"
                                            :model-value="
                                              subAgrees4.includes(
                                                depth3Item.value
                                              )
                                            "
                                            class="agree-item__checkbox item-checkbox__sub"
                                            @update:model-value="
                                              onToggleSub4(
                                                depth3Item.value,
                                                $event
                                              )
                                            "
                                            @click.stop
                                          >
                                            <template #label>
                                              <span
                                                class="agree-item__label item-label__sub"
                                                >{{ depth3Item.label }}</span
                                              >
                                            </template>
                                          </Checkbox>
                                        </div>
                                      </li>
                                    </ul>
                                  </Card>
                                </div>
                              </div>
                            </SolidListAccordion>
                          </template>

                          <!-- 일반 항목 -->
                          <div v-else class="agree-item agree-item__sub">
                            <Checkbox
                              :value="depth2Item.value"
                              variant="mark"
                              align="left"
                              :model-value="
                                subAgrees4.includes(depth2Item.value)
                              "
                              class="agree-item__checkbox item-checkbox__sub"
                              @update:model-value="
                                onToggleSub4(depth2Item.value, $event)
                              "
                              @click.stop
                            >
                              <template #label>
                                <span
                                  class="agree-item__label item-label__sub"
                                  >{{ depth2Item.label }}</span
                                >
                                <template
                                  v-if="
                                    depth2Item.value === 's4-4-8' ||
                                    depth2Item.value === 's4-4-9'
                                  "
                                >
                                  <br />
                                  <!-- [251016] 안심 color 변경 blue에서 color="cyan" -->
                                  <!-- 
                                  <SolidLabel
                                    color="blue"
                                    title="안심"
                                    aria-label="동의등급제 안심"
                                    /> -->
                                  <SolidLabel
                                    color="cyan"
                                    title="안심"
                                    aria-label="동의등급제 안심"
                                  />
                                </template>
                              </template>
                            </Checkbox>
                            <IconButton
                              iconName="Chevron_right"
                              size="small"
                              :aria-label="`${depth2Item.label} 상세 보기`"
                              class="agree-subitem__trigger"
                            />
                          </div>
                        </li>
                      </ul>
                    </div>
                    <div v-else-if="item.value === 's4-5'" class="agree-depth">
                      <!-- ======================================== -->
                      <!-- 2뎁스 영역: 전자문서 서비스 이용약관 -->
                      <!-- ======================================== -->
                      <ul class="agree-sublist agree-sublist__depth2">
                        <li
                          v-for="depth2Item in subItemsDepth2_s4_5"
                          :key="depth2Item.value"
                          class="agree-subitem agree-subitem__depth2"
                        >
                          <div class="agree-item agree-item__sub">
                            <Checkbox
                              :value="depth2Item.value"
                              variant="mark"
                              align="left"
                              :model-value="
                                subAgrees4.includes(depth2Item.value)
                              "
                              class="agree-item__checkbox item-checkbox__sub"
                              @update:model-value="
                                onToggleSub4(depth2Item.value, $event)
                              "
                              @click.stop
                            >
                              <template #label>
                                <span
                                  class="agree-item__label item-label__sub"
                                  >{{ depth2Item.label }}</span
                                >
                              </template>
                            </Checkbox>
                            <IconButton
                              iconName="Chevron_right"
                              size="small"
                              :aria-label="`${depth2Item.label} 상세 보기`"
                              class="agree-subitem__trigger"
                            />
                          </div>
                        </li>
                      </ul>
                    </div>
                    <div v-else-if="item.value === 's4-6'" class="agree-depth">
                      <!-- ======================================== -->
                      <!-- 2뎁스 영역: 마이데이터 서비스 이용약관 -->
                      <!-- ======================================== -->
                      <ul class="agree-sublist agree-sublist__depth2">
                        <li
                          v-for="depth2Item in subItemsDepth2_s4_6"
                          :key="depth2Item.value"
                          class="agree-subitem agree-subitem__depth2"
                        >
                          <div class="agree-item agree-item__sub">
                            <Checkbox
                              :value="depth2Item.value"
                              variant="mark"
                              align="left"
                              :model-value="
                                subAgrees4.includes(depth2Item.value)
                              "
                              class="agree-item__checkbox item-checkbox__sub"
                              @update:model-value="
                                onToggleSub4(depth2Item.value, $event)
                              "
                              @click.stop
                            >
                              <template #label>
                                <span
                                  class="agree-item__label item-label__sub"
                                  >{{ depth2Item.label }}</span
                                >
                              </template>
                            </Checkbox>
                            <IconButton
                              iconName="Chevron_right"
                              size="small"
                              :aria-label="`${depth2Item.label} 상세 보기`"
                              class="agree-subitem__trigger"
                            />
                          </div>
                        </li>
                      </ul>

                      <!-- 개인정보 처리방침 링크 -->
                      <div class="agree-depth__link">
                        <TextButton
                          class="agree-depth__link"
                          color="secondary"
                          size="small"
                          text="개인정보 처리방침"
                          showGoTo
                        />
                      </div>
                    </div>
                    <div v-else-if="item.value === 's4-7'" class="agree-depth">
                      <!-- ======================================== -->
                      <!-- 2뎁스 영역: 마케팅 동의 이용약관 -->
                      <!-- ======================================== -->
                      <ul class="agree-sublist agree-sublist__depth2">
                        <!-- 동의등급제 안내 -->
                        <li class="agree-subitem agree-subitem__depth2">
                          <Card
                            variant="solid"
                            color="gray"
                            class="agree-info__card card-white"
                          >
                            <div class="info-card__header">
                              <p class="info-card__title">동의등급제 안내</p>
                            </div>
                            <div class="info-card__content">
                              <div class="label-group">
                                <SolidLabel color="cyan" title="안심" />
                                <SolidLabel color="green" title="다소안심" />
                                <SolidLabel color="yellow" title="보통" />
                                <SolidLabel color="orange" title="신중" />
                                <SolidLabel color="red" title="주의" />
                              </div>
                              <UnorderedList>
                                <UnorderedListItem
                                  variant="bullet"
                                  size="small"
                                  text="동의등급제는 개인(신용) 선택적 동의 항목에 대해 사생활의 비밀과 자유를 침해할 위험, 이익이나 혜택, 등의 내용의 명확성 등을 고려하여 5가지 등급을 부여하는 제도입니다."
                                />
                              </UnorderedList>
                            </div>
                          </Card>
                        </li>
                        <!-- 동의등급제 안내 이후 추가 항목들 -->
                        <li
                          v-for="depth2Item in subItemsDepth2_s4_7_after"
                          :key="depth2Item.value"
                          class="agree-subitem agree-subitem__depth2"
                          :class="{
                            'agree-subitem__accordion': Boolean(
                              depth2Item.accordion
                            ),
                          }"
                        >
                          <!-- 아코디언이 있는 항목 -->
                          <template v-if="depth2Item.accordion">
                            <SolidListAccordion
                              class="agree-subitem__accordion accordion-depth2"
                              :rowClickable="false"
                              :value="depth2Item.value"
                              v-model:isExpanded="
                                subAccordionState4[depth2Item.value]
                              "
                            >
                              <template #title>
                                <div class="agree-item agree-item__sub">
                                  <Checkbox
                                    :value="depth2Item.value"
                                    variant="mark"
                                    align="left"
                                    :model-value="
                                      subAgrees4.includes(depth2Item.value)
                                    "
                                    class="agree-item__checkbox item-checkbox__sub"
                                    @update:model-value="
                                      onToggleSub4(depth2Item.value, $event)
                                    "
                                    @click.stop
                                  >
                                    <template #label>
                                      <span
                                        class="agree-item__label item-label__sub"
                                        >{{ depth2Item.label }}</span
                                      >
                                      <template v-if="depth2Item.grade">
                                        <br />
                                        <SolidLabel
                                          :color="depth2Item.grade"
                                          :title="
                                            depth2Item.grade === 'cyan'
                                              ? '안심'
                                              : depth2Item.grade === 'green'
                                                ? '다소안심'
                                                : depth2Item.grade === 'yellow'
                                                  ? '보통'
                                                  : depth2Item.grade ===
                                                      'orange'
                                                    ? '신중'
                                                    : '주의'
                                          "
                                          :aria-label="`동의등급제 ${
                                            depth2Item.grade === 'cyan'
                                              ? '안심'
                                              : depth2Item.grade === 'green'
                                                ? '다소안심'
                                                : depth2Item.grade === 'yellow'
                                                  ? '보통'
                                                  : depth2Item.grade ===
                                                      'orange'
                                                    ? '신중'
                                                    : '주의'
                                          }`"
                                        />
                                      </template>
                                    </template>
                                  </Checkbox>
                                </div>
                              </template>
                              <div class="agree-subitem__panel">
                                <!-- 3뎁스 영역: 카드 및 금융상품 ・ 서비스 안내 및 이용권유를 위한 수집 ・ 이용 -->
                                <div
                                  v-if="depth2Item.value === 's4-2-6'"
                                  class="agree-depth"
                                >
                                  <ul
                                    class="agree-sublist agree-sublist__depth3"
                                  >
                                    <li
                                      v-for="depth3Item in subItemsDepth3_s4_2_6"
                                      :key="depth3Item.value"
                                      class="agree-subitem agree-subitem__depth3"
                                    >
                                      <div class="agree-item agree-item__sub">
                                        <Checkbox
                                          :value="depth3Item.value"
                                          variant="mark"
                                          align="left"
                                          :model-value="
                                            subAgrees4.includes(
                                              depth3Item.value
                                            )
                                          "
                                          class="agree-item__checkbox item-checkbox__sub"
                                          @update:model-value="
                                            onToggleSub4(
                                              depth3Item.value,
                                              $event
                                            )
                                          "
                                          @click.stop
                                        >
                                          <template #label>
                                            <span
                                              class="agree-item__label item-label__sub"
                                              >{{ depth3Item.label }}</span
                                            >
                                          </template>
                                        </Checkbox>
                                      </div>
                                    </li>
                                  </ul>
                                  <!-- 자세히보기 링크 -->
                                  <div class="agree-depth__link">
                                    <TextButton
                                      class="agree-depth__link"
                                      color="secondary"
                                      size="small"
                                      text="자세히보기"
                                      showGoTo
                                    />
                                  </div>
                                </div>

                                <!-- 3뎁스 영역: 카드 및 금융상품 ・ 서비스 이외의 부수서비스 안내 등을 위한 수집 ・ 이용 -->
                                <template
                                  v-else-if="depth2Item.value === 's4-2-7'"
                                >
                                  <ul
                                    class="agree-sublist agree-sublist__depth3"
                                  >
                                    <li
                                      v-for="depth3Item in subItemsDepth3_s4_2_7"
                                      :key="depth3Item.value"
                                      class="agree-subitem agree-subitem__depth3"
                                    >
                                      <div class="agree-item agree-item__sub">
                                        <Checkbox
                                          :value="depth3Item.value"
                                          variant="mark"
                                          align="left"
                                          :model-value="
                                            subAgrees4.includes(
                                              depth3Item.value
                                            )
                                          "
                                          class="agree-item__checkbox item-checkbox__sub"
                                          @update:model-value="
                                            onToggleSub4(
                                              depth3Item.value,
                                              $event
                                            )
                                          "
                                          @click.stop
                                        >
                                          <template #label>
                                            <span
                                              class="agree-item__label item-label__sub"
                                              >{{ depth3Item.label }}</span
                                            >
                                          </template>
                                        </Checkbox>
                                      </div>
                                    </li>
                                  </ul>
                                  <!-- 자세히보기 링크 -->
                                  <div class="agree-depth__link">
                                    <TextButton
                                      class="agree-depth__link"
                                      color="secondary"
                                      size="small"
                                      text="자세히보기"
                                      showGoTo
                                    />
                                  </div>
                                </template>

                                <!-- 3뎁스 영역: 전자적 전송매체를 통한 광고성 정보 수신동의 -->
                                <div
                                  v-else-if="depth2Item.value === 's4-2-8'"
                                  class="agree-depth"
                                >
                                  <Card
                                    variant="solid"
                                    color="gray"
                                    class="agree-details"
                                  >
                                    <ul class="agree-sublist" role="group">
                                      <li
                                        v-for="depth3Item in subItemsDepth3_s4_2_8"
                                        :key="depth3Item.value"
                                        class="agree-subitem agree-subitem__depth3"
                                      >
                                        <div class="agree-item agree-item__sub">
                                          <Checkbox
                                            :value="depth3Item.value"
                                            variant="mark"
                                            align="left"
                                            :model-value="
                                              subAgrees4.includes(
                                                depth3Item.value
                                              )
                                            "
                                            class="agree-item__checkbox item-checkbox__sub"
                                            @update:model-value="
                                              onToggleSub4(
                                                depth3Item.value,
                                                $event
                                              )
                                            "
                                            @click.stop
                                          >
                                            <template #label>
                                              <span
                                                class="agree-item__label item-label__sub"
                                                >{{ depth3Item.label }}</span
                                              >
                                            </template>
                                          </Checkbox>
                                        </div>
                                      </li>
                                    </ul>
                                  </Card>
                                  <!-- 설명 텍스트 -->
                                  <UnorderedList class="mt-md mb-md">
                                    <UnorderedListItem
                                      variant="bullet"
                                      size="small"
                                      text="카드상품과 부수서비스의 안내 및 이용권유에 셨더라도 신용정보의 이용 및 보호에 관한 법률에 따라 이용권유 목적의 연락에 대한 중단을 언제라도 카드사에 요청할 수 있습니다. (대표전화 : 1544-7000 / 홈페이지 : www.shinhancard.com)"
                                    />
                                    <UnorderedListItem
                                      variant="bullet"
                                      size="small"
                                      text="갱신 및 상품서비스 변경 안내 등 필수 고지사항은 상기 동의 대상에서 제외됩니다."
                                    />
                                  </UnorderedList>
                                </div>

                                <!-- 3뎁스 영역: [선택] 카드 및 금융상품 ・ 서비스 안내 및 이용권유를 위한 수집 ・ 이용 (s4-2-9) -->
                                <div
                                  v-else-if="depth2Item.value === 's4-2-9'"
                                  class="agree-depth"
                                >
                                  <ul
                                    class="agree-sublist agree-sublist__depth3"
                                  >
                                    <li
                                      v-for="depth3Item in subItemsDepth3_s4_2_9"
                                      :key="depth3Item.value"
                                      class="agree-subitem agree-subitem__depth3"
                                    >
                                      <div class="agree-item agree-item__sub">
                                        <Checkbox
                                          :value="depth3Item.value"
                                          variant="mark"
                                          align="left"
                                          :model-value="
                                            subAgrees4.includes(
                                              depth3Item.value
                                            )
                                          "
                                          class="agree-item__checkbox item-checkbox__sub"
                                          @update:model-value="
                                            onToggleSub4(
                                              depth3Item.value,
                                              $event
                                            )
                                          "
                                          @click.stop
                                        >
                                          <template #label>
                                            <span
                                              class="agree-item__label item-label__sub"
                                              >{{ depth3Item.label }}</span
                                            >
                                          </template>
                                        </Checkbox>
                                      </div>
                                    </li>
                                  </ul>
                                  <!-- 자세히보기 링크 -->
                                  <div class="agree-depth__link">
                                    <TextButton
                                      class="agree-depth__link"
                                      color="secondary"
                                      size="small"
                                      text="자세히보기"
                                      showGoTo
                                    />
                                  </div>
                                </div>
                              </div>
                            </SolidListAccordion>
                          </template>
                        </li>
                      </ul>
                    </div>
                  </div>
                </SolidListAccordion>
              </template>
              <template v-else>
                <div
                  class="agree-item agree-item__sub"
                  :class="{ 'is-checked': subAgrees4.includes(item.value) }"
                >
                  <Checkbox
                    :value="item.value"
                    variant="box"
                    align="left"
                    :model-value="subAgrees4.includes(item.value)"
                    class="agree-item__checkbox item-checkbox__sub"
                    @update:model-value="onToggleSub4(item.value, $event)"
                    @click.stop
                  >
                    <template #label>
                      <span class="agree-item__label item-label__sub">{{
                        item.label
                      }}</span>
                    </template>
                  </Checkbox>
                  <IconButton
                    iconName="Chevron_right"
                    size="small"
                    :aria-label="`${item.label} 상세 보기`"
                    class="agree-subitem__trigger"
                  />
                </div>
              </template>
            </div>
          </div>
        </div>
      </div>
    </section>
  </div>

  <!-- 하단 고정으로 들어가는 부분 위치 수정 -->
  <div class="sc-contents__foot">
    <Divider variant="group" color="tertiary" />

    <div class="sc-bottom-info__inner">
      <h2 class="sc-bottom-info__title">마이데이터 서비스 안내</h2>
      <div class="sc-bottom-info__details">
        <UnorderedList>
          <UnorderedListItem
            variant="bullet"
            text="잘 이용하지 않는 서비스는 탈퇴 후 내 정보를 삭제할 수 있어요."
          />
          <UnorderedListItem
            variant="bullet"
            text="나의 마이데이터 서비스 가입현황은 마이데이터 종합포털에서 확인할 수 있어요."
          />
        </UnorderedList>
      </div>
      <!-- [251027] 마이데이터 서비스 안내 하단 링크 추가 -->
      <div class="agree-depth__link">
        <TextButton
          class="agree-depth__link"
          color="secondary"
          size="small"
          text="종합포털 바로가기"
          showGoTo
        />
      </div>
    </div>
  </div>

  <BottomActionContainer :scrollDim="true">
    <BoxButtonGroup size="xlarge" variant="100">
      <BoxButton text="확인" :disabled="!basicAgree4" />
    </BoxButtonGroup>
  </BottomActionContainer>
</template>

<script setup>
import {
  BottomActionContainer,
  BoxButton,
  BoxButtonGroup,
  Card,
  Checkbox,
  Divider,
  IconButton,
  SolidLabel,
  SolidListAccordion,
  TextButton,
  UnorderedList,
  UnorderedListItem,
} from "@shc-nss/ui/solid";
import { computed, reactive, ref, watch } from "vue";
import { useRoute } from "vue-router";

const route = useRoute();
const bodyTitle = computed(() => route.meta?.title || "");

/**
 * 유형 4 : 약관동의 기본형
 */
const basicItem4 = {
  label: "약관 전체 동의",
};

// JavaScript/TypeScript 호환을 위한 타입 정의 (선택사항)

// JavaScript/TypeScript 호환 배열
const subItems4 = [
  {
    label: "[필수/선택] 서비스 이용약관",
    value: "s4-1",
    accordion: true,
  },
  {
    label: "[필수/선택] 신한Pay머니 이용약관",
    value: "s4-2",
    accordion: true,
  },
  {
    label: "[선택] 온라인 회원 이용약관",
    value: "s4-3",
    accordion: true,
  },
  {
    label: "[선택] 신한 슈퍼SOL 이용약관",
    value: "s4-4",
    accordion: true,
  },
  {
    label: "[선택] 전자문서 서비스 이용약관",
    value: "s4-5",
    accordion: true,
  },
  {
    label: "[선택] 마이데이터 서비스 이용약관",
    value: "s4-6",
    accordion: true,
  },
  {
    label: "[선택] 마케팅 동의 이용약관",
    value: "s4-7",
    accordion: true,
  },
];

// 2뎁스 항목들 - 서비스 이용약관 (s4-1)
const subItemsDepth2_s4_1 = [
  { label: "[필수] 앱카드 서비스 이용약관 동의", value: "s4-1-1" },
  { label: "[필수] 개인(신용)정보의 수집 및 이용동의", value: "s4-1-2" },
  { label: "[필수] 고유식별정보처리 동의", value: "s4-1-3" },
  {
    label: "[선택] 위치기반 서비스 약관동의",
    value: "s4-1-4",
    accordion: true,
  },
  { label: "[선택] 앱(APP) 알림 수신동의", value: "s4-1-5", accordion: true },
];

// 2뎁스 항목들 - 신한Pay머니 이용약관 (s4-2)
const subItemsDepth2_s4_2 = [
  { label: "[필수] 신한Pay머니 이용약관동의", value: "s4-2-1" },
  { label: "[필수] 개인정보 수집 및 이용동의", value: "s4-2-2" },
  { label: "[필수] 고유식별정보처리 동의", value: "s4-2-3" },
  { label: "[필수] 개인(신용)정보 제공동의", value: "s4-2-4" },
  { label: "[필수] 고유식별정보 제공동의", value: "s4-2-5" },
];

// 2뎁스 항목들 - 신한Pay머니 이용약관 동의등급제 이후 항목들 (s4-2)
const subItemsDepth2_s4_2_after = [
  {
    label:
      "[선택] 카드 및 금융상품 ・ 서비스 안내 및 이용권유를 위한 수집 ・ 이용",
    value: "s4-2-6",
    grade: "green", // 다소안심
    accordion: true,
  },
  {
    label:
      "[선택] 카드 및 금융상품 ・ 서비스 이외의 부수서비스 안내 등을 위한 수집 ・ 이용",
    value: "s4-2-7",
    grade: "yellow", // 보통
    accordion: true,
  },
  {
    label: "[선택] 전자적 전송매체를 통한 광고성 정보 수신동의",
    value: "s4-2-8",
    accordion: true,
  },
  {
    label: "[선택] 카드 및 금융상품 ・ 서비스 안내 및 이용권유를 위한 수집 ・ 이용",
    value: "s4-2-9",
    grade: "cyan", // 안심
    accordion: true,
  },
  { label: "[필수] 회원 가입 및 발권신청 동의", value: "s4-2-10" },
];

// 2뎁스 항목들 - 온라인 회원 이용약관 (s4-3)
const subItemsDepth2_s4_3 = [
  { label: "[필수] 온라인 회원 이용약관동의", value: "s4-3-1" },
  { label: "[필수] 개인정보 필수적 수집・이용동의서", value: "s4-3-2" },
];

// 2뎁스 항목들 - 신한 슈퍼SOL 이용약관 (s4-4)
const subItemsDepth2_s4_4 = [
  { label: "[필수] 신한 모바일 플랫폼 이용약관", value: "s4-4-1" },
  { label: "[필수] 신한금융그룹 통합 포인트 서비스 이용동의", value: "s4-4-2" },
  { label: "[필수] 개인(신용)정보 수집・이용・제공 동의", value: "s4-4-3" },
  {
    label: "[필수] 개인(신용)정보 수집・이용・제공 동의(포인트 서비스 제공)",
    value: "s4-4-4",
  },
  {
    label: "[필수] 전자금융서비스 이용동의(신한은행)",
    value: "s4-4-5",
    accordion: true,
  },
  { label: "[필수] 그룹 로열티 서비스 이용동의(신한은행)", value: "s4-4-6" },
  {
    label: "[필수] 개인(신용)정보 수집・이용・제공 동의(신한은행)",
    value: "s4-4-7",
  },
  {
    label: "[선택] 개인(신용)정보 수집・이용・제공 동의(상품 서비스 안내 등)",
    value: "s4-4-8",
  },
  {
    label:
      "[선택] 개인(신용)정보 수집・이용・제공 동의(상품 서비스 안내 등)(신한은행)",
    value: "s4-4-9",
  },
  {
    label: "[선택] 광고성 전자적 수신매체 전송 동의",
    value: "s4-4-10",
    accordion: true,
  },
];

// 3뎁스 항목들 - 전자금융서비스 이용동의(신한은행) (s4-4-5)
const subItemsDepth3_s4_4_5 = [
  { label: "전자금융거래 기본약관", value: "s4-4-5-1" },
  { label: "신한온라인서비스 이용약관", value: "s4-4-5-2" },
  { label: "전자통지서비스 이용약관", value: "s4-4-5-3" },
  { label: "개인정보 수집 이용동의(비여신 금융거래)", value: "s4-4-5-4" },
];

// 3뎁스 항목들 - 광고성 전자적 수신매체 전송 동의 (s4-4-10)
const subItemsDepth3_s4_4_10 = [
  { label: "문자", value: "s4-4-10-1" },
  { label: "이메일", value: "s4-4-10-2" },
  { label: "전화", value: "s4-4-10-3" },
];

// 3뎁스 항목들 - 위치기반 서비스 약관동의 (s4-1-4)
const subItemsDepth3_s4_1_4 = [
  { label: "신한카드 위치기반 사업자 약관동의", value: "s4-1-4-1" },
  { label: "위치정보 서비스 동의사항", value: "s4-1-4-2", accordion: true },
  { label: "개인정보 수집 및 이용동의", value: "s4-1-4-3" },
  { label: "위치기반 혜택 알림 수신동의", value: "s4-1-4-4" },
  { label: "블루칩 씨엔에스 위치정보사업자약관동의", value: "s4-1-4-5" },
];

// 3뎁스 항목들 - 앱(APP) 알림 수신동의 (s4-1-5)
const subItemsDepth3_s4_1_5 = [
  { label: "마케팅 정보 수신동의", value: "s4-1-5-1", accordion: true },
];

// 4뎁스 항목들 - 위치정보 서비스 동의사항 (s4-1-4-2)
const subItemsDepth4_s4_1_4_2 = [
  { label: "LGU+ 위치정보 사업자 약관 동의", value: "s4-1-4-2-1" },
  { label: "LGU+ 개인정보수집이용 및 제3자 제공동의", value: "s4-1-4-2-2" },
  { label: "로플렛 위치정보 사업자 약관동의", value: "s4-1-4-2-3" },
];

// 2뎁스 항목들 - 전자문서 서비스 (s4-5)
const subItemsDepth2_s4_5 = [
  { label: "[필수] 전자문서 서비스 이용약관 동의", value: "s4-5-1" },
  { label: "[필수] 전자문서 개인정보 수집・이용・동의", value: "s4-5-2" },
  { label: "[필수] 개인정보 제3자 제공 동의", value: "s4-5-3" },
  { label: "[필수] 서비스 유의사항 동의", value: "s4-5-4" },
];

// 2뎁스 항목들 - 마이데이터 서비스 (s4-6)
const subItemsDepth2_s4_6 = [
  { label: "[필수] 마이데이터 서비스 이용약관동의", value: "s4-6-1" },
  {
    label: "[필수] 마이데이터 서비스 개인(신용)정보의 수집 및 이용동의",
    value: "s4-6-2",
  },
];

// 2뎁스 항목들 - 마케팅 동의 이용약관 (s4-7)
const subItemsDepth2_s4_7_after = [
  {
    label:
      "[선택] 카드 및 금융상품 ・ 서비스 안내 및 이용권유를 위한 수집 ・ 이용",
    value: "s4-2-6",
    grade: "green", // 다소안심
    accordion: true,
  },
  {
    label:
      "[선택] 카드 및 금융상품 ・ 서비스 이외의 부수서비스 안내 등을 위한 수집 ・ 이용",
    value: "s4-2-7",
    grade: "yellow", // 보통
    accordion: true,
  },
  {
    label: "[선택] 전자적 전송매체를 통한 광고성 정보 수신동의",
    value: "s4-2-8",
    accordion: true,
  },
  {
    label: "[선택] 신한금융 자회사 및 손자회사에 개인(신용)정보를 제공",
    value: "s4-2-9",
    grade: "cyan", // 안심
    accordion: true,
  },
];

// 3뎁스 항목들 - 카드 및 금융상품 ・ 서비스 안내 및 이용권유를 위한 수집 ・ 이용 (s4-2-6)
const subItemsDepth3_s4_2_6 = [
  { label: "고유식별번호 조회 동의", value: "s4-2-6-1" },
  { label: "개인신용정보 제공 동의", value: "s4-2-6-2" },
];

// 3뎁스 항목들 - 카드 및 금융상품 ・ 서비스 이외의 부수서비스 안내 등을 위한 수집 ・ 이용 (s4-2-7)
const subItemsDepth3_s4_2_7 = [
  { label: "고유식별번호 조회 동의", value: "s4-2-7-1" },
  { label: "개인신용정보 제공 동의", value: "s4-2-7-2" },
];

// 3뎁스 항목들 - 전자적 전송매체를 통한 광고성 정보 수신동의 (s4-2-8)
const subItemsDepth3_s4_2_8 = [
  { label: "전체", value: "s4-2-8-1" },
  { label: "서면", value: "s4-2-8-2" },
  { label: "이메일", value: "s4-2-8-3" },
  { label: "전화", value: "s4-2-8-4" },
  {
    label: "휴대폰 메세지(카카오톡, 네이버 알림 등 모바일 메세지 포함)",
    value: "s4-2-8-5",
  },
];

// 3뎁스 항목들 - 신한금융 자회사 및 손자회사에 개인(신용)정보를 제공 (s4-2-9)
const subItemsDepth3_s4_2_9 = [
  { label: "개인신용정보 제공 동의", value: "s4-2-9-1" },
];

const basicAgree4 = ref(false);
const subAgrees4 = ref([]);
const subAccordionState4 = reactive({
  "s4-1": false, // 서비스 이용약관 2뎁스 아코디언 상태
  "s4-2": false, // 신한Pay머니 이용약관 2뎁스 아코디언 상태
  "s4-3": false, // 온라인 회원 이용약관 2뎁스 아코디언 상태
  "s4-4": false, // 신한 슈퍼SOL 이용약관 2뎁스 아코디언 상태
  "s4-5": false, // 전자문서 서비스 2뎁스 아코디언 상태
  "s4-6": false, // 마이데이터 서비스 2뎁스 아코디언 상태
  "s4-7": false, // 마케팅 동의 이용약관 2뎁스 아코디언 상태
  "s4-1-4": false, // 위치기반 서비스 약관동의 3뎁스 아코디언 상태
  "s4-1-5": false, // 앱(APP) 알림 수신동의 3뎁스 아코디언 상태
  "s4-1-4-2": false, // 위치정보 서비스 동의사항 4뎁스 아코디언 상태
  "s4-1-5-1": false, // 마케팅 정보 수신동의 4뎁스 아코디언 상태
  "s4-4-5": false, // 전자금융서비스 이용동의(신한은행) 3뎁스 아코디언 상태
  "s4-4-10": false, // 광고성 전자적 수신매체 전송 동의 3뎁스 아코디언 상태
  "s4-2-6": false, // 카드 및 금융상품 ・ 서비스 안내 및 이용권유를 위한 수집 ・ 이용 2뎁스 아코디언 상태
  "s4-2-7": false, // 카드 및 금융상품 ・ 서비스 이외의 부수서비스 안내 등을 위한 수집 ・ 이용 2뎁스 아코디언 상태
  "s4-2-8": false, // 전자적 전송매체를 통한 광고성 정보 수신동의 2뎁스 아코디언 상태
  "s4-2-9": false, // 신한금융 자회사 및 손자회사에 개인(신용)정보를 제공 2뎁스 아코디언 상태
});

/**
 * 동작 로직
 */
function onToggleSub4(value, checked) {
  const set = new Set(subAgrees4.value);
  if (checked) set.add(value);
  else set.delete(value);
  subAgrees4.value = Array.from(set);

  // 전체 항목 수 계산 (1뎁스 + 2뎁스 + 3뎁스 + 4뎁스)
  const totalItems =
    subItems4.length +
    subItemsDepth2_s4_1.length +
    subItemsDepth2_s4_2.length +
    subItemsDepth2_s4_2_after.length +
    subItemsDepth2_s4_3.length +
    subItemsDepth2_s4_4.length +
    subItemsDepth2_s4_5.length +
    subItemsDepth2_s4_6.length +
    subItemsDepth2_s4_7_after.length +
    subItemsDepth3_s4_1_4.length +
    subItemsDepth3_s4_1_5.length +
    subItemsDepth3_s4_2_6.length +
    subItemsDepth3_s4_2_7.length +
    subItemsDepth3_s4_2_8.length +
    subItemsDepth3_s4_2_9.length +
    subItemsDepth3_s4_4_5.length +
    subItemsDepth3_s4_4_10.length +
    subItemsDepth4_s4_1_4_2.length;
  basicAgree4.value = set.size === totalItems;
}

watch(basicAgree4, (checked) => {
  if (checked) {
    // 1뎁스 항목들 + 아코디언 내부의 모든 하위 항목들 (2뎁스 + 3뎁스 + 4뎁스)
    const allItems = [
      ...subItems4.map((item) => item.value),
      ...subItemsDepth2_s4_1.map((item) => item.value),
      ...subItemsDepth2_s4_2.map((item) => item.value),
      ...subItemsDepth2_s4_2_after.map((item) => item.value),
      ...subItemsDepth2_s4_3.map((item) => item.value),
      ...subItemsDepth2_s4_4.map((item) => item.value),
      ...subItemsDepth2_s4_5.map((item) => item.value),
      ...subItemsDepth2_s4_6.map((item) => item.value),
      ...subItemsDepth2_s4_7_after.map((item) => item.value),
      ...subItemsDepth3_s4_1_4.map((item) => item.value),
      ...subItemsDepth3_s4_1_5.map((item) => item.value),
      ...subItemsDepth3_s4_2_6.map((item) => item.value),
      ...subItemsDepth3_s4_2_7.map((item) => item.value),
      ...subItemsDepth3_s4_2_8.map((item) => item.value),
      ...subItemsDepth3_s4_2_9.map((item) => item.value),
      ...subItemsDepth3_s4_4_5.map((item) => item.value),
      ...subItemsDepth3_s4_4_10.map((item) => item.value),
      ...subItemsDepth4_s4_1_4_2.map((item) => item.value),
    ];
    subAgrees4.value = allItems;
  } else {
    subAgrees4.value = [];
  }
});
</script>




```
{% endraw %}
---
