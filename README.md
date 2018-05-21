# Boilerplate Symfony

> Prerequisites :
- docker & docker-compose
- npm & yarn
- php 7.1 

### Start environment ( with docker )
```
cp .env.dist .env
make start
```

### Install the project ( for dev ):
```
make install
make build
```

### Help
```
make help :
 start:           Start docker containers
 stop:            Stop docker containers
 db@refresh:      Drop and re-create the database
 db@fixtures:     Launch doctrine fixtures
 install:         Install project dependencies
 build:           Build the project
 build@prod:      Build the project for prod (only)
 security:        Security check command from Symfony
 grum:            Run grumphp
 fix:             Launch php-cs-fixer on src/
```

### Technical test
- [French version](docs/technical_test_back_fr.md)
- [English version](docs/technical_test_back_en.md)