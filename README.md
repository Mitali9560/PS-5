# Cryptography Simulation Project

## Overview
This project demonstrates a cryptography simulation using mbedTLS/OpenSSL library for securing a custom communication protocol between two parties: a patient and an AI psychologist named ELIZA. The goal is to secure the traffic using RSA certificates and secure the protocol.

## Problem Statement
1. *Creating Digital Certificates*:
    - Create a self-signed root certificate (rootCA.crt) with RSA key size of 3072, SHA384, and serial number 01.
    - Generate RSA keypair of size 3072 with SHA384 for "Alice", sign with rootCA, and set serial number 02.
    - Generate RSA keypair of size 3072 with SHA384 for "Bob", sign with rootCA, and set serial number 03.

2. *Securing a Custom Protocol*:
    - Secure a custom communication protocol between a patient and the AI psychologist (ELIZA).
    - Implement basic cryptography wrappers and make the crypto unit tests pass.
    - Secure the protocol using your cryptography wrapper implementation.

## Prerequisites
1. *OpenSSL*: Install OpenSSL for Windows from [OpenSSL for Windows](https://slproweb.com/products/Win32OpenSSL.html).
2. *Visual Studio*: Install Visual Studio with C++ development tools from [Visual Studio](https://visualstudio.microsoft.com/).
3. *CMake*: Install CMake from [CMake.org](https://cmake.org/download/).
4. *Git Bash or WSL (optional)*: Install Git Bash from [Git for Windows](https://gitforwindows.org/) or enable Windows Subsystem for Linux (WSL).

## Setup Instructions

### Extract the Zip File
Extract the contents of the zip file into a directory.

### Open the Project in Visual Studio
1. Open the solution file (udp_party.sln) in Visual Studio.

### Configure Project Settings
1. Right-click on the udp_party project in Solution Explorer and select *Properties*.
2. Under *Configuration Properties > C/C++ > General, set the **Additional Include Directories* to the include directory of your OpenSSL installation (e.g., C:\Program Files\OpenSSL-Win64\include).
3. Under *Configuration Properties > Linker > General, set the **Additional Library Directories* to the lib directory of your OpenSSL installation (e.g., C:\Program Files\OpenSSL-Win64\lib).
4. Under *Configuration Properties > Linker > Input, add the OpenSSL libraries (libssl.lib and libcrypto.lib) to the **Additional Dependencies*.

### Generate Certificates (if needed)
Use Git Bash or WSL to generate the necessary certificates, or use the provided certificates. Here are the OpenSSL commands for reference:
```bash
openssl req -x509 -newkey rsa:3072 -keyout certificates/rootCA.key -out certificates/rootCA.crt -days 365 -sha384 -set_serial 01
openssl req -new -newkey rsa:3072 -keyout certificates/alice.key -out certificates/alice.csr -sha384
openssl x509 -req -in certificates/alice.csr -CA certificates/rootCA.crt -CAkey certificates/rootCA.key -out certificates/alice.crt -days 365 -CAcreateserial -sha384 -set_serial 02
openssl req -new -newkey rsa:3072 -keyout certificates/bob.key -out certificates/bob.csr -sha384
openssl x509 -req -in certificates/bob.csr -CA certificates/rootCA.crt -CAkey certificates/rootCA.key -out certificates/bob.crt -days 365 -CAcreateserial -sha384 -set_serial 03
