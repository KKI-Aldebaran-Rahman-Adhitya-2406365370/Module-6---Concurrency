# Commit 1 Reflection Notes
The code so far successfully initializes a web server by binding a TcpListener to the local network address 127.0.0.1 on port 7878.
The bind function returns a Result type and the utilization of unwrap() acts as a way to handle errors where it panics on purpose and terminates the program if the port is already occupied by another process.
When a listener is active, it iterates over incoming TcpStream connections from the client which is the web browser.
Inside the handle_connection function, a BufReader is used to wrap the mutable stream. This is important because it buffers the raw byte reads from the network which prevents the system from making a number of inefficient micro-calls to the operating system.
By mapping over the buffered lines and collecting them into a vector, the program efficiently parses the raw text of the HTTP request, allowing us to see the GET / HTTP/1.1 method and the associated headers.
Overall, this milestone demonstrates the mechanics of how a server intercepts raw TCP network traffic and prepares it for application-level processing.