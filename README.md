# DigiSpine

__DigiSpine - A digital backbone for functionally networking business applications to enable seamless interaction with business data.__


Motivation (WIP):
- Context of business applications 
  - Manufactoring / production plants and facilities
- Goal
  - Integrated solution for operational communication and real-time analytics to: 
    - Optimize manufacturing/production process with integrated analytics 
    - Seamless communication between different business domains/departments (operational and strategic) 
- Design Approach: 
  - Domain-driven design (DDD) focusing on modeling software to match a domain, according to input from that domain's experts
- General idea of DigiSpine (1st citizen components):
  - One SCS-Architecture per domain -> TODO: Link SCS
  - One SCS per subdomain
  - Operational stream(s): The production process is represented as a stream of DomainEvents (TODO: Image)
  - Analytical stream(s): Are derived from operational stream(s) an SCS
  - (Real-time) Data products: Data products (in terms of data mesh) are used   
