<template>
  <div class="tab-pane fade" :class="{ 'active show': customizer == 'layouts' }" id="c-pills-home">
    <ul class="sidebar-type layout-grid layout-types">
      <li data-attr="compact-sidebar">
        <div class="layout-img">
          <a @click="handlePageLayputs('compact-wrapper', 'Dubai')"><img src="/images/landing/layout-images/dubai.jpg"
              class="img-fluid" alt="oneone" /></a>

          <h6>Dubai</h6>
        </div>
      </li>
      <li data-attr="material-layout horizontal-wrapper">
        <div class="layout-img">
          <a @click="
            handlePageLayputs(
              'horizontal-wrapper material-type',
              'LosAngeles'
            )
          "><img src="/images/landing/layout-images/los-angle.png" class="img-fluid" alt="one" /></a>

          <h6>Los Angeles</h6>
        </div>
      </li>
      <li data-attr="dark-sidebar">
        <div class="layout-img">
          <a @click="handlePageLayputs('compact-wrapper dark-sidebar', 'Paris')"><img
              src="/images/landing/layout-images/paris.jpg" class="img-fluid" alt="one" /></a>

          <h6>Paris</h6>
        </div>
      </li>

      <li data-attr="compact-wrap">
        <div class="layout-img">
          <a @click="handlePageLayputs('compact-sidebar', 'Tokyo')"><img src="/images/landing/layout-images/tokyo.jpg"
              class="img-fluid" alt="one" /></a>

          <h6>Tokyo</h6>
        </div>
      </li>
      <li data-attr="compact-small">
        <div class="layout-img">
          <a @click="
            handlePageLayputs('compact-sidebar compact-small', 'Moscow')
          "><img src="/images/landing/layout-images/moscow.jpg" class="img-fluid" alt="one" /></a>

          <h6>Moscow</h6>
        </div>
      </li>
      <li data-attr="enterprice-type">
        <div class="layout-img">
          <a @click="
            handlePageLayputs(
              'horizontal-wrapper enterprice-type',
              'Singapore'
            )
          "><img src="/images/landing/layout-images/singapore.jpg" class="img-fluid" alt="one" /></a>

          <h6>Singapore</h6>
        </div>
      </li>
      <li data-attr="box-layout" class="box-layout">
        <div class="layout-img">
          <a @click="handlePageLayputs('compact-wrapper box-layout', 'NewYork')"><img
              src="/images/landing/layout-images/newyork.png" class="img-fluid" alt="one" /></a>

          <h6>New York</h6>
        </div>
      </li>
      <!-- <li data-attr="advance-type">
        <div class="layout-img">
          <a @click="
            handlePageLayputs(
              'horizontal-wrapper enterprice-type advance-layout',
              'Barcelona'
            )
          "><img src="/images/landing/layout-images/barc.jpg" class="img-fluid" alt="one" /></a>

          <h6>Barcelona</h6>
        </div>
      </li> -->
      <!-- <li data-attr="color-sidebar">
        <div class="layout-img">
          <a @click="
            handlePageLayputs('compact-wrapper color-sidebar', 'Madrid')
          "><img src="/images/landing/layout-images/madrid.jpg" class="img-fluid" alt="one" /></a>

          <h6>Madrid</h6>
        </div>
      </li> -->
      <li data-attr="material-icon">
        <div class="layout-img">
          <a @click="
            handlePageLayputs(
              'compact-sidebar compact-small material-icon',
              'Rome'
            )
          "><img src="/images/landing/layout-images/rome.jpg" class="img-fluid" alt="one" /></a>

          <h6>Rome</h6>
        </div>
      </li>
      <!-- <li data-attr="modern-layout">
        <div class="layout-img">
          <a @click="handlePageLayputs('compact-wrapper modern-type', 'Seoul')"><img
              src="/images/landing/layout-images/seoul.jpg" class="img-fluid" alt="one" /></a>

          <h6>Seoul</h6>
        </div>
      </li> -->
      <li class="only-body" data-attr="default-body">
        <div class="layout-img">
          <a @click="handlePageLayputs('only-body', 'London')"><img src="/images/landing/layout-images/landon.png"
              class="img-fluid" alt="one" /></a>

          <h6>London</h6>
        </div>
      </li>
    </ul>
  </div>
</template>
<script>
import { mapState } from 'pinia';
import { layoutClasses } from '../../constants/layout';
import { useMenuStore } from '~~/store/menu';
import { useLayoutStore } from '~~/store/layout';
export default {
  name: 'Customlayout',
  computed: {
    ...mapState(useMenuStore, {
      customizer: 'customizer',

      menuItems: 'data',
      togglesidebar: 'togglesidebar',
    }),
    ...mapState(useLayoutStore, {
      layout: 'layout',
    })
  },
  methods: {
    handlePageLayputs(val, layout) {
      const layoutobj = layoutClasses.find((item) => Object.keys(item).pop() === layout);
      useLayoutStore().setCustomizeSidebarType(layoutobj[layout])
      this.layout.settings.layout = layout;
      this.$router.push({ query: { layout: layout } }).catch(err => err);

      if (!layoutobj[layout].split(' ').includes('compact-sidebar')) {
        useMenuStore().activeoverlay = true;
        document.getElementById('sidebar-menu').classList.remove('d-flex');
      } else {
        useMenuStore().activeoverlay = false;
        document.getElementById('sidebar-menu').classList.add('d-flex');
      }

      if (layout === 'Dubai') {
        useLayoutStore().boxlayout = true;
      } else {
        useLayoutStore().boxlayout = false;
      }

      if (layout === 'Tokyo' || layout === 'Moscow' || layout === 'Rome') {
        useMenuStore().togglesidebar = true;
      }
    },
  },
};
</script>