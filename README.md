# meteorite-visualization

This is a tutorial to display a list of meteorite landings on a globe visualization! This is a geospatial visualization. This project uses the NASA dataset found here: https://data.nasa.gov/widgets/gh4g-9sfh

## Method

### PART 1: GLOBE SETUP
1. Open "Visual Studio Code" or another text editor. We are coding from scratch!
2. Create index.html
3. `Code <!DOCTYPE html>`, `<html>...</html>` with head and body tags
4. Add `<title>Meteor Visualization</title>` to the head tag
5. Include `<script src="//unpkg.com/globe.gl"></script>` in the head tag
6. Add `<div id="globe"></div>` to the body tag
7. Let's go back to the head. Add the following to the head tag:
   ```html
<style>
  body {
    margin: 0;
  }
</style>
### PART 2: CODE
```html
<script>
// 1. Create and configure the globe object
const globe = new Globe()
  .globeImageUrl("//unpkg.com/three-globe/example/img/earth-night.jpg")
  .backgroundImageUrl("//unpkg.com/three-globe/example/img/night-sky.png")
  .pointAltitude("altitude")
  .pointColor("color")
  .pointLabel("label")
  .pointRadius("radius")
  .pointResolution(24)(document.querySelector("#globe"));

// 2. Get NASA meteorite landings data
fetch("https://data.nasa.gov/resource/y77d-th95.json")
  .then((res) => res.json())
  .then((json) => {
    // 3. Filter out meteorites without coordinates
    let data = json.filter((d) => Number(d.reclat));

    // 4. Sort meteriotes by mass
    data.sort((a, b) => b.mass - a.mass);

    // 5. Choose the largest 2,000 meteorites
    data = data.slice(0, 2000);

    // 6. Format data
    const globeData = data.map((d) => ({
      lat: d.reclat,
      lng: d.reclong,
      radius: 0.02 * d.mass ** 0.333,
      altitude: 0.5 / d.mass ** 0.333,
      color: Math.random() * 16777216,
      label: `
      <div class="tooltip">
        <b>${d.name} ${d.id}</b>
        <div>Mass: ${(+d.mass).toLocaleString()} g</div>
        <div>Year: ${d.year.split("-")[0]}</div>
        <div>Class: ${d.recclass}</div>
      </div>`,
    }));

    // 7. Populate globe with data
    globe.pointsData(globeData);
  });
</script>
```

You can replace /img/earth-night.jpg with `earth-day` or `earth-blue-marble`

### PART 3 ADD THE FINAL CSS AND WE'RE DONE!

Add this CSS code to your `<style>` tag in the head tag. 
```css
    .tooltip {
        border: 1px solid dimgray;
        background-color: cornsilk;
        color: midnightblue;
        padding: 5px;
        border-radius: 2px;
      }
```

