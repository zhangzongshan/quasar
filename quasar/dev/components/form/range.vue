<template>
  <div>
    <div class="q-layout-padding" :class="dark ? 'bg-black text-white' : null">
      <q-toggle v-model="dark" :dark="dark" :dense="dense" label="Dark" />
      <q-toggle v-model="dense" :dark="dark" :dense="dense" label="Dense" />

      <p class="caption">
        Standalone
        <span class="label inline bg-secondary text-white">
          Model <span class="right-detail"><em>{{ standalone.min }} to {{ standalone.max }}</em> &nbsp;&nbsp;(0 to 50)</span>
        </span>
      </p>
      <q-range :dark="dark" :dense="dense" @change="onChange" @input="onInput" v-model="standalone" :min="0" :max="50"/>
      <q-range :dark="dark" :dense="dense" @change="val => { standalone = val; onChange(val); }" @input="onInput" :value="standalone" :min="0" :max="50" label/>
      <q-range :dark="dark" :dense="dense" v-model="standalone" :min="0" :max="50" />

      <p class="caption">
        Step 0
        <span class="label inline bg-secondary text-white">
          Model <span class="right-detail"><em>{{ stepZero.min }} to {{ stepZero.max }}</em> &nbsp;&nbsp;(0 to 100)</span>
        </span>
      </p>
      <q-range :dark="dark" :dense="dense" v-model="stepZero" :step="0" />

      <p class="caption">
        With Floating Point Precision
        <span class="label inline bg-secondary text-white">
          Model <span class="right-detail"><em>{{ precision }}</em> &nbsp;&nbsp;(0.1 to 2.0, step 0.01) - decimals set to 1</span>
        </span>
      </p>
      <q-range :dark="dark" :dense="dense" v-model="precision" :min="0.1" :max="2" :step="0.01" />

      <p class="caption">
        With Floating Point Precision
        <span class="label inline bg-secondary text-white">
          Model <span class="right-detail"><em>{{ precision }}</em> &nbsp;&nbsp;(0.1 to 2.0, step 0.01) - decimals not set (auto 2)</span>
        </span>
      </p>
      <q-range :dark="dark" :dense="dense" v-model="precision" :min="0.1" :max="2" :step="0.01"/>

      <p class="caption">
        With Label
        <span class="label inline bg-secondary text-white">
          Model <span class="right-detail"><em>{{ label.min }} to {{ label.max }}</em> &nbsp;&nbsp;(-20 to 20, step 4)</span>
        </span>
      </p>
      <q-range :dark="dark" :dense="dense" v-model="label" :min="-20" :max="20" :step="4" label/>

      <p class="caption">
        With Step
        <span class="label inline bg-secondary text-white">
          Model <span class="right-detail"><em>{{ step.min }} to {{ step.max }}</em> &nbsp;&nbsp;(0 to 45, step 5)</span>
        </span>
      </p>
      <q-range :dark="dark" :dense="dense" v-model="step" :min="0" :max="45" :step="5" label/>

      <p class="caption">
        Snap to Step
        <span class="label inline bg-secondary text-white">
          Model <span class="right-detail"><em>{{ snap.min }} to {{ snap.max }}</em> &nbsp;&nbsp;(0 to 10, step 2)</span>
        </span>
      </p>
      <q-range :dark="dark" :dense="dense" v-model="snap" :min="0" :max="10" :step="2" label snap/>

      <p class="caption">
        With Markers + Snap to Step
        <span class="label inline bg-secondary text-white">
          Model <span class="right-detail"><em>{{ marker.min }} to {{ marker.max }}</em> &nbsp;&nbsp;(-6 to 10, step 2)</span>
        </span>
      </p>
      <q-range :dark="dark" :dense="dense" v-model="marker" :min="-6" :max="10" :step="2" label snap markers/>

      <p class="caption">
        Display Label Always
        <span class="label inline bg-secondary text-white">
          Model <span class="right-detail"><em>{{ label.min }} to {{ label.max }}</em> &nbsp;&nbsp;(-20 to 20, step 4)</span>
        </span>
      </p>
      <q-range :dark="dark" :dense="dense" v-model="label" :min="-20" :max="20" :step="4" label-always/>

      <p class="caption">
        With custom values for labels
        <span class="label inline bg-secondary text-white">
          Model <span class="right-detail"><em>{{ label.min }} to {{ label.max }}</em> &nbsp;&nbsp;(-20 to 20, step 4)</span>
        </span>
      </p>
      <q-range :dark="dark" :dense="dense" v-model="label" :min="-20" :max="20" :step="4" label-always :left-label-value="`${label.min}px`" :right-label-value="`${label.max}px`"/>

      <p class="caption">
        Drag Range
        <span class="label inline bg-secondary text-white">
          Model <span class="right-detail"><em>{{ range.min }} to {{ range.max }}</em> &nbsp;&nbsp;(0 to 100, step 1)</span>
        </span>
      </p>
      <q-range :dark="dark" :dense="dense" @change="onChange" @input="onInput" v-model="range" :min="0" :max="100" label drag-range/>
      <q-range :dark="dark" :dense="dense" @change="val => { range = val; onChange(val); }" @input="onInput" :value="range" :min="0" :max="100" label drag-range/>

      <p class="caption">
        Drag Range + Snap to Step
        <span class="label inline bg-secondary text-white">
          Model <span class="right-detail"><em>{{ rangeSnap.min }} to {{ rangeSnap.max }}</em> &nbsp;&nbsp;(0 to 100, step 5)</span>
        </span>
      </p>
      <q-range :dark="dark" :dense="dense" v-model="rangeSnap" :min="0" :max="100" :step="5" drag-range label markers snap/>

      <p class="caption">
        Drag Only Range (Fixed Interval)
        <span class="label inline bg-secondary text-white">
          Model <span class="right-detail"><em>{{ onlyRange.min }} to {{ onlyRange.max }}</em> &nbsp;&nbsp;(0 to 100, step 5)</span>
        </span>
      </p>
      <q-range :dark="dark" :dense="dense" v-model="onlyRange" :min="0" :max="100" :step="5" drag-only-range label/>

      <p class="caption">Readonly State</p>
      <q-range :dark="dark" :dense="dense" v-model="standalone" :min="0" :max="50" readonly/>

      <p class="caption">Disabled State</p>
      <q-range :dark="dark" :dense="dense" v-model="standalone" :min="0" :max="50" disable/>

      <p class="caption">Coloring</p>
      <q-range :dark="dark" :dense="dense" color="secondary" v-model="standalone" :min="0" :max="50" label/>
      <q-range :dark="dark" :dense="dense" color="orange" v-model="standalone" :min="0" :max="50" label/>
      <q-range :dark="dark" :dense="dense" color="dark" v-model="standalone" :min="0" :max="50" label/>

      <q-range :dark="dark" :dense="dense" color="purple" left-label-color="deep-orange" right-label-color="black" v-model="standalone" :min="0" :max="50" label-always class="q-mt-md"/>

      <p class="caption">Inside of a List</p>
      <q-list>
        <q-item>
          <q-item-section avatar>
            <q-icon name="local_atm" />
          </q-item-section>
          <q-item-section>
            <q-range :dark="dark" :dense="dense" v-model="standalone" :min="0" :max="50" label />
          </q-item-section>
        </q-item>
        <q-item>
          <q-item-section avatar>
            <q-icon name="euro_symbol" />
          </q-item-section>
          <q-item-section>
            <q-range :dark="dark" :dense="dense" v-model="standalone" :min="0" :max="50" label />
          </q-item-section>
        </q-item>
      </q-list>
    </div>
  </div>
