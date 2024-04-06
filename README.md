# Keccak-f[1600] NIF (SHA3-224, SHA3-256, SHA3-384, SHA3-512, SHAKE128, SHAKE256)

*This is the original keccak-f1600 as used in Ethereum.*

[Keccak-f[1600]](http://keccak.noekeon.org/) NIF with timeslice reductions for Erlang and Elixir.

The timeslice reductions allow the NIF to perform operations on very large inputs without blocking the scheduler or requiring the Erlang VM to support dirty schedulers.  See the [bitwise](https://github.com/vinoski/bitwise) project from which the strategy was derived.


## Installation

Add `keccakf1600` to your project's dependencies in `mix.exs`

```elixir
defp deps do
  [
    :keccakf1600, github: "diodechain/erlang-keccakf1600"},
  ]
end
```

Or add the following to your `rebar.config`

```erlang
{deps, [
  {keccakf1600, ".*", {git, "git://github.com/diodechain/erlang-keccakf1600.git", {branch, "master"}}}
]}.
```

## Usage

This library follows usage semantics from Erlang's own [`crypto`](http://erlang.org/doc/man/crypto.html) library, with the exception of the SHAKE128 and SHAKE256 algorithms as described in `keccakf1600:hash/3` and `keccakf1600:final/2` below.

### `keccakf1600:hash/2`

This function can be used for the following algorithms:

 * SHA3-224 (`sha3_224`)
 * SHA3-256 (`sha3_256`)
 * SHA3-384 (`sha3_384`)
 * SHA3-512 (`sha3_512`)

```erlang
keccakf1600:hash(sha3_224, <<"test">>).
% <<55,151,191,10,251,191,202,74,123,187,167,96,42,43,85,39,70,135,101,23,167,249,183,206,45,176,174,123>>

keccakf1600:hash(sha3_256, <<"test">>).
% <<54,240,40,88,11,176,44,200,39,42,154,2,15,66,0,227,70,226,118,174,102,78,69,238,128,116,85,116,226,245,171,128>>

keccakf1600:hash(sha3_384, <<"test">>).
% <<229,22,218,187,35,182,227,0,38,134,53,67,40,39,128,163,174,13,204,240,85,81,207,2,149,23,141,127,240,241,180,30,236,185,219,63,242,25,0,124,78,9,114,96,213,134,33,189>>

keccakf1600:hash(sha3_512, <<"test">>).
% <<158,206,8,110,155,172,73,31,172,92,29,16,70,202,17,215,55,185,42,43,46,189,147,240,5,215,183,16,17,12,10,103,130,136,22,110,127,190,121,104,131,164,242,233,179,202,159,72,79,82,29,12,228,100,52,92,193,174,201,103,121,20,156,20>>
```

### `keccakf1600:hash/3`

This function can be used for the following algorithms:

 * SHAKE128 (`shake128`)
 * SHAKE256 (`shake256`)

These algorithms can output arbitrary length digests, so an output length must be specified.

```erlang
keccakf1600:hash(shake128, <<"test">>, 16).
% <<211,176,170,156,216,183,37,86,34,206,188,99,30,134,125,64>>

keccakf1600:hash(shake256, <<"test">>, 16).
% <<181,79,247,37,87,5,167,30,226,146,94,74,62,48,228,26>>
```

### `keccakf1600:init/1`

This function can be used for the following algorithms:

 * SHA3-224 (`sha3_224`)
 * SHA3-256 (`sha3_256`)
 * SHA3-384 (`sha3_384`)
 * SHA3-512 (`sha3_512`)
 * SHAKE128 (`shake128`)
 * SHAKE256 (`shake256`)

#### SHA3-224 (`sha3_224`)

```erlang
Sponge0 = keccakf1600:init(sha3_224).
% {sha3_224, <<0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,65,144,0,6,128,28,0>>}
```

#### SHA3-256 (`sha3_256`)

```erlang
Sponge0 = keccakf1600:init(sha3_256).
% {sha3_256, <<0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,65,136,0,6,128,32,0>>}
```

#### SHA3-384 (`sha3_384`)

```erlang
Sponge0 = keccakf1600:init(sha3_384).
% {sha3_384, <<0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,65,104,0,6,128,48,0>>}
```

#### SHA3-512 (`sha3_512`)

```erlang
Sponge0 = keccakf1600:init(sha3_512).
% {sha3_512, <<0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,65,72,0,6,128,64,0>>}
```

#### SHAKE128 (`shake128`)

```erlang
Sponge0 = keccakf1600:init(shake128).
% {shake128, <<0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,65,168,0,31,128,255,0>>}
```

#### SHAKE256 (`shake256`)

```erlang
Sponge0 = keccakf1600:init(shake256).
% {shake256, <<0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,65,136,0,31,128,255,0>>}
```

### `keccakf1600:update/2`

This function can be used for the following algorithms:

 * SHA3-224 (`sha3_224`)
 * SHA3-256 (`sha3_256`)
 * SHA3-384 (`sha3_384`)
 * SHA3-512 (`sha3_512`)
 * SHAKE128 (`shake128`)
 * SHAKE256 (`shake256`)

The examples below use the `Sponge0` for each algorithm from the examples above for `keccakf1600:init/1`.

#### SHA3-224 (`sha3_224`)

```erlang
Sponge1 = keccakf1600:update(Sponge0, <<"test">>).
% {sha3_224, <<116,101,115,116,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,4,65,144,0,6,128,28,0>>}
```

#### SHA3-256 (`sha3_256`)

```erlang
Sponge1 = keccakf1600:update(Sponge0, <<"test">>).
% {sha3_256, <<116,101,115,116,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,4,65,136,0,6,128,32,0>>}
```

#### SHA3-384 (`sha3_384`)

```erlang
Sponge1 = keccakf1600:update(Sponge0, <<"test">>).
% {sha3_384, <<116,101,115,116,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,4,65,104,0,6,128,48,0>>}
```

#### SHA3-512 (`sha3_512`)

```erlang
Sponge1 = keccakf1600:update(Sponge0, <<"test">>).
% {sha3_512, <<116,101,115,116,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,4,65,72,0,6,128,64,0>>}
```

#### SHAKE128 (`shake128`)

```erlang
Sponge1 = keccakf1600:update(Sponge0, <<"test">>).
% {shake128, <<116,101,115,116,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,4,65,168,0,31,128,255,0>>}
```

#### SHAKE256 (`shake256`)

```erlang
Sponge1 = keccakf1600:update(Sponge0, <<"test">>).
% {shake256, <<116,101,115,116,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,4,65,136,0,31,128,255,0>>}
```

### `keccakf1600:final/2`

This function can be used for the following algorithms:

 * SHA3-224 (`sha3_224`)
 * SHA3-256 (`sha3_256`)
 * SHA3-384 (`sha3_384`)
 * SHA3-512 (`sha3_512`)

The examples below use the `Sponge1` for each algorithm from the examples above for `keccakf1600:update/2`.

#### SHA3-224 (`sha3_224`)

```erlang
Out = keccakf1600:final(Sponge1).
% <<55,151,191,10,251,191,202,74,123,187,167,96,42,43,85,39,70,135,101,23,167,249,183,206,45,176,174,123>>
```

#### SHA3-256 (`sha3_256`)

```erlang
Out = keccakf1600:update(Sponge1).
% <<54,240,40,88,11,176,44,200,39,42,154,2,15,66,0,227,70,226,118,174,102,78,69,238,128,116,85,116,226,245,171,128>>
```

#### SHA3-384 (`sha3_384`)

```erlang
Out = keccakf1600:update(Sponge1).
% <<229,22,218,187,35,182,227,0,38,134,53,67,40,39,128,163,174,13,204,240,85,81,207,2,149,23,141,127,240,241,180,30,236,185,219,63,242,25,0,124,78,9,114,96,213,134,33,189>>
```

#### SHA3-512 (`sha3_512`)

```erlang
Out = keccakf1600:update(Sponge1).
% <<158,206,8,110,155,172,73,31,172,92,29,16,70,202,17,215,55,185,42,43,46,189,147,240,5,215,183,16,17,12,10,103,130,136,22,110,127,190,121,104,131,164,242,233,179,202,159,72,79,82,29,12,228,100,52,92,193,174,201,103,121,20,156,20>>
```

### `keccakf1600:final/3`

This function can be used for the following algorithms:

 * SHA3-224 (`sha3_224`)
 * SHA3-256 (`sha3_256`)
 * SHA3-384 (`sha3_384`)
 * SHA3-512 (`sha3_512`)

These algorithms can output arbitrary length digests, so an output length must be specified.

The examples below use the `Sponge1` for each algorithm from the examples above for `keccakf1600:update/2`.

#### SHAKE128 (`shake128`)

```erlang
Out = keccakf1600:final(Sponge1, 16).
% <<211,176,170,156,216,183,37,86,34,206,188,99,30,134,125,64>>
```

#### SHAKE256 (`shake256`)

```erlang
Out = keccakf1600:final(Sponge1, 16).
% <<181,79,247,37,87,5,167,30,226,146,94,74,62,48,228,26>>
```
