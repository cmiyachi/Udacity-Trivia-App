
  

# Trivia App

  

  

This is a project for an Udacity full stack nano-degree. This is a trivia game. When you play the game you will be randomly given five questions that you haven't seen previously. Your score from answering the five questions will be shown when you are done. You can delete questions. And you can pick categories of questions.

  
  

  

## Getting Started:

  
  
  

### Backend:

  

  

From the backend folder `../backend` run ```pip3 install -r requirements.txt```

  

  

All backend codes follow `PEP8 guideline`

  

  

### To run the application :

  

  

```bash

  

export FLASK_APP=flaskr

  

export FLASK_ENV=Development

  

flask run

  

```

  

  

The application is run on http://127.0.0.1:5000

  

  

### Frontend :

  

  

From the frontend folder `../frontend` run the following commands:

  

  

``` bash

  

npm install // only once

  

npm start

  

```

  

  

The front end will run on localhost:3000.

  

  

## Tests:

  

  

From the backend folder `../backend` run the following commands:

  

  

```

  

dropdb trivia_test

  

createdb trivia_test

  

psql trivia_test < trivia.psql

  

python test_flaskr.py

  

```

  

  

## API Reference

  

  

### Getting Started:

  

  

- Base URL: At present this app can only be run locally and is not hosted as a base URL.

  

The backend app is hosted at the default, http://127.0.0.1:5000/,

  

which is set as a proxy in the frontend configuration.

  

  

- Authentication: This version of the application does not require authentication or API keys.

  

  

### Error Handling:

  

Errors are returned as JSON objects in the following format:

  

  

    {
    
    "success": False,
    
    "error": 400,
    
    "message": "bad request"
    
    }

  

The API will return three error types when requests fail:

  

  

- 400: Bad Request

  

- 404: Resource Not Found

  

- 405: Method Not Allowed

  

- 422: Not Processable

  

## Endpoints

  

  

### GET '/categories'

  

- Gets the category names and ids

  

- Request Arguments: None

  

- Returns: A json object with the dictionary of id: category_name and whether there was success, and the total number of categories

  

  

`curl http://127.0.0.1:5000/categories`

  
```
{

    "categories": {
    
    "1": "Science",
    
    "2": "Art",
    
    "3": "Geography",
    
    "4": "History",
    
    "5": "Entertainment",
    
    "6": "Sports"
    
    },
    
    "success": true,
    
    "total_categories": 6
    
    }

  ```  

### GET /questions

  

  

- Gets the list of questions

  

- Request Arguments: optional page number starting from 1

  

- Results are paginated in groups of 10. Includes a list of categories and then a list of question objects along with success status and the number of questions.

  

  

`curl http://127.0.0.1:5000/questions`

  ```

    {
    
    "categories": {
    
    "1": "Science",
    
    "2": "Art",
    
    "3": "Geography",
    
    "4": "History",
    
    "5": "Entertainment",
    
    "6": "Sports"
    
    },
    
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
    
    },
    
    {
    
    "answer": "Blood",
    
    "category": 1,
    
    "difficulty": 4,
    
    "id": 22,
    
    "question": "Hematology is a branch of medicine involving the study of what?"
    
    },
    
    {
    
    "answer": "Escher",
    
    "category": 2,
    
    "difficulty": 1,
    
    "id": 16,
    
    "question": "Which Dutch graphic artist\u2013initials M C was a creator of optical illusions?"
    
    },
    
    {
    
    "answer": "Mona Lisa",
    
    "category": 2,
    
    "difficulty": 3,
    
    "id": 17,
    
    "question": "La Giaconda is better known as what?"
    
    },
    
    {
    
    "answer": "One",
    
    "category": 2,
    
    "difficulty": 4,
    
    "id": 18,
    
    "question": "How many paintings did Van Gogh sell in his lifetime?"
    
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
    
    },
    
    {
    
    "answer": "Agra",
    
    "category": 3,
    
    "difficulty": 2,
    
    "id": 15,
    
    "question": "The Taj Mahal is located in which Indian city?"
    
    },
    
    {
    
    "answer": "Maya Angelou",
    
    "category": 4,
    
    "difficulty": 2,
    
    "id": 5,
    
    "question": "Whose autobiography is entitled 'I Know Why the Caged Bird Sings'?"
    
    }
    
    ],
    
    "success": true,
    
    "total_questions": 18
    
    }

  ```

### DELETE /questions/{question_id}

  

- Deletes a question

  

- Arguments: The id of the question to delete

  

- Returns the id of the question deleted and sucess status

  

  

`curl -X DELETE http://127.0.0.1:5000/questions/10`

 ``` 

{

"deleted": 10,

"success": true

}
```
  

### POST /questions

  

  

Creates a new question or will search through questions. Returns the success value and id of the created question,

  

or a list of the search results if a search term was provided

  

  

`curl http://127.0.0.1:5000/questions --header "Content-Type: application/json" --request POST --data '{"question":"what is your name?", "answer" : "Chris", "difficulty":1,"category":5}' `

  

The output is the id created and success status:

  

  ```

{

"created": 25,

"success": true

}
```
  

  

For searching:

  

  

`curl http://127.0.0.1:5000/questions --header "Content-Type: application/json" --request POST --data '{"searchTerm":"title"}' `

  

  

And you get back:

  

  
```
{

"questions": [

{

"answer": "Maya Angelou",

"category": 4,

"difficulty": 2,

"id": 5,

"question": "Whose autobiography is entitled 'I Know Why the Caged Bird Sings'?"

},

{

"answer": "Edward Scissorhands",

"category": 5,

"difficulty": 3,

"id": 6,

"question": "What was the title of the 1990 fantasy directed by Tim Burton about a young man with multi-bladed appendages?"

}

],

"success": true,

"total_questions": 2

}

  ```

### GET categories/<int:cat_id>/questions

  

- Returns a list of question objects under the category requested, success value, and total number of questions,

  

current_category. Results are paginated in groups of 10.

  

  

-  `curl http://127.0.0.1:5000/categories/3/questions`

  
```
  

{

"current_category": 5,

"questions": [

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

"answer": "Chris",

"category": 5,

"difficulty": 1,

"id": 25,

"question": "what is your name?"

}

],

"success": true,

"total_questions": 4

}

  

 ``` 

### POST /quizzes

  

  

- Returns a random question not prevously used, a success value,

  

- Argument: A list of previous_questions objects and quizCategory;

  
  

`curl http://127.0.0.1:5000/quizzes --header "Content-Type: application/json" --request POST --data '{"previous_questions": [16,18],"quiz_category":{"id": 2}}' `

  

Returns

 ``` 

{

"question": {

"answer": "Mona Lisa",

"category": 2,

"difficulty": 3,

"id": 17,

"question": "La Giaconda is better known as what?"

},

"success": true

}

  ```
  

## Author:

  

  

### Chris Miyachi
