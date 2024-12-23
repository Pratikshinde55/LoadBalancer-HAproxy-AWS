# Load-Balancer
![Screenshot 2024-02-28 193427](https://github.com/Pratikshinde55/Load-Balancer/assets/145910708/e31a4593-3fd0-4421-9c51-ec6dc7210730)

🌟Load Balancer:

Load balancer distribute workload and improve website and application performance.load balancer distribute incomming application traffic across multiple backend(target).load balancer also called as Frontend or reverse proxy.

⭐Haproxy⭐:-
 
HAproxy is one of the product of load balancer, HAproxy is a high-performance, open source load balancer & reverse proxy for HTTP and TCP .

Set-up:

For Loadbalancer setup i launched 4 instances one instance make Load Balancer(Frontend),and remaining
three make backend for my case named as Backend-1 (ip-172-31-44-4) ,Backend-2 (ip-172-31-33-138),Backend-3(ip-172-31-40-19).

![Screenshot 2024-02-28 193350](https://github.com/Pratikshinde55/Load-Balancer/assets/145910708/61be7c3a-fdf8-4947-a775-1b777215eeab)
![Screenshot 2024-02-28 175417](https://github.com/Pratikshinde55/Load-Balancer/assets/145910708/f56ea353-28d4-46c4-8ef2-4f9c718aa491)

⚡Backend Configuration(Web server):

 on three Backend instances, configure following same set-up on each backend node:
 
 1.install httpd php software(Apache)

 
    yum install httpd php -y

 2.DocumentRoot for "Apache server is /var/www/htmt" create here one code folder which for client.
   here put webpage named as index.php

     cd /var/www/html

     vim index.php

code:-


     <pre>
     <?php

          print_r($_SERVER);

     ?>
     </pre>

 3.Start the httpd service:
      
       
      systemctl enable httpd --now

 ![Screenshot 2024-02-28 190802](https://github.com/Pratikshinde55/Load-Balancer/assets/145910708/fef7e5b7-19ae-4197-abe8-1ee2b83841f0)
 

⚡Load Balancer configuration:-
  
1. Install HAproxy load balancer in frontend instance.


     yum install haproxy -y

2.Registration of Backend to Load Balancer, HAproxy has config file "/etc/haproxy/haproxy.cfg" where add backend node and also add port no. which can helps to client to access application.
for this do follow setup:


     vim /etc/haproxy/haproxy.cfg
  
 ADD this code in config file:

 ![Screenshot 2024-02-28 190246](https://github.com/Pratikshinde55/Load-Balancer/assets/145910708/5245435a-d02e-45f1-97c5-f3f31ea67999)


Note: 

here we use Round Robin Algorithm that work as client will connect to web server through Load
balancer , 1st connect to web 1 then web 2 and next web 3 then again go to 1.
here also bind the port no. as 8080 .

3. Start HAproxy service and check status

   
        systemctl restart haproxy
   
        systemctl start haproxy

        systemctl status haproxy

4.check HAproxy config file is valid or not

     haproxy -f haproxy.cfg -c



💫Now loadbalancer configuration is done💫 

 note :
 
 Load Balancer(Frontend) instance change Inbound rule - allow all traffic Anywhere


Check Load balancer on browser:

  Public IP of LB + port no. (http://65.0.18.65:8080) 
    
  also on local command prompt -->>(curl http://65.0.18.65:8080)

 ![Screenshot 2024-02-28 190614](https://github.com/Pratikshinde55/Load-Balancer/assets/145910708/82e506cb-3d7d-454f-8266-ca222508a16d)
 ![Screenshot 2024-02-28 190525](https://github.com/Pratikshinde55/Load-Balancer/assets/145910708/e9f58322-9a2d-4602-a8b1-370db440bf52)
 ![Screenshot 2024-02-28 190456](https://github.com/Pratikshinde55/Load-Balancer/assets/145910708/085efef9-ce7d-4bd5-9b8d-34fc6aa4632d)


  


    










