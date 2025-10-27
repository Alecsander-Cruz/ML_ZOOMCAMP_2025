FROM python:3.12-slim

RUN pip install pipenv

WORKDIR /app
COPY ["Pipfile", "Pipfile.lock", "./"]

# Ensure the lockfile is regenerated inside the image to match the Pipfile
# then install in deploy mode. Regenerating inside the container avoids
# a mismatch when the repo-level Pipfile was edited locally.
RUN pipenv lock --clear && pipenv install --deploy --system

COPY ["predict.py", "model_C=1.0.bin", "./"]

EXPOSE 9696

ENTRYPOINT ["gunicorn", "--bind=0.0.0.0:9696", "predict:app"]