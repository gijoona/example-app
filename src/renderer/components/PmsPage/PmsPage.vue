<template>
  <b-container fluid>
    <b-row>
      <b-col>
        <h2>PMS Admin</h2>
      </b-col>
    </b-row>
    <b-row>
      <b-col>
        <b-list-group>
          <b-list-group-item v-for="item in wrkList" :key="item.wrk" @click="chgWrk(item.wrk)">{{ item.label }}</b-list-group-item>
        </b-list-group>
      </b-col>
      <b-col>
        <b-card>
          <div slot="header">대상정보</div>
          <div v-if="isCurrWrk('delPR')">
            <b-card-body>
              <b-form-group
                id="fieldset-txtPrNo"
                label-cols-sm="3"
                label-cols-lg="3"
                label="PR No."
                label-for="txtPrNo"
                :invalid-feedback="invalidFeedback"
                :valid-feedback="validFeedback"
                :state="prNoState"
              >
                <b-form-input id="txtPrNo" v-model="upperPrNo" :state="prNoState" trim></b-form-input>
              </b-form-group>
              <b-row align-h="end">
                <b-button type="submit" variant="primary">실행</b-button>
              </b-row>
            </b-card-body>
          </div>
        </b-card>
      </b-col>
    </b-row>
  </b-container>
</template>
<script>
export default {
  name: 'pms-page',
  data: function () {
    return {
      prNo: '',
      currWrk: 'delPR',
      wrkList: [
        { wrk: 'delPR', label: '삭제' },
        { wrk: 'chgprice', label: '가격변경' },
        { wrk: 'chginfo', label: '기본정보수정' },
        { wrk: 'donevouchor', label: '입찰건 상태변경(바우처작성)' }
      ]
    }
  },
  computed: {
    upperPrNo: {
      set: function (val) {
        this.prNo = val.toUpperCase()
      },
      get: function () {
        return this.prNo
      }
    },
    prNoState: function () {
      return this.prNo.length > 1
    },
    invalidFeedback: function () {
      if (!(this.prNoState)) {
        return 'PR번호를 입력하세요.'
      }
    },
    validFeedback: function () {
      return this.prNoState === true ? 'OK!!!' : ''
    }
  },
  methods: {
    // 현재의 wrk타입과 display block이 같은지 반환
    isCurrWrk: function (targetWrk) {
      if (this.currWrk === targetWrk) return true
      else return false
    },
    // 리스트를 선택하면 선택된 항목의 wrk타입을 this.wrk타입에 입력한다.
    chgWrk: function (targetWrk) {
      this.currWrk = targetWrk
    }
  }
}
</script>