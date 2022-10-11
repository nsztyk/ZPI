# API Reference

### User
---


#### ∘ Get user's data

```
GET /api/users/
```

response: Dict<userName, userEmail, userCurrency, userWeeklyReports, userAlertsOnEmail>

#### ∘ Update user's data

```
PUT /api/users/
```

#### ∘ Login

```

```

#### ∘ Registration

```

```


#### ∘ Password change

```

```

<br>

### Wallet
---

#### ∘ Get history of total UserAssets value

Also used to:
* get current UserAssets' total value
* get the difference between total values from last day and today

```
GET /api/user-assets/history?date-from=<dateFrom>&date-to=<dateTo>
```

| Parameter | Type     | Description                       |
| :-------- | :------- | :-------------------------------- |
| `dateFrom`      | `date` | **Required**. Beginning date of assetTotalValue|
| `dateTo`      | `date` | **Required**. End date of assetTotalValue |

response: Dict<date;totalUserAssetsValue>

<br>

### Assets
---


#### ∘ Get all assets
```
GET /api/assets/
```
response: Array<assetId, assetName, assetFriendlyName, assetType>


#### ∘ Update asset's value
```
PUT /api/assets/
```
body: Dict<assetName, valueUSD, dateTime>

#### ∘ Get asset history
```
GET /api/asset-history?date-from=<dateFrom>&date-to=<dateTo>&asset-name=<assetName>
```
response: Dict<value(+), date>


#### ∘ Trends of assets
Investigate external api's

<br>

### UserAssets
---

#### ∘ Create UserAsset
```
POST /api/user-assets/
```
body: Dict<asset-id, value>

Can create many UserAssets at once.


#### ∘ Update UserAsset
```
PATCH /api/user-assets/
```
body: Dict<operationType, assetId, value>

| OperationType |
| :-------- |
| add      |
| substract      |
| update  |


#### ∘ Delete user asset
```
DELETE /api/user-assets/id
```
action: deletes UserAsset and adds record to user's transaction history

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

### Alerts
---

#### ∘ Get alerts

```
GET /api/alerts/
```
response: Dict<alertId, targetValue, originAssetName, targetCurrency, originAssetType>

#### ∘ Create alert
```
POST /api/alerts/
```
body: Dict<originAssetName, targetCurrency, targetValue>

#### ∘ Delete alert
```
DELETE /api/alerts/id
```

#### ∘ Update alert
```
PUT  /api/alerts/id
```
body: Dict< targetValue>

returns: Dict<alertId, targetValue, originAssetName, targetCurrency, originAssetType>
