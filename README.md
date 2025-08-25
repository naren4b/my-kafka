# Install 
```bash
docker run --rm -d --name kafka-ui \
       --add-host=host.docker.internal:host-gateway  \
       -p 8080:8080 \
       -e DYNAMIC_CONFIG_ENABLED=true \
       provectuslabs/kafka-ui
       
docker run --rm -d --name=fast-data-dev \
  --add-host=host.docker.internal:host-gateway \
  -p 9092:9092 -p 8081:8081 -p 8083:8083 -p 3030:3030 \
  -e ADV_HOST=host.docker.internal \
  -e ADV_PORT=9092 \
  lensesio/fast-data-dev
```
# Connect 
```mermaid
flowchart LR
    subgraph Host-Machine
        UI8080["kafka-ui container (8080)"]
        FDD9092["fast-data-dev container (Kafka broker 9092)"]
    end

    UserBrowser["Web Browser (http://localhost:8080)"] -->|8080| UI8080

    UI8080 --"connects via host.docker.internal:9092"--> HostNetwork[Host Network :9092]
    HostNetwork --> FDD9092

```
Open http:localhost:8080 
Add Broker: "host.docker.internal:9092"


