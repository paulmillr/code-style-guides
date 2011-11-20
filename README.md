# Code style guides
Code style guides for various programming languages

### All languages
* Readability counts.
* Be consistent.
* Less code is better.
* Code duplication is absolutely no-go.
* Flat is better than nested.
* Beautiful is better than ugly.
* Simple is better than complex.

## Python
* Follow official code style guide — PEP8.
* Use introspection (dir() etc.).
* Double quotes are preferred over single.
* Always use the latest python you can.
* Use list comprehensions instead of map()-s and filter()-s. They are clearer
and in the most cases faster. Also python 3 maps/filters return iterators,
nor lists.
* Use python 3 string formatting instead of old '%'. It's a real string method,
not type overloading spike.
* Use list comprehensions instead of map()-s and filter()-s:

    ```python
    # Bad.
    items = map(lambda i: dict(zip(('method', 'params')), i), params.items())
    filter(lambda i: int(i) > 3, lst)

    # Good.
    items = [dict(zip(('method', 'params'), i)) for i in params.items()]
    [i for i in lst if int(i) > 3]
            </code>
          </pre>
        </li>
        <li>Use Python 3 string formatting instead of old '%':
          <pre>
            <code>
    # No.
    '%s * %s = %s' % (item1, item2, item1 * item2)
    '%(username): %(message)' % {'username': u, 'message': m}

    # Yes.
    '{} * {} = {}'.format(item1, item2, item1 * item2)
    '{username}: {message}'.format(username=u, message=m)
    ```

* Use proper indentation:

    ```python
    # Bad.
    client = Client(
        jid, password, jid.split('@').pop(), registercls=True
    )
    # Bad.
    client = Client(jid, password, jid.split('@').pop(),
        registercls=True)

    # This is preferred.
    client = Client(jid, password, jid.split('@').pop(),
                    registercls=True)

    # If you can't do previous (ex.: >80 chars), do this:
    client = Client(
        jid, password,
        jid.split('@').pop(),
        registercls=True
    )
    ```

### JavaScript
* Use two spaces indentation.
* Use prototypes, split your app into modules / objects.
* Single quotes are preferred over double. Reason: HTML uses double quotes.
* Use K&R braces style.
* Always put braces in "if" statements, even in very short ones:

    ```javascript
    // Good
    if (a) {
      ...
    } else {
      ...
    }

    // Good
    if (a) {
      b = 6;
    }

    // Try avoiding ternary operators, they're harder to debug.
    // But if you use, write them like this:
    item = somethingLong ?
      something :
      somethingOther;
    ```

* Use one var per variable:

    ```javascript
    var a = 5;
    var b = 6;
    var $this = $(this);
    // Exception.
    var a, b, c, d, $this;
    ```

* Use 'self' variable to push current context to the closures:

    ```javascript
    var a = {
     b: function() {
       var self = this;
       $(some).click(function(event) {
         self.c();
       });
     }
    };
    ```

* If you're using jQuery, each DOM manipulation should be made through it.
Reason: jquery methods would remain compatible across browsers.

    ```javascript
    // Good.
    $('#item').val();
    $(this).attr('class');

    // Bad.
    this.className;
    document.getElementById('item').value;

    // Every event callback in jQuery should name event data variable as 'event'.
    $('#item').click(function(event) {
      $.storage.set('item', $(this).val());
    });
    ```

* Do not use quotes in object keys:

    ```javascript
    // Bad.
    {'a': 'testtest'}

    // Good.
    {a: 'testtest'}

    // Exception: reserved word.
    {'delete': 'testtest'}
    ```

* Use '===' for comparing instead of '=='. JavaScript is weakly typed
language, so 5 == '5'. This ambiguity could lead to hard-to-find bugs.

    ```javascript
    if (a === 5) {
      ...
    }
    if ($(this).val() === 'something') {
      ...
    }
    if (typeof a === 'undefined') {
      ...
    }

    // Exception: this compares both to 'null' and 'undefined'.
    if (item == null) {
  
    }
    ```

* Other:

    ```javascript
    // Bad.
    $('#contact').hide().filter(function() {return $(this).find('username').length;}).show();

    // Good.
    $('#contact')
      .hide()
      .parent()
      .toggleClass('selected')
      .show();
    ```

* Use "!!" to convert something to boolean value:

    ```javascript
    var loggedIn = !!$.cookie('user');
    ```

* Cache list length into a variable. You could afford 2x loop performance
increase with this on some browsers.

    ```
    for (var i = 0, l = someList.length; i < l; i++) {
      doSomething(someList[i]);
    }
    ```

### CoffeeScript
* Two spaces indentation.
* Use single quotes when you're not interpolating strings
* Separate class / object methods with 1 blank line. Exceptions are one-line methods.
* Use @ instead of 'this'. Exception: standalone `@`.

### HTML
* Two spaces indentation

