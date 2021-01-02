# Server Based App
Simple  RESTful API created by python flask framework via [flask_restful](https://flask-restful.readthedocs.io/en/latest/) library and [jwt](https://jwt.io) module to secure it.


## Table of contents
* [Description](#description)
* [Perequisites](#perequisites)
* [Installation](#installation)
* [Usage](#usage)
* [Client](#Client)


## Description
Application consists of two sides: server and client side. Server stores all information about flights such as city of departure and arrival, date and time of arrival, date and time of departure, boeing info, passengers number. 
Moreover server stores admins' info for further authentication. The password of admins stored in hash code so even if someone get access to the database, he/she could not gain anything from this information.

Server provides information not only authorized admins but also to any user. However privileges for altering the data in the database have been given only to registered admins. 

>Server read the information about the registered users from json file and then add them to the database. In case of new admins, it is possible to make changes on json file and run the server again. It will update or even delete previous users according to json.

Any user can get information about flights stored in server's database according to the departured city and the destination city or even only by providing one of them.

> Authentication is provided by unique tokens generated by the server for each user.
## Perequisites 
* Python 3
* modules stored in [requirements.txt](/requirements.txt) file


## Installation

To download this repository you should use `git clone` command in your terminal.

```bash
git clone https://github.com/Khaaaan/
```

After downloading this repository, to install requirements to launch this application you can use `pip install` command in appropriate directory.

```bash
pip install -r requirements.txt
```
## Usage
To run this application properly, first of all you need follow the order.
Firstly run [app.py](/app.py)
```bash
>python3 app.py
```
By running the app itself you will create the database or update Admins table in case of you already have this database in [databases](databases) directory

by default there is five different pre-registered admins, but if you want change, delete or update any of them, modify [log_info.json](/log_info.json) file and rerun application to commit changes.
```bash
❯ cat log_info.json
[{
        "login": "admin1",
        "password": "admin1"
    },
    {
        "login": "admin23",
        "password": "admin2"
    },
    {
        "login": "admin34",
        "password": "admin3"
    },
    {
        "login": "admin4",
        "password": "admin4"
    },
    {
        "login": "admin5",
        "password": "admin5"
    }
]%         
```


Finally run [client.py](/client.py):
```bash
>python3 client.py
```

## Client 
Right after running the previous script console will show prompt:

![number_1](/images/number_1) 

There are 4 options (not case sensitive). In case of incorrect operation, client will throw an error and show the prompt again.

> After you enter the operation that you wish to do, application check whether it is **'GET'** operation or not. If ti is **"GET"**, additional prompt will appear to ensure is this *authorization*.
![number_2](/images/number_2)
You can skip it or just enter 'n' if it is not.
> * To be able to make changes to the data in database, authorization will be required

Then *path* will be required.

![number_3](/images/number_3)
> IMPORTANT: base url is **http://localhost:5000** so you should not add it.
### Paths

There are several paths with different usage objectives
1. To login
```bash
path: /authentication_authorization
```
2. To add or get all flights
```bash
path: /flights
```
3. To get the list of flights from (departure city), to (arrival city)
```bash
path: /flights/from/to/
```
4. To delete or update particular flight
```bash
path: /flights/flight_id
```
5. To end session
```bash
path: /end_session
```
### Data provided with POST and PUT requests
When you choose **PUT** or **POST** request, additional prompt for gathering the data will appeared.
In case of POST request it is mandatory to fill all of them while it is optional to enter any of them in PUT request

**POST** request:

![number_4](/images/number_4)

**PUT** request:

![number_5](/images/number_5)
