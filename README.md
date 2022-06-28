# generating-self-signed-certificate
generating-self-signed-certificate-and-applying-to-aws-alb

How to generate Self-Signed Certificate

At first, please generate a private key using the following command.

    # Private Key
    # openssl genrsa -out ./server.key 2048
    
    Generating RSA private key, 2048 bit long modulus
    ....+++
    ....................+++
    e is 65537 (0x10001)

And then, please generate a public key with the following command. I use AWS US-east-2 region, so I set “*.us-east-2.elb.amazonaws.com” as “Common Name”.

    # Public Key
    # openssl req -new -key ./server.key -out ./server.csr
    
        You are about to be asked to enter information that will be incorporated
        into your certificate request.
        What you are about to enter is what is called a Distinguished Name or a DN.
        There are quite a few fields but you can leave some blank
        For some fields there will be a default value,
        If you enter '.', the field will be left blank.
        -----
        Country Name (2 letter code) [XX]:US
        State or Province Name (full name) []:IL
        Locality Name (eg, city) [Default City]:
        Organization Name (eg, company) [Default Company Ltd]:demo.ltd
        Organizational Unit Name (eg, section) []:sales
        Common Name (eg, your name or your server's hostname) []:*.us-east-2.elb.amazonaws.com        
        Email Address []:

        Please enter the following 'extra' attributes
        to be sent with your certificate request
        A challenge password []:
        An optional company name []:


You can create Self-Signed Certificate using the following command with the private/public key.

    Self-Signed Certificate
    #  openssl x509 -in ./server.csr -days 365 -req -signkey ./server.key -out ./server.crt

        Signature ok
        subject=/C=US/ST=IL/L=Default City/O=demo.ltd/OU=sales/CN=*.us-east-2.elb.amazonaws.com
        Getting Private key


    # ll
    total 15868
    -rw-r--r-- 1 root root     1115 Jun 26 02:11 server.crt
    -rw-r--r-- 1 root root      960 Jun 26 02:10 server.csr
    -rw-r--r-- 1 root root     1675 Jun 26 02:09 server.key


**# cat server.crt** 
        -----BEGIN CERTIFICATE-----
        MIIDdDCCAlwCCQCyAVI5ZGXX1jANBgkqhkiG9w0BAQsFADB8MQswCQYDVQQGEwJV
        UzELMAkGA1UECAwCSUwxFTATBgNVBAcMDERlZmF1bHQgQ2l0eTERMA8GA1UECgwI
        ZGVtby5sdGQxDjAMBgNVBAsMBXNhbGVzMSYwJAYDVQQDDB0qLnVzLWVhc3QtMi5l
        bGIuYW1hem9uYXdzLmNvbTAeFw0yMjA2MjgwMjI0MTdaFw0yMzA2MjgwMjI0MTda
        MHwxCzAJBgNVBAYTAlVTMQswCQYDVQQIDAJJTDEVMBMGA1UEBwwMRGVmYXVsdCBD
        aXR5MREwDwYDVQQKDAhkZW1vLmx0ZDEOMAwGA1UECwwFc2FsZXMxJjAkBgNVBAMM
        HSoudXMtZWFzdC0yLmVsYi5hbWF6b25hd3MuY29tMIIBIjANBgkqhkiG9w0BAQEF
        AAOCAQ8AMIIBCgKCAQEAslCS5L92wIKN51isIwnRqTiwQP1hPcCsyYBn0zjgVcwB
        fh1PAFaxJv4HJX3EpKugnmGXx9vQ4tdJr4AlhhY3rVMsLZPuCBvF051BEvZ3oXDx
        xRlfwClNjpCgoxbDYOFQ2KVrKJ1UBR6Dalx2fv7+apyb/gijSuiI3CNPvCMUIE7V
        LHR2szYdeuzRe/QaC3xHVx/t/fTpLRKQ6lskM4asfLiI8Btl0uPFSR/LLPX3tCyZ
        wyPhiNmoYgrkDXNufw/fGk3WPqQA5zfvzaoK0Tgz6QHsaxa7ISZ8Pq/tcC3m3/Vu
        +pW1NgRd0CEt+jxcgjG9p81g8rRqLPg+ylj6qZPyXQIDAQABMA0GCSqGSIb3DQEB
        CwUAA4IBAQBLCJi++i2MkNwnnIT4KTNEPr6X9Qm7jkID7eVr5HP9b2MT0tYnQe4P
        YUEu67X8KPG7ctLelqh4GchUcpRrFboqkCZk9rOPFnHhJ/DbwJ0gkluHVd+7c6T1
        d/DVQfEd+8yMEmczAjE8IBo/PUuwspbUNFhkhpxFXMGrHeyXICxKUSQr6RjiOChu
        ltdbzEVBNsrFNF60pgW9zeevKgVPRUyMYZfMuzHzKfTlYnri+COrqwqLnSXyVksa
        xa45U7jnGKb2Bs8/DEyFHgMyL8q0B6l0nfpcB7I4GleYo0/qgHqvYHhYvUYB/bty
        2I628CxT/OfJYfEh2GW5nTtiISa15Bys
        -----END CERTIFICATE-----


**# cat server.key** 
        -----BEGIN RSA PRIVATE KEY-----
        MIIEpAIBAAKCAQEAslCS5L92wIKN51isIwnRqTiwQP1hPcCsyYBn0zjgVcwBfh1P
        AFaxJv4HJX3EpKugnmGXx9vQ4tdJr4AlhhY3rVMsLZPuCBvF051BEvZ3oXDxxRlf
        wClNjpCgoxbDYOFQ2KVrKJ1UBR6Dalx2fv7+apyb/gijSuiI3CNPvCMUIE7VLHR2
        szYdeuzRe/QaC3xHVx/t/fTpLRKQ6lskM4asfLiI8Btl0uPFSR/LLPX3tCyZwyPh
        iNmoYgrkDXNufw/fGk3WPqQA5zfvzaoK0Tgz6QHsaxa7ISZ8Pq/tcC3m3/Vu+pW1
        NgRd0CEt+jxcgjG9p81g8rRqLPg+ylj6qZPyXQIDAQABAoIBAEMZ2w1Fl5R+DJRg
        Y/aTfVhmwrzSHMO2O89gCLINly3yJSWmNdJ0zRlVQq8zEsq84yZ2pz1IVOToCwyF
        9pjsx2rr/5XvMwXOHbWyWYifQwl3jSOUltmjMVJSzoBQ0pkkcN318ctI2RNMFjvy
        K41Cu862vGTuLzTDKK1ehGTR9oLpRfaJp0/CXbgvzQEd/cBsYcPWd9CGjjLZM+6T
        hZJYwY8/jwYwUkjH5G3G/wgEUTFIFPoNQ0PUPs5jwzWH2lQ4wGIE+T4tASBl5KQf
        g6Zi76CJMUiX48yoRXCRi4GmcYlKEVC0Ff+rZYArQTbPdzNxjGmjY/pvrRpbnc/A
        Rwf0NYECgYEA60I3oqW9yCbETj9gwDiGaLULj0lHUR76a6GC70GMdjMJoYDlcnaN
        Rrdxb/88x/VTDfxQvfWMTTiQm2yDJ2/Eohecy6KnVrGkwyYCgc+zESV5d8na/FSb
        J7CyKZBepU4mHb1Iy3Uh+BqUs7JA4ol/ANZljI759dhzctRSkLzehu0CgYEAwgki
        LFVI2+oeHrQwNaeXCGwOz0fYxMeeNcVUz5fKIZwyAUNpmSoy8Icj/6JdGa5aQnLT
        FXJhfMRYsnQFruy3VTrwXoMXo+d7vt9KnNqrtYF8GteSmpuBvOOebmku/fm97zMS
        VwT8VgTDf/gL8Ia8KhcEqOsiE2Xt8qUOtb2BuzECgYAp/g3UOGVhvpm3pdRtOymy
        su43S0sxjagBYjju3/JkfsOvUkSiY8rf3oqfBR4iSwXiLzFyVswOVJRrSbk3Ztng
        XPqd1pCsBtV0B+rWpO4/l0LRQPSXqbpwITgL9zsNop9nG4xM1MGVeZklYiH2zbgf
        vCUwK60uVs50prV+JFhMGQKBgQC+pUq2VHVp3fYKJPDZRvjWhZVnhCgv8BI6stBJ
        x9IKg/V92EaA/z1dpupv2Y+wE+cLMtbDU8cFV8XuUKDk5iCb1XUm55bqrB6hw7MD
        urbLd5YAqZ6Z2gD3Ho4j3aUWVbOQupVieruTqMqNiaHxifCHSmaBscWhWZ0Zs6No
        XfKBgQKBgQCBKNN1ey0LJvRm2U/obw43aoSP2TsaEsQUX+91M0pYSTxoB3gQ4urp
        0B9bAUM1HAy9Xmomi1/lRxAlXAamQ7hVI05SLYloVxyQOPhcBO6WA8xqIPXdp8it
        0TOub/NSt4CpYBnPhdoPjCMyPi2bQt0sj/RUhzw8vwSUkMIq0iEQ5A==
        -----END RSA PRIVATE KEY-----



Now goto AWS ACM --> Import certificate.

Please copy contents of server.crt to “Certificate body” and contents of server.key to “Certificate private key”. Please keep “Certificate chain” empty and click “Next” button. 

![image](https://user-images.githubusercontent.com/74225291/176089196-222e9cb3-7f80-4584-a0a9-1e21bafcd647.png)


<img width="1218" alt="image" src="https://user-images.githubusercontent.com/74225291/176089161-5ed7a377-593d-42b0-be15-0e44d843971c.png">


