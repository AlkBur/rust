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
