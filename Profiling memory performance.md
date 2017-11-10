 ---
title: Fix Memory Problems
description: DevTools to find memory issues that affect page performance
created:  2017 Nov 10
modified: 
 
 
 
 **DevTools to find memory issues that affect page performance**

    Memory issues are important because they are often perceivable by users. Users can perceive memory issues in the following ways:

*************************************A page's performance gets progressively worse over time********************************************
This is possibly a symptom of a memory leak.
A memory leak is when a bug in the page causes the page to progressively use more and more memory over time.

*****************************************A page's performance is consistently bad********************************************************
This is possibly a symptom of memory bloat.
Memory bloat is when a page uses more memory than is necessary for optimal page speed.
A page's performance is delayed or appears to pause frequently. This is possibly a symptom of frequent garbage collections. 
Garbage collection is when the browser reclaims memory.
The browser decides when this happens. During collections, all script execution is paused. So if the browser is garbage collecting a lot, 
script execution is going to get paused a lot.

**************************************Page's performance is delayed or appears to pause frequently***************************************
 This is possibly a symptom of frequent garbage collections.
 Garbage collection is when the browser reclaims memory. 
 The browser decides when this happens. During collections, all script execution is paused. 
 So if the browser is garbage collecting a lot, script execution is going to get paused a lot.
 

Monitor memory use in realtime with the Chrome Task Manager:-

Use the Chrome Task Manager as a starting point to your memory issue investigation. 
The Task Manager is a realtime monitor that tells you how much memory a page is currently using.

Press Shift+Esc or go to the Chrome main menu and select More tools > Task manager to open the Task Manager.

![alt tag](https://developers.google.com/web/tools/chrome-devtools/memory-problems/imgs/task-manager.png)








![alt tag](https://developers.google.com/web/tools/chrome-devtools/memory-problems/imgs/js-memory.png)

These two columns tell you different things about how your page is using memory:

The Memory column : -
Represents native memory. DOM nodes are stored in native memory. If this value is increasing, DOM nodes are getting created.
The JavaScript Memory column represents the JS heap. This column contains two values.
The value you're interested in is the live number (the number in parentheses). 
The live number represents how much memory the reachable objects on your page are using. 
If this number is increasing, either new objects are being created, or the existing objects are growing.

.Visualize memory leaks with Timeline recordings
You can also use the Timeline panel as another starting point in your investigation. 
The Timeline panel helps you visualize a page's memory use over time.
Open the Timeline panel on DevTools.
Enable the Memory checkbox.
Tip: It's a good practice to start and end your recording with a forced garbage collection. 
Click the collect garbage button (force garbage collection button) while recording to force garbage collection.

![alt tag](https://developers.google.com/web/tools/chrome-devtools/memory-problems/imgs/simple-growth.png)
![alt tag](https://developers.google.com/web/tools/chrome-devtools/memory-problems/imgs/simple-growth.png)
 
 an explanation of the user interface. 
 The HEAP graph in the Overview pane (below NET) represents the JS heap.
 Below the Overview pane is the Counter pane. Here you can see memory usage broken down by JS heap 
 (same as HEAP graph in the Overview pane), documents, DOM nodes, 
 listeners, and GPU memory. Disabling a checkbox hides it from the graph.

Discover detached DOM tree memory leaks with Heap Snapshots
A DOM node can only be garbage collected when there are no references to it from either the page's DOM tree or JavaScript code.
A node is said to be "detached" when it's removed from the DOM tree but some JavaScript still references it. 
Detached DOM nodes are a common cause of memory leaks.
This section teaches you how to use DevTools' heap profilers to identify detached nodes.

To create a snapshot, open DevTools and go to the Profiles panel, select the Take Heap Snapshot radio button, 
and then press the Take Snapshot button.

![alt tag](https://developers.google.com/web/tools/chrome-devtools/memory-problems/imgs/take-heap-snapshot.png)
Type Detached in the Class filter textbox to search for detached DOM trees.

![alt tag](https://developers.google.com/web/tools/chrome-devtools/memory-problems/imgs/detached-filter.png)

Type Detached in the Class filter textbox to search for detached DOM trees.

![alt tag](https://developers.google.com/web/tools/chrome-devtools/memory-problems/imgs/expanded-detached.png)

Expand the carats to investigate a detached tree:
![alt tag](https://developers.google.com/web/tools/chrome-devtools/memory-problems/imgs/expanded-detached.png)

Nodes highlighted yellow have direct references to them from the JavaScript code.
Nodes highlighted red do not have direct references. 
They are only alive because they are part of the yellow node's tree. 
In general, you want to focus on the yellow nodes. Fix your code so that the yellow node isn't alive for longer than it needs to be,
and you also get rid of the red nodes that are part of the yellow node's tree.

![alt tag](https://developers.google.com/web/tools/chrome-devtools/memory-problems/imgs/yellow-node.png)
