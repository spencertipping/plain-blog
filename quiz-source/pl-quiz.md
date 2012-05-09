# Spoiler alert

This code contains the questions and answers verbatim. Don't read it if you are interested in taking the quiz!

    caterwaul.offline(':all', function () {
      $('#contents').empty().append(question_container() -se- questions(it.filter('.quiz')) /~push/ show_score)

      -where [question_container()                         = jquery in h1('Programming language quiz') + p('Scores on this quiz are probably contravariant with employability.') + div.quiz,
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

              questions(ui) = question(jquery [p('Question 1: In which language will the following code print "hello world", assuming no previous definitions?'),
                                               pre('function foo() {\n  echo "hello world";\n}\nfoo;')],

                                       ['Ruby',          0, 'Nope, Ruby has no support for the "function" keyword or the "echo" command.'],
                                       ['Python',        0, 'Nope, Python uses indentation instead of braces.'],
                                       ['Javascript',   50, 'Understandable, but Javascript requires parentheses around arguments and does not support "echo".'],
                                       ['Bash',        100, 'That is correct. Although written in an unusual style, Bash successfully runs this program.'],
                                       ['Scala',         0, 'Nope, Scala does not support the "function" keyword or the "echo" command.'],
                                       ['None of these', 0, 'Nope, Bash successfully runs this code and prints "hello world".'])(ui, 0, 0)

                  /~flat_map/ question(jquery [p('Question 2: Which interpreter will always reject the following code, regardless of what is defined already?'),
                                               pre('def f(x :Integer) :x = 10; end')],

                                       ['python',        0, jquery [p('Nope, Python can handle this code just fine. Type this into the interpreter first:'),
                                                                    pre('Integer = 10\nend = 10')]],
                                       ['irb',         100, 'That is correct. This definition is invalid Ruby because no separator exists between formals and body.'],
                                       ['scala',         0, jquery [p('Nope, Scala can handle it just fine. Type this into the interpreter first:') +
                                                                    pre('class x\nimplicit def int2x(x: Int): x = new x\ntype Integer = Int\ndef end = 5')]],
                                       ['None of these', 0, 'Nope, the code is illegal in Ruby syntax.'])

                  /~flat_map/ question(jquery [p('Question 3: In which language is the following code invalid, regardless of preceding definitions?'),
                                               pre('movq %rax, $42;')],

                                       ['GNU assembler',  50, jquery [p('Almost correct. AT&T-style assemblers move values from left to right, and $42 is a constant. ',
                                                                        'However, it is possible to define an assembler macro to fix it (despite losing access to movq from now on):'),
                                                                      pre('.macro movq x, y\n  addq \\y, \\x\n.endm')]],
                                       ['Javascript',      0, jquery [p('Nope, Javascript runs it just fine. Type this first:'),
                                                                      pre('movq = 3;\nrax = 4;\n$42 = 5;')]],
                                       ['Perl',            0, jquery [p('Nope, Perl runs it just fine. Type this first:'),
                                                                      pre('sub movq {}\nmy %rax;\n')]],
                                       ['Bash',            0, jquery [p('Nope, Bash runs it just fine. Type this first:'),
                                                                      pre('movq() {\n  echo hi\n}')]],
                                       ['None of these', 100, 'That is correct. Given the right preceding definitions, this code works in every language.'])

                  /~flat_map/ question(jquery [p('Question 4: In which language are these two expressions parsed differently?'),
                                               pre('f/x/g\nf /x/g')],

                                       ['Javascript',    0, 'Nope, Javascript treats each one as division.'],
                                       ['Perl',          0, 'Nope, Perl treats each one as a regular expression.'],
                                       ['Ruby',        100, 'That is correct. Ruby uses whitespace to differentiate division from regular expressions.'],
                                       ['None of these', 0, 'Nope, Ruby parses the two expressions differently.'])

                  /~flat_map/ question(jquery [p('Question 5: In which language is the following statement a syntax error?'),
                                               pre('x = y, z;')],

                                       ['C',             0, 'Nope, the comma operator in C evaluates both sides and returns the right.'],
                                       ['Java',        100, 'That is correct. Java does not support the comma operator.'],
                                       ['Javascript',    0, 'Nope, Javascript supports the comma operator.'],
                                       ['Bash',          0, 'Nope, this is perfectly legal in bash. "x" names the program, and "=", "y,", and "z" are its arguments.'],
                                       ['None of these', 0, 'Nope, it is a syntax error in Java.'])

                  /~flat_map/ question(jquery [p('Question 6: In which language will the following code fail to parse and/or run, regardless of preceding definitions?'),
                                               pre('(* x *)')],

                                       ['OCaml',       0, 'Nope, this is a comment in OCaml.'],
                                       ['Scheme',      0, jquery [p('Nope, Scheme runs this just fine. Type this first:'),
                                                                  pre('(define x 5)\n(define (* x y) 10)')]],
                                       ['Common Lisp', 0, jquery [p('Nope, Lisp runs this just fine. Type this first:'),
                                                                  pre('(defmacro * (x y) \'nil')]],
                                       ['Oberon-2',    0, 'Nope, this is a comment in Oberon-2.'],
                                       ['Smalltalk', 100, 'That is correct. Smalltalk requires operators to be infix.'])

                  /~flat_map/ question(jquery [p('Question 7: In which language is this an invalid function body, regardless of preceding definitions?'),
                                               pre('var x = 10;\nvar y = 10;\nreturn x + y;')],

                                       ['Visual Basic 6', 100, 'That is correct. While Visual Basic does support typeless variables, it does not use this syntax.'],
                                       ['Javascript',       0, 'Nope, this is a canonical Javascript function body.'],
                                       ['Scala',           50, 'Understandable, but this code is valid in Scala due to type inference.'],
                                       ['None of these',    0, 'Nope, this code is invalid in Visual Basic.'])

                  /~flat_map/ question(jquery [p('Question 8: In which programming language does this definition create a list-summing function?'),
                                               pre('sum([]) -> 0;\nsum([X|Xs]) -> X + sum(Xs).')],

                                       ['Haskell',  0, 'Nope, Haskell uses = to define things.'],
                                       ['Erlang', 100, 'That is correct.'],
                                       ['Prolog',  50, 'Almost. Prolog uses :- instead of ->, and return values are bound through parameter passing.'],
                                       ['Dylan',    0, 'Nope, Dylan uses "define" to define things.'])

                  /~flat_map/ question(jquery [p('Question 9: In which programming language does this expression have nothing to do with lists?'),
                                               pre('[a b c d e]')],

                                       ['Joy',         0, 'Nope, this is a list in Joy.'],
                                       ['Scheme',      0, 'Nope, this expression is a list in Scheme; [] are equivalent to ().'],
                                       ['Haskell',     0, 'Nope, this expression creates a single-element list in Haskell.'],
                                       ['Smalltalk', 100, 'That is correct. This expression is a block in Smalltalk.'],
                                       ['Ruby',        0, 'Nope, this expression creates a single-element array in Ruby.'])

                  /~flat_map/ question(jquery [p('Question 10: In which language will the following fail to parse?'),
                                               pre('div.m{color: red}')],

                                       ['Perl',          0, 'Nope, it works just fine in Perl.'],
                                       ['Ruby',        100, 'That is correct. The colon form is disallowed in cases where {} would be interpreted as a block.'],
                                       ['CSS',           0, 'Nope, this code is canonical CSS.'],
                                       ['None of these', 0, 'Nope, the code fails in Ruby.'])

                  /~flat_map/ question(jquery [p('Question 11: In which language is the following invalid, regardless of preceding definitions?'),
                                               pre('3 dup cons unswons dup')],

                                       ['GNU sed', 100, 'That is correct. "3 d" is valid, but "u" requires a statement terminator preceding it.'],
                                       ['Forth',     0, 'Nope, this code is perfectly legal in Forth. You just need to define "cons" and "unswons".'],
                                       ['Joy',       0, 'Nope, this code is canonical Joy.'],
                                       ['Scala',     0, jquery [p('Nope, this code works in Scala. Type this first:'),
                                                                pre('def cons = 5\ndef dup = 5\nobject Foo {\n  def dup(x: Int) = this\n  def unswons(x: Int) = this\n}\n' +
                                                                    'implicit def int2foo(x: Int) = Foo')]],
                                       ['Smalltalk', 0, 'Nope, this code is valid Smalltalk. You just need to define "cons", "dup", and "unswons" as methods.'])

                  /~flat_map/ question(jquery [p('Question 12: Which language disallows odd numbers of backtick characters (`) in normal code (i.e. outside of strings, etc)?')],

                                       ['GNU M4',    0, 'Nope, M4 uses backticks to begin strings.'],
                                       ['Haskell', 100, 'That is correct. Haskell uses the backtick for infix function application, and backticks are always paired.'],
                                       ['Clojure',   0, 'Nope, Clojure uses backticks to quasiquote expressions.'],
                                       ['Unlambda',  0, 'Nope, Unlambda uses the backtick to group expressions.'],
                                       ['None of these', 0, 'Nope, Haskell requires an even number of unquoted backticks.'])

                  /~flat_map/ question(jquery [p('Question 13: In which programming language is the following code invalid outside of a function body, regardless of preceding definitions?'),
                                               pre('function foo(x) {\n  return x + 1\n}')],

                                       ['Javascript',    0, 'Nope, this is canonical Javascript.'],
                                       ['Ruby',          0, jquery [p('Nope, strangely enough this is perfectly legal Ruby code, although it is unlikely to do what you want. Type this first:'),
                                                                    pre('def foo(x); 1; end\ndef function; 1; end')]],
                                       ['Scala',       100, 'That is correct. This code fails because "function foo(x)" is not a method call, and because "return" has no surrounding function.'],
                                       ['None of these', 0, 'Nope, it fails in Scala.'])

                  /~flat_map/ question(jquery [p('Question 14: Some programming languages allow you to return multiple values from functions; so, for instance:'),
                                               pre('head(cons(uncons(cons(x, y)))) = x\ntail(cons(uncons(cons(x, y)))) = y'),
                                               p('Assuming that "cons" is monomorphic, in which language is it impossible to define "uncons" to satisfy the above equations?')],

                                       ['Perl',          0, jquery [p('Nope, it works in Perl. You can define them this way:'),
                                                                    pre('sub cons {[@_]}\nsub uncons {@{$_[0]}}')]],
                                       ['Scheme',      100, jquery [p('That is correct. The following formulation, while it seems like it should work, fails in Scheme:'),
                                                                    pre('(define (uncons c) (call/cc (lambda (return)\n  (return (car c) (cdr c)))))')]],
                                       ['Forth',         0, 'Nope, Forth can easily express uncons by pushing two results onto the stack.'],
                                       ['None of these', 0, 'Nope, Scheme is unable to express "uncons" as stated.'])],
      using.caterwaul});