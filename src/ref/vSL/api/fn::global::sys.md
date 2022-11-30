# global::sys



<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn !(x: bool) -> bool
```

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn !=(x: u8, y: u8) -> bool
```

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn !=(x: u64, y: u64) -> bool
```

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn !=(timestamp1: Instant, timestamp2: Instant) -> bool
```

<details>
<summary markdown="span"> details </summary>

Return `true` if two timestamps are not equal.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn !=(x: i32, y: i32) -> bool
```

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn !=(x: int, y: float) -> bool
```

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn !=(map1: Map, map2: Map) -> Result<bool, Box<EvalAltResult>>
```

<details>
<summary markdown="span"> details </summary>

Return `true` if two object maps are not equal (i.e. at least one property value is not equal).

The operator `==` is used to compare property values and must be defined,
otherwise `false` is assumed.

# Example

```rhai
let m1 = #{a:1, b:2, c:3};
let m2 = #{a:1, b:2, c:3};
let m3 = #{a:1, c:3};

print(m1 != m2);        // prints false

print(m1 != m3);        // prints true
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn !=(x: u16, y: u16) -> bool
```

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn !=(x: u128, y: u128) -> bool
```

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn !=(x: i128, y: i128) -> bool
```

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn !=(x: u32, y: u32) -> bool
```

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn !=(x: f32, y: f32) -> bool
```

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn !=(in1: Status, in2: Status) -> bool
```

<details>
<summary markdown="span"> details </summary>

Operator `!=` for `Status`
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn !=(x: i8, y: i8) -> bool
```

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn !=(x: i16, y: i16) -> bool
```

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn !=(array1: Array, array2: Array) -> Result<bool, Box<EvalAltResult>>
```

<details>
<summary markdown="span"> details </summary>

Return `true` if two arrays are not-equal (i.e. any element not equal or not in the same order).

The operator `==` is used to compare elements and must be defined,
otherwise `false` is assumed.

# Example

```rhai
let x = [1, 2, 3, 4, 5];
let y = [1, 2, 3, 4, 5];
let z = [1, 2, 3, 4];

print(x != y);      // prints false

print(x != z);      // prints true
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn !=(x: f32, y: int) -> bool
```

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn !=(x: float, y: int) -> bool
```

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn !=(x: int, y: f32) -> bool
```

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn %(x: f32, y: f32) -> f32
```

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn %(x: u128, y: u128) -> Result<u128, Box<EvalAltResult>>
```

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn %(x: u16, y: u16) -> Result<u16, Box<EvalAltResult>>
```

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn %(x: u8, y: u8) -> Result<u8, Box<EvalAltResult>>
```

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn %(x: i8, y: i8) -> Result<i8, Box<EvalAltResult>>
```

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn %(x: u64, y: u64) -> Result<u64, Box<EvalAltResult>>
```

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn %(x: u32, y: u32) -> Result<u32, Box<EvalAltResult>>
```

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn %(x: i128, y: i128) -> Result<i128, Box<EvalAltResult>>
```

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn %(x: i32, y: i32) -> Result<i32, Box<EvalAltResult>>
```

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn %(x: i16, y: i16) -> Result<i16, Box<EvalAltResult>>
```

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn %(x: int, y: f32) -> f32
```

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn %(x: f32, y: int) -> f32
```

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn &(x: i128, y: i128) -> i128
```

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn &(x: u16, y: u16) -> u16
```

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn &(x: i16, y: i16) -> i16
```

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn &(x: u64, y: u64) -> u64
```

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn &(x: i32, y: i32) -> i32
```

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn &(x: u32, y: u32) -> u32
```

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn &(x: u8, y: u8) -> u8
```

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn &(x: i8, y: i8) -> i8
```

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn &(x: u128, y: u128) -> u128
```

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn *(x: i32, y: i32) -> Result<i32, Box<EvalAltResult>>
```

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn *(x: i8, y: i8) -> Result<i8, Box<EvalAltResult>>
```

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn *(x: int, y: f32) -> f32
```

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn *(x: f32, y: f32) -> f32
```

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn *(x: u8, y: u8) -> Result<u8, Box<EvalAltResult>>
```

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn *(x: u64, y: u64) -> Result<u64, Box<EvalAltResult>>
```

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn *(x: i16, y: i16) -> Result<i16, Box<EvalAltResult>>
```

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn *(x: i128, y: i128) -> Result<i128, Box<EvalAltResult>>
```

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn *(x: u128, y: u128) -> Result<u128, Box<EvalAltResult>>
```

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn *(x: u32, y: u32) -> Result<u32, Box<EvalAltResult>>
```

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn *(x: u16, y: u16) -> Result<u16, Box<EvalAltResult>>
```

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn *(x: f32, y: int) -> f32
```

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn **(x: u8, y: int) -> Result<u8, Box<EvalAltResult>>
```

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn **(x: i8, y: int) -> Result<i8, Box<EvalAltResult>>
```

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn **(x: f32, y: f32) -> f32
```

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn **(x: u64, y: int) -> Result<u64, Box<EvalAltResult>>
```

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn **(x: i16, y: int) -> Result<i16, Box<EvalAltResult>>
```

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn **(x: u128, y: int) -> Result<u128, Box<EvalAltResult>>
```

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn **(x: u32, y: int) -> Result<u32, Box<EvalAltResult>>
```

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn **(x: f32, y: int) -> Result<f32, Box<EvalAltResult>>
```

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn **(x: i32, y: int) -> Result<i32, Box<EvalAltResult>>
```

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn **(x: i128, y: int) -> Result<i128, Box<EvalAltResult>>
```

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn **(x: u16, y: int) -> Result<u16, Box<EvalAltResult>>
```

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn +(x: i16) -> i16
```

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn +(x: int) -> int
```

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn +(x: i32) -> i32
```

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn +(x: i8) -> i8
```

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn +(x: i128) -> i128
```

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn +(x: float) -> float
```

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn +(x: f32) -> f32
```

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn +(_item: (), string: String) -> String
```

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn +(item: ?, string: String) -> String
```

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn +(string: String, mut item: ?) -> String
```

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn +(array1: Array, array2: Array) -> Array
```

<details>
<summary markdown="span"> details </summary>

Combine two arrays into a new array and return it.

# Example

```rhai
let x = [1, 2, 3];
let y = [true, 'x'];

print(x + y);   // prints "[1, 2, 3, true, 'x']"

print(x);       // prints "[1, 2, 3"
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn +(x: u64, y: u64) -> Result<u64, Box<EvalAltResult>>
```

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn +(x: u16, y: u16) -> Result<u16, Box<EvalAltResult>>
```

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn +(x: u32, y: u32) -> Result<u32, Box<EvalAltResult>>
```

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn +(x: int, y: f32) -> f32
```

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn +(x: i8, y: i8) -> Result<i8, Box<EvalAltResult>>
```

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn +(map1: Map, map2: Map) -> Map
```

<details>
<summary markdown="span"> details </summary>

Make a copy of the object map, add all property values of another object map
(existing property values of the same names are replaced), then returning it.

# Example

```rhai
let m = #{a:1, b:2, c:3};
let n = #{a: 42, d:0};

print(m + n);       // prints "#{a:42, b:2, c:3, d:0}"

print(m);           // prints "#{a:1, b:2, c:3}"
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn +(character: char, string: String) -> String
```

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn +(x: i32, y: i32) -> Result<i32, Box<EvalAltResult>>
```

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn +(utf8: Blob, string: String) -> String
```

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn +(string: String, utf8: Blob) -> String
```

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn +(timestamp: Instant, seconds: int) -> Result<Instant, Box<EvalAltResult>>
```

<details>
<summary markdown="span"> details </summary>

Add the specified number of `seconds` to the timestamp and return it as a new timestamp.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn +(x: i16, y: i16) -> Result<i16, Box<EvalAltResult>>
```

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn +(string: String, character: char) -> String
```

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn +(string1: String, string2: String) -> String
```

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn +(x: f32, y: int) -> f32
```

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn +(x: u8, y: u8) -> Result<u8, Box<EvalAltResult>>
```

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn +(x: u128, y: u128) -> Result<u128, Box<EvalAltResult>>
```

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn +(x: i128, y: i128) -> Result<i128, Box<EvalAltResult>>
```

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn +(timestamp: Instant, seconds: float) -> Result<Instant, Box<EvalAltResult>>
```

<details>
<summary markdown="span"> details </summary>

Add the specified number of `seconds` to the timestamp and return it as a new timestamp.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn +(string: String, item: ()) -> String
```

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn +(x: f32, y: f32) -> f32
```

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn +=(string: String, character: char)
```

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn +=(timestamp: Instant, seconds: int) -> Result<(), Box<EvalAltResult>>
```

<details>
<summary markdown="span"> details </summary>

Add the specified number of `seconds` to the timestamp.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn +=(string: String, utf8: Blob)
```

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn +=(timestamp: Instant, seconds: float) -> Result<(), Box<EvalAltResult>>
```

<details>
<summary markdown="span"> details </summary>

Add the specified number of `seconds` to the timestamp.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn +=(string: String, mut item: ?)
```

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn +=(string: String, item: ())
```

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn +=(string1: String, string2: String)
```

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn +=(map: Map, map2: Map)
```

<details>
<summary markdown="span"> details </summary>

Add all property values of another object map into the object map.
Existing property values of the same names are replaced.

# Example

```rhai
let m = #{a:1, b:2, c:3};
let n = #{a: 42, d:0};

m.mixin(n);

print(m);       // prints "#{a:42, b:2, c:3, d:0}"
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn -(x: float) -> float
```

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn -(x: int) -> Result<int, Box<EvalAltResult>>
```

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn -(x: i32) -> Result<i32, Box<EvalAltResult>>
```

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn -(x: f32) -> f32
```

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn -(x: i16) -> Result<i16, Box<EvalAltResult>>
```

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn -(x: i128) -> Result<i128, Box<EvalAltResult>>
```

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn -(x: i8) -> Result<i8, Box<EvalAltResult>>
```

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn -(x: i16, y: i16) -> Result<i16, Box<EvalAltResult>>
```

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn -(x: i8, y: i8) -> Result<i8, Box<EvalAltResult>>
```

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn -(x: u64, y: u64) -> Result<u64, Box<EvalAltResult>>
```

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn -(timestamp: Instant, seconds: float) -> Result<Instant, Box<EvalAltResult>>
```

<details>
<summary markdown="span"> details </summary>

Subtract the specified number of `seconds` from the timestamp and return it as a new timestamp.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn -(timestamp1: Instant, timestamp2: Instant) -> Result<?, Box<EvalAltResult>>
```

<details>
<summary markdown="span"> details </summary>

Return the number of seconds between two timestamps.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn -(timestamp: Instant, seconds: int) -> Result<Instant, Box<EvalAltResult>>
```

<details>
<summary markdown="span"> details </summary>

Subtract the specified number of `seconds` from the timestamp and return it as a new timestamp.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn -(x: f32, y: int) -> f32
```

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn -(x: u16, y: u16) -> Result<u16, Box<EvalAltResult>>
```

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn -(x: i32, y: i32) -> Result<i32, Box<EvalAltResult>>
```

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn -(x: int, y: f32) -> f32
```

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn -(x: u32, y: u32) -> Result<u32, Box<EvalAltResult>>
```

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn -(x: u128, y: u128) -> Result<u128, Box<EvalAltResult>>
```

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn -(x: i128, y: i128) -> Result<i128, Box<EvalAltResult>>
```

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn -(x: u8, y: u8) -> Result<u8, Box<EvalAltResult>>
```

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn -(x: f32, y: f32) -> f32
```

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn -=(timestamp: Instant, seconds: int) -> Result<(), Box<EvalAltResult>>
```

<details>
<summary markdown="span"> details </summary>

Subtract the specified number of `seconds` from the timestamp.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn -=(timestamp: Instant, seconds: float) -> Result<(), Box<EvalAltResult>>
```

<details>
<summary markdown="span"> details </summary>

Subtract the specified number of `seconds` from the timestamp.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn /(x: f32, y: f32) -> f32
```

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn /(x: i8, y: i8) -> Result<i8, Box<EvalAltResult>>
```

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn /(x: u128, y: u128) -> Result<u128, Box<EvalAltResult>>
```

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn /(x: i16, y: i16) -> Result<i16, Box<EvalAltResult>>
```

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn /(x: u32, y: u32) -> Result<u32, Box<EvalAltResult>>
```

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn /(x: i32, y: i32) -> Result<i32, Box<EvalAltResult>>
```

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn /(x: f32, y: int) -> f32
```

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn /(x: u16, y: u16) -> Result<u16, Box<EvalAltResult>>
```

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn /(x: u8, y: u8) -> Result<u8, Box<EvalAltResult>>
```

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn /(x: i128, y: i128) -> Result<i128, Box<EvalAltResult>>
```

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn /(x: u64, y: u64) -> Result<u64, Box<EvalAltResult>>
```

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn /(x: int, y: f32) -> f32
```

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn <(x: i16, y: i16) -> bool
```

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn <(x: float, y: int) -> bool
```

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn <(x: u128, y: u128) -> bool
```

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn <(x: u32, y: u32) -> bool
```

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn <(timestamp1: Instant, timestamp2: Instant) -> bool
```

<details>
<summary markdown="span"> details </summary>

Return `true` if the first timestamp is earlier than the second.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn <(x: f32, y: int) -> bool
```

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn <(x: f32, y: f32) -> bool
```

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn <(x: i8, y: i8) -> bool
```

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn <(x: u8, y: u8) -> bool
```

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn <(x: int, y: float) -> bool
```

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn <(x: u16, y: u16) -> bool
```

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn <(x: int, y: f32) -> bool
```

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn <(x: u64, y: u64) -> bool
```

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn <(x: i128, y: i128) -> bool
```

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn <(x: i32, y: i32) -> bool
```

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn <<(x: u64, y: int) -> Result<u64, Box<EvalAltResult>>
```

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn <<(x: u32, y: int) -> Result<u32, Box<EvalAltResult>>
```

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn <<(x: i32, y: int) -> Result<i32, Box<EvalAltResult>>
```

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn <<(x: u16, y: int) -> Result<u16, Box<EvalAltResult>>
```

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn <<(x: i8, y: int) -> Result<i8, Box<EvalAltResult>>
```

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn <<(x: i128, y: int) -> Result<i128, Box<EvalAltResult>>
```

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn <<(x: u8, y: int) -> Result<u8, Box<EvalAltResult>>
```

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn <<(x: u128, y: int) -> Result<u128, Box<EvalAltResult>>
```

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn <<(x: i16, y: int) -> Result<i16, Box<EvalAltResult>>
```

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn <=(x: u128, y: u128) -> bool
```

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn <=(x: u64, y: u64) -> bool
```

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn <=(x: u32, y: u32) -> bool
```

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn <=(x: f32, y: f32) -> bool
```

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn <=(x: f32, y: int) -> bool
```

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn <=(x: i128, y: i128) -> bool
```

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn <=(x: i32, y: i32) -> bool
```

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn <=(x: i8, y: i8) -> bool
```

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn <=(x: float, y: int) -> bool
```

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn <=(timestamp1: Instant, timestamp2: Instant) -> bool
```

<details>
<summary markdown="span"> details </summary>

Return `true` if the first timestamp is earlier than or equals to the second.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn <=(x: i16, y: i16) -> bool
```

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn <=(x: u16, y: u16) -> bool
```

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn <=(x: int, y: float) -> bool
```

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn <=(x: int, y: f32) -> bool
```

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn <=(x: u8, y: u8) -> bool
```

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn ==(x: int, y: f32) -> bool
```

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn ==(x: u16, y: u16) -> bool
```

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn ==(x: u128, y: u128) -> bool
```

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn ==(x: i16, y: i16) -> bool
```

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn ==(x: int, y: float) -> bool
```

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn ==(x: float, y: int) -> bool
```

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn ==(x: i8, y: i8) -> bool
```

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn ==(x: u8, y: u8) -> bool
```

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn ==(x: u64, y: u64) -> bool
```

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn ==(x: u32, y: u32) -> bool
```

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn ==(map1: Map, map2: Map) -> Result<bool, Box<EvalAltResult>>
```

<details>
<summary markdown="span"> details </summary>

Return `true` if two object maps are equal (i.e. all property values are equal).

The operator `==` is used to compare property values and must be defined,
otherwise `false` is assumed.

# Example

```rhai
let m1 = #{a:1, b:2, c:3};
let m2 = #{a:1, b:2, c:3};
let m3 = #{a:1, c:3};

print(m1 == m2);        // prints true

print(m1 == m3);        // prints false
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn ==(in1: Status, in2: Status) -> bool
```

<details>
<summary markdown="span"> details </summary>

Operator `==` for `Status`
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn ==(array1: Array, array2: Array) -> Result<bool, Box<EvalAltResult>>
```

<details>
<summary markdown="span"> details </summary>

Return `true` if two arrays are equal (i.e. all elements are equal and in the same order).

The operator `==` is used to compare elements and must be defined,
otherwise `false` is assumed.

# Example

```rhai
let x = [1, 2, 3, 4, 5];
let y = [1, 2, 3, 4, 5];
let z = [1, 2, 3, 4];

print(x == y);      // prints true

print(x == z);      // prints false
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn ==(x: i128, y: i128) -> bool
```

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn ==(x: f32, y: f32) -> bool
```

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn ==(x: i32, y: i32) -> bool
```

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn ==(x: f32, y: int) -> bool
```

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn ==(timestamp1: Instant, timestamp2: Instant) -> bool
```

<details>
<summary markdown="span"> details </summary>

Return `true` if two timestamps are equal.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn >(x: u64, y: u64) -> bool
```

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn >(x: u16, y: u16) -> bool
```

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn >(x: i32, y: i32) -> bool
```

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn >(x: f32, y: f32) -> bool
```

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn >(x: i128, y: i128) -> bool
```

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn >(x: u128, y: u128) -> bool
```

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn >(x: f32, y: int) -> bool
```

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn >(timestamp1: Instant, timestamp2: Instant) -> bool
```

<details>
<summary markdown="span"> details </summary>

Return `true` if the first timestamp is later than the second.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn >(x: u32, y: u32) -> bool
```

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn >(x: i8, y: i8) -> bool
```

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn >(x: i16, y: i16) -> bool
```

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn >(x: int, y: f32) -> bool
```

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn >(x: float, y: int) -> bool
```

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn >(x: int, y: float) -> bool
```

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn >(x: u8, y: u8) -> bool
```

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn >=(x: i16, y: i16) -> bool
```

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn >=(x: i8, y: i8) -> bool
```

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn >=(x: i128, y: i128) -> bool
```

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn >=(x: u64, y: u64) -> bool
```

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn >=(x: float, y: int) -> bool
```

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn >=(x: int, y: float) -> bool
```

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn >=(timestamp1: Instant, timestamp2: Instant) -> bool
```

<details>
<summary markdown="span"> details </summary>

Return `true` if the first timestamp is later than or equals to the second.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn >=(x: f32, y: int) -> bool
```

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn >=(x: u32, y: u32) -> bool
```

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn >=(x: i32, y: i32) -> bool
```

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn >=(x: u128, y: u128) -> bool
```

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn >=(x: int, y: f32) -> bool
```

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn >=(x: f32, y: f32) -> bool
```

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn >=(x: u16, y: u16) -> bool
```

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn >=(x: u8, y: u8) -> bool
```

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn >>(x: i8, y: int) -> Result<i8, Box<EvalAltResult>>
```

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn >>(x: u128, y: int) -> Result<u128, Box<EvalAltResult>>
```

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn >>(x: u32, y: int) -> Result<u32, Box<EvalAltResult>>
```

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn >>(x: u8, y: int) -> Result<u8, Box<EvalAltResult>>
```

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn >>(x: u16, y: int) -> Result<u16, Box<EvalAltResult>>
```

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn >>(x: u64, y: int) -> Result<u64, Box<EvalAltResult>>
```

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn >>(x: i128, y: int) -> Result<i128, Box<EvalAltResult>>
```

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn >>(x: i16, y: int) -> Result<i16, Box<EvalAltResult>>
```

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn >>(x: i32, y: int) -> Result<i32, Box<EvalAltResult>>
```

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn E() -> float
```

<details>
<summary markdown="span"> details </summary>

Return the natural number _e_.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn PI() -> float
```

<details>
<summary markdown="span"> details </summary>

Return the number π.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn ^(x: u32, y: u32) -> u32
```

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn ^(x: u128, y: u128) -> u128
```

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn ^(x: i32, y: i32) -> i32
```

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn ^(x: u8, y: u8) -> u8
```

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn ^(x: u64, y: u64) -> u64
```

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn ^(x: i16, y: i16) -> i16
```

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn ^(x: i128, y: i128) -> i128
```

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn ^(x: u16, y: u16) -> u16
```

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn ^(x: i8, y: i8) -> i8
```

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn abs(x: i8) -> Result<i8, Box<EvalAltResult>>
```

<details>
<summary markdown="span"> details </summary>

Return the absolute value of the number.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn abs(x: int) -> Result<int, Box<EvalAltResult>>
```

<details>
<summary markdown="span"> details </summary>

Return the absolute value of the number.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn abs(x: i32) -> Result<i32, Box<EvalAltResult>>
```

<details>
<summary markdown="span"> details </summary>

Return the absolute value of the number.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn abs(x: i128) -> Result<i128, Box<EvalAltResult>>
```

<details>
<summary markdown="span"> details </summary>

Return the absolute value of the number.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn abs(x: float) -> float
```

<details>
<summary markdown="span"> details </summary>

Return the absolute value of the floating-point number.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn abs(x: f32) -> f32
```

<details>
<summary markdown="span"> details </summary>

Return the absolute value of the floating-point number.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn abs(x: i16) -> Result<i16, Box<EvalAltResult>>
```

<details>
<summary markdown="span"> details </summary>

Return the absolute value of the number.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn accept() -> Status
```

<details>
<summary markdown="span"> details </summary>

Return a [`Status::Accept`] with the default code associated
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn accept(code: SharedObject) -> Status
```

<details>
<summary markdown="span"> details </summary>

Return a [`Status::Accept`] with `code`

# Errors

* `code` is not a valid code
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn accept(code: String) -> Status
```

<details>
<summary markdown="span"> details </summary>

Return a [`Status::Accept`] with `code`

# Errors

* `code` is not a valid code
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn acos(x: float) -> float
```

<details>
<summary markdown="span"> details </summary>

Return the arc-cosine of the floating-point number, in radians.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn acosh(x: float) -> float
```

<details>
<summary markdown="span"> details </summary>

Return the arc-hyperbolic-cosine of the floating-point number, in radians.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn add_rcpt_envelop(context: Context, new_addr: String) -> ()
```

<details>
<summary markdown="span"> details </summary>

add a recipient to the envelop.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn add_rcpt_envelop(context: Context, new_addr: SharedObject) -> ()
```

<details>
<summary markdown="span"> details </summary>

add a recipient to the envelop.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn add_rcpt_message(message: Message, new_addr: String) -> ()
```

<details>
<summary markdown="span"> details </summary>

add a recipient to the 'To' mail header.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn add_rcpt_message(message: Message, new_addr: SharedObject) -> ()
```

<details>
<summary markdown="span"> details </summary>

add a recipient to the 'To' mail header.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn all(array: Array, filter: FnPtr) -> Result<bool, Box<EvalAltResult>>
```

<details>
<summary markdown="span"> details </summary>

Return `true` if all elements in the array return `true` when applied the `filter` function.

# Function Parameters

* `element`: copy of array element
* `index` _(optional)_: current index in the array

# Example

```rhai
let x = [1, 2, 3, 4, 1, 2, 3, 4, 1, 2, 3, 4, 5];

print(x.all(|v| v > 3));        // prints false

print(x.all(|v| v > 1));        // prints true

print(x.all(|v, i| i > v));     // prints false
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn all(array: Array, filter: String) -> Result<bool, Box<EvalAltResult>>
```

<details>
<summary markdown="span"> details </summary>

Return `true` if all elements in the array return `true` when applied a function named by `filter`.

# Function Parameters

A function with the same name as the value of `filter` must exist taking these parameters:

* `element`: copy of array element
* `index` _(optional)_: current index in the array

# Example

```rhai
let x = [1, 2, 3, 4, 1, 2, 3, 4, 1, 2, 3, 4, 5];

print(x.all(|v| v > 3));        // prints false

print(x.all(|v| v > 1));        // prints true

print(x.all(|v, i| i > v));     // prints false
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn append(array: Array, new_array: Array)
```

<details>
<summary markdown="span"> details </summary>

Add all the elements of another array to the end of the array.

# Example

```rhai
let x = [1, 2, 3];
let y = [true, 'x'];

x.append(y);

print(x);       // prints "[1, 2, 3, true, 'x']"
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn append(blob: Blob, string: String)
```

<details>
<summary markdown="span"> details </summary>

Add a string (as UTF-8 encoded byte-stream) to the end of the BLOB

# Example

```rhai
let b = blob(5, 0x42);

b.append("hello");

print(b);       // prints "[424242424268656c 6c6f]"
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn append(string: String, mut item: ?)
```

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn append(blob: Blob, character: char)
```

<details>
<summary markdown="span"> details </summary>

Add a character (as UTF-8 encoded byte-stream) to the end of the BLOB

# Example

```rhai
let b = blob(5, 0x42);

b.append('!');

print(b);       // prints "[424242424221]"
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn append(blob1: Blob, blob2: Blob)
```

<details>
<summary markdown="span"> details </summary>

Add another BLOB to the end of the BLOB.

# Example

```rhai
let b1 = blob(5, 0x42);
let b2 = blob(3, 0x11);

b1.push(b2);

print(b1);      // prints "[4242424242111111]"
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn append(blob: Blob, value: int)
```

<details>
<summary markdown="span"> details </summary>

Add a new byte `value` to the end of the BLOB.

Only the lower 8 bits of the `value` are used; all other bits are ignored.

# Example

```rhai
let b = blob();

b.push(0x42);

print(b);       // prints "[42]"
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn append(string: String, utf8: Blob)
```

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn append_header(message: Message, header: String, value: String) -> ()
```

