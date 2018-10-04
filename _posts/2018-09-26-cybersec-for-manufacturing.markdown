---
layout: post
title:  "DMDII & CIRI's Cybersecurity for Manufacturing Workshop"
date:   2018-09-26 18:00:00 -0500
categories: Events
published:  true
---

**Note: "p.##" means the page number in shared slides**

*TODO Share the slides*

## About the institutes

+ About Digital Manufacturing and Design Innovation Institute (DMDII),
  p.4~p.15

  - Provide resource to help manufacturers adopt productivity-enhancing 
    digital technical (include but not limited to cybersecurity)
  - Hold four major workshops year round (See p.14)

    + Other 3 workshops are less related to security but more on digital
      manufacturing

+ About Critical Infrastructure Resilience Institute (CIRI),
  p.16~p.23

  - Funded by Science & Technology Directorate in Department of Homeland
    Security (DHS)
  - Identify and help develop low-hanging fruit technology for manufacturing
  - Education and Training of cybersecurity for manufacturers and their 
    supply chains
  - Promote [NIST CSF Manufacturing Profile][profile] (See later sections)
  - Is also under Information Trust Institute in UIUC

## Main focuses of the workshop

The main goal of the workshop is to raise the awareness of cybersecurity among
manufacturers, and promote the NIST profile as a framework and guideline to
implementation and evaluations on enforcing security measures.

+ [NIST Cybersecurity Framework and Manufacturing Profile][profile]

  - What are the guidelines for manufacturers?
  - What is the road map for researchers?
  - What are some existing software or hardware infrastructures available for
    both manufacturers and researchers?

    + Software simulated test-beds, Digital Twins
    + NIST also has a [test-bed] but more for system design

[profile]: https://www.nist.gov/mep/nist-cybersecurity-framework-and-manufacturing-profile
[test-bed]:https://www.nist.gov/laboratories/tools-instruments/smart-manufacturing-systems-sms-test-bed

## People who are closer to or may be interested in our broad research area

+ With sufficient technical background and experiences in industry
  
  - Director of Manufacturing Cybersecurity in DMDII, Koushik Subramanian
  - Director of R&D in ITAMCO, Joel Neidig

## CYBERSECURITY THREATS IN TODAY’S WORLD

Presenter: Special Agent in FBI Chicago, Jason Rahoy

The presentation slides are not provided

### Some stats and where to find them

+ [**IC3 Internet Crime Annual Report**][IC3]

  - Over $676M victim losses just from Business Email Compromise (BEC)
  - $2.3M over ransomware
  - Tech Support Fraud (E.g., Fake refund for equipment, remote assistant, etc.)
  - Extortion $15M

+ 50% of attack targets small business <= 2500 (31 % <= 250 employees)

  - Because these are easy targets

