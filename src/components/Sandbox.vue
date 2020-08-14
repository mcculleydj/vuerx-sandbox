<template>
  <div class="box">
    <button id="start-btn" v-stream:click="click$">Start Timer</button>
    <h1>{{ tick$ || '...' }}</h1>
  </div>
</template>

<script>
import { interval } from 'rxjs'
import { exhaustMap, map, tap, share } from 'rxjs/operators'

const sharedTick$ = interval(1000).pipe(share())

sharedTick$.subscribe(i => console.log('sub1', i))

setTimeout(() => {
  sharedTick$.subscribe(i => console.log('sub2', i))
}, 3000)

export default {
  domStreams: ['click$'],

  subscriptions() {
    const tick$ = this.click$.pipe(
      exhaustMap(() => interval(1000)),
      map(i => i + 1),
      tap(i => {
        console.log(i)
      }),
    )

    return {
      tick$,
    }
  },
}
</script>

<style scoped>
h1 {
  text-align: center;
}

.box {
  margin-top: 10px;
  padding: 10px;
  width: 100px;
  border: 3px black solid;
}
</style>
