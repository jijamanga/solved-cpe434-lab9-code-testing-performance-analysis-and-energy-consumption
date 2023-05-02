Download Link: https://assignmentchef.com/product/solved-cpe434-lab9-code-testing-performance-analysis-and-energy-consumption
<br>
You will use a few utilities that will help you debug and analyze your software Please run all the experiments and write down your observations.

<h1>Part I: Valgrind</h1>

Valgrind is a tool suite that provides a number of debugging and profiling tools. You can make your program faster and more correct using Valgrind. Of the many tools available, we will use <strong><em>memcheck ​</em></strong>and ​<strong><em>cachegrind ​</em></strong>tools. Please visit the quick start tutorial at the​ ​<a href="https://www.valgrind.org/docs/manual/quick-start.html">official site.</a>

<strong>Part I.a: Cachegrind  </strong>

Cachegrind is a tool available in Valgrind that simulates how your program interacts with the machine’s cache hierarchy and branch predictor. It simulates independent first-level caches: I and D- cache and unified second level cache. Please go through the tutorial at <a href="https://www.valgrind.org/docs/manual/cg-manual.html">this link</a><u>​               </u>​, and try to answer the following question:

Most of the modern processors have three levels of cache. As presented above, cachegrind simulates two levels of caches. How does cachegrind handle the machines that have more than two levels of caches? Why does cachegrind do what it does for handling three levels of cache hierarchy? ​<strong>[5+5]  </strong>

<strong>Assignment I:  </strong>

You are given the following two codes. Please compile and run the codes. Please paste the demonstration run in your report. Write what each of the programs is doing. Please note the difference between the two programs. ​<strong>[5]  </strong>

<table width="589">

 <tbody>

  <tr>

   <td width="589">/*File: test1.cppcompile as g++ test1.cpp -o test1*/using namespace ​std​;  #include &lt;iostream&gt;  main​(){int ​array​[​1000​][​1000​];  int ​i​,​j​;for​(​i​=​0​;​i​&lt;​1000​;​i​++​)for​(​j​=​0​;​j​&lt;​1000​;​j​++​)array​[​i​][​j​]​=​0​;cout ​&lt;&lt; ​”array[0][0] was ” ​&lt;&lt; ​array​[​0​][​0​] ​&lt;&lt; ​endl​;  }</td>

  </tr>

 </tbody>

</table>

<strong> </strong>

<table width="589">

 <tbody>

  <tr>

   <td width="589">/*File: test2.cppcompile as g++ test2.cpp -o test2*/using namespace ​std​;  #include &lt;iostream&gt;  main​(){int ​array​[​1000​][​1000​];  int ​i​,​j​;for​(​i​=​0​;​i​&lt;​1000​;​i​++​)for​(​j​=​0​;​j​&lt;​1000​;​j​++​)array​[​j​][​i​]​=​0​;cout ​&lt;&lt; ​“array​[​0​][​0​] ​was ​” &lt;&lt; array[0][0] &lt;&lt; endl;}</td>

  </tr>

 </tbody>

</table>

<strong>Assignment II:  </strong>

Now run each of the programs with valgrind using the cachegrind tool. ​<strong>Please grab the screenshot of the outputs using cachegrind where you should highlight the D1 cache misses for each of the programs​</strong>. You might want to run the programs as below in your command line. ​<strong>[3]  </strong>




valgrind ​-​v ​–​tool​=​cachegrind ​.​/​test1  valgrind –v ​–​tool​=​cachegrind ​.​/​test2




Do you see any difference in the numbers? Please answer the following questions based on your observations:

<ol>

 <li>Which program is better in terms of performance? ​<strong>[2] </strong></li>

 <li>Why do you think one program is better? ​<strong>Explain in detail [5] </strong></li>

</ol>

<strong>Part I.b memcheck  </strong>

Memcheck is the default tool in valgrind. You may specify ​–​tool=memcheck ​, but it is not needed.​ In our exercise, we will try to find memory leaks in our code exercise. Please go through the official documentation as <u>​</u><a href="https://www.valgrind.org/docs/manual/mc-manual.html">this link</a><u>​</u> ​to learn more on how to use this tool.

