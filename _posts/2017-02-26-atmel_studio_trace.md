---
layout: post
category: "RTOS"
title: "Atmel Studio中 percepio trace使用方法"
tags: ["RTOS"]
---

<a name="top"></a>
### Usage of Percepio Trace



1. Do settings

	* Project > properties(alt+F7) > Tool > interface > SWD (not JTAG)

	* Debug > percepio trace > trace settings  
	here the Frequency is the freq of your MCU clock.  

	![trace setting](http://7xifyp.com1.z0.glb.clouddn.com/traceSetting.JPG){: .center-image}  

	* Debug > percepio trace > enable trace  

2. Do some test

	Start debuging and make sure Trace was enabled.

	![trace_enable](http://7xifyp.com1.z0.glb.clouddn.com/trace_enable.png){: .max-height-image}

	when the Debug started the Trace bar will look like below and were selectable.

	![trace_started](http://7xifyp.com1.z0.glb.clouddn.com/trace_started.png){: .max-height-image}

	The Profiling contains sampling functions.

	![trace_profiling](http://7xifyp.com1.z0.glb.clouddn.com/trace_profiling.png){: .max-height-image}

	* `Profiling`  
	Then let us set a breakpoint and the chart of sampling and Control-Flow will be showen  
	It shows the time of each function taken.

	![trace_PC](http://7xifyp.com1.z0.glb.clouddn.com/trace_PC.png){: .max-height-image}

	* `Control-Flow`

	![trace_Flow](http://7xifyp.com1.z0.glb.clouddn.com/trace_Flow.png){: .max-height-image}

	* `Data Plot`  
	Next let us look at Data Plot.  
	In the code page select a variable and right click check `add data plot`  
	and start Debug the Data Plot will show the figure of the variable.  

	![http://7xifyp.com1.z0.glb.clouddn.com/trace_DataPlot.png](http://7xifyp.com1.z0.glb.clouddn.com/trace_DataPlot.png){: .max-height-image}

	Here the Data Plot just can show the 1D variable, I'm looking for method to plot 1D array variable.  
	If you know, please leave message to me.  
	Thank you.


#### *Reference:*  

1. [Atmel Studio Integrated Development Environment With FreeRTOS Awareness](http://www.freertos.org/FreeRTOS-Plus/BSP_Solutions/Atmel/atmel_studio.html)  
2. [Debugging on Atmel Studio with Percepio Trace-youtube](https://www.youtube.com/watch?v=iioeeViKrsc)  

- - - 

### [TOP](#top)
