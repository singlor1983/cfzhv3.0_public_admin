<template>
  <div class="list-wrap">
    <!-- <a-typography-title class="block-title" :heading="6">
      {{ $t('cardList.tab.title.service') }}
    </a-typography-title> -->
    <a-row class="list-row" :gutter="24">
      <a-col
        v-for="item in renderData"
        :key="item.id"
        :xs="12"
        :sm="12"
        :md="12"
        :lg="6"
        :xl="6"
        :xxl="6"
        class="list-col"
        style="min-height: 162px"
      >
        <CardWrap
          :loading="loading"
          :title="item.title"
          :description="item.description"
          :default-value="item.enable"
          :action-type="item.actionType"
          :expires="item.expires"
          :open-txt="item.openTxt"
          :close-txt="$t('cardList.service.cancel')"
          :expires-text="$t('cardList.service.renew')"
          :tag-text="$t('cardList.service.tag')"
          :expires-tag-text="$t('cardList.service.expiresTag')"
          :icon="item.icon"
          @clickOptions="clickOptions"
        >
          <template #skeleton>
            <a-skeleton :animation="true">
              <a-skeleton-line :widths="['100%', '40%', '100%']" :rows="3" />
              <a-skeleton-line :widths="['40%']" :rows="1" />
            </a-skeleton>
          </template>
        </CardWrap>
      </a-col>
    </a-row>
  </div>
</template>

<script lang="ts" setup>
  import useRequest from '@/hooks/request';
  import CardWrap from './card-wrap.vue';

  const emit = defineEmits(['clickOptions']);

  const renderData = [
    {
      id: 1,
      icon: 'code',
      title: '编辑',
      openTxt: '去编辑',
      description:
        '支持轻松编辑信息，确保数据随时更新，提高工作效率和数据精确性，满足信息管理需求。',
      enable: false,
      enable: false,
    },
    {
      id: 2,
      icon: 'edit',
      title: '删除',
      openTxt: '点击删除',
      description:
        '简单删除不必要记录，保持系统整洁，提高数据管理质量，确保只有重要信息留存。',
      expires: false,
      enable: false,
    },
    {
      id: 3,
      icon: 'user',
      title: '通道',
      openTxt: '查看',
      description:
        '灵活配置和管理通道，保证数据传输顺畅，确保系统之间的数据互通畅通。',
      enable: false,
    },
    {
      id: 4,
      icon: 'user',
      title: '收费规则',
      openTxt: '查看',
      description:
        '制定和优化收费策略，满足多样化收费需求，提高财务管理效率和准确性。',
      enable: false,
    },
    {
      id: 5,
      icon: 'user',
      title: '收款账号',
      openTxt: '查看',
      description: '维护和管理收款账户信息，确保资金流向可追踪，降低支付风险。',
      enable: false,
    },
    {
      id: 6,
      icon: 'user',
      title: '显示屏',
      openTxt: '查看',
      description:
        '掌控和管理显示屏幕内容，展示引人注目的信息和广告，提升宣传和展示效果。',
      enable: false,
    },
    {
      id: 7,
      icon: 'user',
      title: '管理人员',
      openTxt: '查看',
      description:
        '分配职责和权限，合理组织团队，提升管理效率，确保工作流畅有序进行。',
      enable: false,
    },
    {
      id: 8,
      icon: 'user',
      title: '值班记录',
      openTxt: '查看',
      description:
        '详细记录和跟踪人员值班情况，确保工作计划有序执行，提高工作效率。',
      enable: false,
    },
    {
      id: 9,
      icon: 'user',
      title: '电站转让',
      openTxt: '点击转让',
      description: '实现电站资产的过户和交接，确保业务平稳过渡，降低交接风险。',
      enable: false,
    },
    {
      id: 11,
      icon: 'user',
      title: '数据报表',
      openTxt: '查看',
      description:
        '查看充电数据分析，收入报表等，查看该充电站每个渠道的收入情况，充电日报和月报。',
      enable: false,
    }
  ];

  const clickOptions = (clickType: string) => {
    console.log(
      '🚀🚀🚀🚀🚀🚀🚀 ~ file: the-service.vue:144 ~ clickOptions ~ clickType:',
      clickType
    );
    emit('clickOptions', clickType);
  };
</script>

<style scoped lang="less"></style>
