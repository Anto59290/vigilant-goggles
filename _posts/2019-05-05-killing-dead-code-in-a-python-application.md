---
published: true
layout: post
title: "Killing dead code in a Python application"
category: jekyll
---

Let’s see how to clean your python codebase within minutes.

### WTF is dead code ?

In your codebase your probably have some pieces of code that are never executed at run-time. Those pieces of code are known as dead code. Dead code is a form of technical debt and has many downsides:

* Useless increase of the cognitive workload when reading code. As most of our time as developer is spend on reading code (and not writing it) we should make sure our code is clean and easy to read.

* Can mislead developers on what is done in a specific module or library.

* Make searching and grepping through the codebase less efficient as it will increase the number of non-relevant results.

* Dead code can be using libraries that are no longer needed is the application, which will increase build-time or deploy time. It may also increase the size of your image if you are using Docker for example.

* Dead code slows developers down when doing technical migrations. For example migrating from Python 2.X to Python 3.X or changing your framework version. Migrating dead code is a waste of time and energy so be sure that 100% of your code is used before starting big migrations.

![](https://cdn-images-1.medium.com/max/2000/1*DfFfJjC77-DhWNbsokGMtQ.png)

Having dead code is generally a sign of a lack of rigor and tidiness in a codebase. Nonetheless every project has its dark side with pieces of useless code. This happens for many reasons, generally involving the fear of losing code that might be used one day. It can also be code that was refactored in an hurry or a feature that was written overnight to be shipped in the morning. These emergency situation generally tends to less rigor that might create dead code and technical debt.

## Identifying dead code

Identifying dead code in a Python application can be quite a challenge. The most well known approach is to use coverage to find pieces of useless code. This approach relies on two conditions:

* A very high coverage rate, at least more than 80% if you want to be efficient

* A way to run integration test exclusively, omitting unit tests. If a piece of dead code is covered by a unit test, running only the functional test will allow you to spit it. Most of the Python test runners have a tagging system that can be handy in this situation.

While using this approach you may encounter two types of code:

* Untested code but used in the application. Some tests should be written, if relevant.

* Untested code and unused code: dead code. This code should be deleted.

Even if it works, such a technique can be very long and not very reliable. A lot of false positive (untested code) will appear in the results. This leads us too a dedicated tool to dead dead code in a Python project.

## Vulture

Vulture is a Python package dedicated to dead code identification. The code is available here on Github: [https://github.com/jendrikseipp/vulture](https://github.com/jendrikseipp/vulture). The package is available on Pypi and can be installed via pip install vulture. Once installed you can simply run vulture . to detect dead code in your current directory. For a simpler usage I recommend you two options that will ease your life:

* --min-confidence to set the confidence of the analysis made by vulture. After a few tries setting the confidence to 40 gave good results in our application

* --sort-by-size will sort the output so that the larger pieces of dead code will be printed at the end of the output, facilitating their identification.

For example if I run vulture ./ --min-confidence=60 --sort-by-size in one of our project at BackMarket, it gives me this kind of output:

    foo.py:919: unused function 'get_insurance_foo' (60% confidence, 38 lines)
    merchants/products/utils.py:144: unused class 'GetFooBar' (60% confidence, 48 lines)
    merchants/bar/models.py:19: unused class 'BarFoo' (60% confidence, 67 lines)
    ...

As you can see, this is a much more efficient approach. However they still are a few edge cases where this won’t work. 

If you are using a templating language that calls your Python code (typically via a MVC templating engine or via Jinja templates), the methods or properties that are only used in templates will be flagged as dead code by vulture.

Hidden calls to classes such as middlewares in a Django application won’t be understood by vulture. Same things goes for the hidden calls to methods using getattr. Let’s take a closer look at an example. 

    class Foo(object):

        def foo(self):
            print('I <3 foo')

        def bar(self):
            print('I <3 bar')

        def my_company(self):
            print('BackMarket')

    test_object = Foo()
    test_object.my_company()
    methods = ('foo', 'bar')

    for method in methods:
        callable_method = getattr(test_object, method)
        callable_method()

In this snippet we dynamically call a list of methods of a class using getattr to get the callable. Running this code will work and output the following: 

    BackMarket
    I <3 foo
    I <3 bar

Running vulture on this code will get you this output

    test.py:4: unused function 'foo' (60% confidence)
    test.py:7: unused function 'bar' (60% confidence)

As you can see vulture was able to detect the explicit call to my_company method, but not the ones that are implicit. This is due to the method that use vulture (parsing the AST) and checking for method names.

After a couple of minutes you can easily identify the cases where vulture won’t work. To get a cleaner output I generally use grep to exclude some results:

    vulture . --sort-by-size --min-confidence=40 | grep -v template_tags.py | grep -v tests

This trick allows you to get the cleaner output as possible and therefore be more efficient when cleaning your codebase. Make sure to add this line to your Makefile (or equivalent) to be sure other developers enrich the list and run vulture from time to time.

## The removal process

Now that dead code is identified, it is time to remove it from the codebase. At this point you may encounter opposition from people in your team (if any). Some people feel re-insured by the fact of keeping their old legacy code at hand. “We might need it one day” is probably one sentence you will hear in this situation. At this point it is time for some git (or any version control) pedagogy. The code will never be lost, except if someone rewrite the whole git history.

From a practical point of view I recommend you to submit a lot of small pull request over a large one. I will be easier to review for other developers and will be easier to revert if the code was in fact used.

## Is that all ?

Nope. At that point we had removed thousands of lines of code in our main application and were happy with it. But we also knew that we could do more than that.

Another strategy we used was to check for dead models. To do so used the creation date and modification date we have on most of our objects to find the ones that were old and not modified for a long time. From there we did a manual check of the code, using the powers of modern IDE to have a quick overview of where the model were used. Most of the time, code analysis tools such a Vulture won’t be able to detect such case because the object can be used in many place without having a proper application usage.

All of this is an iterative process. Do it once and for all in your application won’t work, as dead code will probably re-appear at some point. Using Vulture you can easily have a quick check from time to time to ensure a better code quality. 

## Kill it with fire 🔥 !

Is there anything more satisfactory than a pull request deleting useless code ? I don’t think so. Now you have all the tools to clean your project, here is a quick sum up:

* Check your code coverage for untested (maybe unused) chunks of code

* pip install vulture and vulture ./ --min-confidence=60 ---sort-by-sweave continuous deliveryize

* Lots of small pull requests

* Check you database for old models

* Speak with your colleagues about it

* Wait — do it again!

PS: a huge clap to Jendrik Seipp (@[jendrikseipp](https://github.com/jendrikseipp/rednotebook) on github) for providing such an amazing tool as vulture. I also recommended [another of his project: a daily notebook : RedNoteBook](https://github.com/jendrikseipp/rednotebook)





