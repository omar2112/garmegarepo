# D3 Heatmap Drawer

## Overview

NOTE: D3 is required to use this API.

This is a generalized heatmap constructor that constructs an easy to edit heatmap quickly.

Define your own:
 * Color scale - Set your own range of colors or use the built in default colors
 * Axes labels - Set what the labels for both axes should be
 * Canvas size - Determine how big you want your heatmap to be
 * Margins - Define how much padding you want your heatmap to have within the canvas
 * Selector - Define the selector you want the heatmap to draw in.
 * File name - Determine where you want your data to be drawn from.


Take a look below to see what you need to get started.


## Construction


This heatmap follows the builder pattern. Which means you must create an object, set your parameters and than build it.

```javascript
var myHeatmap = Heatmap();
...
heatmap.build();
```
The final call will build and draw the heatmap on your screen.


## Available options


### Selector (Required)

Pass in a string value corresponding to the selector for the element you wish to draw in.


```javascript
heatmap.setSelector('#chart');
```

### Data file name (Required)

Pass in a string value corresponding to the file you want to pull data from.

NOTE: Currently only .tsv files are supported. Learn more about .tsv [here](https://en.wikipedia.org/wiki/Tab-separated_values)

```javascript
heatmap.setFileName('data.tsv');
```

### X-Axis Labels (Required)

Pass in an array of strings to define what the labels will look like along the top of the heatmap.

```javascript
heatmap.setXLabels(['xLabel1', 'xLabel2', 'xLabel3']);
```


### Y-Axis Labels (Required)

Pass in an array of strings to define what the labels will look like along the left side of the heatmap.

```javascript
heatmap.setYLabels(['yLabel1', 'yLabel2', 'yLabel3']);
```


### Dimensions (Required)

Pass in two integers; width than height, corresponding to pixels for which to define the size of the heatmap.


```javascript
heatmap.setDimensions(1200, 450);
```

### Fieldnames

Pass in three strings that correspond to column names for the data file to draw data from. For example:

```text
day	hr	value
1	1	0
1	2	9
2	1	4
2	2	11
3	1	5
3	2	12

```
You can think of the this as coordinates to determine where and what value the data point will be drawn.


```javascript
heatmap.setFieldNames('hr', 'day', 'value');
```
If nothing is set the following default will be applied instead;

```javascript
heatmap.setFieldNames('x', 'y', 'value');
```

NOTE: Notice that the data and labels are independant of each other. This means you can have
arbitrary numbered data and label however the data however you wish.

### Default cell color

Pass in a string hex value to set the default color of each of the cells. This only determines what color the cells will start out as.

```javascript
heatmap.setDefaultcolor("#CCCCCC");
```
If nothing is set the following default will be applied instead;

```javascript
heatmap.setDefaultcolor("#ffffff"); //White
```

### Color scale

Pass in an array of string hex values to set the color scale for the heatmap to use. This will also determine how many quantile sections there will be. The legend is automatically drawn according to this color scale as well.

```javascript
heatmap.setColors(["#C1102B", "#C5BFBC", "#CAF1E7", "#5CC9CB", "#2E707B"]);
```

If nothing is set the following default will be applied instead;

```javascript
heatmap.setColors(["#ffffd9","#edf8b1","#c7e9b4","#7fcdbb","#41b6c4","#1d91c0","#225ea8","#253494","#081d58"]);
```

## Misc

There are a few things to note in terms of behavior before you attempt to use this API.

* The width passed in determines the scaling for the chart, not the height. This means you must experiment with the height to a size that feels appropriate after creating the chart. Passing in an inappropriate height will cause the chart to be clipped.
* Data and label independance. In order to provide flexibility for the heatmap to be used however one wishes, the data and labels are decoupled. This means that if there are different number of data values for either axes than there are labels the chart will be under or over drawn. Make sure that the data and labels have the same unique values. For example;
  ```text
  day	hr	value
  1		1	0
  1		2	9
  2		1	4
  2		2	11
  3		1	5
  3		2	12
  4		1	6
  4		2	7
  ```

  ```javascript
  heatmap.setFieldNames('hr', 'day', 'value'); // x = hr, y = day, value = value
  heatmap.setXLabels(['12pm', '1pm']); //Data matches.
  heatmap.setYLabels(['Mon', 'Tue', 'Wed']); //Data mismatch. Missing 4th label. Data will still be drawn regardless and will move other parts of the chart.
  ```


## Mentions

This chart is heavily inspired by a heatmap created by Tom May which can be found [here](http://bl.ocks.org/tjdecke/5558084).

This chart was built with [D3](https://d3js.org/).
