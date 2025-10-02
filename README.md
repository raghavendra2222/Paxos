Paxos Implementation

This repository contains a Go implementation of Single-Decree Paxos for distributed consensus. The primary goal of the project is to implement the Paxos algorithm to reach agreement on a sequence of values across multiple distributed peers, ensuring fault tolerance and consistency.

Project Overview

The project implements the Paxos protocol, specifically focusing on single-decree Paxos. The protocol is designed to achieve consensus in a distributed system by allowing a set of peers (servers) to agree on a single value (the "decree") for each sequence number. The Paxos protocol ensures that a value is chosen (decided) by a majority of peers, even if some peers may fail or messages get lost.

Key Features:

Proposer: Initiates the agreement process by proposing a value for a given sequence number.

Acceptor: Responds to proposals, accepting them if they meet certain conditions.

Learner: Learns the agreed value once the consensus has been reached.

Concurrency: Supports agreement on multiple instances of Paxos (i.e., different sequence numbers) at the same time.

Memory Management: Implements a mechanism to forget instances that are no longer needed to free memory.

RPC-based Communication: Peers communicate via RPC calls to coordinate and agree on values.

Methods to Implement

The following methods need to be implemented for the Paxos protocol to work:

paxos.Make(peers []string, me int): Constructor for initializing a Paxos instance.

paxos.Start(seq int, v interface{}): Initiates the agreement for a sequence number seq with proposed value v.

paxos.Status(seq int) (fate Fate, v interface{}): Returns the current status of a sequence number seq.

paxos.Done(seq int): Indicates that the instance seq can be forgotten.

paxos.Max() int: Returns the highest sequence number known.

paxos.Min() int: Returns the smallest sequence number that can be forgotten.

Installation
Prerequisites

Go version 1.18 or later.

go test command for testing.

Setting Up the Project

Clone this repository to your local machine:

git clone https://github.com/your-username/paxos.git
cd paxos


Install the necessary Go dependencies (if any) and compile the project.

Running Tests

To run the provided test suite, navigate to the paxos folder and run:

go test


The tests will verify that your implementation of Paxos works correctly across various scenarios, including different proposals, network partitions, and the handling of forgotten instances.

Expected Test Output

If your implementation is correct, you will see output similar to the following after running all tests:

Test: Single proposer ...    
... Passed
Test: Many proposers, same value ...
... Passed
Test: Many proposers, different values ...
... Passed
Test: Out-of-order instances ...
... Passed
Test: Deaf proposer ...
... Passed
Test: Forgetting ...
... Passed
Test: Lots of forgetting ...
... Passed
Test: Paxos frees forgotten instance memory ...
... Passed
Test: Many instances ...
... Passed
Test: Minority proposal ignored ...
... Passed
Test: Many instances, unreliable RPC ...
... Passed
Test: No decision if partitioned ...
... Passed
Test: Decision in majority partition ...
... Passed
Test: All agree after full heal ...
... Passed
Test: One peer switches partitions ...
... Passed
Test: One peer switches partitions, unreliable ...
... Passed
Test: Many requests, changing partitions ...
... Passed
PASS
ok      paxos   59.523s

How to Contribute

If you would like to contribute to the project, please fork the repository and submit a pull request with the changes. Ensure that you have passed all the tests before submitting your PR.

Fork the repository.

Make your changes.

Push your changes to your forked repository.

Open a pull request.

Design Notes

Concurrency: Each sequence number is handled concurrently to allow independent progress on multiple instances of Paxos.

Failure Tolerance: The protocol handles network failures and peer crashes gracefully, ensuring that consensus is reached once a majority of the peers agree.

Memory Management: The Done() method is used to discard old instances that are no longer needed, helping free memory.

Efficient Communication: The implementation minimizes the number of messages exchanged between peers to reduce overhead and latency.

Further Reading

Paxos Consensus Algorithm (Wikipedia)

Paxos Made Simple (PDF)

License

This project is licensed under the MIT License – see the LICENSE
 file for details.
