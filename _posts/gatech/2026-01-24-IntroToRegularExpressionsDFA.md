---
toc: true
mermaid: true
hidden: true
math: true
---

### Lexican Analysis (Scanner)
- Reads the input one character at a time
- Groups characters into tokens and sends to parser
- Removes whitespaces and comments
- Encode token types and form typles <token-type, value> and returns to parser
  
123.45 -> <FloatConst, 123.45>  
DaysofWeek -> <VAR, String = DaysOfWeek>  
'+' -> <Operator, Value = +>  

A lexical language is a collection (set) of legal strings that are allowed. 
Lexical rules tell us how to form a legal string. 

### Representations of Strings
Regular expression r (a pattern of characters) and its language L(r)
- Used in many Unix programs (eg grep, vi, etc...)
- Implemented with finite state machine.

#### Basics of Regular Expressions

Collection of all symbols (eg, a, A, 1, #, etc...) is the alphabet of a language. 
Any string has to be prepared by using the alphabet. Alphabet is overall, a set of legal symbols. 

**Metacharacter/metasymbols** are symbols that have special meaning. 
- Defining regex ops like `|`, `(`, `)`, `*`, `+`, etc...
- Escape character `\` to turn off special meanings
- Empty string `ε`, empty set `ϕ = {}`


#### Precedence of Operations
1. Repition (`a*`)
2. Concatentaion (`ab`)
3. Alternation (`a|b`)
   
(Parantheses can be used to change precedence, same as pemdas)

Ex:  
`a|b*` = {a, ε, b, bb, bbb, ...}  
`(a|b)*` = {ε, a, b, ab, ba, aa, bb, aaa, aab, ...}  
`(a|c)*b(a|c)` = Any number of a's and c's (including zero) in any order followed by a single b followed by any number of a's and c's (including zero) in any order. 

#### Unix Style Regular Expressions
- `.` denotes any char in the alphabet
- `[]` character class, allowing range and complement
  - [a-d] smae as [abcd]
  - [^1-3] denotes characters other than 1, 2, or 3
- `+` repeating one or more times
- `?` optional (zero or one time)
- `^` and `$` beginning and end of line

### State machines

Deterministic Finite Auotmata:
- Deterministic: machine is in a state. Upon receipt of a symbol will go to a unique state. The behaviour is repeatable
- Finite: Have a finite number of states
- Automata: Self operating machine

#### Formal Definition of DFA

- Alphabet: Σ
- Set of States: Q
- A transition function: δ : Q × Σ → Q
- One starting state: q₀
- One or more accepting states F ⊆ Q
- Language accepted by a DFA is the set of strings such that the DFA ends up in an accepting state
  - Each string is `c₁c₂...cₙ` with `cᵢ ∈ Σ`
  - States are `qᵢ = δ(qᵢ₋₁, cᵢ)` for `i = 1...n`
  - `qₙ` is an accepting state


DFA's cannot be designed to accept all types of strings. This is because having a finite number of states will never allow us to capture all properties of all possible strings. 

Ex of DFA string recognition:  
- Strings that start out with k zeros followed by k ones
  - Cannot be detected by a DFA. Have to keep track of number of zeros which have been seen thus far
- Strings with an equal number of ones and zeros
  - Cannot be detected by a DFA, same reasoning as above
- Strings with an equal number of strings "01" and "10"
  - Can be detected by a DFA. A 01 can never be followed by another 01, so we can just wait for a 0 to happen and have a small number of states. This proves that it **can** take infinite sized strings depending on context





