BeautifulSoup
=============

References and links
::::::::::::::::::::

* https://pypi.python.org/pypi/beautifulsoup4
* https://www.crummy.com/software/BeautifulSoup/bs4/doc/

.. code-block:: python

    from bs4 import BeautifulSoup
    soup = BeautifulSoup(html, 'lxml')

Recipes, Tips and Tricks
::::::::::::::::::::::::

How to remove comments from a bs4 element?
------------------------------------------

.. code-block:: python

    from bs4 import Comment
    
    # remove comments
    for comment in soup.findAll(text=lambda text:isinstance(text, Comment)):
        comment.extract()
        
How to remove all the AngularJS bullshit attributes so you can actually read the HTML?
--------------------------------------------------------------------------------------

.. code-block:: python

    # remove angular attributes
    for tag in soup.recursiveChildGenerator():
        if hasattr(tag, 'attrs'):
            tag.attrs = {
                key:value
                for key,value in tag.attrs.items()
                if not key.startswith('ng-')
            }
            
