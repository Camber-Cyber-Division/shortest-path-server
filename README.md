shortest-path-server
====================

Instructions
------------

1. If you do not already have a github account, create one.
2. Fork this project.
3. Update the LICENSE file with whatever license you prefer.
4. Add a copyright, license, and warranty notice at the top of each source file
   you create.
 * If you use the LICENSE file included, the information you need to include at
   the top of each source file can be found in the *License* section of this
   README. Just change __your-name-here__ to your full name.
5. Develop a solution to the problem described within the *Requirements*
   section in whatever language you prefer. Recommended languages to use will
   be provided with the link to these instructions.
 * You are welcome to research algorithms and solutions online. However, do
   __not__ copy or use anyone else's code. The solution should be developed by
   you in its entirety
 * The reference solution used to test your application has been written in
   unoptimized C.
6. Add any notes regarding your solution to the *Solution Notes* section.
7. Add the build steps to the *Build Instructions* section.
 * Your solution will need to build and run on a x86\_64 system running Debian
   Stable GNU/Linux.
8. Bonus Points: Like you, we are pedantic nerds. Please let us know if you
   find anything during this process or in our instructions that could use
   improvement.
9. Submit a link to your completed solution as well as any questions to
   <jcook@camber.com>.


Solution Notes
--------------

*Add solution notes here*


Build Instructions
------------------

*Add build instructions here*


Requirements
------------
* The application will take a directed acyclic graph, a starting vertex, and a
  destination vertex and calculate the shortest path from the start to the
  destination
* The application will listen and accept connections on TCP 127.0.0.1:7777
* Upon establishing a connection with a client the application will read the
  starting vertex, destination vertex, and graph from the client file
  descriptor in the format specified under the Input section and write the
  shortest path and distance out over the client file descriptor in the format
  specified under the Output section


Input Format
------------

* The binary input data's endianness is little-endian. If you are developing on
  an x86 system, you do not have to worry about this.
* The binary input data is split into two byte fields
* Each field is a sixteen bit unsigned integer in the set: {1,2,...,65535}
 * Zero is an invalid input; it can be assumed that no field will be set to 0
* There are no delimiters between the fields
* The first and second byte represent a starting vertex
* The third and forth byte represent a destination vertex
* The fifth and sixth byte represent the number of edges that follow
* Each edge is directed
* Each edge is split into three fields
 * The first field is a vertex and predecessor to the next field
 * The second field a vertex and the successor to the previous field
 * The third field is the cost to travel from the predecessor to the successor


Sample Input Data
-----------------

     # Decimal Representation of Binary File
     1  5   9
     1  2  14
     1  3   9
     1  4   7
     2  5   9
     3  2   2
     3  6  11
     4  3  10
     4  6  15
     6  5   6

     # Hexadecimal Representation of Binary File
     0100 0500 0900
     0100 0200 0e00
     0100 0300 0900
     0100 0400 0700
     0200 0500 0900
     0300 0200 0200
     0300 0600 0b00
     0400 0300 0a00
     0400 0600 0f00
     0600 0500 0600


Output Format
-------------

* The output will written to the client file descriptor as a string in the
  following format:

          start_vertex->vertex->destination_vertex (distance)
* If there is no path from the starting vertex to the destination vertex the
  result should be in the follow format:

          No path from 'start_vertex' to 'destination_vertex'


Sample Output Data
------------------

     # Correct output for sample input data above
     1->3->2->5 (20)

     # Correct output for map with no path from start (1) to destination (2)
     No path from '1' to '2'


Testing Instructions
--------------------

There are several `map#.bin` files in the data directory of this project. The
data can be sent to your listening server with the following command (via a
shell in Linux):

     cat map1.bin | netcat 127.0.0.1 7777

License
-------

This file is part of Shortest-Path-Server.

Copyright (c) 2013 __your-name-here__

Shortest-Path-Server is free software: you can redistribute it and/or modify it
under the terms of the GNU General Public License as published by the Free
Software Foundation, either version 3 of the License, or (at your option) any
later version.

Shortest-Path-Server is distributed in the hope that it will be useful, but
WITHOUT ANY WARRANTY; without even the implied warranty of MERCHANTABILITY or
FITNESS FOR A PARTICULAR PURPOSE.  See the GNU General Public License for more
details.

You should have received a copy of the GNU General Public License along with
Shortest-Path-Server.  If not, see <http://www.gnu.org/licenses/>.
