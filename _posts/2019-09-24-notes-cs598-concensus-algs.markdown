---
layout: post
title:  "Notes from Fall 2019 CS598 Consensus Algorithms"
date:   2019-09-24 13:40:00 -0500
categories: Notes
published:  true
---

I only attended lectures in the first couple of weeks.

# Intro

Assume the leader is known beforehand, and the leader sent v.

+ Static adversary

    - Corrupted/Faulty participants are fixed beforehand
    
+ Adaptive adversary

    - Adversary can corrupt participants dynamically
    - Faulty participants remains faulty
    - (Modified) Consensus: Forever non-faulty participants agrees

+ Mobile adversary

    - Release faulty participants to be non-faulty


# Byzantine Broadcast:
    
Adaptive Byz. lock-step synchronization under f < n

## Protocol for adaptive crash faults

In each round, broadcast the value I have.
After f_upper+1 round, output v if I receive v, else \bot.
    f_upper is the upper bound on the number of faulty participants.

Validity: trivial
Safety: non-faulty p_i outputs v ==> for all non-faulty p_j output v

    Case 1: p_i receives v in round <= f_upper
    Case 2: p_i receives v in round = f_upper + 1
        Because at least f_upper + 1 participants saw the message v
    
Complexity:

- Time/Latency: `f_upper + 1` round
- Message: `n^2 * (f + 1)`


## Byzantine Crash

1. Sender injects many values
2. inject arbitrary delay

Additional Rule:
    Each participant adds its sig to the message.
    A message received in round r is valid iff
        it carries r distinct sigs /\ first sig belongs to the sender

Modified Protocol with following validation:
    Extract v if receive a valid message (Check if there are enough distinct sigs)

Safety: At least one in the previous f_upper + 1 participants was non-faulty


## Handling many values

Modified Protocol:

In each round, if I receive a valid msg containing v for the first time, extract v.
    sign msg and send to all.
Relay at most two messages

After f_upper+1 round,
    let V be the set of v being extracted
    if |V| = 1 and V = {v} singleton, output v
    otherwise \bot.


Complexity:

- Time/Latency: `f + 1`
- Message: `2 * n^2 * f * |sig|` where `|sig|` is the length of a signature

## Lower bound

f_upper + 1 rounds are necessary for deterministic protocols.
(Not necessarily true for probabilistic protocols.)

for crash, lock-step sync, and Boolean output

Failure-sparse: at most one crash per round

Valency:

A configuration in
0-valent: in all configs reachable from C, non-faulty output 0
1-valent: in all configs reachable from C, non-faulty output 1

univalent: 0-valent \/ 1-valent
bivalent: ~univalent

Example:

    Broadcast in which sender has input 0 (\bot)
    has uni-valent (0-valent) initial config
    
    Broadcast in which sender has input 1
    has bi-valent initial config

### Proof of Lower Bound

\E initial bi-valent config => \E bi-valent (round - 1) config

Proof by induction:

Base case:

C^0_0: all n participants have 0
C^i_0: first (n-i) have 0, rest i have 1
C^n_0: all n participants have 1

Assume for all i, C^i_0 is uni-valent
Exists i, C^i_0 is 0-valent /\ C^{i+1}_0 is 1-valent.
If a participant having 0 crashes in C^i_0, C^i_0 should output 1.
Proof by contradiction.

Inductive case:

By hypothesis, exists C_{k-1} is a bivalent round (k-1) config where k < f_upper
Assuming that for all C_k are uni-valent,
=>   C+_k 0-valent s.t. C_{k-1} transits to C+_k without a crash
  /\ C-_k 1-valent s.t. C_{k-1} transits to C-_k with node P fails to send to {j_0,...,j_m}
  /\ for all Ci_k univalent s.t. C_{k-1} transits to Ci_k with node P fails to send to {j_0,...,j_i} where i < m
=> Exists i, Ci_k is 0-valent /\ C{i+1} is 1-valent
=> Exist P' crashes Ci_k and Ci_k can eventually output 1
=> Ci_k is not univalent
Proof by contradiction.


# Mitigating Lower Bound

- Early stopping
- Randomization
- Amortization


# Expected O(1) bound with randomization

## Assumptions

