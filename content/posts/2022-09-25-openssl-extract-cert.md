+++ 
draft = false
date = 2022-09-25T07:40:12Z
title = "Extract a Certificate by Using OpenSSL"
authors = ["Saikat"]
tags = ["openssl", "certificate"]
categories = [""]
+++

## Extract a Certificate by Using OpenSSL

In this quick tutorial we are going to see 

On a Linux or UNIX system, you can use the openssl command to extract the certificate from a key pair that you downloaded from the OAuth Configuration page.

To extract the certificate, use these commands, where cer is the file name that you want to use:
`openssl pkcs12 -in store.p12 -out cer.pem`
This extracts the certificate in a .pem format.

`openssl x509 -outform der -in cer.pem -out cer.der`
This formats the certificate in a .der format.

You can also extract the private key by using the command:
`openssl pkcs12 -in store.p12 -out pKey.pem -nodes -nocerts`

For more information, see the [OpenSSL](https://www.openssl.org/docs/) documentation.
