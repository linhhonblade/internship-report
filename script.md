# Start (20s)

Good afternoon everyone
My name is Pham Thi Ngoc Mai
I'm here to present my Bachelor thesis on Cluster Establishment in Vehicular Network - Connectivity Enhancement
My presentation includes 5 parts: First, I will introduce about the technology and then the Methodologies, Tools and Implementation
Next is Results and finally the Conclusion and Future work

# Introduction (1m40)

I am going to start with VANETs, or Vehicular Ad-hoc Networks are the special type of Mobile Ad-hoc Network that aims at providing communication among vehicles on the roads. VANETs are introduced to help journey safer and the driving experience more comfortable and entertaining. There are two types of application in VANETs. Safety application and non-safety applications.

Focus on safety application, here, messages that contain critical events should be disseminated quickly and reliably to a target area so that proper actions can be taken to prevent users from accidents and hazadous situtations. However communication high overload or failures come 2 nodes want to communicate with each other but they are too far and out of communication range.

To overcome this issue, one of the solutions is cluster establishment. The main ideas, we divide vehicles or nodes into groups called clusters. Each cluster has a management node which is called cluster head and others called cluster members.

My supervisor has an idea about a clustering protocol and i realizes that idea by constructing that protocol in each process, implement it on simulator ns3, and run simulation for the clustering protocol.

# Method (3m20)

According to the idea of my supervisor, our system includes vehicles (nodes) and Road Side Unit (a device located road side to provide information to passing by vehicles) . We choose a nodes that has high number of neighboring nodes and closed distance to RSU to become Cluster Head. They will responsible for forwarding the packet within VANET.

To construct the protocol, I let nodes have different state and operate in many cycles (we call it Time Cycle). Each cycle has fixed pre-defined duration including some processes and I provide algorithm for the nodes in each process.

In more details, a Time Cycle has 3 process, in Beacon exchange, all nodes are STANDALONE which mean they are not belong to any cluster. next process is Cluster formation where some node become CH and the others become CM. In Data exchange node start exchanging message for safety and non safety applications.

## Beacon exchange

Jump into beacon exchange, node broadcast messages periodically (we call beacon messages), it contains information about node's mobility and state. Nodes update the table of its stable neighbors (called neighbor list) and keep track with the closest RSU

## Cluster formation

Nodes wait to become CH, the waiting time is calculated base on neighbor list size and the closest RSU.
Node will joins other cluster if receives FormClusterMessage while waiting
Otherwise, it declares CH itself and broadcast the FormClusterMessage
By the end of the process, nodes are divided into one or more clusters

## Data exchange

Communication in data exchange can be devided into 2 types
Intra-cluster communication occurs when src and dest node are in the same cluster
Node with directly send packet to dest or sent to CH and then CH forward it to dest
Inter-cluster on the other hand, dest belongs to another cluster that CH dont know.
Therefore CH sent packet to RSU.
Here we assume RSU have access to the core network and the packet will be delivered to the closest RSU of the destinaton cluster.

# Tools and Implementation (1m50)

To implement the protocol, I use ns-3. a network simulator allows user simulate real world network on computer by writing C++ or Python script. I write a new application module and use the built-in functions from WAVE module of ns3. WAVE is Wireless Access in Vehicular Network - a system architecture for VANET introduced by IEEE standard.

I create 2 Applications classes to handle the behaviors of vehicles and RSUs
We also create different Header classes for different type of packet exchanged in each process

Here is my design of 2 Applications. They extends the built-in application class, contain information about its mobility (position or velocity), VApplication for vehicles also have current process, and states

Next is the designs for headers.
RsuBeaconHeader is for beacon message sent by Rsu
VBeaconHeader is sent by vehicles
DataHeader for data packet exchanged in Data exchange process
FormClusterHeader is sent by CH

# Results (5p)

I finished the implementation of algorithms in Beacon exchange process, form cluster process and the intra-cluster communication in data exchange process.

Next, I evaluated the protocol via two scenarios: stable scenario and non-stable scenario with using metric PDR: Packet Delivery Ratio which is the ratio of sucessully received packets to the total sent.

In our scenarios, we construct experiments for nodes on a 3 lane road 100m long, move with constant velocity in same direction. We increase the number of nodes from 5 to 45 and we also have RSUs every 100m. In Stable scenario, node have same velocity or very closed velociy so that the toplogy doesnot change overtime. Non-stable, nodes have different velocity and can be distributed into different clusters

## Stable Scenario

The yellow line is the PDR for our clustering protocol. It out performs with the case there no protocol applied and node just   blind-broadcast the packet - the blue line. The red line re-broadcast only show a little improvement when the number of nodes are small, and gives no effects with higher number of nodes

## Non-stable Scenario

For the non-stable scenario, the protocol show a lower PDR compare to the first scenario, but still better than with broadcast and rebroadcast case. The packet lost in this scenario, caused by the lack of my implementation for inter-cluster communication in data exchange process

## cycle time

In order to improve the protocol, I analysed the effect of Cycle time.
I do another experiment for a network with wider velocity range and longer simulation time to see how the number of cluster evolves. If cycle time equals 33s, the number of cluster increase fast from 3 to 4 and to 6 in the 3rd cycle time. In 13s case, the No of clusters increases gradually an drops sometimes. In summary if we decrease the cycle time, the results of cluster establishment can up to date with the network topology and this may keep the comm within network more stable.

# Conclusion (1p)

In clusion, base on the idea of my supervisor, i have been construct a clustering algorithm and implement it by ns3 simulatior. The implementation still lack of the Inter communication in Data exchange process. In the future, if this work can be done then our protocol can be evaluated conhensively with more practical scenarios. And some specific parameter like cycle time, duration for each proces or coefficients in waiting time formula can be analyse to improve the performance of data transmission in the future.

This is the end of my presentation. Thanks for your attentions.