- Synchronous
- Authenticated
- n = 2f + 1
- Static adversaries only

## Leader based approach for n = 3f + 1

- Two Phase: Propose then vote

Note: Dolev-Strong is not leader based. Every participant acts the same.

- A Byzantine leader cannot break safety

    - Quorum intersection:
      at least f + 1 participants has to vote for both which is more than f faulty participants.

- A Byzantine leader can break liveness

    - Simply not propose

- A Byzantine leader can still cause some participants to commit but others not

    - By not sending vote to some participants so there is not enough votes

## Non-simultaneous Commit
- Commit != Terminate

    - Need to keep participating to ensure enough votes

## Commit Adopt

- If a node committed, send the votes it received as proof to notify/convince all other nodes.

    - lock on the vote and do not commit to new value
    - remain silent if the leader proposes different value in future iterations

## Subtlety in Lock Updating

- Ignore ill-timed messages.

    + At status update stage, only leader cares about the certificate received.
      Other nodes should disregard the certificates.
    + At propose stage, all nodes only consider message sent by leader.
      Message sent by other nodes should be ignored
This assumes leader for each round is known/predefined for each node.


## When does the system become univalent

+ Static adversary

    - After honest leader finishes status stage

+ Adaptive adversary

    - After leader remains honest after finishing **vote** stage
    - After finishing **propose** stage, ie., before **vote** stage,
      leader can become corrupted and still mess up equivocation check

Note: when leader becomes corrupted in **vote**, it is indistinguishable from a non-leader Bzt. node.


# Other consensus problem definitions

## Total Order Broadcast (Atomic Broadcast)

Input: all parties can send values

Safety: all honest parties decide on the same sequence of values (ledger, blockchain)

Liveness: every value sent by honest parties gets decided

Note: validity notion is left to upper layer to define.
      No clients.


### Naive Solution (Rotating Leader)

for i in 1, 2 ,3, ...
    Run Byzantine Broadcast to agree on slot i
        with party (i % n) as the sender


### Stable Leader Approach

Steady State: always the same leader proposes

View Change: When enough blames are cumulated (f + 1 blames)
             Replace the leader
             Enter status stage in Byz. Broadcast


## State Machine Replication (SMR)

Typically implement using total order broadcast

Input: all clients can send values
Safety: all honest servers/replicas decide on the same sequence of values

    - Replicas also have to convince clients of the consensus decisions

Liveness: every value eventually is committed


# Communication Complexity

Lower Bound for deterministic Broadcast:

    Need bits Omega(n) of comm. (Trivial)
        tight for crash
    Need Omega(f^2) messages for Byz. [Dolev Strong]
        tight for Dolev Strong when f is Theta(n)

Omega(n^2) Byz. Broadcast => Omega(n^2) Byz. Agreement
The other direction is uncertain unless there is a O(1) reduction from BA to BB.


Thm. in any deterministic BB protocol
    non-faulty parties collectively send at least (f/2)^2 messages.

Proof. assume the theorem is false

Scenario 1: sender is honest. sends v != \bot
    Corrupted set of parties B with |B| = f/2
    All parties in B do not send messages to each other
    Each b in B ignores the first f/2 messages
    Exists p in B, p receives < f/2 messages base on the assumption

Scenario 2: A(p) := those who attempt to send p messages in Scenario 1
    |A(p)| < f/2

    Corrupt A(p), B\{p} with combined size (f-1)
    B\{p} behave like in Scenario 1 and ignore messages from p
    A(p)  behave like in Scenario 1 but do not send to p

Claim: Scenario 1 and 2 are indistinguishable to parties in A\A(p)

    B\{p}: B\{p} behaves the same
    A(p): A(p) behaves the same towards A\A(p)
    p: p receives no messages even following the protocol

In Scenario 2,
A\A(p) output v != \bot
p outputs \bot


No signature => Omega(n^2) bits, tight for f < n/3
signature => Omega(n^2*|sig|) bits

Dolev-Strong: O(n^2) with each message n*|sig| length

Multi sig:
    Aggregate n signatures into one string Sigma with the length the same as one signature
    Also need to aggregate n public keys into one aggregated public key PK

    Verify(PK, Sigma, msg, list) now needs an extra argument, the list of nodes

