# create docker network
docker network create mongo-network

# start docker mongodb
docker run -d \
-p 27017:27017 \  
-e MONGO_INITDB_ROOT_USERNAME=admin \ 
-e MONGO_INITDB_ROOT_PASSWORD=secret \
--name mongo-db \
--net mongo-network \
mongo

# start docker mongo-express
docker run -d \
-p 8081:8081 \
-e ME_CONFIG_MONGODB_ADMINUSERNAME=admin \ 
-e ME_CONFIG_MONGODB_ADMINPASSWORD=secret \
--net mongo-network \
--name mongo-express \
-e ME_CONFIG_MONGODB_SERVER=mongo-db \ mongo-express
