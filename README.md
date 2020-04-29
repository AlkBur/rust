# Rust
```rust
fn create_phone_number(numbers: &[u8]) -> String {
    let s: String = numbers.into_iter().map(|i| i.to_string()).collect();
    
    format!("({}) {}-{}", &s[..3], &s[3..6], &s[6..])
  
}
```
```rust
impl MorseDecoder {

    fn decode_morse(&self, encoded: &str) -> String {
        encoded
            .trim()
            .split("   ")
            .map(|x| x.split(' ')
                      .filter_map(|y| { self.morse_code.get(y) })
                      .cloned()
                      .collect())
            .collect::<Vec<String>>()
            .join(" ")
    }
    
}
```
```rust
fn seven(mut n: i64) -> (i64, i32) {   
    let mut steps = 0;
    
    while n >= 100 {
        n = (n / 10) - (n % 10 * 2);
        steps += 1;
    }

    (n, steps)
}
```
```rust
fn high(input: &str) -> &str {
    input.split_ascii_whitespace().rev().max_by_key(|s| s.chars().map(|c| c as u16 - 96).sum::<u16>()).unwrap_or("")
}
```
