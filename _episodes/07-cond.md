---
title: Making Choices
teaching: 30
exercises: 0
questions:
- "How can my programs do different things based on data values?"
objectives:
- "Write conditional statements including `if`, `elif`, and `else` branches."
- "Correctly evaluate expressions containing `and` and `or`."
keypoints:
- "Use `if condition` to start a conditional statement, `elif condition` to
   provide additional tests, and `else` to provide a default."
- "The bodies of the branches of conditional statements must be indented."
- "Use `==` to test for equality."
- "`X and Y` is only true if both `X` and `Y` are true."
- "`X or Y` is true if either `X` or `Y`, or both, are true."
- "Zero, the empty string, and the empty list are considered false;
   all other numbers, strings, and lists are considered true."
- "`True` and `False` represent truth values."
---

{% include modified.md %}

How can we use Python to automatically recognize the different features in our data,
and take a different action for each? In this lesson, we'll learn how to write code that
runs only when certain conditions are true.

## Conditionals

We can ask Python to take different actions, depending on a condition, with an `if` statement:

~~~
num = 37
if num > 100:
    print('greater')
else:
    print('not greater')
print('done')
~~~
{: .language-python}

~~~
not greater
done
~~~
{: .output}

The second line of this code uses the keyword `if` to tell Python that we want to make a choice.
If the test that follows the `if` statement is true,
the body of the `if`
(i.e., the set of lines indented underneath it) is executed.
If the test is false,
the body of the `else` is executed instead.
Only one or the other is ever executed:

![Executing a Conditional](../fig/python-flowchart-conditional.png)

Conditional statements don't have to include an `else`.
If there isn't one,
Python simply does nothing if the test is false:

~~~
num = 53
print('before conditional...')
if num > 100:
    print(num,' is greater than 100')
print('...after conditional')
~~~
{: .language-python}

~~~
before conditional...
...after conditional
~~~
{: .output}

We can also chain several tests together using `elif`,
which is short for "else if".
The following Python code uses `elif` to print the sign of a number.

~~~
num = -3

if num > 0:
    print(num, 'is positive')
elif num == 0:
    print(num, 'is zero')
else:
    print(num, 'is negative')
~~~
{: .language-python}

~~~
-3 is negative
~~~
{: .output}

Note that to test for equality we use a double equals sign `==`
rather than a single equals sign `=` which is used to assign values.

We can also combine tests using `and` and `or`.
`and` is only true if both parts are true:

~~~
if (1 > 0) and (-1 > 0):
    print('both parts are true')
else:
    print('at least one part is false')
~~~
{: .language-python}

~~~
at least one part is false
~~~
{: .output}

while `or` is true if at least one part is true:

~~~
if (1 < 0) or (-1 < 0):
    print('at least one test is true')
~~~
{: .language-python}

~~~
at least one test is true
~~~
{: .output}

> ## `True` and `False`
> `True` and `False` are special words in Python called `booleans`,
> which represent truth values. A statement such as `1 < 0` returns
> the value `False`, while `-1 < 0` returns the value `True`.
{: .callout}


> ## Count dissenting opinions
>
> In the code below, we loop through a list of cases from the Case Law Api, then
> loop through the opinions for each of those cases. Each `opinion` has a `"type"`
> field which describes if it's a majority opinion, dissenting opinion or concurring opinion. 
> First, try to run the code below to check if you can print out the value of this field for each opinion:
>
> ~~~
> import requests
> import json
> 
> URL = "https://api.case.law/v1/cases/?jurisdiction=ill&full_case=true&decision_date_min=2009-01-01&page_size=20"
> data = requests.get(URL).json()
> 
> cases = data["results"]
> for case in cases:
>     opinions = case["casebody"]["data"]["opinions"]
>     for opinion in opinions:
>         print(opinion["type"])
> ~~~
> {: .language-python}
>
> Now, try to modify the code below to count the number of dissenting opinions by using an `if` test with `opinion["type"]`.
> If you find a dissent, you will need to increase the variable `dissent_count`:
>
> ~~~
> import requests
> import json
> 
> URL = "https://api.case.law/v1/cases/?jurisdiction=ill&full_case=true&decision_date_min=2009-01-01&page_size=20"
> data = requests.get(URL).json()
> 
> dissent_count = 0
> 
> cases = data["results"]
> for case in cases:
>     opinions = case["casebody"]["data"]["opinions"]
>     for opinion in opinions:
>         # Your code here:
> 
> print("Number of dissents:", dissent_count)
> ~~~
> {: .language-python}
>
> > ## Solution
> > ~~~
> > import requests
> > import json
> > 
> > URL = "https://api.case.law/v1/cases/?jurisdiction=ill&full_case=true&decision_date_min=2009-01-01&page_size=20"
> > data = requests.get(URL).json()
> > 
> > dissent_count = 0
> > 
> > cases = data["results"]
> > for case in cases:
> >     opinions = case["casebody"]["data"]["opinions"]
> >     for opinion in opinions:
> >         # Your code here:
> >         if opinion["type"] == "dissent":
> >             dissent_count = dissent_count + 1
> > 
> > print("Number of dissents:", dissent_count)
> > ~~~
> > {: .language-python}
> {: .solution}
{: .challenge}