</template>

<script>
export default {
  data () {
    return {
      dark: false,
      dense: false,

      standalone: {
        min: 10,
        max: 35
      },

      stepZero: {
        min: 34.05,
        max: 64.023
      },

      precision: {
        min: 0.2,
        max: 0.7
      },

      step: {
        min: 10,
        max: 20
      },

      label: {
        min: -12,
        max: 8
      },

      snap: {
        min: 2,
        max: 6
      },

      marker: {
        min: 6,
        max: 8
      },

      range: {
        min: 20,
        max: 65
      },

      rangeSnap: {
        min: 35,
        max: 60
      },

      onlyRange: {
        min: 10,
        max: 35
      }
    }
  },
  watch: {
    'standalone.min' (val, old) {
      console.log(`Changed [min] from ${JSON.stringify(old)} to ${JSON.stringify(val)}`)
    },
    'standalone.max' (val, old) {
      console.log(`Changed [max] from ${JSON.stringify(old)} to ${JSON.stringify(val)}`)
    },
    'range.min' (val, old) {
      console.log(`Changed [min] from ${JSON.stringify(old)} to ${JSON.stringify(val)}`)
    },
    'range.max' (val, old) {
      console.log(`Changed [max] from ${JSON.stringify(old)} to ${JSON.stringify(val)}`)
    }
  },
  methods: {
    onChange (val) {
      console.log('@change', JSON.stringify(val))
    },
    onInput (val) {
      console.log('@input', JSON.stringify(val))
    }
  }
}
</script>
