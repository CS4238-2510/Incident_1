# Incident_1

1) (5 marks) Draw the final topology of the discovered network of V.I.L.E.  



2) (4 marks) Describe the techniques used for network scanning.  



3) (6 marks) Describe the techniques used for pivoting. 


4) (2 marks) Alternatives/Enhancements/Out-of-class techniques used in the attack. 



6) (1 mark) Finishing the survey (to be published to Canvas shortly).


What i found:


sed -n '1,120p' /home/tx48/loot/11-updated_samba/project_status.txt
Project: Incident 1
Status: In Progress


sed -n '1,200p' /home/tx48/loot/11-updated_samba/README.txt
Note from the Admin:
“The password to root lies where the shadows meet the numbers:
Three times seven minus the sum of two primes.”
If you were expecting for anything like a flag or hint… so were we :(((



sed -n '1,200p' ~/CERT-ALERT-2025-08-09.txt
Security Advisory – Router Pretending to be a Web Service


Advisory ID: CERT-ALERT-2025-08-09
Release Date: 2025-08-09
Severity: Critical
Affected Component: Web service

Summary

A security weakness has been identified in the service running on the router. Whoever thought it was a good idea to run a web server on a device that is supposed to be router - please DO NOT DO THIS AGAIN!
Our company network is planning an expansion where our goal is to increase our 5 computer network to a network with 10 computers. In wake of these changes, we cannot afford to have more weaknesses in our network.


Technical Details - How to replicate the weakness?

It appears that one of our routers is running a web server at port 80. What is worse? It can has a command injection vulnerability. In the wake of this vulnerability, we see it fit to explain to the developers and admins in our organization as to how this can be exploited by a hacker.

1.Fallacy - Hackers do not have access to internal web servers.
Hackers can use port forwarding to interact with internal websites, if they have access to even one machine in our network.

2.How does port forwarding work? - Assuming that the web server is running on router (IP:10.10.10.12) at port 80, one can use port forwarding using SSH option -L. It means that a service running on port 80 of 10.10.10.12 can now be accessed through your laptop port (e.g., 2500)

ssh -p <portno>  -J tx1000@users.ncl.sg -L 2500:10.10.10.12:80 tx1000@x3550.ddns.comp.nus.edu.sg

3. After ssh succeeds, in your own Laptop, use a browser to go to: http://localhost:2500 (same port mentioned in previous command).

4. You should be able to see FirstSecurity website created by a genius in our company.

5. Command Injection:
   This website is vulnerable to command injection through the URL. Example:
   http://localhost:2500/?page='.system("id").'
6. The Linux 'id' command is run on 10.10.10.12 and the result is displayed on a public facing website.

7. What a disaster!


Mitigation

Remove all unauthorized websites hosted on any machine other than the web server. Mental note: Fire the guy who hosted the website on our router!


Additional Information

We have deployed some decoys as hints. We have done this to confuse the hackers.

Disclaimer

This advisory is intended for system administrators to address the issue promptly. Distribution beyond the organization is not authorized.
