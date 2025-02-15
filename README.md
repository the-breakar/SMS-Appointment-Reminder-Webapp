<h1><center><font size='6'>SMS Medical Appointment Reminders WebApp</br>
by Steven Yan</font></center></h1>


[https://youtu.be/tSKfUlj_sYA](https://youtu.be/tSKfUlj_sYA)

# Setup Instructions:

1. Clone repository and `cd` into the created directory

```
git clone 
cd sms-reminder-flask

```

2. Create a virtual environment with a directory name `venv`: 

```
python -m venv [directory name]

```

3. Activate virtual environment: 

```
source venv/bin/activate

```


4. Change into the `app` directory of the repo, and install prerequisite packages to run Flask webapp:  

```
cd app
pip install -r requirements.txt

```

5. Copy `env.example` file to `.env` and fill in the listed values: 

```
export SECRET_KEY = 'your_secret_key'
export CELERY_BROKER_URL = redis://localhost:6379
export CELERY_RESULT_BACKEND = redis://localhost:6379

export TWILIO_ACCOUNT_SID = 'your_twilio_account_sid'
export TWILIO_AUTH_TOKEN = 'your_twilio_auth_token'
export TWILIO_NUMBER = '+1XXXXXXXXXX'

```


6. Create Flask application variables: 

```
export FLASK_APP = reminders.py
export FLASK_ENV = development

```

7. Run the migrations:

```
flask db upgrade

```

8. Install Docker Desktop and start a Redis server to serve as a broker for Celery tasks:

```
docker run -d -p 6379:6379 redis:latest

```

9. Start development server:

```
flask run

```

10.  Create another virtual environment to send reminders with a separate Celery worker process:

```
cd ..
python3 -m venv env

```

11. Install dependencies:

```
pip install -r requirements.txt

```

12. Activate Flask development environment:

```
export FLASK_ENV = development

```

13. Start the Celery worker:

```
celery -A tasks.celery worker -l info

``` 


# Project Description:

**Here are the challenges presented from client:**

- Easily lose track of postcard reminders
- Manual entry of appointments into calendar
- Different levels of computer literacy for veterans

**Here are our proposed solutions:**

- Needs calendar integration (ICS universal for all phones)
- Develop webapp for provider
- Develop mobile app for patient
- Automated SMS reminder system for non-tech savvy veterans


**Provider End:**

- Develop web application to interact with hospital server to send and receive relevant informatio through APIs
- Without technical details from VA, we created an interfacce for manual entry of patient appointmnets using a SQLAlchemy database within Flask microframework
- Customize SMS reminders according to the following actions:
	- confirmed
	- rescheduled
	- modified
	- canceled
	- no showed

**Patient End:**

- Use Twilio platform to send and receive SMS messages
- Patients will receive an initial text after booking their appointment
- They will have capability to respond to SMS to receive ICS file for easy integration
	- Currently iPhone have capability to create calendar events from any SMS with time details, but Android requires additional software
- At a default of 48 hours prior, patient will receive second SMS reminder to confirm or cancel appointmnet
	- reminder time adjustable to different intervals



# Screenshots:

**Index Page:**

<center><img src="images/index.png" width='600'></center>

**New Appointment Page:**

<center><img src="images/new_appointment.png" width='600'></center>

**Sample SMS Reminders:**

<center><img src="images/texts.png" width='300'></center>


# Presentation:

<!--<object data="docs/VA SMS Medical Appointment Reminder Platform.pdf" width="1000" height="1000" type='application/pdf'/></object>-->



# Folder Structure:

	├── README.md					<- top-level document for explaining project
	├── _app							<- folder of Flask application
	│   ├── _config					<- notebook for displaying augmentations
	│   ├── _forms					<- folder of forms scripts
	│   ├── _migrations			<- notebook for pretrained models
	│   ├── _models					<- folder of models script
	│   ├── _static					<- folder of CSS, Javascript, and image files
	│   ├── _templates				<- folder of HTML files
	│   ├── _views					<- folder of views script
	│   ├── application.py		<- script for defining routes and application
	│   ├── database.py			<- script for SQLAlchemy database
	│   ├── dev.sqlite				<- database file
	│   ├── Procfile				<- file for Heroku deployment
	│   ├── reminders.py			<- script for initiating application
	│   ├── requirements.txt		<- file for Heroku deployment
	│   └── tasks.py				<- script for running Celery tasks
	├── _docs							<- folder of project documentation
	└── _images						<- folder of jpeg and png files


# Contact Information:

[![Email Badge](https://img.shields.io/static/v1?label=Email&message=datascisteven@gmail.com&color=8b0000&style=for-the-badge&logo=GMail&logoColor=white&logoWidth=30)](mailto:datascisteven@gmail.com)

[![Github Badge](https://img.shields.io/static/v1?label=GitHub&message=@datascisteven&color=9966CC&style=for-the-badge&logo=GitHub&logoWidth=30)](https://www.github.com/datascisteven)

[![LinkedIn Badge](https://img.shields.io/static/v1?label=LinkedIn&message=@datascisteven&color=0A66C2&style=for-the-badge&logo=LinkedIn&logoWidth=30)](https://www.linkedin.com/in/datascisteven)

[![Medium Badge](https://img.shields.io/static/v1?label=Medium&message=@datascisteven&color=003366&style=for-the-badge&logo=Medium&logoWidth=30)](https://datascisteven.medium.com)

[![Portfolio Badge](https://img.shields.io/static/v1?label=Website&message=datascisteven.github.io&color=FF6600&style=for-the-badge&logo=GoogleChrome&logoColor=white&logoWidth=30)](https://datascisteven.github.io)

