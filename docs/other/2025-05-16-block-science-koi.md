https://blog.block.science/a-preview-of-the-koi-net-protocol/


BlockScience Blog
Home
Blog
About
A Preview of the KOI-net Protocol
Image created by Ilan Ben-Meir using Midjourney 7. 
A Preview of the KOI-net Protocol
May 16, 2025
Today’s information environment is defined by a strange inversion: Instead of inhabiting a shared reality from which a variety of knowledge objects emerge, we inhabit a variety of realities that each emerge from a particular collection of knowledge objects their inhabitants hold in common. In order to collaborate, distinct actors must first establish sufficient common knowledge to construct the shared reality within and upon which they will work.

BlockScience’s ongoing research into Knowledge Organization Infrastructure (KOI) – part of a collaborative initiative conducted in partnership with the non-profit Metagov and the Royal Melbourne Institute of Technology – is intended to facilitate this process, and today we are excited to announce the public beta release of our new KOI-net protocol. This beta release and accompanying demo are meant to familiarize interested parties with the structure and function of the protocol, so that they can begin experimenting with the affordances it offers prior to its full release later this summer.

The KOI-net protocol is rooted in the latest version of our existing Reference Identifier (RID) protocol, which identifies digital objects in terms of the “means of reference” that relates a “reference” (the RID) to a “referent” (some underlying object or resource). RIDs are similar to Uniform Resource Identifiers (URIs), but are not intended to have universal agreement or a centralized management structure. However, RIDs are compatible with URIs in that all URIs can be valid RIDs.

The RID protocol was designed to enable distinct actors to construct a set of shared references (and thus a common frame of reference) without needing to share the referents themselves. In other words, RIDs make it possible for organizations to communicate knowledge from or about proprietary resources and other objects, while preserving ownership of – and access control over – materials that they may be unwilling or unable to share.

The KOI-net protocol builds on the RID protocol to define standard communication patterns and coordination norms for establishing and maintaining KOI networks: heterogeneous compositions of KOI “nodes” which can autonomously input, process, and output knowledge, both independently and when wired together. The protocol only governs communication between nodes, allowing extensive variability in the behavior of each node and the configuration of each network. KOI networks can have a fractal-like structure, insofar as a given KOI-net can also function as a single node in a larger KOI-net (if it is viewed from an external perspective). These characteristics enable the protocol to serve as a flexible and interoperable foundation for future projects.

KOI-net allows nodes to communicate with one another according to one of two methods: event communication and state communication. Event communication is one-way – a node sends an “event” to another node – while state communication is two-way, with one node requesting RIDs, manifests, or bundles from another node, and receiving a response that contains the requested resource, if it is available. RIDs, manifests, and bundles are defined by the RID protocol, while events are defined by the KOI-net protocol.


How KOI nodes work. Image created by Luke Miller
An event is a signalling construct that conveys information about RID objects between networked nodes: A node emits an event to indicate that its internal state has changed. Events are composed of an RID, manifest, or bundle with one of three “FUN” event types attached; “New” means that the node has cached a previously-unknown RID, “Update” means that the node has cached a change to a previously-known RID, and “Forget” means that the node has deleted a previously-known RID from its cache. Nodes can broadcast events to other nodes in a particular KOI-net, but can also listen to events from other nodes – and can decide to change their own internal state, take some other action, or do nothing in response.

KOI-net also identifies nodes according to two basic types: “Full” nodes implement the API endpoints defined in the KOI-net protocol. They are capable of receiving events via webhooks (another node calls their endpoint), and serving state queries. Full nodes can also call the endpoints of other full nodes to broadcast events or retrieve state. “Partial” nodes, meanwhile, do not implement any API endpoints. They are capable of receiving events via polling (asking another node for events), and can also call the endpoints of full nodes to broadcast events or retrieve state.

Each KOI node can be viewed as dependent only on the KOI-net and RID protocols;  thus, we designed a basic koi-net-node template repository intended as boilerplate for setting up new full node implementations with extensive flexibility. It is simply too early to predict what sorts of nodes users will build, or what kinds of patterns these nodes might fit – but we do anticipate that certain categories of nodes will emerge over time. Nodes might be classified, for example, in terms of their positioning relative to the boundaries of the organization that operates them. “Sensor” nodes, under such an understanding, would be those that take inputs from outside the boundaries of the organization that operates them (i.e. from the world, or from a node operated by another organization) and pass outputs to other nodes within an organization’s KOI-net. “Actuator” nodes would act in reverse, taking internal inputs and passing outputs to some location or service beyond their operators’ organizational boundaries. “Processor” nodes, meanwhile, would operate solely within an organization’s boundary to take inputs from and pass outputs to other nodes.


