# Rust
```rust
let mut iter = IntoIterator::into_iter(v);
loop {
    match iter.next() {
        Some(x) => {
            // тело цикла
        },
        None => break,
    }
}
```
```rust
fn print_prime_numbers_upto(n: i32) {
    println!("Prime numbers lower than {}:", n);
    for x in (2..n).filter(|&i| is_prime(i)) {
        println!("{}", x);
    }
}
```
```rust
extern crate rand;

use std::io;
use std::cmp::Ordering;
use rand::Rng;

fn main() {
   println!("Guess the number!");
   let secret_number = rand::thread_rng().gen_range(1, 101);
   println!("The secret number is: {}", secret_number);
   loop {
       println!("Please input your guess.");
       let mut guess = String::new();
       io::stdin().read_line(&mut guess)
           .expect("Failed to read line");
       let guess: u32 = guess.trim().parse()
           .expect("Please type a number!");
       println!("You guessed: {}", guess);
       match guess.cmp(&secret_number) {
           Ordering::Less => println!("Too small!"),
           Ordering::Greater => println!("Too big!"),
           Ordering::Equal => {
               println!("You win!");
               break;
           }
       }
   }
}
```
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
```rust
fn lexer(bytes: &[u8], mut input: &mut Vec<u8>, mut result: &mut Vec<u8>, mut ptr_input: &mut usize) -> usize {
    println!("bytes {:?}", bytes);
    
    let mut ptr_code = 0;
    loop {
        if bytes[ptr_code]== b',' {
            result.push(input[*ptr_input]);
        }else if bytes[ptr_code]== b'+' {
            if input[*ptr_input] >= 255 {
                input[*ptr_input] = 0;
              }else{
                  input[*ptr_input] += 1;
              }
        }else if bytes[ptr_code]== b'-' {
            if input[*ptr_input] <= 0 {
                input[*ptr_input] = 255;
            }else{
                input[*ptr_input] -= 1;
            }
        }else if bytes[ptr_code]== b'[' {
            ptr_code+=1;
            let delta = lexer(&bytes[ptr_code..], &mut input, &mut result, &mut ptr_input);   
            ptr_code += delta;
            ptr_code -=1;
            println!("delta {}; ptr_code {}", delta, ptr_code);
        }else if bytes[ptr_code]== b']' {
            if *ptr_input < input.len() && input[*ptr_input]!=0 {
                ptr_code = 0;
              }else{
                  ptr_code+=1;
                  break;
              }
        }
        
        ptr_code+=1;
        if ptr_code >= bytes.len() {
            break;
        }
    }
    
    //println!("result {:?}", result);
    
    return ptr_code;    
}


fn brain_luck(code: &str, mut input: Vec<u8>) -> Vec<u8> {
  let bytes = code.as_bytes();

  //let mut ptr_code = 0;
  let mut ptr_input = 0;
  let mut result: Vec<u8> = Vec::new();
  lexer(&bytes[..], &mut input, &mut result, &mut ptr_input);
  
  //result.push(0);
  
  /*
  println!("len input {}; {:?}", input.len(), input);
  
  loop {
      if bytes[ptr_code]== b',' {
          if input[ptr_input] != 255 && input[ptr_input] != 0 {
              result.push(input[ptr_input]);
              println!("add {}; ptr_input {}", input[ptr_input], ptr_input);  
          }
      }else if bytes[ptr_code]== b'[' {
          if ptr_input >= input.len() || ptr_input < 0 || input[ptr_input]==0 {
              loop {
                  ptr_code += 1;
                  if bytes[ptr_code]== b']' {
                      break;
                  }
              } 
          }
          //println!("-> ptr_code={}; INPUT {}", ptr_code, input[ptr_input]);
      }else if bytes[ptr_code]== b']' {
          if ptr_input < input.len() && ptr_input >= 0 && input[ptr_input]!=0 {
              loop {
                  ptr_code -= 1;
                  if bytes[ptr_code]== b'[' {
                      break;
                  }
              }
              ptr_code -= 1;
          }
          //println!("<- ptr_code={}, input {}", ptr_code, input[ptr_input]);
      }else if bytes[ptr_code]== b'+' {
          if input[ptr_input] >= 255 {
              input[ptr_input] = 0;
          }else{
              input[ptr_input] += 1;
          }
      }else if bytes[ptr_code]== b'-' {
          if input[ptr_input] <= 0 {
              input[ptr_input] = 255;
          }else{
              input[ptr_input] -= 1;
          }
      }else if bytes[ptr_code]== b'.' {
          input.remove(ptr_input);    
          println!("len={}", input.len());
      }
      
      ptr_code+=1;
      
      if ptr_code < 0 || ptr_code >= bytes.len() {
          break;
      }
    }
    */
    println!("result {:?}", result);
    
  
    return result
}
```
