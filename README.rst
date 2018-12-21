Information Retrieval
The Notes
RSS

Search
Blog
Archives
Users and Usability
Nov 6th, 2012

Users are extremely variable
Users are not search professionals
Berry Picking
Conventional information retrieval assumes that the user starts with a well-formulated information need and attempt to satisfy that need by a combination of searching and browsing.
In many practical situations, the user begins by exploring a topic. This exploration leads to greater understanding of the topic, which may eventually lead to a well formulated information need, or may lead the user in directions that were not anticipated at the beginning.
Web Search: Browsing
Users give queries of 2 to 4 words.
Most users click on on the first few results. Few go beyond the fold on the first page.
80% of users, use search engine to find sites:
search to find site
browse the site to find information
Amil Singal, Google, 2004

Browsing
If docs are accessible online, user can browse content

Inspecting docs can compensate for weaknesses in the underlying search system, e.g., the difficulty of ranking web docs
… but requires rapid delivery to the desktop.
Otherwise, the user can browse surrogates, e.g., sets of catalog records, subject hierarchies, cluters of documents, etc.

Browsing surrogates puts heavy demands on the underlying search system.
Surrogates heavily used in library catalogs
Browsing by filtering & sorting
Filters are used to extract a small subset from a large collection. Allow users to reject categories
Sorting subsets in various ways allows users to organize data for rapid scanning & quick retrieval
Snippets
A snippet is a short record that a search system returns to describe a hit and provide a link to an online document.
Good snippet design affects usability.
Variation of snippet choices:
Dynamic or static (pre-computed) snippet?
Content only or with related information?
highlighting the search terms
balance b/w length of snippet and # of snippets on the page
Snippets help users understand why the hit was included in the results
Designing the Search Page
Overall organization
Spacious or cramped
Page layout showing division of functionality
Positioning components in the interface
Emphasizing parts of the interface
Queries
insert text string or fill in text boxes
Auto complete, suggested queries, spelling correction, etc.
Interactivity
Performance requirements
The Yahoo! Interface
though incredibly cluttered and unattractive, was somewhat effective
very many brnches from a single web page saved the need for hierarchy of menus
simple HTML markup ensured quickness & accuracy on all browsers
didn’t change often, so familiar users could get what they wanted very quickly
Design/Evaluate Process
Requirements
Design
Implementation
Evaluation
User Interface
Interface (visual elements)
Functions (fields, content, operators, etc)
Data (metadata, data/file structures)
Systems (performance)
Usability is paramount
Evaluation
Process of determining the worth of, or assinging a value to, the usability on the basis of careful examination and judgement.

Categories of evaluation methods
analytical evaluation w/o users
empirical evaluation with users
measurements of operational systems
Usability
Usability has the following aspects:

Effectiveness
The accuracy and completeness with which users achieve certain goals.
Measures: quality of solution, error rates
Efficiency
The relation between the effectiveness and the resources expended in achieving them
Measures: task completion time, learning time, number of clicks
Satisfaction
The users’ comfort with and positive attitudes towards the use of the system
Measures: attitude rating scales
Measurements of Operational Systems
Analysis of system logs
Which user interface options were used?
When was was the help system used?
What errors occurred and how often?
Which hyperlinks were followed (click through data)?
Human feedback
Complaints and praise
Bug reports
Requests made to customer service
Experiments on Op. Systems
Change some small part of the system for a small # of users
Measure effect of change
Is the effect of change positive? Negative? Negligible?
User Testing
Preparation (what is being evaluated?)
Conduct sessions w/ users
Analysis of results
DFS & MapReduce
Nov 1st, 2012

Hadoop
Hadoop is an open-source implementation that combines MapReduce and Distributed File-System technologies.

Useful for the indexing side of web searching.

Designed for hundreds of thousands of server machines
Add or remove physical machines at any time
Automatic detection of faults (with quick, automatic recover)
Optimized for larger files, not many small files.
Supports write-once-read-many access model first and foremost
Automatic replication (~3 times, usually)
No other backup!
Hadoop is used by many large, well-known companies. It is believed that Facebook uses Hadoop.

GFS & HFS
Literature
GFS
Overview
Built from many inexpensive components that often fail.
Optimized for 100MB+ files
High sustained bandwidth is more important than low latency
Workload
Two kinds of reads are most common:
large streamin reads
small random reads
many large, sequential writes that append data to files
once written, files are seldom modified again
Architecture
Cluster
contains a single master and several chunkservers
clients and chunkservers can be run on the same computers
Files divided into fixed-sized chunks. Each chunk has a unique 64-bit chunk handle assigned by master server
Chunkservers store the chunks on local disks as linux files, and read & write
Client interactions
A client asks the master which chunkservers it should contact and completes the file exchange with that chunkserver directly (not via master)
Programming for Large Computer Clusters
Goal
Create env in which less-experienced programmers could develop useful network services quickly
Separate app programmers from the complexities of the DFS
Academic researcher programmers
Deep knowledge of domain
Good algorithmic understanding
BUT…

Has limited understanding of large-scale data analysis
not skilled in any form of concurrent computing
Tape-Based Computing
Problem:
Waaaaay too much data to build data structures in memory
Disk I/O waaaay to slow for random access
Solution
Data managed by short key-value pairs
To process data:
split data into key-value pairs
sort data by key
merge files so that all values wht the same key are processed together
proess all the values for a single key
write out 1+ records for each key
MapReduce
Programming
Map takes an input pair and produces a set of intermediate key-value pairs
Combiner merges all intermediate values associated with the saame intermediate key and passes them to Reduce
Reduce accepts an intermediate key and a set of values for that key, combines these values to form a possibly smaller set of values
Map
Input: (u0, v0)
Output:
(u, d) — Dummy d indicates that u is a from-URL
(v, u) — Indicate that v is a to-URL with link from u
d is a dummy marker. Do not output if u = v.
The output is a set of keys, which are all the URLs, with values that depend on whether they are from-URLs or to-URLs.
Combiner
The input to the reduce process merges the output values from the map task that correspond to each key (URL).
It combines all the (key, value) pairs from Map that have the same key. For each URL, w, it creates a list:
w, {d, ... , d, u1, ..., uk}
The Combine operation is performed automatically by the system libraries.
Reduce
Input: (w, {d, ..., d, u1, ..., uk}), where w is any URL.
Output:
If d does not exist, discard and do not output (corresponds to a URL that never appears as the first element of a (u, v) pair)
Otherwise, remove duplicates from u1, ..., uk and output.
The output is a to-URL and a list of the nodes that link to it: v, {u1, ..., uk}
Cluster Implementation
"Visual representation of MapReduce"

Scalability
Web search services are monolithic centralized systems (though use distributed data centers)
Moore’s Law allows for scalability on a grand scale
Harder to maintain quality of software when more and more people work on the same code base
Solution: MODULAR DEVELOPMENT
Organize for minimal staff in systems management as well as customer service
AUTOMATE AUTOMATE AUTOMATE
Blog Archives
Recent Posts
Users and Usability
DFS & MapReduce
Copyright © 2012 - Parker J. Moore, pjm336[at]cornell.edu - Powered by Octopress
