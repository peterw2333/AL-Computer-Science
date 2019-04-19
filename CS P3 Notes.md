

# 3.1 Data representation 

## 3.1.1 User-defined data types

### Why user defined type is necessary?

For any reasonably **large program** it is likely that their use will make a program **more understandable and less error-prone**.

### Non-composite data types

A **non-composite** type is a <u>single data type</u> that does not involve a reference to another type.

An **enumerated** data type is **a list of possible data values**.

```CIE
TYPE TDays = (Sunday, Monday, Tuesday, Wednesday, Thursday, Friday, Saturday)
TYPE StudentID = 1..3999 // means 1 to 3999
DECLARE Startday: TDays
Startday <- Monday
```

Note that the value of a enumerated type is **not strings**. They are ordinal, which means they have an implied order of values. So you can do this:

```
TYPE
TDays = (Sunday, Monday, Tuesday, Wednesday, Thursday, Friday, Saturday)
Day1 <- Sunday
Day2 <- Monday
```

And the value of `Day1 < Day2` is `TRUE`.

A **pointer** is whole number, which acts as a reference of a memory location

Declare a pointer type:

```
TYPE 
MyPointer = ^INTEGER
```

Usage:

```
DECLARE IntP: MyPointer
DECLARE IntVal: INTEGER
DECLARE Temp1: INTEGER
DECLARE Temp1: INTEGER

IntVal <- 97
IntP <- @IntVal // assigns the address of IntVal to IntP
Temp2 <- IntP^ // assigns the value in the address pointed to by IntP to Temp2
IntP^ <- Temp1 // assigns the value of Temp1 to the address pointed by IntP
```

### Composite data types

a **composite** type is a data type constructed from other data types.

**record**: collection of **related** items.

Format:

```
TYPE <Identifier>
	DECLARE <Identifier1> : <Type1>
	......
ENDTYPE
```

Example:

```
TYPE Student
	DECLARE FirstName : STRING
	DECLARE LastName : STRING
	DECLARE StudentNumber : INTEGER
ENDTYPE

DECLARE Stud1 : Student
Stud1.FirstName <- "Razia" // when accessing elements of a record, we use the dot notation
```

**Set** stores a finite number of different values that have no order and supports mathematical operation.

A **class** or **structure** gives the properties and methods of an object.

## 3.1.2 File organisation and access

**Serial access**: When data is stored with no particular order (normally chronological).

**Sequential access**: Data arranged in a particular order

**Random access**: Data placed randomly, may be scattered in different places.

|            | Serial                                   | Sequential                               | Random                                   |
| ---------- | ---------------------------------------- | ---------------------------------------- | ---------------------------------------- |
| Search     | Searching through the file until reaching the desired data. | Searching through the file until reaching the desired data. | Use a hashing algorithm to calculate the address, then find the file directly (A small-scale search may be needed) |
| Alter      | Unable to perform.                       | Create a new copy of the file, copy all data before the element, **add the altered element**, and copy all data after the element. | Use a hashing algorithm to calculate the address and delete the original data. Calculate the address of the new value and place the data to the new address. |
| Delete     | Unable to perform.                       | Create a new copy of the file, copy all data before the element, **skip the deleted element**, and copy all data after the element. | Use a hashing algorithm to calculate the address, then delete the original data. |
| Access all | Access data in chronological order.      | Access data sequentially.                | Access data one by one.                  |

Sequential organisation requires a **key field** to allow files to be ordered. The difference between **key field** and **primary key** is that key field must not only be unique but also in order.

### Reason for choosing **serial** file organization:

- In the case of small file, sequential access is not very slow.
- Easy to append a record at the end of a file, no need for re-sorting.



## 3.1.3 Real numbers and normalised floating-point representation

A floating point number consists of two parts: **mantissa** and **exponent**.  Each part has a pre-defined length.

Both parts are in binary and **two's complement form**.

The decimal point is defaulted between the first and second digit.

Examples: (6-bit mantissa and 4-bit exponent)

1. 0.10011 0011 = 100.11

2. 0.10011 1100 = 0.000010011

3. 1.00010 0010 = 110.010 = -11.11

4. 1.10010 1101 = 1.111001 = -0.000111

   Note: when encountering **negative mantissa and exponent**, **add 1's** to the left side.

### Normalisation

The first two digits of mantissa should be **0.1 for positive number or 1.0 for negative number**.

Ex1. 0.01000  0010 -> 0.10000 0001

Ex2. 1.111111010 000011 -> 1.010000000 111101

The reason of normalisation is to **make sure each denary number has only one representation** in floating point.

### Allocation of bits

**More bits for mantissa**, higher accuracy, lower range.

**More bits for exponent**, lower accuracy, higher range.

### Underflow and overflow

**underflow** happens when the result is **too small** to represent.

**overflow** happens when the result is **too large** to represent.

### Rounding errors

In such programming there is a slight approximation in recording the result of each calculation. These so-called **rounding errors** can become significant if **calculations are repeated** enough times. The only way of preventing this becoming a serious problem is to **increase the precision** of the floating-point representation by **using more bits for the mantissa**. 



# 3.2 Communication and Internet Technologies

## 3.2.1 Protocols

A **protocol** is a set of rules that governs communication devices in a network and must be agreed between a sender and receiver.

**Port number** - the final destination of communication.

| Port number | Protocol                             |
| ----------- | ------------------------------------ |
| 21          | File Transfer Protocol (FTP)         |
| 25          | Simple Mail Transfer Protocol (SMTP) |
| 80, 8080    | HyperText Transfer Protocol (HTTP)   |
| 110         | Post Office Protocol v3 (POP3)       |

**Socket** – This is the IP address plus the Port number

