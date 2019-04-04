# The Scenario
You have run a temperature simulation of a 3D room that has 4 heat sources. You are given the temperature data from the simulation at each node in a 3D grid. 5ou will be creating several visualizations (in Projects 2, 3, 4, and 5) 5o understand the distribution of temperatures within the 3D room.
  
# Requirements:
Put this project number and your name in the title bar.  
The coordinate range of the data volume is: -1.0 ≤ x,y,z ≤ 1.0  
The number of data points you place within this region will be up to you.  

For the temperature range of the data, use: 0.0 ≤ t ≤ 100.0  
The temperatures defined by the equation actually go higher than 100 degrees in places, but don't worry about it. After computing t, you can just clamp it to 100.:

```cpp
const float TEMPMIN = {   0.f };
const float TEMPMAX = { 100.f };
. . .
if( t > TEMPMAX )
	t = TEMPMAX;
```
Display the temperature data as a point cloud. The number of data points to use is up to you:  
```cpp
#define NX	???
#define NY	???
#define NZ	???
```
Color the dot using grayscale -- a low intensity for a low temperature and a high intensity for a high temperature. Don't go all the way to black -- you won't be able to see your lowest temperature points.
```cpp
const float GRAYMIN = { 0.20f };
const float GRAYMAX = { 1.00f };
. . .
if( t > TEMPMAX )
	t = TEMPMAX;
float gray = GRAYMIN + ( GRAYMAX - GRAYMIN ) * ( t - TEMPMIN ) / ( TEMPMAX - TEMPMIN );
glColor3f( gray, gray, gray );		// r = g = b gives gray
```

# Getting the Temperature Data  
I am going to let you "cheat" on the scalar data. Instead of reading it from a file as would normally be done, compute a scalar temperature value at each node point in each plane according according to a function included in your sample.cpp code called Temperature( x, y, z ); Pass in the x, y, z of where your node is located and it will pass back the temperature there.  
Setting up the Data in your Program  
If you are comfortable with structures, a 3D array of structures is a good way to store and access the data for this project:  
```cpp
struct node
{
        float x, y, z;          // location
        float t;                // temperature
	float rgb[3];		// the assigned color (to be used later)
        float rad;              // radius (to be used later)
        float grad;             // total gradient (to be used later)
};

struct node  Nodes[NX][NY][NZ];
```
If you are not comfortable with C structures, a 3D array for X, a 3D array for Y, etc. will work too.  
The InitGraphics( ) function is a good place to set all these values. Fill the (x,y,z) components of each structure in the 3D array, and use those (x,y,z) to compute a temperature.
