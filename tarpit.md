# Out of the Tar Pit

(I learned of this paper in Rich Hickey's talk [Deconstructing the Database](https://www.youtube.com/watch?v=Cym4TZwTCNU))

## Abstract

> Following Brooks we distinguish accidental from essential difficulty, but disagree with his premise that most complexity remaining in contemporary systems is essential.

## 1 Introduction

> We believe that the major contributor to this complexity in many systems is the handling of state and the burden that this adds when trying to analyse and reason about the
system.

> The classical ways to approach the difficulty of state include object-oriented programming which tightly couples state together with related behaviour, and functional programming which — in its pure form — eschews state and side-effects all together.

## 2 Complexity

> In his classic paper — “No Silver Bullet” Brooks[Bro86] identified four properties of software systems which make building software hard: Complexity, Conformity, Changeability and Invisibility. Of these we believe that Complexity is the only significant one — the others can either be classified as forms of complexity, or be seen as problematic solely because of the complexity in the system.

> The primary status of complexity as the major cause of these other problems comes simply from the fact that being able to understand a system is a prerequisite for avoiding all of them, and of course it is this which complexity destroys.

> the type of complexity we are discussing in this paper is that which makes large systems hard to understand.

# 3 Approaches to Understanding

> There are two widely-used approaches to understanding systems (or components of systems):

> Testing ... is attempting to understand a system from the outside — as a “black box”.

> Informal Reasoning ... is attempting to understand the system by examining it from the inside.

> improvements in informal reasoning will lead to _less errors being created_ whilst all that improvements in testing can do is to lead to _more errors being detected_

> Given a stark choice between investment in testing and investment in simplicity, the latter may often be the better choice because it will facilitate all future attempts to understand the system — attempts of any kind.

# 4 Causes of Complexity

## 4.1 Complexity caused by State

> The reason that many ... errors exist is that the presence of state makes programs hard to understand. It makes them complex.

### 4.1.1 Impact of State on Testing

> The key problem is that a test (of any kind) on a system or component that is in one particular state tells you nothing at all about the behaviour of that system or component when it happens to be in another state.

### 4.1.2 Impact of State on Informal Reasoning

> One of the issues (that affects both testing and reasoning) is the exponential rate at which the number of possible states grows — for every single _bit_ of state that we add we _double_ the total number of possible states.

> If the procedure in question (which is itself stateless) makes use of any other procedure which _is_ stateful — _even indirectly_ — then all bets are off, our procedure becomes _contaminated_ and we can only understand it in the context of state.

## 4.2 Complexity caused by Control

> Control is basically about the order in which things happen.

> When a programmer is forced (through use of a language with implicit control flow) to specify the control, he or she is being forced to specify an aspect of _how_ the system should work rather than simply what is _desired_. Effectively they are being forced to _over-specify_ the problem.

## 4.3 Complexity caused by Code Volume

> This cause is basically in many ways a secondary effect — much code is simply concerned with managing _state_ or specifying _control_.

> it is the easiest form of complexity to _measure_

## 4.4 Other causes of complexity

> unnecessary abstraction, missed abstraction, poor modularity, poor documentation. . .

> Duplication is a prime example of this \[_Complexity breeds complexity_ principle\] — if (due to state, control or code volume) it is not clear that functionality already exists, or it is too complex to understand whether what exists does exactly what is required, there will be a strong tendency to duplicate. This is particularly true in the presence of time pressures.

> significant effort can be required to achieve simplicity. The first solution is often not the most simple, particularly if there is existing complexity, or time pressure. Simplicity can only be attained if it is recognised, sought and prized.

> What we mean by this \[_Power corrups_ principle\] is that, in the absence of language-enforced guarantees (i.e. restrictions on the _power_ of the language) mistakes (and abuses) _will_ happen.

> the more _powerful_ language ..., the harder it is to understand systems constructed in it.

# 5 Classical approaches to managing complexity

TODO

[Back to Table of Contents](#table-of-contents)

----