- A protocol is made up of several modules, each of which is responsible for a certain subtask. All the modules together complete the main task and form the protocol. 
- The idea of dividing a protocol into subtasks can be viewed as a stack structure where each subtask is an individual block.
- Individual protocols within a suite are often designed with a **single purpose** in mind. This [modularization](https://en.wikipedia.org/wiki/Modularity_(programming)) makes design and evaluation easier. 
- Because each protocol module usually communicates with **two others**, they are commonly imagined as [layers](https://en.wikipedia.org/wiki/Abstraction_layer) in a stack of protocols. 
- The lowest protocol always deals with low-level interaction with the communications hardware. Every higher layer adds more features and capability.

## TCP/IP

### TCP - Transmission Control Protocol

TCP is responsible for **breaking data down into small packets** before they can be sent over a network, and for **assembling packets** when they arrive.

#### role of TCP:

- allows applications to exchange data 
- establishes and maintains a connection 􏲬until exchange of data is complete 
- determines how to break application data into packets 
- adds sequence / packet number to (TCP) header 
- sends packets to and accepts packets from the network / Internet layer 
- manages flow control // manages congestion avoidance 
- acknowledges all packets that arrive 
- detects when a packet has not arrived at destination 
- handles retransmission of dropped packets 
- reassembles packets into the correct order 

### IP - Internet Protocol

IP takes care of the **communication** between computers.

It is responsible for **addressing, sending and recieving** the data packets over the Internet.

### Role of IP:

- routes the packets around the network 
- adds to the IP header a source/destination address for each packet 
- encapsulates data into datagram 
- passes datagram to the network access layer (for transmission on the LAN)// passes datagram to the transport layer (on arrival at destination) 
- Defines the addressing method e.g. subnetting, NAT

| Layer                                     | Functionality                                                | Protocols                                                    |
| ----------------------------------------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| Application Layer                         | The scope within which applications create user data and communicate this data to other applications on another or the same host | HTTP, FTP, SMTP                                              |
| Transport Layer                           | Performs host-to-host communications on either the same or different hosts and on either the local network or remote networks separated by routers | TCP, UDP (User Datagram Protocol)                            |
| Network Layer (Internet Layer)            | Exchanges datagrams across network boundaries                | IP, ICMP (Internet Control Message Protocol), IGMP (Internet Group Management Protocol) |
| Data Link Layer (Network Interface Layer) | Defines the networking methods within the scope of the local network link on which hosts communicate without intervening routers | ARP (Address Resolution Protocol) and PPP (Point to Point Protocol) |

The data is transferred from the application layer on one computer to that of another computer, therefore, the sequence of data transmission is first going down and then going up.

#### Sender Side:

1. **Application Layer** Encodes the data in an appropriate format.
2. **Transport Layer** breaks data down into smaller chunks known as packets

3. **Network Layer** adds IP addresses (sender and receiver) and a checksum to the header

4. **Data Link Layer** Formats the packets into a frame. These protocols attach a third header and a footer to “frame” thepacket. The frame header includes a field that checks for errors as the frame travels over the network media.

5. **Physical Layer** receives the frames and converts the IP addresses into the hardware addresses appropriate to the network media. The physical network layer then sends the frame out over the network media.

 Service Provider re-routes the packets according to the IP address.

#### Reciever Side:

1. **Physical Layer** receives the packet in its frame form. It computes the checksum of the packet, and then sends the frame to the data link layer.

2. **Data Link Layer** Verifies that the checksum for the frame is correct and strips off the frame header and checksum. Finally, the data link protocol sends the frame to the Internet layer.

3. **Network Layer** reads information in the header to identify the transmission and determine if it is a fragment. If the transmission was fragmented, IP reassembles the fragments into the original datagram. It then strips off the IP header and passes it on to transport layer protocols.

4. **Transport Layer** reads the header to determine which application layer protocol must receive the data. Then TCP strips off its related header and sends the messageor stream up to the receiving application.

5. **Application Layer** receives the message and performs the operation requested by the sender

## BitTorrent Protocol

It uses the **peer-to-peer** model, while downloading a file from a server uses the client-server model.

**Peer-to-peer model**: When 2 or more computers are connected and share resources without going through a separate server computer.

When a lot of people are downloading a single resource from a server, it is likely that the speed will become slow as people are using the same resource. While the BitTorrent solves this problem by **making everyone a source** (downloading and uploading at the same time).

**BitTorrent Protocol**: a protocol allowing you to download files quickly by **allowing other people** downloading the file to **upload** (distribute) parts of it **at the same time**.

**Tracker**: central server that:
stores details of other computers that have all / part of file to be downloaded;
has data on those peers downloading and uploading file;
shares IP addresses with other clients in swarm, allowing them to connect.

**Seed**: <u>peer computer</u> that has 100% of file // is uploading downloaded content

**Swarm**: all the connected peer computers that have all or part of the file to be downloaded / uploaded // share a torrent

**Leeches** : refers to a peer (or peers) that has a negative effect on the swarm by having a very poor share ratio, downloading much more than they upload.

## HTTP, FTP, POP3 and SMTP

### HTTP

HTTP allows users on the web to **exchange information found on webpages**.

**Transaction-oriented**, **client-server** protocol. 

It involves the client sending a '**request**' message and the server sending back a '**response**' message. 

The HTTP protocol defines the **format** of the message. 

The sequence of protocol actions :

1. HTTP transmits a request message to TCP.
2. TCP creates one or more packets and sends the first one to IP using port 80 for the destination port and a temporary port number for the sending port.
3. IP uses the URL in the message to get an IP address using DNS and sends a datagram. 
4. At the server, IP forwards the datagram to TCP.
5. The server TCP sends an acknowledgement.
6.  When a connection has been established, TCP sends the remaining packets, if any, to IP which then forwards them through the server IP and TCP to the server application layer.
7.  HTTP transmits a response message which is transmitted via TCP, IP, IP and TCP to the client browser application.
  

### FTP

FTP is a standard network protocol used to **copy a file** from one host to another over a TCP/IP-based network, such as the **Internet**.

- Uploading an image from your PC to a website.
- File transfer over Skype

**Server**: central computer which stores files that are to be downloaded

**Command**: user can send action/instruction (or by example, e.g. change directory) that are carried out on server 

**Anonymous**: allows user to access files without identifing themselves to server

### SMTP & POP3

SMTP is a "**push**" protocol for sending and transferring emails, while 

POP3 is a "**pull**" protocol for recieving emails.

**Example**:

  - Transfer email from one email server to another email server
  - Send email to the email server
  - Email client download an email from the email server

## 3.2.2 **Circuit switching, Packet switching, and routers**

### Circuit Switching

**Circuit Switching**: Path is set up in advance of transmission

Before communication can occur between two devices, a **circuit is established** between them.

Once set up, **all** communication between these devices takes place over this circuit, even though there are other possible paths that data could be passed over the network of devices between them.

After the transmission finishes, the circuit is **terminated**.

#### Application

- Telephone system: when A calls B, a circuit is established between them before they can start talking. After the call the circuit is terminated.
- Video-conferencing: video and audio must arrive at the same time, so circuit switching must be used.

#### Advantages

- The dedicated path/circuit established between sender and receiver provides a guaranteed data rate.
- Once the circuit is established, data is transmitted without any delay as there is no waiting time at each switch.
- Since a dedicated continuous transmission path is established, the method is suitable for long continuous transmission.

#### Disadvantages

- As the connection is dedicated it cannot be used to transmit any other data even if the channel is free.
- It is inefficient in terms of utilization of system resources. As resources are allocated for the entire duration of connection, these are not available to other connections.
- Dedicated channels require more bandwidth.
- Prior to actual data transfer, the time required to establish a physical link between the two stations is too long.

### Packet switching

**Packet Switching:** Data is divided into small packets before they are sent over network.

In Packet Switching, no specific route is used for data transfer. 

Instead, the route that a packet takes is decided by the router on the basis of efficiency.

The time taken for each packet to travel to the destination may vary, because:

1. The route taken by packets are different
2. A lot of data may be travelling through a node, which means a packet have to wait in the queue.

#### Advantages

- Efficient use of network: when a switch is used by one user, it is still available for other users.
- If a packet is corrupted, only that packet needs to be resend.
- Packet Switching use digital network and enables digital data to be directly transmitted toward destination.
- Any disruption in the network can be circumvent by re-routing.

#### Disadvantages

- In Packet Switching Packets arriving in wrong order.
- Takes Transmission delay.
- Processing power is required to reconstruct packets
- Packets may be lost on their route, so sequence numbers are required to identify missing packets.

#### Packet switching steps

1. Data is split into packets 
2. Each packet has a source address, destination address and payload (data packet) 
3. If data requires multiple packets, then the order of each packet is noted 
4. Packets sent onto the network, moving from router to router taking different paths (set by the router). Each packet’s journey time can therefore differ. 
5. Once the packets arrive, they are re-ordered 
6. Message sent from recipient to sender indication that the message has been received 
7. If no confirmation message received, sender transmits the data again. 

### The function of a router

A router **connects** multiple networks and **forward** **packets** destined either for its own networks or other networks.

A router connects to many **other routers** and it decides which of them it should send the packet to.

A router uses a **routing table** to decide which node it should forward the message to. The routing table contains:
- Information on which connections lead to a particular groups of addresses
- Priorities for connections to be used
- Rules for handling both routine and special cases of traffic



## 3.2.3 Local Area Networks (LAN)

A **computer network** is a collection of computing devices that are connected in various ways to
communicate and share resources.

A **local-area network (LAN)** connects network devices over a relatively short distance.

#### LAN techonologies

- Ethernet
- Fibre optic
- Token ring

Advantage of LAN:

- Easily accessible

- Quick way of communication

- Lower delay than transmitting over a WAN.

Disadvantage of LAN:

- TBD

### Bus Topology

**Bus topology** is a specific kind of network topology in which all of the various devices in the network are connected to a single cable or line.

The "bus" usually have two terminators at each end.

In a bus network, every station receives all network traffic, and the traffic generated by each station has **equal transmission priority**.

#### Advantages:

- easy to set up
- low cost

#### Disadvantages:

- If the central line is broken the entire network will breakdown
- Two devices cannot transmit data at the same time
- If the backbone cable is long, may cause signal loss

### Star Topology

**Star topology** is a network topology where each individual piece of a network is attached to a central node (a hub, switch or router).

Clearly, a star topology network must have a **central device**.

Each connection must be **bidirectional**.

Each node has a **dedicated connection** to another node.

Nodes may operate under **different protocols**, and a router can act as the translator.

#### Advantages:

- Signal not transmitted to every terminal of the network
- Easy to add and remove network component
- Failure of a node or a link does not affect the rest of the network

#### Disadvantages:

- If central device fails, the whole network breaks down
- The inclusion of a central device increases the overall cost of the network
- Performance of the network is dependent on the central device



### Wireless Network

Wireless network uses RF frequency to transmit data. 

Each wireless network is based on an **access point**.

The primary job of an access point is to broadcast a wireless signal that computers can detect and “tune” into.

An access point usually also serves as a link to the resources on a wired network, such as the Internet.

####Advantages:

- Easier, faster and cheaper to set up

#### Disadvantages:

- Information can be easily spied

### Hardwares Supporting a LAN

#### Switch

A **network switch** is a device that connects devices together on a computer network, by using packet
switching to receive, process and forward data to the destination device.

Unlike hubs, a switch only forwards data to the devices that need to recieve it.

#### Router

**Router** is a device that acts as a node in the internet.

Each router builds up a **routing table** listing the preferred routes between any two systems on the interconnected networks.

Routing table has entry for associated network ID and host address in the network. The router uses the routing table to make decision about where to forward data packet.

#### Server

A **server** is a computer or a device on a network that provides data to other computers on the same network.

##### Types of servers:

 - **file server**: a computer dedicated to storing files
 - **print server**: a computer that manages one or more printers
 - **network server**: a computer that controls network traffic
 - **database server**: a computer that processes database queries.

#### Network Interface Cards (NICs)

A NIC is a card that physically makes the connection between the computer and the network cable. 

It enables a computer to connect to a network; such as a home network, or the Internet using an Ethernet cable.



### CSMA/CD

The **carrier-sense multiple access with collision detection (CSMA/CD)** describes how the Ethernet protocol regulates communication among nodes

**Carrier sense**: attempt to transmit data when the medium is idle (no transmission taking place)

**Multiple access**: each node is competing for the medium

**Collision detection**: when a collision is detected, attempt to send no more packets

- only allow data to be sent when the line is idle 
- to detect a collision on the network 
- to halt transmissions when a collision occurs 
- calculates random wait time 
- allow retransmission after a random amount of time 



# 3.3 Hardware

## 3.3.1 **Logic gates and circuit design**

### Half Adder

A **half-adder** is a combinational arithmetic circuit block that can be used to add 2 bits. Such a circuit thus has 2 inputs that represent the 2 bits to be added and 2 outputs, with one producing the **SUM** output and the other producing the **CARRY** output.

#####Truth Table:

| A    | B    | S    | C    |
| ---- | ---- | ---- | ---- |
| 0    | 0    | 0    | 0    |
| 0    | 1    | 1    | 0    |
| 1    | 0    | 1    | 0    |
| 1    | 1    | 0    | 1    |

### Full Adder

A *full-adder* circuit is a combinational arithmetic circuit block that can be used to add **3 bits** to produce a **SUM** and **CARRY** output. 

#### Truth Table:

| A    | B    | Cin  | Cout | S    |
| ---- | ---- | ---- | ---- | ---- |
| 0    | 0    | 0    | 0    | 0    |
| 0    | 0    | 1    | 0    | 1    |
| 0    | 1    | 0    | 0    | 1    |
| 0    | 1    | 1    | 1    | 0    |
| 1    | 0    | 0    | 0    | 1    |
| 1    | 0    | 1    | 1    | 0    |
| 1    | 1    | 0    | 1    | 0    |
| 1    | 1    | 1    | 1    | 1    |

While adding larger binary numbers, we also consider the carry bit from the last 2 binary numbers. 

A **full-adder** is therefore essential for the hardware implementation of an adder circuit capable of adding larger binary numbers. 

## 3.3.2 Boolean algebra

*In this chapter, we use CIE notation for boolean operators: $+$ for $\or$ (or), $.$ for $\and$ (and), and a horizontal bar for $\not$ (not)*

A **variable** is a symbol used to represent a logical quantity. Any single variable can have a **“1”** or a **“0”** value.

The **complement** is the inverse of a variable and is indicated by a bar over the variable. The complement of a variable is **not considered as a different variable.**

Every occurrence of a variable or its complement is called a **Literal**. It could be its true form
or its complement, both of them are called Literals.

Any logic circuit, no matter how complex, may be completely described using the Boolean operations previously defined. Because the **OR** gate, **AND** gate, and **NOT** gate are the basic building blocks of digital circuits.

### Laws of Boolean Algebra

#### Commutativity

Both boolean **addition** and **multiplication** are **commutative**.

$A+B=B+A$ and $A.B=B.A$.

#### Associativity

Both boolean **addition** and **multiplication** are **associative**.

$A+(B+C)=(A+B)+C$ and $(A.B).C=A.(B.C)$.

#### Distributivity

$A.(B+C) = A.B+A.C$

#### Operations with 0 and 1

$0+X=X, 1+X=1, 0.X=0, 1.X=X​$

#### Idempotent

$X.X.X.X.\cdots.X=X+X+X+\cdots+X=X$

#### Complementation

$X+\overline X=1​$

$X.\overline{X}=0​$

#### Involution Law

$\overline{\overline{X}}=X$

#### Absorption Law

i) $X+X.Y=X$

ii) $X.\overline{Y}+Y=X+Y$

