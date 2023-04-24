# Steps

1 - Make a copy of .env.example to .env

2 - Adjust the variable OPENAI_API_KEY with your OpenAI key.

3 - Run
```
$ docker-compose up -d
```

4 - Run
```
$ docker-compose exec chatservice bash 
```

5 - Run
```
$ make migrate
```

6 - Run
```
$ make start
```