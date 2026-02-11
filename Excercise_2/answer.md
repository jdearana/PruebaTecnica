**Problems:**
- The `total` conditionals should be inside the `then` callback
- In this case, `getTotalVehicles` should return `getTotalVehicles().then(total => ...)`
- Alternatively, make `getPlurial` async and add an `await` before `getTotalVehicles`
- `r` should be parsed because it's a response object

```typescript
// Call web service and return total vehicles, (got is library to call url)
async function getTotalVehicles() {
    return await got.get('https://my-webservice.moveecar.com/vehicles/total');
}

function getPlurial() {
    let total;
    getTotalVehicles().then(r => total = r);
    if (total <= 0) {
        return 'none';
    }
    if (total <= 10) {
        return 'few';
    }
    return 'many';
}
```