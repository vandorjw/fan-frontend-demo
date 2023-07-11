<script lang="ts">
import { ref } from 'vue';

interface Fan {
  id: number;
  name: string;
  slug: string;
  direction_state: number;
  speed_state: number;
}

export default {
  setup() {
    const fanList = ref<Fan[]>([]);

    fetch('https://fan-api-demo-d0fa45500d2d.herokuapp.com/api/fans/')
      .then(response => response.json())
      .then((data: Fan[]) => {
        fanList.value = data;
      });

    return {
      fanList
    };
  }
};
</script>

<template>
  <div class="fan-list">
    <h1>Fan List</h1>

    <div v-if="fanList">

      <section v-for="fan in fanList" :key="fan.id" class="row">
        <div class="col-md-12 col-xs-12">

          <!-- Tab nav -->
          <ul class="nav nav-tabs" role="tablist">
            <li class="nav-item">
              <a class="nav-link active" :href="'#status' + fan.id" role="tab" data-toggle="tab">Status</a>
            </li>
            <li class="nav-item">
              <a class="nav-link" :href="'#settings' + fan.id" role="tab" data-toggle="tab">Settings</a>
            </li>
          </ul>

          <div class="exampleDisplay">
            <div class="tab-content">

              <div role="tabpanel" class="tab-pane fade in active show" :id="'status' + fan.id">
                <div class="ns-form-group ns-toggle--ui-switch">
                  <h3 class="ns-label-wrapper">
                    <div class="ns-label" for="event-name">{{ fan.name }}</div>
                  </h3>

                  <h4>Direction</h4>
                  <input type="checkbox" :id="'fanDirection' + fan.id" class="ns-toggle__input">
                  <label class="ns-toggle__label" :for="'fanDirection' + fan.id">
                    <div class="ns-toggle__disabled-msg" data-checked="Pending" data-unchecked="Completed">
                    </div>
                    <span class="ns-toggle__screenreader">Automatic text notifications</span>
                    <div class="ns-toggle-option-LEFT mr-2" aria-hidden="true">
                      Forward
                    </div>
                    <div class="ns-toggle-switch" role="presentation" aria-hidden="true"></div>
                    <div class="ns-toggle-option-RIGHT ml-2" aria-hidden="true">
                      Reverse
                    </div>
                  </label>
                </div>
              </div><!-- / tabpanel status -->

              <div role="tabpanel" class="tab-pane fade" :id="'settings' + fan.id">
                <div class="ns-form-group ns-toggle--ui-switch">
                  <h3 class="ns-label-wrapper">
                    <div class="ns-label" for="event-name">
                      Not Implemented ...
                    </div>
                  </h3>
                </div>
              </div><!-- / tabpanel settings -->

            </div><!-- / tab-content -->
          </div><!-- / example col -->
        </div><!-- / example col -->
      </section>

    </div>
    <div v-if="!fanList" class="text-center">
      <div class="spinner-border spinner-border-sm"></div>
    </div>

  </div>
</template>


<style>
.fan-list {
  width: 100%;
}
</style>