<details>
<summary markdown="span"> details </summary>

Add a header **at the end** of the Header section of the message.

# Examples

```
"X-My-Header: 250 foo\r\n",
"Subject: Unit test are cool\r\n",
"\r\n",
"Hello world!\r\n",

  preq: [
    rule "append_header" || {
      append_header("X-My-Header-2", "bar");
      append_header("X-My-Header-3", identifier("baz"));
    }
  ]
}
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn append_header(message: Message, header: String, value: SharedObject) -> ()
```

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn as_string(blob: Blob) -> String
```

<details>
<summary markdown="span"> details </summary>

Convert the BLOB into a string.

The byte stream must be valid UTF-8, otherwise an error is raised.

# Example

```rhai
let b = blob(5, 0x42);

let x = b.as_string();

print(x);       // prints "FFFFF"
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn asin(x: float) -> float
```

<details>
<summary markdown="span"> details </summary>

Return the arc-sine of the floating-point number, in radians.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn asinh(x: float) -> float
```

<details>
<summary markdown="span"> details </summary>

Return the arc-hyperbolic-sine of the floating-point number, in radians.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn atan(x: float) -> float
```

<details>
<summary markdown="span"> details </summary>

Return the arc-tangent of the floating-point number, in radians.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn atan(x: float, y: float) -> float
```

<details>
<summary markdown="span"> details </summary>

Return the arc-tangent of the floating-point numbers `x` and `y`, in radians.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn atanh(x: float) -> float
```

<details>
<summary markdown="span"> details </summary>

Return the arc-hyperbolic-tangent of the floating-point number, in radians.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn bits(value: int) -> Iterator<bool>
```

<details>
<summary markdown="span"> details </summary>

Return an iterator over all the bits in the number.

# Example

```rhai
let x = 123456;

for bit in x.bits() {
    print(bit);
}
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn bits(value: int, from: int) -> Iterator<bool>
```

<details>
<summary markdown="span"> details </summary>

Return an iterator over the bits in the number starting from the specified `start` position.

If `start` < 0, position counts from the MSB (Most Significant Bit)>.

# Example

```rhai
let x = 123456;

for bit in x.bits(10) {
    print(bit);
}
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn bits(value: int, range: RangeInclusive<int>) -> Iterator<bool>
```

<details>
<summary markdown="span"> details </summary>

Return an iterator over an inclusive range of bits in the number.

# Example

```rhai
let x = 123456;

for bit in x.bits(10..=23) {
    print(bit);
}
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn bits(value: int, range: Range<int>) -> Iterator<bool>
```

<details>
<summary markdown="span"> details </summary>

Return an iterator over an exclusive range of bits in the number.

# Example

```rhai
let x = 123456;

for bit in x.bits(10..24) {
    print(bit);
}
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn bits(value: int, from: int, len: int) -> Iterator<bool>
```

<details>
<summary markdown="span"> details </summary>

Return an iterator over a portion of bits in the number.

* If `start` < 0, position counts from the MSB (Most Significant Bit)>.
* If `len` ≤ 0, an empty iterator is returned.
* If `start` position + `len` ≥ length of string, all bits of the number after the `start` position are iterated.

# Example

```rhai
let x = 123456;

for bit in x.bits(10, 8) {
    print(bit);
}
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn blob() -> Blob
```

<details>
<summary markdown="span"> details </summary>

Return a new, empty BLOB.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn blob(len: int) -> Result<Blob, Box<EvalAltResult>>
```

<details>
<summary markdown="span"> details </summary>

Return a new BLOB of the specified length, filled with zeros.

If `len` ≤ 0, an empty BLOB is returned.

# Example

```rhai
let b = blob(10);

print(b);       // prints "[0000000000000000 0000]"
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn blob(len: int, value: int) -> Result<Blob, Box<EvalAltResult>>
```

<details>
<summary markdown="span"> details </summary>

Return a new BLOB of the specified length, filled with copies of the initial `value`.

If `len` ≤ 0, an empty BLOB is returned.

Only the lower 8 bits of the initial `value` are used; all other bits are ignored.

# Example

```rhai
let b = blob(10, 0x42);

print(b);       // prints "[4242424242424242 4242]"
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn bytes(string: String) -> int
```

<details>
<summary markdown="span"> details </summary>

Return the length of the string, in number of bytes used to store it in UTF-8 encoding.

# Example

```rhai
let text = "朝には紅顔ありて夕べには白骨となる";

print(text.bytes);      // prints 51
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn ceiling(x: float) -> float
```

<details>
<summary markdown="span"> details </summary>

Return the smallest whole number larger than or equals to the floating-point number.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn chars(string: String) -> Iterator<char>
```

<details>
<summary markdown="span"> details </summary>

Return an iterator over the characters in the string.

# Example

```rhai
for ch in "hello, world!".chars() {
    print(ch);
}
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn chars(string: String, from: int) -> Iterator<char>
```

<details>
<summary markdown="span"> details </summary>

Return an iterator over the characters in the string starting from the `start` position.

* If `start` < 0, position counts from the end of the string (`-1` is the last character).
* If `start` < -length of string, position counts from the beginning of the string.
* If `start` ≥ length of string, an empty iterator is returned.

# Example

```rhai
for ch in "hello, world!".chars(2) {
    print(ch);
}
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn chars(string: String, range: RangeInclusive<int>) -> Iterator<char>
```

<details>
<summary markdown="span"> details </summary>

Return an iterator over an inclusive range of characters in the string.

# Example

```rhai
for ch in "hello, world!".chars(2..=6) {
    print(ch);
}
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn chars(string: String, range: Range<int>) -> Iterator<char>
```

<details>
<summary markdown="span"> details </summary>

Return an iterator over an exclusive range of characters in the string.

# Example

```rhai
for ch in "hello, world!".chars(2..5) {
    print(ch);
}
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn chars(string: String, start: int, len: int) -> Iterator<char>
```

<details>
<summary markdown="span"> details </summary>

Return an iterator over a portion of characters in the string.

* If `start` < 0, position counts from the end of the string (`-1` is the last character).
* If `start` < -length of string, position counts from the beginning of the string.
* If `start` ≥ length of string, an empty iterator is returned.
* If `len` ≤ 0, an empty iterator is returned.
* If `start` position + `len` ≥ length of string, all characters of the string after the `start` position are iterated.

# Example

```rhai
for ch in "hello, world!".chars(2, 4) {
    print(ch);
}
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn check_spf(ctx: Context, srv: Server) -> Map>
```

<details>
<summary markdown="span"> details </summary>

evaluate a sender identity.
the identity parameter can be 'helo', 'mail_from' or 'both'.

# Results
a rhai Map with:
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn chop(blob: Blob, len: int)
```

<details>
<summary markdown="span"> details </summary>

Cut off the head of the BLOB, leaving a tail of the specified length.

* If `len` ≤ 0, the BLOB is cleared.
* If `len` ≥ length of BLOB, the BLOB is not modified.

# Example

```rhai
let b = blob();

b += 1; b += 2; b += 3; b += 4; b += 5;

b.chop(3);

print(b);           // prints "[030405]"

b.chop(10);

print(b);           // prints "[030405]"
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn chop(array: Array, len: int)
```

<details>
<summary markdown="span"> details </summary>

Cut off the head of the array, leaving a tail of the specified length.

* If `len` ≤ 0, the array is cleared.
* If `len` ≥ length of array, the array is not modified.

# Example

```rhai
let x = [1, 2, 3, 4, 5];

x.chop(3);

print(x);       // prints "[3, 4, 5]"

x.chop(10);

print(x);       // prints "[3, 4, 5]"
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn clear(array: Array)
```

<details>
<summary markdown="span"> details </summary>

Clear the array.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn clear(string: String)
```

<details>
<summary markdown="span"> details </summary>

Clear the string, making it empty.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn clear(map: Map)
```

<details>
<summary markdown="span"> details </summary>

Clear the object map.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn clear(blob: Blob)
```

<details>
<summary markdown="span"> details </summary>

Clear the BLOB.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn contains(range: Range<int>, value: int) -> bool
```

<details>
<summary markdown="span"> details </summary>

Return `true` if the range contains a specified value.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn contains(array: Array, value: ?) -> Result<bool, Box<EvalAltResult>>
```

<details>
<summary markdown="span"> details </summary>

Return `true` if the array contains an element that equals `value`.

The operator `==` is used to compare elements with `value` and must be defined,
otherwise `false` is assumed.

This function also drives the `in` operator.

# Example

```rhai
let x = [1, 2, 3, 4, 5];

// The 'in' operator calls 'contains' in the background
if 4 in x {
    print("found!");
}
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn contains(string: String, match_string: String) -> bool
```

<details>
<summary markdown="span"> details </summary>

Return `true` if the string contains a specified string.

# Example

```rhai
let text = "hello, world!";

print(text.contains("hello"));  // prints true

print(text.contains("hey"));    // prints false
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn contains(string: String, character: char) -> bool
```

<details>
<summary markdown="span"> details </summary>

Return `true` if the string contains a specified character.

# Example

```rhai
let text = "hello, world!";

print(text.contains('h'));      // prints true

print(text.contains('x'));      // prints false
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn contains(range: RangeInclusive<int>, value: int) -> bool
```

<details>
<summary markdown="span"> details </summary>

Return `true` if the range contains a specified value.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn contains(blob: Blob, value: int) -> bool
```

<details>
<summary markdown="span"> details </summary>

Return `true` if the BLOB contains a specified byte value.

# Example

```rhai
let text = "hello, world!";

print(text.contains('h'));      // prints true

print(text.contains('x'));      // prints false
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn contains(map: Map, property: String) -> bool
```

<details>
<summary markdown="span"> details </summary>

Returns `true` if the object map contains a specified property.

# Example

```rhai
let m = #{a: 1, b: 2, c: 3};

print(m.contains("b"));     // prints true

print(m.contains("x"));     // prints false
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn cos(x: float) -> float
```

<details>
<summary markdown="span"> details </summary>

Return the cosine of the floating-point number in radians.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn cosh(x: float) -> float
```

<details>
<summary markdown="span"> details </summary>

Return the hyperbolic cosine of the floating-point number in radians.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn count_header(message: Message, header: SharedObject) -> int>
```

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn count_header(message: Message, header: String) -> int>
```

<details>
<summary markdown="span"> details </summary>

Count the number of headers with the given name.

# Examples

```
"X-My-Header: foo\r\n",
"X-My-Header: bar\r\n",
"X-My-Header: baz\r\n",
"Subject: Unit test are cool\r\n",
"\r\n",
"Hello world!\r\n",

  preq: [
    rule "count_header" || {
      accept(`250 count is ${count_header("X-My-Header")} and ${count_header(identifier("Subject"))}`);
    }
  ]
}
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn crop(string: String, range: RangeInclusive<int>)
```

<details>
<summary markdown="span"> details </summary>

Remove all characters from the string except those within an inclusive `range`.

# Example

```rhai
let text = "hello, world!";

text.crop(2..=8);

print(text);        // prints "llo, wo"
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn crop(string: String, start: int)
```

<details>
<summary markdown="span"> details </summary>

Remove all characters from the string except until the `start` position.

* If `start` < 0, position counts from the end of the string (`-1` is the last character).
* If `start` < -length of string, the string is not modified.
* If `start` ≥ length of string, the entire string is cleared.

# Example

```rhai
let text = "hello, world!";

text.crop(5);

print(text);            // prints ", world!"

text.crop(-3);

print(text);            // prints "ld!"
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn crop(string: String, range: Range<int>)
```

<details>
<summary markdown="span"> details </summary>

Remove all characters from the string except those within an exclusive `range`.

# Example

```rhai
let text = "hello, world!";

text.crop(2..8);

print(text);        // prints "llo, w"
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn crop(string: String, start: int, len: int)
```

<details>
<summary markdown="span"> details </summary>

Remove all characters from the string except those within a range.

* If `start` < 0, position counts from the end of the string (`-1` is the last character).
* If `start` < -length of string, position counts from the beginning of the string.
* If `start` ≥ length of string, the entire string is cleared.
* If `len` ≤ 0, the entire string is cleared.
* If `start` position + `len` ≥ length of string, only the portion of the string after the `start` position is retained.

# Example

```rhai
let text = "hello, world!";

text.crop(2, 8);

print(text);        // prints "llo, wor"

text.crop(-5, 3);

print(text);        // prints ", w"
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn date() -> String
```

<details>
<summary markdown="span"> details </summary>

get the current date.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn debug() -> String
```

<details>
<summary markdown="span"> details </summary>

Return the empty string.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn debug(value: bool) -> String
```

<details>
<summary markdown="span"> details </summary>

Convert the boolean value into a string in debug format.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn debug(number: f32) -> String
```

<details>
<summary markdown="span"> details </summary>

Convert the value of `number` into a string.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn debug(number: float) -> String
```

<details>
<summary markdown="span"> details </summary>

Convert the value of `number` into a string.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn debug(f: FnPtr) -> String
```

<details>
<summary markdown="span"> details </summary>

Convert the function pointer into a string in debug format.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn debug(array: Array) -> String
```

<details>
<summary markdown="span"> details </summary>

Convert the array into a string.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn debug(map: Map) -> String
```

<details>
<summary markdown="span"> details </summary>

Convert the object map into a string.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn debug(item: ?) -> String
```

<details>
<summary markdown="span"> details </summary>

Convert the value of the `item` into a string in debug format.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn debug(string: String) -> String
```

<details>
<summary markdown="span"> details </summary>

Convert the string into debug format.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn debug(character: char) -> String
```

<details>
<summary markdown="span"> details </summary>

Convert the string into debug format.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn debug(unit: ()) -> String
```

<details>
<summary markdown="span"> details </summary>

Convert the unit into a string in debug format.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn dedup(array: Array)
```

<details>
<summary markdown="span"> details </summary>

Remove duplicated _consecutive_ elements from the array.

The operator `==` is used to compare elements and must be defined,
otherwise `false` is assumed.

# Example

```rhai
let x = [1, 2, 2, 2, 3, 4, 3, 3, 2, 1];

x.dedup();

print(x);       // prints "[1, 2, 3, 4, 3, 2, 1]"
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn dedup(array: Array, comparer: String) -> Result<(), Box<EvalAltResult>>
```

<details>
<summary markdown="span"> details </summary>

Remove duplicated _consecutive_ elements from the array that return `true` when applied a
function named by `comparer`.

No element is removed if the correct `comparer` function does not exist.

# Function Parameters

* `element1`: copy of the current array element to compare
* `element2`: copy of the next array element to compare

## Return Value

`true` if `element1 == element2`, otherwise `false`.

# Example

```rhai
fn declining(a, b) { a >= b }

let x = [1, 2, 2, 2, 3, 1, 2, 3, 4, 3, 3, 2, 1];

x.dedup("declining");

print(x);       // prints "[1, 2, 3, 4]"
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn dedup(array: Array, comparer: FnPtr)
```

<details>
<summary markdown="span"> details </summary>

Remove duplicated _consecutive_ elements from the array that return `true` when applied the
`comparer` function.

No element is removed if the correct `comparer` function does not exist.

# Function Parameters

* `element1`: copy of the current array element to compare
* `element2`: copy of the next array element to compare

## Return Value

`true` if `element1 == element2`, otherwise `false`.

# Example

```rhai
let x = [1, 2, 2, 2, 3, 1, 2, 3, 4, 3, 3, 2, 1];

x.dedup(|a, b| a >= b);

print(x);       // prints "[1, 2, 3, 4]"
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn deliver(context: Context, rcpt: String) -> ()
```

<details>
<summary markdown="span"> details </summary>

Set the delivery method to [`Transfer::Deliver`] for a single recipient.

# Examples

```
  rcpt: [
    action "deliver (str/str)" || {
      add_rcpt_envelop("my.address@foo.com");
      deliver("my.address@foo.com");
    },
    action "deliver (obj/str)" || {
      let rcpt = address("my.address@bar.com");
      add_rcpt_envelop(rcpt);
      deliver(rcpt);
    },
    action "deliver (str/obj)" || {
      let target = ip6("::1");
      add_rcpt_envelop("my.address@baz.com");
      deliver("my.address@baz.com");
    },
    action "deliver (obj/obj)" || {
      let rcpt = address("my.address@boz.com");
      add_rcpt_envelop(rcpt);
      deliver(rcpt);
    },
  ],
}

```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn deliver(context: Context, rcpt: SharedObject) -> ()
```

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn deliver_all(context: Context) -> ()
```

<details>
<summary markdown="span"> details </summary>

Set the delivery method to [`Transfer::Deliver`] for all recipients.

# Examples

```
  rcpt: [
    action "deliver_all" || {
      add_rcpt_envelop("my.address@foo.com");
      add_rcpt_envelop("my.address@bar.com");
      deliver_all();
    },
  ],
}

```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn deny() -> Status
```

<details>
<summary markdown="span"> details </summary>

Return a [`Status::Deny`] with the default code associated
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn deny(code: String) -> Status
```

<details>
<summary markdown="span"> details </summary>

Return a [`Status::Deny`] with `code`

# Errors

* `code` is not a valid code
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn deny(code: SharedObject) -> Status
```

<details>
<summary markdown="span"> details </summary>

Return a [`Status::Deny`] with `code`

# Errors

* `code` is not a valid code
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn dmarc_check(record: Record, rfc5322_from: String, dkim_result: Map, spf_mail_from: String, spf_result: String) -> bool
```

<details>
<summary markdown="span"> details </summary>


</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn drain(array: Array, filter: FnPtr) -> Result<Array, Box<EvalAltResult>>
```

<details>
<summary markdown="span"> details </summary>

Remove all elements in the array that returns `true` when applied the `filter` function and
return them as a new array.

# Function Parameters

* `element`: copy of array element
* `index` _(optional)_: current index in the array

# Example

```rhai
let x = [1, 2, 3, 4, 5];

let y = x.drain(|v| v < 3);

print(x);       // prints "[3, 4, 5]"

print(y);       // prints "[1, 2]"

let z = x.drain(|v, i| v + i > 5);

print(x);       // prints "[3, 4]"

print(z);       // prints "[5]"
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn drain(blob: Blob, range: Range<int>) -> Blob
```

<details>
<summary markdown="span"> details </summary>

Remove all bytes in the BLOB within an exclusive `range` and return them as a new BLOB.

# Example

```rhai
let b1 = blob();

b1 += 1; b1 += 2; b1 += 3; b1 += 4; b1 += 5;

let b2 = b1.drain(1..3);

print(b1);      // prints "[010405]"

print(b2);      // prints "[0203]"

let b3 = b1.drain(2..3);

print(b1);      // prints "[0104]"

print(b3);      // prints "[05]"
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn drain(array: Array, filter: String) -> Result<Array, Box<EvalAltResult>>
```

<details>
<summary markdown="span"> details </summary>

Remove all elements in the array that returns `true` when applied a function named by `filter`
and return them as a new array.

# Function Parameters

A function with the same name as the value of `filter` must exist taking these parameters:

* `element`: copy of array element
* `index` _(optional)_: current index in the array

# Example

```rhai
fn small(x) { x < 3 }

fn screen(x, i) { x + i > 5 }

let x = [1, 2, 3, 4, 5];

let y = x.drain("small");

print(x);       // prints "[3, 4, 5]"

print(y);       // prints "[1, 2]"

let z = x.drain("screen");

print(x);       // prints "[3, 4]"

print(z);       // prints "[5]"
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn drain(blob: Blob, range: RangeInclusive<int>) -> Blob
```

<details>
<summary markdown="span"> details </summary>

Remove all bytes in the BLOB within an inclusive `range` and return them as a new BLOB.

# Example

```rhai
let b1 = blob();

b1 += 1; b1 += 2; b1 += 3; b1 += 4; b1 += 5;

let b2 = b1.drain(1..=2);

print(b1);      // prints "[010405]"

print(b2);      // prints "[0203]"

let b3 = b1.drain(2..=2);

print(b1);      // prints "[0104]"

print(b3);      // prints "[05]"
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn drain(array: Array, range: Range<int>) -> Array
```

<details>
<summary markdown="span"> details </summary>

Remove all elements in the array within an exclusive `range` and return them as a new array.

# Example

```rhai
let x = [1, 2, 3, 4, 5];

let y = x.drain(1..3);

print(x);       // prints "[1, 4, 5]"

print(y);       // prints "[2, 3]"

let z = x.drain(2..3);

print(x);       // prints "[1, 4]"

print(z);       // prints "[5]"
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn drain(array: Array, range: RangeInclusive<int>) -> Array
```

<details>
<summary markdown="span"> details </summary>

Remove all elements in the array within an inclusive `range` and return them as a new array.

# Example

```rhai
let x = [1, 2, 3, 4, 5];

let y = x.drain(1..=2);

print(x);       // prints "[1, 4, 5]"

print(y);       // prints "[2, 3]"

let z = x.drain(2..=2);

print(x);       // prints "[1, 4]"

print(z);       // prints "[5]"
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn drain(blob: Blob, start: int, len: int) -> Blob
```

<details>
<summary markdown="span"> details </summary>

Remove all bytes within a portion of the BLOB and return them as a new BLOB.

* If `start` < 0, position counts from the end of the BLOB (`-1` is the last byte).
* If `start` < -length of BLOB, position counts from the beginning of the BLOB.
* If `start` ≥ length of BLOB, nothing is removed and an empty BLOB is returned.
* If `len` ≤ 0, nothing is removed and an empty BLOB is returned.
* If `start` position + `len` ≥ length of BLOB, entire portion of the BLOB after the `start` position is removed and returned.

# Example

```rhai
let b1 = blob();

b1 += 1; b1 += 2; b1 += 3; b1 += 4; b1 += 5;

let b2 = b1.drain(1, 2);

print(b1);      // prints "[010405]"

print(b2);      // prints "[0203]"

let b3 = b1.drain(-1, 1);

print(b3);      // prints "[0104]"

print(z);       // prints "[5]"
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn drain(array: Array, start: int, len: int) -> Array
```

<details>
<summary markdown="span"> details </summary>

Remove all elements within a portion of the array and return them as a new array.

* If `start` < 0, position counts from the end of the array (`-1` is the last element).
* If `start` < -length of array, position counts from the beginning of the array.
* If `start` ≥ length of array, no element is removed and an empty array is returned.
* If `len` ≤ 0, no element is removed and an empty array is returned.
* If `start` position + `len` ≥ length of array, entire portion of the array after the `start` position is removed and returned.

# Example

```rhai
let x = [1, 2, 3, 4, 5];

let y = x.drain(1, 2);

print(x);       // prints "[1, 4, 5]"

print(y);       // prints "[2, 3]"

let z = x.drain(-1, 1);

print(x);       // prints "[1, 4]"

print(z);       // prints "[5]"
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn dump(srv: Server, mut ctx: Context, dir: SharedObject) -> ()
```

<details>
<summary markdown="span"> details </summary>

write the content of the current email with it's metadata in a json file.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn dump(srv: Server, mut ctx: Context, dir: String) -> ()
```

<details>
<summary markdown="span"> details </summary>

write the content of the current email with it's metadata in a json file.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn elapsed(timestamp: Instant) -> Result<?, Box<EvalAltResult>>
```

<details>
<summary markdown="span"> details </summary>

Return the number of seconds between the current system time and the timestamp.

# Example

```rhai
let now = timestamp();

sleep(10.0);            // sleep for 10 seconds

print(now.elapsed);     // prints 10.???
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn end(range: Range<int>) -> int
```

<details>
<summary markdown="span"> details </summary>

Return the end of the exclusive range.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn end(range: RangeInclusive<int>) -> int
```

<details>
<summary markdown="span"> details </summary>

Return the end of the inclusive range.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn ends_with(string: String, match_string: String) -> bool
```

<details>
<summary markdown="span"> details </summary>

Return `true` if the string ends with a specified string.

# Example

```rhai
let text = "hello, world!";

print(text.ends_with("world!"));    // prints true

print(text.ends_with("hello"));     // prints false
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn exp(x: float) -> float
```

<details>
<summary markdown="span"> details </summary>

Return the exponential of the floating-point number.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn extract(blob: Blob, range: Range<int>) -> Blob
```

<details>
<summary markdown="span"> details </summary>

Copy an exclusive `range` of the BLOB and return it as a new BLOB.

# Example

```rhai
let b = blob();

b += 1; b += 2; b += 3; b += 4; b += 5;

print(b.extract(1..3));     // prints "[0203]"

print(b);                   // prints "[0102030405]"
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn extract(array: Array, start: int) -> Array
```

<details>
<summary markdown="span"> details </summary>

Copy a portion of the array beginning at the `start` position till the end and return it as
a new array.

* If `start` < 0, position counts from the end of the array (`-1` is the last element).
* If `start` < -length of array, the entire array is copied and returned.
* If `start` ≥ length of array, an empty array is returned.

# Example

```rhai
let x = [1, 2, 3, 4, 5];

print(x.extract(2));        // prints "[3, 4, 5]"

print(x.extract(-3));       // prints "[3, 4, 5]"

print(x);                   // prints "[1, 2, 3, 4, 5]"
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn extract(array: Array, range: Range<int>) -> Array
```

<details>
<summary markdown="span"> details </summary>

Copy an exclusive range of the array and return it as a new array.

# Example

```rhai
let x = [1, 2, 3, 4, 5];

print(x.extract(1..3));     // prints "[2, 3]"

print(x);                   // prints "[1, 2, 3, 4, 5]"
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn extract(blob: Blob, start: int) -> Blob
```

<details>
<summary markdown="span"> details </summary>

Copy a portion of the BLOB beginning at the `start` position till the end and return it as
a new BLOB.

* If `start` < 0, position counts from the end of the BLOB (`-1` is the last byte).
* If `start` < -length of BLOB, the entire BLOB is copied and returned.
* If `start` ≥ length of BLOB, an empty BLOB is returned.

# Example

```rhai
let b = blob();

b += 1; b += 2; b += 3; b += 4; b += 5;

print(b.extract(2));        // prints "[030405]"

print(b.extract(-3));       // prints "[030405]"

print(b);                   // prints "[0102030405]"
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn extract(blob: Blob, range: RangeInclusive<int>) -> Blob
```

