# LogicleTransform

## MATLAB class to apply the logicle transformation to a matrix and provide axes labels.

To apply the logicle transform, the parameters of the transformation must first be set. There are four parameters:

* T = "top of scale" value
* W = number of approximately linear decades
* M = number of approximately logarithmic decades
* A = number of additional decades of negative data values to be included

These parameters are specified when creating a new LogicleTransform object:

`obj = LogicleTransform(T,W,M,A)`  
`obj = LogicleTransform(T,W,M,A,n_bins);`

The optional n_bins parameter specifies the number of bins to be included in the fast logicle transform algorithm. When this parameter is specified, the fast logicle transform is used.

The object stores internal variables for later calculations based on data. In this way, the object guides the calculation of many data points efficiently.

Once the object is created, the data can be tranformed as follows:

`transformed_data = obj.transform(data);`

The inverse operation can be carried out as follows:

`data = obj.inverse(transformed_data);`

The variable data can be a matrix of any number of dimensions. The logicle_transform function calculates the transformed value of each element in turn, and returns a matrix of the same dimention as the input.

Axes ticks amd labels can be set by acessing the Tick and TickLabel properties of the LogicleTransform object.

---
## Example

`obj = LogicleTransform(10000,2,4,0);`  
`x = linspace(obj.inverse(0),obj.T,1000);`  
`y = obj.transform(x);`  
`plot(x,y);`  
`ax = gca;`  
`ax.YTick = obj.Tick;`  
`ax.YTickLabel = obj.TickLabel;`

---
Algorithms were developed by:  
Moore WA, Parks DR. Update for the Logicle Data Scale Including Operational Code Implementations. Cytometry Part A : the journal of the International Society for Analytical Cytology. 2012;81(4):273-277. doi:10.1002/cyto.a.22030.

Here's a [link to the paper](http://www.ncbi.nlm.nih.gov/pmc/articles/PMC4761345/).
