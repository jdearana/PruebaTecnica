**Problems:**
1. `const result = getCountUsers()` needs an await: `const result = await getCountUsers();`
2. `total: await got.get('https://my-webservice.moveecar.com/users/count')` returns a response object, so adding 20 is incorrect. We need to parse the body and search for the total property.

```typescript
// Call web service and return count user, (got is library to call url)
async function getCountUsers() {
  return { total: await got.get('https://my-webservice.moveecar.com/users/count') };
}

// Add total from service with 20
async function computeResult() {
  const result = getCountUsers();
  return result.total + 20;
}
```
