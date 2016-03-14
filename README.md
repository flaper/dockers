# Dockers for flaper

## Web
`docker run -d -p 3010:80 flaper/web` - then open at [http://localhost:3010](http://localhost:3010)

## Api
* `docker pull flaper/api` - only API

## Web with source && build
`docker run -d -p 3010:80 flaper/web.dev` - then open at [http://localhost:3010](http://localhost:3010)

## Others
* `docker pull flaper/backend` - backend
