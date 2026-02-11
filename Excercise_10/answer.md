### 1. Update last connection date

```mongodb
db.collections('users').updateOne(
  { _id: ObjectId("5cd96d3ed5d3e20029627d4a") },
  { $set: { last_connection_date: new Date() } }
)
```

### 2. Add admin role

```mongodb
db.collections('users').updateOne(
  { _id: ObjectId("5cd96d3ed5d3e20029627d4a") },
  { $addToSet: { roles: "admin" } }
)
```

### 3. Remove user role

```mongodb
db.collections('users').updateOne(
  { _id: ObjectId("5cd96d3ed5d3e20029627d4a") },
  { $set: { "addresses.$[addr].city": "Paris 1" } },
  { arrayFilters: [{ "addr.zip": 75001 }] }
)