Valgrind allows you to run your program in Valgrind’s own environment that monitors memory usage such as calls to malloc and free (or new and delete in C++). If you use uninitialized memory, write off the end of an array, or forget to free a pointer, Valgrind can detect it. Since these are particularly common problems, this tutorial will focus mainly on using Valgrind to find these types of simple memory problems, though Valgrind is a tool that can do a lot more.

<strong>Assignment III:  </strong>

You are given the following codes. Please compile and run them. Please write what is the problem with ​<strong>each ​</strong>of the codes. ​<strong>[3]  </strong>

<strong> </strong>

<table width="591">

 <tbody>

  <tr>

   <td width="591">//file: test 3 compile as test3#include &lt;stdlib.h&gt;  int ​main​(){char *​x ​= ​(​char*​)​malloc​(​100​); ​/* or, in C++, “char *x = new char[100] */ ​return ​0​;  }</td>

  </tr>

 </tbody>

</table>

<strong> </strong>

<table width="591">

 <tbody>

  <tr>

   <td width="591">//file: test4 compile as test4#include &lt;stdlib.h&gt;  int ​main​(){char *​x ​= ​(​char*​)​malloc​(​10​);  x​[​10​] ​= ​’a’​;  return ​0​;}</td>

  </tr>

 </tbody>

</table>







<table width="591">

 <tbody>

  <tr>

   <td width="591">//file: test5 compile as test5#include &lt;stdio.h&gt;  int ​main​(){int ​x​;  if​(​x ​== ​0​){printf​(​”X is zero”​); ​/* replace with cout and include iostream for C++ */}  return ​0​;}</td>

  </tr>

 </tbody>

</table>







<strong>Assignment IV:  </strong>

Run each of the following programs with valgrind so that you will test the memory leaks. You might want to use the following commands in the terminal to run them. Please grab the screenshot ​<strong>[3] ​</strong>and try to explain each of them with focus on error/s indicated for ​<strong>each ​</strong>of the programs. ​<strong>[7]  </strong>

valgrind ​–tool=memcheck ​ ​–​leak​-check=yes ./test3 valgrind ​      ​–tool=memcheck ​ ​–​leak​ ​check=yes ./test4 valgrind ​–tool=memcheck ​  ​–​leak​-​check=yes ./test5

<strong>           </strong>

<h1>Part II: Power Consumption measurement</h1>

The next section of this lab involves using a power measurement tool to  determine which is the best sorting algorithm based on power consumption and work performed. If you are running linux natively, you may use the RAPL model. If you are using WSL2, it is recommended to use the Hardware Monitor Pro application. If you are using a MAC, it is recommended to use the Activity Monitor. You will only need to use one of the tools for the second part of this lab.

<h1>Using RAPL model (Native Linux)</h1>

Running Average Power Limit (RAPL) is one of the energy modeling techniques that can be used in some supported CPUs platforms. Intel introduced RAPL first in the Intel Sandy Bridge architecture and it continues in successive generation architectures like the Haswell and Ivy Bridge. There is a set of hardware counters that can be accessed, known as Model-Specific Registers (MSRs).

There are two benefits of using the RAPL model: it can be used to profile the real-time power consumption or to control it by passing the corresponding parameters. In general, there are multiple benefits of using the RAPL; hardware counters are updated without software intervention. Also, these registers are updated automatically. However, these registers are just 32-bit length so it is possible that the registers will overflow after a certain amount of time after starting the machine. <strong> </strong>

<h1>Using Hardware Monitor Pro (WSL2)</h1>

You may download and instal the Hardware Monitor Pro from the following <u>​</u><a href="https://www.cpuid.com/downloads/hwmonitor-pro/hwmonitor-pro_1.44.exe#google_vignette">link</a><u>​</u><a href="https://www.cpuid.com/downloads/hwmonitor-pro/hwmonitor-pro_1.44.exe#google_vignette">.</a> Please only use the trial version of the Hardware Monitor Pro for the lab. The Pro version will allow you to log power consumption over a period of time.

