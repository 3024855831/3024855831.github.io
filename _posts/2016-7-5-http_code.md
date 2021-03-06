---
layout: post
title:  "HTTP返回状态码说明"
date:   2016-7-5 20:56:01 +0800
categories: http
tag: 小记
---

* content
{:toc}



如果某项请求发送到您的服务器要求显示您网站上的某个网页（例如，用户通过浏览器访问您的网页或 Googlebot 抓取网页时），服务器会返回 HTTP 状态码响应请求。

此状态码提供关于请求状态的信息，告诉 Googlebot 
关于您的网站和请求的网页的信息。
一些常见的状态码为：

200 – 服务器成功返回网页
404 – 请求的网页不存在
503 – 服务器超时

以下是 HTTP 状态码的完整列表。您也可以访问 HTTP 状态码上的 W3C 页以了解更多信息。

1xx 状态码

表示临时响应并需要请求者继续执行操作的状态码。

| 100（继续）        | 请求者应当继续提出请求。服务器返回此代码表示已收到请求的第一部分，正在等待其余部分。           |
| 101（切换协议）      | 请求者已要求服务器切换协议，服务器已确认并准备切换。 |
	
	
2xx 状态码

表示成功处理了请求的状态码。

| 200（成功）        | 服务器已成功处理了请求。通常，这表示服务器提供了请求的网页。如果针对您的 robots.txt 文件显示此状态码，则表示 Googlebot 已成功检索到该文件。          |
| 201（已创建）      | 请求成功并且服务器创建了新的资源。 |
| 202（已接受）      | 服务器已接受请求，但尚未处理。 |
| 203（非授权信息）      | 服务器已成功处理了请求，但返回的信息可能来自另一来源。 |
| 204（无内容）      | 服务器成功处理了请求，但没有返回任何内容。 |
| 205（重置内容）      | 服务器成功处理了请求，但没有返回任何内容。与 204 响应不同，此响应要求请求者重置文档视图（例如，清除表单内容以输入新内容）。 |


3xx 状态码

要完成请求，需要进一步操作。通常，这些状态码用来重定向。Google 建议您在每次请求中使用重定向不要超过 5 次。您可以使用网站管理员工具查看一下 Googlebot 在抓取重定向网页时是否遇到问题。诊断下的网络抓取页列出了由于重定向错误导致 Googlebot 无法抓取的网址。

| 300（多种选择）      | 针对请求，服务器可执行多种操作。服务器可根据请求者 (user-agent) 选择一项操作，或提供操作列表供请求者选择。 |
| 301（永久移动）      | 请求的网页已永久移动到新位置。服务器返回此响应（对 GET 或 HEAD 请求的响应）时，会自动将请求者转到新位置。您应使用此代码告诉 Googlebot 某个网页或网站已永久移动到新位置。 |
| 302（临时移动）      | 服务器目前从不同位置的网页响应请求，但申请人应当继续使用原有位置来响应以后的请求。此代码与响应 GET 和 HEAD 请求的 301 代码类似，会自动将请求者转到不同的位置，但不应使用此代码来告诉 Googlebot 页面或网站已经移动，因为 Googlebot 要继续抓取原来的位置并编制索引。 |
| 303（查看其他位置）      | 请求者应当对不同的位置使用单独的 GET 请求来检索响应时，服务器返回此代码。对于除 HEAD 之外的所有请求，服务器会自动转到其他位置。 |
| 304（未修改）      | 自从上次请求后，请求的网页未修改过。服务器返回此响应时，不会返回网页内容。如果网页自请求者上次请求后再也没有更改过，您应当将服务器配置为返回此响应（称为 If-Modified-Since HTTP 标头）。由于服务器可以告诉 Googlebot 自从上次抓取后网页没有变更，因此可节省带宽和开销 |
| 305（使用代理）      | 请求者只能使用代理访问请求的网页。如果服务器返回此响应，还表示请求者应当使用代理。 |
| 307（临时重定向）      | 服务器目前从不同位置的网页响应请求，但请求者应当继续使用原有位置来响应以后的请求。此代码与响应 GET 和 HEAD 请求的 <a href=answer.py?answer=>301</a> 代码类似，会自动将请求者转到不同的位置，但您不应使用此代码来告诉 Googlebot 某个网页或网站已经移动，因为 Googlebot 会继续抓取原有位置并编制索引。 |

	
4xx 状态码

