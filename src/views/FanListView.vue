<script lang="ts">
import { ref } from 'vue';

const apiBaseUrl = import.meta.env.VITE_API_BASE_URL

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
    const url = `${apiBaseUrl}/api/fans/`;
    fetch(url, {method: 'GET'})
      .then(response => response.json())
      .then((data: Fan[]) => {
        fanList.value = data;
      });

    return {
      fanList
    };
  },
  methods: {
    toggleDirection(fan: Fan) {
      const url = `${apiBaseUrl}/api/fans/${fan.id}/toggle_direction/`;
      fetch(url, {method: 'POST'})
        .then(response => response.json())
        .then(data => {
          console.log('Direction toggled:', data);
        })
        .catch(error => {
          console.error('Failed to toggle direction:', error);
        });
    },
    cycleSpeed(fan: Fan) {
      const url = `${apiBaseUrl}/api/fans/${fan.id}/cycle_speed/`;
      fetch(url, {method: 'POST'})
        .then(response => response.json())
        .then(data => {
          fan.speed_state = data.speed_state;
          console.log('Speed changed:', data);
        })
        .catch(error => {
          console.error('Failed to change speed:', error);
        });
    },
  },
  computed: {
    getSpeedLabel() {
      return (speedState: number) => {
        switch (speedState) {
          case 0:
            return 'OFF';
          case 1:
            return 'SLOW';
          case 2:
            return 'MEDIUM';
          case 3:
            return 'FAST';
          default:
            return 'Unknown';
        }
      };
    }
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

                <h2>Fan Location: {{ fan.name }}</h2>

                <div class="row">

                  <div class="col-md-6 col-xs-12">
                    <div class="ns-form-group ns-toggle--ui-switch">
                      <h3 class="ns-label-wrapper">
                        <div class="ns-label" for="event-name">Direction</div>
                      </h3>
                      <input type="checkbox" :id="'fanDirection' + fan.id" class="ns-toggle__input" :checked="fan.direction_state === 1" @change="toggleDirection(fan)">
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
                  </div>

                  <div class="col-md-6 col-xs-12">
                    <div class="ns-form-group">
                      <h3 class="ns-label-wrapper">
                        <label class="ns-label">
                          Speed
                        </label>
                      </h3>
                      <div class="ns-input__wrapper inline">
                        <button class="btn-lg btn-default px-120" @click="cycleSpeed(fan)">{{ getSpeedLabel(fan.speed_state) }}</button>
                      </div>
                    </div>
                  </div>

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
.px-120 {
  width: 120px;
}
</style>
