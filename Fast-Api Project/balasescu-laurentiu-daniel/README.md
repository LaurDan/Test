# Update Service

UpdateService is a simple REST service which allows to manage and packages updates. It provides a set of APIs for:
- Update channels management
- Applications management
- Packages management
- User management

The service is partially compatible with the [updateservicectl](https://github.com/coreos/updateservicectl) client and supports the following command:
- `channel` (`create`, `list`, `update`, `delete`)
- `app` (`create`, `list`, `update`, `delete`)
- `package` (`create`, `list`, `delete`, `upload`, `download`)


## Development

### Technology Stack

#### Runtime environment
- Docker (https://docs.docker.com/get-started/overview/)
- docker-compose for containers management and orchestration (https://docs.docker.com/compose/)
- Python 3.10

##### Additional information
- [Python 3.10 changelog](https://docs.python.org/3/whatsnew/3.10.html)
- [Docker vs Virtual Machine](https://geekflare.com/docker-vs-virtual-machine/)

#### Third-party dependency management and build tool
- Poetry - dependency management and packaging tool (https://python-poetry.org/)
- Poe - task runner for poetry (https://github.com/nat-n/poethepoet)

#### Web/API framework
- REST API (https://docs.microsoft.com/uk-ua/azure/architecture/best-practices/api-design)
- FastAPI as API framework (https://fastapi.tiangolo.com/)
- OpenAPI for API documentation (https://swagger.io/specification/). OpenAPI specification will be autogenerated by FastAPI (https://fastapi.tiangolo.com/features/)
- Result: Swagger for created (auto-generated) API is available and exposed

##### Additional information
- [HTTP Protocol Overview](https://developer.mozilla.org/en-US/docs/Web/HTTP/Overview)

#### RDBMS
- Postgres 14
- SQLAlchemy ORM (https://www.sqlalchemy.org/)
- Alembic for schema and data migrations (https://alembic.sqlalchemy.org/en/latest/)

### Testing
- pytest test runner (https://docs.pytest.org/en/6.2.x/)
- `unittest.mock` for test doubles

### Design Principles (by Uncle Bob)
- [Lesson 1](https://www.youtube.com/watch?v=7EmboKQH8lM&t=582s)
- [Lesson 2](https://www.youtube.com/watch?v=2a_ytyt9sf8&t=1s)
- [Lesson 3](https://www.youtube.com/watch?v=Qjywrq2gM8o)
- [Lesson 4](https://www.youtube.com/watch?v=58jGpV2Cg50&t=4881s)

### Development methodology
We will be using an Agile ([Agile Manifesto](https://agilemanifesto.org/), [Agile Principles](https://agilemanifesto.org/principles)) framework with elements of [Scrum](https://www.scrum.org/resources/what-is-scrum) and [Kanban](https://www.atlassian.com/agile/kanban).


### How to start working on a ticket
We are using the [Gitlab flow](https://docs.gitlab.com/ee/topics/gitlab_flow.html)

All new features (tickets) must be developed in a separate branch. Use the following branch name template: `[feature|bugfix]<ticket-id>-short-description-of-changes` e.g.: in case if I'm working on issue 34, and I'm going to add `/users` endpoint in scope of this ticket, I'm going to create a branch called `feature-34-users-endpoint`.
After you done all needed changes, push branch to GitLab and create a merge request (MR). All MRs must be pointed to the `main` branch. Assign all your teammates as reviewers. Once you get an at least one approve from your peers AND approve from any TL (Tech OR Team Lead), proceed with merge.

In order to start development you need:
1. Pick a ticket and assign it to yourself.
2. Make sure that you understand the task and acceptance criteria (never start a task you do not understand, ask TL and PO to clarify it during grooming).
3. Create a feature branch in the format `[feature|bugfix]-<ticket-id>-<short-feature-description>` e.g.: `git checkout -b feature-42-the-ultimate-answer-to-everything`
4. Implement functionality and tests.
5. Run linter and formatter locally and fix all warnings and errors.
6. Run tests and make sure they are passing locally.
7. Make sure commit messages are descriptive. Commit summary should contain the ticket number and a short summary of the changes you have made. The summary ideally should not exceed 50 characters. The very first word should always reflect the type of changes you have made: “Add …”, “Remove …“, “Update …”, “Create …”. You should “virtually” read your commit summary as follows: (This commit will) "Add base layout”. The format is `<ticket-id> <short summary>.` E.g. `14 Create user endpoint`
8. Push your branch to gitlab e.g. `git push origin -u feature-42-the-ultimate-answer-to-everything`
9. Go to GitLab and create a merge request. Assign, and your teammates as reviewer.
10. Once you get approve from TL and at least one of your peers, feel free to merge the MR, squash commits and delete branch from the GitLab.

### Local dev env

Pre-requisites:
- Python 3.10
- Docker
- docker-compose
- poetry
- Poe

#### Build the app locally
```shell
poetry install
```

#### Run the app locally
```shell
poetry run uvicorn updateservice.app:app --host 0.0.0.0 --port 8080
```
Then open http://127.0.0.1:8080/docs in your browser

#### Run unit tests locally

poe clean
poe pytest
poe pytest --cov-report-type xml
poe pytest --cov-report-type html
poe test
poe test --cov-report-type xml
poe test --cov-report-type html

#### Run functional tests locally
poe test_api (Cleaning and testing)
poe testing (Tests the connection between API and the DB)
#### Create DB migration
TBD (SHOULD be written and updated here after completing Milestone 02 (see issue #11))

#### Upgrade DB schema
TBD (SHOULD be written and updated here after completing Milestone 02 (see issue #11))

#### Downgrade DB schema
TBD (SHOULD be written and updated here after completing Milestone 02 (see issue #11))