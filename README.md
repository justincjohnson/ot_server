# [OT.Server](https://hexdocs.pm/ot_server) [![Build Status](https://travis-ci.org/jclem/ot_server.svg?branch=master)](https://travis-ci.org/jclem/ot_server)

`OT.Server` is an application that manages the correct handling of submitted
operations in an operational transformation system. It ships with an adapter
for persisting data to ETS, but implementing new adapters is simple.

For more detailed information about operational transformation, see the
documentation for [ot_ex](https://github.com/jclem/ot_ex) and the various links
therein.

## Installation

The package can be installed by adding `ot_server` to your list of dependencies
in `mix.exs`:

```elixir
def deps do
  [
    {:ot_server, "~> 0.1.0"}
  ]
end
```

## Usage

Implement an adapter as per `OT.Server.Adapter` and configure it as the adapter
for the `:ot_server` application:

```elixir
config :ot_server,
  adapter: MyOTAdapter,
  max_retries: 25,
  ot_types: %{"text" => OT.Text}
```

For an example of how an adapter can be created, see `OT.Server.ETSAdapter`.

### Configuration Options

- `adapter`: The `OT.Server.Adapter` that `OT.Server` will use to interact with
  your data.
- `max_retries`: The number of times a submission will be attempted before it
  fails permanently.
- `ot_types`: A map with string keys pointing to modules that implement
  `OT.Type`.
