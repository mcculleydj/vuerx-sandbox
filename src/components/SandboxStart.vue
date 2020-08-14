<template>
  <div class="box">
    <button id="start-btn">Start Timer</button>
    <h1>{{ time }}</h1>
  </div>
</template>

<script>
import { interval, fromEvent } from 'rxjs'
import { exhaustMap, map, tap } from 'rxjs/operators'

export default {
  data: () => ({
    time: '...',
  }),

  mounted() {
    const buttonElement = document.querySelector('#start-btn')
    const click$ = fromEvent(buttonElement, 'click')
    const tick$ = click$.pipe(
      exhaustMap(() => interval(1000)),
      map(i => i + 1),
      tap(i => {
        console.log(i)
      }),
    )
    tick$.subscribe(i => {
      this.time = i
    })
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
