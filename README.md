Download Link: https://assignmentchef.com/product/solved-embsys110-assignment-3-led-hsm
<br>
The goal of this assignment is to implement an LED pattern generator using HSM (Hierarchical State Machine). This approach allows the source code (implementation) to be directly traceable to the statechart (design) which can in turn be traced back to the requirements (specifications).

See Session 2.1. Model-Based Software Development of the following publication:

<em>Automatic code generation for instrument flight software. Kiri L. Wagstaff, Edward Benowitz, Dj Byrne, Ken Peters, Garth Watney. Jet Propulsion Laboratory, National Aeronautics and Space Administration, 2007. </em>

<a href="http://citeseerx.ist.psu.edu/viewdoc/download?doi=10.1.1.126.548&amp;rep=rep1&amp;type=pdf">(</a><a href="http://citeseerx.ist.psu.edu/viewdoc/download?doi=10.1.1.126.548&amp;rep=rep1&amp;type=pdf">http://citeseerx.ist.psu.edu/viewdoc/download?doi=10.1.1.126.548&amp;rep=rep1&amp;type=pdf</a><a href="http://citeseerx.ist.psu.edu/viewdoc/download?doi=10.1.1.126.548&amp;rep=rep1&amp;type=pdf">)</a>

<h1>2         Setup</h1>

<ol>

 <li><em>Carefully</em> unplug any extension modules from your Nucleo board. They are not required and may hinder your view of the USER LED. Besides, the USER LED pin (PA.5) is shared with the SPI CLK pin of the LCD module, and therefore they cannot be used together.</li>

 <li>Download the compressed project file (platform-stm32f401-nucleo_assignment3.tgz) from the Assignment 3 course site.</li>

</ol>

Place the downloaded tgz file in your VM under <strong>~/Projects/stm32</strong>.

<ol start="3">

 <li>Move your existing project folder to a backup folder, e.g.</li>

</ol>

mv platform-stm32f401-nucleo platform-stm32f401-nucleo.bak

Note – You may want to pick another backup folder name if the one shown above already exists.

<ol start="4">

 <li>Decompress the tgz file with:</li>

</ol>

tar xvzf platform-stm32f401-nucleo_assignment3.tgz

The project folder will be expanded to <strong>~/Projects/stm32/platform-stm32f401-nucleo</strong>.

<ol start="5">

 <li>Launch Eclipse. Hit F5 to refresh the project content.</li>

</ol>

Or you can right-click on the project in Project Explorer and then click “Refresh”.

<ol start="6">

 <li>Clean and rebuild the project. Download it to the board and make sure it runs.</li>

</ol>

In minicom, type the command “led ?” and verify you see the following help text:

22562 CONSOLE_UART2&gt; led ?                                                   [Commands]                                                                   test           Test function                                                 on             Start a pattern                                               off            Stop a pattern

?              List commands

Type the command “led on 0” and verify that the USER LED does NOT blink.

<ol start="7">

 <li>The statechart was created with the free tools named <strong>UMLet</strong>. You can download the latest version (14.3) with this link:</li>

</ol>

<a href="https://www.umlet.com/download/umlet_14_3/umlet-standalone-14.3.0.zip">https://www.umlet.com/download/umlet_14_3/umlet-standalone-14.3.0.zip</a>

(or on this page: <a href="http://umlet.com/changes.htm">http://umlet.com/changes.htm</a><a href="http://umlet.com/changes.htm">.</a> Be careful NOT to click on those advertisement Download links!)

The stand-alone version is more stable. It runs on Java, so it should work in your VM which has Java installed.

Note – UMLet is to be installed (decompressed) in your VM but not on your host machine. Once installed, CD to the installation folder (e.g. ~/Projects/Umlet) and type “./umlet.sh &amp;” to launch it.

<h1>3         Tasks</h1>

<ol>

 <li>Imagine the following requirements are handed to you about an LED module:

  <ul>

   <li>Upon a pattern request event, the module should show the specified LED pattern.</li>

   <li>If the pattern request includes a “repeated” flag, the module should show the specified LED pattern repeatedly.</li>

   <li>Upon an <em>off</em> request event, the module should turn off the LED.</li>

  </ul></li>

 <li>Think about the above requirements. Could you find any gaps in the specifications?</li>

 <li>Even for a single LED, specifying its behaviors is not as simple as it appears. Now review the provided statechart in <strong>src/UserLed/UserLed.uxf</strong>. Does it tell us more about how the LED module should behave?</li>

 <li>Copy and paste the two LED patterns you added in the previous assignment to <strong>src/UserLed/LedPattern.cpp </strong>(appending them after the two sample patterns). Remember to update the total count to 4.</li>

 <li>Implement the statechart in <strong>src/UserLed/UserLed.cpp</strong> and <strong>src/UserLed/UserLed.h</strong>.</li>

</ol>

The header file already contains declarations for all the state functions, internal events, timers, member variables required by the statechart design. Refer to the washing machine example for the coding rules.

<ol start="6">

 <li>Test your code with the console command: <em>led on &lt;pattern index from 0 to 3 &gt; &lt;0 for non-repeating; 1 for repeating&gt;</em></li>

</ol>

(e.g. “led on 2 1” to show pattern 2 repeatedly.) <em>led off</em>

See how you can start a new pattern or stop it at any time. For example you can stop a pattern in the middle of a cycle. You can change the pattern before a cycle has finished. This design is reactive and responsive, which is the essence of real-time systems