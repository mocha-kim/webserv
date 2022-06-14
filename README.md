# 🌏 webserv

### 42 webserv subject : HTTP 서버 만들기
This project is about writing your ow HTTP server. You will be able to test it with an actual browser.

22.01.24 ~ 21.06.10

[@mocha-kim](https://github.com/mocha-kim) [@AYoungSn](https://github.com/AYoungSn) [@Two-Jay](https://github.com/Two-Jay) [@byeori0306](https://github.com/byeori0306)

- `GET`, `POST`, `DELETE` 메서드를 실행할 수 있습니다.
- 브라우저를 이용해 웹페이지를 띄울 수 있습니다.
- `autoindex`가 켜져있는 서버의 경우에는, 해당 디렉토리의 구조를 자동으로 인덱싱해서 보여줍니다.
- 프로그램은 `configuration` 파일을 인자로 받는데, configuration은 nginx와 비슷하게 적용됩니다.
- configuration에 적혀있는 여러 서버를 한번에 열 수 있습니다. 그러니까, 여러 포트의 여러 서버를 실행 할 수 있습니다.
- configuration 파일에 같은 포트 넘버를 갖고 있는 서버 블록이 여러개일 경우, hostname에 따라 서버를 동작시킵니다(hostname까지 같은 서버 블록은 무시됨). 요청에 hostname이 명시되지 않은 경우에는 가장 첫번째로 등장하는 서버블록을 default로 삼습니다.
- `CGI` 요청을 처리할 수 있습니다.(GET, POST)


> ## Requirements
> - Your program has to take a configuration file as argument, or use a default path.
> - You can’t execve another web server.
> - Your server must never block and the client can be bounced properly if necessary.
> - It must be non-blocking and use only 1 poll() (or equivalent) for all the I/O operations between the client and the server (listen included).
> - poll() (or equivalent) must check read and write at the same time.
> - You must never do a read or a write operation without going through poll() (or equivalent).
> - Checking the value of errno is strictly forbidden after a read or a write operation.
> - You don’t need to use poll() (or equivalent) before reading your configuration file.
> - You can use every macro and define like FD_SET, FD_CLR, FD_ISSET, FD_ZERO (understanding what and how they do it is very useful).
> - A request to your server should never hang forever.
> - Your server must be compatible with the web browser of your choice.
> - We will consider that NGINX is HTTP 1.1 compliant and may be used to compare headers and answer behaviors.
> - Your HTTP response status codes must be accurate.
> - You server must have default error pages if none are provided.
> - You can’t use fork for something else than CGI (like PHP, or Python, and so forth).
> - You must be able to serve a fully static website.
> - Clients must be able to upload files.
> - You need at least GET, POST, and DELETE methods.
> - Stress tests your server. It must stay available at all cost.
> - Your server must be able to listen to multiple ports (see Configuration file).

> ## Configuration file
> - Choose the port and host of each ’server’.
> - Setup the server_names or not.
> - The first server for a host:port will be the default for this host:port
> - Setup default error pages.
> - Limit client body size.
> - Setup routes with one or multiple of the following rules/configuration (routes wont be using regexp):
  > - Define a list of accepted HTTP methods for the route.
  > - Define a HTTP redirection.
  > - Define a directory or a file from where the file should be searched
  > - Turn on or off directory listing.
  > - Set a default file to answer if the request is a directory.
  > - Execute CGI based on certain file extension (for example .php).
  > - Make the route able to accept uploaded files and configure where they should
be saved.
    > - Do you wonder what a CGI is?
    > - Because you won’t call the CGI directly, use the full path as PATH_INFO.
    > - Just remember that, for chunked request, your server needs to unchunked
    > - and the CGI will expect EOF as end of the body.
    > - Same things for the output of the CGI. If no content_length is returned
from the CGI, EOF will mark the end of the returned data.
    > - Your program should call the CGI with the file requested as first argument.
    > - The CGI should be run in the correct directory for relative path file access.
    > - Your server should work with one CGI (php-CGI, Python, and so forth).

