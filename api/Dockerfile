FROM python:3.8 AS base

ENV LANG C.UTF-8
ENV LC_ALL C.UTF-8
ENV PYTHONDONTWRITEBYTECODE 1
ENV PYTHONFAULTHANDLER 1


FROM base AS deps

RUN pip install pipenv
COPY Pipfile .
COPY Pipfile.lock .
RUN PIPENV_VENV_IN_PROJECT=1 pipenv install --deploy


FROM deps AS runtime

COPY --from=deps .venv .venv
ENV PATH="/.venv/bin:$PATH"

COPY . .
EXPOSE 8000

ENTRYPOINT [ "python", "manage.py" ]
CMD [ "runserver", "0.0.0.0:8000" ]

