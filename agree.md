
{% raw %}
```js

<div class="sc-contents__body sc-agree__page">
    <!-- 구조 수정 260318: 개발 전달용 -->
    <div class="agree_wrap">
      <!-- 전체 약관 선택 -->
      <div class="agree_allcheck">
        <Checkbox
          v-model="agreeAll"
          class="agree_checkbox"
          variant="box"
          align="left"
        >
          <template #label>
            <span class="agree_label">
              전체 약관 모두 동의
            </span>
          </template>
        </Checkbox>
      </div>
      <!-- 약관 리스트 (depth1 개수 파악용 ref) -->
      <ul ref="agreeListRef" class="agree_list" @click="onAgreeListClick">
        <li class="depth1">
          <!--
            depth1의 checkbox는 variant="box" variant="mark" 스타일 구분
            디자인에 맞춰서 작업 
          -->
          <div class="agree_item">
            <Checkbox variant="box" align="left" class="agree_checkbox">
              <template #label>
                <span class="agree_label">
                  [필수·선택] 서비스 이용약관
                </span>
              </template>
            </Checkbox>
            <!-- 
              아이콘 버튼은 
              하위 뎁스가 있는 경우 Chevron_down(펼침 시) / Chevron_right(접힘 시)
              하위 뎁스가 없는 경우 Chevron_right(상세 보기만)
              aria-label·aria-expanded 상황에 맞게 사용
            -->
            <IconButton
              v-if="depth1HasChildren"
              iconName="Chevron_down"
              size="small"
              class="agree_trigger"
            />
            <IconButton
              v-else
              iconName="Chevron_right"
              size="small"
              aria-label="[필수·선택] 서비스 이용약관 상세 보기"
              class="agree_trigger"
            />
          </div>
          <!-- depth2 (class is-expand 추가/제거로 펼침/접힘) -->
          <div class="depth2">
            <ul class="agree_sublist">
              <li class="agree_subitem">
                <div class="agree_item">
                  <Checkbox variant="mark" align="left" class="agree_checkbox">
                    <template #label>
                      <span class="agree_label">
                        앱카드 서비스 이용약관 필수 동의
                      </span>
                    </template>
                  </Checkbox>
                  <IconButton
                    iconName="Chevron_right"
                    size="small"
                    aria-label="앱카드 서비스 이용약관 필수 동의 상세 보기"
                    class="agree_trigger"
                  />
                </div>
              </li>
              <li class="agree_subitem">
                <div class="agree_item">
                  <Checkbox variant="mark" align="left" class="agree_checkbox">
                    <template #label>
                      <span class="agree_label">
                        개인(신용)정보의 수집 및 이용 필수 동의
                      </span>
                    </template>
                  </Checkbox>
                  <IconButton
                    iconName="Chevron_right"
                    size="small"
                    aria-label="개인(신용)정보의 수집 및 이용 필수 동의 상세 보기"
                    class="agree_trigger"
                  />
                </div>
              </li>
              <li class="agree_subitem">
                <div class="agree_item">
                  <Checkbox variant="mark" align="left" class="agree_checkbox">
                    <template #label>
                      <span class="agree_label">
                        고유식별정보처리 필수 동의
                      </span>
                    </template>
                  </Checkbox>
                  <IconButton
                    iconName="Chevron_right"
                    size="small"
                    aria-label="고유식별정보처리 필수 동의 상세 보기"
                    class="agree_trigger"
                  />
                </div>
              </li>
              <li class="agree_subitem">
                <div class="agree_item">
                  <Checkbox variant="mark" align="left" class="agree_checkbox">
                    <template #label>
                      <span class="agree_label">
                        [선택] 위치기반 서비스 약관동의
                      </span>
                    </template>
                  </Checkbox>
                  <IconButton
                    v-if="depth2HasChildren"
                    iconName="Chevron_down"
                    size="small"
                    class="agree_trigger"
                  />
                  <IconButton
                    v-else
                    iconName="Chevron_right"
                    size="small"
                    aria-label="[선택] 위치기반 서비스 약관동의 상세 보기"
                    class="agree_trigger"
                  />
                </div>
                <!-- depth3 (class is-expand 추가/제거로 펼침/접힘) -->
                <div class="depth3">
                  <ul class="agree_sublist">
                    <li class="agree_subitem">
                      <div class="agree_item">
                        <Checkbox
                          variant="mark"
                          align="left"
                          class="agree_checkbox"
                        >
                          <template #label>
                            <span class="agree_label">
                              신한카드 위치기반 사업자 약관 동의
                            </span>
                          </template>
                        </Checkbox>
                        <IconButton
                          iconName="Chevron_right"
                          size="small"
                          aria-label="신한카드 위치기반 사업자 약관 동의 상세 보기"
                          class="agree_trigger"
                        />
                      </div>
                    </li>
                    <li class="agree_subitem">
                      <div class="agree_item">
                        <Checkbox
                          variant="mark"
                          align="left"
                          class="agree_checkbox"
                        >
                          <template #label>
                            <span class="agree_label">
                              위치정보 서비스 동의사항
                            </span>
                          </template>
                        </Checkbox>
                        <IconButton
                          v-if="depth3HasChildren"
                          iconName="Chevron_down"
                          size="small"
                          class="agree_trigger"
                        />
                        <IconButton
                          v-else
                          iconName="Chevron_right"
                          size="small"
                          aria-label="위치정보 서비스 동의사항 상세 보기"
                          class="agree_trigger"
                        />
                      </div>
                      <!-- depth4 (class is-expand 추가/제거로 펼침/접힘) -->
                      <div
                        class="depth4"
                      >
                        <ul class="agree_sublist box_type">
                          <li class="agree_subitem">
                            <div class="agree_item">
                              <Checkbox
                                variant="mark"
                                align="left"
                                class="agree_checkbox"
                              >
                                <template #label>
                                  <span class="agree_label">
                                    LG U+ 위치정보 사업자 약관동의
                                  </span>
                                </template>
                              </Checkbox>
                              <IconButton
                                iconName="Chevron_right"
                                size="small"
                                aria-label="LG U+ 위치정보 사업자 약관동의 상세 보기"
                                class="agree_trigger"
                              />
                            </div>
                          </li>
                          <li class="agree_subitem">
                            <div class="agree_item">
                              <Checkbox
                                variant="mark"
                                align="left"
                                class="agree_checkbox"
                              >
                                <template #label>
                                  <span class="agree_label">
                                    LG U+ 개인정보수집 이용 및 제3자 제공동의
                                  </span>
                                </template>
                              </Checkbox>
                              <IconButton
                                iconName="Chevron_right"
                                size="small"
                                aria-label="LG U+ 개인정보수집 이용 및 제3자 제공동의 상세 보기"
                                class="agree_trigger"
                              />
                            </div>
                          </li>
                          <li class="agree_subitem">
                            <div class="agree_item">
                              <Checkbox
                                variant="mark"
                                align="left"
                                class="agree_checkbox"
                              >
                                <template #label>
                                  <span class="agree_label">
                                    로플랫 위치정보 사업자 약관동의
                                  </span>
                                </template>
                              </Checkbox>
                              <IconButton
                                iconName="Chevron_right"
                                size="small"
                                aria-label="로플랫 위치정보 사업자 약관동의 상세 보기"
                                class="agree_trigger"
                              />
                            </div>
                          </li>
                        </ul>
                      </div>
                      <!-- //.depth4 -->
                    </li>
                    <li class="agree_subitem">
                      <div class="agree_item">
                        <Checkbox
                          variant="mark"
                          align="left"
                          class="agree_checkbox"
                        >
                          <template #label>
                            <span class="agree_label">
                              개인정보 수집 및 이용동의
                            </span>
                          </template>
                        </Checkbox>
                        <IconButton
                          iconName="Chevron_right"
                          size="small"
                          aria-label="개인정보 수집 및 이용동의 상세 보기"
                          class="agree_trigger"
                        />
                      </div>
                    </li>
                    <li class="agree_subitem">
                      <div class="agree_item">
                        <Checkbox
                          variant="mark"
                          align="left"
                          class="agree_checkbox"
                        >
                          <template #label>
                            <span class="agree_label">
                              위치기반 혜택 알림 수신동의
                            </span>
                          </template>
                        </Checkbox>
                        <IconButton
                          iconName="Chevron_right"
                          size="small"
                          aria-label="위치기반 혜택 알림 수신동의 상세 보기"
                          class="agree_trigger"
                        />
                      </div>
                    </li>
                    <li class="agree_subitem">
                      <div class="agree_item">
                        <Checkbox
                          variant="mark"
                          align="left"
                          class="agree_checkbox"
                        >
                          <template #label>
                            <span class="agree_label">
                              블루칩 씨앤에스 위치정보사업자약관동의
                            </span>
                          </template>
                        </Checkbox>
                        <IconButton
                          iconName="Chevron_right"
                          size="small"
                          aria-label="블루칩 씨앤에스 위치정보사업자약관동의 상세 보기"
                          class="agree_trigger"
                        />
                      </div>
                    </li>
                  </ul>
                </div>
                <!-- //.depth3 -->
              </li>
              <li class="agree_subitem">
                <div class="agree_item">
                  <Checkbox variant="mark" align="left" class="agree_checkbox">
                    <template #label>
<span class="agree_label">
                  [선택] 앱(APP) 알림 수신동의
                      </span>
                    </template>
                  </Checkbox>
                  <IconButton
                    v-if="depth2HasChildren"
                    iconName="Chevron_down"
                    size="small"
                    class="agree_trigger"
                  />
                  <IconButton
                    v-else
                    iconName="Chevron_right"
                    size="small"
                    aria-label="[선택] 앱(APP) 알림 수신동의 상세 보기"
                    class="agree_trigger"
                  />
                </div>
                <!-- depth3 (class is-expand 추가/제거로 펼침/접힘) -->
                <div class="depth3">
                  <ul class="agree_sublist">
                    <li class="agree_subitem">
                      <div class="agree_item">
                        <Checkbox
                          variant="mark"
                          align="left"
                          class="agree_checkbox"
                        >
                          <template #label>
<span class="agree_label">
                            마케팅 정보 수신동의
                            </span>
                          </template>
                        </Checkbox>
                        <IconButton
                          v-if="depth3HasChildren"
                          iconName="Chevron_down"
                          size="small"
                          class="agree_trigger"
                        />
                        <IconButton
                          v-else
                          iconName="Chevron_right"
                          size="small"
                          aria-label="마케팅 정보 수신동의 상세 보기"
                          class="agree_trigger"
                        />
                      </div>
                      <!-- depth4 (class is-expand 추가/제거로 펼침/접힘) -->
                      <div class="depth4">
                        <div class="agree_sublist box_type">
                          <UnorderedList :gap="8">
                            <UnorderedListItem size="small">
                              <span class="list_label">
                                항목: 앱(APP)을 통한 마케팅 정보 수신동의
                              </span>
                            </UnorderedListItem>
                            <UnorderedListItem size="small">
                              <span class="list_label">
                                이용목적: 각종 이벤트, 할인, 이용정보 등의 안내
                              </span>
                            </UnorderedListItem>
                            <UnorderedListItem size="small">
                              <span class="list_label">
                                보유기간: 별도 동의 철회시까지
                              </span>
                            </UnorderedListItem>
                          </UnorderedList>
                        </div>
                      </div>
                      <!-- //.depth4 -->
                    </li>
                  </ul>
                </div>
                <!-- //.depth3 -->
              </li>
            </ul>
          </div>
          <!-- //.depth2 -->
        </li>
        <!-- //.depth1 -->
        <li class="depth1">
          <div class="agree_item">
            <Checkbox variant="box" align="left" class="agree_checkbox">
              <template #label>
                <span class="agree_label">
                  [필수·선택] 신한Pay머니 이용약관
                </span>
              </template>
            </Checkbox>
            <IconButton
              v-if="depth1HasChildren"
              iconName="Chevron_down"
              size="small"
              class="agree_trigger"
            />
            <IconButton
              v-else
              iconName="Chevron_right"
              size="small"
              aria-label="[필수·선택] 신한Pay머니 이용약관 상세 보기"
              class="agree_trigger"
            />
          </div>
          <!-- depth2 (class is-expand 추가/제거로 펼침/접힘) -->
          <div class="depth2">
            <ul class="agree_sublist">
              <li class="agree_subitem">
                <div class="agree_item">
                  <Checkbox variant="mark" align="left" class="agree_checkbox">
                    <template #label>
                      <span class="agree_label">
                        신한Pay머니 이용약관 필수 동의
                      </span>
                    </template>
                  </Checkbox>
                  <IconButton
                    iconName="Chevron_right"
                    size="small"
                    aria-label="신한Pay머니 이용약관 필수 동의 상세 보기"
                    class="agree_trigger"
                  />
                </div>
              </li>
              <li class="agree_subitem">
                <div class="agree_item">
                  <Checkbox variant="mark" align="left" class="agree_checkbox">
                    <template #label>
                      <span class="agree_label">
                        개인정보 수집 및 이용 필수 동의
                      </span>
                    </template>
                  </Checkbox>
                  <IconButton
                    iconName="Chevron_right"
                    size="small"
                    aria-label="개인정보 수집 및 이용 필수 동의 상세 보기"
                    class="agree_trigger"
                  />
                </div>
              </li>
              <li class="agree_subitem">
                <div class="agree_item">
                  <Checkbox variant="mark" align="left" class="agree_checkbox">
                    <template #label>
                      <span class="agree_label">
                        고유식별정보처리 필수 동의
                      </span>
                    </template>
                  </Checkbox>
                  <IconButton
                    iconName="Chevron_right"
                    size="small"
                    aria-label="고유식별정보처리 필수 동의 상세 보기"
                    class="agree_trigger"
                  />
                </div>
              </li>
              <li class="agree_subitem">
                <!-- S: 동의등급제 안내 -->
                <div class="info_card">
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
                        <SolidLabel
                          color="cyan"
                          title="안심"
                        />
                        <SolidLabel
                          color="green"
                          title="다소안심"
                        />
                        <SolidLabel
                          color="yellow"
                          title="보통"
                        />
                        <SolidLabel
                          color="orange"
                          title="신중"
                        />
                        <SolidLabel
                          color="red"
                          title="주의"
                        />
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
                </div>
                <!-- E: 동의등급제 안내 -->
                <div class="agree_item">
                  <Checkbox variant="mark" align="left" class="agree_checkbox">
                    <template #label>
                      <span class="agree_label">
                        [선택] 카드 및 금융상품 ・ 서비스 안내 및 이용권유를 위한 수집 ・ 이용
                      </span>
                      <br />
                      <SolidLabel
                        color="green"
                        title="다소안심"
                        aria-label="동의등급제 다소안심"
                      />
                    </template>
                  </Checkbox>
                  <IconButton
                    iconName="Chevron_down"
                    size="small"
                    class="agree_trigger"
                  />
                </div>
                <!-- depth3 (class is-expand 추가/제거로 펼침/접힘) -->
                <div class="depth3">
                  <ul class="agree_sublist">
                    <li class="agree_subitem">
                      <div class="agree_item">
                        <Checkbox
                          variant="mark"
                          align="left"
                          class="agree_checkbox"
                        >
                          <template #label>
                            <span class="agree_label">
                              고유식별번호 조회 동의
                            </span>
                          </template>
                        </Checkbox>
                      </div>
                    </li>
                    <li class="agree_subitem">
                      <div class="agree_item">
                        <Checkbox
                          variant="mark"
                          align="left"
                          class="agree_checkbox"
                        >
                          <template #label>
                            <span class="agree_label">
                              개인신용정보 제공 동의
                            </span>
                          </template>
                        </Checkbox>
                      </div>
                    </li>
                  </ul>
                  <!-- 하단 우측 정렬 버튼 -->
                  <div class="agree_more">
                    <TextButton
                      class="agree_link"
                      color="secondary"
                      size="small"
                      text="자세히보기"
                      showGoTo
                    />
                  </div>
                </div>
                <!-- //.depth3 -->
              </li>
              <li class="agree_subitem">
                <div class="agree_item">
                  <Checkbox variant="mark" align="left" class="agree_checkbox">
                    <template #label>
                      <span class="agree_label">
                        [선택] 카드 및 금융상품 ・ 서비스 안내 및 이용권유를 위한 수집 ・ 이용
                      </span>
                      <br />
                      <SolidLabel
                        color="yellow"
                        title="보통"
                        aria-label="동의등급제 보통"
                      />
                    </template>
                  </Checkbox>
                  <IconButton
                    iconName="Chevron_down"
                    size="small"
                    class="agree_trigger"
                  />
                </div>
                <!-- depth3 (class is-expand 추가/제거로 펼침/접힘) -->
                <div class="depth3">
                  <ul class="agree_sublist">
                    <li class="agree_subitem">
                      <div class="agree_item">
                        <Checkbox
                          variant="mark"
                          align="left"
                          class="agree_checkbox"
                        >
                          <template #label>
                            <span class="agree_label">
                              고유식별번호 조회 동의
                            </span>
                          </template>
                        </Checkbox>
                      </div>
                    </li>
                    <li class="agree_subitem">
                      <div class="agree_item">
                        <Checkbox
                          variant="mark"
                          align="left"
                          class="agree_checkbox"
                        >
                          <template #label>
                            <span class="agree_label">
                              개인신용정보 제공 동의
                            </span>
                          </template>
                        </Checkbox>
                      </div>
                    </li>
                  </ul>
                  <!-- 하단 우측 정렬 버튼 -->
                  <div class="agree_more">
                    <TextButton
                      class="agree_link"
                      color="secondary"
                      size="small"
                      text="자세히보기"
                      showGoTo
                    />
                  </div>
                </div>
                <!-- //.depth3 -->
              </li>
              <li class="agree_subitem">
                <div class="agree_item">
                  <Checkbox variant="mark" align="left" class="agree_checkbox">
                    <template #label>
                      <span class="agree_label">
                        [선택] 전자적 전송매체를 통한 광고성 정보 수신동의
                      </span>
                    </template>
                  </Checkbox>
                  <IconButton
                    iconName="Chevron_down"
                    size="small"
                    class="agree_trigger"
                  />
                </div>
                <!-- depth3 (class is-expand 추가/제거로 펼침/접힘) -->
                <div class="depth3">
                  <div class="agree_card">
                    <ul class="agree_sublist box_type">
                      <li class="agree_subitem">
                        <div class="agree_item">
                          <Checkbox
                            variant="mark"
                            align="left"
                            class="agree_checkbox"
                          >
                            <template #label>
                              <span class="agree_label">
                                전체
                              </span>
                            </template>
                          </Checkbox>
                        </div>
                      </li>
                      <li class="agree_subitem">
                        <div class="agree_item">
                          <Checkbox
                            variant="mark"
                            align="left"
                            class="agree_checkbox"
                          >
                            <template #label>
                              <span class="agree_label">
                                서면
                              </span>
                            </template>
                          </Checkbox>
                        </div>
                      </li>
                      <li class="agree_subitem">
                        <div class="agree_item">
                          <Checkbox
                            variant="mark"
                            align="left"
                            class="agree_checkbox"
                          >
                            <template #label>
                              <span class="agree_label">
                                이메일
                              </span>
                            </template>
                          </Checkbox>
                        </div>
                      </li>
                      <li class="agree_subitem">
                        <div class="agree_item">
                          <Checkbox
                            variant="mark"
                            align="left"
                            class="agree_checkbox"
                          >
                            <template #label>
                              <span class="agree_label">
                                전화
                              </span>
                            </template>
                          </Checkbox>
                        </div>
                      </li>
                      <li class="agree_subitem">
                        <div class="agree_item">
                          <Checkbox
                            variant="mark"
                            align="left"
                            class="agree_checkbox"
                          >
                            <template #label>
                              <span class="agree_label">
                                휴대폰 메세지(카카오톡, 네이버 알림 등 모바일 메세지 포함)
                              </span>
                            </template>
                          </Checkbox>
                        </div>
                      </li>
                    </ul>
                    <!-- 정보성 리스트 -->
                    <UnorderedList class="agree_infolist" :gap="8">
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
                </div>
                <!-- //.depth3 -->
              </li>
              <li class="agree_subitem">
                <div class="agree_item">
                  <Checkbox variant="mark" align="left" class="agree_checkbox">
                    <template #label>
                      <span class="agree_label">
                        [선택] 카드 및 금융상품 ・ 서비스 안내 및 이용권유를 위한 수집 ・ 이용
                      </span>
                      <br />
                      <SolidLabel
                        color="cyan"
                        title="안심"
                        aria-label="동의등급제 안심"
                      />
                    </template>
                  </Checkbox>
                  <IconButton
                    iconName="Chevron_down"
                    size="small"
                    class="agree_trigger"
                  />
                </div>
                <!-- depth3 (class is-expand 추가/제거로 펼침/접힘) -->
                <div class="depth3">
                  <ul class="agree_sublist">
                    <li class="agree_subitem">
                      <div class="agree_item">
                        <Checkbox
                          variant="mark"
                          align="left"
                          class="agree_checkbox"
                        >
                          <template #label>
                            <span class="agree_label">
                              개인신용정보 제공 동의
                            </span>
                          </template>
                        </Checkbox>
                      </div>
                    </li>
                  </ul>
                  <!-- 하단 우측 정렬 버튼 -->
                  <div class="agree_more">
                    <TextButton
                      class="agree_link"
                      color="secondary"
                      size="small"
                      text="자세히보기"
                      showGoTo
                    />
                  </div>
                </div>
                <!-- //.depth3 -->
              </li>
              <li class="agree_subitem">
                <div class="agree_item">
                  <Checkbox variant="mark" align="left" class="agree_checkbox">
                    <template #label>
                      <span class="agree_label">
                        회원가입 및 발권신청 필수 동의
                      </span>
                    </template>
                  </Checkbox>
                  <IconButton
                    iconName="Chevron_right"
                    size="small"
                    aria-label="회원가입 및 발권신청 필수 동의 상세 보기"
                    class="agree_trigger"
                  />
                </div>
                <p class="agree_infotext">
                  본인은 카드 실제 소유자와 동일하며, 위 기재된 사실과 다름이 없음을 확인하고 회원가입을 신청합니다.
                </p>
              </li>
            </ul>
          </div>
          <!-- //.depth2 -->
        </li>
        <!-- //.depth1 -->
        <li class="depth1">
          <div class="agree_item">
            <Checkbox variant="box" align="left" class="agree_checkbox">
              <template #label>
                <span class="agree_label">
                  [선택] 온라인 회원 이용약관
                </span>
              </template>
            </Checkbox>
            <IconButton
              v-if="depth1HasChildren"
              iconName="Chevron_down"
              size="small"
              class="agree_trigger"
            />
            <IconButton
              v-else
              iconName="Chevron_right"
              size="small"
              aria-label="[선택] 온라인 회원 이용약관 상세 보기"
              class="agree_trigger"
            />
          </div>
          <!-- depth2 (class is-expand 추가/제거로 펼침/접힘) -->
          <div class="depth2">
            <ul class="agree_sublist">
              <li class="agree_subitem">
                <div class="agree_item">
                  <Checkbox variant="mark" align="left" class="agree_checkbox">
                    <template #label>
                      <span class="agree_label">
                        온라인 회원 이용약관 필수 동의
                      </span>
                    </template>
                  </Checkbox>
                  <IconButton
                    iconName="Chevron_right"
                    size="small"
                    aria-label="온라인 회원 이용약관 필수 동의 상세 보기"
                    class="agree_trigger"
                  />
                </div>
              </li>
              <li class="agree_subitem">
                <div class="agree_item">
                  <Checkbox variant="mark" align="left" class="agree_checkbox">
                    <template #label>
                      <span class="agree_label">
                        개인정보 수집·이용 필수 동의
                      </span>
                    </template>
                  </Checkbox>
                  <IconButton
                    iconName="Chevron_right"
                    size="small"
                    aria-label="개인정보 수집·이용 필수 동의 상세 보기"
                    class="agree_trigger"
                  />
                </div>
              </li>
            </ul>
          </div>
          <!-- //.depth2 -->
        </li>
        <!-- //.depth1 -->
        <li class="depth1">
          <div class="agree_item">
            <Checkbox variant="box" align="left" class="agree_checkbox">
              <template #label>
                <span class="agree_label">
                  [선택] 신한 슈퍼SOL 이용약관
                </span>
              </template>
            </Checkbox>
            <IconButton
              v-if="depth1HasChildren"
              iconName="Chevron_down"
              size="small"
              class="agree_trigger"
            />
            <IconButton
              v-else
              iconName="Chevron_right"
              size="small"
              aria-label="[선택] 신한 슈퍼SOL 이용약관 상세 보기"
              class="agree_trigger"
            />
          </div>
          <!-- depth2 (class is-expand 추가/제거로 펼침/접힘) -->
          <div class="depth2">
            <!-- S: 동의등급제 안내 -->
            <div class="info_card">
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
                    <SolidLabel
                      color="cyan"
                      title="안심"
                    />
                    <SolidLabel
                      color="green"
                      title="다소안심"
                    />
                    <SolidLabel
                      color="yellow"
                      title="보통"
                    />
                    <SolidLabel
                      color="orange"
                      title="신중"
                    />
                    <SolidLabel
                      color="red"
                      title="주의"
                    />
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
            </div>
            <!-- E: 동의등급제 안내 -->
            
            <ul class="agree_sublist">
              <li class="agree_subitem">
                <div class="agree_item">
                  <Checkbox variant="mark" align="left" class="agree_checkbox">
                    <template #label>
                      <span class="agree_label">
                        신한 모바일 플랫폼 이용약관 필수 동의
                      </span>
                    </template>
                  </Checkbox>
                  <IconButton
                    iconName="Chevron_right"
                    size="small"
                    aria-label="신한 모바일 플랫폼 이용약관 필수 동의 상세 보기"
                    class="agree_trigger"
                  />
                </div>
              </li>
              <li class="agree_subitem">
                <div class="agree_item">
                  <Checkbox variant="mark" align="left" class="agree_checkbox">
                    <template #label>
                      <span class="agree_label">
                        신한금융그룹 통합 포인트 서비스 이용 필수 동의
                      </span>
                    </template>
                  </Checkbox>
                  <IconButton
                    iconName="Chevron_right"
                    size="small"
                    aria-label="신한금융그룹 통합 포인트 서비스 이용 필수 동의 상세 보기"
                    class="agree_trigger"
                  />
                </div>
              </li>
              <li class="agree_subitem">
                <div class="agree_item">
                  <Checkbox variant="mark" align="left" class="agree_checkbox">
                    <template #label>
                      <span class="agree_label">
                        개인(신용)정보 수집·이용·제공 필수 동의
                      </span>
                    </template>
                  </Checkbox>
                  <IconButton
                    iconName="Chevron_right"
                    size="small"
                    aria-label="개인(신용)정보 수집·이용·제공 필수 동의 상세 보기"
                    class="agree_trigger"
                  />
                </div>
              </li>
              <li class="agree_subitem">
                <div class="agree_item">
                  <Checkbox variant="mark" align="left" class="agree_checkbox">
                    <template #label>
                      <span class="agree_label">
                        개인(신용)정보 수집·이용·제공 필수 동의(포인트 서비스 제공)
                      </span>
                    </template>
                  </Checkbox>
                  <IconButton
                    iconName="Chevron_right"
                    size="small"
                    aria-label="개인(신용)정보 수집·이용·제공 필수 동의(포인트 서비스 제공) 상세 보기"
                    class="agree_trigger"
                  />
                </div>
              </li>
              <li class="agree_subitem">
                <div class="agree_item">
                  <Checkbox variant="mark" align="left" class="agree_checkbox">
                    <template #label>
                      <span class="agree_label">
                        전자금융서비스 이용 필수 동의(신한은행)
                      </span>
                    </template>
                  </Checkbox>
                  <IconButton
                    iconName="Chevron_down"
                    size="small"
                    class="agree_trigger"
                  />
                </div>
                <!-- depth3 (class is-expand 추가/제거로 펼침/접힘) -->
                <div class="depth3">
                  <div class="agree_card">
                    <ul class="agree_sublist box_type">
                      <li class="agree_subitem">
                        <div class="agree_item">
                          <span class="agree_label">
                            전자금융거래 기본약관
                          </span>
                          <IconButton
                            iconName="Chevron_right"
                            size="small"
                            aria-label="전자금융거래 기본약관 상세 보기"
                            class="agree_trigger"
                          />
                        </div>
                      </li>
                      <li class="agree_subitem">
                        <div class="agree_item">
                          <span class="agree_label">
                            신한온라인서비스 이용약관
                          </span>
                          <IconButton
                            iconName="Chevron_right"
                            size="small"
                            aria-label="신한온라인서비스 이용약관 상세 보기"
                            class="agree_trigger"
                          />
                        </div>
                      </li>
                      <li class="agree_subitem">
                        <div class="agree_item">
                          <span class="agree_label">
                            전자통지서비스 이용약관
                          </span>
                          <IconButton
                            iconName="Chevron_right"
                            size="small"
                            aria-label="전자통지서비스 이용약관 상세 보기"
                            class="agree_trigger"
                          />
                        </div>
                      </li>
                      <li class="agree_subitem">
                        <div class="agree_item">
                          <span class="agree_label">
                            개인정보 수집 이용 동의(비여신 금융거래)
                          </span>
                          <IconButton
                            iconName="Chevron_right"
                            size="small"
                            aria-label="개인정보 수집 이용 동의(비여신 금융거래) 상세 보기"
                            class="agree_trigger"
                          />
                        </div>
                      </li>
                    </ul>
                  </div>
                </div>
                <!-- //.depth3 -->
              </li>
              <li class="agree_subitem">
                <div class="agree_item">
                  <Checkbox variant="mark" align="left" class="agree_checkbox">
                    <template #label>
                      <span class="agree_label">
                        그룹 로열티 서비스 이용 필수 동의(신한은행)
                      </span>
                    </template>
                  </Checkbox>
                  <IconButton
                    iconName="Chevron_right"
                    size="small"
                    aria-label="그룹 로열티 서비스 이용 필수 동의(신한은행) 상세 보기"
                    class="agree_trigger"
                  />
                </div>
              </li>
              <li class="agree_subitem">
                <div class="agree_item">
                  <Checkbox variant="mark" align="left" class="agree_checkbox">
                    <template #label>
                      <span class="agree_label">
                        개인(신용)정보 수집·이용·제공 필수 동의(신한은행)
                      </span>
                    </template>
                  </Checkbox>
                  <IconButton
                    iconName="Chevron_right"
                    size="small"
                    aria-label="개인(신용)정보 수집·이용·제공 필수 동의(신한은행) 상세 보기"
                    class="agree_trigger"
                  />
                </div>
              </li>
              <li class="agree_subitem">
                <div class="agree_item">
                  <Checkbox variant="mark" align="left" class="agree_checkbox">
                    <template #label>
                      <span class="agree_label">
                        [선택] 개인(신용)정보 수집 ・ 이용 ・ 제공 동의(상품 서비스 안내 등)
                      </span>
                      <br />
                      <SolidLabel
                        color="cyan"
                        title="안심"
                      />
                    </template>
                  </Checkbox>
                  <IconButton
                    iconName="Chevron_right"
                    size="small"
                    aria-label="[선택] 개인(신용)정보 수집 ・ 이용 ・ 제공 동의(상품 서비스 안내 등) 상세 보기"
                    class="agree_trigger"
                  />
                </div>
              </li>
              <li class="agree_subitem">
                <div class="agree_item">
                  <Checkbox variant="mark" align="left" class="agree_checkbox">
                    <template #label>
                      <span class="agree_label">
                        [선택] 개인(신용)정보 수집 ・ 이용 ・ 제공 동의(상품 서비스 안내 등)(신한은행)
                      </span>
                      <br />
                      <SolidLabel
                        color="cyan"
                        title="안심"
                      />
                    </template>
                  </Checkbox>
                  <IconButton
                    iconName="Chevron_right"
                    size="small"
                    aria-label="[선택] 개인(신용)정보 수집 ・ 이용 ・ 제공 동의(상품 서비스 안내 등)(신한은행) 상세 보기"
                    class="agree_trigger"
                  />
                </div>
              </li>
              <li class="agree_subitem">
                <div class="agree_item">
                  <Checkbox variant="mark" align="left" class="agree_checkbox">
                    <template #label>
                      <span class="agree_label">
                        [선택] 광고성 전자적 수신매체 전송 동의
                      </span>
                    </template>
                  </Checkbox>
                  <IconButton
                    iconName="Chevron_down"
                    size="small"
                    class="agree_trigger"
                  />
                </div>
                <!-- depth3 (class is-expand 추가/제거로 펼침/접힘) -->
                <div class="depth3">
                  <div class="agree_card">
                    <ul class="agree_sublist box_type">
                      <li class="agree_subitem">
                        <div class="agree_item">
                          <Checkbox
                            variant="mark"
                            align="left"
                            class="agree_checkbox"
                          >
                            <template #label>
                              <span class="agree_label">
                                전체
                              </span>
                            </template>
                          </Checkbox>
                        </div>
                      </li>
                      <li class="agree_subitem">
                        <div class="agree_item">
                          <Checkbox
                            variant="mark"
                            align="left"
                            class="agree_checkbox"
                          >
                            <template #label>
                              <span class="agree_label">
                                이메일
                              </span>
                            </template>
                          </Checkbox>
                        </div>
                      </li>
                      <li class="agree_subitem">
                        <div class="agree_item">
                          <Checkbox
                            variant="mark"
                            align="left"
                            class="agree_checkbox"
                          >
                            <template #label>
                              <span class="agree_label">
                                전화
                              </span>
                            </template>
                          </Checkbox>
                        </div>
                      </li>
                    </ul>
                  </div>
                </div>
                <!-- //.depth3 -->
              </li>
            </ul>
          </div>
          <!-- //.depth2 -->
        </li>
        <!-- //.depth1 -->
        <li class="depth1">
          <div class="agree_item">
            <Checkbox variant="box" align="left" class="agree_checkbox">
              <template #label>
                <span class="agree_label">
                  [선택] 전자문서 서비스 이용약관
                </span>
              </template>
            </Checkbox>
            <IconButton
              v-if="depth1HasChildren"
              iconName="Chevron_down"
              size="small"
              class="agree_trigger"
            />
            <IconButton
              v-else
              iconName="Chevron_right"
              size="small"
              aria-label="[선택] 전자문서 서비스 이용약관 상세 보기"
              class="agree_trigger"
            />
          </div>
          <!-- depth2 (class is-expand 추가/제거로 펼침/접힘) -->
          <div class="depth2">
            <ul class="agree_sublist">
              <li class="agree_subitem">
                <div class="agree_item">
                  <Checkbox variant="mark" align="left" class="agree_checkbox">
                    <template #label>
                      <span class="agree_label">
                        전자문서 서비스 이용약관 필수 동의
                      </span>
                    </template>
                  </Checkbox>
                  <IconButton
                    iconName="Chevron_right"
                    size="small"
                    aria-label="전자문서 서비스 이용약관 필수 동의 상세 보기"
                    class="agree_trigger"
                  />
                </div>
              </li>
              <li class="agree_subitem">
                <div class="agree_item">
                  <Checkbox variant="mark" align="left" class="agree_checkbox">
                    <template #label>
                      <span class="agree_label">
                        전자문서 개인정보 수집·이용 필수 동의
                      </span>
                    </template>
                  </Checkbox>
                  <IconButton
                    iconName="Chevron_right"
                    size="small"
                    aria-label="전자문서 개인정보 수집·이용 필수 동의 상세 보기"
                    class="agree_trigger"
                  />
                </div>
              </li>
              <li class="agree_subitem">
                <div class="agree_item">
                  <Checkbox variant="mark" align="left" class="agree_checkbox">
                    <template #label>
                      <span class="agree_label">
                        개인정보 제3자 제공 필수 동의
                      </span>
                    </template>
                  </Checkbox>
                  <IconButton
                    iconName="Chevron_right"
                    size="small"
                    aria-label="개인정보 제3자 제공 필수 동의 상세 보기"
                    class="agree_trigger"
                  />
                </div>
              </li>
              <li class="agree_subitem">
                <div class="agree_item">
                  <Checkbox variant="mark" align="left" class="agree_checkbox">
                    <template #label>
                      <span class="agree_label">
                        서비스 유의사항 필수 동의
                      </span>
                    </template>
                  </Checkbox>
                  <IconButton
                    iconName="Chevron_right"
                    size="small"
                    aria-label="서비스 유의사항 필수 동의 상세 보기"
                    class="agree_trigger"
                  />
                </div>
              </li>
            </ul>
          </div>
          <!-- //.depth2 -->
        </li>
        <!-- //.depth1 -->
        <li class="depth1">
          <div class="agree_item">
            <Checkbox variant="box" align="left" class="agree_checkbox">
              <template #label>
                <span class="agree_label">
                  [선택] 마이데이터 서비스 이용약관
                </span>
              </template>
            </Checkbox>
            <IconButton
              v-if="depth1HasChildren"
              iconName="Chevron_down"
              size="small"
              class="agree_trigger"
            />
            <IconButton
              v-else
              iconName="Chevron_right"
              size="small"
              aria-label="[선택] 마이데이터 서비스 이용약관 상세 보기"
              class="agree_trigger"
            />
          </div>
          <!-- depth2 (class is-expand 추가/제거로 펼침/접힘) -->
          <div class="depth2">
            <ul class="agree_sublist">
              <li class="agree_subitem">
                <div class="agree_item">
                  <Checkbox variant="mark" align="left" class="agree_checkbox">
                    <template #label>
                      <span class="agree_label">
                        마이데이터 서비스 이용약관 필수 동의
                      </span>
                    </template>
                  </Checkbox>
                  <IconButton
                    iconName="Chevron_right"
                    size="small"
                    aria-label="마이데이터 서비스 이용약관 필수 동의 상세 보기"
                    class="agree_trigger"
                  />
                </div>
              </li>
              <li class="agree_subitem">
                <div class="agree_item">
                  <Checkbox variant="mark" align="left" class="agree_checkbox">
                    <template #label>
                      <span class="agree_label">
                        마이데이터 서비스 개인(신용)정보의 수집 및 이용 필수 동의
                      </span>
                    </template>
                  </Checkbox>
                  <IconButton
                    iconName="Chevron_right"
                    size="small"
                    aria-label="마이데이터 서비스 개인(신용)정보의 수집 및 이용 필수 동의 상세 보기"
                    class="agree_trigger"
                  />
                </div>
              </li>
            </ul>
            <!-- 하단 우측 정렬 버튼 -->
            <div class="agree_more">
              <TextButton
                class="agree_link"
                color="secondary"
                size="small"
                text="개인정보 처리방침"
                showGoTo
              />
            </div>
          </div>
          <!-- //.depth2 -->
        </li>
        <!-- //.depth1 -->
        <li class="depth1">
          <div class="agree_item">
            <Checkbox variant="box" align="left" class="agree_checkbox">
              <template #label>
                <span class="agree_label">
                  [선택] 마케팅 동의 이용약관
                </span>
              </template>
            </Checkbox>
            <IconButton
              v-if="depth1HasChildren"
              iconName="Chevron_down"
              size="small"
              class="agree_trigger"
            />
            <IconButton
              v-else
              iconName="Chevron_right"
              size="small"
              aria-label="[선택] 마케팅 동의 이용약관 상세 보기"
              class="agree_trigger"
            />
          </div>
          <!-- depth2 (class is-expand 추가/제거로 펼침/접힘) -->
          <div class="depth2">
            <ul class="agree_sublist">
              <li class="agree_subitem">
                <div class="agree_item">
                  <Checkbox variant="mark" align="left" class="agree_checkbox">
                    <template #label>
                      <span class="agree_label">
                        [선택] 카드 및 금융상품 ・ 서비스 안내 및 이용권유를 위한 수집 ・ 이용
                      </span>
                      <br />
                      <SolidLabel
                        color="green"
                        title="다소안심"
                        aria-label="동의등급제 다소안심"
                      />
                    </template>
                  </Checkbox>
                  <IconButton
                    iconName="Chevron_down"
                    size="small"
                    class="agree_trigger"
                  />
                </div>
                <!-- depth3 (class is-expand 추가/제거로 펼침/접힘) -->
                <div class="depth3">
                  <ul class="agree_sublist">
                    <li class="agree_subitem">
                      <div class="agree_item">
                        <Checkbox
                          variant="mark"
                          align="left"
                          class="agree_checkbox"
                        >
                          <template #label>
                            <span class="agree_label">
                              고유식별번호 조회 동의
                            </span>
                          </template>
                        </Checkbox>
                      </div>
                    </li>
                    <li class="agree_subitem">
                      <div class="agree_item">
                        <Checkbox
                          variant="mark"
                          align="left"
                          class="agree_checkbox"
                        >
                          <template #label>
                            <span class="agree_label">
                              개인신용정보 제공 동의
                            </span>
                          </template>
                        </Checkbox>
                      </div>
                    </li>
                  </ul>
                  <!-- 하단 우측 정렬 버튼 -->
                  <div class="agree_more">
                    <TextButton
                      class="agree_link"
                      color="secondary"
                      size="small"
                      text="자세히보기"
                      showGoTo
                    />
                  </div>
                </div>
                <!-- //.depth3 -->
              </li>
              <li class="agree_subitem">
                <div class="agree_item">
                  <Checkbox variant="mark" align="left" class="agree_checkbox">
                    <template #label>
                      <span class="agree_label">
                        [선택] 카드 및 금융상품 ・ 서비스 이외의 부수서비스 안내 등을 위한 수집 ・ 이용
                      </span>
                      <br />
                      <SolidLabel
                        color="yellow"
                        title="보통"
                        aria-label="동의등급제 보통"
                      />
                    </template>
                  </Checkbox>
                  <IconButton
                    iconName="Chevron_down"
                    size="small"
                    class="agree_trigger"
                  />
                </div>
                <!-- depth3 (class is-expand 추가/제거로 펼침/접힘) -->
                <div class="depth3">
                  <ul class="agree_sublist">
                    <li class="agree_subitem">
                      <div class="agree_item">
                        <Checkbox
                          variant="mark"
                          align="left"
                          class="agree_checkbox"
                        >
                          <template #label>
                            <span class="agree_label">
                              고유식별번호 조회 동의
                            </span>
                          </template>
                        </Checkbox>
                      </div>
                    </li>
                    <li class="agree_subitem">
                      <div class="agree_item">
                        <Checkbox
                          variant="mark"
                          align="left"
                          class="agree_checkbox"
                        >
                          <template #label>
                            <span class="agree_label">
                              개인신용정보 제공 동의
                            </span>
                          </template>
                        </Checkbox>
                      </div>
                    </li>
                  </ul>
                  <!-- 하단 우측 정렬 버튼 -->
                  <div class="agree_more">
                    <TextButton
                      class="agree_link"
                      color="secondary"
                      size="small"
                      text="자세히보기"
                      showGoTo
                    />
                  </div>
                </div>
                <!-- //.depth3 -->
              </li>
              <li class="agree_subitem">
                <div class="agree_item">
                  <Checkbox variant="mark" align="left" class="agree_checkbox">
                    <template #label>
                      <span class="agree_label">
                        [선택] 전자적 전송매체를 통한 광고성 정보 수신동의
                      </span>
                    </template>
                  </Checkbox>
                  <IconButton
                    iconName="Chevron_down"
                    size="small"
                    class="agree_trigger"
                  />
                </div>
                <!-- depth3 (class is-expand 추가/제거로 펼침/접힘) -->
                <div class="depth3">
                  <div class="agree_card">
                    <ul class="agree_sublist box_type">
                      <li class="agree_subitem">
                        <div class="agree_item">
                          <Checkbox
                            variant="mark"
                            align="left"
                            class="agree_checkbox"
                          >
                            <template #label>
                              <span class="agree_label">
                                전체
                              </span>
                            </template>
                          </Checkbox>
                        </div>
                      </li>
                      <li class="agree_subitem">
                        <div class="agree_item">
                          <Checkbox
                            variant="mark"
                            align="left"
                            class="agree_checkbox"
                          >
                            <template #label>
                              <span class="agree_label">
                                서면
                              </span>
                            </template>
                          </Checkbox>
                        </div>
                      </li>
                      <li class="agree_subitem">
                        <div class="agree_item">
                          <Checkbox
                            variant="mark"
                            align="left"
                            class="agree_checkbox"
                          >
                            <template #label>
                              <span class="agree_label">
                                이메일
                              </span>
                            </template>
                          </Checkbox>
                        </div>
                      </li>
                      <li class="agree_subitem">
                        <div class="agree_item">
                          <Checkbox
                            variant="mark"
                            align="left"
                            class="agree_checkbox"
                          >
                            <template #label>
                              <span class="agree_label">
                                전화
                              </span>
                            </template>
                          </Checkbox>
                        </div>
                      </li>
                      <li class="agree_subitem">
                        <div class="agree_item">
                          <Checkbox
                            variant="mark"
                            align="left"
                            class="agree_checkbox"
                          >
                            <template #label>
                              <span class="agree_label">
                                휴대폰 메세지(카카오톡, 네이버 알림 등 모바일 메세지 포함)
                              </span>
                            </template>
                          </Checkbox>
                        </div>
                      </li>
                    </ul>
                    <!-- 정보성 리스트 -->
                    <UnorderedList class="agree_infolist" :gap="8">
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
                </div>
                <!-- //.depth3 -->
              </li>
              <li class="agree_subitem">
                <div class="agree_item">
                  <Checkbox variant="mark" align="left" class="agree_checkbox">
                    <template #label>
                      <span class="agree_label">
                        [선택] 신한금융 자회사 및 손자회사에 개인(신용)정보를 제공
                      </span>
                      <br />
                      <SolidLabel
                        color="cyan"
                        title="안심"
                        aria-label="동의등급제 안심"
                      />
                    </template>
                  </Checkbox>
                  <IconButton
                    iconName="Chevron_down"
                    size="small"
                    class="agree_trigger"
                  />
                </div>
                <!-- depth3 (class is-expand 추가/제거로 펼침/접힘) -->
                <div class="depth3">
                  <ul class="agree_sublist">
                    <li class="agree_subitem">
                      <div class="agree_item">
                        <Checkbox
                          variant="mark"
                          align="left"
                          class="agree_checkbox"
                        >
                          <template #label>
                            <span class="agree_label">
                              개인신용정보 제공 동의
                            </span>
                          </template>
                        </Checkbox>
                      </div>
                    </li>
                  </ul>
                  <!-- 하단 우측 정렬 버튼 -->
                  <div class="agree_more">
                    <TextButton
                      class="agree_link"
                      color="secondary"
                      size="small"
                      text="자세히보기"
                      showGoTo
                    />
                  </div>
                </div>
                <!-- //.depth3 -->
              </li>
            </ul>
          </div>
          <!-- //.depth2 -->
        </li>
        <!-- //.depth1 -->
      </ul>
    </div>
    <!-- //.agree_wrap -->
  </div>




// 개발 요청 약관 체크 구조
.agree_wrap {
  padding: 0 var(--spacing-2xl);
  ul, li {
    line-height: 1;
  }
  // 전체 약관 모두 동의
  .agree_allcheck {
    margin-bottom: var(--spacing-lg);
    .sv-checkbox {
      display: flex;
      align-items: center;
      height: 58px;
      padding: var(--spacing-xl) var(--spacing-2xl);
      border-radius: var(--radius-xl);
      background-color: var(--bg-graylight);
    }
    .sv-checkbox__label {
      @include font-set("title-m", 500);
      color: var(--text-secondary);
      label {
        width: 100%;
      }
    }
  }
  .agree_trigger {
    flex: 0;
    &.sv-icon-button {
      color: var(--fg-quaternary);
    }
  }
}
// 약관 체크 항목
.agree_list {
  .agree_item {
    display: flex;
    align-items: center;
    min-height: 48px;
    padding: var(--spacing-lg) var(--spacing-2xl);
    .agree_trigger {
      align-self: flex-start;
      .sv-icon-button__icon-container {
        height: 24px !important;
        svg {
          margin-top: 1px;
        }
      }
      &[aria-expanded="true"] {
        transform: rotate(180deg);
        transition: transform 0.2s ease;
      }
    }
  }
  .agree_more {
    display: flex;
    justify-content: flex-end;
    align-items: center;
    height: 40px;
    padding-right: var(--spacing-2xl);
    padding-left: var(--spacing-2xl);
    .agree_link {
      height: 100%;
    }
    .sv-button--size-s.sv-button--variant-ghost .sv-button__label,
    .sv-button__label {
      @include font-set("body-s", 500);
      color: var(--text-secondary);
    }
    .sv-button__right-icon {
      color: var(--fg-secondary);
    }
  }
  .agree_checkbox {
    flex: 1 1 auto;
    ~ .agree_trigger {
      margin-left: var(--spacing-md);
    }
    .sv-checkbox__label {
      @include font-set("title-s", 500);
    }
    .sv-checkbox__input {
      align-self: flex-start;
    }
    .agree_label {
      ~ .sv-label {
        margin-top: var(--spacing-xs);
      }
    }
  }
  .info_card,
  .agree_card {
    padding-right: var(--spacing-2xl);
    padding-left: var(--spacing-2xl);
  }
  .agree_sublist {
    &.box_type {
      margin-bottom: var(--spacing-md);
      padding: var(--spacing-lg) var(--spacing-xl);
      border-radius: var(--radius-lg);
      background-color: var(--bg-ongray_graylight_a5);
      .agree_item {
        align-items: flex-start;
        min-height: 20px;
        padding: 0;

        > .agree_label {
          display: flex;
          flex: 1 1 auto;
          min-width: 0;
          @include font-set("body-s", 300);
          color: var(--text-tertiary);
        }
      }
      .agree_checkbox {
        .sv-checkbox__label {
          @include font-set("body-s", 300);
          color: var(--text-tertiary);
          label {
            width: 100%;
          }
        }
      }
      .sv-checkbox__input {
        align-self: flex-start;
      }
      .agree_trigger {
        .sv-icon-button__icon-container {
          height: 24px !important;
          svg {
            margin-top: 1px;
          }
        }
      }
      .agree_subitem ~ .agree_subitem {
        margin-top: var(--spacing-md);
      }
      .sv-text-list--size-small {
        color: var(--text-tertiary);
      }
      .list_label {
        font-size: inherit;
        font-weight: inherit;
        line-height: inherit;
        letter-spacing: inherit;
        color: inherit;
      }
    }
  }
  .agree_infolist {
    margin-bottom: var(--spacing-md);
    .sv-text-list__content {
      color: var(--text-quaternary);
    }
  }
  .agree_infotext {
    margin-bottom: var(--spacing-md);
    padding-right: var(--spacing-2xl);
    padding-left: calc(var(--spacing-2xl) + var(--spacing-4xl));
    @include font-set("body-s", 300);
    color: var(--text-tertiary);
  }
  // 펼침/접힘: 펼칠 때 .5s ease-strong-in, 접힐 때 ease-strong-out (max-height 숫자만 전환 가능)
  .depth2,
  .depth3,
  .depth4 {
    overflow: hidden;
    height: 0;
    transition: height 0.5s var(--ease-strong-out);
    &.is-expand {
      overflow: visible;
      height: auto;
      transition: height 0.5s var(--ease-strong-in);
    }
  }
  .depth3 {
    padding-left: calc(var(--spacing-4xl) - var(--spacing-sm));
  }
  .depth4 {
    padding-right: var(--spacing-2xl);
    padding-left: 48px;
  }
}


<route lang="yaml">
meta:
  id: SSN017A01-html
  title: 약관동의
  menu: Sign in/up > 약관동의(머니회원)
  layout: SubLayout
  category: Sign in/up
  publish: 김대민
  publishVersion: 0.9
  status: 재작업
  etc: |
    [v0.9]260123: 신한Pay머니 이용약관 문구 수정 및 항목 삭제(디채관),
    안심 color 변경 blue에서 color=cyan,
    [251027] 마이데이터 서비스 안내 하단 링크 추가
  header:
    fixed: true
    close: true
  qa: 퍼블완료
  qa2:
  ui: |
    [완료]260115: 마크업 (문구 수정 셨더라도 -> 동의하셨더라도),
    [완료]260113: (디자인 추가검수 UI 수정),
    [완료]260109: 마크업 (리스트 사이 간격 수정 :gap="8" 추가),
    [완료]260105: 마크업 (260105: 디자인 동기화 - 약관 체크항목 추가, 종합포털 바로가기 버튼 크기 수정 small->xsmall),
</route>
<template>
  <!-- 콘텐츠 영역 -->
  <div class="sc-contents__body sc-agree__page">
    <!-- 구조 수정 260318: 개발 전달용 -->
    <div class="agree_wrap" @click="onAgreeListClick">
      <!-- 전체 약관 선택 -->
      <div class="agree_allcheck">
        <Checkbox
          v-model="agreeAll"
          class="agree_checkbox"
          variant="box"
          align="left"
        >
          <template #label>
            <span class="agree_label">
              전체 약관 모두 동의
            </span>
          </template>
        </Checkbox>
      </div>
      <!-- 약관 리스트 (depth1 개수 파악용 ref) -->
      <ul ref="agreeListRef" class="agree_list">
        <li class="depth1">
          <!--
            depth1의 checkbox는 variant="box" variant="mark" 스타일 구분
            디자인에 맞춰서 작업 
          -->
          <div class="agree_item">
            <Checkbox variant="box" align="left" class="agree_checkbox">
              <template #label>
                <span class="agree_label">
                  [필수·선택] 서비스 이용약관
                </span>
              </template>
            </Checkbox>
            <!-- 
              아이콘 버튼은 
              하위 뎁스가 있는 경우 Chevron_down(펼침 시) / Chevron_right(접힘 시)
              하위 뎁스가 없는 경우 Chevron_right(상세 보기만)
              aria-label·aria-expanded 상황에 맞게 사용
            -->
            <IconButton
              v-if="depth1HasChildren"
              iconName="Chevron_down"
              size="small"
              class="agree_trigger"
            />
            <IconButton
              v-else
              iconName="Chevron_right"
              size="small"
              aria-label="[필수·선택] 서비스 이용약관 상세 보기"
              class="agree_trigger"
            />
          </div>
          <!-- depth2 (class is-expand 추가/제거로 펼침/접힘) -->
          <div class="depth2">
            <ul class="agree_sublist">
              <li class="agree_subitem">
                <div class="agree_item">
                  <Checkbox variant="mark" align="left" class="agree_checkbox">
                    <template #label>
                      <span class="agree_label">
                        앱카드 서비스 이용약관 필수 동의
                      </span>
                    </template>
                  </Checkbox>
                  <IconButton
                    iconName="Chevron_right"
                    size="small"
                    aria-label="앱카드 서비스 이용약관 필수 동의 상세 보기"
                    class="agree_trigger"
                  />
                </div>
              </li>
              <li class="agree_subitem">
                <div class="agree_item">
                  <Checkbox variant="mark" align="left" class="agree_checkbox">
                    <template #label>
                      <span class="agree_label">
                        개인(신용)정보의 수집 및 이용 필수 동의
                      </span>
                    </template>
                  </Checkbox>
                  <IconButton
                    iconName="Chevron_right"
                    size="small"
                    aria-label="앱카드 서비스 이용약관 필수 동의 상세 보기"
                    class="agree_trigger"
                  />
                </div>
              </li>
              <li class="agree_subitem">
                <div class="agree_item">
                  <Checkbox variant="mark" align="left" class="agree_checkbox">
                    <template #label>
                      <span class="agree_label">
                        고유식별정보처리 필수 동의
                      </span>
                    </template>
                  </Checkbox>
                  <IconButton
                    iconName="Chevron_right"
                    size="small"
                    aria-label="앱카드 서비스 이용약관 필수 동의 상세 보기"
                    class="agree_trigger"
                  />
                </div>
              </li>
              <li class="agree_subitem">
                <div class="agree_item">
                  <Checkbox variant="mark" align="left" class="agree_checkbox">
                    <template #label>
                      <span class="agree_label">
                        [선택] 위치기반 서비스 약관동의
                      </span>
                    </template>
                  </Checkbox>
                  <IconButton
                    v-if="depth2HasChildren"
                    iconName="Chevron_down"
                    size="small"
                    class="agree_trigger"
                  />
                  <IconButton
                    v-else
                    iconName="Chevron_right"
                    size="small"
                    aria-label="앱카드 서비스 이용약관 필수 동의 상세 보기"
                    class="agree_trigger"
                  />
                </div>
                <!-- depth3 (class is-expand 추가/제거로 펼침/접힘) -->
                <div class="depth3">
                  <ul class="agree_sublist">
                    <li class="agree_subitem">
                      <div class="agree_item">
                        <Checkbox
                          variant="mark"
                          align="left"
                          class="agree_checkbox"
                        >
                          <template #label>
                            <span class="agree_label">
                              신한카드 위치기반 사업자 약관 동의
                            </span>
                          </template>
                        </Checkbox>
                        <IconButton
                          iconName="Chevron_right"
                          size="small"
                          aria-label="신한카드 위치기반 사업자 약관 동의 상세 보기"
                          class="agree_trigger"
                        />
                      </div>
                    </li>
                    <li class="agree_subitem">
                      <div class="agree_item">
                        <Checkbox
                          variant="mark"
                          align="left"
                          class="agree_checkbox"
                        >
                          <template #label>
                            <span class="agree_label">
                              위치정보 서비스 동의사항
                            </span>
                          </template>
                        </Checkbox>
                        <IconButton
                          v-if="depth3HasChildren"
                          iconName="Chevron_down"
                          size="small"
                          class="agree_trigger"
                        />
                        <IconButton
                          v-else
                          iconName="Chevron_right"
                          size="small"
                          aria-label="신한카드 위치기반 사업자 약관 동의 상세 보기"
                          class="agree_trigger"
                        />
                      </div>
                      <!-- depth4 (class is-expand 추가/제거로 펼침/접힘) -->
                      <div
                        class="depth4"
                      >
                        <ul class="agree_sublist box_type">
                          <li class="agree_subitem">
                            <div class="agree_item">
                              <Checkbox
                                variant="mark"
                                align="left"
                                class="agree_checkbox"
                              >
                                <template #label>
                                  <span class="agree_label">
                                    LG U+ 위치정보 사업자 약관동의
                                  </span>
                                </template>
                              </Checkbox>
                              <IconButton
                                iconName="Chevron_right"
                                size="small"
                                aria-label="LG U+ 위치정보 사업자 약관동의 상세 보기"
                                class="agree_trigger"
                              />
                            </div>
                          </li>
                          <li class="agree_subitem">
                            <div class="agree_item">
                              <Checkbox
                                variant="mark"
                                align="left"
                                class="agree_checkbox"
                              >
                                <template #label>
                                  <span class="agree_label">
                                    LG U+ 개인정보수집 이용 및 제3자 제공동의
                                  </span>
                                </template>
                              </Checkbox>
                              <IconButton
                                iconName="Chevron_right"
                                size="small"
                                aria-label="LG U+ 위치정보 사업자 약관동의 상세 보기"
                                class="agree_trigger"
                              />
                            </div>
                          </li>
                          <li class="agree_subitem">
                            <div class="agree_item">
                              <Checkbox
                                variant="mark"
                                align="left"
                                class="agree_checkbox"
                              >
                                <template #label>
                                  <span class="agree_label">
                                    로플랫 위치정보 사업자 약관동의
                                  </span>
                                </template>
                              </Checkbox>
                              <IconButton
                                iconName="Chevron_right"
                                size="small"
                                aria-label="LG U+ 위치정보 사업자 약관동의 상세 보기"
                                class="agree_trigger"
                              />
                            </div>
                          </li>
                        </ul>
                      </div>
                      <!-- //.depth4 -->
                    </li>
                    <li class="agree_subitem">
                      <div class="agree_item">
                        <Checkbox
                          variant="mark"
                          align="left"
                          class="agree_checkbox"
                        >
                          <template #label>
                            <span class="agree_label">
                              개인정보 수집 및 이용동의
                            </span>
                          </template>
                        </Checkbox>
                        <IconButton
                          iconName="Chevron_right"
                          size="small"
                          aria-label="개인정보 수집 및 이용동의 상세 보기"
                          class="agree_trigger"
                        />
                      </div>
                    </li>
                    <li class="agree_subitem">
                      <div class="agree_item">
                        <Checkbox
                          variant="mark"
                          align="left"
                          class="agree_checkbox"
                        >
                          <template #label>
                            <span class="agree_label">
                              위치기반 혜택 알림 수신동의
                            </span>
                          </template>
                        </Checkbox>
                        <IconButton
                          iconName="Chevron_right"
                          size="small"
                          aria-label="개인정보 수집 및 이용동의 상세 보기"
                          class="agree_trigger"
                        />
                      </div>
                    </li>
                    <li class="agree_subitem">
                      <div class="agree_item">
                        <Checkbox
                          variant="mark"
                          align="left"
                          class="agree_checkbox"
                        >
                          <template #label>
                            <span class="agree_label">
                              블루칩 씨앤에스 위치정보사업자약관동의
                            </span>
                          </template>
                        </Checkbox>
                        <IconButton
                          iconName="Chevron_right"
                          size="small"
                          aria-label="개인정보 수집 및 이용동의 상세 보기"
                          class="agree_trigger"
                        />
                      </div>
                    </li>
                  </ul>
                </div>
                <!-- //.depth3 -->
              </li>
              <li class="agree_subitem">
                <div class="agree_item">
                  <Checkbox variant="mark" align="left" class="agree_checkbox">
                    <template #label>
                      <span class="agree_label">
                        [선택] 앱(APP) 알림 수신동의
                      </span>
                    </template>
                  </Checkbox>
                  <IconButton
                    v-if="depth2HasChildren"
                    iconName="Chevron_down"
                    size="small"
                    class="agree_trigger"
                  />
                  <IconButton
                    v-else
                    iconName="Chevron_right"
                    size="small"
                    aria-label="[선택] 앱(APP) 알림 수신동의 상세 보기"
                    class="agree_trigger"
                  />
                </div>
                <!-- depth3 (class is-expand 추가/제거로 펼침/접힘) -->
                <div class="depth3">
                  <ul class="agree_sublist">
                    <li class="agree_subitem">
                      <div class="agree_item">
                        <Checkbox
                          variant="mark"
                          align="left"
                          class="agree_checkbox"
                        >
                          <template #label>
                            <span class="agree_label">
                              마케팅 정보 수신동의
                            </span>
                          </template>
                        </Checkbox>
                        <IconButton
                          v-if="depth3HasChildren"
                          iconName="Chevron_down"
                          size="small"
                          class="agree_trigger"
                        />
                        <IconButton
                          v-else
                          iconName="Chevron_right"
                          size="small"
                          aria-label="신한카드 위치기반 사업자 약관 동의 상세 보기"
                          class="agree_trigger"
                        />
                      </div>
                      <!-- depth4 (class is-expand 추가/제거로 펼침/접힘) -->
                      <div class="depth4">
                        <div class="agree_sublist box_type">
                          <UnorderedList :gap="8">
                            <UnorderedListItem size="small">
                              <span class="list_label">
                                항목: 앱(APP)을 통한 마케팅 정보 수신동의
                              </span>
                            </UnorderedListItem>
                            <UnorderedListItem size="small">
                              <span class="list_label">
                                이용목적: 각종 이벤트, 할인, 이용정보 등의 안내
                              </span>
                            </UnorderedListItem>
                            <UnorderedListItem size="small">
                              <span class="list_label">
                                보유기간: 별도 동의 철회시까지
                              </span>
                            </UnorderedListItem>
                          </UnorderedList>
                        </div>
                      </div>
                      <!-- //.depth4 -->
                    </li>
                  </ul>
                </div>
                <!-- //.depth3 -->
              </li>
            </ul>
          </div>
          <!-- //.depth2 -->
        </li>
        <!-- //.depth1 -->
        <li class="depth1">
          <div class="agree_item">
            <Checkbox variant="box" align="left" class="agree_checkbox">
              <template #label>
                <span class="agree_label">
                  [필수·선택] 신한Pay머니 이용약관
                </span>
              </template>
            </Checkbox>
            <IconButton
              v-if="depth1HasChildren"
              iconName="Chevron_down"
              size="small"
              class="agree_trigger"
            />
            <IconButton
              v-else
              iconName="Chevron_right"
              size="small"
              aria-label="[필수·선택] 서비스 이용약관 상세 보기"
              class="agree_trigger"
            />
          </div>
          <!-- depth2 (class is-expand 추가/제거로 펼침/접힘) -->
          <div class="depth2">
            <ul class="agree_sublist">
              <li class="agree_subitem">
                <div class="agree_item">
                  <Checkbox variant="mark" align="left" class="agree_checkbox">
                    <template #label>
                      <span class="agree_label">
                        신한Pay머니 이용약관 필수 동의
                      </span>
                    </template>
                  </Checkbox>
                  <IconButton
                    iconName="Chevron_right"
                    size="small"
                    aria-label="신한Pay머니 이용약관 필수 동의 상세 보기"
                    class="agree_trigger"
                  />
                </div>
              </li>
              <li class="agree_subitem">
                <div class="agree_item">
                  <Checkbox variant="mark" align="left" class="agree_checkbox">
                    <template #label>
                      <span class="agree_label">
                        개인정보 수집 및 이용 필수 동의
                      </span>
                    </template>
                  </Checkbox>
                  <IconButton
                    iconName="Chevron_right"
                    size="small"
                    aria-label="개인정보 수집 및 이용 필수 동의 상세 보기"
                    class="agree_trigger"
                  />
                </div>
              </li>
              <li class="agree_subitem">
                <div class="agree_item">
                  <Checkbox variant="mark" align="left" class="agree_checkbox">
                    <template #label>
                      <span class="agree_label">
                        고유식별정보처리 필수 동의
                      </span>
                    </template>
                  </Checkbox>
                  <IconButton
                    iconName="Chevron_right"
                    size="small"
                    aria-label="개인정보 수집 및 이용 필수 동의 상세 보기"
                    class="agree_trigger"
                  />
                </div>
              </li>
              <li class="agree_subitem">
                <!-- S: 동의등급제 안내 -->
                <div class="info_card">
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
                        <SolidLabel
                          color="cyan"
                          title="안심"
                        />
                        <SolidLabel
                          color="green"
                          title="다소안심"
                        />
                        <SolidLabel
                          color="yellow"
                          title="보통"
                        />
                        <SolidLabel
                          color="orange"
                          title="신중"
                        />
                        <SolidLabel
                          color="red"
                          title="주의"
                        />
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
                </div>
                <!-- E: 동의등급제 안내 -->
                <div class="agree_item">
                  <Checkbox variant="mark" align="left" class="agree_checkbox">
                    <template #label>
                      <span class="agree_label">
                        [선택] 카드 및 금융상품 ・ 서비스 안내 및 이용권유를 위한 수집 ・ 이용
                      </span>
                      <br />
                      <SolidLabel
                        color="green"
                        title="다소안심"
                        aria-label="동의등급제 다소안심"
                      />
                    </template>
                  </Checkbox>
                  <IconButton
                    iconName="Chevron_down"
                    size="small"
                    class="agree_trigger"
                  />
                </div>
                <!-- depth3 (class is-expand 추가/제거로 펼침/접힘) -->
                <div class="depth3">
                  <ul class="agree_sublist">
                    <li class="agree_subitem">
                      <div class="agree_item">
                        <Checkbox
                          variant="mark"
                          align="left"
                          class="agree_checkbox"
                        >
                          <template #label>
                            <span class="agree_label">
                              고유식별번호 조회 동의
                            </span>
                          </template>
                        </Checkbox>
                      </div>
                    </li>
                    <li class="agree_subitem">
                      <div class="agree_item">
                        <Checkbox
                          variant="mark"
                          align="left"
                          class="agree_checkbox"
                        >
                          <template #label>
                            <span class="agree_label">
                              개인신용정보 제공 동의
                            </span>
                          </template>
                        </Checkbox>
                      </div>
                    </li>
                  </ul>
                  <!-- 하단 우측 정렬 버튼 -->
                  <div class="agree_more">
                    <TextButton
                      class="agree_link"
                      color="secondary"
                      size="small"
                      text="자세히보기"
                      showGoTo
                    />
                  </div>
                </div>
                <!-- //.depth3 -->
              </li>
              <li class="agree_subitem">
                <div class="agree_item">
                  <Checkbox variant="mark" align="left" class="agree_checkbox">
                    <template #label>
                      <span class="agree_label">
                        [선택] 카드 및 금융상품 ・ 서비스 안내 및 이용권유를 위한 수집 ・ 이용
                      </span>
                      <br />
                      <SolidLabel
                        color="yellow"
                        title="보통"
                        aria-label="동의등급제 보통"
                      />
                    </template>
                  </Checkbox>
                  <IconButton
                    iconName="Chevron_down"
                    size="small"
                    class="agree_trigger"
                  />
                </div>
                <!-- depth3 (class is-expand 추가/제거로 펼침/접힘) -->
                <div class="depth3">
                  <ul class="agree_sublist">
                    <li class="agree_subitem">
                      <div class="agree_item">
                        <Checkbox
                          variant="mark"
                          align="left"
                          class="agree_checkbox"
                        >
                          <template #label>
                            <span class="agree_label">
                              고유식별번호 조회 동의
                            </span>
                          </template>
                        </Checkbox>
                      </div>
                    </li>
                    <li class="agree_subitem">
                      <div class="agree_item">
                        <Checkbox
                          variant="mark"
                          align="left"
                          class="agree_checkbox"
                        >
                          <template #label>
                            <span class="agree_label">
                              개인신용정보 제공 동의
                            </span>
                          </template>
                        </Checkbox>
                      </div>
                    </li>
                  </ul>
                  <!-- 하단 우측 정렬 버튼 -->
                  <div class="agree_more">
                    <TextButton
                      class="agree_link"
                      color="secondary"
                      size="small"
                      text="자세히보기"
                      showGoTo
                    />
                  </div>
                </div>
                <!-- //.depth3 -->
              </li>
              <li class="agree_subitem">
                <div class="agree_item">
                  <Checkbox variant="mark" align="left" class="agree_checkbox">
                    <template #label>
                      <span class="agree_label">
                        [선택] 전자적 전송매체를 통한 광고성 정보 수신동의
                      </span>
                    </template>
                  </Checkbox>
                  <IconButton
                    iconName="Chevron_down"
                    size="small"
                    class="agree_trigger"
                  />
                </div>
                <!-- depth3 (class is-expand 추가/제거로 펼침/접힘) -->
                <div class="depth3">
                  <div class="agree_card">
                    <ul class="agree_sublist box_type">
                      <li class="agree_subitem">
                        <div class="agree_item">
                          <Checkbox
                            variant="mark"
                            align="left"
                            class="agree_checkbox"
                          >
                            <template #label>
                              <span class="agree_label">
                                전체
                              </span>
                            </template>
                          </Checkbox>
                        </div>
                      </li>
                      <li class="agree_subitem">
                        <div class="agree_item">
                          <Checkbox
                            variant="mark"
                            align="left"
                            class="agree_checkbox"
                          >
                            <template #label>
                              <span class="agree_label">
                                서면
                              </span>
                            </template>
                          </Checkbox>
                        </div>
                      </li>
                      <li class="agree_subitem">
                        <div class="agree_item">
                          <Checkbox
                            variant="mark"
                            align="left"
                            class="agree_checkbox"
                          >
                            <template #label>
                              <span class="agree_label">
                                이메일
                              </span>
                            </template>
                          </Checkbox>
                        </div>
                      </li>
                      <li class="agree_subitem">
                        <div class="agree_item">
                          <Checkbox
                            variant="mark"
                            align="left"
                            class="agree_checkbox"
                          >
                            <template #label>
                              <span class="agree_label">
                                전화
                              </span>
                            </template>
                          </Checkbox>
                        </div>
                      </li>
                      <li class="agree_subitem">
                        <div class="agree_item">
                          <Checkbox
                            variant="mark"
                            align="left"
                            class="agree_checkbox"
                          >
                            <template #label>
                              <span class="agree_label">
                                휴대폰 메세지(카카오톡, 네이버 알림 등 모바일 메세지 포함)
                              </span>
                            </template>
                          </Checkbox>
                        </div>
                      </li>
                    </ul>
                    <!-- 정보성 리스트 -->
                    <UnorderedList class="agree_infolist" :gap="8">
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
                </div>
                <!-- //.depth3 -->
              </li>
              <li class="agree_subitem">
                <div class="agree_item">
                  <Checkbox variant="mark" align="left" class="agree_checkbox">
                    <template #label>
                      <span class="agree_label">
                        [선택] 카드 및 금융상품 ・ 서비스 안내 및 이용권유를 위한 수집 ・ 이용
                      </span>
                      <br />
                      <SolidLabel
                        color="cyan"
                        title="안심"
                        aria-label="동의등급제 안심"
                      />
                    </template>
                  </Checkbox>
                  <IconButton
                    iconName="Chevron_down"
                    size="small"
                    class="agree_trigger"
                  />
                </div>
                <!-- depth3 (class is-expand 추가/제거로 펼침/접힘) -->
                <div class="depth3">
                  <ul class="agree_sublist">
                    <li class="agree_subitem">
                      <div class="agree_item">
                        <Checkbox
                          variant="mark"
                          align="left"
                          class="agree_checkbox"
                        >
                          <template #label>
                            <span class="agree_label">
                              개인신용정보 제공 동의
                            </span>
                          </template>
                        </Checkbox>
                      </div>
                    </li>
                  </ul>
                  <!-- 하단 우측 정렬 버튼 -->
                  <div class="agree_more">
                    <TextButton
                      class="agree_link"
                      color="secondary"
                      size="small"
                      text="자세히보기"
                      showGoTo
                    />
                  </div>
                </div>
                <!-- //.depth3 -->
              </li>
              <li class="agree_subitem">
                <div class="agree_item">
                  <Checkbox variant="mark" align="left" class="agree_checkbox">
                    <template #label>
                      <span class="agree_label">
                        회원가입 및 발권신청 필수 동의
                      </span>
                    </template>
                  </Checkbox>
                  <IconButton
                    iconName="Chevron_right"
                    size="small"
                    aria-label="회원가입 및 발권신청 필수 동의 상세 보기"
                    class="agree_trigger"
                  />
                </div>
                <p class="agree_infotext">
                  본인은 카드 실제 소유자와 동일하며, 위 기재된 사실과 다름이 없음을 확인하고 회원가입을 신청합니다.
                </p>
              </li>
            </ul>
          </div>
          <!-- //.depth2 -->
        </li>
        <!-- //.depth1 -->
        <li class="depth1">
          <div class="agree_item">
            <Checkbox variant="box" align="left" class="agree_checkbox">
              <template #label>
                <span class="agree_label">
                  [선택] 온라인 회원 이용약관
                </span>
              </template>
            </Checkbox>
            <IconButton
              v-if="depth1HasChildren"
              iconName="Chevron_down"
              size="small"
              class="agree_trigger"
            />
            <IconButton
              v-else
              iconName="Chevron_right"
              size="small"
              aria-label="[필수·선택] 서비스 이용약관 상세 보기"
              class="agree_trigger"
            />
          </div>
          <!-- depth2 (class is-expand 추가/제거로 펼침/접힘) -->
          <div class="depth2">
            <ul class="agree_sublist">
              <li class="agree_subitem">
                <div class="agree_item">
                  <Checkbox variant="mark" align="left" class="agree_checkbox">
                    <template #label>
                      <span class="agree_label">
                        온라인 회원 이용약관 필수 동의
                      </span>
                    </template>
                  </Checkbox>
                  <IconButton
                    iconName="Chevron_right"
                    size="small"
                    aria-label="온라인 회원 이용약관 필수 동의 상세 보기"
                    class="agree_trigger"
                  />
                </div>
              </li>
              <li class="agree_subitem">
                <div class="agree_item">
                  <Checkbox variant="mark" align="left" class="agree_checkbox">
                    <template #label>
                      <span class="agree_label">
                        개인정보 수집·이용 필수 동의
                      </span>
                    </template>
                  </Checkbox>
                  <IconButton
                    iconName="Chevron_right"
                    size="small"
                    aria-label="개인정보 수집·이용 필수 동의 상세 보기"
                    class="agree_trigger"
                  />
                </div>
              </li>
            </ul>
          </div>
          <!-- //.depth2 -->
        </li>
        <!-- //.depth1 -->
        <li class="depth1">
          <div class="agree_item">
            <Checkbox variant="box" align="left" class="agree_checkbox">
              <template #label>
                <span class="agree_label">
                  [선택] 신한 슈퍼SOL 이용약관
                </span>
              </template>
            </Checkbox>
            <IconButton
              v-if="depth1HasChildren"
              iconName="Chevron_down"
              size="small"
              class="agree_trigger"
            />
            <IconButton
              v-else
              iconName="Chevron_right"
              size="small"
              aria-label="[필수·선택] 서비스 이용약관 상세 보기"
              class="agree_trigger"
            />
          </div>
          <!-- depth2 (class is-expand 추가/제거로 펼침/접힘) -->
          <div class="depth2">
            <!-- S: 동의등급제 안내 -->
            <div class="info_card">
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
                    <SolidLabel
                      color="cyan"
                      title="안심"
                    />
                    <SolidLabel
                      color="green"
                      title="다소안심"
                    />
                    <SolidLabel
                      color="yellow"
                      title="보통"
                    />
                    <SolidLabel
                      color="orange"
                      title="신중"
                    />
                    <SolidLabel
                      color="red"
                      title="주의"
                    />
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
            </div>
            <!-- E: 동의등급제 안내 -->
            
            <ul class="agree_sublist">
              <li class="agree_subitem">
                <div class="agree_item">
                  <Checkbox variant="mark" align="left" class="agree_checkbox">
                    <template #label>
                      <span class="agree_label">
                        신한 모바일 플랫폼 이용약관 필수 동의
                      </span>
                    </template>
                  </Checkbox>
                  <IconButton
                    iconName="Chevron_right"
                    size="small"
                    aria-label="신한 모바일 플랫폼 이용약관 필수 동의 상세 보기"
                    class="agree_trigger"
                  />
                </div>
              </li>
              <li class="agree_subitem">
                <div class="agree_item">
                  <Checkbox variant="mark" align="left" class="agree_checkbox">
                    <template #label>
                      <span class="agree_label">
                        신한금융그룹 통합 포인트 서비스 이용 필수 동의
                      </span>
                    </template>
                  </Checkbox>
                  <IconButton
                    iconName="Chevron_right"
                    size="small"
                    aria-label="신한금융그룹 통합 포인트 서비스 이용 필수 동의 상세 보기"
                    class="agree_trigger"
                  />
                </div>
              </li>
              <li class="agree_subitem">
                <div class="agree_item">
                  <Checkbox variant="mark" align="left" class="agree_checkbox">
                    <template #label>
                      <span class="agree_label">
                        개인(신용)정보 수집·이용·제공 필수 동의
                      </span>
                    </template>
                  </Checkbox>
                  <IconButton
                    iconName="Chevron_right"
                    size="small"
                    aria-label="개인(신용)정보 수집·이용·제공 필수 동의 상세 보기"
                    class="agree_trigger"
                  />
                </div>
              </li>
              <li class="agree_subitem">
                <div class="agree_item">
                  <Checkbox variant="mark" align="left" class="agree_checkbox">
                    <template #label>
                      <span class="agree_label">
                        개인(신용)정보 수집·이용·제공 필수 동의(포인트 서비스 제공)
                      </span>
                    </template>
                  </Checkbox>
                  <IconButton
                    iconName="Chevron_right"
                    size="small"
                    aria-label="개인(신용)정보 수집·이용·제공 필수 동의(포인트 서비스 제공) 상세 보기"
                    class="agree_trigger"
                  />
                </div>
              </li>
              <li class="agree_subitem">
                <div class="agree_item">
                  <Checkbox variant="mark" align="left" class="agree_checkbox">
                    <template #label>
                      <span class="agree_label">
                        전자금융서비스 이용 필수 동의(신한은행)
                      </span>
                    </template>
                  </Checkbox>
                  <IconButton
                    iconName="Chevron_down"
                    size="small"
                    class="agree_trigger"
                  />
                </div>
                <!-- depth3 (class is-expand 추가/제거로 펼침/접힘) -->
                <div class="depth3">
                  <div class="agree_card">
                    <ul class="agree_sublist box_type">
                      <li class="agree_subitem">
                        <div class="agree_item">
                          <span class="agree_label">
                            전자금융거래 기본약관
                          </span>
                          <IconButton
                            iconName="Chevron_right"
                            size="small"
                            aria-label="전자금융거래 기본약관 상세 보기"
                            class="agree_trigger"
                          />
                        </div>
                      </li>
                      <li class="agree_subitem">
                        <div class="agree_item">
                          <span class="agree_label">
                            신한온라인서비스 이용약관
                          </span>
                          <IconButton
                            iconName="Chevron_right"
                            size="small"
                            aria-label="신한온라인서비스 이용약관 상세 보기"
                            class="agree_trigger"
                          />
                        </div>
                      </li>
                      <li class="agree_subitem">
                        <div class="agree_item">
                          <span class="agree_label">
                            전자통지서비스 이용약관
                          </span>
                          <IconButton
                            iconName="Chevron_right"
                            size="small"
                            aria-label="전자통지서비스 이용약관 상세 보기"
                            class="agree_trigger"
                          />
                        </div>
                      </li>
                      <li class="agree_subitem">
                        <div class="agree_item">
                          <span class="agree_label">
                            개인정보 수집 이용 동의(비여신 금융거래)
                          </span>
                          <IconButton
                            iconName="Chevron_right"
                            size="small"
                            aria-label="개인정보 수집 이용 동의(비여신 금융거래) 상세 보기"
                            class="agree_trigger"
                          />
                        </div>
                      </li>
                    </ul>
                  </div>
                </div>
                <!-- //.depth3 -->
              </li>
              <li class="agree_subitem">
                <div class="agree_item">
                  <Checkbox variant="mark" align="left" class="agree_checkbox">
                    <template #label>
                      <span class="agree_label">
                        그룹 로열티 서비스 이용 필수 동의(신한은행)
                      </span>
                    </template>
                  </Checkbox>
                  <IconButton
                    iconName="Chevron_right"
                    size="small"
                    aria-label="그룹 로열티 서비스 이용 필수 동의(신한은행) 상세 보기"
                    class="agree_trigger"
                  />
                </div>
              </li>
              <li class="agree_subitem">
                <div class="agree_item">
                  <Checkbox variant="mark" align="left" class="agree_checkbox">
                    <template #label>
                      <span class="agree_label">
                        개인(신용)정보 수집·이용·제공 필수 동의(신한은행)
                      </span>
                    </template>
                  </Checkbox>
                  <IconButton
                    iconName="Chevron_right"
                    size="small"
                    aria-label="개인(신용)정보 수집·이용·제공 필수 동의(신한은행) 상세 보기"
                    class="agree_trigger"
                  />
                </div>
              </li>
              <li class="agree_subitem">
                <div class="agree_item">
                  <Checkbox variant="mark" align="left" class="agree_checkbox">
                    <template #label>
                      <span class="agree_label">
                        [선택] 개인(신용)정보 수집 ・ 이용 ・ 제공 동의(상품 서비스 안내 등)
                      </span>
                      <br />
                      <SolidLabel
                        color="cyan"
                        title="안심"
                      />
                    </template>
                  </Checkbox>
                  <IconButton
                    iconName="Chevron_right"
                    size="small"
                    aria-label="[선택] 개인(신용)정보 수집 ・ 이용 ・ 제공 동의(상품 서비스 안내 등) 상세 보기"
                    class="agree_trigger"
                  />
                </div>
              </li>
              <li class="agree_subitem">
                <div class="agree_item">
                  <Checkbox variant="mark" align="left" class="agree_checkbox">
                    <template #label>
                      <span class="agree_label">
                        [선택] 개인(신용)정보 수집 ・ 이용 ・ 제공 동의(상품 서비스 안내 등)(신한은행)
                      </span>
                      <br />
                      <SolidLabel
                        color="cyan"
                        title="안심"
                      />
                    </template>
                  </Checkbox>
                  <IconButton
                    iconName="Chevron_right"
                    size="small"
                    aria-label="[선택] 개인(신용)정보 수집 ・ 이용 ・ 제공 동의(상품 서비스 안내 등)(신한은행) 상세 보기"
                    class="agree_trigger"
                  />
                </div>
              </li>
              <li class="agree_subitem">
                <div class="agree_item">
                  <Checkbox variant="mark" align="left" class="agree_checkbox">
                    <template #label>
                      <span class="agree_label">
                        [선택] 광고성 전자적 수신매체 전송 동의
                      </span>
                    </template>
                  </Checkbox>
                  <IconButton
                    iconName="Chevron_down"
                    size="small"
                    class="agree_trigger"
                  />
                </div>
                <!-- depth3 (class is-expand 추가/제거로 펼침/접힘) -->
                <div class="depth3">
                  <div class="agree_card">
                    <ul class="agree_sublist box_type">
                      <li class="agree_subitem">
                        <div class="agree_item">
                          <Checkbox
                            variant="mark"
                            align="left"
                            class="agree_checkbox"
                          >
                            <template #label>
                              <span class="agree_label">
                                전체
                              </span>
                            </template>
                          </Checkbox>
                        </div>
                      </li>
                      <li class="agree_subitem">
                        <div class="agree_item">
                          <Checkbox
                            variant="mark"
                            align="left"
                            class="agree_checkbox"
                          >
                            <template #label>
                              <span class="agree_label">
                                이메일
                              </span>
                            </template>
                          </Checkbox>
                        </div>
                      </li>
                      <li class="agree_subitem">
                        <div class="agree_item">
                          <Checkbox
                            variant="mark"
                            align="left"
                            class="agree_checkbox"
                          >
                            <template #label>
                              <span class="agree_label">
                                전화
                              </span>
                            </template>
                          </Checkbox>
                        </div>
                      </li>
                    </ul>
                  </div>
                </div>
                <!-- //.depth3 -->
              </li>
            </ul>
          </div>
          <!-- //.depth2 -->
        </li>
        <!-- //.depth1 -->
        <li class="depth1">
          <div class="agree_item">
            <Checkbox variant="box" align="left" class="agree_checkbox">
              <template #label>
                <span class="agree_label">
                  [선택] 전자문서 서비스 이용약관
                </span>
              </template>
            </Checkbox>
            <IconButton
              v-if="depth1HasChildren"
              iconName="Chevron_down"
              size="small"
              class="agree_trigger"
            />
            <IconButton
              v-else
              iconName="Chevron_right"
              size="small"
              aria-label="[필수·선택] 서비스 이용약관 상세 보기"
              class="agree_trigger"
            />
          </div>
          <!-- depth2 (class is-expand 추가/제거로 펼침/접힘) -->
          <div class="depth2">
            <ul class="agree_sublist">
              <li class="agree_subitem">
                <div class="agree_item">
                  <Checkbox variant="mark" align="left" class="agree_checkbox">
                    <template #label>
                      <span class="agree_label">
                        전자문서 서비스 이용약관 필수 동의
                      </span>
                    </template>
                  </Checkbox>
                  <IconButton
                    iconName="Chevron_right"
                    size="small"
                    aria-label="전자문서 서비스 이용약관 필수 동의 상세 보기"
                    class="agree_trigger"
                  />
                </div>
              </li>
              <li class="agree_subitem">
                <div class="agree_item">
                  <Checkbox variant="mark" align="left" class="agree_checkbox">
                    <template #label>
                      <span class="agree_label">
                        전자문서 개인정보 수집·이용 필수 동의
                      </span>
                    </template>
                  </Checkbox>
                  <IconButton
                    iconName="Chevron_right"
                    size="small"
                    aria-label="전자문서 개인정보 수집·이용 필수 동의 상세 보기"
                    class="agree_trigger"
                  />
                </div>
              </li>
              <li class="agree_subitem">
                <div class="agree_item">
                  <Checkbox variant="mark" align="left" class="agree_checkbox">
                    <template #label>
                      <span class="agree_label">
                        개인정보 제3자 제공 필수 동의
                      </span>
                    </template>
                  </Checkbox>
                  <IconButton
                    iconName="Chevron_right"
                    size="small"
                    aria-label="개인정보 제3자 제공 필수 동의 상세 보기"
                    class="agree_trigger"
                  />
                </div>
              </li>
              <li class="agree_subitem">
                <div class="agree_item">
                  <Checkbox variant="mark" align="left" class="agree_checkbox">
                    <template #label>
                      <span class="agree_label">
                        서비스 유의사항 필수 동의
                      </span>
                    </template>
                  </Checkbox>
                  <IconButton
                    iconName="Chevron_right"
                    size="small"
                    aria-label="서비스 유의사항 필수 동의 상세 보기"
                    class="agree_trigger"
                  />
                </div>
              </li>
            </ul>
          </div>
          <!-- //.depth2 -->
        </li>
        <!-- //.depth1 -->
        <li class="depth1">
          <div class="agree_item">
            <Checkbox variant="box" align="left" class="agree_checkbox">
              <template #label>
                <span class="agree_label">
                  [선택] 마이데이터 서비스 이용약관
                </span>
              </template>
            </Checkbox>
            <IconButton
              v-if="depth1HasChildren"
              iconName="Chevron_down"
              size="small"
              class="agree_trigger"
            />
            <IconButton
              v-else
              iconName="Chevron_right"
              size="small"
              aria-label="[필수·선택] 서비스 이용약관 상세 보기"
              class="agree_trigger"
            />
          </div>
          <!-- depth2 (class is-expand 추가/제거로 펼침/접힘) -->
          <div class="depth2">
            <ul class="agree_sublist">
              <li class="agree_subitem">
                <div class="agree_item">
                  <Checkbox variant="mark" align="left" class="agree_checkbox">
                    <template #label>
                      <span class="agree_label">
                        마이데이터 서비스 이용약관 필수 동의
                      </span>
                    </template>
                  </Checkbox>
                  <IconButton
                    iconName="Chevron_right"
                    size="small"
                    aria-label="마이데이터 서비스 이용약관 필수 동의 상세 보기"
                    class="agree_trigger"
                  />
                </div>
              </li>
              <li class="agree_subitem">
                <div class="agree_item">
                  <Checkbox variant="mark" align="left" class="agree_checkbox">
                    <template #label>
                      <span class="agree_label">
                        마이데이터 서비스 개인(신용)정보의 수집 및 이용 필수 동의
                      </span>
                    </template>
                  </Checkbox>
                  <IconButton
                    iconName="Chevron_right"
                    size="small"
                    aria-label="마이데이터 서비스 개인(신용)정보의 수집 및 이용 필수 동의 상세 보기"
                    class="agree_trigger"
                  />
                </div>
              </li>
            </ul>
            <!-- 하단 우측 정렬 버튼 -->
            <div class="agree_more">
              <TextButton
                class="agree_link"
                color="secondary"
                size="small"
                text="개인정보 처리방침"
                showGoTo
              />
            </div>
          </div>
          <!-- //.depth2 -->
        </li>
        <!-- //.depth1 -->
        <li class="depth1">
          <div class="agree_item">
            <Checkbox variant="box" align="left" class="agree_checkbox">
              <template #label>
                <span class="agree_label">
                  [선택] 마케팅 동의 이용약관
                </span>
              </template>
            </Checkbox>
            <IconButton
              v-if="depth1HasChildren"
              iconName="Chevron_down"
              size="small"
              class="agree_trigger"
            />
            <IconButton
              v-else
              iconName="Chevron_right"
              size="small"
              aria-label="[선택] 마케팅 동의 이용약관 상세 보기"
              class="agree_trigger"
            />
          </div>
          <!-- depth2 (class is-expand 추가/제거로 펼침/접힘) -->
          <div class="depth2">
            <ul class="agree_sublist">
              <li class="agree_subitem">
                <div class="agree_item">
                  <Checkbox variant="mark" align="left" class="agree_checkbox">
                    <template #label>
                      <span class="agree_label">
                        [선택] 카드 및 금융상품 ・ 서비스 안내 및 이용권유를 위한 수집 ・ 이용
                      </span>
                      <br />
                      <SolidLabel
                        color="green"
                        title="다소안심"
                        aria-label="동의등급제 다소안심"
                      />
                    </template>
                  </Checkbox>
                  <IconButton
                    iconName="Chevron_down"
                    size="small"
                    class="agree_trigger"
                  />
                </div>
                <!-- depth3 (class is-expand 추가/제거로 펼침/접힘) -->
                <div class="depth3">
                  <ul class="agree_sublist">
                    <li class="agree_subitem">
                      <div class="agree_item">
                        <Checkbox
                          variant="mark"
                          align="left"
                          class="agree_checkbox"
                        >
                          <template #label>
                            <span class="agree_label">
                              고유식별번호 조회 동의
                            </span>
                          </template>
                        </Checkbox>
                      </div>
                    </li>
                    <li class="agree_subitem">
                      <div class="agree_item">
                        <Checkbox
                          variant="mark"
                          align="left"
                          class="agree_checkbox"
                        >
                          <template #label>
                            <span class="agree_label">
                              개인신용정보 제공 동의
                            </span>
                          </template>
                        </Checkbox>
                      </div>
                    </li>
                  </ul>
                  <!-- 하단 우측 정렬 버튼 -->
                  <div class="agree_more">
                    <TextButton
                      class="agree_link"
                      color="secondary"
                      size="small"
                      text="자세히보기"
                      showGoTo
                    />
                  </div>
                </div>
                <!-- //.depth3 -->
              </li>
              <li class="agree_subitem">
                <div class="agree_item">
                  <Checkbox variant="mark" align="left" class="agree_checkbox">
                    <template #label>
                      <span class="agree_label">
                        [선택] 카드 및 금융상품 ・ 서비스 이외의 부수서비스 안내 등을 위한 수집 ・ 이용
                      </span>
                      <br />
                      <SolidLabel
                        color="yellow"
                        title="보통"
                        aria-label="동의등급제 보통"
                      />
                    </template>
                  </Checkbox>
                  <IconButton
                    iconName="Chevron_down"
                    size="small"
                    class="agree_trigger"
                  />
                </div>
                <!-- depth3 (class is-expand 추가/제거로 펼침/접힘) -->
                <div class="depth3">
                  <ul class="agree_sublist">
                    <li class="agree_subitem">
                      <div class="agree_item">
                        <Checkbox
                          variant="mark"
                          align="left"
                          class="agree_checkbox"
                        >
                          <template #label>
                            <span class="agree_label">
                              고유식별번호 조회 동의
                            </span>
                          </template>
                        </Checkbox>
                      </div>
                    </li>
                    <li class="agree_subitem">
                      <div class="agree_item">
                        <Checkbox
                          variant="mark"
                          align="left"
                          class="agree_checkbox"
                        >
                          <template #label>
                            <span class="agree_label">
                              개인신용정보 제공 동의
                            </span>
                          </template>
                        </Checkbox>
                      </div>
                    </li>
                  </ul>
                  <!-- 하단 우측 정렬 버튼 -->
                  <div class="agree_more">
                    <TextButton
                      class="agree_link"
                      color="secondary"
                      size="small"
                      text="자세히보기"
                      showGoTo
                    />
                  </div>
                </div>
                <!-- //.depth3 -->
              </li>
              <li class="agree_subitem">
                <div class="agree_item">
                  <Checkbox variant="mark" align="left" class="agree_checkbox">
                    <template #label>
                      <span class="agree_label">
                        [선택] 전자적 전송매체를 통한 광고성 정보 수신동의
                      </span>
                    </template>
                  </Checkbox>
                  <IconButton
                    iconName="Chevron_down"
                    size="small"
                    class="agree_trigger"
                  />
                </div>
                <!-- depth3 (class is-expand 추가/제거로 펼침/접힘) -->
                <div class="depth3">
                  <div class="agree_card">
                    <ul class="agree_sublist box_type">
                      <li class="agree_subitem">
                        <div class="agree_item">
                          <Checkbox
                            variant="mark"
                            align="left"
                            class="agree_checkbox"
                          >
                            <template #label>
                              <span class="agree_label">
                                전체
                              </span>
                            </template>
                          </Checkbox>
                        </div>
                      </li>
                      <li class="agree_subitem">
                        <div class="agree_item">
                          <Checkbox
                            variant="mark"
                            align="left"
                            class="agree_checkbox"
                          >
                            <template #label>
                              <span class="agree_label">
                                서면
                              </span>
                            </template>
                          </Checkbox>
                        </div>
                      </li>
                      <li class="agree_subitem">
                        <div class="agree_item">
                          <Checkbox
                            variant="mark"
                            align="left"
                            class="agree_checkbox"
                          >
                            <template #label>
                              <span class="agree_label">
                                이메일
                              </span>
                            </template>
                          </Checkbox>
                        </div>
                      </li>
                      <li class="agree_subitem">
                        <div class="agree_item">
                          <Checkbox
                            variant="mark"
                            align="left"
                            class="agree_checkbox"
                          >
                            <template #label>
                              <span class="agree_label">
                                전화
                              </span>
                            </template>
                          </Checkbox>
                        </div>
                      </li>
                      <li class="agree_subitem">
                        <div class="agree_item">
                          <Checkbox
                            variant="mark"
                            align="left"
                            class="agree_checkbox"
                          >
                            <template #label>
                              <span class="agree_label">
                                휴대폰 메세지(카카오톡, 네이버 알림 등 모바일 메세지 포함)
                              </span>
                            </template>
                          </Checkbox>
                        </div>
                      </li>
                    </ul>
                    <!-- 정보성 리스트 -->
                    <UnorderedList class="agree_infolist" :gap="8">
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
                </div>
                <!-- //.depth3 -->
              </li>
              <li class="agree_subitem">
                <div class="agree_item">
                  <Checkbox variant="mark" align="left" class="agree_checkbox">
                    <template #label>
                      <span class="agree_label">
                        [선택] 신한금융 자회사 및 손자회사에 개인(신용)정보를 제공
                      </span>
                      <br />
                      <SolidLabel
                        color="cyan"
                        title="안심"
                        aria-label="동의등급제 안심"
                      />
                    </template>
                  </Checkbox>
                  <IconButton
                    iconName="Chevron_down"
                    size="small"
                    class="agree_trigger"
                  />
                </div>
                <!-- depth3 (class is-expand 추가/제거로 펼침/접힘) -->
                <div class="depth3">
                  <ul class="agree_sublist">
                    <li class="agree_subitem">
                      <div class="agree_item">
                        <Checkbox
                          variant="mark"
                          align="left"
                          class="agree_checkbox"
                        >
                          <template #label>
                            <span class="agree_label">
                              개인신용정보 제공 동의
                            </span>
                          </template>
                        </Checkbox>
                      </div>
                    </li>
                  </ul>
                  <!-- 하단 우측 정렬 버튼 -->
                  <div class="agree_more">
                    <TextButton
                      class="agree_link"
                      color="secondary"
                      size="small"
                      text="자세히보기"
                      showGoTo
                    />
                  </div>
                </div>
                <!-- //.depth3 -->
              </li>
            </ul>
          </div>
          <!-- //.depth2 -->
        </li>
        <!-- //.depth1 -->
      </ul>
    </div>
    <!-- //.agree_wrap -->
  </div>
  <!-- //.sc-contents__body -->

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
          size="xsmall"
          text="종합포털 바로가기"
          showGoTo
        />
      </div>
    </div>
  </div>

  <BottomActionContainer :scrollDim="true">
    <BoxButtonGroup size="xlarge" variant="100">
      <BoxButton text="확인" :disabled="!agreeAll" />
    </BoxButtonGroup>
  </BottomActionContainer>
</template>

<script setup>
import {
  BottomActionContainer,
  BoxButton,
  BoxButtonGroup,
  Checkbox,
  Divider,
  IconButton,
  TextButton,
  UnorderedList,
  UnorderedListItem,
  Card,
  SolidLabel,
} from "@shc-nss/ui/solid";
import { onMounted, ref } from "vue";

/* 
  스크립트 부분은 개발시 수정하여 사용 
  현재 UI 확인하기 위한 용도로 작업됨.
*/
/** 전체 약관 모두 동의 (agree_allcheck, 확인 버튼 활성화용) */
const agreeAll = ref(false);

/** 하위 뎁스 존재 여부 (하위 있으면 펼침/접힘 버튼 1개, 없으면 상세 보기 버튼 1개) */
const depth1HasChildren = true;
const depth2HasChildren = true;
const depth3HasChildren = true;

/** 약관 리스트 컨테이너 (depth1 개수 파악용) */
const agreeListRef = ref(null);

/** 펼침/접힘: DOM 기반 (구조 변경 시 마크업 수정 불필요, 클릭 위임 + class/aria 제어) */
function onAgreeListClick(e) {
  const trigger = e.target.closest?.(".agree_trigger");
  if (!trigger) return;
  const agreeItem = trigger.closest(".agree_item");
  const panel = agreeItem?.nextElementSibling;
  if (!panel || !panel.matches(".depth2, .depth3, .depth4")) return;
  const isExpanded = panel.classList.toggle("is-expand");
  panel.setAttribute("aria-hidden", !isExpanded);
  trigger.setAttribute("aria-expanded", isExpanded);
}

onMounted(() => {
  const wrap = agreeListRef.value?.closest(".agree_wrap");
  if (!wrap) return;
  wrap.querySelectorAll(".depth2, .depth3, .depth4").forEach((el) => {
    el.classList.remove("is-expand");
    el.setAttribute("aria-hidden", "true");
  });
  wrap.querySelectorAll(".agree_trigger").forEach((trigger) => {
    const panel = trigger.closest(".agree_item")?.nextElementSibling;
    if (panel?.matches(".depth2, .depth3, .depth4")) {
      trigger.setAttribute("aria-expanded", "false");
    }
  });
});
</script>








<template>
  <div class="sc-contents__body">
    <section class="section">
      <RadioCircleGroup 
        v-model="termsAgree"
        :items="['동의함', '동의 안함']" 
        orientation="horizontal" 
        class="terms-radio__group"
      />
    </section>
    <section class="section">
      <div class="tterms-content" style="height:500px;background-color: var(--gray-50)">
      <!-- 약관 내용, 개발 시 style="background-color는 제거" -->
      </div>
    </section>
  </div>
</template>

<script setup>
import { 
  RadioCircleGroup 
} from "@shc-nss/ui/solid";
import { ref } from "vue";

const termsAgree = ref("동의함");
const termsAgree = ref(undefined);


<route lang="yaml">
meta:
  id: SCD001A02_bs1
  title: "카드"
  menu: 카드 > 약관 동의(BS)
  layout: EmptyLayout
  category: 카드
  publish: 김대민
  publishVersion: 0.8
  status: 작업완료
  etc: | 
    260128: 약관 동의 Bottomsheet 추가(맞춤 카드를 추천받으려면 동의가 필요해요) 
</route>
<template>
  <BottomSheet
    disableMinHeight
    variant="none"
    :closableDimm="true"
    :closableDrag="false"
    dimmed
    title="맞춤 카드를 추천받으려면 동의가 필요해요"
    v-model="isOpen"
    class="bs-card-agree"
  >
    <div class="bs-card-agree__contents">
      <div class="agree-contents__header">
        <img
          :src="$cdnURL + '/images/pages/pay/img_card_double.png'"
          alt=""
          class="img_card_double"
          aria-hidden="true"
        />
      </div>
      <div class="agree-contents__body">
        <div class="sc-agree__list agree-outline">
          <div class="agree-list__group">
            <div class="agree-outline__list">
              <SolidListAccordion
                v-for="item in outlineItems"
                :key="item.value"
                :class="[
                  'outline-accordion',
                  { 'is-checked': outlineChecked.includes(item.value) },
                ]"
                :rowClickable="false"
                :value="item.value"
                :prevent-hash="true"
                v-model:isExpanded="isAccordionExpanded"
              >
                <template #title>
                  <div class="outline-item check-variant-top">
                    <div class="outline-item__body">
                      <Checkbox
                        :value="item.value"
                        variant="box"
                        align="left"
                        :model-value="outlineChecked.includes(item.value)"
                        class="outline-checkbox"
                        @update:model-value="
                          onToggleoutline(item.value, $event)
                        "
                      >
                        <template #label>
                          <div class="outline-label">
                            <span class="outline-label__main">{{
                              item.label
                            }}</span>
                            <span
                              v-if="item.subText"
                              class="outline-label__subtext"
                              >{{ item.subText }}</span
                            >
                          </div>
                        </template>
                      </Checkbox>
                      <div v-if="item.meta" class="outline-label__meta">
                        <span>{{ item.meta }}</span>
                        <Tooltip
                          placement="top-center"
                          :showClose="true"
                          :closeOnClickOutside="true"
                        >
                          <template #content>
                            <div
                              class="sc-tooltip__content agree-grade-tooltip"
                            >
                              <div class="label-group">
                                <SolidLabel color="cyan" title="안심" />
                                <SolidLabel color="green" title="다소안심" />
                                <SolidLabel color="yellow" title="보통" />
                                <SolidLabel color="orange" title="신중" />
                                <SolidLabel color="red" title="주의" />
                              </div>
                              <p class="agree-grade-tooltip__desc">
                                동의등급제는 개인(신용)정보에 관한 선택적 동의
                                항목에 대해 사생활의 비밀과 자유를 침해할 위험,
                                이익이나 혜택, 동의 내용의 명확성 등을 고려한 뒤
                                5가지 등급을 부여하는 제도예요.
                              </p>
                            </div>
                          </template>
                        </Tooltip>
                      </div>
                    </div>
                  </div>
                </template>
                <div class="outline-panel">
                  <div class="outline-depth2__item">
                    <div class="outline-depth2__item-header">
                      <p class="outline-depth2__item-label">
                        카드 및 금융상품·서비스 안내 및 이용권유를 위한
                        수집·이용
                      </p>
                      <SolidLabel
                        class="outline-depth2__item-grade"
                        color="green"
                        title="다소안심"
                      />
                    </div>
                    <div class="outline-depth2__item-body">
                      <ul class="outline-depth2__item-list">
                        <li class="outline-depth2__list-item">
                          <Checkbox
                            value="agree-outline-2-1"
                            variant="mark"
                            align="left"
                            :model-value="
                              outlineChecked.includes('agree-outline-2-1')
                            "
                            class="outline-depth2__item-checkbox"
                            @update:model-value="
                              onToggleoutline('agree-outline-2-1', $event)
                            "
                          >
                            <template #label>
                              <span>고유식별번호 조회 동의</span>
                            </template>
                          </Checkbox>
                        </li>
                        <li class="outline-depth2__list-item">
                          <Checkbox
                            value="agree-outline-2-2"
                            variant="mark"
                            align="left"
                            :model-value="
                              outlineChecked.includes('agree-outline-2-2')
                            "
                            class="outline-depth2__item-checkbox"
                            @update:model-value="
                              onToggleoutline('agree-outline-2-2', $event)
                            "
                          >
                            <template #label>
                              <span>개인신용정보 제공 동의</span>
                            </template>
                          </Checkbox>
                        </li>
                      </ul>
                      <div class="agree-depth__link">
                        <TextButton
                          class="agree-depth__link-button"
                          color="secondary"
                          size="small"
                          text="자세히 보기"
                          showGoTo
                        />
                      </div>
                    </div>
                  </div>
                </div>
              </SolidListAccordion>
            </div>
          </div>
        </div>
      </div>
      <div class="agree-contents__footer">
        <div class="sc-bottom-info__card">
          <p class="sc-bottom-info__inner-title">꼭! 알아두세요</p>
          <div class="sc-bottom-info__details">
            <UnorderedList :gap="8">
              <UnorderedListItem
                variant="bullet"
                size="small"
                data-color="quaternary"
                text="동의를 해제하면 맞춤 카드 관련 안내를 받아볼 수 없어요."
              />
              <UnorderedListItem
                variant="bullet"
                size="small"
                data-color="quaternary"
                text="개인(신용)정보의 보유 및 이용기간은 계약 종료 시까지에요."
              />
              <UnorderedListItem
                variant="bullet"
                size="small"
                data-color="quaternary"
                text="카드상품과 부수서비스의 안내 및 이용권유에 동의했더라도 신용정보의 이용 및 보호에 관한 법률에 따라 언제든 관련한 연락 중단을 요청할 수 있어요. 요청은 신한카드 고객센터(1544-7000) 또는 홈페이지(www.shinhancard.com)에서 해주세요."
              />
            </UnorderedList>
          </div>
        </div>
      </div>
    </div>
    <!-- 하단 확인 버튼 -->
    <template #footer>
      <BottomActionContainer :scrollDim="true">
        <BoxButtonGroup size="xlarge" variant="35:65">
          <BoxButton text="다음에" color="secondary" />
          <BoxButton text="확인" :disabled="!isConfirmEnabled" />
        </BoxButtonGroup>
      </BottomActionContainer>
    </template>
  </BottomSheet>
</template>

<script setup>
import {
  BottomActionContainer,
  BottomSheet,
  BoxButton,
  BoxButtonGroup,
  Checkbox,
  SolidListAccordion,
  SolidLabel,
  TextButton,
  Tooltip,
  UnorderedList,
  UnorderedListItem,
} from "@shc-nss/ui/solid";
import { computed, ref } from "vue";

const isOpen = defineModel({ default: true });
const isAccordionExpanded = ref(true);

const outlineItems = [
  {
    label: "[선택] 개인(신용)정보 수집·이용 동의",
    value: "agree-outline-2",
    meta: "동의등급제 안내",
  },
];

const outlineChecked = ref([]);

const outlineChildMap = {
  "agree-outline-2": ["agree-outline-2-1", "agree-outline-2-2"],
};

const isConfirmEnabled = computed(() => outlineChecked.value.length > 0);

function onToggleoutline(value, checked) {
  const set = new Set(outlineChecked.value);
  if (checked) set.add(value);
  else set.delete(value);

  const parentValue = Object.keys(outlineChildMap).find((key) =>
    outlineChildMap[key].includes(value),
  );
  if (parentValue) {
    const childValues = outlineChildMap[parentValue];
    const hasCheckedChild = childValues.some((child) => set.has(child));
    if (hasCheckedChild) set.add(parentValue);
    else set.delete(parentValue);
  }
  outlineChecked.value = Array.from(set);
}
</script>



<route lang="yaml">
meta:
  id: SPY240A01
  title: ""
  menu: "페이 > 해외NFC결제 > 약관동의"
  layout: SubLayout
  category: 페이
  publish: 김대민
  publishVersion: 0.8
  status: 작업완료
  header:
    fixed: true
    close: true
</route>
<template>
  <BottomSheet
    title="해외 NFC 결제를 이용하려면 약관에 동의해주세요"
    v-model="isOpen"
  >
    <div class="sc-agree__list compound bg-gray" role="region">
      <div class="agree-list__group">
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
                          </SolidListAccordion>
                        </template>

                        <!-- 일반 항목 -->
                        <div v-else class="agree-item agree-item__sub">
                          <Checkbox
                            :value="depth2Item.value"
                            variant="mark"
                            align="left"
                            :model-value="subAgrees4.includes(depth2Item.value)"
                            class="agree-item__checkbox item-checkbox__sub"
                            @update:model-value="
                              onToggleSub4(depth2Item.value, $event)
                            "
                            @click.stop
                          >
                            <template #label>
                              <span class="agree-item__label item-label__sub">{{
                                depth2Item.label
                              }}</span>
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
                </div>
              </SolidListAccordion>
            </template>
          </div>
        </div>
      </div>
    </div>

    <template #footer>
      <BottomActionContainer :scrollDim="true">
        <BoxButtonGroup size="xlarge" variant="100">
          <BoxButton text="확인" :disabled="subAgrees4.length === 0" />
        </BoxButtonGroup>
      </BottomActionContainer>
    </template>
  </BottomSheet>
</template>

<script setup>
import {
  BottomActionContainer,
  BoxButton,
  BottomSheet,
  BoxButtonGroup,
  Checkbox,
  IconButton,
  SolidListAccordion,
} from "@shc-nss/ui/solid";
import { reactive, ref } from "vue";

const isOpen = defineModel({ default: true });

const subItems4 = [
  {
    label: "필수 약관 모두 동의",
    value: "s4-1",
    accordion: true,
  },
];

// 2뎁스 항목들 - 서비스 이용약관 (s4-1)
const subItemsDepth2_s4_1 = [
  { label: "개인정보 제3자 제공동의", value: "s4-1-1" },
  { label: "개인정보 국외 이전 동의", value: "s4-1-2" },
];

const subAgrees4 = ref([]);
const subAccordionState4 = reactive({
  "s4-1": true, // 서비스 이용약관 2뎁스 아코디언 상태
});

/**
 * 동작 로직
 */
function onToggleSub4(value, checked) {
  const set = new Set(subAgrees4.value);
  const parentValue = "s4-1";
  const childValues = subItemsDepth2_s4_1.map((item) => item.value);

  if (value === parentValue) {
    if (checked) {
      set.add(parentValue);
      childValues.forEach((child) => set.add(child));
    } else {
      set.delete(parentValue);
      childValues.forEach((child) => set.delete(child));
    }
  } else {
    if (checked) set.add(value);
    else set.delete(value);

    const allChildrenChecked = childValues.every((child) => set.has(child));
    if (allChildrenChecked) set.add(parentValue);
    else set.delete(parentValue);
  }

  subAgrees4.value = Array.from(set);
}
</script>





// sat164a04
<route lang="yaml">
meta:
  id: SAT166A04
  title: 한국투자증권 금융광고 동의 철회
  menu: "자산 > 금융추천: 투자 > 한투 금융 상품 투자 상세페이지 > 약관 동의 철회"
  layout: SubLayout
  category: 자산
  publish: 김대민
  publishVersion: 0.9
  status: 작업완료
  etc: |
    [v0.9 페이지 추가] 260203: 약관 동의 철회 페이지 추가,
  header:
    fixed: true
    back: true
    close: true
</route>
<template>
  <ScTitle
    description="동의를 해지하면 신한 SOL페이에서 한국투자증권 금융상품을 볼 수 없어요."
  />
  <div class="sc-contents__body sc-agree__page">
    <div class="sc-agree__list compound" role="region">
      <div class="agree-list__group">
        <div class="agree-sublist" role="group">
          <div
            v-for="item in agreementItems"
            :key="item.value"
            class="agree-subitem"
          >
            <div class="agree-item agree-item__sub">
              <span class="agree-item__label item-label__sub flex-auto">
                {{ item.label }}
              </span>
              <IconButton
                size="small"
                icon-name="Chevron_right"
                :aria-label="`${item.label} 상세보기`"
              />
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
  <div class="sc-contents__footer">
    <section class="section">
      <BasicCard color="gray" variant="solid">
        <div class="agree-item item-basic" :class="{ 'is-checked': isChecked }">
          <Checkbox
            v-model="isChecked"
            class="agree-item__checkbox item-checkbox__basic"
            variant="box"
            align="left"
          >
            <template #label>
              <span class="agree-item__label item-label__basic">
                위 내용을 확인했으며 한국투자증권 금융상품 광고 동의를
                해지하겠습니다.
              </span>
            </template>
          </Checkbox>
        </div>
      </BasicCard>
    </section>
  </div>
  <BottomActionContainer :scrollDim="true">
    <BoxButton
      text="동의 해지하기"
      size="xlarge"
      color="primary"
      :disabled="!isChecked"
    />
  </BottomActionContainer>
</template>

<script setup>
import { ScTitle } from "@shc-nss/ui/shc";
import {
  BasicCard,
  BottomActionContainer,
  BoxButton,
  Checkbox,
  IconButton,
} from "@shc-nss/ui/solid";
import { ref } from "vue";

const isChecked = ref(false);

const agreementItems = [
  {
    value: "consent-collect",
    label:
      "[필수] 한국투자증권 금융상품 광고 제휴서비스 개인(신용)정보 수집 및 이용 동의",
  },
  {
    value: "consent-provide",
    label: "[필수] 한국투자증권 금융상품 광고 제휴서비스 제3자 제공동의",
  },
];
</script>



// 추가 bottomsheet case
.bs-card-agree.sv-bottom-sheet {
  max-height: 90vh;
  @supports (max-height: min(1px, 2px)) {
    max-height: min(591px, 90vh);
  }
  &.sv-bottom-sheet--variant-none {
    .sv-bottom-sheet__header-inner {
      padding-right: var(--spacing-2xl);
    }
  }
  .sv-bottom-sheet__body {
    padding-bottom: 0;
  }
  .sc-agree__list.agree-outline {
    .outline-label__main {
      @include font-set("title-s");
      font-weight: 500;
    }
    .outline-accordion {
      border-width: 1px;
      padding: calc(var(--spacing-md) - 1px) 0 calc(var(--spacing-lg) - 1px);
      .sv-accordion-item__header {
        padding: var(--spacing-lg) calc(var(--spacing-2xl) - 2px);
      }
      .sv-accordion-item__title {
        min-height: 46px;
      }
    }
    .outline-panel {
      padding: 0;
      padding-left: 30px;
      @include font-set("body-m");
      font-weight: 300;
      color: var(--text-secondary);
    }
    .outline-depth2__item {
      padding: var(--spacing-md) 0 var(--spacing-lg);
    }
    .outline-depth2__item-header {
      display: flex;
      flex-direction: column;
      gap: var(--spacing-xs);
    }
    .outline-depth2__item-label {
      @include font-set("body-m");
      font-weight: 300;
      color: var(--text-primary);
    }
    .outline-depth2__item-grade {
      align-self: flex-start;
    }
    .outline-depth2__item-list {
      display: flex;
      flex-direction: column;
      margin-top: var(--spacing-lg);
    }
    .outline-depth2__list-item {
      display: flex;
      align-items: center;
      gap: var(--spacing-xs);
      color: var(--text-secondary);

      ~ .outline-depth2__list-item {
        margin-top: var(--spacing-md);
      }

      .sv-icon {
        color: var(--icon-secondary);
      }
      .sv-checkbox__label {
        @include font-set("body-s");
        font-weight: 300;
        color: var(--text-tertiary);
      }
      .sv-checkbox {
        flex: 1;
      }
    }
    .agree-depth__link {
      display: flex;
      flex: 1;
      justify-content: flex-end;
      margin-top: var(--spacing-md);
      .sv-button__label {
        @include font-set("body-s");
        font-weight: 500;
        color: var(--text-secondary);
      }
      .sv-button__right-icon {
        color: var(--fg-secondary);
      }
      .agree-depth__link-button {
      }
    }
  }
  .sv-accordion-item--variant-solid
    .sv-accordion-panel
    .sv-accordion-panel__content {
    padding: 0 calc(var(--spacing-2xl) - 2px);
  }
  .img_card_double {
    display: block;
    max-width: 140px;
    margin: 0 auto;
  }
  .outline-label__meta {
    padding-left: var(--spacing-4xl);
  }
  .sc-tooltip__content.agree-grade-tooltip {
    gap: var(--spacing-md);
  }
  .sv-tooltip-base {
    max-width: 264px;
  }
  .agree-grade-tooltip__desc {
    padding-bottom: 10px;
    font-weight: 300;
    color: var(--text-tertiary);
  }
  .sc-bottom-info__card {
    margin-right: 0;
    margin-left: 0;
    padding: var(--spacing-xl);
    .sc-bottom-info__details {
      margin-bottom: 0;
    }
    .sc-bottom-info__inner-title {
      @include font-set("body-s", 300);
      font-weight: 300;
      color: var(--text-secondary);
    }
    .sv-text-list[data-color="quaternary"] {
      color: var(--text-quaternary);
    }
  }
  .agree-contents {
    &__header {
      margin: 0;
    }
    &__body {
      margin-top: var(--spacing-lg);
    }
    &__footer {
      margin-top: var(--spacing-lg);
    }
  }
}


<route lang="yaml">
meta:
  id: SCD001A02
  title: ""
  menu: "카드 > 약관동의(BS)"
  layout: EmptyLayout
  category: 혜택
  publish: 김대민
  publishVersion: 0.8
  status: 작업완료
  etc: |
    260128: 약관 동의 BottomSheet 추가(맞춤 카드를 추천받으려면 동의가 필요해요)
</route>
<template>
  <BottomSheet
    variant="none"
    :closableDimm="true"
    :closableDrag="false"
    dimmed
    title="맞춤 카드를 추천받으려면 동의가 필요해요"
    v-model="isOpen"
    class="bs-card-agree"
  >
    <div class="bs-card-agree__contents">
      <div class="agree-contents__header">
        <img
          :src="$cdnURL + '/images/pages/pay/img_card_double.png'"
          alt=""
          class="img_card_double"
          aria-hidden="true"
        />
      </div>
      <div class="agree-contents__body">
        <div class="sc-agree__list agree-outline">
          <div class="agree-list__group">
            <div class="agree-outline__list">
              <SolidListAccordion
                v-for="item in outlineItems"
                :key="item.value"
                :class="[
                  'outline-accordion',
                  { 'is-checked': outlineChecked.includes(item.value) },
                ]"
                :rowClickable="false"
                :value="item.value"
                :prevent-hash="true"
              >
                <template #title>
                  <div class="outline-item check-variant-top">
                    <div class="outline-item__body">
                      <Checkbox
                        :value="item.value"
                        variant="box"
                        align="left"
                        :model-value="outlineChecked.includes(item.value)"
                        class="outline-checkbox"
                        @update:model-value="
                          onToggleoutline(item.value, $event)
                        "
                      >
                        <template #label>
                          <div class="outline-label">
                            <span class="outline-label__main">{{
                              item.label
                            }}</span>
                            <span
                              v-if="item.subText"
                              class="outline-label__subtext"
                              >{{ item.subText }}</span
                            >
                          </div>
                        </template>
                      </Checkbox>
                      <div v-if="item.meta" class="outline-label__meta">
                        <span>{{ item.meta }}</span>
                        <Tooltip
                          placement="top-center"
                          :showClose="true"
                          :closeOnClickOutside="true"
                        >
                          <template #content>
                            <div
                              class="sc-tooltip__content agree-grade-tooltip"
                            >
                              <div class="label-group">
                                <SolidLabel color="cyan" title="안심" />
                                <SolidLabel color="green" title="다소안심" />
                                <SolidLabel color="yellow" title="보통" />
                                <SolidLabel color="orange" title="신중" />
                                <SolidLabel color="red" title="주의" />
                              </div>
                              <p class="agree-grade-tooltip__desc">
                                동의등급제는 개인(신용)정보에 관한 선택적 동의
                                항목에 대해 사생활의 비밀과 자유를 침해할 위험,
                                이익이나 혜택, 동의 내용의 명확성 등을 고려한 뒤
                                5가지 등급을 부여하는 제도예요.
                              </p>
                            </div>
                          </template>
                        </Tooltip>
                      </div>
                    </div>
                  </div>
                </template>
                <div class="outline-panel">
                  <div class="outline-depth2__item">
                    <div class="outline-depth2__item-header">
                      <p class="outline-depth2__item-label">
                        카드 및 금융상품·서비스 안내 및 이용권유를 위한
                        수집·이용
                      </p>
                      <SolidLabel
                        class="outline-depth2__item-grade"
                        color="green"
                        title="다소안심"
                      />
                    </div>
                    <div class="outline-depth2__item-body">
                      <ul class="outline-depth2__item-list">
                        <li class="outline-depth2__list-item">
                          <Checkbox
                            value="agree-outline-2-1"
                            variant="mark"
                            align="left"
                            :model-value="
                              outlineChecked.includes('agree-outline-2-1')
                            "
                            class="outline-depth2__item-checkbox"
                            @update:model-value="
                              onToggleoutline('agree-outline-2-1', $event)
                            "
                            @click.stop
                          >
                            <template #label>
                              <span>고유식별번호 조회 동의</span>
                            </template>
                          </Checkbox>
                        </li>
                        <li class="outline-depth2__list-item">
                          <Checkbox
                            value="agree-outline-2-2"
                            variant="mark"
                            align="left"
                            :model-value="
                              outlineChecked.includes('agree-outline-2-2')
                            "
                            class="outline-depth2__item-checkbox"
                            @update:model-value="
                              onToggleoutline('agree-outline-2-2', $event)
                            "
                            @click.stop
                          >
                            <template #label>
                              <span>개인신용정보 제공 동의</span>
                            </template>
                          </Checkbox>
                        </li>
                      </ul>
                      <div class="agree-depth__link">
                        <TextButton
                          class="agree-depth__link-button"
                          color="secondary"
                          size="small"
                          text="자세히 보기"
                          showGoTo
                        />
                      </div>
                    </div>
                  </div>
                </div>
              </SolidListAccordion>
            </div>
          </div>
        </div>
      </div>
      <div class="agree-contents__footer">
        <div class="sc-bottom-info__card">
          <p class="sc-bottom-info__inner-title">꼭! 알아두세요</p>
          <div class="sc-bottom-info__details">
            <UnorderedList :gap="8">
              <UnorderedListItem
                variant="bullet"
                size="small"
                data-color="quaternary"
                text="동의를 해제하면 맞춤 카드 관련 안내를 받아볼 수 없어요."
              />
              <UnorderedListItem
                variant="bullet"
                size="small"
                data-color="quaternary"
                text="개인(신용)정보의 보유 및 이용기간은 계약 종료 시까지에요."
              />
              <UnorderedListItem
                variant="bullet"
                size="small"
                data-color="quaternary"
                text="카드상품과 부수서비스의 안내 및 이용권유에 동의했더라도 신용정보의 이용 및 보호에 관한 법률에 따라 언제든 관련한 연락 중단을 요청할 수 있어요. 요청은 신한카드 고객센터(1544-7000) 또는 홈페이지(www.shinhancard.com)에서 해주세요."
              />
            </UnorderedList>
          </div>
        </div>
      </div>
    </div>
    <!-- 하단 확인 버튼 -->
    <template #footer>
      <BottomActionContainer :scrollDim="true">
        <BoxButtonGroup size="xlarge" variant="35:65">
          <BoxButton text="다음에" color="secondary" />
          <BoxButton text="확인" :disabled="!isConfirmEnabled" />
        </BoxButtonGroup>
      </BottomActionContainer>
    </template>
  </BottomSheet>
</template>

<script setup>
import {
  BottomActionContainer,
  BottomSheet,
  BoxButton,
  BoxButtonGroup,
  Checkbox,
  SolidListAccordion,
  SolidLabel,
  TextButton,
  Tooltip,
  UnorderedList,
  UnorderedListItem,
} from "@shc-nss/ui/solid";
import { computed, ref } from "vue";

const isOpen = defineModel({ default: true });

const outlineItems = [
  {
    label: "[선택] 개인(신용)정보 수집·이용 동의",
    value: "agree-outline-2",
    meta: "동의등급제 안내",
  },
];

const outlineChecked = ref([]);

const outlineChildMap = {
  "agree-outline-2": ["agree-outline-2-1", "agree-outline-2-2"],
};

const isConfirmEnabled = computed(() => outlineChecked.value.length > 0);

function onToggleoutline(value, checked) {
  const set = new Set(outlineChecked.value);
  if (checked) set.add(value);
  else set.delete(value);

  const parentValue = Object.keys(outlineChildMap).find((key) =>
    outlineChildMap[key].includes(value),
  );
  if (parentValue) {
    const childValues = outlineChildMap[parentValue];
    const hasCheckedChild = childValues.some((child) => set.has(child));
    if (hasCheckedChild) set.add(parentValue);
    else set.delete(parentValue);
  }
  outlineChecked.value = Array.from(set);
}
</script>


function getTermsContent(value) {
  const termsMap = {
    "s1-1-1": `신한 마이카 내차고 서비스를 이용하고자 하는 경우 개인정보보호법에 따라 아래의 개인정보 수집•이용 동의가 필요합니다.
