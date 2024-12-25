<header>
# Mozilla Hubs
Ever since I found out about Mozilla Hubs, I wanted to get my own server running. I don’t mean I wanted an AWS-hosted version - I wanted to host it on my own server hardware, and allow users both within my organization, as well as external visitors, to be able to use it.

While there were some articles on self-hosting, there always seemed to be some sort of limitation, especially around sound support. Try as I might, I could never quite get it going, and what I did get working was not very stable.

On May 31st, 2024, everything changed. This is the day Mozilla ended support for Mozilla Hubs, and the non-profit Hubs Foundation was incorporated. 
Hubs Foundation
The community came together to continue supporting and evolving the project(s), eventually releasing the Hubs Cloud Community Edition. This allowed users to deploy a full Hubs stack outside of AWS that was fully under their own control.

Like all good projects, Hubs is a complex infrastructure of services and applications, and (at least as of this writing) still contains some interesting hold-over characteristics from the AWS hosting days. As such, most folks will probably find it easier to deploy on a hosting provider. There are some good articles and instructions to follow on the Hubs Foundation website 
https://hubsfoundation.org/
and gitlhub site 
https://github.com/Hubs-Foundation/hubs-cloud/tree/master/community-edition. 

I’m not most folks. I authored 4 patents on data privacy and security - I have a keen interest in having complete control of my own private server. I also do not want to have to worry about somebody’s business decisions having an impact on me. I like having access to source code that I can pick apart, understand, and maintain myself. I like being the master of my own destiny.
DIY Metaverse - Hubs Cloud Community Edition Server
This document outlines how to take your own bare metal server and turn it into a full Hubs Cloud Community Edition server. It will show you how to deploy and manage;
    • Fully-functional hypervisor as a private cloud
    • Robust firewall that includes NAT, DNS, and DHCP services
    • Private email server for access control
    • Fully functional Hubs Cloud Community Edition server
    • Reverse Proxy to allow public access (optional)

The main differences between this type of deployment versus external hosting provider versions are
    1. Control and Privacy. Since this is running on your own hardware, anything you put on the server is completely under your control. 
    2. Cost. The deployment outlined herein does not require any subscriptions, registrations, or monthly fees. The only costs are for the actual server hardware, and support services such as internet and electricity. 
Final Thoughts Before Proceeding
If you like the idea of controlling your own Hubs Server on your own hardware, this document will give you the blueprints and guidance to help make it a reality. 

There is a lot of work to be done. 

While I will try and explain the purpose of each step, there are a lot of concepts to bring together here including networking, emailing, domain management, certificate management, server management, and more. There are no scripts. There are few GUIs. This all runs on command-line Linux, not on Windows or MacOS (although I have been asked to port it to Windows and/or Windows Server - stay tuned!). 

If I haven’t scared you off yet, then let’s get started on a journey of discovery as we build our own private metaverse together. Enjoy!

Terry
</header>

<footer></footer>
