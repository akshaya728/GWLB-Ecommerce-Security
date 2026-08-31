#     GWLB-Ecommerce-Security


The idea to do this project evolved from a simple question,
How large e-commerce platforms like Amazon during Great Indian sale season handle millions of requests without their servers going down. what happens behind the scenes when lakhs of people hit a website at the same time?

In this journey to find solution, I have understood its all happening by the help of Gateway Load Balancer. I have studied and gathered info on the gateway Load Balancer.Here are my findings regarding it and how implementation of GWLB countered the problem in this work:

## Overview
AWS Gateway Load Balancer Integration to secure the e-commerce network infrastructure against high-volume traffic spikes, an AWS Gateway Load Balancer (GWLB) was deployed to transparently intercept, scale, and manage a fleet of third-party virtual security appliances. This architecture delivers inline "Security-as-a-Service" across the following dimensions

## Network Security Layer — How Traffic is Inspected
TRANSPARENT TRAFFIC INSPECTION: Combines a transparent network gateway with load balancing to intercept and inspect all incoming and outgoing traffic before it reaches target application load balancers.
GENEVE PROTOCOL INSPECTION: Implements the GENEVE protocol to add custom headers to data packets, preserving original source and destination IP addresses so security appliances can accurately inspect network headers without altering the original payload data.
##TARGET GROUP MANAGEMENT: Clusters virtual security appliances into centralized Target Groups to perform automated firewall filtering, intrusion detection system (IDS) monitoring, and deep packet inspection.
##FLOW SYMMETRY VIA HASHING: Employs advanced hashing algorithms to enforce strict flow symmetry. This ensures both requests and corresponding responses route through the exact same security appliance, preventing incomplete bidirectional security analysis.
##PRIVATE VPC ENDPOINT CONNECTIVITY: Leverages AWS VPC Endpoints and Elastic Network Interfaces (ENIs) to act as dedicated entry and exit points, routing traffic privately between consumer VPCs and security appliances entirely within the secure AWS backbone.
##AUTOMATED HEALTH MONITORING: Runs continuous health checks across all security appliances to instantly detect degradation and dynamically reroute traffic to healthy appliances, maintaining maximum uptime during peak shopping hours.


In this work I have designed network architecture by integrating GWLB with TRANSIT GATEWAY(acts as a centralized traffic hub,Hub-and-Spoke model).


## Key Challenges 

Most of the architecture is configured and working on my AWS free tier account. Gateway Load Balancer and Application Load Balancer are pending because  . I have raised a support case with AWS and will complete the deployment once i get access to create Load balancers on my free tier account. All other components including VPCs, Transit Gateway, Security Groups, NACLs, WAF, Auto Scaling and monitoring are fully operational.


## What i learned by this Project:

Before this project I didn't know that GWLB uses GENEVE protocol on port 6081 to forward packets.
I learned the difference between stateful and stateless firewalls — Security Groups are Stateful because they track active connection states and automatically allow return traffic, while NACLs are stateless because evaluate every packet independently and require separate explicit rules for both directions.
Symmetric routing in GWLB ensures the both the forward and reverse packets of a network flow traverse the exact same virtual appliance and network path. — this is called bump in the wire because it operates completely transparently at Layer 3.
Through hands-on deployment of core infrastructure and advanced networking services like GWLB for this project,I have developed a strong mastery of  the AWS environment.




    Traffic Flow Color Guide:
      🔴 Red   — Incoming customer traffic (unfiltered)
      🟢 Green — Clean traffic after NGFW inspection  
      🔵 Blue  — Outbound EC2 traffic via NAT Gateway
      ⚫ Grey  — Monitoring connections to CloudWatch 
                 and CloudTrail

Network Diagram:
<img width="1362" height="698" alt="Network Architecture Diagram(Brainboard)" src="https://github.com/user-attachments/assets/bad6ba95-ddbb-4bc6-8688-4cbeb205a37e" />

