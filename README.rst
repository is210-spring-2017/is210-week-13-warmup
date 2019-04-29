####################
IS 210 Assignment 13
####################
************
Warmup Tasks
************

:College: CUNY School of Professional Studies
:Course-Name: Software Application Programming I
:Course-Code: IS 210

Overview
========

This exercise will have you interacting with several files. You'll create a
series of functions that will correlate two data sources then write your output
to a report.

Instructions
============

The following tasks will either have you interacting with existing files in
the assignment repository or creating new ones on the fly. Don't forget to add
your interpreter directive, utf-8 encoding, and a short docstring with any new
files that you create!

.. important::

    In these exercises, you may, on occasion, come across a task that requres
    you to research or use a function or method not directly covered by the
    course text. Since Python is such a large language it would be impossible
    for the author to have included descriptions of each and every available
    function which would largely duplicate the offical Python documentation.

    A *vital* skill to successful programming is being comfortable searching
    for and using official language documentation sources like the
    `Python String Documentation`_ page. Throughout our coursework we will be
    practicing both the use of the language in practice and the search skills
    necessary to become functional programmers.

Warmup Tasks
============

Task 01
-------

The goal of this particular exercise is to open and read a CSV file found on
the local filesystem. You'll be creating a function that takes a filename
as a string then returning a summarized version of the data.

The particular data we'll be analyzing is one-month of NYC Restaurant
Inspection data. You'll be returning a boro-average score.

Specifications
^^^^^^^^^^^^^^

#.  Open a new Jupyter notebook

#.  Recreate the following grading scale as a dictionary with float values:

    .. table:: Grades

        ====== =====
        Letter Value
        ====== =====
        A      100%
        B      90%
        C      80%
        D      70%
        F      60%
        ====== =====

#.  Give a quick look at ``inspection_results.csv`` to get a sense of the data
    with which we'll be working.

#.  Create a function named ``get_score_summary()``

    #.  ``get_score_summary()`` takes exactly 1 argument, a string which
        represents the filename whose data will be read and interpreted

    #.  Use the file manipulation tools to open the file and read each line
        of the data. The data is stored as a CSV and is split by commas. The
        first row are headers and each subsequent row lists a restaurateur and
        their violations. This means that each vendor has their data duplicated
        several times.

    #.  Loop through the file data by reading each line and de-duplicating our
        vendors by making a simpler dictionary keyed by just the CAMIS id code
        and the GRADE and BORO as a stored value. You can skip ungraded and
        pending (P) restaurateurs since they don't have enough meaningful data
        to analyze.

        .. tip::

            Don't forget to close your file descriptor after you're done!

    #.  Next, loop through our deduplicated list and create a dictionary that
        counts the number of restaurateus per boro and sums their scores after
        converting them to floats using the grading scale.

    #.  Finally, perform one last data conversion and return a dictionary,
        keyed by boro, whose value is a tuple with the number of restaurateurs
        per boro (who have scores), and the average score (as a float) for that
        boro.

Output
^^^^^^^^

.. code:: pycon

    >>> get_score_summary('inspection_results.csv')
    >>> {'BRONX': (156, 0.9762820512820514), 'BROOKLYN': 
    (417, 0.9745803357314141), 'STATEN ISLAND': (46, 0.9804347826086955), 
    'MANHATTAN': (748, 0.9771390374331531), 'QUEENS': 
    (414, 0.9719806763285017)}

Task 02
-------

Next, we'll be performing a similar transformation with a JSON file. JSON is
one of the most popular data formats available because of its compactness and
portability. The Python ``json`` module will be helping us convert the JSON
file.

Specifications
^^^^^^^^^^^^^^

#.  Start by taking a peek inside ``green_markets.json`` to just get a sense
    of what the data looks like. This particular file is very dense as it
    comes from a professional source and describes all the Green Markets
    currently held in the city. We'll be reducing this data to a count of
    markets per borough.

#.  Use the same notebook as in the prior task

#.  Import the ``json`` module.

#.  Create a function named ``get_market_density()``

    #.  Takes one argument, a filename

    #.  Open a file descriptor for our JSON file and pass the opened file
        object to json's ``load()`` function to return the data as a dictionary

    #.  Loop through the data found in the ``'data'`` and count the number of
        markets per borough, saving the result as a dictionary.

    #.  Return a dictionary of the number of green markets per borough.

Output
^^^^^^^^

.. code:: pycon

    >>> get_market_density('green_markets.json')
    {'STATEN ISLAND': 2, 'BROOKLYN': 48, 'BRONX': 32,
    'MANHATTAN': 39, 'QUEENS': 16}

.. note::

    I forced the borough names to uppercase here to make it easier to correlate
    borough data between the two data sources.
    
.. warning::

    There's a bad record in one of the boro names (it has an extra space -- how would you normalize the name?)

Task 03
-------

Finally, we'll combine these two pieces of data on their borough keys and write
the results to a file. This particular relation is fairly noneventful but it
demonstrates the power of I/O methods in Python quite well.

Specifications
^^^^^^^^^^^^^^

#.  Use the same notebook as before

#.  Create a new function, ``correlate_data()``

    #.  Takes three arguments:

        #.  First argument is the name of a file with restaurant scores data

        #.  Next argument is the name of a JSON file with green_market data

        #.  The final argument is the name of a file that will contain the
            output of this function.

    #.  Use the previous two functions to get aggregate market and restaurant
        score data per-borough.

    #.  Combine the data into a single dictionary, keyed by borough, whose
        whose values are tuples containing the borough food score and the
        percentage density of green markets to restaurateurs as a float.

        The result of this should be similar to:

        .. code:: python

            {'BRONX': (0.9762820512820514, 0.1987179487179487)}

    #.  Finally, use the json module's ``dump()`` method to write the combined
        data dictionary to a file (the one occupying the third argument in
        the function call).



Submission
==========

Code should be submitted via Blackboard.


.. _GitHub: https://github.com/
.. _Python String Documentation: https://docs.python.org/2/library/stdtypes.html
