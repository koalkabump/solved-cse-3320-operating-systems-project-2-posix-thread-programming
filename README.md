Download Link: https://assignmentchef.com/product/solved-cse-3320-operating-systems-project-2-posix-thread-programming
<br>
<h1><span style="font-size: 2em; font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen-Sans, Ubuntu, Cantarell, 'Helvetica Neue', sans-serif;">Introduction</span></h1>

The purpose of this project is to practice Pthread programming by solving various problems. The objectives of this project is to learn:

<ol>

 <li>Get familiar with the Pthread creation and termination.</li>

 <li>How to use mutexes and conditional variables in Pthread.</li>

 <li>How to design efficient solutions for mutual exclusion problems.</li>

</ol>

<h2>Project submission</h2>

For each project, create a gzipped file containing the following items, and submit it through Blackboard.

<ol>

 <li>A report that briefly describes how did you solve the problems and what you learned.</li>

 <li>The POSIX thread programming codes and files containing your test cases.</li>

</ol>

<h2>Assignments</h2>

<h3>Assignment 1 (40 pts)</h3>

Given two character strings s1 and s2. Write a Pthread program to find out the number of substrings, in string s1, that is exactly the same as s2. For example, suppose number_substring(s1, s2) implements the function, then number_substring(“abcdab”, “ab”) = 2, number_substring(“aaa”, “a”) = 3, number_substring(“abac”, “bc”) = 0. The size of s1 and s2 (<em>n</em>1 and <em>n</em>2) as well as their data are input by users. Assume that <em>n</em>1 mod <em>NUM</em>_<em>THREADS </em>= 0 and <em>n</em>2<em>&lt;n</em>1<em>/NUM</em>_<em>THREADS</em>.

The following is a sequential solution of the problem. read_f() reads the two strings from a file named “string.txt and num_substring() calculates the number of substrings.

<table width="633">

 <tbody>

  <tr>

   <td colspan="5" width="338">#include &lt;stdlib .h&gt; #include &lt;stdio .h&gt;#include &lt;string .h&gt;#define MAX 1024int total = 0; int n1 , n2 ;char ∗s1 ,∗ s2 ; FILE ∗fp ;int readf (FILE ∗fp ){ if (( fp=fopen (” strings . txt” , “r”) )==NULL){ printf (“ERROR: can ’ t open string . txt !