iii) $(X+Y)(X+Z)=X.X+X.Y+X.Z+Y.Z=X+Y.Z$ (by (i))



### De Morgan's Law

a) $\overline{X_1+X_2+X_3+\cdots+X_n} = \overline{X_1}.\overline{X_2}.\overline{X_3}.\cdots.\overline{X_n}​$.

b) $\overline{X_1.X_2.X_3.\cdots .X_n} = \overline{X_1}+\overline{X_2}+\overline{X_3}+\cdots+\overline{X_n}$.



#### two-terms

$\overline{AB}=\overline{A}+\overline{B}$ and $\overline{A+B}=\overline{A}.\overline{B}$ (note that $\overline{AB} \neq \overline{A}.\overline{B}$!)



This law is useful when simplifying statements including multiple layers of bars. 

#### Example 1:

$\overline{A+\overline{BC}} = \overline{A}\overline{\overline{BC}}=\overline{A}BC​$

#### Example 2:

$\overline{\overline{A+BC}+\overline{A\overline{B}}} = \overline{\overline{A+BC}}.\overline{\overline{A\overline{B}}} = (A+BC).(A\overline{B})=AA\overline{B}+AB\overline{B}C=A\overline{B}$.



## 3.3.3 Karnaugh Maps

略

## 3.3.4 Flip-Flops

