# NestedFilter

NestedFilter drills down into a nested map and filters out keys according to
user specified values.

## Installation

If [available in Hex](https://hex.pm/docs/publish), the package can be installed
by adding `nested_filter` to your list of dependencies in `mix.exs`:

```elixir
def deps do
  [{:nested_filter, "~> 0.1.1"}]
end
```

Documentation can be generated with [ExDoc](https://github.com/elixir-lang/ex_doc)
and published on [HexDocs](https://hexdocs.pm). Once published, the docs can
be found at [https://hexdocs.pm/nested_filter](https://hexdocs.pm/nested_filter).


## Usage

By default, when removing user specified values, empty values will be preserved
(see Case 1 below). You can use the *remove_empty* option which takes a list of
user specified "empty values" (e.g., empty maps) that will be removed.

```elixir
# Case 1: Remove the nil values from a nested map, preserving empty map values

nested_map = %{a: 1, b: %{m: nil, n: 2}, c: %{p: %{q: nil, r: nil}, s: %{t: 2, u: 3}} }
NestedFilter.reject_keys_by_value(nested_map, [nil])

# => %{a: 1, b: %{n: 2}, c: %{p: %{}, s: %{t: 2, u: 3}} }

# Case 2: Remove the nil values from a nested map, removing empty map values
nested_map = %{a: 1, b: %{m: nil, n: 2}, c: %{p: %{q: nil, r: nil}, s: %{t: 2, u: 3}} }
NestedFilter.reject_keys_by_value(nested_map, [nil], %{remove_empty: [%{}]})
# => %{a: 1, b: %{n: 2}, c: %{s: %{t: 2, u: 3}} }
```

You can browse the tests for more examples.
