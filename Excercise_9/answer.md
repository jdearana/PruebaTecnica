## 9. Aggregation

```mongodb
db.collections('users').aggregate([
  {
    $unwind: "$roles"
  },
  {
    $group: {
      _id: "$roles",
      users: { $addToSet: "$email" }
    }
  }
])
```