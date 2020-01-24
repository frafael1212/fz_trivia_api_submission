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

REVIEW_COMMENT
```
This README is missing documentation of your endpoints. Below is an example for your endpoint to get all categories. Please use it as a reference for creating your documentation and resubmit your code. 

Endpoints
GET '/categories'
GET '/questions'
DELETE '/questions'
POST '/questions'
POST '/search'
GET '/categories/<int:c_id>/questions
POST '/quizzes'


GET '/categories'
- Fetches a dictionary of categories in which the keys are the ids and the value is the corresponding string of the category
- Request Arguments: None
- Returns: Dictionary with single key
{'1' : "Science",
'2' : "Art",
'3' : "Geography",
'4' : "History",
'5' : "Entertainment",
'6' : "Sports"}

GET '/questions'
- fetches nested dictionary...
- Request Arguments: "page" is integer variable expecting a value request argument named 'page' (i.e. /questions?page=2)
- Returns several objects. 1)dictionary key "questions" contains sub dictionaries. 2)current_cattegory object is a key with integer value for current catgory 3)categories is key with integer value for the number of categories available 4)'success' key is has a boolean value with result of whether or not questions were fetched successfully
{
  "categories": 6,
  "current_category": 2,
  "questions": [
    {
      "answer": "Maya Angelou",
      "category": 4,
      "difficulty": 2,
      "id": 5,
      "question": "Whose autobiography is entitled 'I Know Why the Caged Bird Sings'?"
    },
    {
      "answer": "Muhammad Ali",
      "category": 4,
      "difficulty": 1,
      "id": 9,
      "question": "What boxer's original name is Cassius Clay?"
    },
    {
      "answer": "Apollo 13",
      "category": 5,
      "difficulty": 4,
      "id": 2,
      "question": "What movie earned Tom Hanks his third straight Oscar nomination, in 1996?"
    },
    {
      "answer": "Tom Cruise",
      "category": 5,
      "difficulty": 4,
      "id": 4,
      "question": "What actor did author Anne Rice first denounce, then praise in the role of her beloved Lestat?"
    },
    {
      "answer": "Edward Scissorhands",
      "category": 5,
      "difficulty": 3,
      "id": 6,
      "question": "What was the title of the 1990 fantasy directed by Tim Burton about a young man with multi-bladed appendages?"
    },
    {
      "answer": "Brazil",
      "category": 6,
      "difficulty": 3,
      "id": 10,
      "question": "Which is the only team to play in every soccer World Cup tournament?"
    },
    {
      "answer": "Uruguay",
      "category": 6,
      "difficulty": 4,
      "id": 11,
      "question": "Which country won the first ever soccer World Cup in 1930?"
    },
    {
      "answer": "George Washington Carver",
      "category": 4,
      "difficulty": 2,
      "id": 12,
      "question": "Who invented Peanut Butter?"
    },
    {
      "answer": "Lake Victoria",
      "category": 3,
      "difficulty": 2,
      "id": 13,
      "question": "What is the largest lake in Africa?"
    },
    {
      "answer": "The Palace of Versailles",
      "category": 3,
      "difficulty": 3,
      "id": 14,
      "question": "In which royal palace would you find the Hall of Mirrors?"
    }
  ],
  "success": true,
  "total_questions": 21
}


DELETE '/questions'
- Deletes a quetion from the the questions table
- Request Arguments: 'id' integer matching question id
- Returns: 'status' string with either successful or failed submission

POST '/questions'
- Inserts a new question into the questions table
- Request Arguments: 'question' is string with the question, 'answer' is string with the answer, 'category' is integer for category joined field, 'difficulty' is integer. These are received through "Content-Type: application/json" header values
- Returns: 'status' string with either successful or failed submission


POST /search
- Fetches questions/objects based on a searchterm/substring
- Posted Arguments: 'searchTerm' is a string obtains from web form through "Content-Type: application/json" header
- Returns several objects. 1)dictionary key "questions" contains sub dictionaries with questions with substrings matchign search term. 2)current_cattegory object is a key with integer value for current catgory 3)total questions is integer with number of questions resulted from the search term 4)'success' key is has a boolean value with result of whether or not questions were fetched successfuly 

GET /cateories/<int:c_id>/questions'
- Returns questions matching category ID
- Request arguments: Category ID is Integer exatracted from endpoint
- Returns several objects. 1)dictionary key "questions" contains sub dictionaries with questions matching category ID 2)current_cattegory object is a key with integer value for current catgory 3)total questions is integer with number of questions matching category ID 4)'success' key is has a boolean value with result of whether or not questions were fetched successfuly


GET /quizzes
- Returns a random question. First it gets json arguments previous question and quiz category. Looks for questions available, with a category if chosen.. Then it removes makes a list of the IDs of the questions and removes any IDs that have already been used in previous questions. From that list of question that it randomly pick ones and returns it.
-Request Arguments: Previous Questions is json containing list of previous questions, and category ID is current category.
- Returns 1) Previous questions to keep avoid repeating and figure out when quizzed has ended 2)The question needed for the quiz and 3)Success boolean confirming question was fetched

```


## Testing
To run the tests, run
```
dropdb trivia_test
createdb trivia_test
psql trivia_test < trivia.psql
python test_flaskr.py
```
