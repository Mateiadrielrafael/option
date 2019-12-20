# Documentation

## Table of contents:

### General:

-   [Option](#Option)
-   [Some](#Some)
-   [None](#None)

### Helpers:

-   [bind](#Bind)
-   [count](#Count)
-   [exists](#Exists)
-   [filter](#Filter)
-   [fold](#Fold)
-   [foldback](#Foldback)
-   [forall](#Forall)

# General

## Option

Data type holding an optional value (can be either None or Some(x))

### Signature

```ts
type Option<T> = Internals.SomeClass<T> | Internals.NoneClass
```

## None

Value holding nothing

### Signature

```ts
const None: Internals.NoneClass
```

## Some

Creates an Option instance holding a value

### Signature

```ts
const Some: <T>(v: T) => Internals.SomeClass<T>
```

### Usage

```ts
import { Some } from '@adrielus/option'

Some(x) // Some(x)
```

# Helpers

## Bind

Invokes a function on an optional value that itself yields an option.

### Signature

```ts
const bind: <T, U>(binder: Mapper<T, Option<U>>, option: Option<T>) => Option<U>
```

### Usage

```ts
import { Some, None, bind } from '@adrielus/option'

const half = (x: number) => (x % 2 ? None : Some(x / 2))

bind(half, Some(14)) // Some(7)
bind(half, Some(13)) // None
bind(half, None) // None
```

## Count

Returns a zero if the option is None, a one otherwise.

### Signature:

```ts
const count: <T>(option: Option<T>) => number
```

### Usage

```ts
import { Some, None, count } from '@adrielus/option'

count(Some(x)) // 1
count(None) // 0
```

## Exists

Returns false if the option is None, otherwise it returns the result of applying the predicate to the option value.

### Signature

```ts
const exists: <T>(predicate: Mapper<T, boolean>, option: Option<T>) => boolean
```

### Usage

```ts
import { Some, None, exists } from '@adrielus/option'

exists(() => true, None) // false
exists(() => true, Some(x)) // true
exists(() => false, Some(x)) // false
```

## Filter

Invokes a function on an optional value that itself yields an option.

### Signature:

```ts
const filter: <T>(predicate: Mapper<T, boolean>, option: Option<T>) => NoneClass
```

### Usage

```ts
import { Some, None, filter } from '@adrielus/option'

filter(() => true, None) // None
filter(() => true, Some(x)) // Some(x)
filter(() => false, Some(x)) // None
```

## Fold

A function to update the state data when given a value from an option.

### Signature

```ts
const fold: <T, U>(folder: Folder<T, U>, initial: U, option: Option<T>) => U
```

### Usage

```ts
import { Some, None, fold } from '@adrielus/option'

const add = (a: number, b: number) => a + b

fold(add, x, None) // x
fold(add, x, Some(y)) // x + y
```

## Foldback

A function to update the state data when given a value from an option.

### Signature

```ts
const foldback: <T, U>(
    folder: BackFolder<T, U>,
    option: Option<T>,
    initial: U
) => U
```

### Usage

```ts
import { Some, None, foldback } from '@adrielus/option'

const add = (a: number, b: number) => a + b

foldback(add, None, x) // x
foldback(add, Some(y), x) // x + y
```

**_This is still work in progress, right now only covering about 60% of the library. Contributions are welcome_**