I am taking a break from this project. I am writing a C compiler first. After it is a working C compiler, I will modify it to become my dream programming language. One being impure functional, containing Rust concepts like `Result` for error handling. Also an intent with the language is going to be for making it a viable option for creating compilers and interpreters.

This language aims to be:
* Modern
* Impure functional
* Simple and bare when it needs to be
* Batteries included when it needs to be
* Able to run on bare metal
* Easy to make fast software

This language **does not** aim to be:
* Garbage collected
* C
* Purely functional
* Inviable for general development
* Manually memory managed

# Where The Language is Right Now
All of tests/stage_1 valid through tests/stage_3 valid. Does not currently generate assembly for stage_3. Unary operators in front of numbers when parsing expressions is currently where I'm stuck at.

# Motivation
The main reason I am making this language is because I am annoyed with how few good options I have when I even set out to make a new programming language; reason two. I don't like when Rust keeps me from making something very dynamic and dangerous. I don't like pure functional programming languages because that's just not how my mind works. I tried Go and liked it until it began presenting values I didn't care for. I thought about using C or C++ but damn those are hard for making compilers. So I settled for Rust as the only con being its safety (of which I don't care for since nothing I write currently requires it). Rust has proven to be really really good for writing compilers or interpreters because its enums can be variants.

The second reason I am making this language is because I just want a language that patches the cons of the others I use. Garbage collection is annoying. While it makes it easy to write complex programs, it similarly makes it hard to write fast programs. Especially when the garbage collector is basically mandatory (\*cough\* D). I like how C++ handles it. I want a programming language that makes it easy to write fast programs so that it is viable for about any type of software including scientific and games. I also want a modern C. Things like module-based imports, a little more safety, ease of development.

# Loss in Drive
I am currently going through loss in drive. I no longer feel I can see this language through to entire implementation. All of this is much to overwhelming. I will probably come back to this at a later time when I understand parsing more.

# Testing
```
$ cargo build
...
$ ./target/debug/oxc.exe ./test/stage_2/not_five.c
Scanner production:
[Keyword(Int), Id("main"), Symbol(LParen), Symbol(RParen), Symbol(LBrace), Keyword(Return), Operator(LogicalNegation), Integer(5), Symbol(Semicolon), Symbol(RBrace)]

Abstract syntax tree:
Func(
    "main",
    Return(
        UnaryOp(
            LogicalNegation,
            Const(
                5
            )
        )
    )
)

Generated assembly:
  .globl _main
_main:
  movl $5, %eax
  cmpl $0, %eax
  xor %eax, %eax
  sete %al
  ret

$ ./not_five
$ echo $?
0
```