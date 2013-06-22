======================
Introduction to Django
======================


What is Django?
===============

So far we know python. Python is just the language (and a set of core libraries) that allows you to
create programs. Creating interactive website in the Python require a huge amount of work, so we'll
use Django.
Django gives us a set of tools, features (such as we learned earlier, but more complex), and classes
to help you create pages.
For the fully interactive website we need a few items:

* application server - here we use Django
* HTML and CSS files - responsible for the appearance of the website
* Database - data, such as survey questions and answers, will be stored here.

We will start by creating an application server.

Installation
============

Install Django by running on the console:

.. code-block:: sh

   ~$ pip install django

A suitable package will be downloaded from `PyPI <http://pypi.python.org>`_ - package repository where
you can find many useful libraries.


Beginning of project
====================

Django provides administrative script "django-admin.py". t allows you to create the skeleton of our
site.

To create a new project with the site launch:

.. code-block:: sh

   # Linux

   ~$ django-admin.py startproject carrots
   ~$ tree carrots
   carrots/
   ├── carrots
   │   ├── __init__.py
   │   ├── settings.py
   │   ├── urls.py
   │   └── wsgi.py
   └── manage.py

   1 directory, 5 files


.. code-block:: bat

   :: Windows

   C:\Users\TeddyBear> python -m django-admin startproject carrots
   C:\Users\TeddyBear> tree /f carrots
   Folder PATH listing
   Volume serial number is 00FA-07FF
   C:\USERS\TEDDYBEAR\DOCUMENTS\CARROTS
   │   manage.py
   │
   └───carrots
           settings.py
           urls.py
           wsgi.py
           __init__.py


Structure of project
====================

The newly created project contains a catalog of "carrots" and some basic files.

The file ``carrots/settings.py`` re the settings such as language, database, installed applications.
We can edit this file by ourselves. Inside you will find the default settings and explanatory comments.

File ``manage.py`` ile allows us to administrate the web site, create or clean up the database, run a
simple application server, etc.

File ``carrots/urls.py`` ontains information about the tracks on the page.

Other files are less interesting. For more curious we recommend Google.

Setting of application
======================

In the file ``carrots/carrots/settings.py`` find:

.. code-block:: py

   DATABASES = {
       'default': {
           'ENGINE': 'django.db.backends.', # Add 'postgresql_psycopg2', 'mysql', 'sqlite3' or 'oracle'.
           'NAME': '',                      # Or path to database file if using sqlite3.
           'USER': '',                      # Not used with sqlite3.
           'PASSWORD': '',                  # Not used with sqlite3.
           'HOST': '',                      # Set to empty string for localhost. Not used with sqlite3.
           'PORT': '',                      # Set to empty string for default. Not used with sqlite3.
       }
   }

Rename ``'django.db.backends.'`` to the ``'django.db.backends.sqlite3'`` and add ``'NAME'`` ``'carrots.
db'``.
Plik ``carrots.db`` file will contain the database.

Set the time zone of Warsaw (or other city) and the default language to Polish (or other language)::

   # Local time zone for this installation. Choices can be found here:
   # http://en.wikipedia.org/wiki/List_of_tz_zones_by_name
   # although not all choices may be available on all operating systems.
   # In a Windows environment this must be set to your system time zone.
   TIME_ZONE = 'Europe/Warsaw'

   # Language code for this installation. All choices can be found here:
   # http://www.i18nguy.com/unicode/language-identifiers.html
   LANGUAGE_CODE = 'pl'


For simplicity, we exclude a powerful support for time zones in the database - it will not be needed
in our project:

   # If you set this to False, Django will not use timezone-aware datetimes.
   USE_TZ = False


Uncomment  two of lines indicated in ``INSTALLED_APPS``.

::

   INSTALLED_APPS = (
       'django.contrib.auth',
       'django.contrib.contenttypes',
       'django.contrib.sessions',
       'django.contrib.sites',
       'django.contrib.messages',
       'django.contrib.staticfiles',
       # Uncomment the next line to enable the admin:
       'django.contrib.admin',
       # Uncomment the next line to enable admin documentation:
       'django.contrib.admindocs',
   )


Now it's time to create the database:

