<script lang="tsx">
import { Component, Prop, Vue } from 'vue-property-decorator';
import Collapsed from '../../Collapse/index.vue';
import { CollapseConfig } from '@model/components/layout.model';
import { Action, namespace, State } from 'vuex-class';
import styles from './Header.module.scss';

@Component
export default class WvtsHeader extends Vue {
  @Prop(Object) readonly editStyle: any;
  @Prop({
    default() {
      return {};
    }
  })
  readonly collapseConfig: CollapseConfig;
  render(h: any) {
    const { $scopedSlots, editStyle } = this;

    /**
     * SiteTitle 插槽渲染判断
     */
    const SiteTitle = $scopedSlots.siteTitle ? (props => $scopedSlots.siteTitle(props))() : null;

    /**
     * 右侧操作栏位插槽
     */
    const Actions = $scopedSlots.actions ? (props => $scopedSlots.actions(props))() : null;

    const { position } = this.collapseConfig;

    return (
      <header class={styles.header} style={editStyle}>
        {SiteTitle && <div class={styles.titlePlace}>{SiteTitle}</div>}
        {position && position === 'header' && <Collapsed />}
        {Actions && <div class={styles.actionPlace}>{Actions}</div>}
      </header>
    );
  }
}
</script>
