# API Reference

### User
---


#### ∘ Get user's data *

```
GET /api/users/
```

response: Dict<userName, userEmail, userCurrency, userWeeklyReports, userAlertsOnEmail>

| Parameter | Type     | Description                       |
| :-------- | :------- | :-------------------------------- |
| `userCurrency`      | `string` | Defines user's main currency (PLN/EUR/USD) |
| `userWeeklyReports`      | `boolean` | Determines whether user will get weekly reports |
| `userAlertsOnEmail`      | `boolean` | Determines whether user will get alerts on email |


#### ∘ Update user's data *

```
PUT /api/users/
```
body: Dict<userCurrency, userWeeklyReports, userAlertsOnEmail>


| Parameter | Type     | Description                       |
| :-------- | :------- | :-------------------------------- |
| `userCurrency`      | `string` | Defines user's main currency (PLN/EUR/USD) |
| `userWeeklyReports`      | `boolean` | Determines whether user will get weekly reports |
| `userAlertsOnEmail`      | `boolean` | Determines whether user will get alerts on email |

#### ∘ Login *

```

```

#### ∘ Registration *

```

```


#### ∘ Password change *

```

```

<br>

### Assets
---


#### ∘ Get all assets *
```
GET /api/assets/
```
response: Array<Name, FriendlyName, Category, Symbol> - for alerts microservice we will need this type of endoint but with Array<Name, Value> (join Asset and AssetValue)


#### ∘ Update asset's value *
```
PUT /api/assets/
```
body: Dict<assetName, valueUSD, dateTime>
after updating assetPrice there should be PUT to alerts microservice:
body: updatedAssetName, Dict<assetName, valueUSD>
The dict contains all assets.

#### ∘ Get asset history 
```
GET /api/asset-history?date-from=<dateFrom>&date-to=<dateTo>&asset-name=<assetName>
```
response: Dict<value(+), date>

#### ∘ Get asset current
```
GET /api/asset-history
```
Same as get asset history but today and batch.

response: Dict<name, value(+)>


#### ∘ Trends of assets
Investigate external api's

<br>

### UserAssets
---

#### ∘ Get all UserAssets *
```
GET /api/user-assets/
```
response: Array<assetId, assetName, assetFriendlyName, assetType, symbol, originValue, userCurrencyValue>


#### ∘ Create UserAsset *
```
POST /api/user-assets/
```
body: Dict<assetId, value>

Can create many UserAssets at once.


#### ∘ Update UserAsset *
```
PATCH /api/user-assets/
```
body: Dict<operationType, assetId, value>

| OperationType |
| :-------- |
| update      |
| set      |

Update +/- and updated 
Set only +, sets


#### ∘ Delete user asset *
```
DELETE /api/user-assets/id
```
action: deletes UserAsset and adds record to user's transaction history

<br>

### Wallet
---

#### ∘ Get history of total UserAssets value

It should be saved somehow at the end of they (worker from c# side, or endpoint provided to execute the save and updater
microservice sending the request.The value should be counted not from datebase, but should be counted from current UserAssets and saved in dolars.
Also this should be returned in users preferenceCurrency, which can be counted by joining it with "Get asset history current" view. 
Also used to:
* get the difference between total values from last day and today

```
GET /api/api/wallet/?from=<dateFrom>&to=<dateTo>
```

| Parameter | Type     | Description                       |
| :-------- | :------- | :-------------------------------- |
| `dateFrom`      | `date` | **Required**. Beginning date of assetTotalValue|
| `dateTo`      | `date` | **Required**. End date of assetTotalValue |

response: Dict<timeStamp;value>

### ∘ Get current total User Assets value
Sums all the assets of user, takes his currency preference and devide by it if nessesary, then returs it.
response: totalUserAssetsValue

```
GET /api/api/wallet/total
```

response: totalValue

<br>


### Transactions
---

#### ∘ Get transaction history

```
GET /api/transactions?date-from=<dateFrom>&date-to=<dateTo>
```

| Parameter | Type     | Description                       |
| :-------- | :------- | :-------------------------------- |
| `dateFrom`      | `date` | **Required**. Beginning date of assetTotalValue|
| `dateTo`      | `date` | **Required**. End date of assetTotalValue |

response: Dict<assetName, value, date>

<br>

### Alerts
alerts endpoints are only proxy beetwen c# service and microservice. There should not be any Alerts database model in c# (only DTO).
---

#### ∘ Get alerts *

```
GET /api/alerts/
```
response: Dict<alertId, targetValue, originAssetName, targetCurrency, originAssetType>

#### ∘ Create alert *
```
POST /api/alerts/
```
body: Dict<originAssetName, targetCurrency, targetValue>
The proxy should sent to microservice:
body: <originAssetName, targetCurrency, targetValue, email, currentValue>
currentValue - originAsset currentValue in targetCurrency

#### ∘ Delete alert *
```
DELETE /api/alerts/id
```
