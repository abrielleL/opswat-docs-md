<!-- source: https://www.opswat.com/docs/mdcore/v5.22.0/configuration/web-server-processing-statistics-query -->

# Web Server Processing Statistics Query

## [Configure Nginx web server](/docs/mdcore/v5.22.0/configuration/web-server-processing-statistics-query#configure-nginx-web-server)

1.) Create a “status.conf” file

- On Windows, under ***<Installation Directory>\nginx\built-in\status.conf***
- On Linux, under **/etc/ometascan/nginx.d/built-in/status.conf**

location = /nginx_status {
stub_status;
}

2.) A restart of the “OPSWAT Metadefender Core” service is required.

## [Query Nginx processing stats infomation](/docs/mdcore/v5.22.0/configuration/web-server-processing-statistics-query#query-nginx-processing-stats-infomation)

| Property | Value |
| --- | --- |
| **DESCRIPTION** | Query Nginx processing stats information |
| **URL** | http://<server>:8008/nginx_status |
| **HTTP METHOD** | GET |

**Response**

| Result code | Value | Description |
| --- | --- | --- |
| **200** | `Active connections: <n>``server accepts handled requests``<a1> <a2> <a3>``Reading: <b1> Writing: <b2> Waiting: <b3>` For example: `Active connections:``1``server accepts handled requests``144``144``358``Reading:``0``Writing:``1``Waiting:``0` | Request processed successfully.   - Active connections <n>   The current number of active client connections including Waiting <b3> connections.   - accepts <a1>   The total number of accepted client connections.   - handled <a2>   The total number of handled connections. Generally, the parameter value is the same as accepts <a1> unless some resource limits have been reached (for example, the [worker_connections](http://nginx.org/en/docs/ngx_core_module.html#worker_connections) limit).   - requests <a3>   The total number of client requests.   - Reading <b1>   The current number of connections where nginx is reading the request header.   - Writing <b2>   The current number of connections where nginx is writing the response back to the client.   - Waiting <b3>   The current number of idle client connections waiting for a request. |
