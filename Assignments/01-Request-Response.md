# Homework 1: Request/Response

## Purpose (Why should I do this?)

Understanding the Request/Response Cycle is critical to being able to design and implement projects on the Web. In this project, you will practice implementing Flask routes to strengthen your understanding of Request/Response.

Scoring for this project is as follows:

| Criteria | Possible |
| :------: | :------: |
| Favorite Animal | `5` |
| User's Favorite Dessert | `10` |
| Mad Libs | `10` |
| Multiply 2 Numbers | `10` |
| **TOTAL** | **`35`** |

## Getting Started

In your course projects directory, create a folder for this project, and call it something like `Homework-1-Request-Response`. (In general, it's a good idea _not_ to use spaces in folder names, which is why we use dashes instead!).

In a terminal window, navigate to your newly created folder and create a new file called `app.py` by running the following command (hint: remember **NOT** to type the `$`):

```
$ touch app.py
```

Set up a new Git repository in your folder by running:

```
$ git init
$ git add .
$ git commit -m'Initial commit'
```

Go to [GitHub.com] and create a new repository for your project (make sure the box for "Initialize with a README" is **NOT** checked). Then, run the command:

```
$ git remote add origin git@github.com:YOUR_USERNAME/YOUR_REPO_NAME.git
```

Finally, make sure you have installed Flask:

```
$ pip3 install flask
```

## Instructions - Core Challenges

### Hello, World! _(Tutorial)_

Programmers often refer to a "Hello World" project as a _proof-of-concept_ of a new skill (or language, framework, etc) they are learning. It is a project that is so simple, all it does is say hello to the user! Writing "Hello World" projects is a very useful first step in learning to code. Think of it like buying a pair of running shoes, putting them on your feet, going outside, and taking your first step!

Let's create a Hello World project together. Open up your newly created `app.py` file, using your favorite text editor (we recommend VSCode). In it, add the following two lines of code:

```py
from flask import Flask

app = Flask(__name__)
```

These two lines of code accomplish the following:
- Import the Flask library
- Set up our `app` variable so that we can start writing routes.

Now, _below_ the first two lines, add the following lines of code to hear a very special message from our Make School mascot:

```py
@app.route('/')
def homepage():
    """Shows a greeting to the user."""
    return 'Are you there, world? It\'s me, Ducky!'
```

These lines of code accomplish the following:
- The first line, `@app.route('/')`, indicates the URL of the web page we'll need to visit in order to see our result. In this case, it's `/` or the home page.
- The second line, `def homepage():`, defines the **route function**. Whatever this function _returns_ will show up in your browser when you visit the appropriate URL!
- The third line is called a **docstring**, and describes the route in a human-readable way. It's completely optional -- try removing it!
- The fourth line _returns_ the page contents.

We're almost there -- we just need to tell Python how to run our server! To the _very bottom_ of `app.py`, add the following two lines of code:

```py
if __name__ == '__main__':
    app.run(debug=True)
```

Now we're ready to run the code! Open up your terminal, in your project folder, and type the following:

```
$ python3 app.py
```

You should see something like this in your Terminal output:

```
 * Serving Flask app "homework-1" (lazy loading)
 * Environment: development
 * Debug mode: on
 * Running on http://127.0.0.1:5000/ (Press CTRL+C to quit)
 * Restarting with stat
 * Debugger is active!
 * Debugger PIN: 246-619-731
```

Go to the URL [http://localhost:5000](http://localhost:5000) and check out your cool new webpage!!

### Your Favorite Animal _(5 points)_

Now that we've got a Hello World under our belts, let's try something more complicated! Usually, when you build a website, it doesn't consist of just one page - it has _many_ pages. Let's practice creating another!

For my website, I want to show off my favorite animal. **Create a route** for the URL `/penguins` and have it show the text `"Penguins are cute!"`. (**HINT**: To pass the tests, make sure that your text matches exactly.)

Now, try writing another route to show off _your_ favorite animal. Make sure to test your app in the browser to make sure it works!

## Your User's Favorite Animal _(Tutorial)_

Writing a website isn't just about showing off your own interests - it's also about keeping your users happy! Let's make a route where the _user_ can type in their favorite animal - regardless of what it might be - and get a response.

For this, we'll have to use a **route variable**. In your `app.py` file, add the following:

```py
@app.route('/animal/<users_animal>')
def favorite_animal(users_animal):
    """Display a message to the user that changes based on their favorite animal."""
    return f'Wow, {users_animal} is my favorite animal, too!'
```

These lines of code accomplish the following:
- The first line again indicates the URL of the web page we'll need to visit. The angle brackets, `<` and `>`, denote a **route variable** for which the user can type _anything at all_! The value of whatever the user types into the URL will be available in a variable called `users_animal`.
- The second line is the function signature for the route function. It takes in the variable `users_animal`.
- The fourth line returns the result, to be shown on the web page. Note how it uses the variable `users_animal` to construct a response.

Now, try it out! Try typing `localhost:5000/animal/zebra` into your browser and see what happens! You should see a message like the following:

```
Wow, zebra is my favorite animal, too!
```

### Your User's Favorite Dessert _(10 points)_

Now that we've gotten the hang of route variables, let's try another. Write a route `favorite_dessert` for the URL `/dessert/<users_dessert>`. If I visit the URL `/dessert/donuts`, I should see the text: `How did you know I liked donuts?`

### Mad Libs _(10 Points)_

Write a route for the URL `/madlibs/<adjective>/<noun>` which takes in 2 strings and displays a funny (but work-appropriate) story using them! 

### Multiply 2 Numbers _(10 points)_

Next, let's try a more challenging one. Write a route `multiply` that takes in 2 numbers, multiplies them, and displays the results. It should use the URL `/multiply/<number1>/<number2>`, then take in `number1` and `number2` as parameters.

Write the rest of the route function, as follows:
- If I go to the URL `/multiply/5/7`, I should see the result: `5 times 7 is 35`.
- If I go to the URL `/multiply/hello/world`, I should see the result: `Invalid inputs. Please try again by entering 2 numbers!`

**HINT 1**: We can check whether a particular string contains only numbers by using the [isdigit()](https://www.w3schools.com/python/ref_string_isdigit.asp) method, which returns a boolean (`True` or `False`).

**HINT 2**: All route variables are of type `string`, which means you'll need to cast them as integers in order to do the multiplication. You can do so using the built-in [int()](https://www.freecodecamp.org/news/how-to-convert-strings-into-integers-in-python/) method.

## Stretch Challenges

The following exercises are **stretch challenges**, which means that while they aren't strictly required for this assignment, they are _highly encouraged_! Please do not attempt these until you've finished the core challenges.

If you have, then carry on!

### Say N Times

Write a route, `sayntimes`, that will repeat a string a given number of times. It should use the URL `/sayntimes/<word>/<n>`. For example:

- If I go to the URL `/sayntimes/hello/6`, I should see the result: `hello hello hello hello hello hello`
- If I go to the URL `/sayntimes/world/3`, I should see the result: `world world world`
- If I go to the URL `/sayntimes/hello/world`, I should see the result: `Invalid input. Please try again by entering a word and a number!`

**HINT**: Use a for loop to add up lots of small strings into one large string!

Try out your route in the browser! What happens when you use a very large number (e.g. `1000000`)?

### Reverse a String

Write a route, `reverse`, that takes in a string and outputs the string backwards, i.e. with the characters in reverse order:

- If I go to the URL `/reverse/hello`, I should see the result: `elloh`

**HINT**: Use a for loop to loop over each character in the string, starting at the end; add each one to a result string as you go.

### Strange Caps

Write a route `strangecaps` that will output a given word in "strange caps", that is, alternating lowercase and uppercase letters:

- If I go to the URL `/strangecaps/hello`, I should see the result: `hElLo`
- If I go to the URL `/strangecaps/goodbye`, I should see the result: `gOoDbYe`

**HINT 1**: You can use a for loop to iterate over each character in a string, just like you would with a list.

**HINT 2**: You can use the string methods [upper()](https://www.w3schools.com/python/ref_string_upper.asp) and [lower()](https://www.w3schools.com/python/ref_string_lower.asp) to transform a given string into all uppercase or lowercase letters. You'll want to call these methods on just one letter at a time.

### Dice Game

Write a route `dicegame` that chooses a random number from 1 to 6. If the user rolls a 6, they win the game; otherwise, they lose.

- If I go to the URL `/dicegame`, I should see a result like: `You rolled a 2. You lost!`
- If I go to the URL `/dicegame` again, I should see a result like: `You rolled a 6. You won!`
- If I go to the URL `/dicegame` again, I should see a result like: `You rolled a 5. You lost!`

**HINT**: You can use the Python `random` library method [randint()](https://www.w3schools.com/python/ref_random_randint.asp) to generate a random number from 1 to 6.

## Submission

Submit your assignment using [Gradescope](https://gradescope.com).

## Resources

1. [Flask Quick Start Guide](https://flask.palletsprojects.com/en/1.1.x/quickstart/)

