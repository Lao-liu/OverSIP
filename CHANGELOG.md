CHANGELOG
=========


Version 1.3.1 (released in 2012-10-04)
--------------------------------------

- [(042fdaf)](https://github.com/versatica/OverSIP/commit/042fdaf17bfeddf22ffa80637b0e0fb387a77bff) Fixed an important bug in record-routing mechanism that makes OverSIP not to add Record-Route/Path headers.


Version 1.3.0 (released in 2012-10-04)
--------------------------------------

- [(6afa5a6)](https://github.com/versatica/OverSIP/commit/6afa5a6c2572aea4b78a3aba2fc5d2f0d81d96ce) All the callbacks in `server.rb` are now executed within a new [Fiber](http://www.ruby-doc.org/core-1.9.3/Fiber.html) allowing synchronous style coding by using [em-synchrony](https://github.com/igrigorik/em-synchrony) libraries.

- [(b950bba)](https://github.com/versatica/OverSIP/commit/b950bba6aa8d7e3e28d69f7fb3d850a4719e02ba) New class `OverSIP::SIP::Uac`that allows OverSIP behaving as a UAC for generating and sending SIP requests. New class `OverSIP::SIP::UacRequest` for generating requests to be sent via `OverSIP::SIP::Uac#route` method (also allows sending a received `OverSIP::SIP::Request` instance).

- New methods `initialize()`, `sip?`, `tel?` and `get_param()` for `OverSIP::SIP::Uri` class ([doc](http://www.oversip.net/documentation/1.3.x/api/sip/uri/)).

- New class `OverSIP::SIP::Client`, parent class of `OverSIP::SIP::Proxy` and `OverSIP::SIP::Uac`. New method `add_target_to_blacklist()` ([doc](http://www.oversip.net/documentation/1.3.x/api/sip/client/)).

- `OverSIP::SIP::Client#on_error()` method is now called with a third argument: a Ruby symbol trat represents the exact (internal) error code.

- `OverSIP::SIP::Client#on_target()` callback is now called with a single parameter: the instance of `OverSIP::SIP::RFC3263::Target` (API change).

- [(7e9733e)](https://github.com/versatica/OverSIP/commit/7e9733e95f04158bb69ed13130984e335c80c73c) New feature: automatic blacklists. When a destination (target) fails due to timeout, connection error or TLS validation error, the target is added to a temporal blacklist and future requests to same target are not attempted until the entry in the blacklist expires.


Version 1.2.0 (released in 2012-09-04)
--------------------------------------

- [(c921687)](https://github.com/versatica/OverSIP/commit/c9216872ccd43c3977b8816551f33d9d0c178899) Added `on_target()` and `abort_routing()` methods for `Proxy` class.

- [(7e54d1c)](https://github.com/versatica/OverSIP/commit/7e54d1c89351e0517bc12d543e577dff46f251a4) Don't raise an exception if the received STUN request contains an invalid IP family (vulnerability!).

- [(f7eefd6)](https://github.com/versatica/OverSIP/commit/f7eefd6d8e02d30e61fd219f4426e6e63ea7f2a8) If request.from or request.to (`NameAddr` instances) are modified before routing the request, changes are applied for the outgoing request and reverted when sending responses upstream.

- [(0f9d3ec)](https://github.com/versatica/OverSIP/commit/0f9d3ec9da96c51197535bcd5f0c65e5749ec855) If request.contact `NameAddr` fields are modified then changes are applied in the forwarded request.

- [(df1389e)](https://github.com/versatica/OverSIP/commit/df1389eda22806dc48f6595cc3e6460c58391411) Added `SystemCallbacks` module for 3rd party modules to set custom callbacks when OverSIP is started, reloaded (HUP signal) or stopped.

- [(9d310d6)](https://github.com/versatica/OverSIP/commit/9d310d6678ee79c47d17b5aab010a49b8683c3da) Added `OverSIP::SIP::Uri#aor()`method which returns "sip:user@domain" for a SIP/SIPS URI (no port or params) and "tel:number" for a TEL URI (no params).

- [(56e099b)](https://github.com/versatica/OverSIP/commit/56e099bb0500e6cda221750ade7848fda614b522) Added a new method `OverSIP::SystemEvents.on_initialize()` useful for 3rd party modules configuration by the user.

- [(aac4bad)](https://github.com/versatica/OverSIP/commit/aac4badafd924cdbd3344a6636fa9588d0b84c79) `OverSIP::SIP::Modules::RegistrarWithoutPath` renamed to `OverSIP::SIP::Modules::OutboundMangling`.

- [(ce48977)](https://github.com/versatica/OverSIP/commit/ce48977ca786def6d9c9f8af8d743da7c105dcf6) `OverSIP::SIP::Modules::Core` moved to `OverSIP::SIP::Core`.

- [(98e5308)](https://github.com/versatica/OverSIP/commit/98e530869e57150778327b29e5a977b2f6985f8d)` OverSIP::SIP::Modules` moved to `OverSIP::Modules`.


Version 1.1.2 (released in 2012-08-28)
--------------------------------------

- [(d91d2e4)](https://github.com/versatica/OverSIP/commit/d91d2e4899a777dd7dd101e83fe36a1bca744398) Require EventMachine-LE >= 1.1.3 which includes the `:use_tls` option for selecting TLSv1 or SSLv23 (fixes [#12](https://github.com/versatica/OverSIP/issues/12)).
