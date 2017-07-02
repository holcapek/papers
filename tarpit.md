# Out of the Tar Pit

I learned of this paper in Rich Hickey's talk [Deconstructing the Database](https://www.youtube.com/watch?v=Cym4TZwTCNU).

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

## 5.1 Object-Orientation

> the dominant method of general software development for traditional (von-Neumann) computers, and many of its characteristics spring from a desire to facilitate von-Neumann style (i.e. state-based) computation.

### 5.1.1 State

> idea of encapsulation ... allows the programmer to enforce integrity constraints over an object’s state by regulating access to that state through the access procedures (“methods”)

> if several of the access procedures access or manipulate the same bit of state, then there may be several places where a given constraint must be enforced

> encapsulation-based integrity constraint enforcement is strongly biased toward single-object constraints and it is awkward to enforce more complicated constraints involving multiple objects with this approach

#### Identity and State

> each object is seen as being a uniquely identifiable entity regardless of its attributes. This is known as _intensional_ identity (in contrast with _extensional_ identity in which things are considered the same if their attributes are the same)

> The intrinsic concept of _object identity_ stems directly from the use of state, and is (being part of the paradigm itself) unavoidable.

#### State in OOP

(nothing)

### 5.1.2 Control

(nothing)

### Summary — OOP

(nothing)

## 5.2 Functional Programming

> functional programming has its roots in the completely stateless lambda calculus of Church

### 5.2.1 State

> by avoiding state (and side-effects) the entire system gains the property of _referential transparency_ — which implies that when supplied with a given set of arguments a function will _always_ return exactly the same result

### 5.2.2 Control

> Functional languages do derive one slight benefit when it comes to control because they encourage a more abstract use of control using functionals (such as `fold` / `map`) rather than explicit looping.

### 5.2.3 Kinds of State

> There is in principle nothing to stop functional programs from passing a single extra parameter into and out of every single function in the entire system. ... this approach recreates a single pool of global variables — hence, even though referential transparency is maintained, ease of reasoning is lost

> there is no reason why the functional style of programming cannot be adopted in stateful languages (i.e. imperative as well as impure functional ones)

### 5.2.4 State and Modularity

> Working within a stateful framework it is possible to add state to any component without adjusting the components which invoke it. Working within a functional framework the same effect can only be achieved by adjusting every single component that invokes it to carry the additional information around

> trade-off is between _complexity_ (with the ability to take a shortcut when making some specific types of change) and _simplicity_ (with _huge_ improvements in both testing and reasoning)

> the main weakness of functional programming is the flip side of its main strength — namely that problems arise when (as is often the case) the system to be built must maintain state of some kind

### 5.2.5 Summary — Functional Programming

(nothing)

## 5.3 Logic Programming

> Together with functional programming, logic programming is considered to be a declarative style of programming because the emphasis is on specifying what needs to be done rather than exactly how to do it.

> Pure logic programming is the approach of doing nothing more than making statements _about_ the problem (and desired solutions).

> Every pure Prolog program can be “read” in two ways — either as a _pure set of logical axioms_ ..., or _operationally_ — as a sequence of commands which are applied (in a particular order) to determine whether a goal can be deduced (from the axioms).

> a single Prolog program can be both correct when read in the first way, and incorrect (for example due to non-termination) when read in the second.

### 5.3.1 State

(nothing)

### 5.3.2 Control

> an _implicit_ ordering for the processing of sub-goals (left to right), and also an _implicit_ ordering of clause application (top down) — these basically correspond to an operational commitment to _process_ the program in the same order as it is read textually

> some particular ways of writing down the program can lead to non-termination

### 5.3.3 Summary — Logic Programming

(nothing)

# 6 Accidents and Essence

> Essential Complexity is inherent in, and the essence of, the _problem_ (as seen by the _users_).

> Accidental Complexity is all the rest — complexity with which the development team would not have to deal in the ideal world

> In order to justify these two definitions we start by considering the role of a software development team — namely to produce (using some given language and infrastructure) and maintain a software system which serves the purposes of its users.

> what is essential to the team is what the _users_ have to be concerned with

> if the user doesn’t even _know what something is_ (e.g. a thread pool or a loop counter — to pick two arbitrary examples) then it cannot possibly be essential

# 7 Recommended General Approach

> complexity could not _possibly_ be avoided even in the ideal world ... is basically how we _define_ essential

## 7.1 Ideal World

> We are going to need to derive formal requirements from the informal ones.

> it is crucial that the formalisation be done without adding any _accidental_ aspects at all.

> formalisation must be done with _no view to execution whatsoever_.

> effectively what we have just described is in fact the very _essence_ of _declarative programming_ — i.e. that you need only specify _what_ you require, not _how_ it must be achieved.

### 7.1.1 State in the ideal world

> aim for state in the ideal world is to get rid of it ... hoping that most state will turn out to be _accidental state_.

#### Input Data

(nothing)

#### Essential Derived Data — Immutable

> can always be re-derived (from the input data — i.e. from the _essential state_) whenever required.

> we do _not_ need to store it ... it is clearly _accidental state_.

#### Essential Derived Data — Mutable

> As with immutable essential derived data, this can be excluded (and the data re-derived on demand) and hence corresponds to _accidental state_.

> Mutability of derived data makes sense only where the function (logic) used to derive the data has an inverse

> An inverse often exists where the derived data represents simple restructurings of the input data. In this situation modifications to the data can simply be treated identically to the corresponding modifications to the existing _essential state_.

#### Accidental Derived Data

> State which is _derived_ but _not_ in the users’ requirements is also _accidental state_.

#### Summary — State in the ideal world

> the ideal world removes _all_ non-essential state.

> No caches, no stores of derived calculations of any kind.

### 7.1.2 Control in the ideal world

> control generally can be completely omitted from the ideal world and as such is considered entirely _accidental_.

> It typically won’t be mentioned in the informal requirements and hence should not appear in the formal requirements (because these are derived with _no view to execution_).

> These are precisely the lessons which logic programming teaches us, ... that control can be separated completely.

### 7.1.3 Summary

(nothing)

## 7.2 Theoretical and Practical Limitations
