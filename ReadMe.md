# ASP.NET Core Developer Roadmap

## Roadmap

![Roadmap](./aspnetcore-developer-roadmap.png)

## Resources

1. General Development Skills
   - [Git Book](https://git-scm.com/book/en/v2) (don't need to dig into deep, it's ok with git add, commit, push, pull, clone, checkout and branch)
   - Http, Https, TLS/SSL
     - In my opinion, Http can be divided into three parts
       - ht (hyper text), that something more than text, like video, images, etc
       - t (transfer), typically two side, client side and server side, they are transferring things by request (from client to server) and response (server back to client)
       - p(protocol), like a contract that anyone aiming to transfer things between client and server side need to comply with.
     - the "s" is stand for the security.
       - http request and response is plaintext, everyone can read by monitoring. So it's unsafe and unsecure.
       - the "s" is like use the cryptography to transfer the plaintext into the cipher text with the algorithm. 
         - symmetric : generate 1 key only. use the this key to encrypt and decrypt
         - asymmetric: generate a pair of keys (one is public key, one is private key). use public key to encrypt and private key to decrypt.
       - "s" stands for TLS/SSL.
         -  Transport Layer Security (TLS) is a cryptographic protocol designed to provide communications security over a computer network.
         -  SSL, or Secure Sockets Layer, is an encryption-based Internet security protocol. 
     -  Simulation of an Http
       -  Client parses the hostname to ip with DNS
       -  Client - Server TCP 3 way handshakes
       -  Client sends Http request
       -  Server sends Http response
     -  Simulation of an Https
       -  Client parses the hostname to ip with DNS
       -  Client says "Hello" to Server
          -  let server know what kind of encrypt algorithm it wants, the version, etc
       -  Once server received the "Hello", it will send the certificate back to client
          -  server should already generate the private key and public key.
          -  the certificate contains information about the Certificate Authority (CA), issued at, expiration, and **public key**. 
          -  server will ask CA to calculate the hash of certificate, encrypt the hash value (I personally call it hash1 here) with CA's private key to generate the digital signature on the certificate.  
          -  server sends this certificate and signature back to client.
       -  Once client received the certificate, it will do the validation and generate a symmetric key (**session key**) and send the encrypted session key to server
          -  client asks CA to decrypt signature with CA's public key and get the hash (I personally call it hash2 here). 
          -  CA checks if hash1 and hash2 are equal and let client know if this certificate is valid.
          -  client will generate a random session key and encrypt the session key with the public key from certificate.
          -  client sends encrypted session key to server
          -  server decrypts the received key with the private key.
          -  client and server both have the session key.
       -  client and server use **session key** to request and response. 
   
1. C#
   
   1. My another repo for C# [TODO]
   
   2. My another repo for [.NET Examples](https://github.com/jiahaoZZ/.NET-Examples)
   
   3. My another repo for Dotnet Cli
   
1. SQL Fundamentals
   
   1. ER diagram, relationships, entities, that we have learned in University, even I forget almost of them. But still don't want to illustrate too much here, it's quite simple and just google it for more details. 
   
   2. [Stored Procedure](https://learn.microsoft.com/en-us/sql/relational-databases/stored-procedures/create-a-stored-procedure?view=sql-server-ver16)
   
      1. a set of pre-written sql commands or queries stored in the database
   
      2. can have parameters and value them when exectuion
   
      3. Examples for creating.
         ```sql
         USE AdventureWorks2022;  
         GO  
         CREATE PROCEDURE HumanResources.uspGetEmployeesTest2   
             @LastName nvarchar(50),   
             @FirstName nvarchar(50)   
         AS   
         
             SET NOCOUNT ON;  
             SELECT FirstName, LastName, Department  
             FROM HumanResources.vEmployeeDepartmentHistory  
             WHERE FirstName = @FirstName AND LastName = @LastName  
             AND EndDate IS NULL;  
         GO  
         ```
   
      4.  Example for invocation
   
         ```sql
         EXECUTE HumanResources.uspGetEmployeesTest2 N'Ackerman', N'Pilar';  
         -- Or  
         EXEC HumanResources.uspGetEmployeesTest2 @LastName = N'Ackerman', @FirstName = N'Pilar';  
         GO  
         -- Or  
         EXECUTE HumanResources.uspGetEmployeesTest2 @FirstName = N'Pilar', @LastName = N'Ackerman';  
         GO  
         
         ```
   
         
   
   3. Constraints 
   
      1. private key, index, foreign key
   
   4. Triggers
   
      1. allows you to specify SQL actions that should be executed automatically when a specific event occurs in the database.
      2. for example, before/after a table update, insert or delete, doing something
      3. the actions could be sql query, commands, or stored procedures. 
   
1. see my another repo for ASP.NET Core Basic [TODO] 
