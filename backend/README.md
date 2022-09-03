# Backend - Trivia API

## Setting up the Backend

### Install Dependencies

1. **Python 3.7** - Follow instructions to install the latest version of python for your platform in the [python docs](https://docs.python.org/3/using/unix.html#getting-and-installing-the-latest-version-of-python)

2. **Virtual Environment** - We recommend working within a virtual environment whenever using Python for projects. This keeps your dependencies for each project separate and organized. Instructions for setting up a virual environment for your platform can be found in the [python docs](https://packaging.python.org/guides/installing-using-pip-and-virtual-environments/)

3. **PIP Dependencies** - Once your virtual environment is setup and running, install the required dependencies by navigating to the `/backend` directory and running:

```bash
pip install -r requirements.txt
```

#### Key Pip Dependencies

- [Flask](http://flask.pocoo.org/) is a lightweight backend microservices framework. Flask is required to handle requests and responses.

- [SQLAlchemy](https://www.sqlalchemy.org/) is the Python SQL toolkit and ORM we'll use to handle the lightweight SQL database. You'll primarily work in `app.py`and can reference `models.py`.

- [Flask-CORS](https://flask-cors.readthedocs.io/en/latest/#) is the extension we'll use to handle cross-origin requests from our frontend server.

### Set up the Database

Go to your SQL Shell to create a `trivia` database:

```bash
CREATE DATABASE trivia;
```

Then, navigate to the `backend` and run this👇 on your terminal depending what your username, password, localhost or port is:

```bash
postgresql://<username>:<password>@<hostname>:<port>/<database>
```

#### Populate the Database

After running the above👆 and it worked, run this👇 after:

```bash
\i trivia.psql
```

### Run the Server

From within the `backend` directory.

To run the server, execute this👇 to start the server:

```bash
pg_ctl -D "C:\Program Files\PostgreSQL\14\data" start
```

Execute this👇 to stop the server but keep the server on until you are done with the projet:

```bash
pg_ctl -D "C:\Program Files\PostgreSQL\14\data" stop
```

To run the flask app execute this👇:

```bash
export FLASK_APP=flaskr
export FLASK_ENV=development
flask run
```

If the `flask run` is resulting to errors, run this instead:

```bash
python -m flask run
```

## Tasks

These are the files you'd want to edit in the backend:

1. `backend/flaskr/__init__.py`
2. `backend/test_flaskr.py`

One note before you delve into your tasks: for each endpoint, you are expected to define the endpoint and response data. The frontend will be a plentiful resource because it is set up to expect certain endpoints and response data formats already. You should feel free to specify endpoints in your own way; if you do so, make sure to update the frontend or you will get some unexpected behavior.

1. Use Flask-CORS to enable cross-domain requests and set response headers.
2. Create an endpoint to handle `GET` requests for questions, including pagination (every 10 questions). This endpoint should return a list of questions, number of total questions, current category, categories.
3. Create an endpoint to handle `GET` requests for all available categories.
4. Create an endpoint to `DELETE` a question using a question `ID`.
5. Create an endpoint to `POST` a new question, which will require the question and answer text, category, and difficulty score.
6. Create a `POST` endpoint to get questions based on category.
7. Create a `POST` endpoint to get questions based on a search term. It should return any questions for whom the search term is a substring of the question.
8. Create a `POST` endpoint to get questions to play the quiz. This endpoint should take a category and previous question parameters and return a random questions within the given category, if provided, and that is not one of the previous questions.
9. Create error handlers for all expected errors including 400, 404, 422, and 500.

## API DOCUMENTATION

GET `/categories`, fetches all available categories in an object

- Request Arguments: None
- Returns: An object with a single key, `categories`, that contains an object of `id: category_string` key: value pairs.

```json
{
  "1": "Science",
  "2": "Art",
  "3": "Geography",
  "4": "History",
  "5": "Entertainment",
  "6": "Sports"
}
```

GET `questions?page=<page_num>`, fetches paginated object of all the categories

- Request Arguments: page_num(optional)
- Example:

```json
{
  "categories": {
    "1": "Science",
    "2": "Art",
    "3": "Geography",
    "4": "History",
    "5": "Entertainment",
    "6": "Sports"
  },
  "current_category": null,
  "questions": [
    {
      "answer": "Maya Angelou",
      "category": 4,
      "difficulty": 2,
      "id": 5,
      "question": "Whose autobiography is entitled 'I Know Why the Caged Bird Sings'?"
    },
    {
      "answer": "Escher",
      "category": 2,
      "difficulty": 1,
      "id": 16,
      "question": "Which Dutch graphic artist\u2013initials M C was a creator of optical illusions?"
    }
  ],
  "success": true,
  "total_questions": 2
}
```

DELETE `/questions/<question_id>`, deletes an existing questions from the repository of available questions

- Request Arguments: question_id
- Example:

```json
{
  "deleted": "5",
  "success": true
}
```

POST `/questions`, adds a new question to the repository of available questions

- Request Arguments: {question, answer, difficulty, category}
- Example:

```json
{
  "created": "6",
  "success": true
}
```

POST `/questions/search` Fetches all questions where a substring matches the search term (case-insensitive)

- Request Arguments: {search_term}
- Example:

```json
{
  "current_category": null,
  "questions": [
    {
      "answer": "Abuja",
      "category": 2,
      "difficulty": 1,
      "id": 29,
      "question": "What is the capital of Nigeria?"
    }
  ],
  "success": true,
  "total_questions": 1
}
```

GET `/categories/<int:category_id>/questions`, fetches a dictionary of questions for the specified category

- Request Arguments: category_id
- Example:

```json
{
  "current_category": 1,
  "questions": [
    {
      "answer": "The Liver",
      "category": 1,
      "difficulty": 4,
      "id": 20,
      "question": "What is the heaviest organ in the human body?"
    },
    {
      "answer": "Alexander Fleming",
      "category": 1,
      "difficulty": 3,
      "id": 21,
      "question": "Who discovered penicillin?"
    }
  ],
  "success": true,
  "total_questions": 2
}
```

POST `/quizzes`, fetches one random question within a specified category. Previously asked questions are not asked again.

- Request Arguments: {previous_questions: arr, quiz_category}
- Example:

```json
{
  "question": {
    "answer": "The Liver",
    "category": 1,
    "difficulty": 4,
    "id": 20,
    "question": "What is the heaviest organ in the human body?"
  },
  "success": true
}
```

## Testing

Write at least one test for the success and at least one error behavior of each endpoint using the unittest library.

To deploy the tests, run

```bash
dropdb trivia_test
createdb trivia_test
psql trivia_test < trivia.psql
python test_flaskr.py
```
