Download Link: https://assignmentchef.com/product/solved-cs2106-tutorial-2-process-abstraction-in-unix
<br>
<ol>

 <li>(Process Creation) [Taken from AY18/19 S1 Midterms]</li>

</ol>




<table width="566">

 <tbody>

  <tr>

   <td width="45"> </td>

   <td width="521"><strong>C code:</strong></td>

  </tr>

  <tr>

   <td width="45"><strong>00</strong> <strong>01</strong><strong>02</strong> <strong>03</strong> <strong>04</strong><strong>05</strong> <strong>06</strong> <strong>07</strong><strong>08</strong> <strong>09</strong> <strong>10</strong><strong>11</strong> <strong>12</strong> <strong>13</strong><strong>14</strong></td>

   <td width="521"><strong>int main( ) {  </strong>//This is process P   <strong>    if ( fork() == 0 ){    </strong>         //This is process Q     <strong>        if ( fork() == 0 ) {    </strong>//This is process R<strong>            ……      </strong> <strong>            return 0;    </strong><strong>        }    `</strong><strong>        &lt;Point α&gt;</strong><strong>    }  </strong><strong>&lt;Point β&gt;</strong><strong>    return 0;</strong><strong>}</strong></td>

  </tr>

 </tbody>

</table>




Each of the following cases insert zero or more lines at Point α and β. <strong>Evaluate whether each described behaviour is correct or incorrect. </strong>(Note that <strong>wait()</strong> does not block when a process has no children.)

<table width="571">

 <tbody>

  <tr>

   <td width="156"><strong>Point α</strong></td>

   <td width="150"><strong>Point </strong><strong>β</strong></td>

   <td width="265"><strong>Behaviour</strong></td>

  </tr>

  <tr>

   <td width="156"><em>nothing</em></td>

   <td width="150"><strong>wait(NULL);</strong></td>

   <td width="265">Process Q <strong><em>always</em> </strong>terminates before P. Process R can terminate at any time w.r.t. P and Q. </td>

  </tr>

  <tr>

   <td width="156"><strong>wait(NULL);</strong></td>

   <td width="150"><em>nothing</em></td>

   <td width="265">Process Q <strong><em>always</em></strong> terminates before P. Process R can terminate at any time w.r.t. P and Q. </td>

  </tr>

  <tr>

   <td width="156"><strong>execl(valid executable….); </strong> </td>

   <td width="150"><strong>wait(NULL);</strong></td>

   <td width="265">Process Q <strong><em>always</em></strong> terminates before P. Process R can terminate at any time w.r.t. P and Q. </td>

  </tr>

  <tr>

   <td width="156"><strong>wait(NULL);</strong></td>

   <td width="150"><strong>wait(NULL);</strong></td>

   <td width="265">Process P <strong>never terminates</strong>.</td>

  </tr>

 </tbody>

</table>







<ol start="2">

 <li>(Behavior of <strong>fork()</strong> system call) The C program below attempts to highlight the behavior of the <strong>fork()</strong> system call:</li>

</ol>

<table width="602">

 <tbody>

  <tr>

   <td width="45"> </td>

   <td width="557"><strong>C code: </strong></td>

  </tr>

  <tr>

   <td width="45"><strong>01</strong><strong>02</strong><strong>03</strong><strong>04</strong><strong>05</strong><strong>06</strong><strong>07</strong><strong>08</strong><strong>09</strong><strong>10</strong><strong>11</strong><strong>12</strong><strong>13</strong><strong>14</strong><strong>15</strong><strong>16</strong><strong>17</strong><strong>18</strong><strong>19</strong><strong>20</strong><strong>21</strong><strong>22</strong><strong>23</strong><strong>24</strong><strong>25</strong><strong>26</strong><strong>27</strong><strong>28</strong><strong>29</strong><strong>30</strong><strong>31</strong><strong>32</strong><strong>33</strong><strong>34</strong><strong>35</strong><strong>36</strong><strong>37</strong><strong>38</strong><strong>39</strong><strong>40</strong><strong>41</strong><strong>42 </strong></td>

   <td width="557"><strong>int dataX = 100;               int main( ) </strong><strong>{ </strong><strong>    pid_t childPID; </strong><strong> </strong><strong>    int dataY = 200;               </strong><strong>    int* dataZptr = (int*) malloc(sizeof(int)); </strong><strong>     </strong><strong>    *dataZptr = 300; </strong><strong> </strong><strong>    </strong><strong>//First Phase</strong><strong>    printf(“PID[%d] | X = %d | Y = %d | Z = %d |
”,              getpid(),  dataX, dataY, *dataZptr); </strong><strong> </strong><strong>    </strong><strong>//Second Phase</strong><strong>     childPID = fork(); </strong><strong>    printf(“*PID[%d] | X = %d | Y = %d | Z = %d |
”,              getpid(),  dataX, dataY, *dataZptr); </strong><strong> </strong><strong>    dataX += 1;     dataY += 2;     (*dataZptr) += 3; </strong><strong>    printf(“#PID[%d] | X = %d | Y = %d | Z = %d |
”,              getpid(),  dataX, dataY, *dataZptr); </strong><strong> </strong><strong>    </strong><strong>//Insertion Point (for parts (g), (h))</strong><strong>     </strong><strong>    </strong><strong>//Third Phase </strong><strong>    childPID = fork(); </strong><strong>    printf(“**PID[%d] | X = %d | Y = %d | Z = %d |
”,              getpid(),  dataX, dataY, *dataZptr); </strong><strong> </strong><strong>    dataX += 1;     dataY += 2;     (*dataZptr) += 3; </strong><strong>    printf(“##PID[%d] | X = %d | Y = %d | Z = %d |
”,              getpid(),  dataX, dataY, *dataZptr); </strong><strong>     </strong><strong>    return 0; </strong><strong>} </strong></td>

  </tr>

 </tbody>

