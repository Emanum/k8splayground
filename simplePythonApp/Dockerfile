FROM python:3.10-slim

RUN pip install pipenv
WORKDIR /code
COPY Pipfile Pipfile.lock ./
RUN pipenv install --deploy --system
ADD *.py *.pyc ./
EXPOSE 8080
CMD ["gunicorn"  , "-b", "0.0.0.0:8080", "main:app"]