*CIE does not distinguish between a flip-flop and a latch.*

A **flip-flop** is a circuit that has **two stable states** and can be used to store information.

In SRAM, each flip-flop is responsible for storing a single bit.

### SR Flip-Flop

**S** stands for set and **R** stands for reset.

All SR flip-flops have an invalid input, which will result in $Q = \overline{Q}$.

A SR Flip-Flop can be implemented using two **NOR-gates** or two **NAND-gates**.

In a **NOR-based** SR flip-flop, the invalid input is $S=R=1$.

In a **NAND-based** SR flip-flop, the invalid input is $S=R=0$.

![image-20190313171754774](/Users/peter/Library/Mobile Documents/com~apple~CloudDocs/学习/Notes/CS/Images/P3/3.3/SR Latch.png)

### JK Flip-Flop

**J** and **K** is after its inventor, Jack Kilby.

A **JK Flip-Flop** consists of a SR Flip-Flop and two interlocked inputs. 

![JK Flip-Flop](/Users/peter/iCloud Drive (Archive)/学习/Notes/CS/Images/P3/JK Flip-Flop.png)

The JK Flip-Flop does not have invalid states. 

Instead, when J and K are both equal to 1, a "toggle" action is performed, which reverses both outputs.

A Clock can be featured (as in diagram), in order to limit changes to the flip-flop only when the clock signal is high.

#### The advantages of JK flip-flop over SR flip-flop:

- SR flip-flop have an invalid combination while JK flip-flop does not.
- SR flip-flop allows outputs to be equal while JK flip-flop does not.
- *The inputs of a SR flip-flop may arrive at different times while JK flip-flop incorporates a clock signal for synchronisation.*
  - *Refer to diagram in the exams!!! Strictly speaking, all flip-flops have clock inputs.*

