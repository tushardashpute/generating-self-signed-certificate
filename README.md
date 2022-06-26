# generating-self-signed-certificate
generating-self-signed-certificate-and-applying-to-aws-alb


# openssl genrsa -out ./server.key 2048
    Generating RSA private key, 2048 bit long modulus
    ....+++
    ....................+++
    e is 65537 (0x10001)

# openssl req -new -key ./server.key -out ./server.csr
    You are about to be asked to enter information that will be incorporated
    into your certificate request.
    What you are about to enter is what is called a Distinguished Name or a DN.
    There are quite a few fields but you can leave some blank
    For some fields there will be a default value,
    If you enter '.', the field will be left blank.
    -----
    Country Name (2 letter code) [XX]:IN
    State or Province Name (full name) []:MH  
    Locality Name (eg, city) [Default City]:Pune
    Organization Name (eg, company) [Default Company Ltd]:
    Organizational Unit Name (eg, section) []:
    Common Name (eg, your name or your server's hostname) []:                      
    Email Address []:

    Please enter the following 'extra' attributes
    to be sent with your certificate request
    A challenge password []:
    An optional company name []:


#  openssl x509 -in ./server.csr -days 365 -req -signkey ./server.key -out ./server.crt
    Signature ok
    subject=/C=IN/ST=MH/L=Pune/O=Default Company Ltd
    Getting Private key


    # ll
    total 15868
    -rw-r--r-- 1 root root     1115 Jun 26 02:11 server.crt
    -rw-r--r-- 1 root root      960 Jun 26 02:10 server.csr
    -rw-r--r-- 1 root root     1675 Jun 26 02:09 server.key
