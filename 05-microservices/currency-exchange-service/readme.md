# Currency Exchange Micro Service - H2

Run com.in28minutes.microservices.currencyconversionservice.CurrencyConversionServiceApplicationH2 as a Java Application.

## Resources

- http://localhost:8000/currency-exchange/from/USD/to/INR

```json
{
  "id": 10001,
  "from": "USD",
  "to": "INR",
  "conversionMultiple": 65.00,
  "environmentInfo": "NA"
}
```

## H2 Console

- http://localhost:8000/h2-console
- Use `jdbc:h2:mem:testdb` as JDBC URL


## Notes

### Basic - currency-conversion-service,currency-exchange-service 

```
docker network create currency-network
docker run -p 8100:8100 --network=currency-network --name=currency-conversion-service --env CURRENCY_EXCHANGE_URI=http://currency-exchange-service:8000 -d in28min/currency-conversion-service:0.0.1-SNAPSHOT
docker run -p 8000:8000 --network=currency-network --name=currency-exchange-service -d in28min/currency-exchange-service:0.0.1-SNAPSHOT
```
docker-compose.yml

```
version: '3.7'
services:
  currency-exchange-service:
    image: in28min/currency-exchange-service:0.0.1-SNAPSHOT
    ports:
      - "8000:8000"
    restart: always
    networks:
      - currency-compose-network

  currency-conversion-service:
    image: in28min/currency-conversion-service:0.0.1-SNAPSHOT
    ports:
      - "8100:8100"
    restart: always
    environment:
      CURRENCY_EXCHANGE_URI: http://currency-exchange-service:8000
    depends_on:
      - currency-exchange-service
    networks:
      - currency-compose-network

```

### Naming Server

```
docker run -p 8761:8761 --name naming-server --network currency-network in28min/netflix-eureka-naming-server:0.0.1-SNAPSHOT
docker run -p 8000:8000 --network currency-network --name currency-exchange-service in28min/currency-exchange-service:0.0.1-SNAPSHOT
docker run -p 8100:8100 --network currency-network --name currency-conversion-service in28min/currency-conversion-service:0.0.1-SNAPSHOT
```

docker-compose.yml

```  
version: '3.7'
services:

  naming-server:
    image: in28min/netflix-eureka-naming-server:0.0.1-SNAPSHOT
    ports:
      - "8761:8761"
    restart: always
    networks:
      - currency-compose-network

  currency-exchange-service:
    image: in28min/currency-exchange-service:0.0.1-SNAPSHOT
    #ports:
      #- "8000:8000"
    restart: always
    depends_on:
      - naming-server
    networks:
      - currency-compose-network

  currency-conversion-service:
    image: in28min/currency-conversion-service:0.0.1-SNAPSHOT
    ports:
      - "8100:8100"
    restart: always
    environment:
      CURRENCY_EXCHANGE_URI: http://currency-exchange-service:8000
    depends_on:
      - currency-exchange-service
      - naming-server
    networks:
      - currency-compose-network
  
# Networks to be created to facilitate communication between containers
networks:
  currency-compose-network:
```
### Naming Server & Zuul

```
docker run -p 8761:8761 --name naming-server --network currency-network in28min/netflix-eureka-naming-server:0.0.1-SNAPSHOT
docker run -p 8765:8765 --network currency-network --name zuul-api-gateway in28min/netflix-zuul-api-gateway-server:0.0.1-SNAPSHOT
docker run -p 8000:8000 --network currency-network --name currency-exchange-service in28min/currency-exchange-service:0.0.1-SNAPSHOT
docker run -p 8100:8100 --network currency-network --name currency-conversion-service in28min/currency-conversion-service:0.0.1-SNAPSHOT

```

```
```