> ## How Many Paths?
>
> Consider this code:
>
> ~~~
> if 4 > 5:
>     print('A')
> elif 4 == 5:
>     print('B')
> elif 4 < 5:
>     print('C')
> ~~~
> {: .language-python}
>
> Which of the following would be printed if you were to run this code?
> Why did you pick this answer?
>
> 1.  A
> 2.  B
> 3.  C
> 4.  B and C
>
> > ## Solution
> > C gets printed because the first two conditions, `4 > 5` and `4 == 5`, are not true,
> > but `4 < 5` is true.
> {: .solution}
{: .challenge}

> ## What Is Truth?
>
> `True` and `False` booleans are not the only values in Python that are true and false.
> In fact, *any* value can be used in an `if` or `elif`.
> After reading and running the code below,
> explain what the rule is for which values are considered true and which are considered false.
>
> ~~~
> if '':
>     print('empty string is true')
> if 'word':
>     print('word is true')
> if []:
>     print('empty list is true')
> if [1, 2, 3]:
>     print('non-empty list is true')
> if 0:
>     print('zero is true')
> if 1:
>     print('one is true')
> ~~~
> {: .language-python}
{: .challenge}

> ## That's Not Not What I Meant
>
> Sometimes it is useful to check whether some condition is not true.
> The Boolean operator `not` can do this explicitly.
> After reading and running the code below,
> write some `if` statements that use `not` to test the rule
> that you formulated in the previous challenge.
>
> ~~~
> if not '':
>     print('empty string is not true')
> if not 'word':
>     print('word is not true')
> if not not True:
>     print('not not True is true')
> ~~~
> {: .language-python}
{: .challenge}

> ## Close Enough
>
> Write some conditions that print `True` if the variable `a` is within 10% of the variable `b`
> and `False` otherwise.
> Compare your implementation with your partner's:
> do you get the same answer for all possible pairs of numbers?
>
> > ## Solution 1
> > ~~~
> > a = 5
> > b = 5.1
> >
> > if abs(a - b) < 0.1 * abs(b):
> >     print('True')
> > else:
> >     print('False')
> > ~~~
> > {: .language-python}
> {: .solution}
>
> > ## Solution 2
> > ~~~
> > print(abs(a - b) < 0.1 * abs(b))
> > ~~~
> > {: .language-python}
> >
> > This works because the Booleans `True` and `False`
> > have string representations which can be printed.
> {: .solution}
{: .challenge}

> ## In-Place Operators
>
> Python (and most other languages in the C family) provides
> [in-place operators]({{ page.root }}/reference/#in-place-operators)
> that work like this:
>
> ~~~
> x = 1  # original value
> x += 1 # add one to x, assigning result back to x
> x *= 3 # multiply x by 3
> print(x)
> ~~~
> {: .language-python}
>
> ~~~
> 6
> ~~~
> {: .output}
>
> Write some code that sums the positive and negative numbers in a list separately,
> using in-place operators.
> Do you think the result is more or less readable
> than writing the same without in-place operators?
>
> > ## Solution
> > ~~~
> > positive_sum = 0
> > negative_sum = 0
> > test_list = [3, 4, 6, 1, -1, -5, 0, 7, -8]
> > for num in test_list:
> >     if num > 0:
> >         positive_sum += num
> >     elif num == 0:
> >         pass
> >     else:
> >         negative_sum += num
> > print(positive_sum, negative_sum)
> > ~~~
> > {: .language-python}
> >
> > Here `pass` means "don't do anything".
> In this particular case, it's not actually needed, since if `num == 0` neither
> > sum needs to change, but it illustrates the use of `elif` and `pass`.
> {: .solution}
{: .challenge}

> ## Counting Vowels
>
> 1. Write a loop that counts the number of vowels in a character string.
> 2. Test it on a few individual words and full sentences.
> 3. Once you are done, compare your solution to your neighbor's.
>    Did you make the same decisions about how to handle the letter 'y'
>    (which some people think is a vowel, and some do not)?
>
> > ## Solution
> > ~~~
> > vowels = 'aeiouAEIOU'
> > sentence = 'Mary had a little lamb.'
> > count = 0
> > for char in sentence:
> >     if char in vowels:
> >         count += 1
> >
> > print("The number of vowels in this string is " + str(count))
> > ~~~
> > {: .language-python}
> {: .solution}
{: .challenge}

{% include links.md %}
