# VGG 16 Feature Extractor

[![](https://img.shields.io/badge/python-2.7%2C%203.5%2B-green.svg)]()
[![GPLv3 license](https://img.shields.io/badge/License-GPLv3-blue.svg)](http://perso.crans.org/besson/LICENSE.html)

> An endpoint for uploading images and getting back VGG16 image feature embeddings

------------------

## Docker Installation

Build the image

```shell
cd publicart-ml-endpoint
docker build -t keras_flask .
docker run -e MODEL_PATH=models/your_model.h5 -p 5000:5000
```

You can mount your model into the container.

```shell
docker run -e MODEL_PATH=/mnt/models/your_model.h5  -v volume-name:/mnt/models -p 5000:5000 keras_flask
```


## Local Installation

### Clone the repo
```shell
$ git clone https://github.com/rememberlenny/publicart-ml-endpoint.git
```

### Install requirements

```shell
$ pip install -r requirements.txt
```

Make sure you have the following installed:
- tensorflow
- keras
- flask
- pillow
- h5py
- gevent
- gunicorn

### Run with Python

Python 2.7 or 3.5+ are supported and tested.

```shell
$ python app.py
```

### Play

Open http://localhost:5000 and have fun. :smiley:

------------------

### Run the app

Run the script and hide it in background with `tmux` or `screen`.
```
$ python app.py
```

You can also use gunicorn instead of gevent
```
$ gunicorn -b 127.0.0.1:5000 app:app
```

More deployment options, check [here](http://flask.pocoo.org/docs/0.12/deploying/wsgi-standalone/)

### Set up Nginx

To redirect the traffic to your local app.
Configure your Nginx `.conf` file.
```
server {
    listen  80;

    client_max_body_size 20M;

    location / {
        proxy_pass http://127.0.0.1:5000;
    }
}
```