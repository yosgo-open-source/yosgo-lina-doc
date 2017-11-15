# Yosgo API

# Yosgo-API-v2

## Restfully Basic （通常）

- [GET] /resources -- 取得資訊
- [POST] /resources -- 新增資訊
- [PUT] /resources/:id -- 更新資訊
- [PATCH] /resources/:id -- 更新資訊
- [DELETE] /resources/:id -- 刪除資訊

## API URL

- https://yosgo-api-policer.herokuapp.com/

---

### Brand

#### < Create >

##### HTTP request

`[POST] /brands`

##### Request headers

|Request header|Description|
|--------------|-----------|
|Content-Type|application/json|
|authorization|api key (Bearer 39281829309809JWIEWOOIJOI8979840234OIJW10293)|

##### Request body

|Field|Type|Required|Description|
|--------------|-----------|----|----|
|title|String|Yes|brand title|

##### Response body

return status 200 and empty JSON object

#### < READ >

##### HTTP request

`[GET] /brands`

##### Request headers

|Request header|Description|
|--------------|-----------|
|Content-Type|application/json|
|authorization|api key (Bearer 39281829309809JWIEWOOIJOI8979840234OIJW10293)|

##### Request body

|Field|Type|Required|Description|
|--------------|-----------|----|----|

##### Response body

|Field|Type|Description|
|--------------|----|----|
|objectId|string|brand uuid|
|title|string|brand title text|
|createdAt|string|brand create date|

return status 200

---

### Product

#### < Create >

##### HTTP request

`[POST] /products`

##### Request headers

|Request header|Description|
|--------------|-----------|
|Content-Type|application/json|
|authorization|api key (Bearer 39281829309809JWIEWOOIJOI8979840234OIJW10293)|

##### Request body

|Field|Type|Required|Description|
|--------------|-----------|----|----|
|brandId|String|Yes|brand id for create own product|
|title|String|Yes|product title|
|description|String|Yes|description|
|photo|File|No|file path|
|requiredQuantity|Number|Yes|required quantity|
|unitPrice|Number|Yes|unit price|
|groupDayLength|Number|Yes|create group end date expired time|
|endDateTime|Date|Yes|end date expired time|
|isActive|Bool|Yes|active this product or not|

##### Response body

return status 200 and empty JSON object

#### < Get >

##### HTTP request

`[GET] /products`

##### Request headers

|Request header|Description|
|--------------|-----------|
|Content-Type|application/json|
|authorization|api key (Bearer 39281829309809JWIEWOOIJOI8979840234OIJW10293)|

##### Request body

|Field|Type|Required|Description|
|--------------|-----------|----|----|

##### Response body

return status 200 and JSON Array< object >

|Field|Type|Description|
|--------------|-----------|----|
|title|string|product title|
|description|string|product description|
|isActive|boolean|product is active or not|
|requiredQuantity|number|product required quantity|
|unitPrice|number|product unit price|
|groupDayLength|number|product group day length|
|endDateTime|Date|product end date time|
|endDateTime|Date|product end time|

#### < Get Info >

##### HTTP request (Cache for 15 min)

`[GET] /products/productId`

##### Request headers

|Request header|Description|
|--------------|-----------|
|Content-Type|application/json|
|authorization|api key (Bearer 39281829309809JWIEWOOIJOI8979840234OIJW10293)|

##### Request body

|Field|Type|Required|Description|
|--------------|-----------|----|----|

##### Request params

/product/:productId

##### Response body

return status 200 and JSON Array<object>

|Field|Type|Description|
|--------------|-----------|----|
|title|string|product title|
|description|string|product description|
|isActive|boolean|product is active or not|
|requiredQuantity|number|product required quantity|
|unitPrice|number|product unit price|
|groupDayLength|number|product group day length|
|endDateTime|Date|product end date time|
|endDateTime|Date|product end time|
|priceInfo|{totalPrice, totalArchevePrice}|this product totalPrice and totalArchevePrice|
|group|Object|product total group|
|payment|Object|product total payment|

---

### Group

#### < Create >

##### HTTP request

`[POST] /groups`

##### Request headers

|Request header|Description|
|--------------|-----------|
|Content-Type|application/json|
|authorization|api key (Bearer 39281829309809JWIEWOOIJOI8979840234OIJW10293)|

##### Request body

|Field|Type|Required|Description|
|--------------|-----------|----|----|
|productId|string|Y|create group for specifies product|
|note|string|N|group note|

##### Response body

return status 200 and JSON

|Field|Type|Description|
|--------------|-----------|----|
|payload|{groupId, createdAt}|create return payload|
|message|string|return message when create success|
|status|number|http create status|
|error|string|return error when create failed|

---

### Order

#### < Create >

##### HTTP request

`[POST] /orders`

##### Request headers

|Request header|Description|
|--------------|-----------|
|Content-Type|application/json|
|authorization|api key (Bearer 39281829309809JWIEWOOIJOI8979840234OIJW10293)|

##### Request body

|Field|Type|Required|Description|
|--------------|-----------|----|----|
|order|OrderCreateType|Y|order create required info|
|registration|RegistrationType|Y|order registration info|

##### TypeInfo

```
OrderCreateType {
  quantity: Number,
  productId: String,
  groupId: String
}

RegistrationType {
  name: String,
  phone: String,
  email: String,
  notes: String,
  address: String
}

OrderType {
  orderId: String,
  createdAt: Date
}
```

##### Response body

return status 200 and JSON

|Field|Type|Description|
|--------------|-----------|----|
|payload|OrderType|create return payload|
|message|string|return message when create success|
|status|number|http create status|
|error|string|return error when create failed|

#### < READ >

##### HTTP request

`[GET] /orders`

##### Request headers

|Request header|Description|
|--------------|-----------|
|Content-Type|application/json|
|authorization|api key (Bearer 39281829309809JWIEWOOIJOI8979840234OIJW10293)|

##### Request body

|Field|Type|Required|Description|
|--------------|-----------|----|----|

##### TypeInfo

```
OrderType {
  objectId: String,
  payment: PaymentType,
  product: ProductType,
  company: CompanyType,
  group: GroupType,
  registration: RegistrationType,
  extraRegistration: Array<Object>,
  data: DataType,
  quantity: Number,
  isArchived: Boolean,
  createdAt: Date,
  updatedAt: Date,
}
```

##### Response body

|Field|Type|Description|
|--------------|----|----|
|payload|OrderType|create return payload|
|message|string|return message when create success|
|status|number|http create status|
|error|string|return error when create failed|

return status 200

---
