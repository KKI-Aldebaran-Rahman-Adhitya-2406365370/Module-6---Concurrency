# Commit 1 Reflection Notes
The code so far successfully initializes a web server by binding a TcpListener to the local network address 127.0.0.1 on port 7878.
The bind function returns a Result type and the utilization of unwrap() acts as a way to handle errors where it panics on purpose and terminates the program if the port is already occupied by another process.
When a listener is active, it iterates over incoming TcpStream connections from the client which is the web browser.
Inside the handle_connection function, a BufReader is used to wrap the mutable stream. This is important because it buffers the raw byte reads from the network which prevents the system from making a number of inefficient micro-calls to the operating system.
By mapping over the buffered lines and collecting them into a vector, the program efficiently parses the raw text of the HTTP request, allowing us to see the GET / HTTP/1.1 method and the associated headers.
Overall, this milestone demonstrates the mechanics of how a server intercepts raw TCP network traffic and prepares it for application-level processing.

# Commit 2 Reflection Notes
![commit2.png](commit2.png)
In this milestone, the server's capability is expanded to actually read web content than just reading incoming requests.
To achieve this, the std::fs module is needed which allows the Rust program to read contents of the local hello.html file directly into a string variable.
The HTML content is then dynamically formatted to be compatible with HTTP's response payload.
A valid HTTP response requires a specific syntax with structure, beginning with a status line, which in this implementation is HTTP/1.1 200 OK to signify a successful network request.
Additionally, the Content-Length header is dynamically calculated using the len() method on the file contents, which is an important standard protocol that lets the receiving web browser know exactly how many bytes to expect.
Finally, the complete string is converted into an array of raw bytes and written back to the TcpStream using the write_all method.
The completion of this step allows the application to demonstrate a full request-response lifecycle by successfully serving a customized, static HTML file over a TCP connection.