<details>
<summary markdown="span"> details </summary>

Copy an inclusive `range` of the BLOB and return it as a new BLOB.

# Example

```rhai
let b = blob();

b += 1; b += 2; b += 3; b += 4; b += 5;

print(b.extract(1..=3));    // prints "[020304]"

print(b);                   // prints "[0102030405]"
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn extract(array: Array, range: RangeInclusive<int>) -> Array
```

<details>
<summary markdown="span"> details </summary>

Copy an inclusive range of the array and return it as a new array.

# Example

```rhai
let x = [1, 2, 3, 4, 5];

print(x.extract(1..=3));    // prints "[2, 3, 4]"

print(x);                   // prints "[1, 2, 3, 4, 5]"
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn extract(array: Array, start: int, len: int) -> Array
```

<details>
<summary markdown="span"> details </summary>

Copy a portion of the array and return it as a new array.

* If `start` < 0, position counts from the end of the array (`-1` is the last element).
* If `start` < -length of array, position counts from the beginning of the array.
* If `start` ≥ length of array, an empty array is returned.
* If `len` ≤ 0, an empty array is returned.
* If `start` position + `len` ≥ length of array, entire portion of the array after the `start` position is copied and returned.

# Example

```rhai
let x = [1, 2, 3, 4, 5];

print(x.extract(1, 3));     // prints "[2, 3, 4]"

print(x.extract(-3, 2));    // prints "[3, 4]"

print(x);                   // prints "[1, 2, 3, 4, 5]"
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn extract(blob: Blob, start: int, len: int) -> Blob
```

<details>
<summary markdown="span"> details </summary>

Copy a portion of the BLOB and return it as a new BLOB.

* If `start` < 0, position counts from the end of the BLOB (`-1` is the last byte).
* If `start` < -length of BLOB, position counts from the beginning of the BLOB.
* If `start` ≥ length of BLOB, an empty BLOB is returned.
* If `len` ≤ 0, an empty BLOB is returned.
* If `start` position + `len` ≥ length of BLOB, entire portion of the BLOB after the `start` position is copied and returned.

# Example

```rhai
let b = blob();

b += 1; b += 2; b += 3; b += 4; b += 5;

print(b.extract(1, 3));     // prints "[020303]"

print(b.extract(-3, 2));    // prints "[0304]"

print(b);                   // prints "[0102030405]"
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn faccept() -> Status
```

<details>
<summary markdown="span"> details </summary>

Return a [`Status::Faccept`] with the default code associated
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn faccept(code: SharedObject) -> Status
```

<details>
<summary markdown="span"> details </summary>

Return a [`Status::Faccept`] with `code`

# Errors

* `code` is not a valid code
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn faccept(code: String) -> Status
```

<details>
<summary markdown="span"> details </summary>

Return a [`Status::Faccept`] with `code`

# Errors

* `code` is not a valid code
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn fill_with(map: Map, map2: Map)
```

<details>
<summary markdown="span"> details </summary>

Add all property values of another object map into the object map.
Only properties that do not originally exist in the object map are added.

# Example

```rhai
let m = #{a:1, b:2, c:3};
let n = #{a: 42, d:0};

m.fill_with(n);

print(m);       // prints "#{a:1, b:2, c:3, d:0}"
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn filter(array: Array, filter: FnPtr) -> Result<Array, Box<EvalAltResult>>
```

<details>
<summary markdown="span"> details </summary>

Iterate through all the elements in the array, applying a `filter` function to each element
in turn, and return a copy of all elements (in order) that return `true` as a new array.

# Function Parameters

* `element`: copy of array element
* `index` _(optional)_: current index in the array

# Example

```rhai
let x = [1, 2, 3, 4, 5];

let y = x.filter(|v| v >= 3);

print(y);       // prints "[3, 4, 5]"

let y = x.filter(|v, i| v * i >= 10);

print(y);       // prints "[12, 20]"
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn filter(array: Array, filter_func: String) -> Result<Array, Box<EvalAltResult>>
```

<details>
<summary markdown="span"> details </summary>

Iterate through all the elements in the array, applying a function named by `filter` to each
element in turn, and return a copy of all elements (in order) that return `true` as a new array.

# Function Parameters

A function with the same name as the value of `filter` must exist taking these parameters:

* `element`: copy of array element
* `index` _(optional)_: current index in the array

# Example

```rhai
fn screen(x, i) { x * i >= 10 }

let x = [1, 2, 3, 4, 5];

let y = x.filter("is_odd");

print(y);       // prints "[1, 3, 5]"

let y = x.filter("screen");

print(y);       // prints "[12, 20]"
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn floor(x: float) -> float
```

<details>
<summary markdown="span"> details </summary>

Return the largest whole number less than or equals to the floating-point number.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn forward(context: Context, rcpt: SharedObject, forward: SharedObject) -> ()
```

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn forward(context: Context, rcpt: String, forward: String) -> ()
```

<details>
<summary markdown="span"> details </summary>

Set the delivery method to [`Transfer::Forward`] for a single recipient.

# Examples

```
  rcpt: [
    action "forward (str/str)" || {
      add_rcpt_envelop("my.address@foo.com");
      forward("my.address@foo.com", "127.0.0.1");
    },
    action "forward (obj/str)" || {
      let rcpt = address("my.address@bar.com");
      add_rcpt_envelop(rcpt);
      forward(rcpt, "127.0.0.2");
    },
    action "forward (str/obj)" || {
      let target = ip6("::1");
      add_rcpt_envelop("my.address@baz.com");
      forward("my.address@baz.com", target);
    },
    action "forward (obj/obj)" || {
      let rcpt = address("my.address@boz.com");
      add_rcpt_envelop(rcpt);
      forward(rcpt, ip4("127.0.0.4"));
    },
  ],
}

```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn forward(context: Context, rcpt: SharedObject, forward: String) -> ()
```

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn forward(context: Context, rcpt: String, forward: SharedObject) -> ()
```

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn forward_all(context: Context, forward: SharedObject) -> ()
```

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn forward_all(context: Context, forward: String) -> ()
```

<details>
<summary markdown="span"> details </summary>

Set the delivery method to [`Transfer::Forward`] for all recipients.

# Examples

```
  rcpt: [
    action "forward_all" || {
      add_rcpt_envelop("my.address@foo.com");
      add_rcpt_envelop("my.address@bar.com");
      forward_all("127.0.0.1");
    },
    action "forward_all (obj)" || {
      add_rcpt_envelop("my.address@foo2.com");
      add_rcpt_envelop("my.address@bar2.com");
      forward_all(ip4("127.0.0.1"));
    },
  ],
}

```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn fraction(x: float) -> float
```

<details>
<summary markdown="span"> details </summary>

Return the fractional part of the floating-point number.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn generate_signature_dkim(message: Message, context: Context, selector: String, private_key: Arc<PrivateKey>, headers_field: Array, canonicalization: String) -> String
```

<details>
<summary markdown="span"> details </summary>

Create a new signature of the message for the DKIM.

# Examples

```
Date: Wed, 26 Oct 2022 14:30:51 -0700
From: Mathieu Lala <noreply@github.com>
To: mlala@negabit.com
Subject: Testing and documenting the dkim signature

This message has not been signed yet, meaning someone could change it...
; // .eml ends here


  postq: [
    action "add a DKIM signature" || {
      for i in get_private_keys(srv(), "testserver.com") {
        sign_dkim("2022-09", i, ["From", "To", "Date", "Subject", "From"], "simple/relaxed");
      }
    },
    rule "check signature" || {
      let signature = "v=1; a=rsa-sha256; d=testserver.com; s=2022-09;\r\n\
          \tc=simple/relaxed; q=dns/txt; h=From:To:Date:Subject:From;\r\n\
          \tbh=ATHiC1KD8OegIorswWts+SlujGUpgqR6pqXYlNWA01Y=;\r\n\tb=Ur\
          /frdH3beyU3LRQMGBdI6OdxRvfpu+s04hmHcVkpBYzR4cXuDPByWpUCqhO4C\
          sEwpPRDcWQtsCfuzSK1FTf7XCWgsKKGPmsdQ40pUviA0UrrzpIDIziMxSI/S\
          8ohNnxvqxrtxZoN6Wo2lnQ+kYAATYxJPOjC57JIBJ89RGrf+6Wbvz6/PofcU\
          9VwpylegZRU5Cial69lN2qaIkoVFOE9fz8ZIz9VV2A9Lh/xgKFM7eipBWCR6\
          ZUU1HZTbSiqiL9Q6A823az/E2jqOUZXtsGK/Bo/vDjTV166d5vY34JA3189C\
          x83Rbif9A/kdCO6C8gGK0WOasp5R0ONmVz41TaGQ==";

      if get_header("DKIM-Signature") == signature {
        accept()
      } else {
        deny()
      }
    }
  ]
}

```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn get(map: Map, property: String) -> ?
```

<details>
<summary markdown="span"> details </summary>

Get the value of the `property` in the object map and return a copy.

If `property` does not exist in the object map, `()` is returned.

# Example

```rhai
let m = #{a: 1, b: 2, c: 3};

print(m.get("b"));      // prints 2

print(m.get("x"));      // prints empty (for '()')
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn get(array: Array, index: int) -> ?
```

<details>
<summary markdown="span"> details </summary>

Get a copy of the element at the `index` position in the array.

* If `index` < 0, position counts from the end of the array (`-1` is the last element).
* If `index` < -length of array, `()` is returned.
* If `index` ≥ length of array, `()` is returned.

# Example

```rhai
let x = [1, 2, 3];

print(x.get(0));        // prints 1

print(x.get(-1));       // prints 3

print(x.get(99));       // prints empty (for '()')
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn get(blob: Blob, index: int) -> int
```

<details>
<summary markdown="span"> details </summary>

Get the byte value at the `index` position in the BLOB.

* If `index` < 0, position counts from the end of the BLOB (`-1` is the last element).
* If `index` < -length of BLOB, zero is returned.
* If `index` ≥ length of BLOB, zero is returned.

# Example

```rhai
let b = blob();

b += 1; b += 2; b += 3; b += 4; b += 5;

print(b.get(0));        // prints 1

print(b.get(-1));       // prints 5

print(b.get(99));       // prints 0
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn get(string: String, index: int) -> ?
```

<details>
<summary markdown="span"> details </summary>

Get the character at the `index` position in the string.

* If `index` < 0, position counts from the end of the string (`-1` is the last character).
* If `index` < -length of string, zero is returned.
* If `index` ≥ length of string, zero is returned.

# Example

```rhai
let text = "hello, world!";

print(text.get(0));     // prints 'h'

print(text.get(-1));    // prints '!'

print(text.get(99));    // prints empty (for '()')'
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn get auid(signature: Signature) -> String
```

<details>
<summary markdown="span"> details </summary>

return the `auid` property of the [`Signature`]
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn get auth(context: Context) -> Credentials
```

<details>
<summary markdown="span"> details </summary>

Get the `auth` property of the connection.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn get authid(credentials: Credentials) -> String
```

<details>
<summary markdown="span"> details </summary>

Get the `authid` property of the connection.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn get authpass(credentials: Credentials) -> String
```

<details>
<summary markdown="span"> details </summary>

Get the `authpass` property of the connection.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn get bits(value: int) -> Iterator<bool>
```

<details>
<summary markdown="span"> details </summary>

Return an iterator over all the bits in the number.

# Example

```rhai
let x = 123456;

for bit in x.bits {
    print(bit);
}
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn get bytes(string: String) -> int
```

<details>
<summary markdown="span"> details </summary>

Return the length of the string, in number of bytes used to store it in UTF-8 encoding.

# Example

```rhai
let text = "朝には紅顔ありて夕べには白骨となる";

print(text.bytes);      // prints 51
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn get ceiling(x: float) -> float
```

<details>
<summary markdown="span"> details </summary>

Return the smallest whole number larger than or equals to the floating-point number.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn get chars(string: String) -> Iterator<char>
```

<details>
<summary markdown="span"> details </summary>

Return an iterator over all the characters in the string.

# Example

```rhai
for ch in "hello, world!".chars {
    print(ch);
}
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn get client_address(context: Context) -> String
```

<details>
<summary markdown="span"> details </summary>

Get the peer address of the client.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn get client_ip(context: Context) -> String
```

<details>
<summary markdown="span"> details </summary>

Get the peer ip address of the client.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn get client_port(context: Context) -> int>
```

<details>
<summary markdown="span"> details </summary>

Get the peer port of the client.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn get connection_timestamp(context: Context) -> OffsetDateTime>
```

<details>
<summary markdown="span"> details </summary>

Get the timestamp when the client connected to the server.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn get dkim_result(ctx: Context) -> Map>
```

<details>
<summary markdown="span"> details </summary>

Return the DKIM signature verification result in the `ctx()` or
an error if no result is found.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn get elapsed(timestamp: Instant) -> Result<?, Box<EvalAltResult>>
```

<details>
<summary markdown="span"> details </summary>

Return the number of seconds between the current system time and the timestamp.

# Example

```rhai
let now = timestamp();

sleep(10.0);            // sleep for 10 seconds

print(now.elapsed);     // prints 10.???
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn get end(range: Range<int>) -> int
```

<details>
<summary markdown="span"> details </summary>

Return the end of the exclusive range.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn get end(range: RangeInclusive<int>) -> int
```

<details>
<summary markdown="span"> details </summary>

Return the end of the inclusive range.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn get floor(x: float) -> float
```

<details>
<summary markdown="span"> details </summary>

Return the largest whole number less than or equals to the floating-point number.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn get fraction(x: float) -> float
```

<details>
<summary markdown="span"> details </summary>

Return the fractional part of the floating-point number.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn get has_debug_flag(key: PublicKey) -> bool
```

<details>
<summary markdown="span"> details </summary>

A public key may contains a `debug flag`, used for testing purpose.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn get has_dkim_result(ctx: Context) -> bool
```

<details>
<summary markdown="span"> details </summary>

Has the `ctx()` a DKIM signature verification result ?
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn get helo(context: Context) -> String
```

<details>
<summary markdown="span"> details </summary>

Get the domain named introduced by the client.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn get int(x: float) -> float
```

<details>
<summary markdown="span"> details </summary>

Return the integral part of the floating-point number.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn get is_anonymous(fn_ptr: FnPtr) -> bool
```

<details>
<summary markdown="span"> details </summary>

Return `true` if the function is an anonymous function.

# Example

```rhai
let f = |x| x * 2;

print(f.is_anonymous);      // prints true
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn get is_authenticated(context: Context) -> bool
```

<details>
<summary markdown="span"> details </summary>

Has the connection validated the client credentials?
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn get is_empty(blob: Blob) -> bool
```

<details>
<summary markdown="span"> details </summary>

Return true if the BLOB is empty.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn get is_empty(array: Array) -> bool
```

<details>
<summary markdown="span"> details </summary>

Return true if the array is empty.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn get is_empty(range: RangeInclusive<int>) -> bool
```

<details>
<summary markdown="span"> details </summary>

Return true if the range contains no items.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn get is_empty(string: String) -> bool
```

<details>
<summary markdown="span"> details </summary>

Return true if the string is empty.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn get is_empty(range: Range<int>) -> bool
```

<details>
<summary markdown="span"> details </summary>

Return true if the range contains no items.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn get is_even(x: i32) -> bool
```

<details>
<summary markdown="span"> details </summary>

Return true if the number is even.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn get is_even(x: u32) -> bool
```

<details>
<summary markdown="span"> details </summary>

Return true if the number is even.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn get is_even(x: i8) -> bool
```

<details>
<summary markdown="span"> details </summary>

Return true if the number is even.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn get is_even(x: int) -> bool
```

<details>
<summary markdown="span"> details </summary>

Return true if the number is even.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn get is_even(x: u128) -> bool
```

<details>
<summary markdown="span"> details </summary>

Return true if the number is even.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn get is_even(x: i16) -> bool
```

<details>
<summary markdown="span"> details </summary>

Return true if the number is even.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn get is_even(x: u64) -> bool
```

<details>
<summary markdown="span"> details </summary>

Return true if the number is even.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn get is_even(x: u16) -> bool
```

<details>
<summary markdown="span"> details </summary>

Return true if the number is even.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn get is_even(x: i128) -> bool
```

<details>
<summary markdown="span"> details </summary>

Return true if the number is even.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn get is_even(x: u8) -> bool
```

<details>
<summary markdown="span"> details </summary>

Return true if the number is even.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn get is_exclusive(range: Range<int>) -> bool
```

<details>
<summary markdown="span"> details </summary>

Return `true` if the range is exclusive.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn get is_exclusive(range: RangeInclusive<int>) -> bool
```

<details>
<summary markdown="span"> details </summary>

Return `true` if the range is exclusive.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn get is_finite(x: float) -> bool
```

<details>
<summary markdown="span"> details </summary>

Return `true` if the floating-point number is finite.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn get is_inclusive(range: RangeInclusive<int>) -> bool
```

<details>
<summary markdown="span"> details </summary>

Return `true` if the range is inclusive.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn get is_inclusive(range: Range<int>) -> bool
```

<details>
<summary markdown="span"> details </summary>

Return `true` if the range is inclusive.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn get is_infinite(x: float) -> bool
```

<details>
<summary markdown="span"> details </summary>

Return `true` if the floating-point number is infinite.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn get is_nan(x: float) -> bool
```

<details>
<summary markdown="span"> details </summary>

Return `true` if the floating-point number is `NaN` (Not A Number).
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn get is_odd(x: u128) -> bool
```

<details>
<summary markdown="span"> details </summary>

Return true if the number is odd.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn get is_odd(x: u16) -> bool
```

<details>
<summary markdown="span"> details </summary>

Return true if the number is odd.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn get is_odd(x: u64) -> bool
```

<details>
<summary markdown="span"> details </summary>

Return true if the number is odd.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn get is_odd(x: i16) -> bool
```

<details>
<summary markdown="span"> details </summary>

Return true if the number is odd.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn get is_odd(x: i8) -> bool
```

<details>
<summary markdown="span"> details </summary>

Return true if the number is odd.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn get is_odd(x: int) -> bool
```

<details>
<summary markdown="span"> details </summary>

Return true if the number is odd.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn get is_odd(x: u32) -> bool
```

<details>
<summary markdown="span"> details </summary>

Return true if the number is odd.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn get is_odd(x: i32) -> bool
```

<details>
<summary markdown="span"> details </summary>

Return true if the number is odd.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn get is_odd(x: u8) -> bool
```

<details>
<summary markdown="span"> details </summary>

Return true if the number is odd.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn get is_odd(x: i128) -> bool
```

<details>
<summary markdown="span"> details </summary>

Return true if the number is odd.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn get is_secured(context: Context) -> bool
```

<details>
<summary markdown="span"> details </summary>

Is the connection under TLS?
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn get is_zero(x: f32) -> bool
```

<details>
<summary markdown="span"> details </summary>

Return true if the floating-point number is zero.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn get is_zero(x: float) -> bool
```

<details>
<summary markdown="span"> details </summary>

Return true if the floating-point number is zero.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn get is_zero(x: u32) -> bool
```

<details>
<summary markdown="span"> details </summary>

Return true if the number is zero.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn get is_zero(x: int) -> bool
```

<details>
<summary markdown="span"> details </summary>

Return true if the number is zero.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn get is_zero(x: u128) -> bool
```

<details>
<summary markdown="span"> details </summary>

Return true if the number is zero.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn get is_zero(x: u64) -> bool
```

<details>
<summary markdown="span"> details </summary>

Return true if the number is zero.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn get is_zero(x: u16) -> bool
```

<details>
<summary markdown="span"> details </summary>

Return true if the number is zero.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn get is_zero(x: i8) -> bool
```

<details>
<summary markdown="span"> details </summary>

Return true if the number is zero.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn get is_zero(x: i32) -> bool
```

<details>
<summary markdown="span"> details </summary>

Return true if the number is zero.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn get is_zero(x: i128) -> bool
```

<details>
<summary markdown="span"> details </summary>

Return true if the number is zero.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn get is_zero(x: i16) -> bool
```

<details>
<summary markdown="span"> details </summary>

Return true if the number is zero.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn get is_zero(x: u8) -> bool
```

<details>
<summary markdown="span"> details </summary>

Return true if the number is zero.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn get len(blob: Blob) -> int
```

<details>
<summary markdown="span"> details </summary>

Return the length of the BLOB.

# Example

```rhai
let b = blob(10, 0x42);

print(b);           // prints "[4242424242424242 4242]"

print(b.len());     // prints 10
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn get len(string: String) -> int
```

<details>
<summary markdown="span"> details </summary>

Return the length of the string, in number of characters.

# Example

```rhai
let text = "朝には紅顔ありて夕べには白骨となる";

print(text.len);        // prints 17
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn get len(array: Array) -> int
```

<details>
<summary markdown="span"> details </summary>

Number of elements in the array.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn get mail(this: Message) -> String
```

<details>
<summary markdown="span"> details </summary>

Get the message body as a string
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn get mail_from(context: Context) -> SharedObject
```

<details>
<summary markdown="span"> details </summary>

Get the `MailFrom` envelope.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn get mail_timestamp(context: Context) -> OffsetDateTime>
```

<details>
<summary markdown="span"> details </summary>

Get the timestamp when the client started to send the message.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn get message_id(context: Context) -> String
```

<details>
<summary markdown="span"> details </summary>

Get the `message_id`
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn get name(fn_ptr: FnPtr) -> String
```

<details>
<summary markdown="span"> details </summary>

Return the name of the function.

# Example

```rhai
fn double(x) { x * 2 }

let f = Fn("double");

print(f.name);      // prints "double"
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn get rcpt(context: Context) -> SharedObject
```

<details>
<summary markdown="span"> details </summary>

Get the lase element in the `RcptTo` envelope.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn get rcpt_list(context: Context) -> Array>
```

<details>
<summary markdown="span"> details </summary>

Get the `RcptTo` envelope.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn get receiver_policy(record: Record) -> String
```

<details>
<summary markdown="span"> details </summary>


</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn get round(x: float) -> float
```

<details>
<summary markdown="span"> details </summary>

Return the nearest whole number closest to the floating-point number.
Rounds away from zero.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn get sdid(signature: Signature) -> String
```

<details>
<summary markdown="span"> details </summary>

return the `sdid` property of the [`Signature`]
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn get server_address(context: Context) -> String
```

<details>
<summary markdown="span"> details </summary>

Get the server address which served this connection.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn get server_ip(context: Context) -> IpAddr>
```

<details>
<summary markdown="span"> details </summary>

Get the server ip address which served this connection.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn get server_name(context: Context) -> String
```

<details>
<summary markdown="span"> details </summary>

Get server name under which the client has been served.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn get server_port(context: Context) -> int>
```

<details>
<summary markdown="span"> details </summary>

Get the server port which served this connection.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn get start(range: RangeInclusive<int>) -> int
```

<details>
<summary markdown="span"> details </summary>

Return the start of the inclusive range.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn get start(range: Range<int>) -> int
```

<details>
<summary markdown="span"> details </summary>

Return the start of the exclusive range.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn get tag(value: ?) -> int
```

<details>
<summary markdown="span"> details </summary>

Return the _tag_ of a `Dynamic` value.

# Example

```rhai
let x = "hello, world!";

x.tag = 42;

print(x.tag);           // prints 42
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn get type(credentials: Credentials) -> String
```

<details>
<summary markdown="span"> details </summary>

Get the type of the `auth` property of the connection.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn get_all_headers(message: Message) -> Array>
```

<details>
<summary markdown="span"> details </summary>

Return the complete list of headers.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn get_all_headers(message: Message, name: String) -> Array>
```

<details>
<summary markdown="span"> details </summary>

Return a list of headers bearing the `name` given as argument.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn get_all_headers(message: Message, name: SharedObject) -> Array>
```

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn get_bit(value: int, bit: int) -> Result<bool, Box<EvalAltResult>>
```

<details>
<summary markdown="span"> details </summary>

Return `true` if the specified `bit` in the number is set.

If `bit` < 0, position counts from the MSB (Most Significant Bit).

# Example

```rhai
let x = 123456;

print(x.get_bit(5));    // prints false

print(x.get_bit(6));    // prints true

print(x.get_bit(-48));  // prints true on 64-bit
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn get_bits(value: int, range: RangeInclusive<int>) -> Result<int, Box<EvalAltResult>>
```

<details>
<summary markdown="span"> details </summary>

Return an inclusive range of bits in the number as a new number.

# Example

```rhai
let x = 123456;

print(x.get_bits(5..=9));       // print 18
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn get_bits(value: int, range: Range<int>) -> Result<int, Box<EvalAltResult>>
```

<details>
<summary markdown="span"> details </summary>

Return an exclusive range of bits in the number as a new number.

# Example

```rhai
let x = 123456;

print(x.get_bits(5..10));       // print 18
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn get_bits(value: int, start: int, bits: int) -> Result<int, Box<EvalAltResult>>
```

<details>
<summary markdown="span"> details </summary>

Return a portion of bits in the number as a new number.

* If `start` < 0, position counts from the MSB (Most Significant Bit).
* If `bits` ≤ 0, zero is returned.
* If `start` position + `bits` ≥ total number of bits, the bits after the `start` position are returned.

# Example

```rhai
let x = 123456;

print(x.get_bits(5, 8));        // print 18
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn get_dmarc_record(server: Server, domain: String) -> Record>
```

<details>
<summary markdown="span"> details </summary>

Get a valid DMARC record for the domain.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn get_dmarc_record(server: Server, domain: SharedObject) -> Record>
```

<details>
<summary markdown="span"> details </summary>

Get a valid DMARC record for the domain.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn get_fn_metadata_list() -> Array
```

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn get_fn_metadata_list(name: String) -> Array
```

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn get_fn_metadata_list(name: String, params: int) -> Array
```

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn get_header(message: Message, header: String) -> String
```

<details>
<summary markdown="span"> details </summary>

return the value of a header if it exists. Otherwise, returns an empty string.

# Examples

```
X-My-Header: 250 foo
Subject: Unit test are cool