### Application of Flip-Flop in computer:

- A flip-flop can store either a 0 or a 1 
- Computers use bits to store data 
- Flip-flops can therefore be used to store bits (of data) 
- Memory can be created from flip-flops 



## 3.3.5 RISC Processors

The **instruction set** is the set of basic instructions that a processor understands. 

The instruction set is a portion of what makes up architecture.

### RISC vs. CISC

| RISC                                               | CISC                                         |
| -------------------------------------------------- | -------------------------------------------- |
| Fewer instructions                                 | More instructions                            |
| Many registers                                     | Fewer registers                              |
| Simple instructions                                | Complex instructions                         |
| Few instruction formats                            | Many instruction formats                     |
| Usually use single-cycle instructions              | Use multi-cycle instructions                 |
| Fixed-length instructions                          | Variable length instructions                 |
| Easier pipelining                                  | Difficult pipelining                         |
| Simpler circuits                                   | Complex circuits                             |
| Fewer addressing modes                             | More addressing modes                        |
| More use of RAM                                    | Less use of RAM, more use of cache           |
| Hard-wired control unit                            | Programmable control unit                    |
| Only load and store instructions to address memory | Many types of instructions to address memory |

### Pipelining

Pipelining is **instruction-level parallelism**.

In pipelining, the processor works on **different steps** of the instruction at the same time. 

Therefore more instructions can be executed in a shorter period of time.

For example, If instruction A, B, C, D are to be executed four times, each instruction needs to be fetched, decoded, executed, and finally write result to register. Each of which step requires one time interval. Instead of using $4\times 4 = 16$ time intervals, pipelining can reduce the time required to $7$ intervals.

| Stage                  | 1    | 2    | 3    | 4    | 5    | 6    | 7    |
| ---------------------- | ---- | ---- | ---- | ---- | ---- | ---- | ---- |
| Fetch instruction      | A    | B    | C    | D    |      |      |      |
| Decode instruction     |      | A    | B    | C    | D    |      |      |
| Execute instruction    |      |      | A    | B    | C    | D    |      |
| Write result to memory |      |      |      | A    | B    | C    | D    |

### Interrupt Handling in RISC and CISC

- TBD



## 3.3.6 Parallel Processing

This is **processor-level parallelism**.

| Type of parallel processing | Class of computer                         | Application                             |
| --------------------------- | ----------------------------------------- | --------------------------------------- |
| Pipeline                    | Single Instruction Single Data (SISD)     | Inside a CPU                            |
| Array Processor             | Single Instruction Multiple Data (SIMD)   | Graphic cards                           |
| Multi-Core                  | Multiple Instruction Multiple Data (MIMD) | Supercomputers, modern multi-core chips |
| Pipeline                    | Multiple Instruction Single Data (MISD)   | Rarely implemented                      |

### Advantages

- Faster when handling a large amount of data, with each data set requiring the same instruction (array and multi-core methods)
- Not limited by the bus transfer rate (Von Neumann Bottleneck)
- Maximise use of CPU (pipeline method)

### Disadvantages

- Only certain types of data are suitable for parallel processing. 
  - **data dependency** problem: before the result of previous instruction is stored, it needs to be used by another instruction.
- More costly in terms of hardware



### Massively Parallel Computer

This is **computer-level parallelism**.

#### Characteristics:

- Many separate processors
- A network structure instead of bus structure



#### Code that will be ran on a massively parallel computer needs to be changed:

- Code needs to be split into blocks that can run simultaneously
- Each block is processed by a different processor
- Requires both parallelism and co-ordination



#### Difficulties:

- Communication between different processors
- Each processor needs to be link to a different processor, and there is a large amount of processor, which leads to challenging network topology.



# 3.4 System Software

## 3.4.1 Purposes of an Operating System

An **operating system (OS)** is a set of programs that manage computer resources and run in the background on a computer system, giving an environment in which application software can be executed.

### Responsibilities of the OS:

- Hiding the complexities of hardware from the user. 

- Managing between the hardware’s resources which include the processors, memory, data storage and I/O devices. 

- Handling “interrupts” generated by the I/O controllers 
- Sharing of I/O between many programs using the CPU. 



**System Software**: programs that manage the operation of a computer 

**Application Software**: programs that help the user perform a particular task. 



### User Interfaces

#### Command Line Interface (CLI)

A **command-line interface** allows the user to interact with the computer by typing in **commands**. 

The computer displays a prompt, the user keys in the command and presses the enter button. 



- Commands must be typed correctly and in the right order or the command will not work. 

- Experienced users who know the commands can work out very quickly without having to find their way around the menus. 

- An advantage of command driven programs is that they do not need the memory and processing power of the latest computer and will often run on lower spec machines. 

- A command-line interface can run many programs, for example a batch file could launch half a dozen programs to do its task. 

- An inexperienced user can sometimes find a command driven program difficult to use because of the number of commands that have to be learnt. 



#### Graphical User Interface (GUI)

In a **GUI**, he user chooses an option usually by pointing a mouse at an icon representing that option. 



- Much easier to use for beginners, visually intuitive, more user-friendly. 

- They enable you to easily exchange information between software using cut and paste 

- They use a lot of memory and processing power. It can be slower to use than a command- line interface. 

- They can be irritating to experienced users when simple tasks require a number of operations. 

- Multitasking - multiple windows can be opened at the same time



### Interrupts

An **interrupt** is a signal sent to the processor from a hardware device, indicating that the device requires attention of the processor to take a specified action in precedence. 



#### Types of Interrupt:

- Program interrupt
  - Division by zero 
  - File not found
- I/O interrupt
  - Printer out of paper
  - Keyboard stroke

- Timer Interrupt
  - A process has run out of time
  - Processor must do a pre-set task
- Hardware Interrupt
  - Power failure



#### The steps after a processor receive an interrupt:

1. Save the contents of the program counter **on the stack** 
2. Also save contents of all other registers  
3. Load and run the appropriate Interrupt Service routine (ISR)
4. Restore all other registers 
5. Restore the Program Counter 
6. Continue execution of the interrupted process 



