# Spoiler alert

This code contains the questions and answers verbatim. Don't read it if you are interested in taking the quiz!

    caterwaul.offline(':all', function () {
      $('#contents').empty().append(question_container() -se- questions(it.filter('.quiz')) /~push/ show_score)

      -where [question_container()                         = jquery in h1('Javascript quiz') + div.quiz,
              question(xs = arguments)(ui, total, maximum) = ui.empty() /~append/ jquery [div.question[q] + div.interaction(div.choices[answers()] + div.explanation /hide())]
                                                             -then- f
                                                             -where [q                             = xs[0],
                                                                     f                             = future(),
                                                                     answer(x)                     = jquery in button[x[0]] /click(x[1] /-choose/ x[2]),
                                                                     answers()                     = Array.prototype.slice.call(xs, 1) *answer /[x0 /~add/ x] -seq,

                                                                     choose(score, explanation)(e) = children.toggle() -then-
                                                                                                     explanation_div.empty() /~append/ explanation /~append/ next_button_for(score)
                                                                                                     -where [interaction            = $(this).parents('.interaction').first(),
                                                                                                             children               = interaction.children(),
                                                                                                             explanation_div        = children.filter('.explanation'),

                                                                                                             next_button_for(score) = jquery in button('next >>')
                                                                                                                                      /click("f(ui, total + score, maximum + 100)".qf)]],

              show_score(ui, total, maximum)               = ui /~text/ "score: #{total / maximum * 100 /!Math.round}%",

              questions(ui) = question(jquery [p('Question 1: Which method is automatically called on x when the expression below is evaluated?'),
                                               pre('// assume typeof x === "object" and x !== null\nx == 5')],

                                       ['toNumber',      0, 'Nope, toNumber is not defined in the Javascript spec.'],
                                       ['toString',      0, 'Nope, toString is defined in the spec but is not used here.'],
                                       ['valueOf',     100, 'That is correct. Javascript coerces non-primitives to primitives using the valueOf() method.'],
                                       ['None of these', 0, 'Nope, valueOf() is called to coerce the object into a number.'])(ui, 0, 0)

                  /~flat_map/ question(jquery [p('Question 2: Which Javascript native constructor has this property for some value of x? (Assume the constructor does not raise an error)'),
                                               pre('(new ctor(x)).constructor !== ctor')],

                                       ['Function',      0, 'Nope, Function instances retain their constructor.'],
                                       ['Object',      100, 'That is correct. If x is 5, for instance, then new Object(x) returns an instance of Number, whose superclass is Object.'],
                                       ['Array',         0, 'Nope, all array constructor return values are arrays.'],
                                       ['RegExp',        0, 'Nope, all RegExp constructor return values are regular expressions.'],
                                       ['None of these', 0, 'Nope, the Object constructor returns subclasses of Object, which have the above property.'])

                  /~flat_map/ question(jquery [p('Question 3: Where does .constructor come from?'),
                                               ol(li('It is inherited from Object.prototype.'),
                                                  li('It is a magic property (like __proto__) that always points to the constructor function for each object.'),
                                                  li('It is an immutable property of every prototype and is automatically initialized by Javascript when you create a constructor.'),
                                                  li('It is a mutable property of every prototype and is automatically initialized by Javascript when you create a constructor.'))],

                                       ['Option 1',      0, 'Nope, if it were inherited from Object then it would always point to Object and never to a subclass.'],
                                       ['Option 2',      0, 'Nope, if this were the case then the answer to question 2 would have been "none of these".'],
                                       ['Option 3',     50, 'Nope, but close. The property is, unfortunately, mutable.'],
                                       ['Option 4',    100, 'That is correct. You can easily cause objects to misrepresent their constructors by changing ctor.prototype.constructor.'],
                                       ['None of these', 0, 'Nope, the constructor property is a mutable attribute of the prototype that Javascript initializes for you.'])

                  /~flat_map/ question(jquery [p('Question 4: Most Javascript precedence tables are incorrect about ternary operator precedence. How is this expression grouped?'),
                                               pre('a = b ? c = d : e = f'),
                                               ol(li(code('(a = b) ? (c = d) : (e = f)')),
                                                  li(code('a = (b ? (c = d) : (e = f))')),
                                                  li(code('(a = (b ? (c = d) : e)) = f')))],

                                       ['Option 1',      0, 'Nope, the ternary operator is right-associative and has the same precedence as =.'],
                                       ['Option 2',    100, 'That is correct. The ternary operator has the same precedence and associativity as =.'],
                                       ['Option 3',      0, 'Nope, = is right-associative.'],
                                       ['None of these', 0, 'Nope, the ternary operator has the same precedence and associativity as =.'])

                  /~flat_map/ question(jquery [p('Question 5: Which xor implementation is correct? (Assume that the parameter "x" can take on arbitrary value; its truthiness should be used.)'),
                                               pre('// Method 1:\n',
                                                   'Boolean.prototype.xor = function (x) {\n  return this !== x;\n}'),
                                               pre('// Method 2:\n',
                                                   'Boolean.prototype.xor = function (x) {\n  return this.valueOf() !== x.valueOf();\n}'),
                                               pre('// Method 3:\n',
                                                   'Boolean.prototype.xor = function (x) {\n  return !this !== !x;\n}'),
                                               pre('// Method 4:\n',
                                                   'Boolean.prototype.xor = function (x) {\n  return !+this !== !+x;\n}')],

                                       ['Method 1',   0, 'Nope, this quickly fails if x is not a boolean.'],
                                       ['Method 2',   0, 'Nope, this fails if x is null or undefined, since neither of these values supports the valueOf() method.'],
                                       ['Method 3',   0, 'Nope, this fails because "this" is an object and is therefore always truthy under !-coercion.'],
                                       ['Method 4', 100, 'That is correct. The unary +-coercion is necessary to reduce Boolean instances to primitive form prior to logical negation.'])

                  /~flat_map/ question(jquery [p('Question 6: What is the value of the following expression?'),
                                               pre('(function (x) {\n',
                                                   '  x.foo = "bar";\n',
                                                   '  if (x !== false) throw new Error("eek");\n',
                                                   '  return x.foo;\n',
                                                   '})(false)')],

                                       ['undefined',   100, 'That is correct. Javascript constructs a temporary object, assigns to its "foo" property, and then discards it.'],
                                       ['"bar"',         0, 'Nope, property assignment onto primitive values silently fails to happen.'],
                                       ['an error',      0, 'Nope, x remains equal to false the whole time.'],
                                       ['None of these', 0, 'Nope, the expression returns undefined because of autoboxing.'])

                  /~flat_map/ question(jquery [p('Question 7: Suppose you have this code:'),
                                               pre('var f = function (c) {\n',
                                                   '  return function (a, b) {\n',
                                                   '    return a(b);\n',
                                                   '  };\n',
                                                   '};\n',
                                                   'var r = function (code) {return new Function(code)};\n',
                                                   'var g = f(mystery_value);'),
                                              p('Which expression will return mystery_value?')],

                                       ['g(eval, "c")',                 50, 'Close, but nope. c is not even stored in the inner function scope, so there is no way to retrieve it.'],
                                       ['g(r, "return c")',              0, 'Nope, the Function constructor always compiles functions into the global environment.'],
                                       ['g(eval, "arguments.callee.c")', 0, 'Nope, closure variables are not stored as attributes on function objects.'],
                                       ['None of these',               100, 'That is correct. c cannot be retrieved because it is not stored in the inner function\'s scope chain.'])

                  /~flat_map/ question(jquery [p('Question 8: What does this expression do? (Assume that "y" has not been previously defined in the outer scope)'),
                                               pre('(function (x) {\n',
                                                   '  y = x;\n',
                                                   '  if (y) var y = true;\n',
                                                   '  return y;\n',
                                                   '})(false) || y')],

                                       ['throws a ReferenceError', 100, 'That is correct. The function will return false, causing the outer "y" to be evaluated. But "y" is function-scoped.'],
                                       ['returns false',             0, 'Nope, "y" is scoped to the function because of the "var" modifier. "var" does not need to be executed to impact scope.'],
                                       ['returns undefined',         0, 'Nope, the inner "y" is function-scoped, so the outer "y" refers to an undefined variable.'],
                                       ['None of these',             0, 'Nope, this expression throws a ReferenceError because the global "y" is undefined.'])

                  /~flat_map/ question(jquery [p('Question 9: Most Javascript precedence tables are incorrect about the precedence of the "new" operator. What does this expression do?'),
                                               pre('(function () {\n  return new new new new new\n  Function.constructor("return Function")()\n  .constructor("this.x = Date")().x;\n})()'),
                                               p('(Note that the line breaks do not trigger automatic semicolon insertion in this code.)')],

                                       ['the same thing as "new Date()"', 100, 'That is correct. Each "new" binds until it reaches the first function call to its right, and the last "new" ' +
                                                                               'implicitly invokes .x as a constructor on an empty argument list.'],
                                       ['returns the Date constructor',    50, 'Close, but nope. .x is invoked as a constructor function because of the leftmost "new".'],
                                       ['throws a TypeError',               0, 'Nope, this expression returns a value and does not throw any errors.'],
                                       ['None of these',                    0, 'Nope, this expression returns an instance of Date. Each "new" modifies exactly one function invocation.'])

                  /~flat_map/ question(jquery [p('Question 10: For which value of x is the following expression always true, including immediately after executing "y = x"?'),
                                               pre('x !== y')],

                                       ['undefined',     0, 'Nope, undefined === undefined.'],
                                       ['void 0',        0, 'Nope, void 0 === undefined, and also void 0 === void 0.'],
                                       ['null',          0, 'Nope, null === null.'],
                                       ['NaN',         100, 'That is correct. NaN is not equal to any value, including itself.'],
                                       ['{}',            0, 'Nope, if x = {} and y = x, then x !== y will return false.'],
                                       ['None of these', 0, 'Nope, NaN is not equal to any value, including itself.'])

                  /~flat_map/ question(jquery [p('Question 11: Which of these statements is/are true?')],

                                       ['!(NaN instanceof Number)',   33, 'This statement is true, but so are the others.'],
                                       ['typeof NaN === "number"',    33, 'This statement is true, but so are the others.'],
                                       ['NaN.constructor === Number', 33, 'This statement is true, but so are the others.'],
                                       ['All of these',              100, 'That is correct. These statements are all true.'])

                  /~flat_map/ question(jquery [p('Question 12: After executing the code below, what is the behavior of the expression "pathological()"?'),
                                               pre('var f = function () {return 1};\n',
                                                   'var g = function () {return 2};\n',
                                                   'var h = function () {return 3};\n',
                                                   'var pathological = function () {\n',
                                                   '  return f()\n',
                                                   '  /h()/g()\n',
                                                   '};')],

                                       ['returns 1/6',      100, 'That is correct. The line is continued because / can be interpreted as a binary operator.'],
                                       ['returns 1',         50, 'Close, but nope. The line is continued because / can be interpreted as a binary operator.'],
                                       ['throws a TypeError', 0, 'Nope. Even if the second line were interpreted as a regular expression, it would never be executed.'],
                                       ['None of these',      0, 'Nope, it returns 1/6.'])

                  /~flat_map/ question(jquery [p('Question 13: What does this expression do?'),
                                               pre('new new Function')],

                                       ['returns an anonymous class instance', 100, 'That is correct. The rightmost "new" constructs an empty function, which is then invoked via "new".'],
                                       ['returns undefined',                     0, 'Nope, an object is returned.'],
                                       ['returns null',                          0, 'Nope, an object is returned.'],
                                       ['throws a TypeError',                    0, 'Nope, the expression evaluates without errors.'])],
      using.caterwaul});