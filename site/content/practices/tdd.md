---
title: Test-Driven Development
weight: 1
type: docs
---

{{< callout type="info" >}}This page summarizes James Shore's article on [Test-Driven Development](https://www.jamesshore.com/v2/books/aoad1/test_driven_development) from _The Art of Agile Development_.{{< /callout >}}

**Write Tests First, Let Them Guide Design**

Test-Driven Development (TDD) is a rapid cycle of testing, coding, and refactoring. You write a small test before writing the code that makes it pass. Then you clean up. Repeat. This tight feedback loop catches mistakes almost immediately and naturally produces well-designed, well-tested code.

## Why TDD Works

Modern compilers give instant feedback on syntax errors. TDD applies the same principle to _intent_—it verifies that code does what you think it should do, often every 20-30 seconds. When something goes wrong, there are only a few lines to check. Mistakes become trivially easy to find.

TDD works like double-entry bookkeeping: you express your intent twice, in different ways—first as a test, then as production code. When they match, both are likely correct. When they don't, you know exactly where to look.

Writing the test first also improves design. You're forced to think about how a class will be _used_ rather than how it will be _implemented_. This naturally creates cleaner, more usable interfaces.

## The Red-Green-Refactor Cycle

TDD follows a simple rhythm:

**1. Think** — Identify the smallest increment of behavior you can add, typically requiring fewer than five lines of code. Then think of a test that will fail unless that behavior exists.

**2. Red** — Write the test. Run all tests and watch the new one fail. This confirms your test is actually testing something. If it passes unexpectedly, something is wrong with your understanding.

**3. Green** — Write just enough production code to make the test pass. Don't worry about elegance yet—just make it work. Sometimes hardcoding the answer is fine; you'll refactor in a moment.

**4. Refactor** — With all tests passing, improve the code. Remove duplication, choose better names, simplify. Run tests after each small change to ensure nothing broke.

**5. Repeat** — Start the cycle again with the next small increment.

With practice, you can complete this cycle in under five minutes, often much faster. The key is taking very small steps.

## The Power of Small Increments

Programmers new to TDD are often surprised at how small each step should be. But experienced practitioners take _smaller_ steps, not larger ones. Small increments keep you in control. When something breaks, there's almost nothing to debug.

The goal isn't just to have tests that work—it's to remain in control of your code at all times. You should always know what the code is doing and why. When tests fail unexpectedly (or pass unexpectedly), stop and figure out why before continuing.

## Types of Tests

Not all tests are created equal:

**Unit tests** run entirely in memory and execute at hundreds per second. They test one class or method in isolation. The vast majority of your tests should be unit tests.

**Focused integration tests** verify that your code correctly interacts with external systems (databases, networks, file systems). They're slower—a handful per second—so you should have relatively few of them.

**End-to-end tests** exercise large parts of the system. They're slow, brittle, and hard to maintain. Use them sparingly, if at all. Prefer exploratory testing to verify that unit and integration tests mesh properly.

If your code is hard to unit test, that's a design signal. Tightly coupled code resists testing. The difficulty is telling you something—listen to it.

## TDD and Legacy Code

Legacy code—code without tests, code you're afraid to change—presents a chicken-and-egg problem. You need tests to change safely, but you need to change code to add tests.

Start with "smoke tests" that exercise common scenarios. These won't catch everything, but they'll alert you to major breakages. Then look for "seams"—places where you can strategically interrupt program flow to inject test-friendly alternatives.

Adding tests to legacy code often produces ugly code temporarily. That's okay. Make it worse to make it better—once tests are in place, you can refactor toward cleaner design.

## Common Questions

**What should I test?** Test everything that could possibly break. If you're not absolutely confident that code is correct _and_ won't be accidentally broken by future changes, test it. The only exceptions are truly trivial code with no logic—simple getters and setters.

**How do I test private methods?** You usually don't need to. Start by testing public methods. As you refactor, code moves into private methods, but existing tests still cover the behavior. If you feel compelled to test a private method directly, consider whether it should be extracted into its own class.

**What about UI testing?** Most UI frameworks weren't designed for testability. A common approach is to keep the UI layer extremely thin—just forwarding calls to a presentation layer that contains the actual logic. Test the presentation layer with normal TDD.

## The Learning Curve

TDD has a two-to-three month learning curve. The basic steps are easy; the mindset takes time. Until it clicks, TDD will feel clumsy and slow. Push through—the payoff is substantial.

One word of caution: if you're the only one on your team using TDD, your teammates may break your tests and not fix them. It's better to get the whole team to try it together.

## Results

When TDD becomes habit, debugging nearly disappears. You still make mistakes, but you catch them in seconds rather than hours. You gain confidence to refactor aggressively, knowing the tests will catch errors. The codebase stays clean because improving it is no longer scary.

TDD isn't just about testing. It's about building software in tiny, proven increments—always knowing exactly what your code does and why.

## References

- [James Shore - Test-Driven Development](https://www.jamesshore.com/v2/books/aoad1/test_driven_development) — The primary source for this section, from _The Art of Agile Development_. Includes an excellent worked example and discussion of unit vs. integration testing.
- Kent Beck, _Test-Driven Development: By Example_ (2002) — The foundational book on TDD with extended examples.
- Michael Feathers, _Working Effectively with Legacy Code_ (2004) — Essential reading for applying TDD to existing codebases.