### CSS
* Two spaces indentation.
* Use CSS3 where you can.
* Use tree-style indentation
* Use one sequence of properties.
* Remember: browser handles selectors RIGHT-TO-LEFT
* Use hex colors (e.g. #fff) instead of color names (e.g. white).

```css
/* Low performance selectors.
   If you're developing a fat web-app with heavy use of CSS, selectors
   optimization is extremely useful for improving page rendering speed.
**/

/*
How browser handles selector 'ul li':

* Get ALL page elements.
* Filter 'li'-s.
* Filter that elements from 'li'-s, where one of ancestors is 'ul'.

How browser handles selector '#main .contact-list-item':

* Get all elements with class 'contact-list-item'.
* Filter ones that has '#main' in ancestors.
* Much faster than previous.

*/

/* Slow */
ul li
/* Slow, but better than previous. */
ul > li

/* Very slow. */
ul li ul li strong
* #promo ul a
[data-hidden="true"]
div > [data-hidden="true"]

/* Also bad, they're overly qualified. */
ul#top-nav
form#login

/* OK. */
.double.active


/* Example. */
.login-page {
  background: #d00; }
  .login-form {
    padding: 5px; }
    .username, .password {
      font-size: 0.9em; }
    .button {
      margin-left: 15px; }

.signup-page {
  background: #0d0; }
  .signup-button {
    padding: 10px;
    background-image: url("../img/signup.png"); }

.chat-page {
  font-size: 0.9em; }
  .identity {
    margin-bottom: 20px; }
    .identity .profile {
      height: 4em; }
    .identity .nickname {
      float: left;
      width: 165px; }
    .identity .avatar {
      float: right; }
    .identity .updates {
      margin-top: 10px; }
    .identity .status {
      height: 30px; }
    .identity .current-mood {
      padding-left: 5px; }
    .identity .button {
      float: right; }

/* Sequence of properties. */
.item {
  position: static;
  z-index: 0;
  top: 0;
  right: 0;
  bottom: 0;
  left: 0;

  display: block;
  visibility: hidden;
  float: none;
  clear: none;
  overflow: hidden;
  clip: rect(0 0 0 0);

  box-sizing: content-box;
  width: auto;
  min-width: 0;
  max-width: 0;
  height: auto;
  min-height: 0;
  max-height: 0;
  margin: 0;
  padding: 0;

  table-layout: fixed;
  empty-cells: show;
  border-spacing: 0;
  border-collapse: collapse;
  list-style: none;

  content: "";
  cursor: default;
  text-align: left;
  vertical-align: top;
  line-height: 1;
  white-space: normal;
  text-decoration: none;
  text-indent: 1;
  text-transform: uppercase;
  letter-spacing: 1;
  word-spacing: normal;

  font: 1em sans-serif;
  font-family: Arial, sans-serif;
  font-size: 1em;
  font-weight: normal;
  font-style: normal;
  font-variant: normal;

  opacity: 1;
  color: #d00;
  text-shadow: 5px 5px 5px #d59;
  border: 1px solid #d00;
  border-radius: 15px;
  box-shadow: inset 1px 0 0 #fff;
  background: #fff url("../i/bg.png") no-repeat 0 0; }
```

### Scala
* Follow [official language style guide](http://davetron5000.github.com/scala-style/index.html).

### Erlang
* Spend an hour reading the official Programming Rules and Conventions. Then follow it.
* Use idiomatic Erlang and functional programming patterns.
* Use types and function specifications and discrepancy analysis.
* Avoid if-s, throw-s and catch-es whenever possible.
* Always consider time and memory complexity:

    ```erlang
    %% DO NOT
    %% Since the ++ operator copies its left operand, the result will be copied again and again and again...
    %% leading to quadratic complexity.
    naive_reverse([H|T]) ->
        naive_reverse(T)++[H];
    naive_reverse([]) ->
        [].

    %% OK
    naive_but_ok_reverse([H|T], Acc) ->
        naive_but_ok_reverse(T, [H]++Acc);
    naive_but_ok_reverse([], Acc) ->
        Acc.

    %% DO
    %% This is slightly more efficient because you don't build a list element only to directly copy it.
    vanilla_reverse([H|T], Acc) ->
        vanilla_reverse(T, [H|Acc]);
    vanilla_reverse([], Acc) ->
        Acc.
    ```

### Other
* Structure your commit message like this:

    ```
    One line summary (less than 50 characters)

    Longer description (wrap at 72 characters)
    ```

* Commit summary:
    * Less than 50 characters
    * What was changed
    * Imperative present tense (fix, add, change): ("Fix bug 123", "Add 'foobar' command, "Change default timeout to 123")
    * End with period
* Commit description:
    * Wrap at 72 characters
    * Why, explain intention and implementation approach
    * Present tense
* Commit atomicity:
    * Break up logical changes
    * Make whitespace changes separately

## Contributors
* Paul Miller
* [Oleg Smirnov](http://nord.org.ua)

## License
The MIT License (MIT)

Copyright (c) 2011 Paul Miller

Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the "Software"), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.