.. code-block:: sh

   ~$ cd carrots
   ~$ python manage.py syncdb

    Creating tables ...
    Creating table auth_permission
    Creating table auth_group_permissions
    Creating table auth_group
    Creating table auth_user_groups
    Creating table auth_user_user_permissions
    Creating table auth_user
    Creating table django_content_type
    Creating table django_session
    Creating table django_site
    Creating table django_admin_log

    You just installed Django's auth system, which means you don't have any superusers defined.
    Would you like to create one now? (yes/no): yes
    Username (leave blank to use 'admin'): admin
    Email address: admin@example.com
    Password:
    Password (again):
    Superuser created successfully.
    Installing custom SQL ...
    Installing indexes ...
    Installed 0 object(s) from 0 fixture(s)

If all went well Django will ask you to provide an administrator account.


Administrative interface
========================

Now the file ``carrots/urls.py`` uncomment all the lines below ``Uncomment`` (by removing the ``#``
from the beginning of the line). The resulting file should look like this:

.. code-block:: py

   from django.conf.urls import patterns, include, url

   # Uncomment the next two lines to enable the admin:
   from django.contrib import admin
   admin.autodiscover()

   urlpatterns = patterns('',
       # Examples:
       # url(r'^$', 'carrots.views.home', name='home'),
       # url(r'^carrots/', include('carrots.foo.urls')),

       # Uncomment the admin/doc line below to enable admin documentation:
       url(r'^admin/doc/', include('django.contrib.admindocs.urls')),

       # Uncomment the next line to enable the admin:
       url(r'^admin/', include(admin.site.urls)),
   )

We need tools for documentation. Please run:

.. code-block:: sh

   ~$ pip install docutils
   (...)
   Successfully installed docutils
   Cleaning up...

Then start the server:

.. code-block:: sh

   ~$ python manage.py runserver
   Validating models...

   0 errors found
   April 19, 2013 - 20:14:37
   Django version 1.5.1, using settings 'carrots.settings'
   Development server is running at http://127.0.0.1:8000/
   Quit the server with CTRL-BREAK.

Then enter the link link http://localhost:8000/admin/.


We create a new application for surveys
=======================================

For now, we have created a draft ``carrots``. Projekty w Django dzielą się na aplikacje dostarczające określone funkcje.

We want to put surveys on our website, that’s why we will add application ``polls``.

From the command line type:

::

   ~$ python manage.py startapp polls
   ~$ tree .
   .
   ├── carrots
   │   ├── __init__.py
   │   ├── settings.py
   │   ├── urls.py
   │   ├── wsgi.py
   ├── carrots.db
   ├── manage.py
   └── polls
       ├── __init__.py
       ├── models.py
       ├── tests.py
       └── views.py

   2 directories, 14 files

After creating the application it must be activated in our project.
In the file  ``carrots/settings.py`` we have to add the application polls ``polls`` to
``INSTALLED_APPS``.
The result should look like this::

    INSTALLED_APPS = (
        'django.contrib.auth',
        'django.contrib.contenttypes',
        'django.contrib.sessions',
        'django.contrib.sites',
        'django.contrib.messages',
        'django.contrib.staticfiles',
        # Uncomment the next line to enable the admin:
        'django.contrib.admin',
        # Uncomment the next line to enable admin documentation:
        'django.contrib.admindocs',

        'polls',
    )

Models
======

The next step is to define the model of our application.
The model describes what and how it can be stored in the database.

Our application will include questions and answers to them, so we'll create two models:  ``Poll`` and
``Choice``.
Model ``Poll`` contains the contents of questions and date of publication. Model ``Choice`` contains a
reference to the relevant questions, the content of responses and the number of votes.

In a file ``polls/models.py`` type::

    from django.db import models

    class Poll(models.Model):
        question = models.CharField(max_length=200)
        pub_date = models.DateTimeField('date published')

    class Choice(models.Model):
        poll = models.ForeignKey(Poll)
        choice_text = models.CharField(max_length=200)
        votes = models.IntegerField(default=0)

By adding new models we have changed the database schema.
We need to make ``syncdb``, so that new models could appear in the database.

.. warning::
    After the ``syncdb`` ou can not add new fields to the model. You can only add new models.
    There are some ways to find a way around, but it's another story.

