# 2.3.1

* Fixed a compatibility but with Erlang 27 (@bunnylushington)

# 2.3.0

* Add support `sbw:host/1` function (#80, thanks @dmsnell)
* Ensure a cookie's `SameSite` attribute is properly cast to a binary (fixing a
  crash if it's specified as, say, an atom)
* Add CSS to inets fallback mimetype support

# 2.2.0

* Add proper support for the cookie `SameSite` attribute.
* Remove use of deprecated `httpd_util:flatlength`
* Remove official support for P-mod/Tuple-Module calls (no code change,
  required, just removed from documentation).
* Add a bunch of build rules and rebar3 profiles to build and test all backends
  with rebar3.
* Add `sbw:host/1` that will try to intelligently return the hostname from the
  request, either from the full URI, the host header, or the X-forwarded-for
  header. (Thanks @dmsnell)

# 2.1.1

* Add basic rebar3 Compatibility

# 2.1.0

* Backwards incompatible change: Converted the pre-cached headers to a map.
* Converted to cowboy 2.x (Thanks Eric, @etxemag75)
* Deprecated `sbw:set_cookie/5` in favor of a new, more flexible,
  `sbw:set_cookie/4`, which takes an `Options` argument for specifying
  `http_only`, `max_age`, `secure`, etc. (Dmitry Polyanovsky)
* Remove deprecated `erlang:now()`.
* Expose the cowboy dispatch table generation so that a user can use it to
  build their own dispatch table based on it,
  (`cowboy_simple_bridge_sup:get_dispatch_info/2`).  (Olivier-Boudeville)
* Fix tail-call bug in `simple_bridge_websocket`
* Fix a bug looking for a custom inets.config
* Add dialyzer and travis rules to Makefile
* Fix a handful of issues found by dialyzer
* Fix a number of yaws-related issues (max post size, keepalive, static file
  fallback)
* Set the cowboy supervisor to not `infinity`.
* Add a few more tests.
* Ensure support up to Erlang 23.
* Fix a multipart parsing error related to mismatched content-length vs actual
  content length.

# 2.0.1

* Allow binary headers for the inets bridge
* Set up supervision properly for cowboy

# 2.0.0

* Simple Bridge is no longer dependent on the deprecated parameter module
  contruct, however, all relevant modules have retained the necessary structure
  to treat them as parameter modules, if you so choose. The standard interface
  is now through a module called `sbw`.
* All backends now provide a default supervisor for simplified starting and
  building backend-specific configurations.
* All backends now provide an "anchor" module, which serves as an intermediary
  between the server and the "handler" module.
* Merged Request and Response bridge into a single `Bridge` "object" using the
  module `sbw` (simple bridge wrapper).
* Added `simple_bridge:make(Backend)` function to replace having to make both
  request and response bridges.
* Added a handler behaviour (`-behaviour(simple_bridge_handler)`) for each
  platform, customizable with `simple_bridge:start(Backend, HandlerMod)`. This
  relies on the use of an "Anchor" module, a default provided for each module.
* Added a sample handler module which can be used as a basis for future
  functionality. (`simple_bridge_handler_sample.erl`)
* Added Websocket Support for Yaws, Cowboy using their native implementations.
* Added a Websocket Hijacker to support websockets on non-websocket backends,
  particularly Mochiweb, Inets, and Webmachine.
* Header values will be returned as binaries if the Header name provided is a
  binary. If header is provided as an atom or a list, it will return a list.
* Provided a quickstart demo to try out all backends with request, response,
  and websockets. `make run_BACKEND`, where BACKEND is `cowboy`, `inets`,
  `mochiweb`, `webmachine`, or `yaws`.
* Rewrote the test suite to use the same testing codebase for all backends.
* Removed support for Misultin.

# 1.4.1

* Added protocol() for cowboy.
* Use `erlang/pmod_transform` instead of `choptastic/pmod_transform` for
  backwards compatible pmod transforms
* Added `x-forwarded-proto` header
* Fixed `peer_name` and `peer_port` for yaws
* Fix Cowboy's bridge so `request_body` just returns a binary

# 1.4

* Add ability to store temp files in memory if they are small enough,
  otherwise.

# 1.3 and earlier

* Supports Cowboy, Inets, Mochiweb, Webmachine, Yaws, and Misultin

