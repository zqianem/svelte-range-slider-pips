<script>
  import RangeSlider from "../../src/RangeSlider.svelte";
  const num = new Intl.NumberFormat("en-US");
  const numzh = new Intl.NumberFormat("zh-Hans-CN-u-nu-hanidec");
  let values = [20, 40, 60, 80];
  let day = [3];
  let hue = [244];
  let dynamic = [0,50];
  let pushy = [30,60]
  const formatter = v => {
    return num.format(v);
  };
  const days = [
    "Monday",
    "Tuesday",
    "Wednesday",
    "Thursday",
    "Friday",
    "Saturday",
    "Happy Days"
  ];
  const dayFormat = v => days[v];
  const dayFormatCn = v => {
    if (v === 6) {
      return "星期日";
    }
    return "星期" + numzh.format(v + 1);
  };
  $: lightColor = `hsl(${Math.round(hue[0]) - 10}, 65%, 70%)`;
  $: color = `hsl(${Math.round(hue[0])}, 63%, 54%)`;
</script>

<svelte:head>
<style>
  #test-id {
    --range-slider: rgb(245, 200, 230);
    --range-handle: var(--range-slider);
    --range-handle-inactive: var(--range-slider);
    --range-handle-focus: rgb(245, 0, 46);
  }
  #clr-test {
    --range-slider: rgb(195, 228, 222);
    --range-handle-inactive: rgb(81, 185, 180);
    --range-handle: rgb(81, 185, 180);
    --range-handle-focus: rgb(35, 241, 214);
    --range-float-text: darkcyan;
    --pip: #eee;
    --pip-text: #aaa;
    --pip-active: black;
    --pip-active-text: darkcyan;
  }
</style>
</svelte:head>

<main>
	
  <div class="content" style="--range-handle-focus: {color}; --range-handle: {lightColor}">

    <RangeSlider vertical range values={[10,30]} pips all="label" />
    <RangeSlider vertical range="min" values={[10]} pips all />
    <RangeSlider vertical range="max" values={[30]} pips />
    <br>
    <RangeSlider id="test-id" />
    <RangeSlider bind:values />{values}
    <RangeSlider float />
    <RangeSlider float pips all="label" />
    <RangeSlider float pips first="label" last="label" />
    <RangeSlider float pips first="label" last="label" rest="label" />
    <br>
    <RangeSlider range bind:values={pushy} float />
    <RangeSlider range pushy bind:values={pushy} pips all="label" float />
    <RangeSlider range="min" values={[65]} pips all="label" float />
    <RangeSlider range="max" values={[35]} pips all="label" float />
    <br>
    <RangeSlider float pips step={10} pipstep={1} />
    <RangeSlider float pips step={10} pipstep={2} />
    <RangeSlider float pips step={0.1} min={dynamic[0]} max={dynamic[1]} />
    <br>
    <RangeSlider float pips first="label" last="label" rest pipstep={1} bind:values={dynamic} range />
    <RangeSlider prefix="$" range values={[20,80]} float pips first="label" last="label" />
    <RangeSlider id="clr-test" prefix="~" suffix="m²" {formatter} range values={[100,3000]} min={100} max={3000} step={50} float pips first="label" last="label" />
    <RangeSlider handleFormatter={()=>"O²"} formatter={(v)=>`${v}% O²`} step={1} float pips first="label" last="label" hover={false} />
    <br>
    <RangeSlider bind:values={day} min={0} max={6} formatter={dayFormat} float pips first="label" last="label" rest="label" />
    <RangeSlider bind:values={day} min={0} max={6} formatter={dayFormatCn} float pips first="label" last="label" rest="label" />
    <br>
    <br>{dayFormatCn(day[0])} | {dayFormat(day[0])}<br>
    <br>
    <RangeSlider bind:values={hue} max={360} range="min" float formatter={(v)=>color} />
  </div>


</main>

<style>
  :global(body,html) {
    padding: 0;
    margin: 0;
  }
  main {
    font-family: sans-serif;
    text-align: center;
    padding: 15px;
  }
  @media screen and ( min-width: 600px ) {
    main {
      padding: 50px;
    }
  }
</style>