Hello world!
; // .eml ends here

  preq: [
    rule "get_header" || {
      if get_header("X-My-Header") != "250 foo"
        || get_header(identifier("Subject")) != "Unit test are cool" {
        deny();
      } else {
        accept(`${get_header("X-My-Header")} ${get_header(identifier("Subject"))}`);
      }
    }
  ]
}
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn get_header(message: Message, header: SharedObject) -> String
```

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn get_header_untouched(this: Message, name: String) -> Array>
```

<details>
<summary markdown="span"> details </summary>


</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn get_private_keys(server: Server, sdid: String) -> Array
```

<details>
<summary markdown="span"> details </summary>

Get the list of DKIM private keys associated with this sdid
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn get_public_key(server: Server, signature: Signature, on_multiple_key_records: String) -> ?>
```

<details>
<summary markdown="span"> details </summary>

Get the list of public keys associated with this [`Signature`]

The current implementation will make a TXT query on the dns of the signer

`on_multiple_key_records` value can be `first` or `cycle` :
* `first` return the first key found (one element array)
* `cycle` return all the keys found
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn get_root_domain(domain: SharedObject) -> String
```

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn get_root_domain(domain: String) -> String
```

<details>
<summary markdown="span"> details </summary>

Get the root domain (the registrable part)

# Examples

`foo.bar.example.com` => `example.com`
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn handle_dkim_error(err: ?) -> String
```

<details>
<summary markdown="span"> details </summary>

get the dkim status from an error produced by this module
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn has_expired(signature: Signature, epsilon: int) -> bool
```

<details>
<summary markdown="span"> details </summary>

Has the signature expired?

return `true` if the argument are invalid (`epsilon` is negative)
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn has_header(message: Message, header: String) -> bool
```

<details>
<summary markdown="span"> details </summary>

Return a boolean, `true` if a header named `header` exists in the message.

# Examples

```
"X-My-Header: foo\r\n",
"Subject: Unit test are cool\r\n",
"\r\n",
"Hello world!\r\n",

  preq: [
    rule "check if header exists" || {
      if has_header("X-My-Header") && has_header(identifier("Subject")) {
        accept();
      } else {
        deny();
      }
    }
  ]
}
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn has_header(message: Message, header: SharedObject) -> bool
```

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn hostname() -> String
```

<details>
<summary markdown="span"> details </summary>

Get the hostname of the machine.

# Examples

```
  connect: [
    rule "hostname" || {
      accept(`250 ${hostname()}`);
    }
  ]
}
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn hypot(x: float, y: float) -> float
```

<details>
<summary markdown="span"> details </summary>

Return the hypotenuse of a triangle with sides `x` and `y`.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn index_of(string: String, find_string: String) -> int
```

<details>
<summary markdown="span"> details </summary>

Find the specified `character` in the string and return the first index where it is found.
If the `character` is not found, `-1` is returned.

# Example

```rhai
let text = "hello, world! hello, foobar!";

print(text.index_of("ll"));     // prints 2 (first index)

print(text.index_of("xx:));     // prints -1
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn index_of(array: Array, value: ?) -> Result<int, Box<EvalAltResult>>
```

<details>
<summary markdown="span"> details </summary>

Find the first element in the array that equals a particular `value` and return its index.
If no element equals `value`, `-1` is returned.

The operator `==` is used to compare elements with `value` and must be defined,
otherwise `false` is assumed.

# Example

```rhai
let x = [1, 2, 3, 4, 1, 2, 3, 4, 1, 2, 3, 4, 5];

print(x.index_of(4));       // prints 3 (first index)

print(x.index_of(9));       // prints -1

print(x.index_of("foo"));   // prints -1: strings do not equal numbers
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn index_of(string: String, character: char) -> int
```

<details>
<summary markdown="span"> details </summary>

Find the specified `character` in the string and return the first index where it is found.
If the `character` is not found, `-1` is returned.

# Example

```rhai
let text = "hello, world!";

print(text.index_of('l'));      // prints 2 (first index)

print(text.index_of('x'));      // prints -1
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn index_of(array: Array, filter: String) -> Result<int, Box<EvalAltResult>>
```

<details>
<summary markdown="span"> details </summary>

Iterate through all the elements in the array, applying a function named by `filter` to each
element in turn, and return the index of the first element that returns `true`.
If no element returns `true`, `-1` is returned.

# Function Parameters

A function with the same name as the value of `filter` must exist taking these parameters:

* `element`: copy of array element
* `index` _(optional)_: current index in the array

# Example

```rhai
fn is_special(x) { x > 3 }

fn is_dumb(x) { x > 8 }

let x = [1, 2, 3, 4, 1, 2, 3, 4, 1, 2, 3, 4, 5];

print(x.index_of("is_special"));    // prints 3

print(x.index_of("is_dumb"));       // prints -1
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn index_of(array: Array, filter: FnPtr) -> Result<int, Box<EvalAltResult>>
```

<details>
<summary markdown="span"> details </summary>

Iterate through all the elements in the array, applying a `filter` function to each element
in turn, and return the index of the first element that returns `true`.
If no element returns `true`, `-1` is returned.

# Function Parameters

* `element`: copy of array element
* `index` _(optional)_: current index in the array

# Example

```rhai
let x = [1, 2, 3, 4, 1, 2, 3, 4, 1, 2, 3, 4, 5];

print(x.index_of(|v| v > 3));           // prints 3: 4 > 3

print(x.index_of(|v| v > 8));           // prints -1: nothing is > 8

print(x.index_of(|v, i| v * i > 20));   // prints 7: 4 * 7 > 20
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn index_of(array: Array, value: ?, start: int) -> Result<int, Box<EvalAltResult>>
```

<details>
<summary markdown="span"> details </summary>

Find the first element in the array, starting from a particular `start` position, that
equals a particular `value` and return its index. If no element equals `value`, `-1` is returned.

* If `start` < 0, position counts from the end of the array (`-1` is the last element).
* If `start` < -length of array, position counts from the beginning of the array.
* If `start` ≥ length of array, `-1` is returned.

The operator `==` is used to compare elements with `value` and must be defined,
otherwise `false` is assumed.

# Example

```rhai
let x = [1, 2, 3, 4, 1, 2, 3, 4, 1, 2, 3, 4, 5];

print(x.index_of(4, 2));        // prints 3

print(x.index_of(4, 5));        // prints 7

print(x.index_of(4, 15));       // prints -1: nothing found past end of array

print(x.index_of(4, -5));       // prints 11: -5 = start from index 8

print(x.index_of(9, 1));        // prints -1: nothing equals 9

print(x.index_of("foo", 1));    // prints -1: strings do not equal numbers
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn index_of(array: Array, filter: String, start: int) -> Result<int, Box<EvalAltResult>>
```

<details>
<summary markdown="span"> details </summary>

Iterate through all the elements in the array, starting from a particular `start` position,
applying a function named by `filter` to each element in turn, and return the index of the
first element that returns `true`. If no element returns `true`, `-1` is returned.

* If `start` < 0, position counts from the end of the array (`-1` is the last element).
* If `start` < -length of array, position counts from the beginning of the array.
* If `start` ≥ length of array, `-1` is returned.

# Function Parameters

A function with the same name as the value of `filter` must exist taking these parameters:

* `element`: copy of array element
* `index` _(optional)_: current index in the array

# Example

```rhai
fn plural(x) { x > 1 }

fn singular(x) { x < 2 }

fn screen(x, i) { x * i > 20 }

let x = [1, 2, 3, 4, 1, 2, 3, 4, 1, 2, 3, 4, 5];

print(x.index_of("plural", 3));     // prints 5: 2 > 1

print(x.index_of("singular", 9));   // prints -1: nothing < 2 past index 9

print(x.index_of("plural", 15));    // prints -1: nothing found past end of array

print(x.index_of("plural", -5));    // prints 9: -5 = start from index 8

print(x.index_of("plural", -99));   // prints 1: -99 = start from beginning

print(x.index_of("screen", 8));     // prints 10: 3 * 10 > 20
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn index_of(string: String, find_string: String, start: int) -> int
```

<details>
<summary markdown="span"> details </summary>

Find the specified sub-string in the string, starting from the specified `start` position,
and return the first index where it is found.
If the sub-string is not found, `-1` is returned.

* If `start` < 0, position counts from the end of the string (`-1` is the last character).
* If `start` < -length of string, position counts from the beginning of the string.
* If `start` ≥ length of string, `-1` is returned.

# Example

```rhai
let text = "hello, world! hello, foobar!";

print(text.index_of("ll", 5));      // prints 16 (first index after 5)

print(text.index_of("ll", -15));    // prints 16

print(text.index_of("xx", 0));      // prints -1
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn index_of(string: String, character: char, start: int) -> int
```

<details>
<summary markdown="span"> details </summary>

Find the specified `character` in the string, starting from the specified `start` position,
and return the first index where it is found.
If the `character` is not found, `-1` is returned.

* If `start` < 0, position counts from the end of the string (`-1` is the last character).
* If `start` < -length of string, position counts from the beginning of the string.
* If `start` ≥ length of string, `-1` is returned.

# Example

```rhai
let text = "hello, world!";

print(text.index_of('l', 5));       // prints 10 (first index after 5)

print(text.index_of('o', -7));      // prints 8

print(text.index_of('x', 0));       // prints -1
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn index_of(array: Array, filter: FnPtr, start: int) -> Result<int, Box<EvalAltResult>>
```

<details>
<summary markdown="span"> details </summary>

Iterate through all the elements in the array, starting from a particular `start` position,
applying a `filter` function to each element in turn, and return the index of the first
element that returns `true`. If no element returns `true`, `-1` is returned.

* If `start` < 0, position counts from the end of the array (`-1` is the last element).
* If `start` < -length of array, position counts from the beginning of the array.
* If `start` ≥ length of array, `-1` is returned.

# Function Parameters

* `element`: copy of array element
* `index` _(optional)_: current index in the array

# Example

```rhai
let x = [1, 2, 3, 4, 1, 2, 3, 4, 1, 2, 3, 4, 5];

print(x.index_of(|v| v > 1, 3));    // prints 5: 2 > 1

print(x.index_of(|v| v < 2, 9));    // prints -1: nothing < 2 past index 9

print(x.index_of(|v| v > 1, 15));   // prints -1: nothing found past end of array

print(x.index_of(|v| v > 1, -5));   // prints 9: -5 = start from index 8

print(x.index_of(|v| v > 1, -99));  // prints 1: -99 = start from beginning

print(x.index_of(|v, i| v * i > 20, 8));    // prints 10: 3 * 10 > 20
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn info(code: SharedObject) -> Status
```

<details>
<summary markdown="span"> details </summary>

Return a [`Status::Info`] with `code`

# Errors

* `code` is not a valid code
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn info(code: String) -> Status
```

<details>
<summary markdown="span"> details </summary>

Return a [`Status::Info`] with `code`

# Errors

* `code` is not a valid code
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn insert(array: Array, index: int, item: ?)
```

<details>
<summary markdown="span"> details </summary>

Add a new element into the array at a particular `index` position.

* If `index` < 0, position counts from the end of the array (`-1` is the last element).
* If `index` < -length of array, the element is added to the beginning of the array.
* If `index` ≥ length of array, the element is appended to the end of the array.

# Example

```rhai
let x = [1, 2, 3];

x.insert(0, "hello");

x.insert(2, true);

x.insert(-2, 42);

print(x);       // prints ["hello", 1, true, 2, 42, 3]
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn insert(blob: Blob, index: int, value: int)
```

<details>
<summary markdown="span"> details </summary>

Add a byte `value` to the BLOB at a particular `index` position.

* If `index` < 0, position counts from the end of the BLOB (`-1` is the last byte).
* If `index` < -length of BLOB, the byte value is added to the beginning of the BLOB.
* If `index` ≥ length of BLOB, the byte value is appended to the end of the BLOB.

Only the lower 8 bits of the `value` are used; all other bits are ignored.

# Example

```rhai
let b = blob(5, 0x42);

b.insert(2, 0x18);

print(b);       // prints "[4242184242]"
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn int(x: float) -> float
```

<details>
<summary markdown="span"> details </summary>

Return the integral part of the floating-point number.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn is_anonymous(fn_ptr: FnPtr) -> bool
```

<details>
<summary markdown="span"> details </summary>

Return `true` if the function is an anonymous function.

# Example

```rhai
let f = |x| x * 2;

print(f.is_anonymous);      // prints true
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn is_empty(range: Range<int>) -> bool
```

<details>
<summary markdown="span"> details </summary>

Return true if the range contains no items.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn is_empty(array: Array) -> bool
```

<details>
<summary markdown="span"> details </summary>

Return true if the array is empty.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn is_empty(range: RangeInclusive<int>) -> bool
```

<details>
<summary markdown="span"> details </summary>

Return true if the range contains no items.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn is_empty(blob: Blob) -> bool
```

<details>
<summary markdown="span"> details </summary>

Return true if the BLOB is empty.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn is_empty(map: Map) -> bool
```

<details>
<summary markdown="span"> details </summary>

Return true if the map is empty.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn is_empty(string: String) -> bool
```

<details>
<summary markdown="span"> details </summary>

Return true if the string is empty.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn is_even(x: i8) -> bool
```

<details>
<summary markdown="span"> details </summary>

Return true if the number is even.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn is_even(x: u16) -> bool
```

<details>
<summary markdown="span"> details </summary>

Return true if the number is even.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn is_even(x: u32) -> bool
```

<details>
<summary markdown="span"> details </summary>

Return true if the number is even.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn is_even(x: u128) -> bool
```

<details>
<summary markdown="span"> details </summary>

Return true if the number is even.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn is_even(x: u8) -> bool
```

<details>
<summary markdown="span"> details </summary>

Return true if the number is even.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn is_even(x: int) -> bool
```

<details>
<summary markdown="span"> details </summary>

Return true if the number is even.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn is_even(x: i128) -> bool
```

<details>
<summary markdown="span"> details </summary>

Return true if the number is even.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn is_even(x: i32) -> bool
```

<details>
<summary markdown="span"> details </summary>

Return true if the number is even.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn is_even(x: u64) -> bool
```

<details>
<summary markdown="span"> details </summary>

Return true if the number is even.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn is_even(x: i16) -> bool
```

<details>
<summary markdown="span"> details </summary>

Return true if the number is even.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn is_exclusive(range: RangeInclusive<int>) -> bool
```

<details>
<summary markdown="span"> details </summary>

Return `true` if the range is exclusive.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn is_exclusive(range: Range<int>) -> bool
```

<details>
<summary markdown="span"> details </summary>

Return `true` if the range is exclusive.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn is_finite(x: float) -> bool
```

<details>
<summary markdown="span"> details </summary>

Return `true` if the floating-point number is finite.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn is_inclusive(range: Range<int>) -> bool
```

<details>
<summary markdown="span"> details </summary>

Return `true` if the range is inclusive.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn is_inclusive(range: RangeInclusive<int>) -> bool
```

<details>
<summary markdown="span"> details </summary>

Return `true` if the range is inclusive.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn is_infinite(x: float) -> bool
```

<details>
<summary markdown="span"> details </summary>

Return `true` if the floating-point number is infinite.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn is_nan(x: float) -> bool
```

<details>
<summary markdown="span"> details </summary>

Return `true` if the floating-point number is `NaN` (Not A Number).
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn is_odd(x: u32) -> bool
```

<details>
<summary markdown="span"> details </summary>

Return true if the number is odd.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn is_odd(x: u128) -> bool
```

<details>
<summary markdown="span"> details </summary>

Return true if the number is odd.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn is_odd(x: i32) -> bool
```

<details>
<summary markdown="span"> details </summary>

Return true if the number is odd.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn is_odd(x: u64) -> bool
```

<details>
<summary markdown="span"> details </summary>

Return true if the number is odd.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn is_odd(x: int) -> bool
```

<details>
<summary markdown="span"> details </summary>

Return true if the number is odd.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn is_odd(x: i8) -> bool
```

<details>
<summary markdown="span"> details </summary>

Return true if the number is odd.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn is_odd(x: i128) -> bool
```

<details>
<summary markdown="span"> details </summary>

Return true if the number is odd.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn is_odd(x: u8) -> bool
```

<details>
<summary markdown="span"> details </summary>

Return true if the number is odd.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn is_odd(x: u16) -> bool
```

<details>
<summary markdown="span"> details </summary>

Return true if the number is odd.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn is_odd(x: i16) -> bool
```

<details>
<summary markdown="span"> details </summary>

Return true if the number is odd.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn is_zero(x: u128) -> bool
```

<details>
<summary markdown="span"> details </summary>

Return true if the number is zero.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn is_zero(x: i128) -> bool
```

<details>
<summary markdown="span"> details </summary>

Return true if the number is zero.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn is_zero(x: i8) -> bool
```

<details>
<summary markdown="span"> details </summary>

Return true if the number is zero.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn is_zero(x: u16) -> bool
```

<details>
<summary markdown="span"> details </summary>

Return true if the number is zero.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn is_zero(x: u64) -> bool
```

<details>
<summary markdown="span"> details </summary>

Return true if the number is zero.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn is_zero(x: i32) -> bool
```

<details>
<summary markdown="span"> details </summary>

Return true if the number is zero.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn is_zero(x: int) -> bool
```

<details>
<summary markdown="span"> details </summary>

Return true if the number is zero.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn is_zero(x: i16) -> bool
```

<details>
<summary markdown="span"> details </summary>

Return true if the number is zero.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn is_zero(x: f32) -> bool
```

<details>
<summary markdown="span"> details </summary>

Return true if the floating-point number is zero.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn is_zero(x: u32) -> bool
```

<details>
<summary markdown="span"> details </summary>

Return true if the number is zero.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn is_zero(x: float) -> bool
```

<details>
<summary markdown="span"> details </summary>

Return true if the floating-point number is zero.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn is_zero(x: u8) -> bool
```

<details>
<summary markdown="span"> details </summary>

Return true if the number is zero.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn keys(map: Map) -> Array
```

<details>
<summary markdown="span"> details </summary>

Return an array with all the property names in the object map.

# Example

```rhai
let m = #{a:1, b:2, c:3};

print(m.keys());        // prints ["a", "b", "c"]
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn len(blob: Blob) -> int
```

<details>
<summary markdown="span"> details </summary>

Return the length of the BLOB.

# Example

```rhai
let b = blob(10, 0x42);

print(b);           // prints "[4242424242424242 4242]"

print(b.len());     // prints 10
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn len(string: String) -> int
```

<details>
<summary markdown="span"> details </summary>

Return the length of the string, in number of characters.

# Example

```rhai
let text = "朝には紅顔ありて夕べには白骨となる";

print(text.len);        // prints 17
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn len(map: Map) -> int
```

<details>
<summary markdown="span"> details </summary>

Return the number of properties in the object map.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn len(array: Array) -> int
```

<details>
<summary markdown="span"> details </summary>

Number of elements in the array.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn ln(x: float) -> float
```

<details>
<summary markdown="span"> details </summary>

Return the natural log of the floating-point number.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn log(x: float) -> float
```

<details>
<summary markdown="span"> details </summary>

Return the log of the floating-point number with base 10.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn log(level: SharedObject, message: SharedObject)
```

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn log(x: float, base: float) -> float
```

<details>
<summary markdown="span"> details </summary>

Return the log of the floating-point number with `base`.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn log(level: SharedObject, message: String)
```

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn log(level: String, message: String)
```

<details>
<summary markdown="span"> details </summary>

# Examples

```
  connect: [
    action "log on connection (str/str)" || {
      log("info", `[${date()}/${time()}] client=${client_ip()}`);
    },
    action "log on connection (str/obj)" || {
      log("error", identifier("Ehllo world!"));
    },
    action "log on connection (obj/obj)" || {
      const level = "trace";
      const message = "connection established";

      log(identifier(level), identifier(message));
    },
    action "log on connection (obj/str)" || {
      const level = "warn";

      log(identifier(level), "I love vsl!");
    },
  ],
}
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn log(level: String, message: SharedObject)
```

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn lookup(server: Server, name: String) -> Array>
```

<details>
<summary markdown="span"> details </summary>

Perform a dns lookup using the root dns.

# Errors

* Root resolver was not found.
* Lookup failed.

# Examples

```
  preq: [
    action "lookup recipients" || {
      let domain = "gmail.com";
      let ips = lookup(domain);

      print(`ips found for ${domain}`);
      for ip in ips { print(`- ${ip}`); }
    },
  ],
}
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn lookup(server: Server, name: SharedObject) -> Array>
```

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn maildir(context: Context, rcpt: String) -> ()
```

<details>
<summary markdown="span"> details </summary>

Set the delivery method to [`Transfer::Maildir`] for a single recipient.

# Examples

```
  rcpt: [
    action "setup maildir" || {
        const doe = address("doe@example.com");
        add_rcpt_envelop(doe);
        add_rcpt_envelop("a@example.com");
        maildir(doe);
        maildir("a@example.com");
    },
  ],
}

```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn maildir(context: Context, rcpt: SharedObject) -> ()
```

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn maildir_all(context: Context) -> ()
```

<details>
<summary markdown="span"> details </summary>

Set the delivery method to [`Transfer::Maildir`] for all recipients.

# Examples

```
  rcpt: [
    action "setup maildir" || {
        const doe = address("doe@example.com");
        add_rcpt_envelop(doe);
        add_rcpt_envelop("a@example.com");
        maildir_all();
    },
  ],
}

```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn make_lower(string: String)
```

<details>
<summary markdown="span"> details </summary>

Convert the string to all lower-case.

# Example

```rhai
let text = "HELLO, WORLD!"

text.make_lower();

print(text);        // prints "hello, world!";
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn make_lower(character: char)
```

<details>
<summary markdown="span"> details </summary>

Convert the character to lower-case.

# Example

```rhai
let ch = 'A';

ch.make_lower();

print(ch);          // prints 'a'
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn make_upper(character: char)
```

<details>
<summary markdown="span"> details </summary>

Convert the character to upper-case.

# Example

```rhai
let ch = 'a';

ch.make_upper();

print(ch);          // prints 'A'
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn make_upper(string: String)
```

<details>
<summary markdown="span"> details </summary>

Convert the string to all upper-case.

# Example

```rhai
let text = "hello, world!"

text.make_upper();

print(text);        // prints "HELLO, WORLD!";
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn map(array: Array, mapper: FnPtr) -> Result<Array, Box<EvalAltResult>>
```

<details>
<summary markdown="span"> details </summary>

Iterate through all the elements in the array, applying a `mapper` function to each element
in turn, and return the results as a new array.

# Function Parameters

* `element`: copy of array element
* `index` _(optional)_: current index in the array

# Example

```rhai
let x = [1, 2, 3, 4, 5];

let y = x.map(|v| v * v);

print(y);       // prints "[1, 4, 9, 16, 25]"

let y = x.map(|v, i| v * i);

print(y);       // prints "[0, 2, 6, 12, 20]"
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn map(array: Array, mapper: String) -> Result<Array, Box<EvalAltResult>>
```

<details>
<summary markdown="span"> details </summary>

Iterate through all the elements in the array, applying a function named by `mapper` to each
element in turn, and return the results as a new array.

# Function Parameters

A function with the same name as the value of `mapper` must exist taking these parameters:

* `element`: copy of array element
* `index` _(optional)_: current index in the array

# Example

```rhai
fn square(x) { x * x }

fn multiply(x, i) { x * i }

let x = [1, 2, 3, 4, 5];

let y = x.map("square");

print(y);       // prints "[1, 4, 9, 16, 25]"

let y = x.map("multiply");

print(y);       // prints "[0, 2, 6, 12, 20]"
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn mbox(context: Context, rcpt: SharedObject) -> ()
```

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn mbox(context: Context, rcpt: String) -> ()
```

<details>
<summary markdown="span"> details </summary>

Set the delivery method to [`Transfer::Mbox`] for a single recipient.

# Examples

```
  rcpt: [
    action "setup mbox" || {
        const doe = address("doe@example.com");
        add_rcpt_envelop(doe);
        add_rcpt_envelop("a@example.com");
        mbox(doe);
        mbox("a@example.com");
    },
  ],
}

```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn mbox_all(context: Context) -> ()
```

<details>
<summary markdown="span"> details </summary>

Set the delivery method to [`Transfer::Mbox`] for all recipients.

# Examples

```
  rcpt: [
    action "setup mbox" || {
        const doe = address("doe@example.com");
        add_rcpt_envelop(doe);
        add_rcpt_envelop("a@example.com");
        mbox_all();
    },
  ],
}

```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn mixin(map: Map, map2: Map)
```

<details>
<summary markdown="span"> details </summary>

Add all property values of another object map into the object map.
Existing property values of the same names are replaced.

# Example

```rhai
let m = #{a:1, b:2, c:3};
let n = #{a: 42, d:0};

m.mixin(n);

print(m);       // prints "#{a:42, b:2, c:3, d:0}"
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn name(fn_ptr: FnPtr) -> String
```

<details>
<summary markdown="span"> details </summary>

Return the name of the function.

# Example

```rhai
fn double(x) { x * 2 }

let f = Fn("double");

print(f.name);      // prints "double"
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn next() -> Status
```

<details>
<summary markdown="span"> details </summary>

Return a [`Status::Next`]
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn pad(string: String, len: int, character: char) -> Result<(), Box<EvalAltResult>>
```

<details>
<summary markdown="span"> details </summary>

Pad the string to at least the specified number of characters with the specified `character`.

If `len` ≤ length of string, no padding is done.

# Example

```rhai
let text = "hello";

text.pad(8, '!');

print(text);        // prints "hello!!!"

text.pad(5, '*');

print(text);        // prints "hello!!!"
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn pad(array: Array, len: int, item: ?) -> Result<(), Box<EvalAltResult>>
```

<details>
<summary markdown="span"> details </summary>

Pad the array to at least the specified length with copies of a specified element.

If `len` ≤ length of array, no padding is done.

# Example

```rhai
let x = [1, 2, 3];

x.pad(5, 42);

print(x);       // prints "[1, 2, 3, 42, 42]"

x.pad(3, 123);

