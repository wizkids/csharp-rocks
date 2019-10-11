# C# Rocks!

Welcome to the Wizkids C# test!
The test is inspired by one of our products (AppWriter) which helps people with reading/writing troubles by enabling them to read text out load and get word suggestions (predictions) while typing.

Predictions are word completions based on the input text, for example:
If the input text is `I like ca` the predictions could be `cars`, `cats` and `cake`.

The test requires you to create a small front-end and back-end that implements the word prediction functionality with results from a custom dictionary and our word prediction web service.

If you encounter any unexpected issues please contact us at `srs AT wizkids.dk` and we will get back to you ASAP.

## Scope

We expect a simply structured HTML/CSS/JS/C# project with good readability. Design and UX is not a major consideration - keeping it simple is fine.

We expect a well-versed developer to be able to complete the tasks within a couple of hours.

*While a simple test project you should treat it as a project that should run in production in a business environment.*

## Back-end tasks

#### 1. Write a client for the word predictions web service.

#### 2. Write a service for fetching words from the custom dictionary.

#### 3. Write a web API for your front-end.

The API should perform the following tasks:

1. Listen for HTTP requests from the front-end.
2. Fetch word predictions from the word predictions web service based on input from the front-end (using the client from task #1).
3. Fetch custom dictionary words based on input from the front-end (using the service from task #2).
4. Send the two lists of words as a JSON result in the HTTP response.


## Front-end tasks

#### 1. Write HTML/CSS for displaying a `<textarea>` and two lists of word prediction results (word prediction web service and custom dictionary).

#### 2. Write a JavaScript function that performs a web request to fetch word predictions from your back-end API.

#### 3. On every keypress event in the `<textarea>` fetch word predictions based on the text value and display the results in the two lists.


## Miscellaneous tasks

#### 1. Generate a token for use with the word predictions web service at https://services.lingapps.dk/misc/jobAdvert.

#### 2. Add your code in a Git project on GitHub and submit the link at https://services.lingapps.dk/misc/jobAdvert.

(OPTIONAL, but strongly recommended) Also add a link to one of your C# projects (in which you've been a major contributor) - Git repository preferred.

## Custom dictionary description

The custom dictionary is implemented as an SQLite 3 database (`Dictionary.db`). It contains a `Words`table with the columns `Id` and `Value`.

The database is not encrypted/does not require a password.

If you have issues downloading the database file directly (GitHub some times display a 404 error), try cloning the project instead.


## Word predictions web service description

#### URL
`https://services.lingapps.dk/misc/getPredictions`

#### Authorization
Header: `Authorization: Bearer [TOKEN]` (token generated in Miscellaneous task #1)

#### Parameters
  - `locale`: String, the language in which the predictions should be computed. Valid values are `da-DK` and `en-GB`.
  - `text`: String, the text from which to compute the predictions.

#### Response
JSON encoded array of strings ordered by prediction probability (descending), for example:
`["cars", "cats", "cake"]`

#### Example

**Request**
```
GET /misc/getPredictions?locale=en-GB&text=I%20like%20ca HTTP/1.1
Host: services.lingapps.dk
Authorization: Bearer MjAxOS0wMS0wMQ==.dGVzdEBleGFtcGxlLmNvbQ==.MjExMWMyYjdjZGY3YTU3MmU4MTA5OWY0MDgyMmM0OTk=
Connection: Close

```
**Response**
```
HTTP/1.1 200 OK
Content-Length: 34
Connection: close
Content-Type: application/json

[
    "cars",
    "cats",
    "cake"
]
```
