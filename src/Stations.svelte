<g>
  <!-- r={$selectedStations.includes(station['short-name']) ? 4 : 2} -->
  {#each stations as station}
    <circle
      r={station.type.toLowerCase().indexOf('megastation') > -1 ? 4 : station.type.toLowerCase().indexOf('knooppunt') > -1 ? 3 : 2}
      cx={x(station.lon)}
      cy={y(station.lat)}
      style="fill: {$selectedStations.includes(station['short-name']) ? 'red' : 'white'}; stroke: {$selectedStations.includes(station['short-name']) ? 'orange' : 'black'}; stroke-width: 2;"
      on:mouseover="console.log(station)"
      on:click="setSelectedStation(station)"
    />
    <!-- <text
      x={x(station.lon)}
      y={y(station.lat)}
      dy="-5"
      style="font-size: 8px; text-anchor: middle; fill: black; stroke: black; stroke-width: 1;"
    >{station['full-name']}</text>
    <text
      x={x(station.lon)}
      y={y(station.lat)}
      dy="-5"
      style="font-size: 8px; text-anchor: middle; fill: white;"
    >{station['full-name']}</text> -->
  {/each}
</g>

<script>
  

  export default {
    namespace: 'svg',
    methods: {
      setSelectedStation(station) {
        // this.store.set({ selectedStations: [station['short-name']] })
        const old = this.store.get().selectedStations

        this.store.set({
          selectedStations: old.includes(station['short-name']) ? old.filter(d => d !== station['short-name']) : old.concat([station['short-name']])
        })
      }
    }
  }
</script>