”) ;return 0;} s1=(char ∗) malloc ( sizeof (char)∗MAX) ; if ( s1==NULL){ printf (“ERROR: Out of memory!
”) ;return −1;} s2=(char ∗) malloc ( sizeof (char)∗MAX) ; if ( s1==NULL){ printf (“ERROR: Out of memory
”) ;return −1;}<em>/</em>∗<em>read s1 s2 from the f i l e </em>∗<em>/ </em>s1=fgets (s1 , MAX, fp ) ; s2=fgets (s2 , MAX, fp ) ;n1=strlen ( s1 ) ;   <em>/</em>∗ <em>length    of               s1</em>∗<em>/ </em>n2=strlen ( s2 ) −1; <em>/</em>∗ <em>length        of               s2</em>∗<em>/</em>if ( s1==NULL | |          s2==NULL | |        n1&lt;n2)                 <em>/</em>∗<em>when error</em></td>

   <td width="54"><em>exit </em>∗<em>/</em></td>

   <td width="34"></td>

   <td width="47"></td>

   <td width="21"></td>

   <td width="33"></td>

   <td width="105"></td>

  </tr>

  <tr>

   <td colspan="2" width="196">return −1;}int num_substring(void){int i , j , k ; int count ; for ( i = 0; i &lt;= (n1−n2) ;</td>

   <td colspan="2" width="74">i++){</td>

   <td width="68"></td>

   <td width="54"></td>

   <td width="34"></td>

   <td width="47"></td>

   <td width="21"></td>

   <td width="33"></td>

   <td width="105"></td>

  </tr>

  <tr>

   <td colspan="2" width="196">count=0;for ( j = i , k = 0; k &lt; n2 ;</td>

   <td colspan="2" width="74">j++,k++){</td>

   <td width="68"><em>/</em>∗<em>search</em></td>

   <td width="54"><em>for           the</em></td>

   <td width="34"><em>next</em></td>

   <td width="47"><em>string</em></td>

   <td width="21"><em>of</em></td>

   <td width="33"><em>size</em></td>

   <td width="105"><em>of n2</em>∗<em>/</em></td>

  </tr>

  <tr>

   <td colspan="2" width="196">if (∗( s1+j ) !=∗(s2+k) ){ break;} else count++;if ( count==n2)total++;                <em>/</em>∗ <em>find       a</em></td>

   <td colspan="2" width="74"><em>substring</em></td>

   <td width="68"><em>in       this    step</em></td>

   <td width="54">∗<em>/</em></td>

   <td width="34"></td>

   <td width="47"></td>

   <td width="21"></td>

   <td width="33"></td>

   <td width="105"></td>

  </tr>

  <tr>

   <td colspan="4" width="270">}}return total ;}int main( int argc , char ∗argv [ ] ){int count ;readf ( fp ) ; count = num_substring () ;</td>

   <td colspan="2" width="122"></td>

   <td width="34"></td>

   <td width="47"></td>

   <td width="21"></td>

   <td width="33"></td>

   <td width="105"></td>

  </tr>

  <tr>

   <td width="168">printf (“The number ofreturn 1;}</td>

   <td colspan="2" width="75">substrings</td>

   <td colspan="8" width="389">is : %d
” , count ) ;</td>

  </tr>

  <tr>

   <td width="168"></td>

   <td width="27"></td>

   <td width="48"></td>

   <td width="26"></td>

   <td width="68"></td>

   <td width="54"></td>

   <td width="34"></td>

   <td width="47"></td>

   <td width="21"></td>

   <td width="33"></td>

   <td width="105"></td>

  </tr>

 </tbody>

</table>

Write a parallel program using Pthread based on this sequential solution.

HINT: Strings s1 and s2 are stored in a file named “string.txt”. String s1 is evenly partitioned for NUM_THREADS threads to concurrently search for matching with string s2. After a thread finishes its work and obtains the number of local matchings, this local number is added into a global variable showing the total number of matched substrings in string s1. Finally this total number is printed out. You can find an example of the “string.txt” in the attached source code.

<h3>Assignment 2 (35 pts)</h3>

Use <em>condition variables </em>to implement the producer-consumer algorithm. Assume two threads: one producer and one consumer. The producer reads characters one by one from a string stored in a file named “message.txt”, then writes sequentially these characters into a circular queue. Meanwhile, the consumer reads sequentially from the queue and prints them in the same order. Assume a buffer (queue) size of 5 characters. Write a Pthread program using condition variables.

<h3>Assignment 3 (25 pts)</h3>

Write two micro-benchmarks to quantify the costs of context switch between multiple processes and multiple threads. Learn from the lat_ctx benchmark from the lmbench benchmark suite about how to measure the context switch cost between multiple processes. Understand how this benchmark works and adapt it to write your own benchmarks. Configure the number of vCPUs to more than one but run all processes/threads on one vCPU. Vary the number of processes/threads to study if the context switch cost varies. Below is a related work on quantifying the cost of context switch. <a href="https://www.cs.rochester.edu/~kshen/papers/expcs2007.pdf">https://www.cs.rochester.edu/~kshen/papers/expcs2007.pdf</a>

Tips

<ul>

 <li>Shutdown your VM and change to VM setting to use 4 vCPUs.</li>

 <li>Verify that your VM has 4 vCPUs:</li>

</ul>

$ cat /proc/cpuinfo

You should have 4 CPUs (processor: 0-3).