</table>




Please run the given program “<strong>ForkTest.c</strong>” on your system before answering the questions below.







<ol>

 <li>What is the difference in how the 3 variables: <strong>dataX, </strong><strong>dataY, dataZptr, </strong>and the memory location pointed to by <strong>dataZptr,</strong> are stored?</li>

</ol>




<ol>

 <li>Explain the <strong>values</strong> that are printed by the program.</li>

</ol>




<ol>

 <li>Focusing on the messages generated by second phase (they are prefixed with either “<strong>*</strong>” and “<strong>#</strong>“), what can you say about the behavior of the <strong>fork()</strong> system call?</li>

</ol>




<ol>

 <li>Using the messages seen on your system, draw a <strong>process tree</strong> to represent the processes generated. Use the process tree to explain the values printed by the child processes.</li>

</ol>




<ol>

 <li>Do you think it is possible to get different orderings between the output messages? Why?</li>

</ol>




<ol>

 <li>Can you point out which pair(s) of messages can never swap places? i.e., their relative order is always the same?</li>

</ol>




<ol>

 <li>If we       insert   the       following        code    at         the    insertion          point:</li>

</ol>




<table width="482">

 <tbody>

  <tr>

   <td width="482"><strong>Sleep Code </strong></td>

  </tr>

  <tr>

   <td width="482"><strong>if (childPID == 0){ </strong><strong>    sleep(5);  </strong><strong>//sleep for 5 seconds</strong><strong> } </strong></td>

  </tr>

 </tbody>

</table>




How does this change the ordering of the output messages? State your assumptions, if any.




<ol>

 <li>Instead of the code in (g), we insert the following code at the insertion point:</li>

</ol>




<table width="482">

 <tbody>

  <tr>

   <td width="482"><strong>Wait Code </strong></td>

  </tr>

  <tr>

   <td width="482"><strong>if (childPID != 0){ </strong><strong>    wait(NULL);  </strong><strong>//NULL means we don’t care                   //   about the return result</strong><strong> } </strong></td>

  </tr>

 </tbody>

</table>




How does this change the ordering of the output messages? State your assumption, if any.







<ol start="3">

 <li>(Parallel computation) Even with this crude synchronization mechanism, we can solve programming problems in new (and exciting) ways. We will attempt to utilize multiple processes to work on a problem simultaneously in this question.</li>

</ol>




You are given two C source code files: “<strong>Parallel.c</strong>” and “<strong>PrimeFactors.c</strong>“. “<strong>PrimeFactors.c</strong>” is a simple prime factorization program. “<strong>Parallel.c</strong>” uses the

“<strong>fork</strong>()” and “<strong>execl</strong>()” combination to spawn off a new process to run

“<strong>PrimeFactors.c</strong>”




Let’s setup the programs as follows:

<ol>

 <li>Compile “<strong>c</strong>” to get an executable with the name “<strong>PF</strong>“: <strong>gcc PrimeFactors.c –o PF </strong></li>

</ol>




<ol start="2">

 <li>Compiles “<strong>c</strong>“: <strong>gcc Parallel.c</strong></li>

</ol>




Run the <strong>a.out</strong> generated from step (2). Below is a sample session:

<h1>$&gt; a.out 1024</h1>

1024 has 10 prime factors //note: not unique prime factors




If you try large prime numbers, e.g. 111113111, the program may take a while.




<strong><u>Modify only </u></strong><strong><u>Parallel.c</u></strong> such that we can now initiate prime factorization on [1-9] user inputs <u>simultaneously</u>. More importantly, we want to report results as soon as they are ready regardless of the user input order.







Sample session below:




<h1>$&gt; a.out &lt; test2.in</h1>

9 has 2 prime factors      //Results

118689518 has 3 prime factors

44721359 has 1 prime factors

99999989 has 1 prime factors 111113111 has 1 prime factors




Note the order of the result may differ on your system. Most of time, they should follow roughly the computation time needed (composite number &lt; prime number and small number &lt; large number).  Two simple test cases are given “<strong>test1.in</strong>” and “<strong>test2.in</strong>” to aid your testing.




Most of what you need is already demonstrated in the original <strong>Parallel.c</strong> (so that this is more of a mechanism question rather than a coding question). You only need “<strong>fork</strong>()”,

“<strong>execl</strong>()” and “<strong>wait</strong>()” for your solution.




After you have solved the problem, find a way to change your <strong>wait()</strong> to <strong>waitpid(), what do you think is the effect of this change? </strong>







Additional Questions (For exploration only, not for tutorial discussion)




<ol>

 <li>(Process Creation) Consider the following sequence of instructions in a C program:</li>

</ol>




<table width="557">

 <tbody>

  <tr>

   <td width="557"><strong>C code: </strong></td>

  </tr>

  <tr>

   <td width="557"><strong>int x = 10; int y = 123; </strong><strong> </strong><strong>y = fork(); if (y == 0)      x–; </strong><strong> </strong><strong>y = fork(); if (y == 0)      x–; </strong><strong> </strong><strong>printf(“[PID %d]: x=%d, y=%d
”,getpid(),x ,y); </strong></td>

  </tr>

 </tbody>

</table>




You can assume that the first process has process number <strong><sub>100</sub></strong> (and so <strong><sub>getpid()</sub></strong> returns the value <strong><sub>100</sub></strong> for this process), and that the processes created (in order) are <strong><sub>101</sub></strong>,<strong><sub>102</sub></strong> and so on.




Give:

<ol>

 <li>A possible final set of printed messages.</li>

 <li>An impossible final set of printed messages.</li>

</ol>


