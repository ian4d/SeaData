---
layout: post
title: "Fremont Bridge Crossing Diff"
date: 2023-12-23 14:11:13 -0800
categories: jekyll update
---



Lorem ipsum dolor sit amet, consectetur adipiscing elit. Vivamus arcu mauris, suscipit vel nibh a, dignissim tincidunt libero. Pellentesque a malesuada purus, eu vulputate quam. Duis et lectus id risus accumsan condimentum ac et diam. Mauris est nisl, iaculis a massa facilisis, viverra placerat mi. Sed eget eleifend orci, sit amet placerat enim. Etiam massa odio, pulvinar id ante non, sodales eleifend odio. Aliquam erat volutpat. Aliquam dignissim at magna quis tincidunt. Donec malesuada euismod lectus, ac tempus lacus tempus vitae.

Vivamus commodo, justo quis viverra laoreet, purus ipsum interdum erat, nec pellentesque massa augue et tellus. Duis nec lacus sed eros rutrum facilisis. Quisque imperdiet leo id velit congue egestas. Duis ac leo scelerisque, pellentesque mauris nec, finibus massa. Nullam neque justo, malesuada non malesuada et, suscipit at augue. Integer ac euismod nunc, sed finibus neque. Pellentesque habitant morbi tristique senectus et netus et malesuada fames ac turpis egestas. Nullam tincidunt ante vel neque vestibulum aliquet. Vivamus mauris nunc, congue sit amet fermentum vitae, fermentum a odio. Praesent vestibulum aliquet fermentum. Duis in accumsan nibh, congue commodo libero. Aliquam porta pretium massa, id vulputate ante maximus a. Curabitur sodales augue leo, quis vehicula mi pretium id. Fusce porta odio vel magna vestibulum, sit amet scelerisque magna egestas.

<div id="plot-holder" class="plot-holder">
  <div id="container" class="graph-wide"></div>
</div>

<!-- <div id="container" class="graph-wide"></div>
<script src="https://cdn.jsdelivr.net/npm/d3@7"></script>
<script src="https://cdn.jsdelivr.net/npm/@observablehq/plot@0.6"></script> -->
<script type="module">

  var xhr = new XMLHttpRequest();
  // App Key ID: fkv02qvh5ggcnx00bnc1ict
  // SECRET: 69jmq1yzuvtma2e2angsj50fa36keo3j1w14pix7x7icth6cch
  xhr.open('GET', 'https://data.seattle.gov/resource/65db-xm6k.json');
  // xhr.withCredentials = true;
  xhr.setRequestHeader("Content-Type", "application/json");
  // xhr.setRequestHeader("Authorization", "Basic " + btoa("fkv02qvh5ggcnx00bnc1ict:69jmq1yzuvtma2e2angsj50fa36keo3j1w14pix7x7icth6cch")); 
  xhr.onload = function () {
    if (xhr.status === 200) {

      const plotContainer = document.querySelector("#container");


      let roadData = JSON.parse(xhr.response);
      roadData.splice(0, roadData.length - 24);

      console.log(`road data: ${roadData}`);
      roadData = roadData.map((row, index) => {
        let newData = {
          date: new Date(Date.parse(row.date)),
          nb: parseInt(row['fremont_bridge_nb']),
          sb: parseInt(row['fremont_bridge_sb']),
          total: parseInt(row['fremont_bridge'])
        };
        console.log(`index: ${index}, data: ${newData}`);
        return newData;
      });
      console.log(`road data: ${roadData}`);

      let plot = Plot.plot({
        title: 'Fremont Bridge Crossings',
        caption: 'Crossings broken down by which side of the bridge they occurred on.',
        y: {
          grid: true,
        },
        color: { scheme: "RdYlBu", legend: true },
        marks: [
          Plot.differenceY(
            roadData,
            {
              x: "date",
              y1: 'nb',
              y2: 'sb',
              positiveFill: () => 'West Side Crossings',
              negativeFill: () => 'East Side Crossings',
              curve: 'step',
              // tip: true,
            }),
          Plot.lineY(
            roadData,
            {
              x: 'date',
              y: 'total',
              color: {
                legend: true
              },
              curve: 'natural'
            }
          ),
          Plot.frame(),
        ],
        marginTop: 50,
        marginLeft: 20,
        marginRight: 20,
        marginBottom: 50,
        width: plotContainer.offsetWidth,
        height: 500
      });
      plotContainer.append(plot);

      console.log("DONE!");

    }
    else {
      console.log('Request failed.  Returned status of ' + xhr.status);
    }
  };
  xhr.send();

</script>



Cras sit amet suscipit lacus. Praesent blandit nibh et convallis pretium. Nunc nibh nibh, fermentum a justo ac, semper dapibus ipsum. Donec ac ex congue orci commodo ultrices. Aenean ornare, elit eget pellentesque suscipit, leo urna venenatis nunc, quis ultrices ipsum metus quis tellus. Aenean vel sem euismod, laoreet justo sit amet, vehicula est. Quisque magna dui, hendrerit vitae mollis vel, dictum vel sem. Sed ornare sapien at tristique consequat. Aenean mollis ante ut sollicitudin congue. Praesent suscipit pulvinar felis, lacinia placerat quam.

Vestibulum nibh dui, vestibulum ut quam sed, molestie porttitor tellus. Aenean a ipsum ac nisi dignissim efficitur. Fusce nec turpis eu metus hendrerit vehicula quis vitae magna. Nulla ut erat vulputate sem tempus suscipit quis id dui. Nulla feugiat pulvinar libero, eu interdum eros fermentum nec. Donec sodales sit amet lorem nec dictum. Sed et ante sapien. Vestibulum a ex sed metus ullamcorper pellentesque. Nullam vitae tellus est. Phasellus ornare lobortis sem a tincidunt. Nullam gravida risus quis varius porta.

Nam at eleifend purus. Suspendisse in neque ut est dictum fermentum. Nunc tincidunt a mi suscipit sodales. Sed semper, lacus ac condimentum cursus, eros ex consectetur lacus, eu dictum velit nisl nec elit. Praesent ultricies, turpis vitae mollis ultrices, orci odio auctor mi, quis cursus nulla ligula et justo. Aenean sit amet enim ut tortor vehicula dignissim eu non nisi. Morbi congue fermentum nulla id mattis.