print(x);       // prints "[1, 2, 3, 42, 42]"
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn pad(blob: Blob, len: int, value: int) -> Result<(), Box<EvalAltResult>>
```

<details>
<summary markdown="span"> details </summary>

Pad the BLOB to at least the specified length with copies of a specified byte `value`.

If `len` ≤ length of BLOB, no padding is done.

Only the lower 8 bits of the `value` are used; all other bits are ignored.

# Example

```rhai
let b = blob(3, 0x42);

b.pad(5, 0x18)

print(b);               // prints "[4242421818]"

b.pad(3, 0xab)

print(b);               // prints "[4242421818]"
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn pad(string: String, len: int, padding: String) -> Result<(), Box<EvalAltResult>>
```

<details>
<summary markdown="span"> details </summary>

Pad the string to at least the specified number of characters with the specified string.

If `len` ≤ length of string, no padding is done.

# Example

```rhai
let text = "hello";

text.pad(10, "(!)");

print(text);        // prints "hello(!)(!)"

text.pad(8, '***');

print(text);        // prints "hello(!)(!)"
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn parse_be_float(blob: Blob, range: RangeInclusive<int>) -> float
```

<details>
<summary markdown="span"> details </summary>

Parse the bytes within an inclusive `range` in the BLOB as a `FLOAT`
in big-endian byte order.

* If number of bytes in `range` < number of bytes for `FLOAT`, zeros are padded.
* If number of bytes in `range` > number of bytes for `FLOAT`, extra bytes are ignored.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn parse_be_float(blob: Blob, range: Range<int>) -> float
```

<details>
<summary markdown="span"> details </summary>

Parse the bytes within an exclusive `range` in the BLOB as a `FLOAT`
in big-endian byte order.

* If number of bytes in `range` < number of bytes for `FLOAT`, zeros are padded.
* If number of bytes in `range` > number of bytes for `FLOAT`, extra bytes are ignored.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn parse_be_float(blob: Blob, start: int, len: int) -> float
```

<details>
<summary markdown="span"> details </summary>

Parse the bytes beginning at the `start` position in the BLOB as a `FLOAT`
in big-endian byte order.

* If `start` < 0, position counts from the end of the BLOB (`-1` is the last byte).
* If `start` < -length of BLOB, position counts from the beginning of the BLOB.
* If `start` ≥ length of BLOB, zero is returned.
* If `len` ≤ 0, zero is returned.
* If `start` position + `len` ≥ length of BLOB, entire portion of the BLOB after the `start` position is parsed.

* If number of bytes in range < number of bytes for `FLOAT`, zeros are padded.
* If number of bytes in range > number of bytes for `FLOAT`, extra bytes are ignored.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn parse_be_int(blob: Blob, range: Range<int>) -> int
```

<details>
<summary markdown="span"> details </summary>

Parse the bytes within an exclusive `range` in the BLOB as an `INT`
in big-endian byte order.

* If number of bytes in `range` < number of bytes for `INT`, zeros are padded.
* If number of bytes in `range` > number of bytes for `INT`, extra bytes are ignored.

```rhai
let b = blob();

b += 1; b += 2; b += 3; b += 4; b += 5;

let x = b.parse_be_int(1..3);   // parse two bytes

print(x.to_hex());              // prints "02030000...00"
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn parse_be_int(blob: Blob, range: RangeInclusive<int>) -> int
```

<details>
<summary markdown="span"> details </summary>

Parse the bytes within an inclusive `range` in the BLOB as an `INT`
in big-endian byte order.

* If number of bytes in `range` < number of bytes for `INT`, zeros are padded.
* If number of bytes in `range` > number of bytes for `INT`, extra bytes are ignored.

```rhai
let b = blob();

b += 1; b += 2; b += 3; b += 4; b += 5;

let x = b.parse_be_int(1..=3);  // parse three bytes

print(x.to_hex());              // prints "0203040000...00"
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn parse_be_int(blob: Blob, start: int, len: int) -> int
```

<details>
<summary markdown="span"> details </summary>

Parse the bytes beginning at the `start` position in the BLOB as an `INT`
in big-endian byte order.

* If `start` < 0, position counts from the end of the BLOB (`-1` is the last byte).
* If `start` < -length of BLOB, position counts from the beginning of the BLOB.
* If `start` ≥ length of BLOB, zero is returned.
* If `len` ≤ 0, zero is returned.
* If `start` position + `len` ≥ length of BLOB, entire portion of the BLOB after the `start` position is parsed.

* If number of bytes in range < number of bytes for `INT`, zeros are padded.
* If number of bytes in range > number of bytes for `INT`, extra bytes are ignored.

```rhai
let b = blob();

b += 1; b += 2; b += 3; b += 4; b += 5;

let x = b.parse_be_int(1, 2);

print(x.to_hex());      // prints "02030000...00"
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn parse_float(string: String) -> Result<float, Box<EvalAltResult>>
```

<details>
<summary markdown="span"> details </summary>

Parse a string into a floating-point number.

# Example

```rhai
let x = parse_int("123.456");

print(x);       // prints 123.456
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn parse_int(string: String) -> Result<int, Box<EvalAltResult>>
```

<details>
<summary markdown="span"> details </summary>

Parse a string into an integer number.

# Example

```rhai
let x = parse_int("123");

print(x);       // prints 123
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn parse_int(string: String, radix: int) -> Result<int, Box<EvalAltResult>>
```

<details>
<summary markdown="span"> details </summary>

Parse a string into an integer number of the specified `radix`.

`radix` must be between 2 and 36.

# Example

```rhai
let x = parse_int("123");

print(x);       // prints 123

let y = parse_int("123abc", 16);

print(y);       // prints 1194684 (0x123abc)
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn parse_json(json: String) -> Result<?, Box<EvalAltResult>>
```

<details>
<summary markdown="span"> details </summary>

Parse a JSON string into a value.

# Example

```rhai
let m = parse_json(`{"a":1, "b":2, "c":3}`);

print(m);       // prints #{"a":1, "b":2, "c":3}
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn parse_le_float(blob: Blob, range: Range<int>) -> float
```

<details>
<summary markdown="span"> details </summary>

Parse the bytes within an exclusive `range` in the BLOB as a `FLOAT`
in little-endian byte order.

* If number of bytes in `range` < number of bytes for `FLOAT`, zeros are padded.
* If number of bytes in `range` > number of bytes for `FLOAT`, extra bytes are ignored.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn parse_le_float(blob: Blob, range: RangeInclusive<int>) -> float
```

<details>
<summary markdown="span"> details </summary>

Parse the bytes within an inclusive `range` in the BLOB as a `FLOAT`
in little-endian byte order.

* If number of bytes in `range` < number of bytes for `FLOAT`, zeros are padded.
* If number of bytes in `range` > number of bytes for `FLOAT`, extra bytes are ignored.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn parse_le_float(blob: Blob, start: int, len: int) -> float
```

<details>
<summary markdown="span"> details </summary>

Parse the bytes beginning at the `start` position in the BLOB as a `FLOAT`
in little-endian byte order.

* If `start` < 0, position counts from the end of the BLOB (`-1` is the last byte).
* If `start` < -length of BLOB, position counts from the beginning of the BLOB.
* If `start` ≥ length of BLOB, zero is returned.
* If `len` ≤ 0, zero is returned.
* If `start` position + `len` ≥ length of BLOB, entire portion of the BLOB after the `start` position is parsed.

* If number of bytes in range < number of bytes for `FLOAT`, zeros are padded.
* If number of bytes in range > number of bytes for `FLOAT`, extra bytes are ignored.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn parse_le_int(blob: Blob, range: Range<int>) -> int
```

<details>
<summary markdown="span"> details </summary>

Parse the bytes within an exclusive `range` in the BLOB as an `INT`
in little-endian byte order.

* If number of bytes in `range` < number of bytes for `INT`, zeros are padded.
* If number of bytes in `range` > number of bytes for `INT`, extra bytes are ignored.

```rhai
let b = blob();

b += 1; b += 2; b += 3; b += 4; b += 5;

let x = b.parse_le_int(1..3);   // parse two bytes

print(x.to_hex());              // prints "0302"
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn parse_le_int(blob: Blob, range: RangeInclusive<int>) -> int
```

<details>
<summary markdown="span"> details </summary>

Parse the bytes within an inclusive `range` in the BLOB as an `INT`
in little-endian byte order.

* If number of bytes in `range` < number of bytes for `INT`, zeros are padded.
* If number of bytes in `range` > number of bytes for `INT`, extra bytes are ignored.

```rhai
let b = blob();

b += 1; b += 2; b += 3; b += 4; b += 5;

let x = b.parse_le_int(1..=3);  // parse three bytes

print(x.to_hex());              // prints "040302"
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn parse_le_int(blob: Blob, start: int, len: int) -> int
```

<details>
<summary markdown="span"> details </summary>

Parse the bytes beginning at the `start` position in the BLOB as an `INT`
in little-endian byte order.

* If `start` < 0, position counts from the end of the BLOB (`-1` is the last byte).
* If `start` < -length of BLOB, position counts from the beginning of the BLOB.
* If `start` ≥ length of BLOB, zero is returned.
* If `len` ≤ 0, zero is returned.
* If `start` position + `len` ≥ length of BLOB, entire portion of the BLOB after the `start` position is parsed.

* If number of bytes in range < number of bytes for `INT`, zeros are padded.
* If number of bytes in range > number of bytes for `INT`, extra bytes are ignored.

```rhai
let b = blob();

b += 1; b += 2; b += 3; b += 4; b += 5;

let x = b.parse_le_int(1, 2);

print(x.to_hex());      // prints "0302"
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn parse_rfc5322_from(message: Message) -> SharedObject
```

<details>
<summary markdown="span"> details </summary>

Get the address of the sender in the message body, also known as RFC5322.From
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn parse_signature(input: String) -> Signature
```

<details>
<summary markdown="span"> details </summary>

create a [`Signature`] from a `DKIM-Signature` header
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn pop(array: Array) -> ?
```

<details>
<summary markdown="span"> details </summary>

Remove the last element from the array and return it.

If the array is empty, `()` is returned.

# Example

```rhai
let x = [1, 2, 3];

print(x.pop());     // prints 3

print(x);           // prints "[1, 2]"
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn pop(string: String) -> ?
```

<details>
<summary markdown="span"> details </summary>

Remove the last character from the string and return it.

If the string is empty, `()` is returned.

# Example

```rhai
let text = "hello, world!";

print(text.pop());      // prints '!'

print(text);            // prints "hello, world"
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn pop(blob: Blob) -> int
```

<details>
<summary markdown="span"> details </summary>

Remove the last byte from the BLOB and return it.

If the BLOB is empty, zero is returned.

# Example

```rhai
let b = blob();

b += 1; b += 2; b += 3; b += 4; b += 5;

print(b.pop());         // prints 5

print(b);               // prints "[01020304]"
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn pop(string: String, len: int) -> String
```

<details>
<summary markdown="span"> details </summary>

Remove a specified number of characters from the end of the string and return it as a
new string.

* If `len` ≤ 0, the string is not modified and an empty string is returned.
* If `len` ≥ length of string, the string is cleared and the entire string returned.

# Example

```rhai
let text = "hello, world!";

print(text.pop(4));     // prints "rld!"

print(text);            // prints "hello, wo"
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn prepend_header(message: Message, header: String, value: String) -> ()
```

<details>
<summary markdown="span"> details </summary>

Add a header **at the beginning** of the Header section of the message.

# Examples

```
"X-My-Header: 250 foo\r\n",
"Subject: Unit test are cool\r\n",
"\r\n",
"Hello world!\r\n",

  preq: [
    rule "prepend_header" || {
      prepend_header("X-My-Header-2", "bar");
      prepend_header("X-My-Header-3", identifier("baz"));
    }
  ]
}
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn prepend_header(message: Message, header: String, value: SharedObject) -> ()
```

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn print() -> String
```

<details>
<summary markdown="span"> details </summary>

Return the empty string.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn print(map: Map) -> String
```

<details>
<summary markdown="span"> details </summary>

Convert the object map into a string.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn print(string: String) -> String
```

<details>
<summary markdown="span"> details </summary>

Return the `string`.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn print(number: f32) -> String
```

<details>
<summary markdown="span"> details </summary>

Convert the value of `number` into a string.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn print(character: char) -> String
```

<details>
<summary markdown="span"> details </summary>

Return the character into a string.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn print(item: ?) -> String
```

<details>
<summary markdown="span"> details </summary>

Convert the value of the `item` into a string.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn print(array: Array) -> String
```

<details>
<summary markdown="span"> details </summary>

Convert the array into a string.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn print(value: bool) -> String
```

<details>
<summary markdown="span"> details </summary>

Return the boolean value into a string.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn print(number: float) -> String
```

<details>
<summary markdown="span"> details </summary>

Convert the value of `number` into a string.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn print(unit: ()) -> String
```

<details>
<summary markdown="span"> details </summary>

Return the empty string.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn push(array: Array, item: ?)
```

<details>
<summary markdown="span"> details </summary>

Add a new element, which is not another array, to the end of the array.

If `item` is `Array`, then `append` is more specific and will be called instead.

# Example

```rhai
let x = [1, 2, 3];

x.push("hello");

print(x);       // prints [1, 2, 3, "hello"]
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn push(blob: Blob, value: int)
```

<details>
<summary markdown="span"> details </summary>

Add a new byte `value` to the end of the BLOB.

Only the lower 8 bits of the `value` are used; all other bits are ignored.

# Example

```rhai
let b = blob();

b.push(0x42);

print(b);       // prints "[42]"
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn quarantine(queue: SharedObject) -> Status
```

<details>
<summary markdown="span"> details </summary>

Return a [`Status::Quarantine`] with `queue`

# Errors

* a mutex is poisoned
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn quarantine(queue: String) -> Status
```

<details>
<summary markdown="span"> details </summary>

Return a [`Status::Quarantine`] with `queue`

# Errors

* a mutex is poisoned
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn range(range: Range<float>, step: float) -> Iterator<float>
```

<details>
<summary markdown="span"> details </summary>

Return an iterator over an exclusive range, each iteration increasing by `step`.

If `range` is reversed and `step` < 0, iteration goes backwards.

Otherwise, if `range` is empty, an empty iterator is returned.

# Example

```rhai
// prints all values from 8 to 17 in steps of 3
for n in range(8..18, 3) {
    print(n);
}

// prints all values down from 18 to 9 in steps of -3
for n in range(18..8, -3) {
    print(n);
}
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn range(range: Range<u128>, step: u128) -> Iterator<u128>
```

<details>
<summary markdown="span"> details </summary>

Return an iterator over an exclusive range, each iteration increasing by `step`.

If `range` is reversed and `step` < 0, iteration goes backwards.

Otherwise, if `range` is empty, an empty iterator is returned.

# Example

```rhai
// prints all values from 8 to 17 in steps of 3
for n in range(8..18, 3) {
    print(n);
}

// prints all values down from 18 to 9 in steps of -3
for n in range(18..8, -3) {
    print(n);
}
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn range(range: Range<i8>, step: i8) -> Iterator<i8>
```

<details>
<summary markdown="span"> details </summary>

Return an iterator over an exclusive range, each iteration increasing by `step`.

If `range` is reversed and `step` < 0, iteration goes backwards.

Otherwise, if `range` is empty, an empty iterator is returned.

# Example

```rhai
// prints all values from 8 to 17 in steps of 3
for n in range(8..18, 3) {
    print(n);
}

// prints all values down from 18 to 9 in steps of -3
for n in range(18..8, -3) {
    print(n);
}
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn range(range: Range<i32>, step: i32) -> Iterator<i32>
```

<details>
<summary markdown="span"> details </summary>

Return an iterator over an exclusive range, each iteration increasing by `step`.

If `range` is reversed and `step` < 0, iteration goes backwards.

Otherwise, if `range` is empty, an empty iterator is returned.

# Example

```rhai
// prints all values from 8 to 17 in steps of 3
for n in range(8..18, 3) {
    print(n);
}

// prints all values down from 18 to 9 in steps of -3
for n in range(18..8, -3) {
    print(n);
}
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn range(range: Range<i16>, step: i16) -> Iterator<i16>
```

<details>
<summary markdown="span"> details </summary>

Return an iterator over an exclusive range, each iteration increasing by `step`.

If `range` is reversed and `step` < 0, iteration goes backwards.

Otherwise, if `range` is empty, an empty iterator is returned.

# Example

```rhai
// prints all values from 8 to 17 in steps of 3
for n in range(8..18, 3) {
    print(n);
}

// prints all values down from 18 to 9 in steps of -3
for n in range(18..8, -3) {
    print(n);
}
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn range(from: u32, to: u32) -> Iterator<u32>
```

<details>
<summary markdown="span"> details </summary>

Return an iterator over the exclusive range of `from..to`.
The value `to` is never included.

# Example

```rhai
// prints all values from 8 to 17
for n in range(8, 18) {
    print(n);
}
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn range(range: Range<u64>, step: u64) -> Iterator<u64>
```

<details>
<summary markdown="span"> details </summary>

Return an iterator over an exclusive range, each iteration increasing by `step`.

If `range` is reversed and `step` < 0, iteration goes backwards.

Otherwise, if `range` is empty, an empty iterator is returned.

# Example

```rhai
// prints all values from 8 to 17 in steps of 3
for n in range(8..18, 3) {
    print(n);
}

// prints all values down from 18 to 9 in steps of -3
for n in range(18..8, -3) {
    print(n);
}
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn range(range: Range<int>, step: int) -> Iterator<int>
```

<details>
<summary markdown="span"> details </summary>

Return an iterator over an exclusive range, each iteration increasing by `step`.

If `range` is reversed and `step` < 0, iteration goes backwards.

Otherwise, if `range` is empty, an empty iterator is returned.

# Example

```rhai
// prints all values from 8 to 17 in steps of 3
for n in range(8..18, 3) {
    print(n);
}

// prints all values down from 18 to 9 in steps of -3
for n in range(18..8, -3) {
    print(n);
}
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn range(from: i8, to: i8) -> Iterator<i8>
```

<details>
<summary markdown="span"> details </summary>

Return an iterator over the exclusive range of `from..to`.
The value `to` is never included.

# Example

```rhai
// prints all values from 8 to 17
for n in range(8, 18) {
    print(n);
}
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn range(from: u128, to: u128) -> Iterator<u128>
```

<details>
<summary markdown="span"> details </summary>

Return an iterator over the exclusive range of `from..to`.
The value `to` is never included.

# Example

```rhai
// prints all values from 8 to 17
for n in range(8, 18) {
    print(n);
}
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn range(from: u16, to: u16) -> Iterator<u16>
```

<details>
<summary markdown="span"> details </summary>

Return an iterator over the exclusive range of `from..to`.
The value `to` is never included.

# Example

```rhai
// prints all values from 8 to 17
for n in range(8, 18) {
    print(n);
}
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn range(from: i32, to: i32) -> Iterator<i32>
```

<details>
<summary markdown="span"> details </summary>

Return an iterator over the exclusive range of `from..to`.
The value `to` is never included.

# Example

```rhai
// prints all values from 8 to 17
for n in range(8, 18) {
    print(n);
}
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn range(range: Range<i128>, step: i128) -> Iterator<i128>
```

<details>
<summary markdown="span"> details </summary>

Return an iterator over an exclusive range, each iteration increasing by `step`.

If `range` is reversed and `step` < 0, iteration goes backwards.

Otherwise, if `range` is empty, an empty iterator is returned.

# Example

```rhai
// prints all values from 8 to 17 in steps of 3
for n in range(8..18, 3) {
    print(n);
}

// prints all values down from 18 to 9 in steps of -3
for n in range(18..8, -3) {
    print(n);
}
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn range(from: i16, to: i16) -> Iterator<i16>
```

<details>
<summary markdown="span"> details </summary>

Return an iterator over the exclusive range of `from..to`.
The value `to` is never included.

# Example

```rhai
// prints all values from 8 to 17
for n in range(8, 18) {
    print(n);
}
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn range(from: i128, to: i128) -> Iterator<i128>
```

<details>
<summary markdown="span"> details </summary>

Return an iterator over the exclusive range of `from..to`.
The value `to` is never included.

# Example

```rhai
// prints all values from 8 to 17
for n in range(8, 18) {
    print(n);
}
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn range(from: u64, to: u64) -> Iterator<u64>
```

<details>
<summary markdown="span"> details </summary>

Return an iterator over the exclusive range of `from..to`.
The value `to` is never included.

# Example

```rhai
// prints all values from 8 to 17
for n in range(8, 18) {
    print(n);
}
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn range(from: u8, to: u8) -> Iterator<u8>
```

<details>
<summary markdown="span"> details </summary>

Return an iterator over the exclusive range of `from..to`.
The value `to` is never included.

# Example

```rhai
// prints all values from 8 to 17
for n in range(8, 18) {
    print(n);
}
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn range(range: Range<u32>, step: u32) -> Iterator<u32>
```

<details>
<summary markdown="span"> details </summary>

Return an iterator over an exclusive range, each iteration increasing by `step`.

If `range` is reversed and `step` < 0, iteration goes backwards.

Otherwise, if `range` is empty, an empty iterator is returned.

# Example

```rhai
// prints all values from 8 to 17 in steps of 3
for n in range(8..18, 3) {
    print(n);
}

// prints all values down from 18 to 9 in steps of -3
for n in range(18..8, -3) {
    print(n);
}
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn range(range: Range<u16>, step: u16) -> Iterator<u16>
```

<details>
<summary markdown="span"> details </summary>

Return an iterator over an exclusive range, each iteration increasing by `step`.

If `range` is reversed and `step` < 0, iteration goes backwards.

Otherwise, if `range` is empty, an empty iterator is returned.

# Example

```rhai
// prints all values from 8 to 17 in steps of 3
for n in range(8..18, 3) {
    print(n);
}

// prints all values down from 18 to 9 in steps of -3
for n in range(18..8, -3) {
    print(n);
}
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn range(from: int, to: int) -> Iterator<int>
```

<details>
<summary markdown="span"> details </summary>

Return an iterator over the exclusive range of `from..to`.
The value `to` is never included.

# Example

```rhai
// prints all values from 8 to 17
for n in range(8, 18) {
    print(n);
}
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn range(range: Range<u8>, step: u8) -> Iterator<u8>
```

<details>
<summary markdown="span"> details </summary>

Return an iterator over an exclusive range, each iteration increasing by `step`.

If `range` is reversed and `step` < 0, iteration goes backwards.

Otherwise, if `range` is empty, an empty iterator is returned.

# Example

```rhai
// prints all values from 8 to 17 in steps of 3
for n in range(8..18, 3) {
    print(n);
}

// prints all values down from 18 to 9 in steps of -3
for n in range(18..8, -3) {
    print(n);
}
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn range(from: u128, to: u128, step: u128) -> Iterator<u128>
```

<details>
<summary markdown="span"> details </summary>

Return an iterator over the exclusive range of `from..to`, each iteration increasing by `step`.
The value `to` is never included.

If `from` > `to` and `step` < 0, iteration goes backwards.

If `from` > `to` and `step` > 0 or `from` < `to` and `step` < 0, an empty iterator is returned.

# Example

```rhai
// prints all values from 8 to 17 in steps of 3
for n in range(8, 18, 3) {
    print(n);
}

// prints all values down from 18 to 9 in steps of -3
for n in range(18, 8, -3) {
    print(n);
}
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn range(from: float, to: float, step: float) -> Iterator<float>
```

<details>
<summary markdown="span"> details </summary>

Return an iterator over the exclusive range of `from..to`, each iteration increasing by `step`.
The value `to` is never included.

If `from` > `to` and `step` < 0, iteration goes backwards.

If `from` > `to` and `step` > 0 or `from` < `to` and `step` < 0, an empty iterator is returned.

# Example

```rhai
// prints all values from 8 to 17 in steps of 3
for n in range(8, 18, 3) {
    print(n);
}

// prints all values down from 18 to 9 in steps of -3
for n in range(18, 8, -3) {
    print(n);
}
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn range(from: u32, to: u32, step: u32) -> Iterator<u32>
```

<details>
<summary markdown="span"> details </summary>

Return an iterator over the exclusive range of `from..to`, each iteration increasing by `step`.
The value `to` is never included.

If `from` > `to` and `step` < 0, iteration goes backwards.

If `from` > `to` and `step` > 0 or `from` < `to` and `step` < 0, an empty iterator is returned.

# Example

```rhai
// prints all values from 8 to 17 in steps of 3
for n in range(8, 18, 3) {
    print(n);
}

// prints all values down from 18 to 9 in steps of -3
for n in range(18, 8, -3) {
    print(n);
}
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn range(from: u16, to: u16, step: u16) -> Iterator<u16>
```

<details>
<summary markdown="span"> details </summary>

Return an iterator over the exclusive range of `from..to`, each iteration increasing by `step`.
The value `to` is never included.

If `from` > `to` and `step` < 0, iteration goes backwards.

If `from` > `to` and `step` > 0 or `from` < `to` and `step` < 0, an empty iterator is returned.

# Example

```rhai
// prints all values from 8 to 17 in steps of 3
for n in range(8, 18, 3) {
    print(n);
}

// prints all values down from 18 to 9 in steps of -3
for n in range(18, 8, -3) {
    print(n);
}
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn range(from: i16, to: i16, step: i16) -> Iterator<i16>
```

<details>
<summary markdown="span"> details </summary>

Return an iterator over the exclusive range of `from..to`, each iteration increasing by `step`.
The value `to` is never included.

If `from` > `to` and `step` < 0, iteration goes backwards.

If `from` > `to` and `step` > 0 or `from` < `to` and `step` < 0, an empty iterator is returned.

# Example

```rhai
// prints all values from 8 to 17 in steps of 3
for n in range(8, 18, 3) {
    print(n);
}

// prints all values down from 18 to 9 in steps of -3
for n in range(18, 8, -3) {
    print(n);
}
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn range(from: int, to: int, step: int) -> Iterator<int>
```

<details>
<summary markdown="span"> details </summary>

Return an iterator over the exclusive range of `from..to`, each iteration increasing by `step`.
The value `to` is never included.

If `from` > `to` and `step` < 0, iteration goes backwards.

If `from` > `to` and `step` > 0 or `from` < `to` and `step` < 0, an empty iterator is returned.

# Example

