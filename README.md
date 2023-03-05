# example-mongodb [![Build Status](https://dev.azure.com/lganzzzo/lganzzzo/_apis/build/status/oatpp.example-mongodb?branchName=master)](https://dev.azure.com/lganzzzo/lganzzzo/_build/latest?definitionId=27&branchName=master)

Example project how to work with MongoDB using [oatpp-mongo](https://github.com/oatpp/oatpp-mongo) mondule.
Project is a web-service with basic CRUD and Swagger-UI.
*Dockerfile and docker-compose.yaml files included.*

More About Oat++:

- [Oat++ Website](https://oatpp.io/)
- [Oat++ Github Repository](https://github.com/oatpp/oatpp)
- [Get Started](https://oatpp.io/docs/start)

## Overview

### Dependencies

- [oatpp](https://github.com/oatpp/oatpp)
- [oatpp-swagger](https://github.com/oatpp/oatpp-swagger)
- [oatpp-mongo](https://github.com/oatpp/oatpp-mongo)
- [mongocxx](http://mongocxx.org/) - Temporary dependency. Until the oatpp-mongo driver will be ready-to-use*

### Project layout

```
|- CMakeLists.txt                        // projects CMakeLists.txt
|- src/
|    |
|    |- controller/                      // Folder containing Controller where all endpoints are declared
|    |- db/                              // Database class is here 
|    |- dto/                             // DTOs are declared here
|    |- App.cpp                          // main() is here
|    |- AppComponent.hpp                 // Service configuration is loaded here
|    |- SwaggerComponent.hpp             // Configuration for swagger-ui
|    
|- utility/install-oatpp-modules.sh      // utility script to install required oatpp-modules.
|- Dockerfile                            // Dockerfile
|- docker-compose.yaml                   // Docker-compose with this service and postgresql
```

## Build and Run
### Before run
**Requires** 

- mongocxx installed. To install mongocxx:  
   - On Mac `$ brew install mongo-cxx-driver`
   - On Linux - See Installing mongocxx on Linux section
      1. [Build mongo-c-driver]('https://mongoc.org/libmongoc/current/installing.html')  
         ```bash
         $  wget https://github.com/mongodb/mongo-c-driver/releases/download/1.23.2/mongo-c-driver-1.23.2.tar.gz
         $ tar xzf mongo-c-driver-1.23.2.tar.gz
         $ cd mongo-c-driver-1.23.2 
         $ mkdir cmake-build
         $ sudo cmake -DENABLE_AUTOMATIC_INIT_AND_CLEANUP=OFF ..
         $ sudo cmake --build . --target install
         ```
      2. [Build mongo-cxx-driver](https://mongocxx.org/mongocxx-v3/installation/linux/)
         ```bash
         $  curl -OL https://github.com/mongodb/mongo-cxx-driver/releases/download/r3.7.0/mongo-cxx-driver-r3.7.0.tar.gz
         $ tar -xzf mongo-cxx-driver-r3.7.0.tar.gz
         $ cd mongo-cxx-driver-r3.7.0
         $ mkdir cmake-build
         $ sudo cmake ..
         $ sudo cmake --build . --target install
         ```
   
- `oatpp`, `oatpp-swagger`, `oatpp-mongo` modules installed. You may run `utility/install-oatpp-modules.sh` 
script to install required oatpp modules. 
- add Environment Variable DEMO_MONGO_CONN_STR like:
   ```bash
   $ export DEMO_MONGO_CONN_STR=mongodb://localhost/UserDB
   ```
   or modify this line:
   ``` c++
   connectionString = m_cmdArgs.getNamedArgumentValue("--conn-str", "mongodb://localhost/UserDB");
   ```




```bash
$ mkdir build && cd build
$ cmake ..
$ make 
$ ./example-mongodb  # - run application.
```

- On `windows`:
   - use wsl2 and install ubuntu (or anorther distributions)
   - install mongodb on windows (or in wls2 linux distribution)

### After run

Go to [http://localhost:8000/swagger/ui](http://localhost:8000/swagger/ui) to try endpoints.

## Installing mongocxx on Linux

Installing mongocxx on Linux is an unclear and painful process.
See [ubuntu-cmake-mongocxx/Dockerfile](https://github.com/oatpp/dockerfiles/blob/master/ci/ubuntu-cmake-mongocxx/Dockerfile)
for instructions that worked for us.
