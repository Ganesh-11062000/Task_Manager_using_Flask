#getting the requirements
sudo apt install virtualenv

#creating a virtual environment
virtualenv -p python3 env

# entering into the virtual environment
source env/bin/activate

#all the dependencies will now be installed inside the virtual environment env
pip3 install flask flask-sqlalchemy

#Let's create a simple hello world app in flask
#create a app.py in given folder

####################################
from flask import Flask

app = Flask(__name__)

@app.route('/')

def index():
    return "hello world"

if __name__ == "__main__":
    app.run(debug=True)

####################################
#python3 app.py  
#open browser and type localhost:5000

congratulations you just made a hello world app in Flask


--------------------------------

The project directory - 

Flask_tutorial 
    >env
    >static
        >css
    >templates
        >index.html
        >base.html
    app.py

-------------------------------
index.html :

{%extends 'base.html' %}

{% block body %}
<p>Jinjer text : hello world<p>
{% endblock %}

#It's like implementing an interface
#blocks will be defined somewhere in base html files
#content of which will be written in html files extending base.html

--------------------------------
 To link css from static

<link rel="stylesheet" href="{{url_for('static',filename='css/main.css')}}">

----------------------------------
#################### app.py ###############################

from flask import Flask,render_template,url_for
from flask_sqlalchemy import SQLAlchemy
from datetime import datetime

app = Flask(__name__)
app.config['SQLALCHEMY_DATABASE_URI'] = 'sqlite:///test.db'
db = SQLAlchemy(app)

class TODO(db.Model):
    id = db.Column(db.Integer,primary_key=True)
    content = db.Column(db.String(200),nullable=False)
    completed = db.Column(db.Integer,default=0)
    date_created = db.Column(db.DateTime,default=datetime.utcnow)

    def __repr__(self):
        return '<Task %r>' % self.id

@app.route('/')

def index():
    return render_template('index.html')

if __name__ == "__main__":
    app.run(debug=True)

###################################################################
 python3 app.py 
/home/ganesh/Desktop/Flask_py3/env/lib/python3.6/site-packages/flask_sqlalchemy/__init__.py:835: FSADeprecationWarning: SQLALCHEMY_TRACK_MODIFICATIONS adds significant overhead and will be disabled by default in the future.  Set it to True or False to suppress this warning.
  'SQLALCHEMY_TRACK_MODIFICATIONS adds significant overhead and '
 * Serving Flask app "app" (lazy loading)
 * Environment: production
   WARNING: This is a development server. Do not use it in a production deployment.
   Use a production WSGI server instead.
 * Debug mode: on
 * Running on http://127.0.0.1:5000/ (Press CTRL+C to quit)
 * Restarting with stat
/home/ganesh/Desktop/Flask_py3/env/lib/python3.6/site-packages/flask_sqlalchemy/__init__.py:835: FSADeprecationWarning: SQLALCHEMY_TRACK_MODIFICATIONS adds significant overhead and will be disabled by default in the future.  Set it to True or False to suppress this warning.
  'SQLALCHEMY_TRACK_MODIFICATIONS adds significant overhead and '
 * Debugger is active!
 * Debugger PIN: 275-370-319
127.0.0.1 - - [09/Mar/2020 12:34:22] "GET / HTTP/1.1" 200 -
^C(env) ganesh@ganesh-2020:~/Desktop/Flask_py3$ 

----------------------------------------------------
#creating database
from app import db
db.create_all()

#test.db will get created in your directory

-------------------------------------------------

#changed the index.html
# added all the html code required for our project

------------------------------------------------

updating index method in app.py 
if method == POST : 
    // add it to database
else:
    //display all the tasks

----------------------------------------------
