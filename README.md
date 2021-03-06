# Appsembler Launch
## Local development set up

This instructions are written under the assumption that you have [virtualenvwrapper](http://virtualenvwrapper.readthedocs.org/en/latest/) set up on your machine.

You also need working [OpenShift](https://www.openshift.com/), [Pusher](http://pusher.com/), [Segment.io](https://segment.io/) and [Customer.io](http://customer.io/) accounts.

1. Create a new virtual env: `mkvirtualenv appsemblerlaunch`
2. Set the required env variables in your virtual environments `bin/postactivate` script:

		#!/usr/local/bin/zsh
		# This hook is run after this virtualenv is activated.
		
		# Django settings
		export SECRET_KEY=''

		# Pusher settings
		export PUSHER_APP_ID=''
		export PUSHER_APP_KEY=''
		export PUSHER_APP_SECRET=''

		# OpenShift settings
		export OPENSHIFT_USER=''
		export OPENSHIFT_PASSWORD=''

		# Customer.io settings
		export CUSTOMERIO_SITE_ID=''
		export CUSTOMERIO_API_KEY=''

		# Segment.io settings
		export CUSTOMERIO_SITE_ID=''
		export CUSTOMERIO_API_KEY=''

3. Clone this repo: `git clone git@github.com:appsembler/appsembler-launch.git`
4. Activate the virtualenv: `workon appsemblerlaunch`
5. `cd appsembler-launch; setvirtualenvproject`
6. Install the requirements: `pip install -r requirements/local.txt`
7. Run syncdb: `./manage.py syncdb --settings=openshift_deploy.settings.local`
8. Run migrations: `./manage.py migrate --settings=openshift_deploy.settings.local`
9. Start celery in one shell: `./manage.py celery worker -B --loglevel=info --autoreload --settings=openshift_deploy.settings.local --concurrency=2 -s celerybeat-schedule`
10. And runserver in other: `./manage.py runserver --settings=openshift_deploy.settings.local`