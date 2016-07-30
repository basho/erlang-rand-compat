# Erlang random number compatibility library

This project allows you to generate a compatibility module, exposing the common
subset API of `rand` and `random`. It is meant to be used as a migration helper
in projects that want to run on Erlang/OTP installations that may or may not
have the new `rand` module.  It does this by using `rand` if available or
falling back to `random` if not.

## Build

    $ rebar compile

or

    $ erlc +debug_info -o ebin src/*.erl

## Documentation

    $ rebar doc

## Test

    $ rebar eunit

## Dialyze

Build the PLT

    $ rebar build-plt

Run Dialyzer

    $ rebar dialyze

By using abbreviated commands, you can also (0) `build-plt`, (1) `compile`, (2)
`eunit` (test), and (3) `dialyze` the code like this:

    $ rebar b-p
    $ rebar co eu di

This is shorter to type. See `rebar help` for a description of
abbreviated command support.


## Using

First we need to generate and load the module.

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