아래 사항 확인 후 동의하여 주시기 바랍니다.

(1) 개인정보의 수집, 이용 목적
마이카 차량관리 서비스, 중고차 시세정보 서비스 제공
(2) 개인정보 수집∙이용 항목
일반개인정보 : 성명, 닉네임, 차명, 세부유형, 자동차등록번호, 제원관리번호, 차종, 차대번호, 원동기형식, 용도, 연식, 색상, 최초등록일, 최종소유자, 제작연월일, 주민(법인)등록번호, 사용본거지, 검사유효기간, 등록사항확인일, 폐쇄일, 시세정보, 리콜정보
(3) 개인(신용)정보의 보유, 이용 기간
서비스 이용 동의 철회 , 회원 탈회 또는 채권채무관계 소멸 후 5년 (단, 관련법령의 별도 규정이 명시되어 있는 경우 그 기간을 따름)

위와 같은 개인정보 수집, 이용 동의를 거부할 권리가 있습니다. 그러나 동의를 거부할 경우 마이카 내차고 서비스를 받으실 수 없습니다.`,
    "s1-1-2": `신한 마이카 내차고 서비스 이용을 위하여 제3자에게 개인정보를 제공할 경우 개인정보보호법에 따라 본인이 사전 동의가 필요합니다.
아래 사항 확인 후 동의하여 주시기 바랍니다.