.. code-block:: sh

   ~$ python manage.py syncdb
   Creating tables ...
   Creating table polls_poll
   Creating table polls_choice
   Installing custom SQL ...
   Installing indexes ...
   Installed 0 object(s) from 0 fixture(s)

That’s it! Probably, however, we would like to be able to edit objects. Doing it in the administrative
interface is the easiest way.

Create a file ``polls/admin.py`` and there::

    from django.contrib import admin
    from polls.models import Poll, Choice

    admin.site.register(Poll)
    admin.site.register(Choice)

.. note::

    Some changes require a server restart. In a console click ``Ctrl+C`` and then ``python manage.py
    runserver`` again.

When we go back to http://localhost:8000/admin/ zobaczymy, see it’s visible that new bookmark `Polls`
appeared.


Game in a console
=================

Django provides its console. It is a simple Python console (where we can do exactly the same thing as
when you run ``python``), but also we can use the tools and models of Django.


.. code-block:: sh

   ~$ python manage.py shell

When you are in a shell already::

    >>> from polls.models import Poll, Choice

    # All the surveys in the database, and now there's nothing here, so we get an empty list
    >>> Poll.objects.all()
    []

    # We create first survey.
    >>> import datetime
    >>> p = Poll(question="What's new?", pub_date=datetime.datetime.now())

    # Save the poll in the database. For this purpose, you always need to call save ().
    >>> p.save()

    # Each object in the database is assigned to a unique ID .
    >>> p.id
    1

    # p is a simple object. We can read his attributes.
    >>> p.question
    "What's new?"
    >>> p.pub_date
    datetime.datetime(2012, 2, 26, 13, 0, 0, 775217)

    # After the changing of attributes we again call save() to save changes.
    >>> p.question = "What's up?"
    >>> p.save()

    # objects.all() returns a list of all the objects in the database
    >>> Poll.objects.all()
    [<Poll: Poll object>]

Django models are classes and classes can define methods. The method is one function that gets extra 
parameter ``self`` which is the current object (for example, the current survey). Methods in classes (
models) allow you to add additional behaviors or change existing ones.

One such method is the ``__str__``, which allows you to change the display of the model (or survey
questions).
``<Poll: Poll object>`` doesn’t tell us much. Let's fix that by adding the ``__str__`` do ``Poll`` and ``Choice``::

    class Poll(models.Model):
        # ...
        def __str__(self):
            return self.question

    class Choice(models.Model):
        # ...
        def __str__(self):
            return self.choice_text

Django will use these methods for displaying objects, not just in the console, but also in, mentioned
before, the administrative interface.

We can also add other methods::

    import datetime
    from django.utils import timezone
    # ...
    class Poll(models.Model):
        # ...
        def was_published_recently(self):
            return self.pub_date >= datetime.datetime.now() - datetime.timedelta(days=1)

Note that we had to add an import datetime to use objects representing the time in Python.

