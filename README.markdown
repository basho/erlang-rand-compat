# Erlang random number compatibility library

This project allows you to generate a compatibility module, exposing the common
subset API of `rand` and `random`. It is meant to be used as a migration helper
in projects that want to run on Erlang/OTP installations that may or may not
have the new `rand` module. It does this by using `rand` if available or
falling back to `random` if not.

This is useful if you want (1) your beam files to work across OTP releases, and
(2) avoid a runtime check in the compat functions. If, however, you're free to
use conditional compilation, you can still avoid runtime checks while skipping
runtime generation of the compat module. Therefore, if, say, your project isn't
distributed as an escript archive, you should go the conditional compilation
route. Avoiding runtime generated modules also has the benefit of not hiding
code from Dialyzer.

## Using

First we need to generate and load the module:

    {ok, rnd} = rand_compat:init().

Alternatively, you can specify the name of the generated module like this:

    {ok, some_module} = rand_compat:init(some_module).

Now, you can use the provided common subset API (shared between `rand` and
`random`) by calling functions like `rnd:seed()` or `some_module:seed()`.

The full list of functions in the generated module is as follows:

    -export([ seed/0
            , seed/1
            , uniform/0
            , uniform/1
            , uniform_s/1
            , uniform_s/2
            ]).

## Building

    $ rebar3 compile

or

    $ erlc +debug_info -o ebin src/*.erl

## Documentation

    $ rebar3 edoc

## Test

    $ rebar3 eunit

## Dialyze

    $ rebar3 dialyzer
