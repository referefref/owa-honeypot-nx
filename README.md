Adapted from https://github.com/joda32/owa-honeypot by Willem Mouton (joda32).

# owa-honeypot-nx

owa-honeypot-nx is owa-honeypot (last upstream commit 17d7166, June 2019) updated so that it installs and runs on current Python 3 and Flask. The upstream `requirements.txt` pins Flask 1.0.2, which no longer imports on Python 3.10 or later (it uses `collections.MutableMapping`) and does not work with current Jinja2 and Werkzeug releases. The routes, templates, responses and log format are unchanged. The original README follows below.

## Changes from the original

* `requirements.txt` pins Flask 3.1.3 and Werkzeug 3.1.9 instead of Flask 1.0.2.
* `send_from_directory()` is called with `path=` instead of the `filename=` keyword, which Flask removed in 2.2.
* Optional environment variables, with the original values as defaults: `OWA_POT_LOG` (credential log file, default `dumpass.log` in the working directory), `OWA_POT_PORT` (default `80`) and `OWA_POT_HOST` (default `0.0.0.0`).

Note that `python owa_pot.py` still uses Flask's built-in development server, as the original does (see "here be dragons" below). Current Werkzeug releases send their own `Server` and `Date` headers in addition to the `Server: Microsoft-IIS/7.5` header the application sets.

# owa-honeypot
A basic flask based Outlook Web Honey pot

![](docs/OWA_honeypot_1.png)

## why?
Most corps have some form of OWA and I couldn't find an out of the box OWA only honeypot (I'm sure if I spent more than 2 minutes googling I probably would have found one) and I wanted to mess around with some ideas I have. So I spent some time putting this together, maybe it could help someone else :)

## requirements
python3 + flask

## how to install
git clone https://github.com/joda32/owa-honeypot.git
cd owa-honeypot
python3 -m venv env
source env/bin/activate
pip install -r requirements.txt

python owa_pot.py

## here be dragons!
In the code I basically start the flask dev server on port 80, that is a really bad idea if you want to run it on the internet. I have a todo to change that. :)

Anyway, it did work for what I wanted. I've added a crude write up here (https://joda32.github.io/2019/06/11/owa-plus-pastebin.html)

![](docs/OWA_honeypot_2.png)
![](docs/OWA_honeypot_3.png)
