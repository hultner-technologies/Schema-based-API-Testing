all : activate install test-http test-imported test-stateful run-server run-server-gunicorn
.PHONY : all

activate: 
	poetry shell

install:
	poetry install

test-http:
	poetry run schemathesis run http://127.0.0.1:5000/swagger.json

# Won't really do anything here, as no links exist
test-stateful:
	poetry run schemathesis run http://127.0.0.1:5000/swagger.json --stateful=links

test-imported:
	poetry run schemathesis run --app=flask_example:app /swagger.json

run-server:
	poetry run python flask_example.py

run-server-gunicorn:
	poetry run gunicorn flask_example:app --bind 127.0.0.1:5000 --workers 17
