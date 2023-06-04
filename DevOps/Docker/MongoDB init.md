Volumes:
```yml
volumes:

      - ./mongoinit.js:/docker-entrypoint-initdb.d/mongoinit.js:ro

      - ./mongo:/data/db
```
MongoINIT.js
```js
const adminDatabase = db.getSiblingDB("admin");

adminDatabase.createUser({

  user: "<username>",

  pwd: "<password>",

  roles: [

    {

      role: "readWrite",

      db: "<database>",

    },

  ],

});

  

const tsmdb = db.getSiblingDB("<database>");

tsmdb.createCollection("delete_this");
```

And connection string will be this:
```
mongodb://tsmu:tsmpwd@localhost:27018/tsmdb?authSource=admin
```