```rhai
// prints all values from 8 to 17 in steps of 3
for n in range(8, 18, 3) {
    print(n);
}

// prints all values down from 18 to 9 in steps of -3
for n in range(18, 8, -3) {
    print(n);
}
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn range(from: i8, to: i8, step: i8) -> Iterator<i8>
```

<details>
<summary markdown="span"> details </summary>

Return an iterator over the exclusive range of `from..to`, each iteration increasing by `step`.
The value `to` is never included.

If `from` > `to` and `step` < 0, iteration goes backwards.

If `from` > `to` and `step` > 0 or `from` < `to` and `step` < 0, an empty iterator is returned.

# Example

```rhai
// prints all values from 8 to 17 in steps of 3
for n in range(8, 18, 3) {
    print(n);
}

// prints all values down from 18 to 9 in steps of -3
for n in range(18, 8, -3) {
    print(n);
}
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn range(from: i32, to: i32, step: i32) -> Iterator<i32>
```

<details>
<summary markdown="span"> details </summary>

Return an iterator over the exclusive range of `from..to`, each iteration increasing by `step`.
The value `to` is never included.

If `from` > `to` and `step` < 0, iteration goes backwards.

If `from` > `to` and `step` > 0 or `from` < `to` and `step` < 0, an empty iterator is returned.

# Example

```rhai
// prints all values from 8 to 17 in steps of 3
for n in range(8, 18, 3) {
    print(n);
}

// prints all values down from 18 to 9 in steps of -3
for n in range(18, 8, -3) {
    print(n);
}
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn range(from: u64, to: u64, step: u64) -> Iterator<u64>
```

<details>
<summary markdown="span"> details </summary>

Return an iterator over the exclusive range of `from..to`, each iteration increasing by `step`.
The value `to` is never included.

If `from` > `to` and `step` < 0, iteration goes backwards.

If `from` > `to` and `step` > 0 or `from` < `to` and `step` < 0, an empty iterator is returned.

# Example

```rhai
// prints all values from 8 to 17 in steps of 3
for n in range(8, 18, 3) {
    print(n);
}

// prints all values down from 18 to 9 in steps of -3
for n in range(18, 8, -3) {
    print(n);
}
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn range(from: i128, to: i128, step: i128) -> Iterator<i128>
```

<details>
<summary markdown="span"> details </summary>

Return an iterator over the exclusive range of `from..to`, each iteration increasing by `step`.
The value `to` is never included.

If `from` > `to` and `step` < 0, iteration goes backwards.

If `from` > `to` and `step` > 0 or `from` < `to` and `step` < 0, an empty iterator is returned.

# Example

```rhai
// prints all values from 8 to 17 in steps of 3
for n in range(8, 18, 3) {
    print(n);
}

// prints all values down from 18 to 9 in steps of -3
for n in range(18, 8, -3) {
    print(n);
}
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn range(from: u8, to: u8, step: u8) -> Iterator<u8>
```

<details>
<summary markdown="span"> details </summary>

Return an iterator over the exclusive range of `from..to`, each iteration increasing by `step`.
The value `to` is never included.

If `from` > `to` and `step` < 0, iteration goes backwards.

If `from` > `to` and `step` > 0 or `from` < `to` and `step` < 0, an empty iterator is returned.

# Example

```rhai
// prints all values from 8 to 17 in steps of 3
for n in range(8, 18, 3) {
    print(n);
}

// prints all values down from 18 to 9 in steps of -3
for n in range(18, 8, -3) {
    print(n);
}
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn reduce(array: Array, reducer: String) -> Result<?, Box<EvalAltResult>>
```

<details>
<summary markdown="span"> details </summary>

Reduce an array by iterating through all elements while applying a function named by `reducer`.

# Function Parameters

A function with the same name as the value of `reducer` must exist taking these parameters:

* `result`: accumulated result, initially `()`
* `element`: copy of array element
* `index` _(optional)_: current index in the array

# Example

```rhai
fn process(r, x) {
    x + (r ?? 0)
}
fn process_extra(r, x, i) {
    x + i + (r ?? 0)
}

let x = [1, 2, 3, 4, 5];

let y = x.reduce("process");

print(y);       // prints 15

let y = x.reduce("process_extra");

print(y);       // prints 25
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn reduce(array: Array, reducer: FnPtr) -> Result<?, Box<EvalAltResult>>
```

<details>
<summary markdown="span"> details </summary>

Reduce an array by iterating through all elements while applying the `reducer` function.

# Function Parameters

* `result`: accumulated result, initially `()`
* `element`: copy of array element
* `index` _(optional)_: current index in the array

# Example

```rhai
let x = [1, 2, 3, 4, 5];

let y = x.reduce(|r, v| v + (r ?? 0));

print(y);       // prints 15

let y = x.reduce(|r, v, i| v + i + (r ?? 0));

print(y);       // prints 25
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn reduce(array: Array, reducer: FnPtr, initial: ?) -> Result<?, Box<EvalAltResult>>
```

<details>
<summary markdown="span"> details </summary>

Reduce an array by iterating through all elements while applying the `reducer` function.

# Function Parameters

* `result`: accumulated result, starting with the value of `initial`
* `element`: copy of array element
* `index` _(optional)_: current index in the array

# Example

```rhai
let x = [1, 2, 3, 4, 5];

let y = x.reduce(|r, v| v + r, 5);

print(y);       // prints 20

let y = x.reduce(|r, v, i| v + i + r, 5);

print(y);       // prints 30
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn reduce(array: Array, reducer: String, initial: ?) -> Result<?, Box<EvalAltResult>>
```

<details>
<summary markdown="span"> details </summary>

Reduce an array by iterating through all elements while applying a function named by `reducer`.

# Function Parameters

A function with the same name as the value of `reducer` must exist taking these parameters:

* `result`: accumulated result, starting with the value of `initial`
* `element`: copy of array element
* `index` _(optional)_: current index in the array

# Example

```rhai
fn process(r, x) { x + r }

fn process_extra(r, x, i) { x + i + r }

let x = [1, 2, 3, 4, 5];

let y = x.reduce("process", 5);

print(y);       // prints 20

let y = x.reduce("process_extra", 5);

print(y);       // prints 30
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn reduce_rev(array: Array, reducer: FnPtr) -> Result<?, Box<EvalAltResult>>
```

<details>
<summary markdown="span"> details </summary>

Reduce an array by iterating through all elements, in _reverse_ order,
while applying the `reducer` function.

# Function Parameters

* `result`: accumulated result, initially `()`
* `element`: copy of array element
* `index` _(optional)_: current index in the array

# Example

```rhai
let x = [1, 2, 3, 4, 5];

let y = x.reduce_rev(|r, v| v + (r ?? 0));

print(y);       // prints 15

let y = x.reduce_rev(|r, v, i| v + i + (r ?? 0));

print(y);       // prints 25
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn reduce_rev(array: Array, reducer: String) -> Result<?, Box<EvalAltResult>>
```

<details>
<summary markdown="span"> details </summary>

Reduce an array by iterating through all elements, in _reverse_ order,
while applying a function named by `reducer`.

# Function Parameters

A function with the same name as the value of `reducer` must exist taking these parameters:

* `result`: accumulated result, initially `()`
* `element`: copy of array element
* `index` _(optional)_: current index in the array

# Example

```rhai
fn process(r, x) {
    x + (r ?? 0)
}
fn process_extra(r, x, i) {
    x + i + (r ?? 0)
}

let x = [1, 2, 3, 4, 5];

let y = x.reduce_rev("process");

print(y);       // prints 15

let y = x.reduce_rev("process_extra");

print(y);       // prints 25
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn reduce_rev(array: Array, reducer: String, initial: ?) -> Result<?, Box<EvalAltResult>>
```

<details>
<summary markdown="span"> details </summary>

Reduce an array by iterating through all elements, in _reverse_ order,
while applying a function named by `reducer`.

# Function Parameters

A function with the same name as the value of `reducer` must exist taking these parameters:

* `result`: accumulated result, starting with the value of `initial`
* `element`: copy of array element
* `index` _(optional)_: current index in the array

# Example

```rhai
fn process(r, x) { x + r }

fn process_extra(r, x, i) { x + i + r }

let x = [1, 2, 3, 4, 5];

let y = x.reduce_rev("process", 5);

print(y);       // prints 20

let y = x.reduce_rev("process_extra", 5);

print(y);       // prints 30
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn reduce_rev(array: Array, reducer: FnPtr, initial: ?) -> Result<?, Box<EvalAltResult>>
```

<details>
<summary markdown="span"> details </summary>

Reduce an array by iterating through all elements, in _reverse_ order,
while applying the `reducer` function.

# Function Parameters

* `result`: accumulated result, starting with the value of `initial`
* `element`: copy of array element
* `index` _(optional)_: current index in the array

# Example

```rhai
let x = [1, 2, 3, 4, 5];

let y = x.reduce_rev(|r, v| v + r, 5);

print(y);       // prints 20

let y = x.reduce_rev(|r, v, i| v + i + r, 5);

print(y);       // prints 30
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn remove(array: Array, index: int) -> ?
```

<details>
<summary markdown="span"> details </summary>

Remove the element at the specified `index` from the array and return it.

* If `index` < 0, position counts from the end of the array (`-1` is the last element).
* If `index` < -length of array, `()` is returned.
* If `index` ≥ length of array, `()` is returned.

# Example

```rhai
let x = [1, 2, 3];

print(x.remove(1));     // prints 2

print(x);               // prints "[1, 3]"

print(x.remove(-2));    // prints 1

print(x);               // prints "[3]"
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn remove(map: Map, property: String) -> ?
```

<details>
<summary markdown="span"> details </summary>

Remove any property of the specified `name` from the object map, returning its value.

If the property does not exist, `()` is returned.

# Example

```rhai
let m = #{a:1, b:2, c:3};

let x = m.remove("b");

print(x);       // prints 2

print(m);       // prints "#{a:1, c:3}"
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn remove(blob: Blob, index: int) -> int
```

<details>
<summary markdown="span"> details </summary>

Remove the byte at the specified `index` from the BLOB and return it.

* If `index` < 0, position counts from the end of the BLOB (`-1` is the last byte).
* If `index` < -length of BLOB, zero is returned.
* If `index` ≥ length of BLOB, zero is returned.

# Example

```rhai
let b = blob();

b += 1; b += 2; b += 3; b += 4; b += 5;

print(x.remove(1));     // prints 2

print(x);               // prints "[01030405]"

print(x.remove(-2));    // prints 4

print(x);               // prints "[010305]"
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn remove(string: String, character: char)
```

<details>
<summary markdown="span"> details </summary>

Remove all occurrences of a character from the string.

# Example

```rhai
let text = "hello, world! hello, foobar!";

text.remove("o");

print(text);        // prints "hell, wrld! hell, fbar!"
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn remove(string: String, sub_string: String)
```

<details>
<summary markdown="span"> details </summary>

Remove all occurrences of a sub-string from the string.

# Example

```rhai
let text = "hello, world! hello, foobar!";

text.remove("hello");

print(text);        // prints ", world! , foobar!"
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn remove_header(message: Message, header: String) -> bool
```

<details>
<summary markdown="span"> details </summary>

Remove a header from the raw or parsed email contained in ctx.

# Examples

```
"Subject: The initial header value\r\n",
"\r\n",
"Hello world!\r\n",

  preq: [
    rule "remove_header" || {
      remove_header("Subject");
      if has_header("Subject") { return deny(); }

      prepend_header("Subject-2", "Rust is good");
      remove_header(identifier("Subject-2"));

      prepend_header("Subject-3", "Rust is good !!!!!");

      accept(`250 ${get_header("Subject-3")}`);
    }
  ]
}
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn remove_header(message: Message, header: SharedObject) -> bool
```

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn remove_rcpt_envelop(context: Context, addr: SharedObject) -> ()
```

<details>
<summary markdown="span"> details </summary>

remove a recipient from the envelop.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn remove_rcpt_envelop(context: Context, addr: String) -> ()
```

<details>
<summary markdown="span"> details </summary>

remove a recipient from the envelop.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn remove_rcpt_message(message: Message, addr: SharedObject) -> ()
```

<details>
<summary markdown="span"> details </summary>

remove a recipient from the mail 'To' header.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn remove_rcpt_message(message: Message, addr: String) -> ()
```

<details>
<summary markdown="span"> details </summary>

remove a recipient from the mail 'To' header.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn rename_header(message: Message, old: SharedObject, new: String) -> ()
```

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn rename_header(message: Message, old: String, new: SharedObject) -> ()
```

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn rename_header(message: Message, old: String, new: String) -> ()
```

<details>
<summary markdown="span"> details </summary>

Change the **key** of a header for a new one.
Do not confuse with [`set_header()`].

# Examples

```
"Subject: The initial header value\r\n",
"\r\n",
"Hello world!\r\n",

  preq: [
    rule "rename_header" || {
      rename_header("Subject", "bob");
      if has_header("Subject") { return deny(); }

      rename_header("bob", identifier("Subject"));
      if has_header("bob") { return deny(); }

      rename_header(identifier("Subject"), "foo");
      if has_header("Subject") { return deny(); }

      rename_header(identifier("foo"), identifier("Subject"));
      if has_header("foo") { return deny(); }

      accept(`250 ${get_header("Subject")}`);
    }
  ]
}
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn rename_header(message: Message, old: SharedObject, new: SharedObject) -> ()
```

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn replace(string: String, find_string: String, substitute_string: String)
```

<details>
<summary markdown="span"> details </summary>

Replace all occurrences of the specified sub-string in the string with another string.

# Example

```rhai
let text = "hello, world! hello, foobar!";

text.replace("hello", "hey");

print(text);        // prints "hey, world! hey, foobar!"
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn replace(string: String, find_character: char, substitute_character: char)
```

<details>
<summary markdown="span"> details </summary>

Replace all occurrences of the specified character in the string with another character.

# Example

```rhai
let text = "hello, world! hello, foobar!";

text.replace("l", '*');

print(text);        // prints "he**o, wor*d! he**o, foobar!"
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn replace(string: String, find_string: String, substitute_character: char)
```

<details>
<summary markdown="span"> details </summary>

Replace all occurrences of the specified sub-string in the string with the specified character.

# Example

```rhai
let text = "hello, world! hello, foobar!";

text.replace("hello", '*');

print(text);        // prints "*, world! *, foobar!"
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn replace(string: String, find_character: char, substitute_string: String)
```

<details>
<summary markdown="span"> details </summary>

Replace all occurrences of the specified character in the string with another string.

# Example

```rhai
let text = "hello, world! hello, foobar!";

text.replace('l', "(^)");

print(text);        // prints "he(^)(^)o, wor(^)d! he(^)(^)o, foobar!"
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn retain(array: Array, filter: FnPtr) -> Result<Array, Box<EvalAltResult>>
```

<details>
<summary markdown="span"> details </summary>

Remove all elements in the array that do not return `true` when applied the `filter`
function and return them as a new array.

# Function Parameters

* `element`: copy of array element
* `index` _(optional)_: current index in the array

# Example

```rhai
let x = [1, 2, 3, 4, 5];

let y = x.retain(|v| v >= 3);

print(x);       // prints "[3, 4, 5]"

print(y);       // prints "[1, 2]"

let z = x.retain(|v, i| v + i <= 5);

print(x);       // prints "[3, 4]"

print(z);       // prints "[5]"
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn retain(array: Array, filter: String) -> Result<Array, Box<EvalAltResult>>
```

<details>
<summary markdown="span"> details </summary>

Remove all elements in the array that do not return `true` when applied a function named by
`filter` and return them as a new array.

# Function Parameters

A function with the same name as the value of `filter` must exist taking these parameters:

* `element`: copy of array element
* `index` _(optional)_: current index in the array

# Example

```rhai
fn large(x) { x >= 3 }

fn screen(x, i) { x + i <= 5 }

let x = [1, 2, 3, 4, 5];

let y = x.retain("large");

print(x);       // prints "[3, 4, 5]"

print(y);       // prints "[1, 2]"

let z = x.retain("screen");

print(x);       // prints "[3, 4]"

print(z);       // prints "[5]"
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn retain(blob: Blob, range: Range<int>) -> Blob
```

<details>
<summary markdown="span"> details </summary>

Remove all bytes in the BLOB not within an exclusive `range` and return them as a new BLOB.

# Example

```rhai
let b1 = blob();

b1 += 1; b1 += 2; b1 += 3; b1 += 4; b1 += 5;

let b2 = b1.retain(1..4);

print(b1);      // prints "[020304]"

print(b2);      // prints "[0105]"

let b3 = b1.retain(1..3);

print(b1);      // prints "[0304]"

print(b2);      // prints "[01]"
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn retain(array: Array, range: Range<int>) -> Array
```

<details>
<summary markdown="span"> details </summary>

Remove all elements in the array not within an exclusive `range` and return them as a new array.

# Example

```rhai
let x = [1, 2, 3, 4, 5];

let y = x.retain(1..4);

print(x);       // prints "[2, 3, 4]"

print(y);       // prints "[1, 5]"

let z = x.retain(1..3);

print(x);       // prints "[3, 4]"

print(z);       // prints "[1]"
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn retain(array: Array, range: RangeInclusive<int>) -> Array
```

<details>
<summary markdown="span"> details </summary>

Remove all elements in the array not within an inclusive `range` and return them as a new array.

# Example

```rhai
let x = [1, 2, 3, 4, 5];

let y = x.retain(1..=3);

print(x);       // prints "[2, 3, 4]"

print(y);       // prints "[1, 5]"

let z = x.retain(1..=2);

print(x);       // prints "[3, 4]"

print(z);       // prints "[1]"
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn retain(blob: Blob, range: RangeInclusive<int>) -> Blob
```

<details>
<summary markdown="span"> details </summary>

Remove all bytes in the BLOB not within an inclusive `range` and return them as a new BLOB.

# Example

```rhai
let b1 = blob();

b1 += 1; b1 += 2; b1 += 3; b1 += 4; b1 += 5;

let b2 = b1.retain(1..=3);

print(b1);      // prints "[020304]"

print(b2);      // prints "[0105]"

let b3 = b1.retain(1..=2);

print(b1);      // prints "[0304]"

print(b2);      // prints "[01]"
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn retain(blob: Blob, start: int, len: int) -> Blob
```

<details>
<summary markdown="span"> details </summary>

Remove all bytes not within a portion of the BLOB and return them as a new BLOB.

* If `start` < 0, position counts from the end of the BLOB (`-1` is the last byte).
* If `start` < -length of BLOB, position counts from the beginning of the BLOB.
* If `start` ≥ length of BLOB, all elements are removed returned.
* If `len` ≤ 0, all elements are removed and returned.
* If `start` position + `len` ≥ length of BLOB, entire portion of the BLOB before the `start` position is removed and returned.

# Example

```rhai
let b1 = blob();

b1 += 1; b1 += 2; b1 += 3; b1 += 4; b1 += 5;

let b2 = b1.retain(1, 2);

print(b1);      // prints "[0203]"

print(b2);      // prints "[010405]"

let b3 = b1.retain(-1, 1);

print(b1);      // prints "[03]"

print(b3);      // prints "[02]"
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn retain(array: Array, start: int, len: int) -> Array
```

<details>
<summary markdown="span"> details </summary>

Remove all elements not within a portion of the array and return them as a new array.

* If `start` < 0, position counts from the end of the array (`-1` is the last element).
* If `start` < -length of array, position counts from the beginning of the array.
* If `start` ≥ length of array, all elements are removed returned.
* If `len` ≤ 0, all elements are removed and returned.
* If `start` position + `len` ≥ length of array, entire portion of the array before the `start` position is removed and returned.

# Example

```rhai
let x = [1, 2, 3, 4, 5];

let y = x.retain(1, 2);

print(x);       // prints "[2, 3]"

print(y);       // prints "[1, 4, 5]"

let z = x.retain(-1, 1);

print(x);       // prints "[3]"

print(z);       // prints "[2]"
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn reverse(array: Array)
```

<details>
<summary markdown="span"> details </summary>

Reverse all the elements in the array.

# Example

```rhai
let x = [1, 2, 3, 4, 5];

x.reverse();

print(x);       // prints "[5, 4, 3, 2, 1]"
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn reverse(blob: Blob)
```

<details>
<summary markdown="span"> details </summary>

Reverse the BLOB.

# Example

```rhai
let b = blob();

b += 1; b += 2; b += 3; b += 4; b += 5;

print(b);           // prints "[0102030405]"

b.reverse();

print(b);           // prints "[0504030201]"
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn rewrite_mail_from_envelop(context: Context, new_addr: String) -> ()
```

<details>
<summary markdown="span"> details </summary>

Change the sender of the envelop.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn rewrite_mail_from_envelop(context: Context, new_addr: SharedObject) -> ()
```

<details>
<summary markdown="span"> details </summary>

Change the sender of the envelop using an object.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn rewrite_mail_from_message(message: Message, new_addr: SharedObject) -> ()
```

<details>
<summary markdown="span"> details </summary>

replace the value of the `From` header by another address.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn rewrite_mail_from_message(message: Message, new_addr: String) -> ()
```

<details>
<summary markdown="span"> details </summary>

replace the value of the `From` header by another address.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn rewrite_rcpt_envelop(context: Context, old_addr: SharedObject, new_addr: String) -> ()
```

<details>
<summary markdown="span"> details </summary>

Replace a recipient of the envelop.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn rewrite_rcpt_envelop(context: Context, old_addr: String, new_addr: SharedObject) -> ()
```

<details>
<summary markdown="span"> details </summary>

Replace a recipient of the envelop.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn rewrite_rcpt_envelop(context: Context, old_addr: String, new_addr: String) -> ()
```

<details>
<summary markdown="span"> details </summary>

Replace a recipient of the envelop.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn rewrite_rcpt_envelop(context: Context, old_addr: SharedObject, new_addr: SharedObject) -> ()
```

<details>
<summary markdown="span"> details </summary>

Replace a recipient of the envelop.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn rewrite_rcpt_message(message: Message, old_addr: String, new_addr: String) -> ()
```

<details>
<summary markdown="span"> details </summary>

replace the value of the `To:` header by another address.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn rewrite_rcpt_message(message: Message, old_addr: SharedObject, new_addr: SharedObject) -> ()
```

<details>
<summary markdown="span"> details </summary>

replace the value of the `To:` header by another address.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn rewrite_rcpt_message(message: Message, old_addr: String, new_addr: SharedObject) -> ()
```

<details>
<summary markdown="span"> details </summary>

replace the value of the `To:` header by another address.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn rewrite_rcpt_message(message: Message, old_addr: SharedObject, new_addr: String) -> ()
```

<details>
<summary markdown="span"> details </summary>

replace the value of the `To:` header by another address.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn rlookup(server: Server, name: SharedObject) -> Array>
```

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn rlookup(server: Server, name: String) -> Array>
```

<details>
<summary markdown="span"> details </summary>

Perform a dns reverse lookup using the root dns.

# Errors

* Failed to convert the `ip` parameter from a string into an IP.
* Reverse lookup failed.

# Examples

```
  connect: [
    rule "rlookup" || {
      accept(`250 client ip: ${"127.0.0.1"} -> ${rlookup("127.0.0.1")}`);
    }
  ],
}
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn round(x: float) -> float
```

<details>
<summary markdown="span"> details </summary>

Return the nearest whole number closest to the floating-point number.
Rounds away from zero.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn send_mail(from: String, to: Array, path: String, relay: String) -> ()
```

<details>
<summary markdown="span"> details </summary>

send a mail from a template.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn set(array: Array, index: int, value: ?)
```

<details>
<summary markdown="span"> details </summary>

Set the element at the `index` position in the array to a new `value`.

* If `index` < 0, position counts from the end of the array (`-1` is the last element).
* If `index` < -length of array, the array is not modified.
* If `index` ≥ length of array, the array is not modified.

# Example

```rhai
let x = [1, 2, 3];

x.set(0, 42);

print(x);           // prints "[42, 2, 3]"

x.set(-3, 0);

print(x);           // prints "[0, 2, 3]"

x.set(99, 123);

print(x);           // prints "[0, 2, 3]"
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn set(blob: Blob, index: int, value: int)
```

<details>
<summary markdown="span"> details </summary>

Set the particular `index` position in the BLOB to a new byte `value`.

* If `index` < 0, position counts from the end of the BLOB (`-1` is the last byte).
* If `index` < -length of BLOB, the BLOB is not modified.
* If `index` ≥ length of BLOB, the BLOB is not modified.

# Example

```rhai
let b = blob();

b += 1; b += 2; b += 3; b += 4; b += 5;

b.set(0, 0x42);

print(b);           // prints "[4202030405]"

b.set(-3, 0);

print(b);           // prints "[4202000405]"

b.set(99, 123);

print(b);           // prints "[4202000405]"
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn set(string: String, index: int, character: char)
```

<details>
<summary markdown="span"> details </summary>

Set the `index` position in the string to a new `character`.

* If `index` < 0, position counts from the end of the string (`-1` is the last character).
* If `index` < -length of string, the string is not modified.
* If `index` ≥ length of string, the string is not modified.

# Example

```rhai
let text = "hello, world!";

text.set(3, 'x');

print(text);     // prints "helxo, world!"

text.set(-3, 'x');

print(text);    // prints "hello, worxd!"

text.set(99, 'x');

print(text);    // prints "hello, worxd!"
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn set(map: Map, property: String, value: ?)
```

<details>
<summary markdown="span"> details </summary>

Set the value of the `property` in the object map to a new `value`.

If `property` does not exist in the object map, it is added.

# Example

```rhai
let m = #{a: 1, b: 2, c: 3};

m.set("b", 42)'

print(m);           // prints "#{a: 1, b: 42, c: 3}"

x.set("x", 0);

print(m);           // prints "#{a: 1, b: 42, c: 3, x: 0}"
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn set tag(value: ?, tag: int) -> Result<(), Box<EvalAltResult>>
```

<details>
<summary markdown="span"> details </summary>

Set the _tag_ of a `Dynamic` value.

# Example

```rhai
let x = "hello, world!";

x.tag = 42;