If an interrupt occurs while another interrupt is already being dealt with, 

the simplest way is to place the interrupts in a **queue**, 

and only allow the processor to return to the original program **when the queue is empty**.



### Scheduling

**Multitasking**: executing many programs simultaneously.

**Process:** a program in memory that has an associated process control block.

**Process control block (PCB):** a complex data structure containing all data relevant to the running of a process.

It is possible for a process to be separated into different parts for execution. The separate parts are called **threads.** 

#### Why multitasking is needed:

The computer may have multiple users that need to use it, running different programs at the same time.



Some programs need more IO resources (**IO Bound)**, while some need more processing power (**CPU Bound**).

The most efficient way to run these programs is to let the IO bound program use IO resources while the CPU bound program use CPU resources, and vice versa.



#### Why scheduling is needed:

- to allow multiprogramming 
- to give each process a fair share of the CPU time 
- to allow all processes to complete in a reasonable amount of time 
- to allow highest priority jobs to be executed first 
- to keep the CPU busy all the time 
- to service the largest possible number of jobs in a given amount of time 
- to minimize the amount of time users must wait for their results 
- to maximise the use of peripherals 



To acheive these goals, **several criterias** are used to determine the order in which jobs are executed.

- **Priority.** Give some jobs a greater priority than others when deciding which job should be given access to the processor.
- **I/O or Processor Bound.** If a processor bound job is given the main access to the processor, it could prevent the I/O devices being serviced efficiently. 
- **Type of job.** Batch processing, on-line and real-time jobs all require different response times.
- **Resource requirements.** The amount of time needed to complete the job, the memory required, I/O and processor time.
- **Resources used so far.** The amount of processor time used so far, how much I/O used so far. 
- **Waiting time.** The time the job has been waiting to use the system. 



#### Running, Ready and Blocked States

- Any job is in **one and only one** states of the three.

- Ready and blocked states are **queues** which can hold multiple jobs.
- On a standard, **single-processor** computer, **only one** job can be in running state. 



#### Schedulers

##### High Level Scheduler (HLS)

- To place a job in the ready queue
- to ensure the system is not overloaded

##### Medium Level Scheduler (MLS)

- Swap jobs between the memory and the backing store

##### Low Level Scheduler (MLS)

- Move jobs in and out of ready state
- Decide the order in which jobs are placed in the running state using different **scheduling policies**



#### Scheduling Policies

Scheduling policies can be divided into two categories: **pre-emptive** and **non pre-emptive**.

A pre-emptive scheme allows the LLS to **remove a job from the running state** so that another job can be placed in the running state. 

A non-pre-emptive scheme allows each job to run until it no longer requires the processor. This may be **because it has finished or it needs an I/O device**. 

##### Pre-emptive algorithms

- **First Come First Served (FCFS)**: the first job to enter the ready queue is the first to be executed.
- **Shortest Job First (SJF)**: the job that requires the shortest time to run is the first to be executed.
- **Round Robin (RR)**: each job is given a maximum amount of time (called a **time slice**) in running state before it is put into the back of the ready queue, allowing the next job to be executed. If a job ends before the end of its time slice, it leaves the system.
- **Shortest Remaining Time (SRT)**: The ready queue is sorted by each job's shortest remaining time. **Jobs that requires a long time may be prevented from execution.**
- **Multi-level Feedback Queues (MFQ)**: Includes queues of several priorities, between which jobs are moved. 
  - A job that requires too much time may be moved to a lower-priority queue
  - A job that has waited for a long time may be moved to a higher-priority queue
  - A job that is IO-Bound is favoured and is placed in a high-priority queue.



### Memory Management

#### Partitioning

Each process gets a partition of memory.

The partition can be **dynamic**, so the size of a partition is variable, and is equal to the size of the process.



#### Paging

Each process is further divided into **equal-sized** pages.

Memory is divided into **frames** of the same size, which is equal to the size of a page.

**All pages** of a process is loaded into memory in the same time.



#### Segmentation

Each process is divided into **variable-sized** segments.

Each segment is a dynamic partition.



##### Difference between partitioning and paging/segmentation:

Partitioning requires the memory occupied by a process to be **contiguous**, but paging and segmentation allows pages/segments to be **separated**.



#### Virtual Memory

**Not all pages** are loaded into memory at the same time.

Pages are only loaded when the user needs it.

##### Advantages: 

- Allows a program larger than the memory available to be run
- **Only part of a program** is in the memory at the same time, saves memory space

##### Disadvantage:

- **Disk thrashing**: When pages are requiring each other, and they cannot be loaded at the same time, there will be **perpetual loading and saving of pages**, which occupies a lot of processor time.

##### Page-Replacement Algorithm

A page-replacement algorithm is needed to decide which page is to be swapped in and out of memory.

- First-In-First-Out (FIFO)

- Least Recently Used (LRU)

- Least Frequently Used (LFU)

- Most Frequently Used (MFU)

- Optimal Page Algorithm (OPA): **looks forward in time** to see which page is going to be used and which will not be used.

  

## 3.4.2 Virtual Machine

A **virtual machine** is a process that interacts directly with a software interface provided by the operating system.

A **virtual machine software** is a computer program that **creates a virtual computer system** with **virtual hardware devices**. 

The virtual computer system is called the **guest operating system**, while the system that is running on the real hardwares is called the **host operating system**.



#### When an application on a guest OS requires a file:

1. Guest OS handles request as usual, as if it is running on a physical computer system
2. I/O requests are **translated** by the virtual machine software into **instructions of the host OS**
3. The host OS retrieves data from the file
4. The host OS passes data to the virtual machine software
5. The virtual machine software passes data to guest OS
6. The guest OS passes data to the application



#### Benefits:

- Software can be tried on different OS with the same hardware
- No need to purchase different hardware to run different OS
- Easy to recover if software causes the system to crash
- Protects the host OS from malfunctioning software

#### Limitations:

- VM may not be able to emulate some hardware.
  - *emulate vs simulate: emulate is to duplicate the inner workings, while simulate is to duplicate the behaviour*.
- VM requires the execution of extra lines of code, so it runs slower.
- VM is less efficient.



## 3.4.3 Translation Software

