# Django Interview Questions

### How does Django work??

- The Browser sends a request to our web server.
- Our request is handed over to a Web Server Gateway Interface(WSGI) or directly serves a file from the file system.
- Unlike Web Server, WSGI can run python applications. The request populates a python dictionary called `environ` and passes through some layers of middleware before finally reaching our application.
- The `URLconf`  contained in our `urls.py` of our project selects a view to handle the request based on the requested URL, and is turned into a `HttpRequest` python object.

- ![](./imgs/Screenshot%202024-06-08%20at%206.51.32 PM.png)

- Here, Django manages and queries data through Python objects reffered as Models.
- Models define the structure of stored data such as it's field, maximum size, default value etc.

### Explain the Django Architecture

- Django follows MVT(Model View Template) pattern which is based on MVC(Model View Controller) Architecture. It's slightly different from the MVC cause it has it's own conventions, so the controller is handeled by framework itself.
- The template is a presentation layer. The Developer provides the model, the template and the view, and maps it to a URL, and than finally serves it to the user.
- ![](./imgs/Screenshot%202024-06-08%20at%206.58.20 PM.png)

### What are models in Django?

- Models in Django are classes that represent the structure of a Database Table.
- Example:

    ```python
    from django,db import models
    class SampleDatabse(models.model):
        field1 = models.CharField()
        field2 = models.IntegerField()

        class Meta:
            db_table = "Database"
    ```

### What are views in Django??

- Views in Django are functions that take a web request and return a web response.. This response can be a HTML Content or a query from the database or a redirect or error or any file.
- Example:

    ```python
    from django.http import HttpResponse
    def sample_view(request):
        return HttpResponse("Hello World")
    ```


### What is Django ORM??

- Django ORM(Object Relational Mapping) is a way to interact with the database using Python objects.
- Using this actually minimises the use of SQL queries.

### What is django-admin and manage.py??

- `django-admin` is a command line utility that lets you interact with Django project.
- A `manage.py` file is automatically created in each Django project. It is a thin wrapper around the `django-admin.py` that takes care of module settings for us, pointing to the `settings.py` file.

### What is Jinja Templating??

- Jinja is a templating engine for Python, which is used in Django.
- It is easier to debug compared to other default engines.
- It offers template inheritence.
- Generates HTML Templates faster compared to other engines.
- HTML Escaping - Some special characters have special values which can lead to XSS Attacks in Templating Engines. Jinja automatically deals with it.

### Difference b/w project and app in Django??

- Project is the entire django application.
- While, app is just a small module inside the project with a uique use case.