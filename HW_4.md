Question P1.1
1-No
2-Because it assign the new IP address randomly.

Question P1.2
2-Onion Proxy (OP) obtains data from the directory, establishes circuits through the TOR network and manages user application connections.
After obtaining a list of TOR nodes from a directory server, the user's Tor client picks a random series of Tor nodes to the destination server.
OP pre-sets circuits(Usually 3 Onion Routers (OR)) and switches to a new circuit once per minute, ensuring that only a limited number of requets can be connected to each other in the output OR.