print(x.tag);           // prints 42
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn set_bit(value: int, bit: int, new_value: bool) -> Result<(), Box<EvalAltResult>>
```

<details>
<summary markdown="span"> details </summary>

Set the specified `bit` in the number if the new value is `true`.
Clear the `bit` if the new value is `false`.

If `bit` < 0, position counts from the MSB (Most Significant Bit).

# Example

```rhai
let x = 123456;

x.set_bit(5, true);

print(x);               // prints 123488

x.set_bit(6, false);

print(x);               // prints 123424

x.set_bit(-48, false);

print(x);               // prints 57888 on 64-bit
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn set_bits(value: int, range: RangeInclusive<int>, new_value: int) -> Result<(), Box<EvalAltResult>>
```

<details>
<summary markdown="span"> details </summary>

Replace an inclusive range of bits in the number with a new value.

# Example

```rhai
let x = 123456;

x.set_bits(5..=9, 42);

print(x);           // print 123200
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn set_bits(value: int, range: Range<int>, new_value: int) -> Result<(), Box<EvalAltResult>>
```

<details>
<summary markdown="span"> details </summary>

Replace an exclusive range of bits in the number with a new value.

# Example

```rhai
let x = 123456;

x.set_bits(5..10, 42);

print(x);           // print 123200
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn set_bits(value: int, bit: int, bits: int, new_value: int) -> Result<(), Box<EvalAltResult>>
```

<details>
<summary markdown="span"> details </summary>

Replace a portion of bits in the number with a new value.

* If `start` < 0, position counts from the MSB (Most Significant Bit).
* If `bits` ≤ 0, the number is not modified.
* If `start` position + `bits` ≥ total number of bits, the bits after the `start` position are replaced.

# Example

```rhai
let x = 123456;

x.set_bits(5, 8, 42);

print(x);           // prints 124224

x.set_bits(-16, 10, 42);

print(x);           // prints 11821949021971776 on 64-bit
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn set_header(message: Message, header: String, value: String) -> ()
```

<details>
<summary markdown="span"> details </summary>

Set the **value** of a message header.
Do not confuse with [`rename_header()`].

# Examples

```
"Subject: The initial header value\r\n",
"\r\n",
"Hello world!\r\n",

  preq: [
    rule "set_header" || {
      set_header("Subject", "The header value has been updated");
      set_header("Subject", identifier("The header value has been updated again"));
      accept(`250 ${get_header("Subject")}`);
    }
  ]
}
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn set_header(message: Message, header: String, value: SharedObject) -> ()
```

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn set_tag(value: ?, tag: int) -> Result<(), Box<EvalAltResult>>
```

<details>
<summary markdown="span"> details </summary>

Set the _tag_ of a `Dynamic` value.

# Example

```rhai
let x = "hello, world!";

x.tag = 42;

print(x.tag);           // prints 42
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn shift(blob: Blob) -> int
```

<details>
<summary markdown="span"> details </summary>

Remove the first byte from the BLOB and return it.

If the BLOB is empty, zero is returned.

# Example

```rhai
let b = blob();

b += 1; b += 2; b += 3; b += 4; b += 5;

print(b.shift());       // prints 1

print(b);               // prints "[02030405]"
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn shift(array: Array) -> ?
```

<details>
<summary markdown="span"> details </summary>

Remove the first element from the array and return it.

If the array is empty, `()` is returned.

# Example

```rhai
let x = [1, 2, 3];

print(x.shift());   // prints 1

print(x);           // prints "[2, 3]"
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn sign(x: int) -> int
```

<details>
<summary markdown="span"> details </summary>

Return the sign (as an integer) of the number according to the following:

* `0` if the number is zero
* `1` if the number is positive
* `-1` if the number is negative
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn sign(x: i32) -> int
```

<details>
<summary markdown="span"> details </summary>

Return the sign (as an integer) of the number according to the following:

* `0` if the number is zero
* `1` if the number is positive
* `-1` if the number is negative
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn sign(x: i128) -> int
```

<details>
<summary markdown="span"> details </summary>

Return the sign (as an integer) of the number according to the following:

* `0` if the number is zero
* `1` if the number is positive
* `-1` if the number is negative
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn sign(x: i8) -> int
```

<details>
<summary markdown="span"> details </summary>

Return the sign (as an integer) of the number according to the following:

* `0` if the number is zero
* `1` if the number is positive
* `-1` if the number is negative
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn sign(x: f32) -> Result<int, Box<EvalAltResult>>
```

<details>
<summary markdown="span"> details </summary>

Return the sign (as an integer) of the floating-point number according to the following:

* `0` if the number is zero
* `1` if the number is positive
* `-1` if the number is negative
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn sign(x: i16) -> int
```

<details>
<summary markdown="span"> details </summary>

Return the sign (as an integer) of the number according to the following:

* `0` if the number is zero
* `1` if the number is positive
* `-1` if the number is negative
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn sign(x: float) -> Result<int, Box<EvalAltResult>>
```

<details>
<summary markdown="span"> details </summary>

Return the sign (as an integer) of the floating-point number according to the following:

* `0` if the number is zero
* `1` if the number is positive
* `-1` if the number is negative
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn sin(x: float) -> float
```

<details>
<summary markdown="span"> details </summary>

Return the sine of the floating-point number in radians.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn sinh(x: float) -> float
```

<details>
<summary markdown="span"> details </summary>

Return the hyperbolic sine of the floating-point number in radians.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn sleep(seconds: float)
```

<details>
<summary markdown="span"> details </summary>

Block the current thread for a particular number of `seconds`.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn sleep(seconds: int)
```

<details>
<summary markdown="span"> details </summary>

Block the current thread for a particular number of `seconds`.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn some(array: Array, filter: String) -> Result<bool, Box<EvalAltResult>>
```

<details>
<summary markdown="span"> details </summary>

Return `true` if any element in the array that returns `true` when applied a function named
by `filter`.

# Function Parameters

A function with the same name as the value of `filter` must exist taking these parameters:

* `element`: copy of array element
* `index` _(optional)_: current index in the array

# Example

```rhai
fn large(x) { x > 3 }

fn huge(x) { x > 10 }

fn screen(x, i) { i > x }

let x = [1, 2, 3, 4, 1, 2, 3, 4, 1, 2, 3, 4, 5];

print(x.some("large"));     // prints true

print(x.some("huge"));      // prints false

print(x.some("screen"));    // prints true
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn some(array: Array, filter: FnPtr) -> Result<bool, Box<EvalAltResult>>
```

<details>
<summary markdown="span"> details </summary>

Return `true` if any element in the array that returns `true` when applied the `filter` function.

# Function Parameters

* `element`: copy of array element
* `index` _(optional)_: current index in the array

# Example

```rhai
let x = [1, 2, 3, 4, 1, 2, 3, 4, 1, 2, 3, 4, 5];

print(x.some(|v| v > 3));       // prints true

print(x.some(|v| v > 10));      // prints false

print(x.some(|v, i| i > v));    // prints true
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn sort(array: Array) -> Result<(), Box<EvalAltResult>>
```

<details>
<summary markdown="span"> details </summary>

Sort the array.

All elements in the array must be of the same data type.

# Supported Data Types

* integer numbers
* floating-point numbers
* decimal numbers
* characters
* strings
* booleans
* `()`

# Example

```rhai
let x = [1, 3, 5, 7, 9, 2, 4, 6, 8, 10];

x.sort();

print(x);       // prints "[1, 2, 3, 4, 5, 6, 7, 8, 9, 10]"
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn sort(array: Array, comparer: String) -> Result<(), Box<EvalAltResult>>
```

<details>
<summary markdown="span"> details </summary>

Sort the array based on applying a function named by `comparer`.

# Function Parameters

A function with the same name as the value of `comparer` must exist taking these parameters:

* `element1`: copy of the current array element to compare
* `element2`: copy of the next array element to compare

## Return Value

* Any integer > 0 if `element1 > element2`
* Zero if `element1 == element2`
* Any integer < 0 if `element1 < element2`

# Example

```rhai
fn reverse(a, b) {
    if a > b {
        -1
    } else if a < b {
        1
    } else {
        0
    }
}
let x = [1, 3, 5, 7, 9, 2, 4, 6, 8, 10];

x.sort("reverse");

print(x);       // prints "[10, 9, 8, 7, 6, 5, 4, 3, 2, 1]"
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn sort(array: Array, comparer: FnPtr) -> Result<(), Box<EvalAltResult>>
```

<details>
<summary markdown="span"> details </summary>

Sort the array based on applying the `comparer` function.

# Function Parameters

* `element1`: copy of the current array element to compare
* `element2`: copy of the next array element to compare

## Return Value

* Any integer > 0 if `element1 > element2`
* Zero if `element1 == element2`
* Any integer < 0 if `element1 < element2`

# Example

```rhai
let x = [1, 3, 5, 7, 9, 2, 4, 6, 8, 10];

// Do comparisons in reverse
x.sort(|a, b| if a > b { -1 } else if a < b { 1 } else { 0 });

print(x);       // prints "[10, 9, 8, 7, 6, 5, 4, 3, 2, 1]"
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn splice(blob: Blob, range: Range<int>, replace: Blob)
```

<details>
<summary markdown="span"> details </summary>

Replace an exclusive `range` of the BLOB with another BLOB.

# Example

```rhai
let b1 = blob(10, 0x42);
let b2 = blob(5, 0x18);

b1.splice(1..4, b2);

print(b1);      // prints "[4218181818184242 42424242]"
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn splice(array: Array, range: RangeInclusive<int>, replace: Array)
```

<details>
<summary markdown="span"> details </summary>

Replace an inclusive range of the array with another array.

# Example

```rhai
let x = [1, 2, 3, 4, 5];
let y = [7, 8, 9, 10];

x.splice(1..=3, y);

print(x);       // prints "[1, 7, 8, 9, 10, 5]"
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn splice(blob: Blob, range: RangeInclusive<int>, replace: Blob)
```

<details>
<summary markdown="span"> details </summary>

Replace an inclusive `range` of the BLOB with another BLOB.

# Example

```rhai
let b1 = blob(10, 0x42);
let b2 = blob(5, 0x18);

b1.splice(1..=4, b2);

print(b1);      // prints "[4218181818184242 424242]"
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn splice(array: Array, range: Range<int>, replace: Array)
```

<details>
<summary markdown="span"> details </summary>

Replace an exclusive range of the array with another array.

# Example

```rhai
let x = [1, 2, 3, 4, 5];
let y = [7, 8, 9, 10];

x.splice(1..3, y);

print(x);       // prints "[1, 7, 8, 9, 10, 4, 5]"
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn splice(array: Array, start: int, len: int, replace: Array)
```

<details>
<summary markdown="span"> details </summary>

Replace a portion of the array with another array.

* If `start` < 0, position counts from the end of the array (`-1` is the last element).
* If `start` < -length of array, position counts from the beginning of the array.
* If `start` ≥ length of array, the other array is appended to the end of the array.
* If `len` ≤ 0, the other array is inserted into the array at the `start` position without replacing any element.
* If `start` position + `len` ≥ length of array, entire portion of the array after the `start` position is replaced.

# Example

```rhai
let x = [1, 2, 3, 4, 5];
let y = [7, 8, 9, 10];

x.splice(1, 2, y);

print(x);       // prints "[1, 7, 8, 9, 10, 4, 5]"

x.splice(-5, 4, y);

print(x);       // prints "[1, 7, 7, 8, 9, 10, 5]"
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn splice(blob: Blob, start: int, len: int, replace: Blob)
```

<details>
<summary markdown="span"> details </summary>

Replace a portion of the BLOB with another BLOB.

* If `start` < 0, position counts from the end of the BLOB (`-1` is the last byte).
* If `start` < -length of BLOB, position counts from the beginning of the BLOB.
* If `start` ≥ length of BLOB, the other BLOB is appended to the end of the BLOB.
* If `len` ≤ 0, the other BLOB is inserted into the BLOB at the `start` position without replacing anything.
* If `start` position + `len` ≥ length of BLOB, entire portion of the BLOB after the `start` position is replaced.

# Example

```rhai
let b1 = blob(10, 0x42);
let b2 = blob(5, 0x18);

b1.splice(1, 3, b2);

print(b1);      // prints "[4218181818184242 42424242]"

b1.splice(-5, 4, b2);

print(b1);      // prints "[4218181818184218 1818181842]"
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn split(string: String) -> Array
```

<details>
<summary markdown="span"> details </summary>

Split the string into segments based on whitespaces, returning an array of the segments.

# Example

```rhai
let text = "hello, world! hello, foo!";

print(text.split());        // prints ["hello,", "world!", "hello,", "foo!"]
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn split(string: String, delimiter: char) -> Array
```

<details>
<summary markdown="span"> details </summary>

Split the string into segments based on a `delimiter` character, returning an array of the segments.

# Example

```rhai
let text = "hello, world! hello, foo!";

print(text.split('l'));     // prints ["he", "", "o, wor", "d! he", "", "o, foo!"]
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn split(string: String, index: int) -> Array
```

<details>
<summary markdown="span"> details </summary>

Split the string into two at the specified `index` position and return it both strings
as an array.

The character at the `index` position (if any) is returned in the _second_ string.

* If `index` < 0, position counts from the end of the string (`-1` is the last character).
* If `index` < -length of string, it is equivalent to cutting at position 0.
* If `index` ≥ length of string, it is equivalent to cutting at the end of the string.

# Example

```rhai
let text = "hello, world!";

print(text.split(6));       // prints ["hello,", " world!"]

print(text.split(13));      // prints ["hello, world!", ""]

print(text.split(-6));      // prints ["hello, ", "world!"]

print(text.split(-99));     // prints ["", "hello, world!"]
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn split(blob: Blob, index: int) -> Blob
```

<details>
<summary markdown="span"> details </summary>

Cut off the BLOB at `index` and return it as a new BLOB.

* If `index` < 0, position counts from the end of the BLOB (`-1` is the last byte).
* If `index` is zero, the entire BLOB is cut and returned.
* If `index` < -length of BLOB, the entire BLOB is cut and returned.
* If `index` ≥ length of BLOB, nothing is cut from the BLOB and an empty BLOB is returned.

# Example

```rhai
let b1 = blob();

b1 += 1; b1 += 2; b1 += 3; b1 += 4; b1 += 5;

let b2 = b1.split(2);

print(b2);          // prints "[030405]"

print(b1);          // prints "[0102]"
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn split(array: Array, index: int) -> Array
```

<details>
<summary markdown="span"> details </summary>

Cut off the array at `index` and return it as a new array.

* If `index` < 0, position counts from the end of the array (`-1` is the last element).
* If `index` is zero, the entire array is cut and returned.
* If `index` < -length of array, the entire array is cut and returned.
* If `index` ≥ length of array, nothing is cut from the array and an empty array is returned.

# Example

```rhai
let x = [1, 2, 3, 4, 5];

let y = x.split(2);

print(y);           // prints "[3, 4, 5]"

print(x);           // prints "[1, 2]"
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn split(string: String, delimiter: String) -> Array
```

<details>
<summary markdown="span"> details </summary>

Split the string into segments based on a `delimiter` string, returning an array of the segments.

# Example

```rhai
let text = "hello, world! hello, foo!";

print(text.split("ll"));    // prints ["he", "o, world! he", "o, foo!"]
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn split(string: String, delimiter: String, segments: int) -> Array
```

<details>
<summary markdown="span"> details </summary>

Split the string into at most the specified number of `segments` based on a `delimiter` string,
returning an array of the segments.

If `segments` < 1, only one segment is returned.

# Example

```rhai
let text = "hello, world! hello, foo!";

print(text.split("ll", 2));     // prints ["he", "o, world! hello, foo!"]
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn split(string: String, delimiter: char, segments: int) -> Array
```

<details>
<summary markdown="span"> details </summary>

Split the string into at most the specified number of `segments` based on a `delimiter` character,
returning an array of the segments.

If `segments` < 1, only one segment is returned.

# Example

```rhai
let text = "hello, world! hello, foo!";

print(text.split('l', 3));      // prints ["he", "", "o, world! hello, foo!"]
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn split_rev(string: String, delimiter: char) -> Array
```

<details>
<summary markdown="span"> details </summary>

Split the string into segments based on a `delimiter` character, returning an array of
the segments in _reverse_ order.

# Example

```rhai
let text = "hello, world! hello, foo!";

print(text.split_rev('l'));     // prints ["o, foo!", "", "d! he", "o, wor", "", "he"]
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn split_rev(string: String, delimiter: String) -> Array
```

<details>
<summary markdown="span"> details </summary>

Split the string into segments based on a `delimiter` string, returning an array of the
segments in _reverse_ order.

# Example

```rhai
let text = "hello, world! hello, foo!";

print(text.split_rev("ll"));    // prints ["o, foo!", "o, world! he", "he"]
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn split_rev(string: String, delimiter: char, segments: int) -> Array
```

<details>
<summary markdown="span"> details </summary>

Split the string into at most the specified number of `segments` based on a `delimiter` character,
returning an array of the segments.

If `segments` < 1, only one segment is returned.

# Example

```rhai
let text = "hello, world! hello, foo!";

print(text.split('l', 3));      // prints ["o, foo!", "", "hello, world! he"
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn split_rev(string: String, delimiter: String, segments: int) -> Array
```

<details>
<summary markdown="span"> details </summary>

Split the string into at most a specified number of `segments` based on a `delimiter` string,
returning an array of the segments in _reverse_ order.

If `segments` < 1, only one segment is returned.

# Example

```rhai
let text = "hello, world! hello, foo!";

print(text.split_rev("ll", 2));     // prints ["o, foo!", "hello, world! he"]
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn sqrt(x: float) -> float
```

<details>
<summary markdown="span"> details </summary>

Return the square root of the floating-point number.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn start(range: Range<int>) -> int
```

<details>
<summary markdown="span"> details </summary>

Return the start of the exclusive range.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn start(range: RangeInclusive<int>) -> int
```

<details>
<summary markdown="span"> details </summary>

Return the start of the inclusive range.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn starts_with(string: String, match_string: String) -> bool
```

<details>
<summary markdown="span"> details </summary>

Return `true` if the string starts with a specified string.

# Example

```rhai
let text = "hello, world!";

print(text.starts_with("hello"));   // prints true

print(text.starts_with("world"));   // prints false
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn store_dkim(ctx: Context, result: Map) -> ()
```

<details>
<summary markdown="span"> details </summary>

Store the result produced by the DKIM signature verification in the `ctx()`.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn sub_string(string: String, range: Range<int>) -> String
```

<details>
<summary markdown="span"> details </summary>

Copy an exclusive range of characters from the string and return it as a new string.

# Example

```rhai
let text = "hello, world!";

print(text.sub_string(3..7));   // prints "lo, "
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn sub_string(string: String, start: int) -> String
```

<details>
<summary markdown="span"> details </summary>

Copy a portion of the string beginning at the `start` position till the end and return it as
a new string.

* If `start` < 0, position counts from the end of the string (`-1` is the last character).
* If `start` < -length of string, the entire string is copied and returned.
* If `start` ≥ length of string, an empty string is returned.

# Example

```rhai
let text = "hello, world!";

print(text.sub_string(5));      // prints ", world!"

print(text.sub_string(-5));      // prints "orld!"
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn sub_string(string: String, range: RangeInclusive<int>) -> String
```

<details>
<summary markdown="span"> details </summary>

Copy an inclusive range of characters from the string and return it as a new string.

# Example

```rhai
let text = "hello, world!";

print(text.sub_string(3..=7));  // prints "lo, w"
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn sub_string(string: String, start: int, len: int) -> String
```

<details>
<summary markdown="span"> details </summary>

Copy a portion of the string and return it as a new string.

* If `start` < 0, position counts from the end of the string (`-1` is the last character).
* If `start` < -length of string, position counts from the beginning of the string.
* If `start` ≥ length of string, an empty string is returned.
* If `len` ≤ 0, an empty string is returned.
* If `start` position + `len` ≥ length of string, entire portion of the string after the `start` position is copied and returned.

# Example

```rhai
let text = "hello, world!";

print(text.sub_string(3, 4));   // prints "lo, "

print(text.sub_string(-8, 3));  // prints ", w"
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn tag(value: ?) -> int
```

<details>
<summary markdown="span"> details </summary>

Return the _tag_ of a `Dynamic` value.

# Example

```rhai
let x = "hello, world!";

x.tag = 42;

print(x.tag);           // prints 42
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn tan(x: float) -> float
```

<details>
<summary markdown="span"> details </summary>

Return the tangent of the floating-point number in radians.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn tanh(x: float) -> float
```

<details>
<summary markdown="span"> details </summary>

Return the hyperbolic tangent of the floating-point number in radians.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn time() -> String
```

<details>
<summary markdown="span"> details </summary>

get the current time.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn timestamp() -> Instant
```

<details>
<summary markdown="span"> details </summary>

Create a timestamp containing the current system time.

# Example

```rhai
let now = timestamp();

sleep(10.0);            // sleep for 10 seconds

print(now.elapsed);     // prints 10.???
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn to_array(blob: Blob) -> Array
```

<details>
<summary markdown="span"> details </summary>

Convert the BLOB into an array of integers.

# Example

```rhai
let b = blob(5, 0x42);

let x = b.to_array();

print(x);       // prints "[66, 66, 66, 66, 66]"
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn to_binary(value: int) -> String
```

<details>
<summary markdown="span"> details </summary>

Convert the `value` into a string in binary format.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn to_binary(value: i16) -> String
```

<details>
<summary markdown="span"> details </summary>

Convert the `value` into a string in binary format.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn to_binary(value: i32) -> String
```

<details>
<summary markdown="span"> details </summary>

Convert the `value` into a string in binary format.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn to_binary(value: u8) -> String
```

<details>
<summary markdown="span"> details </summary>

Convert the `value` into a string in binary format.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn to_binary(value: i8) -> String
```

<details>
<summary markdown="span"> details </summary>

Convert the `value` into a string in binary format.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn to_binary(value: u64) -> String
```

<details>
<summary markdown="span"> details </summary>

Convert the `value` into a string in binary format.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn to_binary(value: u16) -> String
```

<details>
<summary markdown="span"> details </summary>

Convert the `value` into a string in binary format.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn to_binary(value: u32) -> String
```

<details>
<summary markdown="span"> details </summary>

Convert the `value` into a string in binary format.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn to_binary(value: i128) -> String
```

<details>
<summary markdown="span"> details </summary>

Convert the `value` into a string in binary format.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn to_binary(value: u128) -> String
```

<details>
<summary markdown="span"> details </summary>

Convert the `value` into a string in binary format.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn to_blob(string: String) -> Blob
```

<details>
<summary markdown="span"> details </summary>

Convert the string into an UTF-8 encoded byte-stream as a BLOB.

# Example

```rhai
let text = "朝には紅顔ありて夕べには白骨となる";

let bytes = text.to_blob();

print(bytes.len());     // prints 51
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn to_chars(string: String) -> Array
```

<details>
<summary markdown="span"> details </summary>

Return an array containing all the characters of the string.

# Example

```rhai
let text = "hello";

print(text.to_chars());     // prints "['h', 'e', 'l', 'l', 'o']"
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn to_debug(array: Array) -> String
```

<details>
<summary markdown="span"> details </summary>

Convert the array into a string.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn to_debug(this: OffsetDateTime) -> String
```

<details>
<summary markdown="span"> details </summary>

Convert a `time::OffsetDateTime` to a `String`
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn to_debug(f: FnPtr) -> String
```

<details>
<summary markdown="span"> details </summary>

Convert the function pointer into a string in debug format.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn to_debug(number: f32) -> String
```

<details>
<summary markdown="span"> details </summary>

Convert the value of `number` into a string.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn to_debug(record: Record) -> String
```

<details>
<summary markdown="span"> details </summary>

Produce a debug output for the parsed [`dmarc::Record`]
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn to_debug(status: Status) -> String
```

<details>
<summary markdown="span"> details </summary>

Convert a `Status` to a debug string
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn to_debug(item: ?) -> String
```

<details>
<summary markdown="span"> details </summary>

Convert the value of the `item` into a string in debug format.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn to_debug(character: char) -> String
```

<details>
<summary markdown="span"> details </summary>

Convert the string into debug format.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn to_debug(number: float) -> String
```

<details>
<summary markdown="span"> details </summary>

Convert the value of `number` into a string.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn to_debug(unit: ()) -> String
```

<details>
<summary markdown="span"> details </summary>

Convert the unit into a string in debug format.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn to_debug(context: Server) -> String
```

<details>
<summary markdown="span"> details </summary>

Convert a `Server` to a debug string.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn to_debug(string: String) -> String
```

<details>
<summary markdown="span"> details </summary>

Convert the string into debug format.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn to_debug(value: bool) -> String
```

<details>
<summary markdown="span"> details </summary>

Convert the boolean value into a string in debug format.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn to_debug(map: Map) -> String
```

<details>
<summary markdown="span"> details </summary>

Convert the object map into a string.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn to_debug(context: Context) -> String
```

<details>
<summary markdown="span"> details </summary>

Convert a `Context` to a debug string.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn to_degrees(x: float) -> float
```

<details>
<summary markdown="span"> details </summary>

Convert radians to degrees.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn to_float(x: u32) -> float
```

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn to_float(x: i16) -> float
```

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn to_float(x: int) -> float
```

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn to_float(x: u8) -> float
```

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn to_float(x: i8) -> float
```

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn to_float(x: u128) -> float
```

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn to_float(x: f32) -> float
```

<details>
<summary markdown="span"> details </summary>

Convert the 32-bit floating-point number to 64-bit.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn to_float(x: u16) -> float
```

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn to_float(x: i128) -> float
```

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn to_float(x: i32) -> float
```

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn to_hex(value: i16) -> String
```

<details>
<summary markdown="span"> details </summary>

Convert the `value` into a string in hex format.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn to_hex(value: u32) -> String
```

<details>
<summary markdown="span"> details </summary>

Convert the `value` into a string in hex format.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn to_hex(value: i8) -> String
```

<details>
<summary markdown="span"> details </summary>

Convert the `value` into a string in hex format.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn to_hex(value: int) -> String
```

<details>
<summary markdown="span"> details </summary>

Convert the `value` into a string in hex format.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn to_hex(value: u16) -> String
```