Threshold sig:
    Verify(PK, Sigma, msg)
        return True if enough nodes signed
        return False otherwise


## Randomize

Static Adv: pick k parties randomly to vote
    f < (1/2-error) * n
    k out of n has honest majority with probability e^{-Theta(k)}
    

# Bounds on number of faulty nodes

Non-Lockstep and Lockstep Synchrony:
    Crash:
        Broadcast: f < n (Dolev-Strong)
        Agreement: f < n
        Total Order Broadcast: f < n
        State Machine Replication: f < n
    Byz:
        W/o Sig: f < n/3
        With Sig:
            Broadcast: f < n (Dolev-Strong)
            Agreement: f < n/2
            Total Order Broadcast: f < n
            State Machine Replication: f < n/2

n = 2f, 

Let P and Q be two sets |P| = |Q| = f

Scenario 1.
    P is honest with input v
    Q is Byz but behaves honestly as if input is v'!=v

    P should output v (validity)

Scenario 2.
    Q is honest with input v'
    P is Byz but behaves honestly as if input is v

    Q should output v' (validity)

P and Q cannot distinguish Scenario 1 and 2, but the output differs. Contradiction


# Asynchronous

Fisher-Lynch-Paterson proof (FLP).
Thm. No deterministic asynchronous BA protocol can tolerate one crash fault node

Event e: a message m arrives ar a node *P*, denote as m -> p

If e1 and e2 are applicable to a configuration C,
    then they do not trigger each other.
If e1 and e2 are applicable to a configuration C
    and they have different recipients, then
    (1) they cannot be ordered
    (2) they can be applied in an arbitrary order (Lemma 1)

Lemma 2. There exists a bi-valent initial configuration.
Lemma 3.
    Let C be a bi-valent configuration, e an event applicable to C,
    Let *E* a set of configs reachable from C (including C) without applying e
    Let *D* a set of configs reachable from C after applying e to *E*
    then *D* contains at least one bi-valent configuration

Proof of Lemma3.
Assume there is no bi-valent configuration in *D*
1. Exists F0 and F1 in *D* that F0 is 0-valent and F1 is 1-valent
2. Exists neighboring C* and C** in *E* (C* can reach C** in one event e')
   s.t. C* -e-> D0 and C** -e-> D1
   Because *E* should be a connected graph and can be partitioned into
        one set going to 0-valent and the other set going to 1-valent
        there must be neighboring configurations on the border of the partition.
Since D0 and D1 cannot transit to each other,
    e and e' must have the same recipient p. (Otherwise, D0 can transit to D1 via e')
We cannot distinguish if p is slow or p crashed.


Randomization (for BA, TOB, SMR)
    crash: f < n/2
    Byz: f < n/3


# Partial Synchrony

## Paxos

Partial Synchrony:
    After some unknown time, Global Synchronization Time (GST),
    a known synchronous bound Δ holds forever.

    Or equivalently, there exists an unknown message delay bound Δ


Status-Propose-Vote
quorum intersect, lock ranking

Let n = 2f + 1, k is the view/ranking

Leader                   Followers
(new-views, k)      -->  Enter view k
                    <--  (status, k, v_lock, k_lock)
receiving f+1 status
find v w/ max k_lock 
(propose v, k)      -->  if still in view k:
                    <--     (vote, v, k)
received f+1 votes          lock on v, k
commit v
(success, v, k)     -->  upon receiving success, commit v


Safety:
    if a node commits v in view k, no proposal for v'!=v in views k'>k
Proof 1:
    1 commit => f+1 nodes lock on v
    => Leader k+1 collects f+1 status, at least one lock on (v, k)
    => Leader k+1 proposes v
    Proof by induction
Proof 2:
    1 commit => f+1 nodes lock on v
    Let k' be the smallest view in which leader proposes v'!=v
    => f+1 (status,k',v',k_lock) where k_lock < k'
    By quorum intersection, this is impossible.
    Proof by contradiction

Liveness:
    Eventually a leader is guaranteed to finish a view in 5Δ time

## Multi-Paxos

State Machine Replication with f < n/2 crashes in partial synchrony

steady state  vs  view change

Leader adds more info about the slots it committed in the new-view message.
Followers compare the slots and can optimize.
