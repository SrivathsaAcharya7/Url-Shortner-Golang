# G0LANGBITLY

A golang implementation of URL shortener like <a href="https://bitly.com/">Bitly</a>


## Tech-Stack

<a href="https://go.dev/" target="_blank">Golang</a>&nbsp;
<a href="https://gofiber.io/" target="_blank">Gofiber</a>&nbsp;
<a href="https://redis.io/" target="_blank">Redis</a>&nbsp;
<a href="https://www.docker.com/" target="_blank">Docker</a>&nbsp;


## Features

: &nbsp;Users can create custom shorten URL

: &nbsp;Rate limiter to restrict users to exploit the API

: &nbsp;Containerized the whole application using Docker and Docker-compose for easy set-up

: &nbsp;Suitable checks for non-redundancy in URL creation 

## Project Setup
- Clone the repository using `git clone <repo_url>`
- Go to the project directory using `cd golang-url-shortener`
- Run `go mod tidy` or you can manually install all the golang dependencies using `go get <dep_name>` command.
- Install docker and docker-compose on windows, follow these [instructions](https://docs.docker.com/desktop/install/windows-install/) for easy setup.
- Create a `.env` file in `/api/` folder similar to `.env.example` file. 
- Run `docker-compose up -d` to spin the docker containers for Go-Fiber server and Redis database at ports `localhost:3000` and `localhost:6379` respectively.
- You can test the API using [postman](https://www.postman.com/) or VSCode's [thunder client](https://marketplace.visualstudio.com/items?itemName=rangav.vscode-thunder-client) using following api call:
  - **POST** request at `localhost:3000/api/v1` with body:
  ```json
  {
    "url" : "URL_TO_BE_SHORTEN",
    "custom" : "UNIQUE_CUSTOM_URL_ID"
  }
  ```
  which will respond you with a response format:
  ```json
  {
     "url":                "URL_TO_BE_SHORTEN",
     "short":              "SHORTEN_URL",
	 "expiry":             "Cache expiry {set to 30 mins}",
	 "rate_limit":         "No of times the API have been called", 
	 "rate_limit_reset":   "After how much time the rate limit will reset (in hours)",
  }
  ```
  
  - **GET** request at `localhost:3000/:URL_TO_BE_SHORTEN` will redirect to the original URL.