+ [InfraGard.org](https://www.infragard.org/)

  - Information sharing platform between FBI and private sectors

[IC3]: https://www.ic3.gov/media/annualreports.aspx

### Some common attack vectors and case studies

+ Insider Threat

  - Preexisting infrastructure of already compromised network
    (E.g., old phone network)
  - Inadvertent insider (E.g., employee being deceived as video below)

    + [Video][video-url] about using social engineering to get access to a
      phone account

[video-url]:https://www.youtube.com/watch?v=lc7scxvKQOo

+ Proprietary systems allowing external network access

  - Target (the department store company) data breach
  - A third party company (refrigeration supplier) is attacked first,
    and their credentials are used to attack the interface Target provided
    to this company

+ Attacks normally start from social engineering on a specific target,
  i.e., collecting publicly available information of a target employee with
  enough administration

  - Opposite to my belief that it's actually rare to start from a known exploit
    to certain softwares because those either are likely fixed or seldom provide
    enough permission to compromise the system.

## ISACA 2018 State of Cybersecurity Survey

p.28~p.61 in slides. Mainly about various survey results.

+ Education and Training: Top three attacks

  - Phishing
  - Malware (Ransomware)
  - Social Engineering

## Panel: State of Cybersecurity for manufacturing

Mainly discussing that IT in manufacturing is far behind

+ Obsolete products running old OSs that cannot patched

  - Win NT, 98, and even Dos

+ Education for manufacturers and how they communicate with IT support

  - No security tools will work if their users are the weak spot

+ Outsourcing IT framework
+ Manufacturing specific technical challenges in security

  - No active community like open source community for software development
  - Authenticated patching, when patches might be from one of a thousand vendors,
    how to authenticate patches?
  - Re-certification of the whole system due to updates on few hardware/software

    + Not so common in software development

## Panel: The Mindset of An Attacker

Targeted by state affiliated group

+ Manufacturing is an easy target
+ First world country GDP

Pen test technique for Operational Tech~(OT)

+ IT attack still works on OT Env
+ OT is more fragile therefore cause more damages if not pen tested properly

  - Whole assembly line shut down just for pen tests is not helping 

Backup plan

+ Security of the backup
+ Test how to restore the backup
+ Consultant from attacker minded
+ zero trust model

  - Any user-touched component are dirty
  - Network segment between dirty devices and critical infrastructure
  - Trusted firmware

Pen test brings down system (valid)

+ Traffic monitoring, passive measures, statically detect vulnerability
+ Resilience against pen testing is also a test on the backup plan

+ Most known exploits are difficulty to utilize


## Break Sessions

See p.71 for the three break sessions

### ISACA Training Lab

Presenter: T. Frank Downs, fdowns@isaca.org

Provide trainings from basic network knowledge such as port scanning, packet
sniffing, etc., or more advanced scenarios such as detecting breaches or
recovering after attacks. Students are provided with a virtual machine and
complete all tasks on the machine. The OS can Windows, Ubuntu, or Kali OS,
and both CLI and GUI are supported.

+ **Sandbox network environment** based on Microsoft Azure and HyperV

  - Scale up and down based on demand (i.e., how many students online)
  - Emulation for different hardware architectures are not implemented.
  - The developer thinks particular attacks against different hardwares such as
    ARM CPU are possible; therefore, it is a valid point that it might be not
    enough to virtualize network topology and service entry points that use only
    x86 architecture.


### MFG. FLOOR DEMO

A live breach based on phishing mail and social engineering to ask a manager
level employee to install a fake update on software used on assembly line 
(a software projecting images on the table to show which parts to assemble).
The adversary is able to obtain a patented design from a 3D printer connected
to the network somewhere else. The attack is done in 15 mins.

+ Some reasons why the attack is so easily done

  - Email is not digitally signed 
  - Update program is not certified
  - Network are not segmented. Should have separated the 3d printers from
    assembly line computers

+ Asked Koushik about the system demoed for penetration testing. He said the
  system is for internal use only now. There is a plan to provide external
  access but unlikely to happen in half an year or so


## [Cyber Secure Dashboard]

Developed by CIRI and Heartland

How to comply to or even interpret the requirements and standards with hundreds
of pages in the framework? Even worse there are different frameworks!

+ Provide web interface to cross-references and top-down views
  (from abstract level to more and more details)
+ List best practices for guidance
+ Templates for policies
+ Document management and automatic tagging based on the web entry point where
  the document is uploaded

  - In their terms, the **implementation** that complies to the requirement

+ Merely aggregate all the information into a nice web interface? Not really

  - Also provides revision control over updates of "implementation" due to
    changes in standards or framework
  - Docker container to ship to any other internal server in the enterprise and
    customizable to fit with existing databases

[Cyber Secure Dashboard]:https://cybersecuredashboard.com/


## Company Booths

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
  all discovered devices, vulnerability analysis results. It can also perform
  simulated attack.

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



## Cyber Insurance

+ Started for integrity and secure storage of sensitive data

  - Liability for the data

+ WANNACRY and NOTPETYA in 2017
+ Regulations (GDPR)

Basic risk management: Avoid, Mitigate, Transfer, Accept

# More notes and thoughts

+ "Deliver Uncompromised", a document on strategies from the nation-wide 
  point of view

+ Test-bed is for the whole manufacturing process. Which aspect can we get involved?

+ 73% of manufacturers have <= 20 employees in US and only 2% over 500 people

Risk management is their focus. I guess it is not really related to our researches?

Just in time inventory, Ransomware

+ Cyber for supply chain is mentioned many times, but what parts exactly are
  about software development, or all of them are just about using existing
  software stacks?
