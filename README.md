# ROCKSTAR

## Timeline & Setting
###       History:
- Rockstar was written by [Dylan Beattie](https://twitter.com/dylanbeattie)
- The language spec was posted on July 21, 2018 and became well known and implemented by the end of Summer to early Fall 2018. This is when articles got posted and some of the implementations started popping up.
- [The Tweet That Started it All](https://twitter.com/paulstovell/status/1013960369465782273)
- Paul Stovell is the Founder/CEO of the [Octopus Deploy](https://octopus.com/) and tweeted one day in frustration directed at technical recuiters that constantly ask for "Rockstar Developers" [[2](#-sources)]
- Dylan Beattie saw this and thought to himself "This is an interesting idea" but thought that someone else would do it. After a few weeks of no new "Rockstar" repos showing up on github. He decided to meld his love for classic rock he grew up listening to and mix it with his love for programming. After a night at a bar with his laptop, he wrote up the [Language Spec](https://github.com/RockstarLang/rockstar/blob/master/spec.md) and posted it to github and [twitter](https://twitter.com/dylanbeattie/status/1020769511086219264?lang=en). [[2](#-sources)]
- Seemingly overnight, the internet fell in love with the Rockstar Programming Language, with interviews in [Classic Rock Magazine ](https://www.loudersound.com/features/meet-the-boffin-behind-a-computer-programming-language-based-on-power-ballads) and discussions on [Hacker News](https://news.ycombinator.com/item?id=17585589). [[2](#-sources)]

###       Usage:
- Rockstar was written as a "joke" language, according to Dylan in his [2019 DOTNEXT Talk](https://www.youtube.com/watch?v=1jg1HqZKeKU). With only the spec written down and posted to github, other programmers started to implement it and open issues on the github page. With such a large boost in popularity and demand for some kind of implementation to use, he used this as an opportunity to practice and explore the process of writing compilers.

###       Tools:
- Due to Rockstar's nature as a joke esoteric programming language, there is no one implementation that is "correct" or "pure" Rockstar, instead there are a slew of implementations that take rockstar file and either compile, transpile, or interpret it. [Full list of implementations](https://github.com/RockstarLang/rockstar) under the implentations heading. Any of these can be used to "work" in rockstar. I ended up using this [link](https://codewithrockstar.com/online) to just write the code online.


## Characteristics
- Note that all of these properties were either explicitly stated or garnered from the [Language Spec](https://github.com/RockstarLang/rockstar/blob/master/spec.md)
- **Paradigm:** Imperative
- **Interpreted / Compiled:** Both Interpreted and Compiled depending on what implementation you follow
- **Typing:** Dymamically Typed

- **Pure / Impure:** Impure

- **Lazy / Strict:** Strict

- **Scoping:** Variables defined outside of functions are in a global scope and anything inside the function is in local scope. These scopes are nested and while inside a local scope you can manipulate variables in the global scope.

###       Implementation Details:
#####         Variables:
- Rockstar has 3 types of variable names:
  - Simple - Simple variables are names that only contain letters, and are case insensitive
  ```
  X is 1
  Y is 2
  Z is nothing
  put x plus y into z
  shout z
  ```
  ```
  3
  ```
  - Common - These are names consisting of keywords like `a` `an` `the` `my` etc. followed by whitespace and a unique variable name with only lowercase letters. This leads to variables like `the boy` being completely different from `my boy`
  ```
  my number is 1
  a number is 2
  your number is nothing
  put my number plus a number into your number
  shout your number
  ```
  ```
  3
  ```
  - Proper - These are names that are proper nouns and can be any word that isn't a keyword, that starts with an uppercase letter.
  ```
  Mark Snyder is 1
  Comparative Programming Languages is 2
  My Grade is nothing
  put Mark Snyder plus Comparative Programming Languages into My Grade
  shout My Grade
  ```
  ```
  3
  ```

#####         Poetic Literals:
- Poetic Literals "allow the programmer to simultaneously initialize a variable and express their innermost angst"
  - Poetic Constant Literals
    - Single line consisting of a variable name and the keyword `is` or one of its aliases (`are` `was` `were`)
    - This is how we declared the variables in the above examples
  - Poetic String Literals
    - Single line consisting of a variable name, followed by the keyword `says` followed by a space. The rest of the line up until the `\n` is treated as an unquoted string
    ```
    John Lennon says Imagine
    shout John Lennon
    ```
    - This is equivalent to the following C code
    ```c
    char* john_lennon = "Imagine";
    printf("%s",john_lennon);
    ```
    - Both outputting
    ```c
    "Imagine"
    ```
  - Poetic Number Literals
    - Single line consisting of a variable name, `is` or one of its aliases. As long as the next simbol is not a Literal, everything else in the line is treated as a decimal number in which the word lengths are that "place's" value. A `.` denotes a decimal place. To allow for zero, each word is modulo 10 to keep us in the power of 10.
    - In the example below, `a` is of length 1, `polynomial` and `depression` is of length 10 giving us `1 % 10`, `10 % 10`, `10 % 10` concatinated together resulting in `100`
    ```
    My Grade is a polynomial depression
    Cherry Pie was red. Undemanding food
    ```
    - This is equivalent to the following C code
    ```c
    int my_grade = 100;
    float cherry_pie = 3.14;
    ```

#####         Typing:
  - Types:
    - *Mysterious* - variables without any value use `mysterious` as a keyword
    - *Null* - just like null everywhere else. Evaluates to 0 and equal to false. Keywords for null: `nothing` `nowhere` `nobody` `gone` etc.
    - *Booleans* - true or false.
      - True: `right` `yes` `ok`
      - False: `wrong` `no` `lies`
    - *Numbers* - double precision floats
    - *Strings* - sequences of 16bit unsigned integers representing UTF-16 code units

#####         Functions:
- Functions are declared with a variable name followed by `takes` and a list of arguements separated by: `and` `,` `&` `, and` `'n'`
```
  Multiply takes rock'n'roll
  Give back rock times roll
```
- Is equivalent to:
```c
  int mul (int x, int y)
  {
    return x * y;
  }
```

###       Data Abstractions:
- There isn't any mention of these types of mechanisms in the language spec. I believe this is because everything is so aliased that adding classes on top of whats already in the language would make it very unwieldy.

## Discussion
###       Hello World:
```
  Shout "Hello World!"
```
###       FizzBuzz:
- Rockstar [FizzBuzz Example](https://github.com/RockstarLang/rockstar/blob/master/examples/fizzbuzz.rock)
- FizzBuzz is program that loops over an incrementing number until it hits some kind of cap (in our case 100), and prints something whenever that number is divisible by some other number. Here whenever `my world` is divisible by `3` or `5` `"Fizz!"` or `"Buzz!"` is printed and `"FizzBuzz!"` is printed instead
```
  Midnight takes your heart and your soul
  While your heart is as high as your soul
  Put your heart without your soul into your heart

  Give back your heart

  Desire is a lovestruck ladykiller
  My world is nothing
  Fire is ice
  Hate is water
  Until my world is Desire,
  Build my world up
  If Midnight taking my world, Fire is nothing and Midnight taking my world, Hate is nothing
  Shout "FizzBuzz!"
  Take it to the top

  If Midnight taking my world, Fire is nothing
  Shout "Fizz!"
  Take it to the top

  If Midnight taking my world, Hate is nothing
  Say "Buzz!"
  Take it to the top

  Whisper my world
```

###       My Motivation:
- I chose to write about Rockstar because I find it's entire existance to be hilarious, entertaining, and educational. I really love how Rockstar really forces the programmer to be creative and have fun while programming by making them write song lyrics in a logical fashion.


## Sources:
###      1. [Language Spec](https://github.com/RockstarLang/rockstar/blob/master/spec.md)
###      2. [Dylan Beattie — How I built Rockstar: Parsing esoteric languages with .NET](https://www.youtube.com/watch?v=1jg1HqZKeKU)
###      3. [Dice.com on Rockstar](https://insights.dice.com/2018/07/27/rockstar-programming-language-developers/)
###      4. [boingboing.net on Rockstar](https://boingboing.net/2018/07/25/hello-cleveland-world.html)
###      5. [Rockstar's Rosetta Code Entry](http://www.rosettacode.org/wiki/Category:Rockstar)
###      6. [Dylan Battie's Classic Rock Magazine Interview](https://www.loudersound.com/features/meet-the-boffin-behind-a-computer-programming-language-based-on-power-ballads)
###      7. [Hacker News Thread](https://news.ycombinator.com/item?id=17585589)
