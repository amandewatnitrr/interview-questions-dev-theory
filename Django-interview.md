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