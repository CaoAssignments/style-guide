# Style Guidelines

Having good coding style makes your code readable and easier to understand for everyone reading it. Treat your programs as if another programmer will continue to maintain the code after you. This includes your future self!

These are the CSE 11 Style Guidelines, based on Google Style Guidelines:

1. **File header:** At the top of your file, include 
   - a 1-4 sentence high-level description about the file that tells the reader the purpose of your file
   - Your name
   - Your email
   - Your PID
   - References to sources used (e.g. write-up, JDK documentation)
2. **Class Header:** Describe in 1-2 sentences the purpose and capabilities of your Class. Talk about important instance variables if there are any. See Guideline #10 for how you will be graded on formatting.
3. **Method Header:** Describe method functionality briefly and mention special cases if there are any. Include arguments and return value descriptions. You also need method headers for all main methods in your code, describing the behavior and parameters `args`. See Guideline #10 for how you will be graded on formatting.
4. **Inline Comments:** If there is a length of code that is left unexplained, take the time to type a **non-redundant** line summarizing this length of code (e.g. `// initialize an int` is redundant, vs. `// set initial length to 10 inches`). It will let others who look at your code understand what's going on without having to spend time understanding your logic first. But don't be too descriptive, as too many comments reduces readability.
    - See examples of this in the book and in the code samples below.
5. **Use proper indenting:** Indent each block of code consistently (e.g., method body, loop body). Line up the lines in the block so that they are all indented to the same degree.
    - See examples of this in the book and in the code samples below.
    - Make sure you use spaces instead of tabs.
    - We recommend that each tab is set to be 4 spaces for Java files.
6. **Use descriptive variable names:** The names of your variables should describe the data they hold. Your variable names should be words (or abbreviations), not single letters.
    - e.g. `a` --> `indexOfApple`; `letter1` and `letter2` --> `lowerCaseLetter` and `upperCaseLetter`
    - **Exception:** If it is a loop index like `i`, `j`, `k`, one char is OK and sometimes preferred.
7. **Avoid using magic numbers:** Magic numbers are direct usages of numerical or text values throughout the code that should be refactored for readability and easier code maintenance, i.e. any value that is **not true, false, null, -1, 0, or 1.** This applies to **chars and string literals** as well (note that even the empty string is a magic number). These values should be stored in a **`private static final`** variable (usually named with caps and underscores). Use the keyword "private", unless we specify to use "public", since most likely no other classes and files need to access these constants. These variable names should also be descriptive and placed in the beginning of the class/method grouped together. For example, `private static final int TWO = 2`; is not descriptive enough; name it after its purpose, like `private static final int LENGTH = 2`;
    - See examples of this in the book and in the code samples below.
    - **Exception:** Magic numbers can be used for testing.
8. **Write short methods**: Keep in mind that you should be optimizing your code after you have understood the problem, planned an approach to your code, written some pseudocode, written the actual code, and have checked that the code behaves correctly. To optimize, break your methods into sub-methods if they are too complicated or long. If you find yourself having to repeat typing similar code (can be copy-pasted), then modularize the code by making a helper method. 
9. **Write short lines**: Each line of code should be no longer than **80 characters**, so it can fit in a reasonable size window. Your vim setup should highlight lines that are longer than 80 characters. You may find that you need to wrap your lines of code to preserve the character limit (examples below). You can do so by following these general principles:
    - Break after a comma *(example 1, 3 and 4)*
    - Break before/after an operator *(example 2 and 5)*
    - Align the new line with the beginning of the expression at the same level of the previous line *(example 4 and 5)*
    - If the above rules lead to confusing code or to code that's squished up against the right margin, indent about 8 spaces instead. *(all examples)*
10. **Add header (javadoc style) comments** for each method in your code. This means using `@param` and `@return` tags and `/** block comment */` style. Describe method functionality briefly and mention special cases if there are some. Describe argument and return types and purposes.

<u>**Example Java File:**</u>
https://github.com/CaoAssignments/style-guide/blob/main/SampleFile.java

## Example Method Code Style:
```java
/**	
 * Return the score of the letter in scrabble.
 *  
 * @param letter The letter in question
 * @return the scrabble value of the letter
 */
private int letterScore(char letter) {
    char lowerCaseLetter = Character.toLowerCase(letter);
    switch (lowerCaseLetter) {
        case CASE_A: return CASE_A_RETURN;
        ...
        case CASE_Z: return CASE_Z_RETURN;
        default: return DEFAULT_RETURN;
    }
}
```
## Example Inline Comment:
```java
private int countCapitalLetters(String word) {
    // counter to keep track of number of letters <- REDUNDANT COMMENT
    int count = 0;
    // iterate through characters and increment count when uppercase
    for (int i = 0; i < word.length(); i++) {
        if (Character.isUpperCase(word.charAt(i))) {
            count++;
        }
    }
   return count;
}
```
## Example Magic Number Refactor:
```java
/**
 * In this example, 7 is used as the max password size. To avoid having
 * to sprinkle the value 7 all over the code, MAX_PASSWORD_SIZE is used
 * instead, which makes more sense. If the max password size needs to
 * be changed, the value is updated everywhere MAX_PASSWORD_SIZE is 
 * used.
 */

// don't do this
public class Foo {
   public void setPassword(String password) {
        if (password.length() > 7) {
            System.out.println(“Password is long!”);
        }
    }
}

// should be refactored to:
public class Foo {
    private static final int MAX_PASSWORD_SIZE = 7;
    private static final String PASSWORD_LONG = “Password is long!”;

    public void setPassword(String password) {
        if (password.length() > MAX_PASSWORD_SIZE) {
            System.out.println(PASSWORD_LONG);
        }
    }
}
```

## Example Line Wrapping Style:
Example 1: calling a method
```java
someMethod(longExpression1, longExpression2, longExpression3,
        longExpression4, longExpression5);
```

Example 2: math expression
```java
longName1 = longName2 * (longName3 + longName4 - longName5)
        + CONSTANT * longname6;
```

Example 3: method header
```java
int someMethod(int anArg, Object anotherArg, String yetAnotherArg,
        Object andStillAnother) {
    ...
}
```

Example 4: method header with a lot of arguments
```java
private static synchronized horkingLongMethodName(int anArg,
        Object anotherArg, String yetAnotherArg,
        Object andStillAnother) {
    ...
}
```
Example 5: conditional statements
```java
if ((condition1 && condition2)
        || (condition3 && condition4)
        || !(condition5 && condition6)) {
    doSomethingAboutIt();
}

// this could also work
if ((condition1 && condition2) || (condition3 && condition4)
        || !(condition5 && condition6)) {
    doSomethingAboutIt();
}
```
If you’re curious, more coding style guides can be found on the Google website.
Google Style Guidelines - https://google.github.io/styleguide/javaguide.html
