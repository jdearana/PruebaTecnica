# What should be added to the collection so that the query is not slow?
 Add indexes (createIndex) to email, last_connection_date, last_name, first_name


```mongodb
db.users.find({
  $expr: {
    $gte: [
      "$last_connection_date",
      {
        $dateSubtract: {
          startDate: "$$NOW",
          unit: "month",
          amount: 6
        }
      }
    ]
  },
  $or: [
    { email: searchTerm },
    { first_name: { $regex: "^" + searchTerm, $options: "i" } },
    { last_name: { $regex: "^" + searchTerm, $options: "i" } }
  ]
})
.collation({ locale: "en", strength: 2 })
.sort({ last_name: 1, first_name: 1 });
```