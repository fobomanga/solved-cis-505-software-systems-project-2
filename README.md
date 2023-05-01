Download Link: https://assignmentchef.com/product/solved-cis-505-software-systems-project-2
<br>
<h1><u>Introduction</u></h1>

In this exercise, you will design and implement a simple electronic voting system using the “socket” interface (UDP &amp; TCP) and also Sun remote procedure calls.




This simple voting system should allow clients to vote for their favorite candidate in an election over a network. Each implementation needs to support following functions:




<ul>

 <li><strong>changepassword(), </strong>which enables the admin to change the password of the server. You should use standard input instead of command line arguments to ask for current username and password, and should allow to change the password only if the entered information is correct. The username can just be considered as a name for the server, hence we are not interested in changing that. Return TRUE if successful, FALSE otherwise.</li>

</ul>




<ul>

 <li><strong>zeroize(),</strong> which sets or resets the system to an initial state, with no candidates, no voters, and zero votes. Return TRUE if successful, FALSE otherwise.</li>

</ul>




<ul>

 <li><strong>addvoter(int voterid), </strong>which adds the <em>voterid</em> to a list of authorized voters. Return OK if successful, EXISTS if the <em>voterid</em> is already present in the system, and ERROR if there’s any error.</li>

</ul>




<ul>

 <li><strong>votefor(char *name, int voterid),</strong> which adds one vote to the total vote count of the candidate referred to by <em>name</em> if the <em>voterid</em> has not already voted. If the named candidate is not already present in the system, add the candidate to the system with a vote count of 1. Else,</li>

</ul>

if the candidate is already present in the system, increment his or her vote count by 1. Return EXISTS if the candidate exists and was successfully voted for, NEW if the candidate didn’t exist previously and was successfully voted for, NOTAVOTER if <em>voterid</em> is not in the list of authorized voters, ALREADYVOTED if the <em>voterid</em> had already voted, and ERROR if there’s any error.




<ul>

 <li><strong>listcandidates(), </strong>which returns a list of candidates currently with votes (but not their vote totals).</li>

</ul>




<ul>

 <li><strong>votecount(char *name),</strong> which returns the integer vote total for the candidate referred to by <em>name</em>, or -1 if the candidate isn’t in the system.</li>

</ul>




<ul>

 <li><strong>viewresult(char *username, char *password), </strong>which returns the list of candidates with their vote count and also declare the winner/tie/null(for no candidate) from the server and shuts down the server so that no new votes can be added. The processing of the result should be done on the server side. The client program should be able to view the results only if the username and password, passed as arguments, match with the current admin credentials of the server. Return the list if successful, else return UNAUTHORIZED or ERROR if there’s any error.</li>

</ul>




<strong>NOTE:  </strong>

<ul>

 <li>If the server is invoked without any command line arguments, it should have a default username <strong>“cis505”</strong> and password <strong>“project2”</strong>, otherwise you should set the username and password of the server according to the input arguments. Print an error if the number of arguments is not equal to 0 or 2.</li>

 <li>For each system (socket datagrams and RPCs), please specify the data structures, network protocols, and other aspects of the system (using C, XDR, and English as appropriate) in sufficient detail so that if your documentation is provided to other people they should be able to produce compatible client and server implementations. In particular, for the UDP and TCP parts, please state the format of the seven datagram message payloads (and the response message from the server) clearly. Similarly, in the case of the RPC version, specify the various functions and their arguments clearly.</li>

 <li>You may impose reasonable limits on certain aspects of the system, for e.g., the number of candidates, the length of candidate names, etc, but be sure to document these limits in your specification.</li>

</ul>

<strong>IMPORTANT:</strong> You do not need to handle failures (lost messages, machine crashes) beyond what the socket and RPC mechanisms themselves do. While your code should be designed to work over the network, you can run the server locally on the same machine as the client by using the “localhost” (127.0.0.1) interface for the server running on any available port number (which you should report when you start the server so you can specify it on the client command line). We propose that you use the last 4/5 digits of your Penn ID as Server’s port number if possible. However, do ensure that the port number is greater than 1024 and do mention the port numbers that you use in the write-up. If you plan to run multiple clients on the same machine, you may consider using the ports that are at an incremental offset of 1,2,3..etc from this port number.

<strong>VERY IMPORTANT:</strong> To submit your work, please <strong>put your source and text files in a directory</strong> and use the turnin command on the Eniac machine (not speclab). All programs should be written in C (with XDR and RPCGEN) and you should be able to compile and execute them on Speclab Linux machines. <strong>Take the time to write and code your answers clearly and lucidly, whether the language you are using is English or C.</strong> <strong>Submit only your source code and supporting text. </strong>Do not include compiled or large output files (e.g, write.out or fprint.out) in your submission. Those files can be very large and submitting them can have a disruptive effect on our shared computing resources.




<h1>Milestone 1 (Due: 26 Feb 2016 at 11:59pm)</h1>

<h2>Part 1 (28% credit)</h2>

For this part, you should use the socket API package and the UDP datagram; write a server for the voting system and seven client programs that exercise each of the seven functions specified above. Your server may be a single-threaded process (where each incoming call is processed in sequence).  In addition to your server, you should build seven separate client programs (which can be executed from the linux command line) that exercise each of the seven voting functions mentioned above. Your clients should accept command line arguments that specify the server’s IP address and the port number along with the appropriate arguments to whatever function is being executed. E.g., “./vote-udp localhost 7432 bush 01” should send a message to the server running on localhost port 7432 to cast a vote for “bush” with voter’s Id as 01. <strong>You must follow the name conventions for clients and the server in table 1, and include any customizations in a README. </strong>




