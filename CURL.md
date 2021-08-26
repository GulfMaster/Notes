官方教程

~~~
https://curl.se/docs/manual.html
~~~

官方参数说明

~~~
https://curl.se/docs/manpage.html
~~~



curl -w参数说明

~~~
url_effective 最终获取的url地址，尤其是当你指定给curl的地址存在301跳转，且通过-L继续追踪的情形。

http_code http状态码，如200成功,301转向,404未找到,500服务器错误等。(The numerical response code that was found in the last retrieved HTTP(S) or FTP(s) transfer. In 7.18.2 the alias response_code was added to show the same info.)

http_connect The numerical code that was found in the last response (from a proxy) to a curl CONNECT request. (Added in 7.12.4)

time_total 总时间，按秒计。精确到小数点后三位。 （The total time, in seconds, that the full operation lasted. The time will be displayed with millisecond resolution.）

time_namelookup DNS解析时间,从请求开始到DNS解析完毕所用时间。(The time, in seconds, it took from the start until the name resolving was completed.)

time_connect 连接时间,从开始到建立TCP连接完成所用时间,包括前边DNS解析时间，如果需要单纯的得到连接时间，用这个time_connect时间减去前边time_namelookup时间。以下同理，不再赘述。(The time, in seconds, it took from the start until the TCP connect to the remote host (or proxy) was completed.)

time_appconnect 连接建立完成时间，如SSL/SSH等建立连接或者完成三次握手时间。(The time, in seconds, it took from the start until the SSL/SSH/etc connect/handshake to the remote host was completed. (Added in 7.19.0))

time_pretransfer 从开始到准备传输的时间。(The time, in seconds, it took from the start until the file transfer was just about to begin. This includes all pre-transfer commands and negotiations that are specific to the particular protocol(s) involved.)

time_redirect 重定向时间，包括到最后一次传输前的几次重定向的DNS解析，连接，预传输，传输时间。(The time, in seconds, it took for all redirection steps include name lookup, connect, pretransfer and transfer before the final transaction was started. time_redirect shows the complete execution time for multiple redirections. (Added in 7.12.3))

time_starttransfer 开始传输时间。在发出请求之后，Web 服务器返回数据的第一个字节所用的时间(The time, in seconds, it took from the start until the first byte was just about to be transferred. This includes time_pretransfer and also the time the server needed to calculate the result.)


content_type 就是content-Type，示例(text/html; charset=UTF-8)；(The Content-Type of the requested document, if there was any.)

num_connects 最近的的一次传输中创建的连接数目。Number of new connects made in the recent transfer. (Added in 7.12.3)

num_redirects 在请求中跳转的次数。Number of redirects that were followed in the request. (Added in 7.12.3)

redirect_url When a HTTP request was made without -L to follow redirects, this variable will show the actual URL a redirect would take you to. (Added in 7.18.2)

ftp_entry_path 当连接到远程的ftp服务器时的初始路径。The initial path libcurl ended up in when logging on to the remote FTP server. (Added in 7.15.4)

ssl_verify_result ssl认证结果，返回0表示认证成功。( The result of the SSL peer certificate verification that was requested. 0 means the verification was successful. (Added in 7.19.0))
~~~

英文原版

~~~
Make curl display information on stdout after a completed transfer. The format is a string that may contain plain text mixed with any number of variables. The format can be specified as a literal "string", or you can have curl read the format from a file with "@filename" and to tell curl to read the format from stdin you write "@-".

The variables present in the output format will be substituted by the value or text that curl thinks fit, as described below. All variables are specified as %{variable_name} and to output a normal % you just write them as %%. You can output a newline by using \n, a carriage return with \r and a tab space with \t.

The output will be written to standard output, but this can be switched to standard error by using %{stderr}.

NOTE: The %-symbol is a special symbol in the win32-environment, where all occurrences of % must be doubled when using this option.

