### TERMINAL1
```bash
start mongod --replSet m101 -logpath \data\rs1\1.log --dbpath \data\rs1 --port 27020
```

### TERMINAL2
```bash
start mongod --replSet m101 -logpath \data\rs2\2.log --dbpath \data\rs2 --port 27021
```

### TERMINAL3
```bash
start mongod --replSet m101 -logpath \data\rs3\3.log --dbpath \data\rs3 --port 27022
```

### TERMINAL1
```bash
mongosh --port 27020

config = { _id: "m101", members:[
          { _id : 0, host : "localhost:27020"},
          { _id : 1, host : "localhost:27021"},
          { _id : 2, host : "localhost:27022"} ]
         };


rs.initiate(config);
rs.status();

use cbit
db.it3.find();

```

### TERMINAL2

```bash
mongosh --port 27021
rs.secondaryOk()
db.products.find();
```
### TERMINAL3

```bash
mongosh --port 27022
rs.secondaryOk()
db.products.find();
```

### TERMINAL1
```bash
use admin;
db.shutdownServer();
```


### open a TERMINAL2 & TERMINAL3
```bash
rs.status();
```

