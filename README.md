Lua bindings for the Telegram bot API, used by
[otouto](https://github.com/topkecleon/otouto).

Usage:

```
$ git clone https://github.com/topkecleon/bindings
$ lua
> bindings = require('bindings')
> bindings.set_token('12345678:ABCDEFGHIJKLM')
> bindings.sendMessage{chat_id = -87654321, text = "Sent from Lua"}
```

Every function call is routed into the `bindings.request` function.
`bindings.getChat{chat_id = -8675309}` becomes
`bindings.request("getChat", {chat_id = -8675309})`. This way, all methods and
parameters are supported.

Sending a file by file_id or URL is simple:

```lua
bindings.sendPhoto{
    chat_id = -8675309,
    photo = file_id or file_url,
    caption = "etc"
}
```

Uploading a local file requires putting that parameter in its own table:

```lua
bindings.sendPhoto({chat_id = -8675309}, {photo = "path/to/file"})
```

This is quirky, but it is a simple and seemingly future-proof way to tell the
request function to send a local file rather than to pass the string. The
submodule never needs to interpret a parameter, and the way it would interpret
them will never need to be updated.

`bindings.FILE_URL` is available for building bot API file URLs conveniently.

Rights to this code are granted under the terms of the MIT license:

>Permission is hereby granted, free of charge, to any person obtaining a copy
>of this software and associated documentation files (the "Software"), to deal
>in the Software without restriction, including without limitation the rights
>to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
>copies of the Software, and to permit persons to whom the Software is
>furnished to do so, subject to the following conditions:
>
>The above copyright notice and this permission notice shall be included in all
>copies or substantial portions of the Software.
>
>THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
>IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
>FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
>AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
>LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
>OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
>SOFTWARE.
