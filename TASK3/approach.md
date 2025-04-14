To solve the given problem,I used djikstra's algorithm  which is perfect for finding the least-cost path in weighted graphs like this grid. 
First of all I represented the given path into grid by indexing rows and columns from 0 to 9.
Then I defined a cost function using given parameters.
Then I implemented djikstra's algorithm by:a)Using a priority queue to always expand the lowest cost node. b)Tracking visited nodes and the cost to reach them. c)Tracking the path by storing predecessors.
