<template>
  <!--判断是否是标签节点-->
  <block v-if="node.node == 'element'">
    <block v-if="node.tag == 'button'">
      <button type="default" size="mini">
        <block v-for="node of node.nodes" :key="node.index">
          <wx-parse-template :node="node" />
        </block>
      </button>
    </block>

    <!--li类型-->
    <block v-else-if="node.tag == 'li'">
      <view :class="node.classStr" class="li" :style="node.styleStr">
        <view :class="node.classStr" class="li-inner">
          <view :class="node.classStr" class="li-text">
            <view :class="node.classStr" class="li-circle"></view>
          </view>
          <view :class="node.classStr" class="li-text">
            <block v-for="node of node.nodes" :key="node.index">
              <wx-parse-template :node="node" />
            </block>
          </view>
        </view>
      </view>
    </block>

    <!--video类型-->
    <block v-else-if="node.tag == 'video'">
      <wx-parse-video :node="node" />
    </block>

    <!--img类型-->
    <block v-else-if="node.tag == 'img'">
      <wx-parse-img :node="node" />
    </block>

    <!--a类型-->
    <block v-else-if="node.tag == 'a'">
      <view bindtap="wxParseTagATap" :class="node.classStr" class="inline a" data-src="node.attr.href" :style="node.styleStr">
        <block v-for="node of node.nodes" :key="node.index">
          <wx-parse-template :node="node" />
        </block>
      </view>
    </block>

    <!--br类型-->
    <block v-else-if="node.tag == 'br'">
      <text>\n</text>
    </block>

    <!--其他块级标签-->
    <block v-else-if="node.tagType == 'block'">
      <view :class="[node.classStr, node.tag]" :style="node.styleStr">
        <block v-for="node of node.nodes" :key="node.index">
          <wx-parse-template :node="node" />
        </block>
      </view>
    </block>

    <!--内联标签-->
    <view v-else :class="[node.classStr, node.tag]" class="inline" :style="node.styleStr">
      <block v-for="node of node.nodes" :key="node.index">
        <wx-parse-template :node="node" />
      </block>
    </view>

  </block>

  <!--判断是否是文本节点-->
  <block v-else-if="node.node == 'text'">
    <view class="wxParseText inline" :style="node.styleStr">
      {{node.text}}
    </view>
  </block>
</template>

<script>
import wxParseTemplate from './wxParseTemplate3'
import wxParseImg from './wxParseImg'
import wxParseVideo from './wxParseVideo'

export default {
  name: 'wxParseTemplate2',
  props: {
    node: {}
  },
  components: {
    wxParseTemplate,
    wxParseImg,
    wxParseVideo
  }
}
</script>
