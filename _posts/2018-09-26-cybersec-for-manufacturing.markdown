---
layout: post
title:  "DMDII & CIRI's Cybersecurity for Manufacturing Workshop"
date:   2018-09-26 18:00:00 -0500
categories: Events
published:  false
---
# Questions and Goals

+ Digital Manufacturing and Design Innovation Institute (DMDII)


+ Critical Infrastructure Resilience Institute (CIRI)

  - Education and Training
  - Identify and help develop Technology that is easy to transit to industry

    + Decide who receives funding from Department of Homeland Security (DHS)??

+ [NIST Cybersecurity Framework and Manufacturing Profile][profile]

  - What are the guidelines for manufacturers?
  - What is the road map for researchers?
  - What are some existing software or hardware infrastructures available for
    both manufacturers and researchers?

    + Software simulated test-beds, Digital Twins
    + Koushik mentioned in an [article] that a test-bed for penetration
      testing is ongoing in DMDII
    + NIST also has a [test-bed] but more for system design

[profile]: https://www.nist.gov/mep/nist-cybersecurity-framework-and-manufacturing-profile
[article]: https://www.smartindustry.com/articles/2018/big-fast-smart-vulnerable-manufacturing/
[test-bed]:https://www.nist.gov/laboratories/tools-instruments/smart-manufacturing-systems-sms-test-bed

+ Identify people who are closer to or interested in our broad research area

  - With sufficient technical background and experiences in industry
  
    + Director of Manufacturing Cybersecurity, Koushik Subramanian
    + Director of R&D in ITAMCO, Joel Neidig
  
  - Potential speakers for future events
  - Further collaboration with industry or government
  

# My Info

+ [NSF CPS: Software Defined Control for Smart Manufacturing Systems][grant]

  - Project is on formal model for controller networks in Manufacturing Systems
  - I focus on security aspect of the system
  - In particular, communication security analysis. In short, can we guarantee
    messages are kept secret even when adversaries are sniffing and spoofing?


[grant]: https://www.nsf.gov/awardsearch/showAward?AWD_ID=1544901

# Notes

Test-bed is for the whole manufacturing process. Which aspect can we get involved?

Digital thread?

+ 73% of manufacturers have <= 20 employees in US
  
  - What about Taiwan?

+ 2% over 500 people

5 stages in the *learning cycle*?? They are also mentioned in the profile

Other 3 workshops are less related to security but more on digital manufacturing

Live breach!!

CIRI is actually under ITI as well?

Risk management is their focus. I guess it is not really related to our researches?

Just in time inventory, Ransomware

"deliver uncompromised"

When he mentions cyber for supply chain, what parts exactly are about software
development, or all of them are just about using existing software stacks?

### FBI agent's talk !!! Presenter: Jason Rahoy

+ [**IC3 Internet Crime Report**](IC3.gov)

  - Over $676M victim losses just from Business Email Compromise (BEC)
  - $2.3M over ransomware
  - Tech Support Fraud (E.g., Fake refund, remote assistant)
  - Extortion $15M

+ InfraGard.gov

  - information sharing platform

+ Insider Threat

  - Video about using social engineering to get access to the account
    [![Preview][video-img]][video-url]
  - Inadvertent insider (E.g., victim of social engineering who is employee)
  - Preexisting infrastructure of already compromised network

[video-img]:https://img.youtube.com/vi/lc7scxvKQOo/0.jpg
[video-url]:https://www.youtube.com/watch?v=lc7scxvKQOo

+ Target data breach

  - Attack third party company (refrigeration supplier) and finally use their credentials
    to attack the interface Target provided to this company

+ Proprietary systems allowing external network access

+ 50% of attack targets small business <= 2500 (31 % <= 250 employees)

  - easy targets

+ Start from social engineering on a specific target??

  - Not start from an exploit to certain software?

## ISACA 2018 State of Cybersecurity Survey

+ Education and Training: Top three attacks

  - Phishing
  - Malware (Ransomware)
  - Social Engineering

## Panel: State of Cybersecurity for manufacturing

+ Obsolete products running old OSs that cannot patched

  - Win NT, 98, and even Dos

+ Education for business owner and how they communicate with IT guys

  - No security means will work if their users are the weakness

+ Outsourcing IT framework
+ Manufacturing specific technical challenges in security

  - No community like open source community in software development
  - Authenticated patching, when patches might be from one of thousand vendors,
    how to authenticate updates?
  - Re-certification of the whole system due to updates on few modules
    (hardware + softwares)

    + Not so common in software dev because of no safety or mission critical requirement

## Break Session 1

+ Talked to Koushik about the test-bed system for pen testing. He said the
  system is for internal use only now. There is a plan to provide external
  access but unlikely to happen in 6-months or so.

+ A live breach based on phishing mail and social engineering to ask employees
  inside to install a fake update on software assisted assembly line 
  (projecting images to the table to show which parts to assemble).
  However, the adversary is able to obtain patented 3D printing design.
  The attack is done in 15 mins.

  - Email is not digitally signed 
  - Update program is not certified
  - Network are not segmented. Should have separated the 3d printers from
    assembly line computers

## Booth and Exhibition

+ Verve worked on energy grid and provide services to discover all devices
  in a place

  - Kurt
  - An agent (a program) that are spread to any device that are capable of
    running itself. Sounds like a worm to me
  - A database that helps identify the device

+ Identify3D provides a software to encrypt all data in centralized server,
  and enforce authentication over all communications internally and more strict
  for data sharing to external parties such as other companies in supply chain.

+ cyberpoint provides CATO, a small RasperyPI like device for the company to plug
  in to the network to discover devices (for Ethernet/IP only, not really on
  layer 2 protocols such as CAN bus), and provide a web interface to navigate
  all dis covered devices, vulnerability analysis results, perform simulated attack.

    - Have to deal with nontrivial amount false alarms

      + For vulnerability analysis, there seem to be several other existing tools
      + Simulated attack is more on the human side, e.g., sending phishing emails.

    - The developer thinks an attack purely on flaws of layer 2 protocols is
      possible but extremely unlikely. Some low level devices such as CNC
      easily hang (and thus be detected) if packets are ill-formed;
      hence these networks are most likely isolated and only connected to a PC
      that controls them.
    - Access those PCs is a more plausible scenario.
    - Automatic discovering devices over low level buses seems to be technically
      difficult. Two 
    - In this case, it does not seem to be important to investigate layer 2
      protocol security for manufacturing. Safety-wise I don't know.

+ IoTium provides software defined infrastructure

  + Eliminate human interactions when deploying system
  + Provide gateway device blocking any access to devices behind except from their
    services hosted on AWS, as well as, the functionality of SDN Datapath to expose
    visibility
  + Their service on AWS is the SDN controller responding to application requests
    on desired network configs
  + Closely related to the NSF project

## Important Issues

+ Still ensure security when integrating a third-party module
+ Incremental re-certifications?
+ Certified Patching
+ Unpatchable components