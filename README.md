<img align="right" width="120" alt="rmotr.com" src="https://user-images.githubusercontent.com/7065401/45454218-80bee800-b6b9-11e8-97bb-bb5e7675f440.png">

# Coinmarketcap Relationships and HTML Forms

Remember the [https://coinmarketcap.com/](https://coinmarketcap.com/) clone we did in our [previous class](https://github.com/rmotr-curriculum/wdc-class-1-coinmarketcap-clone)? 💪 Today we will augment it with some more Django functionalities. 🙌

We want you to learn how to make relationships between models and the way that Django ORM handles this in order to search and filter objects.

Also we'll work with HTML forms and create/delete objects in our database based on incoming actions that come from the templates.

## Setting up the environment

Before we get started with Django, we need to make sure our local Python environment is properly set up. For that, we will use `virtualenv` and the awesome `virtualenvwrapper` tool.

*note: this app has been developed using Python 3.5*

```bash
$ mkvirtualenv -p $(which python3.5) coinmarketcap
$ pip install -r requirements/base.txt
```

You can now run the development server and point the browser to the correct URL:

```bash
$ make runserver
```

_Note: If you're using RMOTR Notebooks, you don't need to create a virtualenv_

## 1) Adding a new Exchange model

In order to practice some relationships between models through ForeignKeys, we'll create a brand new `Exchange` model that will be linked to our already created `Cryptocurrency`.

For simplicity, we'll assume that each Cryptocurrency will be in sale in one Exchange at a time.

For linking this two models, we need to add a `ForeignKey` field in the Cryptocurrency model.

A new column will be added in our Cryptocurrencies table, that will show the Exchange to which the coin belongs to. It should looks like this:

<img width="878" alt="screen shot 2019-01-01 at 16 54 48" src="https://user-images.githubusercontent.com/2788551/50575932-0c35c380-0de6-11e9-88c1-1bf4719b29ac.png">

Also we'll extend our Search input in order to allow searching both for Cryptocurrency name, or Exchange name. For this task we'll make usage of the [Django Q object](https://docs.djangoproject.com/en/2.1/topics/db/queries/#complex-lookups-with-q-objects).

## 2) Creating new coins

As a second step, we want the users of our app to be able to create new Cryptocurrencies. For that we need to create an HTML form that will be in charged of sending input data from the user, and the proper view will handle the creation (with previous validation) of the object.

Add a button in the main page, with a link to `/create-currency`. Should look something like:

<img width="1038" alt="screen shot 2019-01-01 at 16 46 15" src="https://user-images.githubusercontent.com/2788551/50575876-e22fd180-0de4-11e9-880f-ef2eab042d70.png">

In the `/create-currency` template, we will render a form using plain HTML, with an input for each Cryptocurrency model field. We'll use [Bootstrap](https://getbootstrap.com/) to make the form prettier. Check the following screenshot for extra details:

<img width="868" alt="screen shot 2019-01-01 at 16 49 23" src="https://user-images.githubusercontent.com/2788551/50575892-43f03b80-0de5-11e9-9846-73891049bf35.png">

If any of the required inputs is not completed, the view should re-render the template sending the errors that must be shown

## 3) Deleting coins

A new `Actions` column will be added to the Cryptocurrencies table, with a delete icon for each row. Should look like this:

<img width="1028" alt="screen shot 2019-01-01 at 16 43 51" src="https://user-images.githubusercontent.com/2788551/50575865-af85d900-0de4-11e9-8493-2562dafa148c.png">

This icon will point to `/delete-currency/<id>` URL and a `delete` view will be in charged of searching the coin with given id and delete it.

That's all! 🎉 We just did a second iteration to the Coinmarketcap clone, adding some more advanced functionalities of the Django framework.