### Zipkin, Naming Server & Zuul
```
docker network create currency-network
docker run -p 5672:5672 -p 15672:15672 --network currency-network --name rabbitmq rabbitmq:3.5.3-management
docker run -p 9411:9411 --env RABBIT_URI=amqp://guest:guest@rabbitmq:5672 --network currency-network --name zipkin openzipkin/zipkin
docker run -p 8761:8761 --name naming-server --network currency-network in28min/netflix-eureka-naming-server:0.0.1-SNAPSHOT
docker run -p 8000:8000 --network currency-network --name currency-exchange-service --env RABBIT_URI=amqp://guest:guest@rabbitmq:5672 in28min/currency-exchange-service:0.0.1-SNAPSHOT

docker run -p 8100:8100 --network currency-network --name currency-conversion-service --env RABBIT_URI=amqp://guest:guest@rabbitmq:5672 in28min/currency-conversion-service:0.0.1-SNAPSHOT

docker run -p 8765:8765 --network currency-network --name zuul-api-gateway  --env RABBIT_URI=amqp://guest:guest@rabbitmq:5672 in28min/netflix-zuul-api-gateway-server:0.0.1-SNAPSHOT
```

docker-compose.yml

```
version: '3.7'
services:

  rabbitmq:
    image: rabbitmq:3.5.3-management
    ports:
      - "5672:5672"
      - "15672:15672"
    restart: always
    networks:
      - currency-compose-network

  naming-server:
    image: in28min/netflix-eureka-naming-server:0.0.1-SNAPSHOT
    ports:
      - "8761:8761"
    restart: always
    networks:
      - currency-compose-network

  zipkin-server:
    image: openzipkin/zipkin
    container_name: zipkin
    environment:
      STORAGE_TYPE: mem
      RABBIT_URI: amqp://guest:guest@rabbitmq:5672
    ports:
      - "9411:9411"
    restart: always
    depends_on:
      - rabbitmq
    networks:
      - currency-compose-network


  zuul-api-gateway:
    image: in28min/netflix-zuul-api-gateway-server:0.0.1-SNAPSHOT
    environment:
      RABBIT_URI: amqp://guest:guest@rabbitmq:5672
    ports:
      - "8765:8765"
    restart: always
    depends_on:
      - naming-server
      - rabbitmq
      - zipkin-server
    networks:
      - currency-compose-network

  currency-exchange-service:
    image: in28min/currency-exchange-service:0.0.1-SNAPSHOT
    environment:
      RABBIT_URI: amqp://guest:guest@rabbitmq:5672
    ports:
      - "8000:8000"
    restart: always
    depends_on:
      - naming-server
      - rabbitmq
      - zipkin-server
    networks:
      - currency-compose-network

  currency-conversion-service:
    image: in28min/currency-conversion-service:0.0.1-SNAPSHOT
    ports:
      - "8100:8100"
    restart: always
    environment:
      #CURRENCY_EXCHANGE_URI: http://currency-exchange-service:8000
      RABBIT_URI: amqp://guest:guest@rabbitmq:5672
    depends_on:
      - currency-exchange-service
      - naming-server
      - rabbitmq
      - zipkin-server
    networks:
      - currency-compose-network
  
# Networks to be created to facilitate communication between containers
networks:
  currency-compose-network:
```

## Tables Created
```
create table exchange_value 
(
	id bigint not null, 
	conversion_multiple decimal(19,2), 
	currency_from varchar(255), 
	currency_to varchar(255), 
	primary key (id)
)
```

## Containerization

### Troubleshooting

- Problem - Caused by: com.spotify.docker.client.shaded.javax.ws.rs.ProcessingException: java.io.IOException: No such file or directory
- Solution - Check if docker is up and running!
- Problem - Error creating the Docker image on MacOS - java.io.IOException: Cannot run program “docker-credential-osxkeychain”: error=2, No such file or directory
- Solution - https://medium.com/@dakshika/error-creating-the-docker-image-on-macos-wso2-enterprise-integrator-tooling-dfb5b537b44e

### Creating Container

- mvn package

### Running Container

#### Basic
```
docker container run --publish 8000:8000 in28min/currency-exchange-service:0.0.1-SNAPSHOT
```
#### Custom Network
```
docker run --publish 8000:8000 --network currency-network --name=currency-exchange-service in28min/currency-exchange-service:0.0.1-SNAPSHOT
```

Test API 
- http://localhost:8000/currency-exchange/from/USD/to/INR

```
docker login
docker push @@@REPO_NAME@@@/currency-exchange-service:0.0.1-SNAPSHOT
```
