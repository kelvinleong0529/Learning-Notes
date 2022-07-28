# **Test-Driven Development**
## 1. Automatic Regression Detection
- sometime we might introduce a bug in the program that might cause code that used to function properly to no longer do so, this is called **regression**
- regression might sneak by unnoticed for a long time if we dont have any automated testing
- If we write tests for every bug we fix, we can guarantee that we didnt introduce any old bug / new bug
## 2. Bold Refactoring
- When we try to refactor codes, automated testing can help us cover the edge cases (extreme cases) and ensure we won't break the code logic or functionality when we make any changes
## 3. Documentation
- Other developers can look at the unit tests to see how the code was designed to be used
- Indirectly acting as a Documentation
## 4. Robustness
- Automated testing ensure our application becomes robust when it gets more complex