There are three types of translators: 

- **Assembler**: translate assembly language directly into machine code.
- **Interpreter**: translate high-level language **(source code)** line-by-line into equivalent machine code **(object code)**.
- **Compiler**: translate a whole high-level language program into equivalent machine code.



### Compiler vs Interpreter

#### Advantages of compiler:

- No disclosure of source code to user
- Faster execution as no need of translation
- Compiled code can execute alone

#### Disadvantage of compiler:

- Use a lot of resources during compilation process
- Platform-dependent: re-compilation is needed when the same program is to be executed on a different platform
- Difficult to locate the source of error in the source code 



#### Advantages of interpreter:

- Use less resources when interpreting
- Platform-independent: the software can translate the source code into different object code on different platform
- When the program is not complete, part of the source code can still be executed
- Produce an error message as soon as the error is detected

#### Disadvantage of interpreter:

- Code runs slower as:
  - source code needs to be interpreted before execution
  - instructions in a loop needs to be translated each time the program enters the loop
- The source code needs the interpreter to execute
- Source code needs to be disclosed to the user



### Steps of code translation: 

lexical analysis $\to$ syntax analysis $\to$ *semantic analysis* $\to$ code generation $\to$ code optimisation 



#### Lexical Analysis

- Uses the source code to produce **a sequence of tokens**.
  - Each keyword, operator, variable or literal is replaced by a token.

- Add the **names of variable** to a symbol table.

- Removal of spaces, comments and blank lines
- Report obvious errors, such as an invalid variable name



#### Syntax Analysis

- The code generated by the lexical analyser is parsed (broken into small units) to check if it is follows the grammatical rules of the programming language.

The grammar of a programming language is defined in terms of **Backus-Naur Form (BNF)** notation.



#### Semantic Analysis (not required)

- Type checking: checking that variable is of the correct data type
- Make sure that a variable is declared before use, which is impossible to describe in BNF.



#### Code Generation

- Breaking of complex statements into simple statements (**Three Address Codes, TAC**)..

TACs have the following form: `Operand1 := Operand2 Operator Operand3`

For example: `A := (B + C) * D + E` can be broken down to:

```
R1 := B + C
R2 := R1 * D
A := R2 + E
```

`R1` and `R2` are variables used to store intermediate results.

This can also be represented in a **tree format**.



#### Code Optimisation

Code can be improved to increase speed of execution, and/or decrease memory usage. The process of improving the code is called **code optimisation**.



### Backus-Naur Form

**Backus-Naur Form** is a **meta-language** (a language used to describe another language) which describes the <u>syntax</u> or <u>structure</u> of all program statements of a high-level programming language.



`::=` is the definition operator

`< >` encloses a term.

`|` means "or", separates possible values



**Eg.1** `<character> ::= a|b|c`

**Eg.2** `<word> ::= <character> | <word><character>`

Note that this definition is **recursive** (defined in terms of itself).



When checking if a line of code is satifying the rules, each element of it is checked against each term of the corresponding definition, and each term is then checked individually.

###  

###Reverse-Polish Notation (RPN)

Reverse-Polish Notation is a mathematical notation in which **every operator follows all of its operands**.

Therefore, it is also called the **postfix notation**.



#### Advantages: 

- RPN can be processed directly from left to right
- No need to use brackets
- No requirement for the rule of precedence in infix notation (multiplication over addition)
- Use of stack permits the automatic storage of intermediate results for later use, allowing evaluation of expression of arbitrary complexity



#### Evaluation of RPN using stack:

Eg1. `2 3 * 8 + 7 /`

Stack:

```
2
2 3
6
6 8
14
14 7
2
```



#### Conversion from postfix to infix

This can also be achieved using stack.

Eg2. `3 x y + z + *`

Stack: 

```
3
3 x
3 x y
3 x+y
3 x+y z
3 x+y+z
3*(x+y+z)
```



#### Conversion from infix to postfix

##### Rules: 

1. If the term is a variable or a number, output it directly
2. If the term is an operator:
   1. If stack is empty or the top of stack is an operator of **lower precedence**, push the operator into stack
   2. If the top of stack is an operator of **higher precedence**, pop the top of stack to output, then push the new operator into stack.
3. If the term is a bracket:
   1. If it is a left bracket, push it into stack
   2. If it is a right bracket, 
      1. if the top of stack is an operator, pop it to output
      2. if the top of stack is a left bracket, **pop and discard it**.
4. If there is no more input, 
   1. pop all operators in the stack. 
   2. ignore bracket.
5. Precedence:   `^`  > ` *`  = ` / ` > ` + ` = ` -`



Eg3.  `3 * (x * y + 3)`

