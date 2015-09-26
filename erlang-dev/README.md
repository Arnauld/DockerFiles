Don't forget to change `UPDATED` ENV value to ensure git's repositories are fetched when modified, 
otherwise docker's layers are considered unchanged.

(in dockermachine bash)

```bash
$ docker build -t arnauld/erlang-dev .
$ docker run -t -i arnauld/erlang-dev
```
