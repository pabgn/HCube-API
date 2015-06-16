# HCube API

HCube comes with a RESTful API for accessing every led on the matrix with a comprenhensive JSON structure which defines every LED in the 3D cube. 

Endpoints
---------

##### /leds: changes color for every LED
Parameters:
> key: API user key

>data: Multidimensional array defining colors for every led.

### data structure
Every led has a definite index depending on its position in the cube. In the following image you can check how X, Y, Z have been arranged in space:

![alt text](http://i.imgur.com/NvOLAko.png
 "Structure")

So, for turning on the very first led with a red color, you will have to access LED at index 0,0,0 and send an array containing [255,0,0] (RGB for red).

Remember /leds endpoint expects the structure for the whole cube, so you will have to send the complete matrix on every request.

###### Example of data structure:

![alt text](http://i.imgur.com/kFUYOxr.png
 "Structure")
 
 #### Example of request in JavaScript
 ###### Final structure containing color for every led
 
 ```
    final = [];
    for(x=0;x<20;x++){ 
		final[x] = new Array(); 
		for(y=0;y<20;y++){ 
		    final[x][y]= new Array(); 
			for(z=0;z<20;z++){ 
				red =Math.floor(Math.random() * 256);
				green = Math.floor(Math.random() * 256);
				blue = Math.floor(Math.random() * 256);
            	d = [red, green, blue];
				final[x][y][z]=d; 
			}
	    } 
	}

```
 ###### Send request
```
$.ajax
    ({
	    type: "POST",
		url: 'http://'+url+'/api/leds/',
		dataType: 'json',
		data: JSON.stringify({'data':final, 'key':key}),
		success: function () {}
	        alert("Yuju!");
	    })
	});
```
