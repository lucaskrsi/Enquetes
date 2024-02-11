# NLW Expert Poll API

An API developed at the NLW Expert event that allows users to vote in polls and receive updates on the ranking of voted options in each poll in real time.

## 🚀 Technologies

<ul>
<li><img align="center" alt="Rafa-Js" height="30" width="40" src="https://cdn.jsdelivr.net/gh/devicons/devicon@latest/icons/docker/docker-plain-wordmark.svg"> Docker</li>
<li><img align="center" alt="Rafa-Js" height="30" width="40" src="https://cdn.jsdelivr.net/gh/devicons/devicon@latest/icons/typescript/typescript-original.svg"> Typescript</li>
<li><img align="center" alt="Rafa-Js" height="30" width="40" src="https://cdn.jsdelivr.net/gh/devicons/devicon@latest/icons/prisma/prisma-original.svg"> Prisma</li>
<li><img align="center" alt="Rafa-Js" height="30" width="40" src="https://cdn.jsdelivr.net/gh/devicons/devicon@latest/icons/redis/redis-original.svg"> Redis</li>
<li><img align="center" alt="Rafa-Js" height="30" width="40" src="https://cdn.jsdelivr.net/gh/devicons/devicon@latest/icons/nodejs/nodejs-original.svg"> NodeJS</li>
</ul>

## 🔨 How to setup


1. Clone this repository
2. Install the dependeces `npm install`
3. Setup PostgreSQL and Redis with `docker-compose up -d`
4. Setup your `.env` or copy `.env.example` and rename to `.env`
5. Run the application with `npm run dev`

💡TIPS: I recommend the usage of <a href="https://www.postman.com">Postman</a> or <a href="https://hoppscotch.io">Hoppscotch</a> to test it.

## Routes

### HTTP

#### POST `/polls`

Create a new poll.

##### Request body

```json
{
  "title": "What is your favorite color?",
  "options": [
    "Purple",
    "Red",
    "Orange",
    "Blue"
  ]
}
```

##### Response body

```json
{
  "pollId": "194cef63-2ccf-46a3-aad1-aa94b2bc89b0"
}
```

#### GET `/polls/:pollId`

Returns data from a single poll by ID..

##### Response body

```json
{
	"poll": {
		"id": "e4365599-0205-4429-9808-ea1f94062a5f",
		"title": "Qual a melhor linguagem de programação?",
		"options": [
			{
				"id": "4af3fca1-91dc-4c2d-b6aa-897ad5042c84",
				"title": "Purple",
				"score": 1
			},
			{
				"id": "780b8e25-a40e-4301-ab32-77ebf8c79da8",
				"title": "Red",
				"score": 0
			},
			{
				"id": "539fa272-152b-478f-9f53-8472cddb7491",
				"title": "Orange",
				"score": 0
			},
			{
				"id": "ca1d4af3-347a-4d77-b08b-528b181fe80e",
				"title": "Blue",
				"score": 0
			}
		]
	}
}
```

#### POST `/polls/:pollId/votes`

Add a vote to specific poll option.

##### Request body

```json
{
  "pollOptionId": "31cca9dc-15da-44d4-ad7f-12b86610fe98"
}
```

### WebSockets

#### ws `/polls/:pollId/results`

Receive updates from a specific poll.

##### Message

```json
{
  "pollOptionId": "da9601cc-0b58-4395-8865-113cbdc42089",
  "votes": 2
}
```