<details>
<summary markdown="span"> details </summary>

Convert the `value` into a string in hex format.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn to_hex(value: i128) -> String
```

<details>
<summary markdown="span"> details </summary>

Convert the `value` into a string in hex format.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn to_hex(value: u128) -> String
```

<details>
<summary markdown="span"> details </summary>

Convert the `value` into a string in hex format.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn to_hex(value: u64) -> String
```

<details>
<summary markdown="span"> details </summary>

Convert the `value` into a string in hex format.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn to_hex(value: u8) -> String
```

<details>
<summary markdown="span"> details </summary>

Convert the `value` into a string in hex format.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn to_hex(value: i32) -> String
```

<details>
<summary markdown="span"> details </summary>

Convert the `value` into a string in hex format.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn to_int(x: i16) -> int
```

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn to_int(x: i128) -> int
```

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn to_int(x: i32) -> int
```

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn to_int(x: f32) -> Result<int, Box<EvalAltResult>>
```

<details>
<summary markdown="span"> details </summary>

Convert the floating-point number into an integer.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn to_int(x: u128) -> int
```

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn to_int(x: u8) -> int
```

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn to_int(x: u32) -> int
```

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn to_int(x: float) -> Result<int, Box<EvalAltResult>>
```

<details>
<summary markdown="span"> details </summary>

Convert the floating-point number into an integer.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn to_int(x: u16) -> int
```

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn to_int(x: char) -> int
```

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn to_int(x: i8) -> int
```

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn to_int(x: u64) -> int
```

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn to_int(x: int) -> int
```

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn to_json(map: Map) -> String
```

<details>
<summary markdown="span"> details </summary>

Return the JSON representation of the object map.

# Data types

Only the following data types should be kept inside the object map:
`INT`, `FLOAT`, `ImmutableString`, `char`, `bool`, `()`, `Array`, `Map`.

# Errors

Data types not supported by JSON serialize into formats that may
invalidate the result.

# Example

```rhai
let m = #{a:1, b:2, c:3};

print(m.to_json());     // prints {"a":1, "b":2, "c":3}
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn to_lower(string: String) -> String
```

<details>
<summary markdown="span"> details </summary>

Convert the string to all lower-case and return it as a new string.

# Example

```rhai
let text = "HELLO, WORLD!"

print(text.to_lower());     // prints "hello, world!"

print(text);                // prints "HELLO, WORLD!"
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn to_lower(character: char) -> char
```

<details>
<summary markdown="span"> details </summary>

Convert the character to lower-case and return it as a new character.

# Example

```rhai
let ch = 'A';

print(ch.to_lower());       // prints 'a'

print(ch);                  // prints 'A'
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn to_octal(value: u16) -> String
```

<details>
<summary markdown="span"> details </summary>

Convert the `value` into a string in octal format.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn to_octal(value: u128) -> String
```

<details>
<summary markdown="span"> details </summary>

Convert the `value` into a string in octal format.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn to_octal(value: u8) -> String
```

<details>
<summary markdown="span"> details </summary>

Convert the `value` into a string in octal format.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn to_octal(value: u32) -> String
```

<details>
<summary markdown="span"> details </summary>

Convert the `value` into a string in octal format.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn to_octal(value: i128) -> String
```

<details>
<summary markdown="span"> details </summary>

Convert the `value` into a string in octal format.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn to_octal(value: i16) -> String
```

<details>
<summary markdown="span"> details </summary>

Convert the `value` into a string in octal format.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn to_octal(value: u64) -> String
```

<details>
<summary markdown="span"> details </summary>

Convert the `value` into a string in octal format.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn to_octal(value: int) -> String
```

<details>
<summary markdown="span"> details </summary>

Convert the `value` into a string in octal format.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn to_octal(value: i32) -> String
```

<details>
<summary markdown="span"> details </summary>

Convert the `value` into a string in octal format.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn to_octal(value: i8) -> String
```

<details>
<summary markdown="span"> details </summary>

Convert the `value` into a string in octal format.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn to_radians(x: float) -> float
```

<details>
<summary markdown="span"> details </summary>

Convert degrees to radians.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn to_string(character: char) -> String
```

<details>
<summary markdown="span"> details </summary>

Return the character into a string.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn to_string(string: String) -> String
```

<details>
<summary markdown="span"> details </summary>

Return the `string`.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn to_string(number: float) -> String
```

<details>
<summary markdown="span"> details </summary>

Convert the value of `number` into a string.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn to_string(item: ?) -> String
```

<details>
<summary markdown="span"> details </summary>

Convert the value of the `item` into a string.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn to_string(unit: ()) -> String
```

<details>
<summary markdown="span"> details </summary>

Return the empty string.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn to_string(_: Context) -> String
```

<details>
<summary markdown="span"> details </summary>

Convert a `Context` to a `String`.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn to_string(map: Map) -> String
```

<details>
<summary markdown="span"> details </summary>

Convert the object map into a string.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn to_string(_: Server) -> String
```

<details>
<summary markdown="span"> details </summary>

Convert a `Server` to a `String`.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn to_string(array: Array) -> String
```

<details>
<summary markdown="span"> details </summary>

Convert the array into a string.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn to_string(status: Status) -> String
```

<details>
<summary markdown="span"> details </summary>

Convert a `Status` to a `String`
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn to_string(this: OffsetDateTime) -> String
```

<details>
<summary markdown="span"> details </summary>

Convert a `time::OffsetDateTime` to a `String`
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn to_string(value: bool) -> String
```

<details>
<summary markdown="span"> details </summary>

Return the boolean value into a string.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn to_string(number: f32) -> String
```

<details>
<summary markdown="span"> details </summary>

Convert the value of `number` into a string.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn to_upper(string: String) -> String
```

<details>
<summary markdown="span"> details </summary>

Convert the string to all upper-case and return it as a new string.

# Example

```rhai
let text = "hello, world!"

print(text.to_upper());     // prints "HELLO, WORLD!"

print(text);                // prints "hello, world!"
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn to_upper(character: char) -> char
```

<details>
<summary markdown="span"> details </summary>

Convert the character to upper-case and return it as a new character.

# Example

```rhai
let ch = 'a';

print(ch.to_upper());       // prints 'A'

print(ch);                  // prints 'a'
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn trim(string: String)
```

<details>
<summary markdown="span"> details </summary>

Remove whitespace characters from both ends of the string.

# Example

```rhai
let text = "   hello     ";

text.trim();

print(text);    // prints "hello"
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn truncate(array: Array, len: int)
```

<details>
<summary markdown="span"> details </summary>

Cut off the array at the specified length.

* If `len` ≤ 0, the array is cleared.
* If `len` ≥ length of array, the array is not truncated.

# Example

```rhai
let x = [1, 2, 3, 4, 5];

x.truncate(3);

print(x);       // prints "[1, 2, 3]"

x.truncate(10);

print(x);       // prints "[1, 2, 3]"
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn truncate(string: String, len: int)
```

<details>
<summary markdown="span"> details </summary>

Cut off the string at the specified number of characters.

* If `len` ≤ 0, the string is cleared.
* If `len` ≥ length of string, the string is not truncated.

# Example

```rhai
let text = "hello, world! hello, foobar!";

text.truncate(13);

print(text);    // prints "hello, world!"

x.truncate(10);

print(text);    // prints "hello, world!"
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn truncate(blob: Blob, len: int)
```

<details>
<summary markdown="span"> details </summary>

Cut off the BLOB at the specified length.

* If `len` ≤ 0, the BLOB is cleared.
* If `len` ≥ length of BLOB, the BLOB is not truncated.

# Example

```rhai
let b = blob();

b += 1; b += 2; b += 3; b += 4; b += 5;

b.truncate(3);

print(b);           // prints "[010203]"

b.truncate(10);

print(b);           // prints "[010203]"
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn user_exist(name: String) -> bool
```

<details>
<summary markdown="span"> details </summary>

Does the `name` correspond to an existing user in the system.

# Examples

```
  connect: [
    rule "user_exist" || {
      accept(`250 root exist ? ${if user_exist("root") { "yes" } else { "no" }}`);
    }
  ],
  mail: [
    rule "user_exist (obj)" || {
      accept(`250 ${user_exist(mail_from())}`);
    }
  ]
}
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn user_exist(name: SharedObject) -> bool
```

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn values(map: Map) -> Array
```

<details>
<summary markdown="span"> details </summary>

Return an array with all the property values in the object map.

# Example

```rhai
let m = #{a:1, b:2, c:3};

print(m.values());      // prints "[1, 2, 3]""
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn verify_dkim(message: Message, signature: Signature, key: PublicKey) -> ()
```

<details>
<summary markdown="span"> details </summary>

Operate the hashing of the `message`'s headers and body, and compare the result with the
`signature` and `key` data.

# Examples

```
Received: from github.com (hubbernetes-node-54a15d2.ash1-iad.github.net [10.56.202.84])
	by smtp.github.com (Postfix) with ESMTPA id 19FB45E0B6B
	for <mlala@negabit.com>; Wed, 26 Oct 2022 14:30:51 -0700 (PDT)
DKIM-Signature: v=1; a=rsa-sha256; c=relaxed/relaxed; d=github.com;
	s=pf2014; t=1666819851;
	bh=7gTTczemS/Aahap1SpEnunm4pAPNuUIg7fUzwEx0QUA=;
	h=Date:From:To:Subject:From;
	b=eAufMk7uj4R+bO5Nr4DymffdGdbrJNza1+eykatgZED6tBBcMidkMiLSnP8FyVCS9
	 /GSlXME6/YffAXg4JEBr2lN3PuLIf94S86U3VckuoQQQe1LPtHlnGW5ZwJgi6DjrzT
	 klht/6Pn1w3a2jdNSDccWhk5qlSOQX9JKnE7UD58=
Date: Wed, 26 Oct 2022 14:30:51 -0700
From: Mathieu Lala <noreply@github.com>
To: mlala@negabit.com
Message-ID: <viridIT/vSMTP/push/refs/heads/test/rule-engine/000000-c6459a@github.com>
Subject: [viridIT/vSMTP] c6459a: test: add test on message
Mime-Version: 1.0
Content-Type: text/plain;
 charset=UTF-8
Content-Transfer-Encoding: 7bit
Approved: =?UTF-8?Q?hello_there_=F0=9F=91=8B?=
X-GitHub-Recipient-Address: mlala@negabit.com
X-Auto-Response-Suppress: All

  Branch: refs/heads/test/rule-engine
  Home:   https://github.com/viridIT/vSMTP
  Commit: c6459a4946395ba90182ce7181bdbc327994c038
      https://github.com/viridIT/vSMTP/commit/c6459a4946395ba90182ce7181bdbc327994c038
  Author: Mathieu Lala <m.lala@viridit.com>
  Date:   2022-10-26 (Wed, 26 Oct 2022)

  Changed paths:
    M src/vsmtp/vsmtp-rule-engine/src/api/message.rs
    M src/vsmtp/vsmtp-rule-engine/src/lib.rs
    M src/vsmtp/vsmtp-test/src/vsl.rs

  Log Message:
  -----------
  test: add test on message


; // .eml ends here

  preq: [
    rule "verify_dkim" || {
      verify_dkim();
      if !get_header("Authentication-Results").contains("dkim=pass") {
        return deny();
      }
      // the result of dkim verification is cached, so this call will
      // not recompute the signature and recreate a header
      verify_dkim();

      // FIXME: should be one
      if count_header("Authentication-Results") != 2 {
        return deny();
      }

      accept();
    }
  ]
}
```

Changing the header `Subject` will result in a dkim verification failure.

```
Received: from github.com (hubbernetes-node-54a15d2.ash1-iad.github.net [10.56.202.84])
	by smtp.github.com (Postfix) with ESMTPA id 19FB45E0B6B
	for <mlala@negabit.com>; Wed, 26 Oct 2022 14:30:51 -0700 (PDT)
DKIM-Signature: v=1; a=rsa-sha256; c=relaxed/relaxed; d=github.com;
	s=pf2014; t=1666819851;
	bh=7gTTczemS/Aahap1SpEnunm4pAPNuUIg7fUzwEx0QUA=;
	h=Date:From:To:Subject:From;
	b=eAufMk7uj4R+bO5Nr4DymffdGdbrJNza1+eykatgZED6tBBcMidkMiLSnP8FyVCS9
	 /GSlXME6/YffAXg4JEBr2lN3PuLIf94S86U3VckuoQQQe1LPtHlnGW5ZwJgi6DjrzT
	 klht/6Pn1w3a2jdNSDccWhk5qlSOQX9JKnE7UD58=
Date: Wed, 26 Oct 2022 14:30:51 -0700
From: Mathieu Lala <noreply@github.com>
To: mlala@negabit.com
Message-ID: <viridIT/vSMTP/push/refs/heads/test/rule-engine/000000-c6459a@github.com>
Subject: Changing the header produce an invalid dkim verification
Mime-Version: 1.0
Content-Type: text/plain;
 charset=UTF-8
Content-Transfer-Encoding: 7bit
Approved: =?UTF-8?Q?hello_there_=F0=9F=91=8B?=
X-GitHub-Recipient-Address: mlala@negabit.com
X-Auto-Response-Suppress: All

  Branch: refs/heads/test/rule-engine
  Home:   https://github.com/viridIT/vSMTP
  Commit: c6459a4946395ba90182ce7181bdbc327994c038
      https://github.com/viridIT/vSMTP/commit/c6459a4946395ba90182ce7181bdbc327994c038
  Author: Mathieu Lala <m.lala@viridit.com>
  Date:   2022-10-26 (Wed, 26 Oct 2022)

  Changed paths:
    M src/vsmtp/vsmtp-rule-engine/src/api/message.rs
    M src/vsmtp/vsmtp-rule-engine/src/lib.rs
    M src/vsmtp/vsmtp-test/src/vsl.rs

  Log Message:
  -----------
  test: add test on message


; // .eml ends here

  preq: [
    rule "verify_dkim" || {
      verify_dkim();
      if !get_header("Authentication-Results").contains("dkim=fail") {
        return deny();
      }
      accept();
    }
  ]
}
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn write(srv: Server, mut ctx: Context, message: Message, dir: SharedObject) -> ()
```

<details>
<summary markdown="span"> details </summary>

write the current email to a specified folder.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn write(srv: Server, mut ctx: Context, message: Message, dir: String) -> ()
```

<details>
<summary markdown="span"> details </summary>

write the current email to a specified folder.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn write_ascii(blob: Blob, range: RangeInclusive<int>, string: String)
```

<details>
<summary markdown="span"> details </summary>

Write an ASCII string to the bytes within an inclusive `range` in the BLOB.

Each ASCII character encodes to one single byte in the BLOB.
Non-ASCII characters are ignored.

* If number of bytes in `range` < length of `string`, extra bytes in `string` are not written.
* If number of bytes in `range` > length of `string`, extra bytes in `range` are not modified.

```rhai
let b = blob(8);

b.write_ascii(1..=5, "hello, world!");

print(b);       // prints "[0068656c6c6f0000]"
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn write_ascii(blob: Blob, range: Range<int>, string: String)
```

<details>
<summary markdown="span"> details </summary>

Write an ASCII string to the bytes within an exclusive `range` in the BLOB.

Each ASCII character encodes to one single byte in the BLOB.
Non-ASCII characters are ignored.

* If number of bytes in `range` < length of `string`, extra bytes in `string` are not written.
* If number of bytes in `range` > length of `string`, extra bytes in `range` are not modified.

```rhai
let b = blob(8);

b.write_ascii(1..5, "hello, world!");

print(b);       // prints "[0068656c6c000000]"
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn write_ascii(blob: Blob, start: int, len: int, string: String)
```

<details>
<summary markdown="span"> details </summary>

Write an ASCII string to the bytes within an exclusive `range` in the BLOB.

* If `start` < 0, position counts from the end of the BLOB (`-1` is the last byte).
* If `start` < -length of BLOB, position counts from the beginning of the BLOB.
* If `start` ≥ length of BLOB, the BLOB is not modified.
* If `len` ≤ 0, the BLOB is not modified.
* If `start` position + `len` ≥ length of BLOB, only the portion of the BLOB after the `start` position is modified.

* If number of bytes in `range` < length of `string`, extra bytes in `string` are not written.
* If number of bytes in `range` > length of `string`, extra bytes in `range` are not modified.

```rhai
let b = blob(8);

b.write_ascii(1, 5, "hello, world!");

print(b);       // prints "[0068656c6c6f0000]"
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn write_be(blob: Blob, range: Range<int>, value: int)
```

<details>
<summary markdown="span"> details </summary>

Write an `INT` value to the bytes within an exclusive `range` in the BLOB
in big-endian byte order.

* If number of bytes in `range` < number of bytes for `INT`, extra bytes in `INT` are not written.
* If number of bytes in `range` > number of bytes for `INT`, extra bytes in `range` are not modified.

```rhai
let b = blob(8, 0x42);

b.write_be_int(1..3, 0x99);

print(b);       // prints "[4200004242424242]"
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn write_be(blob: Blob, range: RangeInclusive<int>, value: float)
```

<details>
<summary markdown="span"> details </summary>

Write a `FLOAT` value to the bytes within an inclusive `range` in the BLOB
in big-endian byte order.

* If number of bytes in `range` < number of bytes for `FLOAT`, extra bytes in `FLOAT` are not written.
* If number of bytes in `range` > number of bytes for `FLOAT`, extra bytes in `range` are not modified.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn write_be(blob: Blob, range: Range<int>, value: float)
```

<details>
<summary markdown="span"> details </summary>

Write a `FLOAT` value to the bytes within an exclusive `range` in the BLOB
in big-endian byte order.

* If number of bytes in `range` < number of bytes for `FLOAT`, extra bytes in `FLOAT` are not written.
* If number of bytes in `range` > number of bytes for `FLOAT`, extra bytes in `range` are not modified.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn write_be(blob: Blob, range: RangeInclusive<int>, value: int)
```

<details>
<summary markdown="span"> details </summary>

Write an `INT` value to the bytes within an inclusive `range` in the BLOB
in big-endian byte order.

* If number of bytes in `range` < number of bytes for `INT`, extra bytes in `INT` are not written.
* If number of bytes in `range` > number of bytes for `INT`, extra bytes in `range` are not modified.

```rhai
let b = blob(8, 0x42);

b.write_be_int(1..=3, 0x99);

print(b);       // prints "[4200000042424242]"
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn write_be(blob: Blob, start: int, len: int, value: float)
```

<details>
<summary markdown="span"> details </summary>

Write a `FLOAT` value to the bytes beginning at the `start` position in the BLOB
in big-endian byte order.

* If `start` < 0, position counts from the end of the BLOB (`-1` is the last byte).
* If `start` < -length of BLOB, position counts from the beginning of the BLOB.
* If `start` ≥ length of BLOB, zero is returned.
* If `len` ≤ 0, zero is returned.
* If `start` position + `len` ≥ length of BLOB, entire portion of the BLOB after the `start` position is parsed.

* If number of bytes in `range` < number of bytes for `FLOAT`, extra bytes in `FLOAT` are not written.
* If number of bytes in `range` > number of bytes for `FLOAT`, extra bytes in `range` are not modified.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn write_be(blob: Blob, start: int, len: int, value: int)
```

<details>
<summary markdown="span"> details </summary>

Write an `INT` value to the bytes beginning at the `start` position in the BLOB
in big-endian byte order.

* If `start` < 0, position counts from the end of the BLOB (`-1` is the last byte).
* If `start` < -length of BLOB, position counts from the beginning of the BLOB.
* If `start` ≥ length of BLOB, zero is returned.
* If `len` ≤ 0, zero is returned.
* If `start` position + `len` ≥ length of BLOB, entire portion of the BLOB after the `start` position is parsed.

* If number of bytes in `range` < number of bytes for `INT`, extra bytes in `INT` are not written.
* If number of bytes in `range` > number of bytes for `INT`, extra bytes in `range` are not modified.

```rhai
let b = blob(8, 0x42);

b.write_be_int(1, 3, 0x99);

print(b);       // prints "[4200000042424242]"
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn write_le(blob: Blob, range: RangeInclusive<int>, value: float)
```

<details>
<summary markdown="span"> details </summary>

Write a `FLOAT` value to the bytes within an inclusive `range` in the BLOB
in little-endian byte order.

* If number of bytes in `range` < number of bytes for `FLOAT`, extra bytes in `FLOAT` are not written.
* If number of bytes in `range` > number of bytes for `FLOAT`, extra bytes in `range` are not modified.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn write_le(blob: Blob, range: RangeInclusive<int>, value: int)
```

<details>
<summary markdown="span"> details </summary>

Write an `INT` value to the bytes within an inclusive `range` in the BLOB
in little-endian byte order.

* If number of bytes in `range` < number of bytes for `INT`, extra bytes in `INT` are not written.
* If number of bytes in `range` > number of bytes for `INT`, extra bytes in `range` are not modified.

```rhai
let b = blob(8);

b.write_le_int(1..=3, 0x12345678);

print(b);       // prints "[0078563400000000]"
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn write_le(blob: Blob, range: Range<int>, value: int)
```

<details>
<summary markdown="span"> details </summary>

Write an `INT` value to the bytes within an exclusive `range` in the BLOB
in little-endian byte order.

* If number of bytes in `range` < number of bytes for `INT`, extra bytes in `INT` are not written.
* If number of bytes in `range` > number of bytes for `INT`, extra bytes in `range` are not modified.

```rhai
let b = blob(8);

b.write_le_int(1..3, 0x12345678);

print(b);       // prints "[0078560000000000]"
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn write_le(blob: Blob, range: Range<int>, value: float)
```

<details>
<summary markdown="span"> details </summary>

Write a `FLOAT` value to the bytes within an exclusive `range` in the BLOB
in little-endian byte order.

* If number of bytes in `range` < number of bytes for `FLOAT`, extra bytes in `FLOAT` are not written.
* If number of bytes in `range` > number of bytes for `FLOAT`, extra bytes in `range` are not modified.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn write_le(blob: Blob, start: int, len: int, value: float)
```

<details>
<summary markdown="span"> details </summary>

Write a `FLOAT` value to the bytes beginning at the `start` position in the BLOB
in little-endian byte order.

* If `start` < 0, position counts from the end of the BLOB (`-1` is the last byte).
* If `start` < -length of BLOB, position counts from the beginning of the BLOB.
* If `start` ≥ length of BLOB, zero is returned.
* If `len` ≤ 0, zero is returned.
* If `start` position + `len` ≥ length of BLOB, entire portion of the BLOB after the `start` position is parsed.

* If number of bytes in `range` < number of bytes for `FLOAT`, extra bytes in `FLOAT` are not written.
* If number of bytes in `range` > number of bytes for `FLOAT`, extra bytes in `range` are not modified.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn write_le(blob: Blob, start: int, len: int, value: int)
```

<details>
<summary markdown="span"> details </summary>

Write an `INT` value to the bytes beginning at the `start` position in the BLOB
in little-endian byte order.

* If `start` < 0, position counts from the end of the BLOB (`-1` is the last byte).
* If `start` < -length of BLOB, position counts from the beginning of the BLOB.
* If `start` ≥ length of BLOB, zero is returned.
* If `len` ≤ 0, zero is returned.
* If `start` position + `len` ≥ length of BLOB, entire portion of the BLOB after the `start` position is parsed.

* If number of bytes in `range` < number of bytes for `INT`, extra bytes in `INT` are not written.
* If number of bytes in `range` > number of bytes for `INT`, extra bytes in `range` are not modified.

```rhai
let b = blob(8);

b.write_le_int(1, 3, 0x12345678);

print(b);       // prints "[0078563400000000]"
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn write_utf8(blob: Blob, range: RangeInclusive<int>, string: String)
```

<details>
<summary markdown="span"> details </summary>

Write a string to the bytes within an inclusive `range` in the BLOB in UTF-8 encoding.

* If number of bytes in `range` < length of `string`, extra bytes in `string` are not written.
* If number of bytes in `range` > length of `string`, extra bytes in `range` are not modified.

```rhai
let b = blob(8);

b.write_utf8(1..=5, "朝には紅顔ありて夕べには白骨となる");

print(b);       // prints "[00e69c9de3810000]"
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn write_utf8(blob: Blob, range: Range<int>, string: String)
```

<details>
<summary markdown="span"> details </summary>

Write a string to the bytes within an exclusive `range` in the BLOB in UTF-8 encoding.

* If number of bytes in `range` < length of `string`, extra bytes in `string` are not written.
* If number of bytes in `range` > length of `string`, extra bytes in `range` are not modified.

```rhai
let b = blob(8);

b.write_utf8(1..5, "朝には紅顔ありて夕べには白骨となる");

print(b);       // prints "[00e69c9de3000000]"
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn write_utf8(blob: Blob, start: int, len: int, string: String)
```

<details>
<summary markdown="span"> details </summary>

Write a string to the bytes within an inclusive `range` in the BLOB in UTF-8 encoding.

* If `start` < 0, position counts from the end of the BLOB (`-1` is the last byte).
* If `start` < -length of BLOB, position counts from the beginning of the BLOB.
* If `start` ≥ length of BLOB, the BLOB is not modified.
* If `len` ≤ 0, the BLOB is not modified.
* If `start` position + `len` ≥ length of BLOB, only the portion of the BLOB after the `start` position is modified.

* If number of bytes in `range` < length of `string`, extra bytes in `string` are not written.
* If number of bytes in `range` > length of `string`, extra bytes in `range` are not modified.

```rhai
let b = blob(8);

b.write_utf8(1, 5, "朝には紅顔ありて夕べには白骨となる");

print(b);       // prints "[00e69c9de3810000]"
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn |(x: u128, y: u128) -> u128
```

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn |(x: i8, y: i8) -> i8
```

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn |(x: u32, y: u32) -> u32
```

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn |(x: i16, y: i16) -> i16
```

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn |(x: u16, y: u16) -> u16
```

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn |(x: u64, y: u64) -> u64
```

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn |(x: i32, y: i32) -> i32
```

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn |(x: u8, y: u8) -> u8
```

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn |(x: i128, y: i128) -> i128
```

</div>
</br>

