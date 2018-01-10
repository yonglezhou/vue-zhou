<template>
  <div class="MsgFlashList">
    <transition-group class="msgul" :class="{ 'reverse-list': reverse }" name="msg-fade" tag="ul">
      <li class="msgli" v-for="msgItem in msgList" :key="msgItem.key">
        {{ msgItem.msg }}
      </li>
    </transition-group>
  </div>
</template>
<script>
/**
 * MsgFlashList
 * @reverse reverse msg list direction
 * @methods: addFlashMsg(newMsg) add new msg
 */
export default {
  name: 'MsgFlashList',
  props: {
    reverse: Boolean
  },
  data: function () {
    return {
      msgList: [],
      msgKey: (new Date()).getTime()
    }
  },
  methods: {
    addFlashMsg: function (newMsg) {
      console.log(newMsg)
      var _this = this
      var msgItem = { msg: newMsg !== undefined ? newMsg : this.msgKey, key: this.msgKey++ }
      if (!this.reverse) {
        this.msgList.unshift(msgItem)
        setTimeout(function () {
          _this.msgList.pop()
        }, 5000)
      } else {
        this.msgList.push(msgItem)
        setTimeout(function () {
          _this.msgList.shift()
        }, 5000)
      }
    }
  }
}

</script>
<style>
.MsgFlashList {
  height: 500px;
  position: relative;
}

.MsgFlashList ul {
  list-style: none;
  max-width: 100%;
  padding-left: 0rem;
  margin-top: 0rem;
  margin-bottom: 0rem;
}

.reverse-list {
  position: absolute;
  bottom: 0px;
}

.MsgFlashList ul li {
  list-style: none;
  float: left;
  clear: both;
  max-width: 100%;
  margin-top: 2px;
  border-radius: 0.25rem;
  padding-left: 0.2rem;
  padding-right: 0.2rem;
  text-align: left;
  overflow: hidden;
  text-overflow: ellipsis;
  background-color: #c2c2d6;
}

.msg-fade-move,
.msg-fade-enter-active,
.msg-fade-leave-active {
  transition: opacity 0.5s;
}

.msg-fade-enter,
.msg-fade-leave-to {
  opacity: 0;
}

</style>
