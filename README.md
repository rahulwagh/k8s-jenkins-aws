## 1. Build Docker image
```commandline
docker build -t java-rest-api .
```

## 2. Run Docker image
```commandline
docker run -p 9002:9002 java-rest-api
```