(1) 개인정보를 제공받는 자
나이스평가정보㈜
(2) 제공대상 개인정보
일반개인정보 : 성명, 자동차번호
(3) 제공받는자의 이용목적
자동차 정보 및 중고차 시세 조회 / 제공
(4) 보유 및 이용기간
서비스 이용 동의 철회 , 회원 탈회 또는 채권채무관계 소멸 후 5년 (단, 관련법령의 별도 규정이 명시되어 있는 경우 그 기간을 따름)

위와 같은 개인정보 수집, 이용 동의를 거부할 권리가 있습니다. 그러나 동의를 거부할 경우 마이카 내차고 서비스를 받으실 수 없습니다.`,
  };

  // TODO: 실제 API 호출로 변경
  // 예: return await fetchTermsContent(value);
  return termsMap[value] || "";
}






// v0.9 또는 0.8에서 신규로 추가된 부분부터 1뎁스 항목체크 모양은 box->mark로 수정 2뎁스항목은 좌측 들여쓰기 구조 class agree_new 추가
.sc-agree__list.agree_new {
  .agree-subitem {
    .sv-accordion-item--variant-solid  {
      > .sv-accordion-panel {
        > .sv-accordion-panel__content {
          padding-left: calc(var(--spacing-3xl) + var(--spacing-2xl));
        }
      }
    }
  }
}


// 체크항목 없는 유형
<template>
  <BottomSheet
    v-model="isOpen"
    title="자산 연결하기 전에 동의가 필요해요"
    variant="closeButton"
    class="sc-terms__popup px-none"
  >
    <!-- 콘텐츠 영역 -->
    <div class="sc-contents__body sc-agree__page">
      <section>
        <div class="sc-agree__list compound" role="region">
          <div class="agree-list__group">
            <!-- ======================================== -->
            <!-- 1뎁스 영역: 기본 약관 항목들 -->
            <!-- ======================================== -->
            <!-- 260116: 좌측 체크항목 제거 후 item-label__sub 에 class flex-auto 추가 -->
            <div class="agree-sublist" role="group">
              <div
                v-for="item in subItems4"
                :key="item.value"
                class="agree-subitem"
              >
                <div class="agree-item agree-item__sub">
                  <span class="agree-item__label item-label__sub flex-auto">{{
                    item.label
                  }}</span>
                  <IconButton
                    size="small"
                    icon-name="Chevron_right"
                    :aria-label="`${item.label} 상세보기`"
                    @click="handleDetailClick(item)"
                  />
                </div>
              </div>
              <!-- 개인정보 처리방침 링크 -->
              <div class="agree-depth__link pr-2xl">
                <TextButton
                  class="agree-depth__link"
                  color="secondary"
                  size="small"
                  text="개인정보 처리방침"
                  showGoTo
                />
              </div>
            </div>
          </div>
        </div>
      </section>
    </div>

    <Divider variant="group" color="tertiary" class="mb-4xl" />

    <div class="sc-contents__foot">
      <div class="sc-bottom-info__inner">
        <div class="sc-bottom-info__details">
          <UnorderedList :gap="8" data-color="quaternary">
            <UnorderedListItem
              text="잘 이용하지 않는 서비스는 탈퇴 후 내 정보를 삭제할 수 있어요."
            />
            <UnorderedListItem
              text="나의 마이데이터 서비스 가입현황은 마이데이터 종합포털에서 확인할 수 있어요."
            />
          </UnorderedList>
        </div>
        <!-- [251027] 마이데이터 서비스 안내 하단 링크 추가 -->
        <div class="agree-depth__link">
          <TextButton
            class="agree-depth__link"
            color="secondary"
            size="xsmall"
            text="종합포털 바로가기"
            showGoTo
          />
        </div>
      </div>
    </div>

    <template #footer>
      <BoxButtonGroup size="xlarge" variant="35:65">
        <BoxButton text="괜찮아요" color="secondary" @click="isOpen = false" />
        <BoxButton text="좋아요" color="primary" />
      </BoxButtonGroup>
    </template>
  </BottomSheet>
</template>

<script setup>
import {
  BottomSheet,
  BoxButton,
  BoxButtonGroup,
  Divider,
  IconButton,
  TextButton,
  UnorderedList,
  UnorderedListItem,
} from "@shc-nss/ui/solid";

// 팝업 상태 관리
const isOpen = defineModel({ default: true });

// JavaScript/TypeScript 호환 배열
const subItems4 = [
  {
    label: "[필수] 마이데이터 서비스 이용약관",
    value: "s4-1",
  },
  {
    label: "[필수] 마이데이터 서비스 수집이용동의",
    value: "s4-1-2",
  },
];

/**
 * 상세보기 클릭 핸들러
 */
function handleDetailClick(item) {
  // TODO: 상세보기 페이지로 이동하거나 모달 표시
  console.log("상세보기 클릭:", item);
}
</script>























// 체크항목 있는 유형

<template>
  <BottomSheet
    v-model="isOpen"
    title="자산 연결하기 전에 동의가 필요해요"
    variant="closeButton"
    class="sc-terms__popup px-none"
  >
    <!-- 콘텐츠 영역 -->
    <div class="sc-contents__body sc-agree__page">
      <section>
        <div class="sc-agree__list compound" role="region">
          <div class="agree-list__group">
            <!-- ======================================== -->
            <!-- 1뎁스 영역: 기본 약관 항목들 -->
            <!-- ======================================== -->
            <div class="agree-sublist" role="group">
              <div
                v-for="item in subItems4"
                :key="item.value"
                class="agree-subitem"
              >
                <div
                  class="agree-item agree-item__sub"
                  :class="{
                    'is-checked': subAgrees4.includes(item.value),
                  }"
                >
                  <Checkbox
                    :value="item.value"
                    variant="mark"
                    align="left"
                    :model-value="subAgrees4.includes(item.value)"
                    class="agree-item__checkbox item-checkbox__sub"
                    @update:model-value="onToggleSub4(item.value, $event)"
                  >
                    <template #label>
                      <span class="agree-item__label item-label__sub">{{
                        item.label
                      }}</span>
                    </template>
                  </Checkbox>
                  <IconButton
                    size="small"
                    icon-name="Chevron_right"
                    :aria-label="`${item.label} 상세보기`"
                    @click="handleDetailClick(item)"
                  />
                </div>
              </div>
              <!-- 개인정보 처리방침 링크 -->
              <div class="agree-depth__link pr-2xl">
                <TextButton
                  class="agree-depth__link"
                  color="secondary"
                  size="small"
                  text="개인정보 처리방침"
                  showGoTo
                />
              </div>
            </div>
          </div>
        </div>
      </section>
    </div>

    <Divider variant="group" color="tertiary" class="mb-4xl" />

    <div class="sc-contents__foot">
      <div class="sc-bottom-info__inner">
        <div class="sc-bottom-info__details">
          <UnorderedList :gap="8" data-color="quaternary">
            <UnorderedListItem text="잘 이용하지 않는 서비스는 탈퇴 후 내 정보를 삭제할 수 있어요." />
            <UnorderedListItem text="나의 마이데이터 서비스 가입현황은 마이데이터 종합포털에서 확인할 수 있어요." />
          </UnorderedList>
        </div>
        <!-- [251027] 마이데이터 서비스 안내 하단 링크 추가 -->
        <div class="agree-depth__link">
          <TextButton
            class="agree-depth__link"
            color="secondary"
            size="xsmall"
            text="종합포털 바로가기"
            showGoTo
          />
        </div>
      </div>
    </div>

    <template #footer>
      <BoxButtonGroup size="xlarge" variant="35:65">
        <BoxButton text="괜찮아요" color="secondary" @click="isOpen = false" />
        <BoxButton
          text="좋아요"
          color="primary"
        />
      </BoxButtonGroup>
    </template>
  </BottomSheet>
</template>

<script setup>
import {
  BottomSheet,
  BoxButton,
  BoxButtonGroup,
  Checkbox,
  Divider,
  IconButton,
  TextButton,
  UnorderedList,
  UnorderedListItem,
} from "@shc-nss/ui/solid";
import { ref } from "vue";

// 팝업 상태 관리
const isOpen = defineModel({ default: true });

// JavaScript/TypeScript 호환 배열
const subItems4 = [
  {
    label: "[필수] 마이데이터 서비스 이용약관",
    value: "s4-1",
  },
  {
    label: "[필수] 마이데이터 서비스 수집이용동의",
    value: "s4-1-2",
  },
];

const subAgrees4 = ref([]);

/**
 * 동작 로직
 */
function onToggleSub4(value, checked) {
  const set = new Set(subAgrees4.value);
  if (checked) set.add(value);
  else set.delete(value);
  subAgrees4.value = Array.from(set);
}

/**
 * 상세보기 클릭 핸들러
 */
function handleDetailClick(item) {
  // TODO: 상세보기 페이지로 이동하거나 모달 표시
  console.log("상세보기 클릭:", item);
}



```
{% endraw %}
---