<strong><u>Part 2 (28% credit)</u></strong>

Repeat part 1, using TCP stream sockets instead of UDP datagrams.




<h1>Milestone 2 (Due: 14 March 2016 at 11:59pm)</h1>

<h2>Part 3 (28% credit)</h2>

For this part, you should use the RPCGEN package, write a server for the voting system and clients that use each of the RPCs you specified above. Your server may be a single-threaded process (where each RPC call is processed in sequence).

In addition to your server, you should build seven separate client programs (executed from the linux command line) that exercise each of the seven voting functions mentioned above. Your clients should accept command line arguments that specify the name of the server along with the appropriate arguments to whatever function is being executed, e.g., “./vote-rpc localhost hillary 01”. <strong>You must follow the name conventions for clients and the server in table 1, and include any customizations in a README. </strong>

<strong>             </strong>

<h2>Part 4 (16% credit)</h2>

<strong>Non-blocking I/O – </strong>For this part, enhance your implementation in part 2, but utilize non-blocking I/O for implementing your TCP communication <strong>(HINT: use select() which was covered in class). </strong>You should follow the same naming convention as part 2, from the table 1.




To standardize the grading, please use the following command line arguments to implement each function.




<table width="616">

 <tbody>

  <tr>

   <td width="130"><strong> </strong></td>

   <td width="153"><strong>Part 1 </strong></td>

   <td width="156"><strong>Part 2 </strong></td>

   <td width="177"><strong>Part 3 </strong></td>

  </tr>

  <tr>

   <td width="130"><strong>Server </strong></td>

   <td width="153">./server-udp&lt;username&gt;&lt;password&gt;</td>

   <td width="156">./server-tcp&lt;username&gt;&lt;password&gt;</td>

   <td width="177">./server-rpc&lt;username&gt;&lt;password&gt;</td>

  </tr>

  <tr>

   <td width="130"><strong>changepassword() </strong></td>

   <td width="153">./change-password-udp&lt;server_ip_address&gt;&lt;server_port&gt;</td>

   <td width="156">./change-password-tcp&lt;server_ip_address&gt;&lt;server_port&gt;</td>

   <td width="177">./change-password-rpc&lt;server_ip_address&gt;</td>

  </tr>

  <tr>

   <td width="130"><strong>zeroize() </strong></td>

   <td width="153">./vote-zero-udp&lt;server_ip_address&gt;&lt;server_port&gt;</td>

   <td width="156">./vote-zero-tcp&lt;server_ip_address&gt;&lt;server_port&gt;</td>

   <td width="177">./vote-zero-rpc &lt;server_ip_address&gt;</td>

  </tr>

  <tr>

   <td width="130"><strong>addvoter(int voterid) </strong></td>

   <td width="153">./add-voter-udp&lt;server_ip_address&gt;&lt;server_port&gt;&lt;voter_id&gt;</td>

   <td width="156">./add-voter-tcp&lt;server_ip_address&gt;&lt;server_port&gt;&lt;voter_id&gt;</td>

   <td width="177">./add-voter-rpc&lt;server_ip_address&gt;&lt;voter_id&gt;</td>

  </tr>

  <tr>

   <td width="130"><strong>votefor(char *name, int voterid) </strong></td>

   <td width="153">./vote-udp&lt;server_ip_address&gt;&lt;server_port&gt;&lt;candidate_name&gt;&lt;voter_id&gt;</td>

   <td width="156">./vote-tcp&lt;server_ip_address&gt;&lt;server_port&gt;&lt;candidate_name&gt;&lt;voter_id&gt;</td>

   <td width="177">./vote-rpc&lt;server_ip_address&gt;&lt;candidate_name&gt;&lt;voter_id&gt;</td>

  </tr>

  <tr>

   <td width="130"><strong>listcandidates() </strong></td>

   <td width="153">./list-candidates-udp&lt;server_ip_address&gt;&lt;server_port&gt;</td>

   <td width="156">./list-candidates-tcp&lt;server_ip_address&gt;&lt;server_port&gt;</td>

   <td width="177">./list-candidates-rpc&lt;server_ip_address&gt; </td>

  </tr>

  <tr>

   <td width="130"><strong>votecount(char </strong><strong>*name) </strong></td>

   <td width="153">./vote-count-udp&lt;server_ip_address&gt;&lt;server_port&gt;&lt;candidate_name&gt;</td>

   <td width="156">./vote-count-tcp&lt;server_ip_address&gt;&lt;server_port&gt;&lt;candidate_name&gt;</td>

   <td width="177">./vote-count-rpc&lt;server_ip_address&gt;&lt;candidate_name&gt;</td>

  </tr>

  <tr>

   <td width="130"><strong>viewresult(char *username, char *password) </strong></td>

   <td width="153">./view-result-udp&lt;server_ip_address&gt;&lt;server_port&gt;&lt;username&gt; &lt;password&gt;</td>

   <td width="156">./view-result-tcp&lt;server_ip_address&gt;&lt;server_port&gt;&lt;username&gt; &lt;password&gt;</td>

   <td width="177">./view-result-rpc&lt;server_ip_address&gt;&lt;username&gt; &lt;password&gt;</td>

  </tr>

 </tbody>

</table>

<strong>Table 1: Naming Conventions </strong>

For the RPC implementation, you can also choose to include all the RPC calls in one file. If you do so, indicate in a README.<strong>        </strong>


