**Build Back-End (Node)**
```
cd backend
docker build -t goals-node .
```

Create `.env` file in backend and add the following
```
MONGODB_USERNAME=yourusername
MONGODB_PASSWORD=yourpassword
```

**Build Front-End (React)**
```
cd frontend
docker build -t goals-react .
```

**Create Network**
```
docker network create goals-net
```

**Run MongoDB**
```
docker run -d -v data:/data/db -e MONGO_INITDB_ROOT_USERNAME=yourusername -e MONGO_INITDB_ROOT_PASSWORD=yourpassword --network goals-net --name mongodb mongo
```

MSYS_NO_PATHCONV=1 is required if using Git Bash under Windows

**Run Back-End (Node)**
```
MSYS_NO_PATHCONV=1 docker run -p 80:80 --env-file ./.env -v logs:/app/logs -v $(pwd):/app:ro -v /app/node_modules --network goals-net --name goals-backend goals-node
```

**Run Front-End (React)**
```
MSYS_NO_PATHCONV=1 docker run -it -p 3000:3000 -v $(pwd)/src:/app/src --name goals-frontend goals-react
```