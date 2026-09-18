# Home Cybersecurity Lab: Service Detection and Log Analysis

## Objective

The purpose of this lab was to build a controlled cybersecurity environment using Kali Linux and Ubuntu through WSL. I used Nmap to identify open ports and running services, tested an HTTP service, and analyzed server logs to understand how network reconnaissance can be detected.

## Lab Environment

- Host: Windows 11 ARM64
- Security workstation: Kali Linux (WSL)
- Target environment: Ubuntu 24.04 LTS (WSL)
- Architecture: ARM64 (aarch64)
- Security tool: Nmap 7.99
- Test service: Python HTTP server
- Test port: TCP 8080

## What I Did

I started by scanning my Kali system with Nmap to see if any common ports were open.

`nmap 127.0.0.1`

All 1,000 ports were closed. I then started a Python web server on port 8000 and scanned again. This time Nmap showed port 8000 as open.

`nmap -sV -p 8000 127.0.0.1`

Using `-sV` also showed me what service was running on the port.

Next, I created another Python HTTP server using Ubuntu WSL on port 8080. From Kali, Nmap detected:

`8080/tcp open http SimpleHTTPServer 0.6 (Python 3.12.3)`

I also used curl to connect to the server:

`curl http://127.0.0.1:8080`

The server returned:

`Authorized Cybersecurity Lab Target`

## What I Learned

I learned how Nmap can find open ports and identify services running on them. I also learned that when a service is stopped, the port goes back to being closed.

When I used Nmap service detection, I noticed that it created multiple requests in the HTTP server logs. This showed me that scanning activity can leave evidence that a security analyst could investigate.

## Log Analysis & Findings

I saved the HTTP server logs and compared normal web traffic with the Nmap scan.

A normal request showed:

`GET / HTTP/1.1 200`

The `200` meant the request was successful. During the Nmap scan, I noticed multiple requests that returned `404` and `501` errors. One request even included `nmaplowercheck` in the log.

This showed me that an Nmap service scan creates activity that can be seen in server logs. Looking at logs can help a security analyst understand what is happening on a system.

## Security Takeaway

This lab helped me understand why open ports and unnecessary services can create security risks. I also learned how tools like Nmap can be used to discover services and how logs can provide evidence of scanning activity.
