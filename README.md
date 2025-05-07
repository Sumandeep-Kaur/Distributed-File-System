# Distributed-File-System
This project implements a simple Distributed File System using C and a multi-threaded client-server architecture. The system supports basic file operations and intelligently distributes files across multiple sub-servers based on their type, while remaining transparent to the user.

## Features
- Client-Server Architecture: A client connects to a main server to request file operations.
- Multi-Threaded Server: The main server can handle multiple clients concurrently.
- Distributed File Handling: Based on file type, requests are forwarded to specialized sub-servers:
  - PDF files: Handled by server_pdf.c
  - Text files: Handled by server_txt.c
  - Other file types: Handled by server_misc.c
- Transparent Redirection: Users interact with a single interface (the client) and are unaware of the underlying distribution.

## File Structure
<pre>
├── client.c            # Client program
├── server_main.c       # Main server handling client requests 
├── server_pdf.c        # Sub-server handling .pdf files 
├── server_txt.c        # Sub-server handling .txt files 
├── server_misc.c       # Sub-server for other file types 
├── README.md           # Project documentation 
</pre>

## Setup Instructions

#### 1. Compilation
Use gcc to compile each component. Run these commands in the terminal:
<pre>
gcc -o client client.c 
gcc -o server_main server_main.c -lpthread
gcc -o server_pdf server_pdf.c
gcc -o server_txt server_txt.c
gcc -o server_misc server_misc.c 
</pre>

#### 2. Running Servers
Start each server in a separate terminal window:
<pre>
./server_pdf
./server_txt
./server_misc
./server_main
</pre>

#### 3. Running Client
In another terminal window, start the client:
<pre>./client </pre>

## How It Works

#### 1. Client Sends Command
The client accepts user input in the format:
- UPLOAD filename.pdf
- DOWNLOAD filename.txt
- LIST
- DELETE filename
- EXIT

#### 2. Main Server Handles Command
The server_main receives this command, parses the file type, and forwards the request to the appropriate sub-server.

#### 3. Sub-Server Processes Request
The corresponding server (server_pdf, server_txt, or server_misc) responds to the request and sends a confirmation message back.
