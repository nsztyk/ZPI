# API Reference

### User

#### Login

```

```

#### Registration

```

```


### Wallet

#### Get total UserAssets value history 
also used to get current UserAssets total value and to get the difference of total value from last day
```
GET /api/user-assets/history?dateFrom=<dateFrom>&dateTo=<dateTo>
```
| Parameter | Type     | Description                       |
| :-------- | :------- | :-------------------------------- |
| `dateFrom`      | `date` | **Required**. Beginning date of assetTotalValue|
| `dateTo`      | `date` | **Required**. End date of assetTotalValue |

Response data:
```
Dict<date;total_user_assets_value>

Number - total UserAssets value
```

### Assets

#### Trends of assets
Investigate external api's

#### Get all assets
```
GET /api/assets/
```
Response data
```
Array<asset_id, asset_name, asset_friendly_name, asset_type>
```
