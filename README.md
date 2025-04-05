**The English documentation is shown below the Chinese version.**

这是一个Python的轻量级HTTP文件服务器，可以取代python自带的`http.server`模块，基于`socket`模块实现。  
服务器应用`mimetypes`库，自动根据扩展名判断文件的类型`content-type`，并基于`chardetect`库自动检测编码；  
此外服务器实现了分块发送响应数据，实现了限制下载速度和断点续传功能，适合传输大文件，并能处理POST请求提交的表单和文件。  

## 用法

1. **启动服务器**：
   运行程序时，需要提供端口号作为命令行参数。例如：
   ```bash
   python http_file_server.py <可选的端口号，如8080>
   ```
   这将启动一个在8080端口监听的HTTP文件服务器。如果没有指定端口号，端口默认为HTTP使用的80。

2. **访问文件**：
   启动服务器后，可以通过浏览器访问当前工作目录中的文件，例如：
   ```
   http://127.0.0.1/path/index.html
   ```
   `.htm`或`.html`文件的扩展名可以省略。如`127.0.0.1/path/index`和`127.0.0.1/path/index.html`是一样的。
   此外，如果文件夹下有名为`index`的文件（无论扩展名为何），文件名也是可以省略的。
   如`127.0.0.1/path`和`127.0.0.1/path/index.css`也是相同的。

3. **日志记录**：
   可以将服务器的输出日志重定向到文件以记录日志，例如：
   ```bash
   python http_file_server.py 8080 > server_log.txt
   ```
   这将把所有的日志记录到 `server_log.txt` 文件中。

## 功能

1. **基于扩展名自动检测Content-Type**：
   服务器应用 `mimetypes` 库自动判断文件的内容类型。客户端在请求文件时，服务器会根据文件的扩展名来设置 `Content-Type` 头。

2. **自动编码检测**：
   服务器使用 `chardet` 库来自动检测文件的编码格式，解决了乱码问题。

3. **分块发送响应数据**：
   服务器实现了分块发送响应数据，使得服务器能限制下载速度，并支持断点续传。

4. **处理POST请求**：
   服务器实现了处理POST请求，支持用户通过表单提交数据，以及上传文件。

5. **安全性**：
   服务器能检测`..`等常见的上级目录攻击格式，避免了常见的目录遍历攻击。


This is a lightweight HTTP file server implemented in Python, serving as a replacement for the built-in `http.server` module and based on the `socket` module.  
The server utilizes the `mimetypes` library to automatically determine the file's content type based on its file extension, and uses the `chardet` library for automatic encoding detection.  
In addition, the server implements chunked response data transfer, enabling download speed limits and resume capabilities, making it suitable for large file transfers. The server can also handle POST requests submitted by forms and files.  

## Usage

1. **Starting the Server**:
   When running the program, you need to provide a port number as a command line argument. For example:
   ```bash
   python http_file_server.py <optional port number, e.g., 8080>
   ```
   This will start an HTTP file server listening on port 8080. If no port number is specified, the default port will be 80 for HTTP.

2. **Accessing Files**:
   After starting the server, you can access files in the current working directory via a browser, for example:
   ```
   http://127.0.0.1/path/index.html
   ```
   The extensions `.htm` or `.html` can be omitted. For instance, `127.0.0.1/path/index` and `127.0.0.1/path/index.html` are equivalent.
   Additionally, if there is a file named `index` in a folder (regardless of the extension), the filename can also be omitted.
   For example, `127.0.0.1/path` and `127.0.0.1/path/index.css` are the same.

3. **Logging**:
   You can redirect the server's output logs to a file for logging purposes, for example:
   ```bash
   python http_file_server.py 8080 > server_log.txt
   ```
   This will log all output to the `server_log.txt` file.

## Features

1. **Automatic Content-Type Detection Based on File Extension**:  
   The server application uses the `mimetypes` library to automatically determine the content type of files. When the client requests a file, the server sets the `Content-Type` header based on the file's extension.

2. **Automatic Encoding Detection**:  
   The server uses the `chardet` library to automatically detect the encoding format of files, resolving issues with garbled text.

3. **Chunked Response Data Transmission**:  
   The server implements chunked response data transmission, allowing it to limit download speeds and support resuming interrupted downloads.

4. **Handling POST Requests**:  
   The server is capable of handling POST requests, enabling users to submit data through forms and upload files.

5. **Security**:  
   The server can detect common directory traversal attack patterns, such as `..`, preventing common directory traversal attacks.