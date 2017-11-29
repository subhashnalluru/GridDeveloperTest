**Grid-Developer-Test**

The program aims to find the 5 closest events to a location, passed as a pair of coordinates, by the user.

**Running The Program:**

The project comes with a Makefile. To run the program:
 
 1) Open the Terminal (Linux / iOS) or Command Prompt (Windows).
 
 2) Run the command 'make' (without the single quotes).
 
 The project should be compiled at this stage. Now, 
 
 3) Move into the 'bin' directory with 'cd bin'
 
 4) Run the command 'java GridDeveloper'.
 
 The project will now be up and running.
 
 For subsequent runs (when compilation isn't required) simply run: 'java GridDeveloper'
 
 To remove all class files and other unecessary files before the next run, use the command, 'make clean'
 
 This project uses Java and will work normally with Java 7 or higher. 

**Assumptions made:**

1) When no tickets are available for an event, the event is still considered if it is one of the 5 closest, even though it
may not have any "cheapest ticket".

2) Ticket prices are within the range of $10 to $50.

3) A event may have a maximum of 20 tickets.

4) There may be a minimum of only 3 events.

The last 3 assumptions are made only to impose limits on the data being generated by the seed.

**How might you change your program if you needed to support multiple events at the same location?**

--> Solution involving minimal change in code

As per the current version, in the populateEvents function of the "GridDeveloper" class, the Set (HashSet) allows for 
only 1 event per location by checking if the coordinates of a randomly generated event have not already been allocated to 
another event (absent from the Set). Removing this check allows for supporting multiple events at the same location. 

--> Solution involving a little more change in code but improves complexity

Apart from the above, if a location was to support multiple events I would use a Map (HashMap) instead, where a Coordinate 
would be "mapped" to a 'list of Events' taking place at that location. The proximity to the key set of the Map 
(the coordinates) would then be used to filter out events closest to the user's input and the first 5 would be considered.

**How would you change your program if you were working with a much larger world size?**

When working on a global scale, an issue to consider is the amount of the data being dealt with and where it is being stored.
Most systems I have learnt of or come across store it externally, in some disks or databases.

Restricting a user to querying for events only around their geographical location (i.e. town or city or country) would be 
inaccurate given that they could be querying for events at a different time and on a different day, where they
may even be in a different location. Therefore, a user's query should be able to produce results considering events all over the world. 

In order to allow for such capabilities, each Event object can be stored in the external memory (disk/database) and logical 
decision structures, such as trees, binary trees for instance, can be used. These decision structures, will in turn store
information regarding the events and their locations in a map, where each location may correspond to any number of events. In
the case of a binary tree each node of the tree may store a map containing a subset of all the events and a 
lookup may be performed for checking if the location being queried is present in that node or any node descending from it. 
Since maps have a low complexity lookup of O(1) (if it is a HashMap) or a O(log n) if it is a balanced tree map, etc querying
for the presence of a location at a node has minimal cost. So, based on the coordinate, input by the user, the choice of 
which subtree to visit can be decided. This representation gives the memory a "cluster" like appearance, as all the 
coordinates in a particular geographical location can be clustered together. This decreases and hence, improves the number
of accesses to the external memory and thus, reduces the searching/querying time in the external memory.

To improve on the above, caching algorithms may also be deployed to store information regarding events at locations most 
frequently queried. This may be achieved via the Adapter and Caching Proxy software engineering patterns.