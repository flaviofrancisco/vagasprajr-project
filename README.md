# Welcome

This is the @vagasprajr project, where you can have a fully functional environment to work with the [Vagas Pra Jr](https://vagasprajr.com.br) API locally.

## How to use

1. Clone this repository
2. Rename the `.env.example` file to `.env` and update the variables with your own values
3. Run the following command to install the dependencies:

```bash
docker-compose up -d
```

4. Access the [Vagas Pra Jr](http://localhost:3000) home page at [http://localhost:300](http://localhost:3001)

5. Create you account at: [http://localhost:3000/criar-conta](http://localhost:3000/criar-conta)

Once you account is created you need to access the database container and update the user role to `admin` in order to have access to the admin panel.

```bash
docker exec -it db bash
```

Then, access the database:

mongodb://admin:password@localhost:27017/vagasprajrdb?authSource=admin

```bash
mongosh

use admin

db.auth("admin", "password")

use vagasprajrdb

db.createCollection('roles')

db.('roles').insertMany([
    {
        _id: ObjectId("650d5e137ece568cd2f11a0a"),
        name: "admin"
    },
    {
        _id: ObjectId("650d5e137ece568cd2f11a0b"),
        name: "candidate"
    },
    {
        _id: ObjectId("650d5e137ece568cd2f11a0c"),
        name: "recruiter"
    },
    {
        _id: ObjectId("650d5e137ece568cd2f11a0d"),
        name: "company"
    }
])

db.users.updateOne(
  { email: "your_email@domain.com" }, 
  { $set: { is_email_confirmed: true } },
  { upsert: true }
);
```

Now you can login with your credentials and access all the features at [http://localhost:3000](http://localhost:3000)