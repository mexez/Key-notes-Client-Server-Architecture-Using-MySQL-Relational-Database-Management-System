### Setup of Client-Server architecture using Mysql RDMS

As expected on this setup, client (send request and its expected to get a rewsponse from the server)and web server (has {web service nginx, apache, tomcat} which i installed mysql running on it making it a DB server)
<p>I demostrated the client-server concept using Mysql. I created 2 server (ubuntu OS) in AWS for the server and client.</p>
<p>Instance ID i-0b07da4e1c8695e3a (DB_server) Public 3.143.204.220 Private 172.31.15.30 </p>  
<p>Instance ID i-01b66bcae6b876e2c (P5_Client_Server) Public 3.145.111.141 Private 172.31.8.15 </p>

Basic info on this setup;

Updated the servers and installed mysql-server and mysql-client

<!-- Code Blocks--> 
```server update and install mysql
    sudo apt update -y
    sudo apt install mysql-server -y  (DB server)
    sudo apt install mysql-client -y  (client)
￼```￼
enabled mysql service

	sudo systemctl enable mysql

<p>On the DB server, I allowed inbound on Tcp protocol for MySql which is port 3306 installed the security script sudo mysql_secure_installation (its used to test the password and improve security)</P>

    sudo mysql (i'm able to login to mysql)

I created a remote user on mysql (where % means any ip address can be used by the remote user, Password is password, i granted all priviledge on the DB * )

```MySql to create a user
    CREATE USER 'remote_user'@'%' IDENTIFIED BY 'password';
    GRANT ALL PRIVILEGES ON *.* TO 'remote_user'@'%' WITH GRANT OPTION;
    FLUSH PRIVILEGES;
```
So DB is created. I exited the DB 

<p>I configured Mysql server to allow connection from remote host with the below command to replace ‘127.0.0.1’ {bind address} to ‘0.0.0.0’ in the text editor.  and I restart mysql server </P>


    sudo vi /etc/mysql/mysql.conf.d/mysqld.cnf

    sudo systemctl restart mysql

On the client server i ran below command (specifying the host ip address of the DB server) and got connected to Mysql server
    
    sudo mysql -u remote_user -h 172.31.15.30 -p

    show databases; 
WIth this command,i can see the DB (test_db) i created in the DB server

<!--docs link-->
[Docs on Client Server Architecture with MySql](https://docs.google.com/document/d/1Dyt_rRdf_vAMJSPSKinXfRDTVSLGd_e5KtkX7LFJN-U/edit?usp=sharing "A snippet of the Client Server Archi with MySql setup") 