| Input           | Stack | Output        |
| --------------- | ----- | ------------- |
| 3 * (x * y + 3) |       |               |
| * (x * y + 3)   |       | 3             |
| (x * y + 3)     | *     | 3             |
| x * y + 3)      | * (   | 3             |
| * y + 3)        | * (   | 3 x           |
| y + 3)          | * ( * | 3 x           |
| + 3)            | * ( * | 3 x y         |
| 3)              | * ( + | 3 x y *       |
| )               | * ( + | 3 x y * 3     |
|                 | * (   | 3 x y * 3 +   |
|                 | *     | 3 x y * 3 +   |
|                 |       | 3 x y * 3 + * |



# 3.5 System Software

## 3.5.1 Asymmetric keys and encryption methods

### Definitions

**Encryption**: the process of encoding a message or information in such a way that only authorized parties can interpret it.

**Encryption algorithm**: The calculation/process/sequence of steps for converting the message text/data

**Encryption key**: A parameter used by the encryption algorithm

**Key strength:** Difficulty of discovering the key/computational burden

**Cipher text**: The result of encryption that is transmitted to the recipient

**Plain text:** Any message that is not encrypted



### Symmetric vs. Asymmetric Encryption

**Symmetric encryption**: The same key is used to encrypt and decrypt the message

**Asymmetric encryption:** The type of cryptography where different keys are used, one for encryption and one for decryption.

- Uses a pair of keys
- Public key known to everyone to encrypt
- Private key known only to the recipient of the message to decrypt
- Virtually impossible to reverse engineer - to deduce the private key given public key, so cipher algorithm and private key should both be kept secret
- Cipher algorithm based on intractability of certain mathematical problems, key pair is usually based on prime numbers



Asymmetric encryption can be used other way around to **send a verified message to the public**. 

The sender uses the private key to encrypt the message, as private key is kept secret, a message encryption using this key can only be from the owner of this key.

This can be used to combat **repudiation**: denial of involvement in transaction



#### Comparison

| Symmetric                                    | Asymmetric                              |
| -------------------------------------------- | --------------------------------------- |
| Shorter key                                  | Longer key, so stronger key strength    |
| Less computational burden                    | More computational burden               |
| Can be intercepted when transmitting the key | Guarantees security even if intercepted |



## 3.5.2 Digital Signatures and Certificates

**Digital certificate**: 

- An **attachment** to an electronic message used for security purposes. 
- Issued and signed by a **Certificate Authority (CA)**.
- **Binds a digital signature to an entity.**

**Digital signature**: an electronic document used to prove that the data is from a trusted source.



#### Signing a digital signature

- The message is applied a **cryptographic hash algorithm** 
- Which creates a number, called a **"digest"**
- The sender encrypts the digest using private key
- The cipher text is attached to the message

#### Verifying a digital signature

- The recipient uses the same algorithm to hash the message

- The result is decrypted using the corresponding public key

- The recipient compares the result with the signature attached

  The message is **authentic** (from the original sender) and **unaltered** if the two numbers are the same.



## 3.5.3 Encryption Protocols

### Definitions

**Secure Socket Layer (SSL)**: provides a secure connection between internet browsers and websites

**Transport Socket Layer (TLS)** is a newer and improved version of SSL.



When SSL is implemented it functions as an additional layer, between the Transport Layer and Application Layer.

When SSL is in place, the application layer protocol HTTP becomes **HTTPS** (S stands for secured).

SSL is in fact a protocol suite, other than a protocol.

**Purpose of using SSL or TLS:** to provide **privacy** and **data integrity** in transmission of data between two or more communicating computer applications.

#### Steps to set up a secure connection using SSL

- Browser requests that the server identifies itself
- Server sends a copy of its SSL Certificate and its public key.
- Browser checks the certificate against a list of trusted Certificate Authorities
- If the browser trusts the certificate, it creates, encrypts and sends the server a symmetric session key using the server’s public key.
- Server decrypts the symmetric session key using its private key.
- Server sends the browser an acknowledgement, encrypted with the session key.
- Server and browser now encrypt all transmitted data with the session key.

**Situations when use of SSL/TLS is appropriate**: when the **transmission of confidential information** is needed, such as e-commerce.



## 3.5.4 Malware

### Definitions

**Virus**: tries to replicate itself inside other executable code 

**Spyware**: A piece of software that records/stores user actions/keystrokes <u>without the user’s knowledge</u> and sends them to a third party for analysis

**Worm**: A standalone piece of malicious software that replicates itself 

**Phishing: ** **Use email** to attempt to gain a user’s confidential data

**Pharming:** Redirection to a bogus website that **appears to be legitimate** to gain confidential data



### Vulnerabilities

Malware can be introduced inadvertently when:

- Attaching a portable storage device
- Opening an email attachment
- Accessing a website
- Downloading a file from the Internet

Other factors:

- Weak passwords

- Buffer overflow
- Operating systems that lack security



### Methods to restrict the effect of malware

- Using anti-virus software
- Install packages to keep OS up to date
- Avoid attaching unreliable portable devices
- (TBD)

For phishing and pharming:

- Do not open suspicious email/websites

# 3.6 Monitoring and control systems 

## 3.6.1 Overview of monitoring and control systems

### Definitions

**Sensor:**  A hardware device that measures a property and transmits a value to a processor

**Actuator**: a hardware device that recieves physical signal from a processor and adjusts the setting of a controlling device

A monitoring system consists of only **sensor(s) but not actuator**.

A control/monitoring-and-control system consists of **actuators**.



Sensors such as temperature and humidity sensor records analogue data, so an **analogue to digital converter (ADC)** is needed to convert the data to digital.



#### Feedback cycle

A **feedback cycle** is some cyclic structure of cause and effect that causes some initial change in the system to run through a series of secondary effects, **eventually influencing the initial change** in some way.

The importance of feedback is to keep the real-world physical property in an acceptable range.

#### Eg.1 

sensor detects that water level is high -> data transmit and processed by processor -> processor let valve open to let water flow out -> sensor detects that water level is now low -> processor let valve close



#### Two methods of using processor in a control system:

1. **Polling**: processors reading sensors in turn

   **Disadvantages**:

   - It wastes processor time to read the unchanged values
   - Changed values may not be responded as soon as possible

2. **Interrupt**: when a sensor has a change in value, it raises an interrupt

   **Advantages**:

   - Processor only need to check sensors when <u>interrupt occurs</u>
   - Changed value is responded as soon as it happens

## 3.6.2 Bit manipulation to monitor and control devices

### Definitions

A **bitmask** is a way of accessing a particular bit.

We can **AND, OR or XOR** the bitmask with the original number.



|        | AND                 | OR                  | XOR              |
| ------ | ------------------- | ------------------- | ---------------- |
| with 0 | Set to 0            | Keep original value | Retain the value |
| with 1 | Keep original value | Sset to 1           | Invert the value |



### Using assembly language instructions

We always need to first load the value to accumulator (ACC) and then access it.

`LDD <address>`

And then we can use AND, OR or XOR mask

Syntax:

We need to add a # before the number.

```
AND #n
OR #n
XOR #n
```

The #n can be **decimal, hexadecimal or binary.**

```
AND #B00010001 // add a B before the number
// is the same as
AND #17
// is the same as
AND #&11 // add a & before the number
```



### Scratches

**Data security**: data is protected against accidental or malicious corruption or loss.

**Data integrity**: the safeguarding of validity of correctness of data

**Data privacy**: Prevent access of data by unauthorised users, only authorised people can access it.



**proxy server**: A computer hardware and software setup as a gateway between a user and the Internet.

It can save a copy of a werbpage in scahce fore subsequent request, and/or act as a firewall.