这些状态码表示请求可能出错，这妨碍了服务器的处理。

| 401（身份验证错误）      | 此页要求授权。您可能不希望将此网页纳入索引。如果您的 Sitemap 中列出该网页，您可以将其删除。但如果您将其保留在您的 Sitemap 中，我们就不会抓取或索引该网页（尽管该网页将继续保持错误状态在此处列出）。如果我们将其作为搜索抓取的一部分抓取，您可以在我们的网站管理员信息中查 阅其原因。 |
| 403（禁止）      | 服务器拒绝请求。如果您在 Googlebot 尝试抓取您网站上的有效网页时看到此状态码（可以在 Google 网站管理员工具<strong>诊断</strong>下的<strong>网络抓取< /strong>页面上看到此信息），可能是您的服务器或主机拒绝 Googlebot 访问。 |
| 404（未找到）      | 服务器找不到请求的网页。例如，对于服务器上不存在的网页经常会返回此代码。 |
| 405（方法禁用）      | 禁用请求中指定的方法。 |
| 406（不接受）      | 无法使用请求的内容特性响应请求的网页。 |
| 407（需要代理授权）      | 此状态码与 401 类似，但指定请求者必须授权使用代理。如果服务器返回此响应，还表示请求者应当使用代理。 |
| 408（请求超时）      | 服务器等候请求时发生超时。 |
| 409（冲突）      | 服务器在完成请求时发生冲突。服务器必须在响应中包含有关冲突的信息。服务器在响应与前一个请求相冲突的 PUT 请求时可能会返回此代码，以及两个请求的差异列表。 |
| 410（已删除）      | 请求的资源永久删除后，服务器返回此响应。该代码与 404（未找到）代码相似，但在资源以前存在而现在不存在的情况下，有时会用来替代 404 代码。如果资源已永久删除，您应当使用 301 指定资源的新位置。 |
| 411（需要有效长度）      | 服务器不接受不含有效内容长度标头字段的请求。 |
| 412（未满足前提条件）      | 服务器未满足请求者在请求中设置的其中一个前提条件。 |
| 413（请求实体过大）      | 服务器无法处理请求，因为请求实体过大，超出服务器的处理能力。 |
| 414（请求的 URI 过长）      | 请求的 URI（通常为网址）过长，服务器无法处理。 |
| 415（不支持的媒体类型）      | 请求的格式不受请求页面的支持。 |
| 416（请求范围不符合要求）      | 如果页面无法提供请求的范围，则服务器会返回此状态码。 |
| 417（未满足期望值）      | 服务器未满足”期望”请求标头字段的要求。 |


5xx 状态码

这些状态码表示服务器在处理请求时发生内部错误。这些错误可能是服务器本身的错误，而不是请求出错。

| 500（服务器内部错误）      | 服务器遇到错误，无法完成请求。 |
| 501（尚未实施）      | 服务器不具备完成请求的功能。例如，服务器无法识别请求方法时则会返回此代码。 |
| 502（错误网关）      | 服务器作为网关或代理，从上游服务器收到无效响应。 |
| 503（服务不可用）      | 服务器目前无法使用（由于超载或停机维护）。通常，这只是暂时状态。 |
| 504（网关超时）      | 服务器作为网关或代理，但是没有及时从上游服务器收到请求。 |
| 505（HTTP 版本不受支持）      | 服务器不支持请求中所用的 HTTP 协议版本。 |
| 400（错误请求）      | 服务器不理解请求的语法。 |
| 400（错误请求）      | 服务器不理解请求的语法。 |


如下内容重复

1、HTTP协议状态码表示的意思主要分为五类 ,大体是 :  

~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

1×× 　　保留   

