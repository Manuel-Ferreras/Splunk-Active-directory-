# Investigating and remediating security issues in Active Directory using Splunk Security Search.

Previously, I was able to set up a Splunk environment on an Amazon AWS EC2 https://github.com/Manuel-Ferreras/Setting-Up-SIEM-SPLUNK-AWS-

 - window event codes refer to specific numerical codes that are used to categorize and identify events in the Windows Event Log. 
 - Event code 4625	Failed account Logon	Indicates potential brute-force attacks or unauthorized attempts to access a system.
 - data structure=index wildcard=* Window EventCode=4625

<img src="https://i.imgur.com/wROfKka.png.png" height="40%" width="44%" alt=/> 

 - There were 5,748 Event in 24 hour. It has not been logical in this scenario as there are only 20 employees.
 - Another sign of a threat actor attempting to compromise an account is the account name "ALTERDATA"
 - The IP address 64.64.x.x is based in Chicago, Illinois according to Censys. In this scenario, no employees work from Chicago, Illinois.
 
   <img src="https://imgur.com/8WQ9mxu.png" height="20%" width="20%" alt=/> 

 - To get a better, more clear data on the login attempts, you can search with the query: index=* EventCode=4625 LogName=Security | stats count by src_ip. This query will display the count of login attempts by IP address."
 - They were 9,500 failed login attempts, which is a clear sign of a brute force attack.
 
   <img src="https://imgur.com/92S1sIk.png" height="1000%" width="100%" alt=/> 

 - With this information, you can block this IP address from the access control list in AWS or your firewall.

- If you're looking for a visual representation of the data for Event Code 4625, you can use this query: index=* EventCode=4625 LogName=Security | stats count by src_ip | chart sum(count) as Failures by src_ip
 
 <img src="https://imgur.com/VZfga9Z.png" height="40%" width="40%" alt=/> 


 <h2> 4720 A user account was created.</h2> 


   

