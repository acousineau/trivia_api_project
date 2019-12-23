# Full Stack Trivia API Backend

## Getting Started

### Installing Dependencies

#### Python 3.7

Follow instructions to install the latest version of python for your platform in the [python docs](https://docs.python.org/3/using/unix.html#getting-and-installing-the-latest-version-of-python)

#### Virtual Enviornment

We recommend working within a virtual environment whenever using Python for projects. This keeps your dependencies for each project separate and organaized. Instructions for setting up a virual enviornment for your platform can be found in the [python docs](https://packaging.python.org/guides/installing-using-pip-and-virtual-environments/)

#### PIP Dependencies

Once you have your virtual environment setup and running, install dependencies by naviging to the `/backend` directory and running:

```bash
pip install -r requirements.txt
```

This will install all of the required packages we selected within the `requirements.txt` file.

##### Key Dependencies

- [Flask](http://flask.pocoo.org/)  is a lightweight backend microservices framework. Flask is required to handle requests and responses.

- [SQLAlchemy](https://www.sqlalchemy.org/) is the Python SQL toolkit and ORM we'll use handle the lightweight sqlite database. You'll primarily work in app.py and can reference models.py. 

- [Flask-CORS](https://flask-cors.readthedocs.io/en/latest/#) is the extension we'll use to handle cross origin requests from our frontend server. 

## Database Setup
With Postgres running, restore a database using the trivia.psql file provided. From the backend folder in terminal run:
```bash
psql trivia < trivia.psql
```

## Running the server

From within the `backend` directory first ensure you are working using your created virtual environment.

To run the server, execute:

```bash
export FLASK_APP=flaskr
export FLASK_ENV=development
flask run
```

Setting the `FLASK_ENV` variable to `development` will detect file changes and restart the server automatically.

Setting the `FLASK_APP` variable to `flaskr` directs flask to use the `flaskr` directory and the `__init__.py` file to find the application. 

## Tasks

One note before you delve into your tasks: for each endpoint you are expected to define the endpoint and response data. The frontend will be a plentiful resource because it is set up to expect certain endpoints and response data formats already. You should feel free to specify endpoints in your own way; if you do so, make sure to update the frontend or you will get some unexpected behavior. 

1. Use Flask-CORS to enable cross-domain requests and set response headers. 
2. Create an endpoint to handle GET requests for questions, including pagination (every 10 questions). This endpoint should return a list of questions, number of total questions, current category, categories. 
3. Create an endpoint to handle GET requests for all available categories. 
4. Create an endpoint to DELETE question using a question ID. 
5. Create an endpoint to POST a new question, which will require the question and answer text, category, and difficulty score. 
6. Create a POST endpoint to get questions based on category. 
7. Create a POST endpoint to get questions based on a search term. It should return any questions for whom the search term is a substring of the question. 
8. Create a POST endpoint to get questions to play the quiz. This endpoint should take category and previous question parameters and return a random questions within the given category, if provided, and that is not one of the previous questions. 
9. Create error handlers for all expected errors including 400, 404, 422 and 500. 

## API Reference

### `GET '/api/categories'`
Fetches a dictionary of `categories` in which the keys are the ids and the value is the corresponding string of the category

**Request Arguments**: `None`
* Example Request URL: `/api/categories`

```javascript
// Example Response
{
    "success": true,
    "categories": {
        "1" : "Science",
        "2" : "Art",
        "3" : "Geography",
        "4" : "History",
        "5" : "Entertainment",
        "6" : "Sports"
    }
}
```

### `GET '/api/questions'`
Fetches a dictionary containing:
* array of paginated `questions` (10 per page)
* object of `categories`
* a default `current_category`
* total number of `questions`.

**Request Arguments**:

Query Params:
* `page`: `<int>`
* Example Request URL: `/api/questions?page=2`

```javascript
// Example Response
{
    "success": true, 
    "categories": {
        "1": "Science", 
        ...
    }, 
    "current_category": "Science", 
    "questions": [
        {
            "answer": "Apollo 13", 
            "category": 5, 
            "difficulty": 4, 
            "id": 2, 
            "question": "What movie earned Tom Hanks his third straight Oscar nomination, in 1996?"
        },
        ...
    ], 
    "total_questions": 22
}
```

### `DELETE '/api/questions/<int:question_id>'`
Deletes a question specified by `question_id`

**Request Arguments**:
* Example Request URL: `/api/questions/3`

```javascript
// Example Response
{
    "success": true, 
    "deleted": 3
}
```

### `POST '/api/questions'` - **Question Creation**
Creates a question

**Request Arguments**:

* `question`: `<string>`
* `answer`: `<string>`
* `category`: `<string:category_id>`
* `difficulty`: `<string:1-5>`

```javascript
// Example Request Body
{
    "question": "How old am I?",
    "answer": "30",
    "difficulty": "3",
    "category": "4"
}
```

```javascript
// Example Response
{
    "success": true,
    "created": 29,
}
```

### `POST '/api/questions'` - **Search**
Searches against all questions and returns questions where the question text contains the entered search text

**Request Arguments**:

* `searchTerm`: `<string>`

```javascript
// Example Request Body
{
    "searchTerm": "How",
}
```

```javascript
// Example Response
// See Example Response for GET /api/questions
```

### `GET '/api/categories/<int:category_id>/questions'`
Gets paginated array of questions for given category based on `category_id`

**Request Arguments**:
* Example Request URL: `/api/categories/3/questions`

```javascript
// Example Response
{
    "success": true, 
    "current_category": "Science", 
    "questions": [
        {
            "answer": "Apollo 13", 
            "category": 5, 
            "difficulty": 4, 
            "id": 2, 
            "question": "What movie earned Tom Hanks his third straight Oscar nomination, in 1996?"
        },
        ...
    ], 
    "total_questions": 22
}
```

### `POST '/api/quizzes'`
Takes in a list of previous question_ids and a selected category to return a new random question that has not been used in previous questions and is part of the selected category.

**Request Arguments**:

* `previous_questions`: `[...<question_ids>]`
* `quiz_category`: `{ "type": <category_type>, id: <category_id> }`

```javascript
// Example Request Body
{
    "previous_questions": [2, 3],
    "quiz_category": {"type": "Science", "id": 3}
}
```

```javascript
// Example Response
{
  "question": {
    "answer": "Agra", 
    "category": 3, 
    "difficulty": 2, 
    "id": 15, 
    "question": "The Taj Mahal is located in which Indian city?"
  }, 
  "success": true
}
```

## Testing
To run the tests, run
```
dropdb trivia_test
createdb trivia_test
psql trivia_test < trivia.psql
python test_flaskr.py
```
