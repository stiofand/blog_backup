## Foundational functional programming, part I

### The return of the once-popular

**Functional programming** (*FP*) is a well-discussed area of software development that seems to be making a resurgence once more, after losing a little ground to Object Orientated approaches (OO) particularly from the 80's to now. This was largely due to a rise in popularity of languages like C++, Java, and more recently C# and similar. However, perhaps somewhat paradoxically, many of these popular languages are now trying harder than ever to provide a strong degree of functional behavior. In some aspects, this has even led to the hybridization' of a language to more functional platforms. This predominantly is in languages that ship their own runtimes, like JVM or MLR, from these has arisen languages such as Scala, Kotlin, Groovy, Clojure, R. Additionally new FP languages based on older runtimes have seen a new boost in popularity such as Elixir which runs on the Erlang Runtime, and even more significant still is the rise in popularity of once common languages, such as Erlang, and the Lisp languages, once almost redundant throwbacks to the 60s and 70's now being found in many modern codebases around the world.

### Not Rocket Science

Despite this resurgence, there remains a good degree of mystery and misconception about what FP actually is. Hopefully, this article can shed a little of that mystery and show that really it's not some black magic or some involved rocket science like category theory implementation. In some aspects yes there is some degree of complexity as FP has always been a strong foundation to mathematical and scientific research and implementation, here the more "purer" FP like languages, such as Haskell have dominated and often led to the misconception about the complexity of programming in this manner, but these are the edge cases, the areas where FP evolved, where *lambda calculus,* *monads*, and *category theory* are words to wrestle with. 

### In the world of mortals

Back in the world of us, mortals, FP is far more general and far less involved, it's more removed from its purer scientific foundations, it provides an approach to programming that opens up a degree of flexibility and opportunity for more focused code, less code in some aspects, more robust code, testable, predictable and cleaner, well in some eyes it does anyhow. What it is not, is any specific language, platform, or framework, these are nothing but tools to aid in more functional approaches to writing software. Then what on earth is it?

Functional programming, at its core, is a *paradigm*, that is a way of viewing and approaching writing code, how to implement software in the most optimal and simplest way possible, the exact code for the job it does. It's perspective on the wider picture, not how it should do it but what it does. Throughout this series, there will be a number of terms, such as idempotency, pure, side-effects, which may seem daunting at first but merely represent the way to think about code when you write it.

### Symptoms of functional ability

Ok so this explanation so far is all well and good, but in practice, what makes something functional where it may not be elsewhere. Well, thankfully, there are some symptoms, features, or markers which functional programming exhibits, and go some way to thinking about the FP approach to programming. These are certainly not exhaustive features, but they are, some more clear examples of how the paradigm is approached. Later we will see some simple examples of this in code. 

- **Expressions over Statements**:

Firstly in FP, as the name suggests, the nucleus of the approach is the function. The unit of code that does some particular job with a particular outcome. Now, this is nothing new to any of us, even in the OO world. However, the difference here, is that in FP the unit of work, the function must always return something, in this sense all functions are valid expressions in FP, a unit of code that returns a value.

- **Paradigm of declarative programming**

Now there is much debate about this, but at its core, FP suggests you approach code from its particular units of intention. In the code, you describe what is the desired outcome, not how it is undertaken. This can be difficult to grasp for beginners, but the logic provides for working on the desired transformation of the data not how it works. This is one large separating facet from OO, which usually describes how something is and what it does. This will be clearer in the examples in this series, for now, think of it as I want to calculate the VAT on x amount, I don't care how it's done, but the returned value should be x + vat:

- **Avoidance of Side-Effects, and State (*purity*)**

In FP, the concept of Global State is largely eschewed, the concept revolves around the rather obscure term of purity. This basically provides that in the FP paradigm, functions should only work on their own input and output without changing the wider scope or affecting any external resource. Despite the obsession, many FP proponents have with obtaining this purity Nirvana, it's a difficult position to achieve, and in some aspects, impossible, particularly in domains like web apps, and services. So what does this side effect mean? Well, it's fundamentally a change in a non-functional scope resource, like app state, or an IO action such as a console log or println or print statement, a call to an action that does not return a value. It can be an update of a referenced value that is not in the current scope of the function (like a global), such changes are common to many languages, and the concept of avoiding any alteration of values in memory is one feature that sometimes stumps newcomers. In fact, in javascript there are many functions that act on types that alter the type rather than return a new copy of the type, such approach is considered an anti-pattern to FP.

- **The First class function & Higher-order function (HOC)**

Now, this is not necessarily an FP trait, but the concept arose from the FP paradigm, though you have probably come across the term quite often. At its bare bones, first class functions are functions they can be passed about like objects , they can be used as parameters to other functions and assigned to variable references. This makes things like composition (see below) far more facile. HOC's are functions that can take other functions as their parameters. This is either as a potential callback in code, or, as is the case in FP the resulting returned value of that function as the actual parameter value (called in place). We will see this in the code later in the series, especially when we look at the order of calls LTR (left to right) in FP. Many languages now support such HOC, including JavaScript, and they are a powerful way of programming and are core facets of functional composition, something else we will look at.

- **Functional composition, currying, and partial application***

More terms to deal with here, but fundamentally, they are building blocks within the FP paradigm, they provide the coder with the ability to construct expressions of different building blocks from other expressions thus not having to bloat functions or repeat oneself. Since FP is a call to simplicity and specificity,  re-use of code is an inherent facet of building expressions, the common idiom DRY (do not repeat yourself) is fully embraced here. Currying and Partial application, are almost converse to HOC, where HOC provides for functions as parameters, Currying, and Partial application provide for returning functions, either whole or partial from an expression. This allows for powerful constructs which can be re-used in many contexts.

### Conclusion to Part I

These are the basic foundational concepts of FP, and as mentioned previously, are not exhaustive. There are many faces to FP, some more complex than the simple overview mentioned here. How we actually implement these will be shown in examples, in the next installments, and as you will see there is nothing particularly complex, and hopefully, the core concept of FP will shine through. After that, we will discuss in more depth the advantages and disadvantages of FP, is it something you should embrace strive for, or something which fits in all areas? We shall see. Stay tuned!
