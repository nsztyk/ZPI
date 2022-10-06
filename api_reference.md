# API Reference

### User
---

#### ∘ Login

```

```

#### ∘ Registration

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

#### ∘ Trends of assets
Investigate external api's

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
