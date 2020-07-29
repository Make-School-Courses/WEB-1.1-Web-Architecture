# Homework 2: Forms

## Purpose (Why should I do this?)

You've probably seen forms on nearly every website you've ever visited. For example, on Amazon.com, you can fill out a form to search for a particular item and see relevant results. On Facebook.com, you can fill out forms to sign up, log in, and post a status update!

For this assignment, we'll be practicing using forms in our web applications. This will allow you to collect user data on everything from their username and password to their search query, favorite food, hometown, next move in a chess game... and more!

Scoring for this project is as follows:

| Criteria | Possible |
| :------: | :------: |
| Fro-Yo Ordering | `10` |
| Favorite Things | `10` |
| Secret Message | `10` |
| Calculator | `20` |
| **TOTAL** | **`50`** |


## Getting Started

Clone the [Starter Code]() for this assignment into your projects directory by running the following command:

```
$ git clone ...
```

Then, open up the project folder in your favorite code editor (we recommend VSCode) and open up `app.py` to get started!

## Instructions

### Fro-Yo Ordering _(10 points)_

Let's recreate one of the problems from the last assignment - learning your user's favorite dessert - by creating a mini **fro-yo** (or, frozen yogurt) shop. However, this time we'll be using a **form** to do so to collect our data. This is a more proper, industry-standard way of collecting user data!

First, update the route called `choose_froyo` with the following contents:

```py
@app.route('/froyo')
def choose_froyo():
    """Shows a form to collect the user's Fro-Yo order."""
    return """
    <form action="/froyo_results/" method="GET">
        What is your favorite Fro-Yo flavor? <br/>
        <input type="text" name="froyo_flavor"><br/>
        <input type="submit" value="Submit!">
    </form>
    """
```

Before moving on, let's review each component of an **HTML form**:

1. The `action=` attribute specifies _which URL the user will be sent to_ when they submit the form. Here, the user will be sent to the URL `/froyo_results/`.
1. The `method=` attribute specifies the **HTTP method** the form will use to submit its results. It can be either `GET` or `POST`.
1. At least one `input` field for the user to enter data. An input field with `type="text"` will accept a text input. Each `input` field must contain a `name=` attribute, which will be used to retrieve the data later.
1. A submit button.

After saving your work, start up your server with `python3 app.py` and visit the page `http://localhost:5000/froyo` in your browser. Fill out the form and press the submit button. What happens? Take a look at what is in the URL bar. Where do you go?

Next, create a second route for `show_froyo_results`, with the following contents:

```py
@app.route('/froyo_results')
def show_froyo_results():
    users_froyo_flavor = request.args.get('froyo_flavor')
    return f'You ordered {users_froyo_flavor} flavored Fro-Yo!'
```

Here, we're using a **dictionary** called `request.args`, which stores all of the data that the user entered into the form as **key-value pairs**. We can retrieve each piece of user-entered data from the dictionary using `.get()`.

***CHECK FOR UNDERSTANDING***: Why did we use `request.args`, and not `request.form`?

Save your work, and try out your route again by re-submitting the form. Do you see a result?

Next, **add another input field for the user to enter what toppings they want.** To do so, you'll need to do the following:

1. Add another HTML `input type="text"` field to the `choose_froyo` route for toppings. Make sure to give it a unique `name=` attribute that's different than the one we already used for the flavor.
1. Add some extra text above the input tag to tell the user what to type in.
1. In the `show_froyo_results` route, create another variable to store the user's chosen toppings. Use `request.form` to get the toppings and store it in the variable.
1. Add the variable to the route's output string to show the user what they ordered!

When you're done, try out the route again. When you submit the form, you should see something like:

```
You ordered Lychee flavored Fro-Yo with toppings Mochi, Brownie Bites, and Gummy Bears!
```

### Favorite Things _(10 points)_

Update the `favorites` route to show a form for the user to enter their favorite color, animal, and city. Each of these inputs should be collected in a different text box. The page should submit the results of the form to the URL `/favorite_results` when the user presses the submit button.

Then, update the `favorite_results` route to show the user the following sentence (with `purple`, `penguin`, and `San Francisco` changed to whichever color, animal, and city the user entered):

```
Wow, I didn't know purple penguins lived in San Francisco!
```

### Secret Message _(10 points)_

Update the `secret_message` to show a form for the user to enter a secret message. We want to send this information securely, so make sure your form uses the `method='POST'` attribute. The page should submit the results of the form to the URL `/message_results`.

Then, update the `message_results` route to show the secret message -- with its letters **sorted in alphabetical order**.

**HINT**: Call the `.sort_letters()` method that's included in the starter code!

So, if I enter the phrase `Spongebob Squarepants` into the form field and press submit, I should see the result of:

```
Here's your secret message!
 SSaabbeegnnooppqrstu
```

### Calculator _(20 points)_

Let's recreate the "Calculator" problem from the last homework, by properly using a form!

Take a look at the `calculator` route. It shows a form for the user to enter two numbers, as well as choose an operator from a drop-down menu of `+` (add), `-` (subtract), `*` (multiply), and `/` (divide).

Complete the route `calculator_results` route to show the user the result of the operation. It should also show the two operands and the operation!

**HINT**: All route variables are of type `string`, which means you'll need to cast them as integers in order to do the operations. You can do so using the built-in [int()](https://www.freecodecamp.org/news/how-to-convert-strings-into-integers-in-python/) method.

So, after submitting the form, you should see something like:

```
You chose to add 2 and 5. Your result is: 7
```

## Submission

Submit your assignment using [Gradescope](https://gradescope.com).

## Resources

1. [Processing Request Data in Flask](https://scotch.io/bar-talk/processing-incoming-request-data-in-flask)

<!--
### Animal Facts

First, we'll create a web app that teaches you facts about all of your favorite animals! This will also introduce the concept of **forms** for collecting user data.

Create a route called `choose_animal` with the following contents:

```py
@app.route('/animal')
def choose_animal():
    """Shows a form to collect an animal name."""
    return """
    <form action="/animal_facts/" method="GET">
        Which animal would you like to see facts about?<br/>
        <input type="text" name="animal"><br/>
        <input type="submit" value="Submit!">
    </form>
    """
```

Next, let's create a **dictionary** to store our animal facts in! **Above all of your routes**, create the following **global variable** to hold a dictionary of key-value pairs:

```py
animal_to_fact = {
    'koala': 'The fingerprints of a koala are so indistinguishable from humans that they have on occasion been confused at a crime scene.',
    'otter': 'Sea otters hold hands while they\'re sleeping so they don\'t drift apart.',
    'sloth': 'It takes a sloth two weeks to digest its food.'
}
```

Feel free to add your own animal facts as well! Check out [here](https://www.mentalfloss.com/article/86578/50-incredible-animal-facts-youll-want-share) for more.

Finally, we'll need to create a route to show the results for the user's query. Create a route `show_animal_facts` with the following contents:

```py
@app.route('/animal_facts')
def show_animal_facts():
    """Shows animal facts for a given animal."""
    chosen_animal = request.args.get('animal')
    if chosen_animal in animal_to_fact:
        fact_to_show = animal_to_fact.get(chosen_animal)
        return f'Here is your fact about {chosen_animal}s: {fact_to_show}'
    else:
        return f'Sorry, we don\'t have any facts about {chosen_animal}! Check back later!'
```

Now, test out your routes by entering the name of one of the animals in your dictionary!
-->