To log power consumption, select Tools&gt;Logs&gt;Start Recording. Once your program has finished, end the recording with Tools&gt;Logs&gt;Stop Recording. A new window should appear with the current logs. Navigate from this window to the subfolder containing the logs in graphical form. The package power graph is what you will need to reference for your power measurements. Additionally, under Tools&gt;Options you can also save a corresponding csv file that those graphs are based on.

If you are using this method, you will need to log your host machine’s power consumption normally, to act as a baseline when you log power consumption during program execution.

<h1>Using Activity Monitor (for MACs)</h1>

If you are using a MAC, you make use of the Activity Monitor. You may refer to this ​<a href="https://support.apple.com/en-ca/guide/activity-monitor/actmntr43697/mac">link </a>​to help get started. You will need to record your host machine’s idle power consumption before running any programs to act as a baseline.

<strong>Assignment V:  </strong>

Write a function or cite a source for each of the following three sorting algorithms. If you are running linux natively, you will edit a source file provided (​<em>rapl_read​</em>.c) at around line 809 to make a call to each of these functions separately (one at a time).

Quick Sort

Merge Sort

Insertion Sort

You can create a top level function e.g. ​<em>quick_sort_top_level​</em>() that can be called from the location specified in ​<em>rapl_read​</em>.c if you are running linux natively or from main if you are using the other methods. Your top level function should accept a long integer ​<em>n ​</em>as an argument, generate ​<em>n </em>integer elements and call the actual sorting function. The top level function should also call another function ​<em>sort_verify​</em>() that verifies if the sorting is done correctly (you can iterate through all the items of the sorted array to see if every ​<em>i+1​</em>th item is greater or equal to ​<em>i​</em>th item).

If you are using either the Hardware Monitor Pro or Activity Monitor, you will need to include timing as the recorded information will need to be converted from Watts into Joules (Watts X Second). Additionally, you will need to increase the number of elements to make each of your sorting algorithms take around 10 to 20 seconds so that you can record more data for their power consumption.

You should time your programs to run for around 10 to 20 seconds. For some of these algorithms that may require tens of millions of elements. You cannot allocate arrays of this size on the stack, you must allocate them in the global area or the heap. Algorithms obtained from the web may incur segmentation faults because of this issue. You may consider the following:




<table width="591">

 <tbody>

  <tr>

   <td width="591">#include &lt;sdtdio.h&gt;int arraya[1000000];                               /* this is ok it is from global memory */ int main(){int arrayb[1000000];                              /*this is not ok it is from the stack and will fail with a segmentation error for large enough arrays */int *arrayc = malloc(1000000);           /* this is ok it is from the heap */} </td>

  </tr>

 </tbody>

</table>




Make sure to make proper use of allocating and deleting the elements of the array. <strong>[20]  </strong>

<strong>Assignment VI:  </strong>

Your program should generate at least 1M elements of an array and run for around 10 to 20 seconds. Please use pointer for dynamic array using new/delete or malloc/free rather than using static array. Compile and run code with each of the algorithms 5 times and report all of the values in Joules. Find the average values of the five runs. Please make sure that you have turned off any compiler optimization (i.e. Please use -O0 flag while compiling) ​<strong>[15]  </strong>

<strong>Assignment VII:  </strong>

Perform the same set of experiments as in Assignment VI, but with optimization flag -O3. Run each of the sorting algorithms 5 times and report the average as the final output. ​<strong>[15]  </strong>

<strong>Assignment VIII:  </strong>

Which algorithm was the best in terms of energy consumption per element? Did the compiler flag make things any better? ​<strong>[12]  </strong>

<strong>Extra Credit Research:  </strong>

<strong> </strong>

<ol>

 <li>Why is the power consumption roughly the same (power, not energy) for the different algorithms? ​<strong>[3]</strong></li>

 <li>How would you determine if the hardware monitor is corrupting the power measurement? ​<strong>[5]</strong></li>

 <li>Please research and discuss the MSR registers. ​<strong>[2]</strong></li>

</ol>




<strong>             </strong>