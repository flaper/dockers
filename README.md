# Dockers for flaper

## Web
`docker run -d -p 3010:80 flaper/web` - then open at [http://localhost:3010](http://localhost:3010)

## Api
 `docker run -it --net="host" flaper/api` - starts API on 4000 port, expect host mongo to be available

## Web with source && build
`docker run -d -p 3010:80 flaper/web.dev` - then open at [http://localhost:3010](http://localhost:3010)

## Others

#### Render
`docker run -it --net="host" flaper/render` - starts render on [http://localhost:1337](http://localhost:1337), , expect host mongo to be available

#### Backend
 `docker pull flaper/backend` - backend