A representation of different types of nodes in a KOI-net, categorized according to their relationship to the boundary between the network and the external world. Image created by Luke Miller
The video below demonstrates deployment of the koi-net-demo-v1 repository, resulting in the self-assembly of a modular knowledge processing network implemented using the KOI-net protocol. The example network is composed of five nodes: a coordinator node for facilitating node discovery, two sensor nodes pulling data from GitHub and HackMD, and two processor nodes for transforming and storing that data. It includes a flexible orchestration layer for both local and Docker-based deployments, along with command-line tools for system management. This demonstration is the first of a series designed for educational purposes, and is not intended for production use.


The architecture of the demo KOI-net can be seen below:


The architecture of the demo KOI-net. Image created by Sayer Tindall
Deployment of the demo repository begins with orchestration, as users interact with setup tools to deploy demonstration nodes. At runtime, the coordinator node manages node discovery and registration, the sensor nodes collect data from GitHub and HackMD APIs, and the processor nodes transform and store that data for analysis, all following the KOI-net protocol and communicating using RID exchange.


The data flow through the demo KOI-net. Image created by Sayer Tindall
The data flow through this demo KOI-net has seven stages: 

Collection: Sensor nodes fetch external data from GitHub and HackMD
Discovery: Sensors register with the Coordinator for system-wide visibility
Exchange: RIDs facilitate standardized event communication
Processing: Data moves through event handlers to services
Storage: Processed data is indexed in structured databases
Access: CLI and REST interfaces provide query capabilities
Monitoring: Continuous updates create a live processing stream
The demo features automated repository cloning and setup (after an initial manual cloning of the koi-net-demo-v1 repository itself), dynamic configuration generation, a centralized command-line interface for system management, and decoupled nodes communicating via a coordinator – highlighting the event-driven communication patterns, distributed data processing workflows, automated deployment and configuration generation, and application of microservice architecture principles to networks with decoupled components enabled by the KOI-net protocol.

This first demonstration is simple by design – intended only to familiarize users with the KOI-net protocol’s underlying structure and mechanics, and provide a first look at how it can be used to generate context-specific bespoke networks while ensuring that privileged information remains privileged. Nonetheless, it should make it easy to imagine the kind of further applications that the new protocol makes possible – especially when combined with AI-related tools, such as Anthropic’s Model Context Protocol (MCP) and/or Google’s Agent-to-Agent (A2A) protocol, which the KOI-net protocol is capable of supporting but does not require. 

MCP standardizes how models receive context and invoke external functionality, eliminating the need for custom integrations for each data source. A KOI-net could include an “MCP adapter” node that unifies the network’s datastreams into a searchable registry and facilitates LLM integration; the KOI-net resulting from the demo repository, for example, could easily be plugged into an MCP server that can access information from the sensors and is connected to an LLM interface, which would enable the network to answer questions about whether a particular github repository adheres to the specifications and requirements put forth by a particular HackMD. A2A, on the other hand, uses a task-based model with capability discovery, asynchronous management, and standardized message formats to allow agents to work together seamlessly, regardless of their underlying implementation – and could thus be used to enable a KOI-net to present a controlled interface to “outside” systems. Together, the two additional protocols can form a powerful combination: MCP connects KOI nodes to non-KOI data/tools within a particular KOI-net’s boundaries, while A2A enables secure, standardized communication across those boundaries.

Integration with MCP and A2A will be explored further in subsequent demos. 

About BlockScience
BlockScience® is a complex systems engineering, R&D, and analytics firm. By integrating cutting-edge research, applied mathematics, and computational engineering, we analyze and design safe and resilient socio-technical systems. We provide engineering, design, and analytics services to a wide range of clients, including for-profit, non-profit, academic, and government organizations, and contribute to open-source research and software development.

🌐 Website | 🐦 Twitter | 📚 Medium | 👻 Blog | 🎥 YouTube | 👥 Linkedin
Share this article
Facebook
 
Twitter
 
Linkedin
 
Pinterest
Subscribe to the BlockScience Blog
Get the latest posts delivered right to your inbox.

