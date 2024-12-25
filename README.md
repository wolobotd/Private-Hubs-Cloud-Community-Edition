<body lang="en-US" link="#000080" vlink="#800000" dir="ltr"><p style="margin-top: 0.42cm; margin-bottom: 0.21cm; line-height: 100%; page-break-after: avoid">
<font face="Liberation Sans, sans-serif"><font size="4" style="font-size: 16pt"><b>Mozilla
Hubs</b></font></font></p>
<p>Ever since I found out about Mozilla Hubs, I wanted to get my own
server running. I don’t mean I wanted an AWS-hosted version - I
wanted to host it on my own server <font face="Liberation Sans, sans-serif"><font size="2" style="font-size: 11pt">hardware</font></font>,
and allow users both within my organization, as well as external
visitors, to be able to use it.</p>
</p>
<p>While there were some articles on self-hosting, there always
seemed to be some sort of limitation, especially around sound
support. Try as I might, I could never quite get it going, and what I
did get working was not very stable.</p>
</p>
<p>On May 31<sup>st</sup>, 2024, everything changed. This is the day
Mozilla ended support for Mozilla Hubs, and the non-profit Hubs
Foundation was incorporated. 
</p>
<p style="margin-top: 0.42cm; margin-bottom: 0.21cm; line-height: 100%; page-break-after: avoid">
<font face="Liberation Sans, sans-serif"><font size="4" style="font-size: 16pt"><b>Hubs
Foundation</b></font></font></p>
<p>The community came together to continue supporting and evolving
the project(s), eventually releasing the Hubs Cloud Community
Edition. This allowed users to deploy a full Hubs stack outside of
AWS <font face="Liberation Sans, sans-serif"><font size="2" style="font-size: 11pt">that
was fully</font></font> under their own control.</p>
</p>
<p>Like all good projects, Hubs is a complex infrastructure of
services and applications, and (at least as of this writing) still
contains some interesting hold-over characteristics from the AWS
hosting days. As such, most folks will probably find it easier to
deploy on <font face="Liberation Sans, sans-serif"><font size="2" style="font-size: 11pt">a</font></font>
hosting provider. There are some good articles and instructions to
follow on the Hubs Foundation website 
</p>
<p>https://hubsfoundation.org/</p>
<p>and gitlhub site 
</p>
<p>https://github.com/Hubs-Foundation/hubs-cloud/tree/master/community-edition.
</p>
<p><br/>
I have a keen interest in <font face="Liberation Sans, sans-serif"><font size="2" style="font-size: 11pt">having</font></font>
<font face="Liberation Sans, sans-serif"><font size="2" style="font-size: 11pt">complete</font></font>
control of my own private server. I also do not want to have to worry
about somebody’s business decisions having an impact on me. I like
having access to source code that I can pick apart, understand, and
maintain myself. I like being the master of my own destiny.</p>
<p style="margin-top: 0.42cm; margin-bottom: 0.21cm; line-height: 100%; page-break-after: avoid">
<font face="Liberation Sans, sans-serif"><font size="4" style="font-size: 16pt"><b>DIY
Metaverse - Hubs Cloud Community Edition Server</b></font></font></p>
<p>This document outlines how to take your own bare metal server and
<font face="Liberation Sans, sans-serif"><font size="2" style="font-size: 11pt">turn
it into a full Hubs Cloud Community Edition server. I</font></font><font face="Liberation Sans, sans-serif"><font size="2" style="font-size: 11pt">t</font></font><font face="Liberation Sans, sans-serif"><font size="2" style="font-size: 11pt">
will show you h</font></font><font face="Liberation Sans, sans-serif"><font size="2" style="font-size: 11pt">o</font></font><font face="Liberation Sans, sans-serif"><font size="2" style="font-size: 11pt">w
to </font></font><font face="Liberation Sans, sans-serif"><font size="2" style="font-size: 11pt">deploy
and manage</font></font><font face="Liberation Sans, sans-serif"><font size="2" style="font-size: 11pt">;</font></font></p>
<ul>
	<li><p><font face="Liberation Sans, sans-serif"><font size="2" style="font-size: 11pt">F</font></font>ully-functional
	hypervisor as a private cloud</p>
	<li><p><font face="Liberation Sans, sans-serif"><font size="2" style="font-size: 11pt">R</font></font>obust
	<font face="Liberation Sans, sans-serif"><font size="2" style="font-size: 11pt">f</font></font>irewall
	that includes NAT, DNS, and DHCP services</p>
	<li><p><font face="Liberation Sans, sans-serif"><font size="2" style="font-size: 11pt">P</font></font>rivate
	email server for access control</p>
	<li><p><font face="Liberation Sans, sans-serif"><font size="2" style="font-size: 11pt">F</font></font>ully
	functional Hubs Cloud Community Edition server</p>
	<li><p>Reverse Proxy to allow public access (optional)</p>
</ul>
<p>The main differences between this type of deployment versus
<font face="Liberation Sans, sans-serif"><font size="2" style="font-size: 11pt">external
</font></font>hosting provider versions are</p>
<ol>
	<li><p><b>Control and Privacy.</b> Since this is running on your own
	hardware, anything you put on the server is completely under your
	control. 
	</p>
	<li><p><b>Cost.</b> The deployment outlined herein does not <i>require</i>
	any subscriptions, registrations, or monthly fees. The only costs
	are for the actual server hardware, and support services such as
	internet and electricity. 
	</p>
</ol>
<p style="margin-top: 0.42cm; margin-bottom: 0.21cm; line-height: 100%; page-break-after: avoid">
<font face="Liberation Sans, sans-serif"><font size="4" style="font-size: 16pt"><b>Final
Thoughts Before Proceeding</b></font></font></p>
<p>If you like the idea of controlling your own Hubs Server on your
own hardware, this document will give you the blueprints and guidance
to help make it a reality. 
</p>
</p>
<p>There is a lot of work to be done. 
</p>
<p>While I will try and explain the purpose of each step, there are a
lot of concepts to bring together here including networking,
emailing, domain management, certificate management, server
management, and more. There are no scripts. <font face="Liberation Sans, sans-serif"><font size="2" style="font-size: 11pt">T</font></font>here
are <font face="Liberation Sans, sans-serif"><font size="2" style="font-size: 11pt">few</font></font>
GUIs. This all runs on command-line Linux, not on Windows or MacOS
(although I have been asked to port it to Windows and/or Windows
Server - stay tuned!). 
</p>
<p>If I haven’t scared you off yet, then let’s get started on a
journey of discovery as we build our own private metaverse together.
Enjoy!</p>
<p><font face="Dancing Script"><font size="4" style="font-size: 15pt">Terry</font></font></p>
<p style="margin-top: 0.15cm; margin-bottom: 0cm; border: 1px solid #ff0000; padding: 0.1cm; line-height: 100%; background: #fff5ce; page-break-before: auto">
<font color="#3e454c"><font face="Courier 10 Pitch"><font size="2" style="font-size: 10pt"><strong>Disclaimer:</strong><br/>
The
instructions provided in this guide are for informational purposes
only. While every effort has been made to ensure accuracy, the author
is not responsible for any damage, loss of data, or other issues that
may arise from following these instructions. Proceed at your own
risk, and ensure you have adequate backups and recovery measures in
place before making any changes to your systems.</font></font></font></p>
</body>
</html>
