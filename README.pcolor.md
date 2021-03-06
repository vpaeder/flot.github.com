## 2D pseudo-color plot plugin for Flot ##
This plugin takes a 2D array and maps the values to a defined color map.
## Basic usage ##
When creating a Flot chart, simply add the *pcolor* tag to the series definition, like this:
```
var my_plot = $.plot($("#plot_container"), [data], series:{pcolor:{ active:true, show:true, colormap: my_colormap, scalebar: scalebar_options }});
```

## Data format ##
The pcolor plugin expects that the data is composed of 3 arrays, one for the horizontal coordinates, one for the vertical coordinates, and one for the values:
```
data = [x coordinates <1D or 2D array>, y coordinates <1D or 2D array>, values <2D array>]
```
The coordinate arrays can be either 1D or 2D.

## Data range ##
The minima and maxima in x and y directions are accessible in this way:
```
var x_min = my_plot.getAxes().xaxis.datamin
var x_max = my_plot.getAxes().xaxis.datamax
var y_min = my_plot.getAxes().yaxis.datamin
var y_max = my_plot.getAxes().yaxis.datamax
```
The displayed range can be adjusted in this way:
```
my_plot.getAxes().xaxis.options.min = new_x_min;
my_plot.getAxes().xaxis.options.max = new_x_max;
my_plot.getAxes().yaxis.options.min = new_y_min;
my_plot.getAxes().yaxis.options.max = new_y_max;
```

## Color map ##
The colormap is an array defining a linear gradient. Each element of the array must be [color position, color code].
For example, a blue/white/red gradient would be defined as:
```
var colormap_bwr = [[0,"#0000ff"],[0.5,"#ffffff"],[1,"#ff0000"]];
```
Another popular color map is the *jet* color map:
```
var colormap_jet = [ [0,"#00007f"], [0.125,"#0000ff"], [0.25,"#007fff"], [0.375,"#00ffff"],
[0.5,"#7fff7f"], [0.625,"#ffff00"], [0.75,"#ff7f00"], [0.875,"#ff0000"], [1.0,"#7f0000"] ];
```

## Scale bar ##
By default, a scale bar showing the extent of the represented colours appears in the top right corner of the plot. The scale bar options are:
```
scalebar_options = {
	location:"top right" // combination of top, left, right and bottom
	orientation:"vertical" // horizontal or vertical
	width:100,
	height:15,
	fontsize:"9px",
	fontfamily:"times",
	labels:3, // number of labels, >1 to display any
	labelformat:"1f",
	labelformatter: function(value,precision){ return "text"; },
	textalign:"right"
}
```
The label format number represents the truncation precision and the letter the JavaScript function used to format the numbers: *f* = toFixed, *p* = toPrecision, *e* = toExponential, *c* = custom function provided in the *labelformatter* option.
The label alignment, set by the ```textalign``` property, can be *left*, *center*, *right*, or *spread*. The last option, when the bar is horizontally oriented, spreads the labels across the whole scale bar width.
The scale bar is deactivated by settings ```scalebar_options = null```.

## Grid ##
The grid can be displayed by setting ```grid: {aboveData:true}``` in Flot options. Note that it will display above the color bar.
Another option exists, which requires to expose the *drawGrid* function of Flot. If you did so, you can add ```grid:true``` to *pcolor* options. The grid will be drawn above the plot but below the scale bar.

## Performances and compatibility ##
The pcolor plugin has been tested to work on Safari, Chrome and Firefox under Mac OS X. The behaviour in terms of performance was similar.

## Example ##
See included file example.pcolor.html
