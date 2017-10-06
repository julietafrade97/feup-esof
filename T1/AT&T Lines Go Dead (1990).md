## AT&T Lines Go Dead (1990)
At 2:25pm on Monday, January 15th, network managers at AT&T's Network Operations Center in Bedminster, N.J. began noticing an alarming number of red warning signals from various parts of their world-wide network. **Within seconds, the giant 72 screen video array that graphically represented the network was crisscrossed with a tangle of red lines as a rapidly spreading malfunction leapfrogged from one computer-operated switching center to another**. The standard procedures the managers tried first **failed** to bring the network back up to speed and **for nine hours**, while engineers raced to stabilize the network, almost 50% of the calls placed through AT&T failed to go through. Until 11:30pm, when network loads were low enough to allow the system to stabilize, AT&T alone **lost more than $60 million in unconnected calls**. Still unknown is the amount of business lost by airline reservations systems, hotels, rental car agencies and other businesses that relied on the telephone network. This wasn't supposed to happen. AT&T had built a reputation and a huge advertising campaign base on its reliability and security.
<br><br>
It is known that **75 million phone calls were missed and 200 thousand airline reservations were lost**. Working backwards through the data, a team of 100 frantically searching telephone technicians identified the problem, which **began in New York City**. The New York switch had performed a routine self-test that indicated it was nearing its load limits. 
<br><br>
As standard procedure, the switch performed a 4 second maintenance reset and sent a message over the signalling network that it would take no more calls until further notice. After reset, the New York switch began to distribute the signals that had backed up during the time it was off-line. Across the country, another switch received a message that a call from New York was on its way, and began to update its records to show the New York switch back on line. A second message from the New York switch then arrived, less than ten milliseconds after the first. **Because the first message had not yet been handled, the second message should have been saved until later. A software defect then caused the second message to be written over crucial communications information**. Software in the receiving switch detected the overwrite and immediately activated a backup link while it reset itself, **but another pair of closely timed messages triggered the same response in the backup processor, causing it to shut down also**. When the second switch recovered, it began to route its backlogged calls, and propagated the cycle of close-timed messages and shut-downs throughout the network. The problem repeated iteratively throughout the 114 switches in the network, blocking over 50 million calls in the nine hours it took to stabilize the system.
<br><br>
```
1  while (ring receive buffer not empty 
          and side buffer not empty) DO

2    Initialize pointer to first message in side buffer
     or ring receive buffer

3    get copy of buffer

4    switch (message)

5       case (incoming_message):

6             if (sending switch is out of service) DO

7                 if (ring write buffer is empty) DO

8                     send "in service" to status map

9                 else

10                    break

                  END IF

11           process incoming message, set up pointers to
             optional parameters

12           break
       END SWITCH


13   do optional parameter work
```

The cause of the problem had come months before. In early December, technicians had upgraded the software to speed processing of certain types of messages. Although the upgraded code had been rigorously tested, **a one-line bug was inadvertently added to the recovery software of each of the 114 switches in the network**. The defect was a **C program** that featured a break statement located within an if clause, that was nested within a switch clause.
<br>
#### References:
[http://users.csc.calpoly.edu](http://users.csc.calpoly.edu/~jdalbey/SWE/Papers/att_collapse.html)
<br>
[www.phworld.org](http://www.phworld.org/history/attcrash.htm)
<br>
[www.slideshare.net](https://www.slideshare.net/ItrisAutomationSquare/risk-management-and-business-protection-with-coding-standardization-static-analyzer)
