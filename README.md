# rust-advpro | Advance Programming Repository by Muhammad Fadhlan Karimuddin (2306245011)

## Commit 1 Reflection notes

In this commit, I implemented a simple **single threaded** TCP server that listens on `127.0.0.1:7878`. This project has been a valuable opportunity to learn how Rust’s standard library can be used for network programming. I explored the use of `TcpListener` and `TcpStream` to accept and manage incoming connections sequentially. Delving into the `handle_connection` function, I learned how a `BufReader` can efficiently process incoming data line by line until an empty line indicates the end of an HTTP request header. Reading the Rust documentation for these components helped deepen my understanding of error handling, borrowing, and ownership in I/O operations.

### Deeper Dive into the `handle_connection` Function

The `handle_connection` function plays a critical role in managing each client connection. It begins by creating a `BufReader` from the mutable TCP stream:

```rust
let buf_reader = BufReader::new(&mut stream);
```

This use of `BufReader` not only simplifies reading from the stream but also improves performance by buffering input. Next, it processes the incoming data:

```rust
let http_request: Vec<_> = buf_reader
    .lines()
    .map(|result| result.unwrap())
    .take_while(|line| !line.is_empty())
    .collect();
```

In this snippet, the `lines` method creates an iterator over the stream’s content, and each line is unwrapped to obtain the string data. The `take_while` method ensures that reading stops when an empty line is encountered, which traditionally marks the end of the HTTP request header. Finally, the collected lines are printed out, providing a clear view of the request structure.