The variables available are:

    content_type The Content-Type of the requested document, if there was any.

    errormsg The error message. (Added in 7.75.0)

    exitcode The numerical exitcode of the transfer. (Added in 7.75.0)

    filename_effective The ultimate filename that curl writes out to. This is only meaningful if curl is told to write to a file with the -O, --remote-name or -o, --output option. It's most useful in combination with the -J, --remote-header-name option. (Added in 7.26.0)

    ftp_entry_path The initial path curl ended up in when logging on to the remote FTP server. (Added in 7.15.4)

    http_code The numerical response code that was found in the last retrieved HTTP(S) or FTP(s) transfer. In 7.18.2 the alias response_code was added to show the same info.

    http_connect The numerical code that was found in the last response (from a proxy) to a curl CONNECT request. (Added in 7.12.4)

    http_version The http version that was effectively used. (Added in 7.50.0)

    json A JSON object with all available keys.

    local_ip The IP address of the local end of the most recently done connection - can be either IPv4 or IPv6. (Added in 7.29.0)

    local_port The local port number of the most recently done connection. (Added in 7.29.0)

    method The http method used in the most recent HTTP request. (Added in 7.72.0)

    num_connects Number of new connects made in the recent transfer. (Added in 7.12.3)

    num_headers The number of response headers in the most recent request (restarted at each  redirect). Note that the status line IS NOT a header. (Added in 7.73.0)

    num_redirects Number of redirects that were followed in the request. (Added in 7.12.3)

    onerror The rest of the output is only shown if the transfer returned a non-zero error (Added in 7.75.0)

    proxy_ssl_verify_result The result of the HTTPS proxy's SSL peer certificate verification that was requested. 0 means the verification was successful. (Added in 7.52.0)

    redirect_url When an HTTP request was made without -L, --location to follow redirects (or when --max-redirs is met), this variable will show the actual URL a redirect would have gone to. (Added in 7.18.2)

    referer The Referer: header, if there was any. (Added in 7.76.0)

    remote_ip The remote IP address of the most recently done connection - can be either IPv4 or IPv6. (Added in 7.29.0)

    remote_port The remote port number of the most recently done connection. (Added in 7.29.0)

    response_code The numerical response code that was found in the last transfer (formerly known as "http_code"). (Added in 7.18.2)

    scheme The URL scheme (sometimes called protocol) that was effectively used. (Added in 7.52.0)

    size_download The total amount of bytes that were downloaded.

    size_header The total amount of bytes of the downloaded headers.

    size_request The total amount of bytes that were sent in the HTTP request.

    size_upload The total amount of bytes that were uploaded.

    speed_download The average download speed that curl measured for the complete download. Bytes per second.

    speed_upload The average upload speed that curl measured for the complete upload. Bytes per second.

    ssl_verify_result The result of the SSL peer certificate verification that was requested. 0 means the verification was successful. (Added in 7.19.0)

    stderr From this point on, the -w, --write-out output will be written to standard error. (Added in 7.63.0)

    stdout From this point on, the -w, --write-out output will be written to standard output. This is the default, but can be used to switch back after switching to stderr. (Added in 7.63.0)

    time_appconnect The time, in seconds, it took from the start until the SSL/SSH/etc connect/handshake to the remote host was completed. (Added in 7.19.0)

    time_connect The time, in seconds, it took from the start until the TCP connect to the remote host (or proxy) was completed.

    time_namelookup The time, in seconds, it took from the start until the name resolving was completed.

    time_pretransfer The time, in seconds, it took from the start until the file transfer was just about to begin. This includes all pre-transfer commands and negotiations that are specific to the particular protocol(s) involved.

    time_redirect The time, in seconds, it took for all redirection steps including name lookup, connect, pretransfer and transfer before the final transaction was started. time_redirect shows the complete execution time for multiple redirections. (Added in 7.12.3)

    time_starttransfer The time, in seconds, it took from the start until the first byte was just about to be transferred. This includes time_pretransfer and also the time the server needed to calculate the result.

    time_total The total time, in seconds, that the full operation lasted.

    url The URL that was fetched. (Added in 7.75.0)

    urlnum The URL index number of this transfer, 0-indexed. De-globbed URLs share the same index number as the origin globbed URL. (Added in 7.75.0)

    url_effective The URL that was fetched last. This is most meaningful if you've told curl to follow location: headers.


    If this option is used several times, the last one will be used.

--xattr

When saving output to a file, this option tells curl to store certain file metadata in extended file attributes. Currently, the URL is stored in the xdg.origin.url attribute and, for HTTP, the content type is stored in the mime_type attribute. If the file system does not support extended attributes, a warning is issued.
~~~

