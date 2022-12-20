<p><b>In order to create a basic controller, we use classes and decorators. Decorators associate classes with required metadata and enable Nest to create a routing map (tie requests to the corresponding controllers).</b></p>

```
import { Controller, Get } from '@nestjs/common';

@Controller('cats')  // <--------- This decorator is required to define a basic controller. 
export class CatsController { // <------ This class is required to define the controller
  @Get()                      // <------ This decorator is required to define request VERB
  findAll(): string {         // <------ This function handles the  request !
    return 'This action returns all cats';
  }
}

```

<b> We specify an optional route path prefix of cats. Using a path prefix in a @Controller() decorator allows us to easily group a set of related routes, and minimize repetitive code. For example, we may choose to group a set of routes that manage interactions with a customer entity under the route /customers. In that case, we could specify the path prefix customers in the @Controller() decorator so that we don't have to repeat that portion of the path for each route in the file. </b>

<b>The two options for manipulating responses</b>
<table>
  <tr>
    <td>Standard (recommended)</td>
    <td>1. Objects or Arrays are automagically converted to JSON. 2. Literals are returned directly. </td>
  </tr>
  <tr>
    <td>Library-specific (Express, Fastify etc.)</td>
    <td>@Res() decorator in the method handler signature (e.g., findAll(@Res() response))</td>
  </tr>
</table>

<b>The request object represents the HTTP request and has properties for the request query string, parameters, HTTP headers, and body (read more here).</b>

<table><tbody><tr><td><code>@Request(), @Req()</code></td><td><code>req</code></td></tr><tr><td><code>@Response(), @Res()</code><span class="table-code-asterisk">*</span></td><td><code>res</code></td></tr><tr><td><code>@Next()</code></td><td><code>next</code></td></tr><tr><td><code>@Session()</code></td><td><code>req.session</code></td></tr><tr><td><code>@Param(key?: string)</code></td><td><code>req.params</code> / <code>req.params[key]</code></td></tr><tr><td><code>@Body(key?: string)</code></td><td><code>req.body</code> / <code>req.body[key]</code></td></tr><tr><td><code>@Query(key?: string)</code></td><td><code>req.query</code> / <code>req.query[key]</code></td></tr><tr><td><code>@Headers(name?: string)</code></td><td><code>req.headers</code> / <code>req.headers[name]</code></td></tr><tr><td><code>@Ip()</code></td><td><code>req.ip</code></td></tr><tr><td><code>@HostParam()</code></td><td><code>req.hosts</code></td></tr></tbody></table>

<b>Nest provides decorators for all of the standard HTTP methods: @Get(), @Post(), @Put(), @Delete(), @Patch(), @Options(), and @Head(). In addition, @All() defines an endpoint that handles all of them.</b>

<b>Example:</b>

```
import { Controller, Get, Post } from '@nestjs/common';

@Controller('cats')
export class CatsController {
  @Post()
  create(): string {
    return 'This action adds a new cat';
  }

  @Get()
  findAll(): string {
    return 'This action returns all cats';
  }
}

```

<b>Pattern based routes are supported as well. For instance, the asterisk is used as a wildcard, and will match any combination of characters.</b>

```
@Get('ab*cd')
findAll() {
  return 'This route uses a wildcard';
}
```
