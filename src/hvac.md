# High-Velocity AI Cache (HVAC)

Distributed deep learning training time can be divided into three parts:
- computation time
- communication time
- I/O time (67% - 85% of the total time)

It's a caching library for AI applications. Uses node-local storage on compute nodes + near node-local storage on the network for caching on the parallel filesystem. Distributed hashing is used to determine the cache location.

All items during training are traversed one time for each epoch. Between epochs items are shuffled. 
- Within the DL job we have high shareability of I/O (several passes over the same data (cache friendly)). 
- Random access pattern for each epoch is bad. 
- The random sequence order is not correlated with accuracy, therefore I/O is substitutable.

HVAC uses a client-server architecture. 
- The server uses node-local storage across the compute nodes, spawns a dedicated data mover thread managing a shared FIFO queue for I/O requests (aggregated shared cache layer on node local storage).
- The client intercepts I/O calls and registers and sends them to the server. 