Enter your email...
or subscribe via RSS FEED
Previous Post
LLM, Research & Development
Understanding Large-Language Models
avatar BlockScience
April 30, 2025
Next Post
Artificial Intelligence, Systems Engineering, Complex Systems, System Design
A Systems Engineering Perspective on Artificial Intelligence (AI) Agents
avatar BlockScience
June 10, 2025
Recent Posts
Q3 Newsletter: 2025
October 13, 2025
Solving Coordination Challenges with Multidisciplinary Design Optimization (MDO)
October 04, 2025
New Paper: Online Governance Surfaces and Attention Economies
September 23, 2025
Subscribe to the BlockScience Blog
Get the latest posts delivered right to your inbox....


Enter your email...
About
BlockScience® is a complex systems engineering, R&D, and analytics firm. Our goal is to combine academic-grade research with advanced mathematical and computational engineering to design safe and resilient socio-technical systems. We provide engineering, design, and analytics services to a wide range of clients, including for-profit, non-profit, academic, and government organizations, and contribute to open-source research and software development.

See our Privacy Policy and Terms of Use.
    
© 2025 BlockScience Blog. All right Reserved. Powered by Ghost

Youtube transcript: 
https://www.youtube.com/watch?v=ifeQfpEQx8I

# Coinet Demo: Setting Up a Distributed Knowledge Network

## Introduction

This demonstration walks through the setup and configuration of Coinet, a distributed system for monitoring and processing knowledge objects across multiple platforms. The system creates a network of interconnected services that can sense, coordinate, and process changes to documents and repositories in real-time.

## Initial Setup and Configuration

The foundation begins with preparatory work—downloading the repository, configuring environment variables for GitHub and HackMD APIs, and running the initial setup command. The `make set of all` command orchestrates this symphony of preparation, cloning the necessary repositories and generating the configuration files that will guide each service.

As the setup unfolds, the system verifies each component, downloading requirements and presenting an overview of all available services. The process moves with quiet efficiency, checking dependencies and ensuring everything is properly aligned before the network comes to life.

## Building the Network Architecture

### The Coordinator

Step one brings the coordinator online with `make coordinator`. This central node will orchestrate the flow of information across the entire network, serving as the nexus point for all connected services.

### HackMD Integration

The HackMD sensor springs to life next with `make hackmd sensor`, followed immediately by the HackMD processor. These paired services work in concert—the sensor monitoring a specified HackMD note for any changes, while the processor stands ready to interpret and act upon those changes.

### GitHub Integration

The GitHub sensor follows, connecting to a specified repository. This component watches for updates to the codebase, tracking commits, issues, and repository events. Like its HackMD counterpart, the GitHub sensor feeds information to its dedicated processor, creating a complete pipeline for repository intelligence.

## The Living Network

With all five nodes now running—coordinator, GitHub sensor, GitHub processor, HackMD sensor, and HackMD processor—the network becomes a living system. Five individual services, each with its own purpose, yet interconnected in their mission to transform raw knowledge objects into actionable intelligence.

The architecture embodies a powerful premise: imagine maintaining a HackMD note containing project requirements alongside an active GitHub repository. As the requirements evolve in the document and the codebase changes in the repository, the network maintains a real-time feed of both streams. The configuration of these services determines what becomes possible with this synchronized knowledge.

## Demonstration and Capabilities

### HackMD Processor Interface

The processor node provides a command-line interface for accessing the monitored information. When queried about the HackMD note, it reveals comprehensive metadata: the note ID, title, creation dates, and word count. This is merely the surface—the content itself remains accessible, along with numerous other properties that enable sophisticated analysis.

### GitHub Processor Output

Querying the GitHub processor yields similarly rich information about the Block Science Coinet repository. The system reports when the repository was first indexed, when it was last updated, and the total number of events it has captured. From this foundation, virtually any analysis or automation becomes possible.

## The Power of Integration

The true elegance of this architecture reveals itself in the possibilities it enables. Consider the scenario where requirements documented in HackMD evolve over time. As these requirements update, the system can automatically run comparative evaluations against changes in the GitHub repository. When discrepancies or concerns arise, it can dispatch notifications—perhaps through Slack—warning the team of potential misalignments.

All of this automation flows through a single orchestrator script, transforming what might require constant human vigilance into a self-monitoring, self-reporting system. The network watches, processes, and alerts, freeing humans to focus on decisions rather than monitoring.

## Conclusion

This demonstration showcases a fundamental shift in how we can manage knowledge objects across distributed platforms. By creating sensors and processors for each knowledge source, and coordinating them through a central node, we build systems that don't just store information—they actively understand relationships, detect changes, and enable intelligent responses to the evolution of our work.

The five services running in concert represent more than technical infrastructure. They embody a vision of knowledge work where our tools don't merely record what we do—they help us understand what it means.