Let’s save the changes and run intepreter with the command ``python manage.py shell`` once again::

    >>> from polls.models import Poll, Choice

    # Let’s find out if our method __str__() works
    >>> Poll.objects.all()
    [<Poll: What's up?>]

We have used  ``all``,the methods which allow you to draw a list of all objects of that type (for
example all questions). There are other methods that allow to draw objects that meet certain
conditions:

.. code-block:: python

    # Django provides a very easy search of the objects in the database. Let's look at some examples.

    >>> Poll.objects.filter(id=1)
    [<Poll: What's up?>]
    >>> Poll.objects.filter(question__startswith='What')
    [<Poll: What's up?>]
    >>> Poll.objects.get(pub_date__year=2012)
    <Poll: What's up?>

    # The attempt to retrieve a nonexistent object will make a strong protest of Python.
    # But we already get used to this.
    >>> Poll.objects.get(id=2)
    Traceback (most recent call last):
        ...
    DoesNotExist: Poll matching query does not exist. Lookup parameters were {'id': 2}

    # Let’s try our own method.
    >>> p = Poll.objects.get(pk=1)
    >>> p.was_published_recently()
    True

We can also gain access to the answers (``Choice``) questions:

.. code-block:: python

    # For now our survey did not include any questions. Let's add some!
    >>> p.choice_set.all()
    []

    # ... for example three. We will use the method "create". As a result, we get an object "Choice".
    >>> p.choice_set.create(choice_text='Not much', votes=0)
    <Choice: Not much>
    >>> p.choice_set.create(choice_text='The sky', votes=0)
    <Choice: The sky>
    >>> c = p.choice_set.create(choice_text='Just hacking again', votes=0)

    # With object "Choice" we can find the survey, to which it belongs.
    >>> c.poll
    <Poll: What's up?>

    # ...conversely, all of the answers to the questionnaire
    >>> p.choice_set.all()
    [<Choice: Not much>, <Choice: The sky>, <Choice: Just hacking again>]
    >>> p.choice_set.count()
    3

    # And now something more difficult. What this question does?
    >>> Choice.objects.filter(poll__pub_date__year=2012)
    [<Choice: Not much>, <Choice: The sky>, <Choice: Just hacking again>]

    # Finally, let's remove one of the questions. Use method ``delete``.
    >>> c = p.choice_set.filter(choice_text__startswith='Just hacking')
    >>> c.delete()



Screening of websites
=====================

Enter the main address http://localhost:8000/ still displays an ugly error page. It can not be like
that!

It's good to start working on a new website from reflection about structure of URLs (addresses).
Wiemy, ze będziemy
We want to see a list of all polls on the site, let users vote and view aggregated results of the 
survey.

Again, let's open the file ``urls.py`` add four new entries. Eventually file should look like this::

  from django.conf.urls import patterns, include, url

  from django.contrib import admin
  admin.autodiscover()

  urlpatterns = patterns('',
      url(r'^polls/$', 'polls.views.index'),
      url(r'^polls/(?P<poll_id>\d+)/$', 'polls.views.detail'),
      url(r'^polls/(?P<poll_id>\d+)/results/$', 'polls.views.results'),
      url(r'^polls/(?P<poll_id>\d+)/vote/$', 'polls.views.vote'),
      url(r'^admin/', include(admin.site.urls)),
  )

Let's look at this example again. Each argument passed to the function ``patterns`` (except for the
first, but more on that later) determines our standard URL (address). This pattern is written using a
`regular expression. <http://pl.wikipedia.org/wiki/Wyra%C5%BCenie_regularne#Wyra.C5.
BCenia_regularne_w_praktyce>`_.
This is a difficult technical term for tiny language used for concise representation of a pattern.

When a user tries to enter a specific address on our website, such as http://localhost:8000/polls/1/
selects the third part of the URL after the slash (in this case ``polls/1/``)  and try  turn it into a
regular expression to match the``urlpatterns``. Let's look at an example of such expressions::

  r'^polls/(?P<poll_id>\d+)/vote/$'

This is a normal string (maybe except for the initial ``r``, which is used here only for convenience). 
When we try to fit the text (still thinking of ``polls/1/``),we need to remember the following:

.. admonition:: Regular expressions
   :class: alert alert-info

   * Each letter and number of the regular expression applies  to the same letters / numbers over 
     matched string. The same us slash (``/``),  space (`` ``), the underscore (``_``) and hyphen (``-``).
   * ``^`` applies only to the beginning of the string (no to string,  "beginning" is here as a 
     abstraction before the first string).
   * ``$`` matches only at the end of the string (on the similar base as "beginning").
   * The dot (``.``) matches any character.
   * If several characters will embraced in the square brackets, like this  ``[aBde]`` the group 
     counts as one unit and will match any one character within the group.
   * There is a shorthand notation for such groups. Rather than write out all the small letters of the
     alphabet, we can write ``[a-z]`` to match any single lowercase letter. Same for the upper case letters``[A-Z]`` or digits``[0-9]``.
   * Matching one number can be even shorter by using the stamp ``\d``.
   * If after any of the above expressions we put the sign ``?``, it will be treated as
     *opcjonalne*. 

     Oznacza
     to, ze jeżeli w ciągu dopasowywanym nie będzie takiego wyrażenia, nadal będzie mozliwe jego dopasowanie. Jeżeli
     będzie, zostanie dopasowane.
   * Jeżeli po wyrażeniu postawimy znak ``*`` dopasuje się ono z dowolną ilością powtorzeń wyrażenia (wliczając w to zero
     powtórzeń, czyli tak jakby bylo *opcjonalne*).
   * Jeżeli po wyrażeniu postawimy znak ``+`` dopasuje się ono z dowolną ilością powtórzeń wyrażenia, z wyjątkiem zera
     powtórzen (tzn. wyrażenie musi wystąpić conajmniej raz).
   * Jeżeli kilka znaków obejmiemy nawiasami zwykłymi, np. tak ``(\d\d)`` zostaną one potraktowane jako grupa i wszystkie
     powyższe modyfikatory będą na nie działały w całości. Jeżeli dodatkowo napiszemy to z ``(?P<NAZWA>napis)``, grupa
     zostanie nazwana i będzie się do niej można potem odwołać pod nazwą ``NAZWA``. Jest to bardzo popularne przy pracy w
     Django.

Uff... Jest jeszcze wiele reguł ale tak naprawdę nikt ich wszystkich nie pamięta. Te powyższe wystarczają w większości
przypadków.

Czy widzisz już, ze przykładowe wyrażenie dopasuje się do ``polls/1/``? Dlaczego?

Kiedy już Django znajdzie dopasowanie, popatrzy na drugą część linii. Określa ona widok, który ma być wywołany w celu
utworzenia strony dla użytkownika. Dla ``polls/1/`` będzie to ``polls.views.detail``. Wszystkie nazwane grupy zostaną
przekazane widokowi jako argumenty o tej samej nazwie, tak jakby wywolać z konsoli:

.. code-block:: python

  detail(request=<HttpRequest object>, poll_id='1')


Pierwszy widok
==============

Dobra, zobaczmy jak to działa w praktyce. Niestety wejscie pod adres http://localhost:8000/polls/1/ nie konczy się
dobrze::

  ViewDoesNotExist at /polls/1/

  Could not import polls.views.detail. View does not exist in module polls.views.

Ach, to dlatego, ze nie zdefiniowalismy jeszcze widoku (Django podpowiada nam, że szukało ``polls.views.detail``,
niestety pod powodzenia)! Otworzmy w tym celu plik `polls/views.py` i dodajmy kilka nowych funkcji::

  from django.http import HttpResponse

  def index(request):
      return HttpResponse("Hello, world. You're at the poll index.")

  def detail(request, poll_id):
      return HttpResponse("You're looking at poll %s." % poll_id)

  def results(request, poll_id):
      return HttpResponse("You're looking at the results of poll %s." % poll_id)

  def vote(request, poll_id):
      return HttpResponse("You're voting on poll %s." % poll_id)

Tak wygladają najprostsze możliwe widoki. Nie zwracają one zwykłych ciagow znaków, tak jak funkcja budująca choinkę w
Pythonie, bo muszą mówić protokołem HTTP, który jest nieco bardziej skomplikowany (tutaj dobrze byłoby zobaczyc w
przeglądarce, co się tak naprawde dzieje, gdy wchodzimy pod adres http://localhost:8000/polls/1/).


Widok, który naprawdę coś robi
==============================

Nasze widoki na razie nie robią zbyt wiele. Dajmy im troche popracowac!

Wszystko czego Django potrzebuje od widoku to obiekt
`HttpResponse <https://docs.djangoproject.com/en/1.4/ref/request-response/#django.http.HttpResponse>`_
lub wyrzucenie wyjątku. Cała reszta jest pod naszą kontrolą. Możemy na przykład użyć funkcji, które poznaliśmy w trybie
interaktywnym aby wyświetlić wszystkie ankiety użytkownikowi::

  from polls.models import Poll
  from django.http import HttpResponse

  def index(request):
      latest_poll_list = Poll.objects.all().order_by('-pub_date')[:5]
      output = ', '.join([p.question for p in latest_poll_list])
      return HttpResponse(output)

.. note::

    Teraz nie podajemy już całej treści pliku, bo byłaby ona za długa. Podawane są tylko najważniejsze zmiany. W tym
    wypadku zmieniła się funkcja ``index`` oraz sam początek pliku (dodana linijka
    ``from django.http import HttpResponse``).

Działa! Jest tylko jeden problem z tym przykładem: Określamy w widoku nie tylko to, co ma być zwrócone, ale też w jakim
formacie ma zostać zwrócone użytkownikowi serwisu. Jedna z najważniejszych umiejętności programisty jest umiejetność
odróżniania i rozdzielania dwóch niezależnych rzeczy. Programisci Django o tym pomyśleli i stworzyli system szablonow::

  from django.template import Context, loader
  from polls.models import Poll
  from django.http import HttpResponse

  def index(request):
      latest_poll_list = Poll.objects.all().order_by('-pub_date')[:5]
      t = loader.get_template('polls/index.html')
      c = Context({
          'latest_poll_list': latest_poll_list,
      })
      return HttpResponse(t.render(c))

Za obsługę szablonu w tym wypadku są odpowiedzialne funkcje ``get_template`` (Znajduje szablon) oraz ``render`` (zmienia
szablon na test, który dostanie ostatecznie użytkownik).

Kod jest trochę dluższy, ale zaraz zobaczymy o ile wszystko będzie czytelniejsze. Najpierw załadujmy jednak stronę
http://localhost:8000/polls/, aby zobaczyć wynik naszej pracy::

  TemplateDoesNotExist at /polls/
  polls/index.html

Ups! No tak, nie dodaliśmy jeszcze szablonu. Aby to zrobić, stworzmy plik ``polls/templates/polls/index.html`` i dodajmy
do niego:

.. note::
    Szablony aplikacji znajdują się w katalogu ``templates`` aplikacji, a funkcja ``get_template`` sama szuka szablonów
    w tych katalogach, dlatego nie musieliśmy podawać całej ścieżki ``polls/templates/polls/index.html``, wystarczyło
    ``polls/index.html``.

.. code-block:: django

  {% if latest_poll_list %}
  <ul>
      {% for poll in latest_poll_list %}
          <li><a href="/polls/{{ poll.id }}/">{{ poll.question }}</a></li>
      {% endfor %}
  </ul>
  {% else %}
      <p>No polls are available.</p>
  {% endif %}

Po przeładowaniu strony w przeglądarce powinniśmy zobaczyć listę zawierającą wszystkie utworzone wcześniej ankiety.

.. note::

    Jeżeli po odświerzeniu strony nadal widać błąd, należy ponownie uruchomić serwer. W konsoli gdzie jest uruchomiony
    serwer wciskamy ``Ctrl+C`` i wykonujemy ``python manage.py runserver`` ponownie. Teraz powinno już dzialać.

.. note::

   HTML i CSS sa formatami slużacymi do określania wyglądu stron internetowych. Szablonow Django będziemy używac po to
   aby generować kod HTML. Dobry opis HTML znajduje się w ksiazce
   `Interactive Data Visualization for the Web <http://ofps.oreilly.com/titles/9781449339739/k_00000003.html>`_.
   Zachwycającą własnością sieci WWW jest to, ze kody HTML i CSS każdej strony są calkiem jawne. Polecam obejrzenie kodu
   ulubionych stron.

Prawie w każdym widoku będziemy chcieli ostatecznie użyc szablonu. Dlatego w Django jest funkcja ``render_to_response``,
która pozwala zrobić to w krótszy sposób::

  from django.shortcuts import render_to_response
  from polls.models import Poll

  def index(request):
      latest_poll_list = Poll.objects.all().order_by('-pub_date')[:5]
      return render_to_response('polls/index.html', {'latest_poll_list': latest_poll_list},
                            context_instance=RequestContext(request)))


Zwracanie 404
=============

Zajmijmy się teraz widokiem szczegółow ankiety -- strona, która wyświetla pytania z konkretnej ankiety. Tak wygląda kod
widoku::

    from django.http import Http404
    # ...
    def detail(request, poll_id):
        try:
            p = Poll.objects.get(pk=poll_id)
        except Poll.DoesNotExist:
            raise Http404
        return render_to_response('polls/detail.html', {'poll': p})

Tak wygląda kod szablonu ``polls/templates/polls/detail.html``:

.. code-block:: django

    <h1>{{ poll.question }}</h1>
    <ul>
    {% for choice in poll.choice_set.all %}
        <li>{{ choice.choice_text }}</li>
    {% endfor %}
    </ul>

Nowością jest tutaj wyrzucanie wyjątku ``Http404``, gdy sprawdzimy, ze ankieta o konkretnym ID nie istnieje. Django
obsluzy taki wyjatek wyswietlajac domyslna strone 404.

.. note::

   Można zmienić stronę wyswietlaną przez Django w wypadku błędu 404 (brak strony) i 500 (nieoczekiwany błąd serwera).
   W tym celu trzeba stworzyć szablony ``404.html`` i ``500.html``. Przed sprawdzeniem czy to zadziałało należy zmienić
   ``DEBUG`` w pliku ``settings.py`` na ``False``. W innym wypadku Django nadal będzie wyświetlac swoje pomocnicze
   *żółte* strony.


Obsluga formularzy
==================

Zmieńmy szablon ``polls/templates/polls/details.html``, dodając tam prosty formularz HTML.

.. code-block:: django

  <h1>{{ poll.question }}</h1>

  {% if error_message %}<p><strong>{{ error_message }}</strong></p>{% endif %}

  <form action="/polls/{{ poll.id }}/vote/" method="post">
  {% csrf_token %}
  {% for choice in poll.choice_set.all %}
      <input type="radio" name="choice" id="choice{{ forloop.counter }}" value="{{ choice.id }}" />
      <label for="choice{{ forloop.counter }}">{{ choice.choice_text }}</label><br />
  {% endfor %}
  <input type="submit" value="Vote" />
  </form>

.. note::

   ``{% csrf_token %}`` to bardzo magiczny sposób zabezpieczenia przed stosunkowo nowym sposobem ataku na użytkowników
   stron internetowych. Wiecej opisane jest w
   `dokumentacji Cross Site Request Forgery <https://docs.djangoproject.com/en/1.4/ref/contrib/csrf/>`_.

Aby działały niektóre tagi szablonu (w szczególnosci ``{% csrf_token %}``), musimy przekazać do `render_to_response`
obiekt `RequestContext <https://docs.djangoproject.com/en/1.4/ref/templates/api/#subclassing-context-requestcontext>`_.
Robimy to w następujacy sposób::

  from django.template import RequestContext
  from django.shortcuts import get_object_or_404
  # ...
  def detail(request, poll_id):
      p = get_object_or_404(Poll, pk=poll_id)
      return render_to_response('polls/detail.html', {'poll': p},
                                 context_instance=RequestContext(request))

Uważny czytelnik zauważy, że formularz wysyłany jest na adres ``/polls/{{ poll.id }}/vote/``, który nie obsługuje
jeszcze danych formularza. Poprawmy to teraz::

    from django.http import HttpResponseRedirect
    from django.core.urlresolvers import reverse

    from polls.models import Choice
    # ...
    def vote(request, poll_id):
        p = get_object_or_404(Poll, pk=poll_id)
        try:
            selected_choice = p.choice_set.get(pk=request.POST['choice'])
        except (KeyError, Choice.DoesNotExist):
            # Wyświetl błąd użytkownikowi, gdy wybrał złą opcję
            return render_to_response('polls/detail.html', {
                'poll': p,
                'error_message': "Musisz wybrać poprawną opcję.",
            }, context_instance=RequestContext(request))

        # Zapisz nową liczbę głósów
        selected_choice.votes += 1
        selected_choice.save()
        # Przekieruj użytkownika do widoku detali ankiety na, którą właśnie zagłosował
        return HttpResponseRedirect(reverse('polls.views.results', args=(p.id,)))

W tym widoku pojawia się sporo nowych koncepcji, o których nie mówiliśmy.

Obiekt ``request`` zawiera dane wysłane przez użytkownika, a ``request.POST`` zawiera dane z formularza
wysłanego przez użytkownika. W ten sposób wiemy, która opcja została wybrana.

Tutaj pojawia się ważna kwestia. Może okazać się, że widok dostał nieistniejącą odpowiedź.
Zawsze musimy sprawdzać dane otrzymane od użytkownika i reagować na sytuację, gdy te dane są bezsensowne.
To właśnie dzieje się w po :keyword:`except`. Odsyłamy wtedy użytkownika do ankiety i wyświetlamy błąd.

Jeżeli użytkownik wybrał poprawną opcję, możemy zwiększyć liczbę głosów i zapisać zmiany.
Następnie wykonujemy przekierowanie za pomocą ``HttpResponseRedirect`` do wcześniej napisanego
widoku detali ankiety.

Kolejna istotna sprawa. Po zagłosowaniu mogliśmy po prostu wyświetlić jakąś stronę, podobnie jak na końcu widoku detali
(za pomocą ``render_to_response``). To niestety mogłoby prowadzić do ponownego wysyłania ankiety, jeżeli użytkownik
zacznie bawić się przyciskami ``wstecz`` i ``dalej`` w przeglądarce, albo po prostu odświerzył stronę (klawiszem ``f5``)
W skrócie, zawsze po poprawnym wysłaniu formularza (w tym wypadku, zagłosowaniu na ankietę) powinniśmy wykonać
przekierowanie za pomocą ``HttpResponseRedirect``.

Na koniec pozostał nam do opracowania widok wyników ankiety, wyświetlany po zagłosowaniu::

  def results(request, poll_id):
      p = get_object_or_404(Poll, pk=poll_id)
      return render_to_response('polls/results.html', {'poll': p},
                             context_instance=RequestContext(request))

Szablon ``polls/templates/polls/results.html``:

.. code-block:: django

  <h1>{{ poll.question }}</h1>

  <ul>
  {% for choice in poll.choice_set.all %}
      <li>{{ choice.choice_text }} -- {{ choice.votes }} vote{{ choice.votes|pluralize }}</li>
  {% endfor %}
  </ul>

  <a href="/polls/{{ poll.id }}/">Vote again?</a>

To wszystko! Wejdź pod adres http://localhost:8000/admin/ i stwórz kilka nowych ankiet i pytań a potem pobaw się
głosując na nie i namawiając inne osoby aby zrobiły to samo.


.. admonition:: ``polls/views.py``
   :class: alert alert-hidden

   .. code-block:: python

        from django.http import Http404
        from django.http import HttpResponse
        from django.http import HttpResponseRedirect
        from django.template import Context, loader
        from django.template import RequestContext
        from django.shortcuts import render_to_response
        from django.shortcuts import get_object_or_404
        from django.core.urlresolvers import reverse

        from polls.models import Choice
        from polls.models import Poll

        def index(request):
            latest_poll_list = Poll.objects.all().order_by('-pub_date')[:5]
            return render_to_response('polls/index.html',
                                    {'latest_poll_list': latest_poll_list},
                                    context_instance=RequestContext(request))

        def detail(request, poll_id):
            p = get_object_or_404(Poll, pk=poll_id)
            return render_to_response('polls/detail.html', {'poll': p},
                                     context_instance=RequestContext(request))

        def results(request, poll_id):
            p = get_object_or_404(Poll, pk=poll_id)
            return render_to_response('polls/results.html', {'poll': p},
                             context_instance=RequestContext(request))

        def vote(request, poll_id):
            p = get_object_or_404(Poll, pk=poll_id)
            try:
                selected_choice = p.choice_set.get(pk=request.POST['choice'])
            except (KeyError, Choice.DoesNotExist):
                # Wyświetl błąd użytkownikowi, gdy wybrał złą opcję
                return render_to_response('polls/detail.html', {
                    'poll': p,
                    'error_message': "Musisz wybrać poprawną opcję.",
                }, context_instance=RequestContext(request))

            selected_choice.votes += 1
            selected_choice.save()
            # Przekieruj użytkownika do widoku detali ankiety na, którą właśnie zagłosował
            return HttpResponseRedirect(reverse('polls.views.results', args=(p.id,)))

.. admonition:: ``urls.py``
   :class: alert alert-hidden

   .. code-block:: python

        from django.conf.urls import patterns, include, url

        from django.contrib import admin
        admin.autodiscover()

        urlpatterns = patterns('',
          url(r'^polls/$', 'polls.views.index'),
          url(r'^polls/(?P<poll_id>\d+)/$', 'polls.views.detail'),
          url(r'^polls/(?P<poll_id>\d+)/results/$', 'polls.views.results'),
          url(r'^polls/(?P<poll_id>\d+)/vote/$', 'polls.views.vote'),
          url(r'^admin/', include(admin.site.urls)),
        )



.. admonition:: ``polls/models.py``
   :class: alert alert-hidden

   .. code-block:: python

        from django.db import models

        class Poll(models.Model):
            question = models.CharField(max_length=200)
            pub_date = models.DateTimeField('date published')

            def __str__(self):
                return self.question


        class Choice(models.Model):
            poll = models.ForeignKey(Poll)
            choice_text = models.CharField(max_length=200)
            votes = models.IntegerField(default=0)

            def __str__(self):
                return self.choice_text