2×× 　　表示请求成功地接收 
  
3×× 　　为完成请求客户需进一步细化请求 
  
4×× 　　客户错误   

5×× 　　服务器错误   

100 Continue

指示客户端应该继续请求。回送用于通知客户端此次请求已经收到，并且没有被服务器拒绝。

客户端应该继续发送剩下的请求数据或者请求已经完成，或者忽略回送数据。服务器必须发送

最后的回送在请求之后。

101 Switching Protocols

服务器依照客服端请求，通过Upgrade头信息，改变当前连接的应用协议。服务器将根据Upgrade头立刻改变协议

在101回送以空行结束的时候。

 
2、Successful

=======================================

200 OK

指示客服端的请求已经成功收到，解析，接受。

201 Created

请求已经完成并一个新的返回资源被创建。被创建的资源可能是一个URI资源，通常URI资源在Location头指定。回送应该包含一个实体数据
并且包含资源特性以及location通过用户或者用户代理来选择合适的方法。实体数据格式通过煤体类型来指定即content-type头。最开始服务 器
必须创建指定的资源在返回201状态码之前。如果行为没有被立刻执行，服务器应该返回202。

202 Accepted

请求已经被接受用来处理。但是处理并没有完成。请求可能或者根本没有遵照执行，因为处理实际执行过程中可能被拒绝。

203 Non-Authoritative Information

204 No Content

服务器已经接受请求并且没必要返回实体数据，可能需要返回更新信息。回送可能包含新的或更新信息由entity-headers呈现。

205 Reset Content

服务器已经接受请求并且用户代理应该重新设置文档视图。

206 Partial Content

服务器已经接受请求GET请求资源的部分。请求必须包含一个Range头信息以指示获取范围可能必须包含If-Range头信息以成立请求条件。

 
3、Redirection

=======================================

300 Multiple Choices

请求资源符合任何一个呈现方式。

301 Moved Permanently

请求的资源已经被赋予一个新的URI。

302 Found

通过不同的URI请求资源的临时文件。

303 See Other

304 Not Modified

如果客服端已经完成一个有条件的请求并且请求是允许的，但是这个文档并没有改变，服务器应该返回304状态码。304
状态码一定不能包含信息主体，从而通常通过一个头字段后的第一个空行结束。

305 Use Proxy

请求的资源必须通过代理（由Location字段指定）来访问。Location资源给出了代理的URI。

306 Unused

307 Temporary Redirect

 
4、Client Error

======================================

400 Bad Request

因为错误的语法导致服务器无法理解请求信息。

401 Unauthorized

如果请求需要用户验证。回送应该包含一个WWW-Authenticate头字段用来指明请求资源的权限。

402 Payment Required

保留状态码

403 Forbidden

服务器接受请求，但是被拒绝处理。

404 Not Found

服务器没有找到任何匹配Request-URI的资源。

405 Menthod Not Allowed

Request-Line 请求的方法不被允许通过指定的URI。

406 Not Acceptable

407 Proxy Authentication Required

408 Reqeust Timeout

客服端没有提交任何请求在服务器等待处理时间内。

409 Conflict

410 Gone

411 Length Required

服务器拒绝接受请求在没有定义Content-Length字段的情况下。

412 Precondition Failed

413 Request Entity Too Large

服务器拒绝处理请求因为请求数据超过服务器能够处理的范围。服务器可能关闭当前连接来阻止客服端继续请求。

414 Request-URI Too Long

服务器拒绝服务当前请求因为URI的长度超过了服务器的解析范围。

415 Unsupported Media Type

服务器拒绝服务当前请求因为请求数据格式并不被请求的资源支持。

416 Request Range Not Satisfialbe

417 Expectation Failed

 
5、Server Error

======================================

500 Internal Server Error

服务器遭遇异常阻止了当前请求的执行

501 Not Implemented

服务器没有相应的执行动作来完成当前请求。

502 Bad Gateway

503 Service Unavailable

因为临时文件超载导致服务器不能处理当前请求。

504 Gateway Timeout

505 Http Version Not Supported