<head>
               <script src="https://cdn.plot.ly/plotly-latest.min.js"></script>
</head>
<div id="tester" style="width:600px;height:250px;"></div>
<div id="myDiv" style="width:600px;height:250px;"></div>
<div id="myDiv1"></div>
<script>
	TESTER = document.getElementById('tester');
	Plotly.newPlot( TESTER, [{
	x: [1, 2, 3, 4, 5],
	y: [1, 2, 4, 8, 16] }], {
	margin: { t: 0 } } );
</script>

<script>
var data = [{
  type: "choroplethmapbox", locations: ["NY", "MA", "VT"], z: [-50, -10, -20],
  geojson: "https://raw.githubusercontent.com/python-visualization/folium/master/examples/data/us-states.json"
}];

var layout = {mapbox: {center: {lon: -74, lat: 43}, zoom: 3.5},
              width: 600, height:400};

var config = {mapboxAccessToken: "pk.eyJ1IjoiZmxvYnJlY2h0IiwiYSI6ImNrODRoaHI0bzE5bWYzdG1zMTZ4NmYxZTUifQ.vrpEIGfPE92RFKgQnYbPxA"};

Plotly.newPlot('myDiv', data, layout, config);
</script>

<script>
Plotly.d3.csv("https://raw.githubusercontent.com/plotly/datasets/master/gapminder_with_codes.csv", function(err, rows){

  function filter_and_unpack(rows, key, year) {
  return rows.filter(row => row['year'] == year).map(row => row[key])
  }

  var frames = []
  var slider_steps = []

  var n = 11;
  var num = 1952;
  for (var i = 0; i <= n; i++) {
    var z = filter_and_unpack(rows, 'lifeExp', num)
    var locations = filter_and_unpack(rows, 'iso_alpha', num)
    frames[i] = {data: [{z: z, locations: locations, text: locations}], name: num}
    slider_steps.push ({
        label: num.toString(),
        method: "animate",
        args: [[num], {
            mode: "immediate",
            transition: {duration: 300},
            frame: {duration: 300}
          }
        ]
      })
    num = num + 5
  }

var data = [{
      type: 'choropleth',
      locationmode: 'world',
      locations: frames[0].data[0].locations,
      z: frames[0].data[0].z,
      text: frames[0].data[0].locations,
      zauto: false,
      zmin: 30,
      zmax: 90

}];
var layout = {
    title: 'World Life Expectency<br>1952 - 2007',
    geo:{
       scope: 'world',
       countrycolor: 'rgb(255, 255, 255)',
       showland: true,
       landcolor: 'rgb(217, 217, 217)',
       showlakes: true,
       lakecolor: 'rgb(255, 255, 255)',
       subunitcolor: 'rgb(255, 255, 255)',
       lonaxis: {},
       lataxis: {}
    },
    updatemenus: [{
      x: 0.1,
      y: 0,
      yanchor: "top",
      xanchor: "right",
      showactive: false,
      direction: "left",
      type: "buttons",
      pad: {"t": 87, "r": 10},
      buttons: [{
        method: "animate",
        args: [null, {
          fromcurrent: true,
          transition: {
            duration: 200,
          },
          frame: {
            duration: 500
          }
        }],
        label: "Play"
      }, {
        method: "animate",
        args: [
          [null],
          {
            mode: "immediate",
            transition: {
              duration: 0
            },
            frame: {
              duration: 0
            }
          }
        ],
        label: "Pause"
      }]
    }],
    sliders: [{
      active: 0,
      steps: slider_steps,
      x: 0.1,
      len: 0.9,
      xanchor: "left",
      y: 0,
      yanchor: "top",
      pad: {t: 50, b: 10},
      currentvalue: {
        visible: true,
        prefix: "Year:",
        xanchor: "right",
        font: {
          size: 20,
          color: "#666"
        }
      },
      transition: {
        duration: 300,
        easing: "cubic-in-out"
      }
    }]
};

Plotly.newPlot('myDiv1', data, layout).then(function() {
    Plotly.addFrames('myDiv1', frames);
  });
})

</script>
## Welcome to GitHub Pages

You can use the [editor on GitHub](https://github.com/flobrec/plotly/edit/master/README.md) to maintain and preview the content for your website in Markdown files.

Whenever you commit to this repository, GitHub Pages will run [Jekyll](https://jekyllrb.com/) to rebuild the pages in your site, from the content in your Markdown files.

### Markdown

Markdown is a lightweight and easy-to-use syntax for styling your writing. It includes conventions for

```markdown
Syntax highlighted code block

# Header 1
## Header 2
### Header 3

- Bulleted
- List

1. Numbered
2. List

**Bold** and _Italic_ and `Code` text

[Link](url) and ![Image](src)
```

For more details see [GitHub Flavored Markdown](https://guides.github.com/features/mastering-markdown/).

### Jekyll Themes

Your Pages site will use the layout and styles from the Jekyll theme you have selected in your [repository settings](https://github.com/flobrec/plotly/settings). The name of this theme is saved in the Jekyll `_config.yml` configuration file.

### Support or Contact

Having trouble with Pages? Check out our [documentation](https://help.github.com/categories/github-pages-basics/) or [contact support](https://github.com/contact) and we’ll help you sort it out.
