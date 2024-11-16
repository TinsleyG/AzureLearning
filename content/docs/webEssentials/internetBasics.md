---
title: Internet Basics
type: docs
weight: 1
sidebar:
  open: false
prev: webEssentials/
next: docs/folder/
---

The process of accessing a website in a browser involves several steps that occur in a matter of milliseconds. Here's a detailed breakdown of what happens behind the scenes:

---

### **1. User Action**
- You type a URL (e.g., `www.example.com`) into your browser or click a link.

---

### **2. Browser Processes the URL**
- The browser parses the URL to determine:
  - The protocol (`http://` or `https://`).
  - The domain name (`www.example.com`).
  - The path (`/home`).
  - Query parameters (e.g., `?id=123`).

---

### **3. Domain Name System (DNS) Lookup**
- The browser checks if it has the IP address of the domain cached.
- If not, it sends a query to a DNS resolver (your ISP or a third-party service like Google DNS).
  - The resolver queries root name servers, Top-Level Domain (TLD) servers, and authoritative name servers to find the IP address associated with `www.example.com`.
  - The resolved IP address (e.g., `93.184.216.34`) is returned to the browser.

---

### **4. Establishing a Connection**
- **TCP Handshake**: The browser establishes a connection to the web server using the Transmission Control Protocol (TCP).
  - The client and server exchange packets to synchronize and agree on communication parameters.
  - This involves three steps:
    1. SYN (synchronize).
    2. SYN-ACK (synchronize-acknowledge).
    3. ACK (acknowledge).
- **TLS Handshake (if HTTPS)**: For secure websites, the browser negotiates encryption parameters with the server using the Transport Layer Security (TLS) protocol.

---

### **5. Sending the HTTP Request**
- Once the connection is established, the browser sends an HTTP (or HTTPS) request to the server.
  - Example:
    ```
    GET /home HTTP/1.1
    Host: www.example.com
    ```

---

### **6. Server Processes the Request**
- The server receives the request and:
  - Determines which resource (e.g., a webpage or image) is being requested.
  - Executes any backend processes (e.g., retrieving data from a database or running scripts).
  - Prepares the response, typically an HTML document along with associated resources (CSS, JavaScript, images).

---

### **7. Response Sent Back to Browser**
- The server sends the response over the established connection.
  - Example:
    ```
    HTTP/1.1 200 OK
    Content-Type: text/html
    ```
  - This is followed by the HTML content of the webpage.

---

### **8. Browser Renders the Page**
- The browser processes the HTML and starts rendering the webpage:
  1. **HTML Parsing**: Builds the Document Object Model (DOM) tree.
  2. **CSS Parsing**: Applies styles to the DOM tree.
  3. **JavaScript Execution**: Executes scripts to add interactivity.
  4. **Resource Fetching**: Downloads additional resources (e.g., images, fonts) referenced in the HTML.

---

### **9. Displaying the Website**
- The browser assembles all the elements and renders the fully styled, interactive webpage for you to see.

---

### **Key Concepts Behind the Scenes**
- **Caching**: Intermediate systems (e.g., DNS caches, browser caches, or Content Delivery Networks) can store copies of frequently accessed data to speed up the process.
- **Protocols**: HTTP, HTTPS, TCP/IP, and DNS protocols govern the communication between your browser, the DNS servers, and the web server.
- **Network Routing**: Data packets travel through multiple routers and networks to reach the server and back, using the fastest available paths.

---

### Diagrammatic Flow (Simplified)
1. **Browser** → DNS Lookup → IP Address
2. **Browser** → TCP/TLS Handshake → Web Server
3. **Browser** → HTTP Request → Web Server
4. **Web Server** → Response (HTML, CSS, JS, etc.) → Browser
5. **Browser** → Renders Content