# Invoice

## Get invoice

This command is used to obtain an invoice for a client.


```curl
$ch = curl_init();
curl_setopt($ch, CURLOPT_URL, 'http://api.dichvuchothuechodat.top/api/v1/getinvoice');
curl_setopt($ch, CURLOPT_POST, 1);
curl_setopt($ch, CURLOPT_POSTFIELDS,
    http_build_query(
        array(
        	'email'		 	=> 'lanpt@kdata.vn',
        	'password'   	=> '$2y$10$vWkQJ45jOC47ujpxxu6eWesZNodJnbqD.K.vlsUNYb9pl3',
        	'invoiceid'    	=> '171'
        )
    )
);
$response = curl_exec($ch);
curl_close($ch);
```

>The above command returns JSON structured like this:

```json
{
  "result": "success",
  "invoiceid": "171",
  "invoicenum": "",
  "userid": "3",
  "date": "2017-01-06",
  "duedate": "2017-01-06",
  "datepaid": "0000-00-00 00:00:00",
  "subtotal": "450000.00",
  "credit": "0.00",
  "tax": "0.00",
  "tax2": "0.00",
  "total": "450000.00",
  "balance": "450000.00",
  "taxrate": "0.00",
  "taxrate2": "0.00",
  "status": "Unpaid",
  "paymentmethod": "banktransfer",
  "notes": "",
  "ccgateway": false,
  "items": {
    "item": [
      {
        "id": "172",
        "type": "Hosting",
        "relid": "171",
        "description": "VPS 01 (06/01/2017 - 05/02/2017)\nDATA CENTER: VIỆT NAM\nServer OS: Centos 6.x 64Bit\nCPU: 2 Core\nRAM: 1GB\nHDD: 40G\nExtra IP: 3 x IP VND50,000VND",
        "amount": "450000.00",
        "taxed": "0"
      }
    ]
  },
  "transactions": ""
}
```

### Http Request

`POST http://api.dichvuchothuechodat.top/api/v1/getinvoice`


### Request Parameters

Parameter | Type | Description | Required
--------- | ---- | ----------- | --------
email | string | Your email | Yes
password | string | Provided by Kdata | Yes
invoiceid | int |  The ID of the invoice to retrieve| Yes

### Response Parameters
Parameter | Type | Description
--------- | ---- | -----------
result | string | The result of the operation: success or error
invoiceid | int | The id of the invoice
invoicenum | string | The Sequential invoice number assigned (if enabled)
userid | int | The id of the user owning  this invoice
date | \Carbon\Carbon | The date of the invoice YYYY-MM-DD
duedate | \Carbon\Carbon | The due date of the invoice YYYY-MM-DD
datepaid | \Carbon\Carbon | The date the invoice was paid YYYY-MM-DD HH:ii:ss
subtotal | float | The subtotal on the invoice
credit | float | The amount of credit assigned to the invoice
tax | float | The amount of first level tax charged on the invoice
tax2 | float | The amount of second level tax charged on the invoice
total | float | The total of the invoice
balance | float | The amount left to pay on the invoice
taxrate | float | The rate of the first level tax
taxrate2 | float | The rate of the second level tax
status | string | The status of the invoice
paymentmethod | string | The payment method on the invoice in system format
notes | string | The notes associated with the invoice
ccgateway | bool | Is the payment method associated with the invoice a CC Gateway
items | array | The items on the invoice
transactions | array | The transactions on the invoice

### Error Responses
Error | Result
----- | ------
Invalid email or password | { "result": "error", "messages": "User not exists"}
Invoice id of another account | {"result":"error","messages":"Permission denied!"}


## Get invoice product

```curl
$ch = curl_init();
curl_setopt($ch, CURLOPT_URL, 'http://api.dichvuchothuechodat.top/api/v1/getinvoiceproduct');
curl_setopt($ch, CURLOPT_POST, 1);
curl_setopt($ch, CURLOPT_POSTFIELDS,
    http_build_query(
        array(
        	'email'		 	=> 'lanpt@kdata.vn',
        	'password'   	=> '$2y$10$vWkQJ45jOC47ujpxxu6eWesZNodJnbqD.K.vlsUNYb9pl3',
        	'serviceid'    	=> '171'
        )
    )
);
$response = curl_exec($ch);
curl_close($ch);
```

>The above command returns JSON structured like this:

```json
{
  "result": "true",
  "data": [
    {
      "id": 171,
      "userid": "3",
      "invoicenum": "",
      "date": "2017-01-06",
      "duedate": "2017-01-06",
      "datepaid": "2017-01-09 15:39:30",
      "subtotal": "450000.00",
      "credit": "450000.00",
      "tax": "0.00",
      "tax2": "0.00",
      "total": "0.00",
      "taxrate": "0.00",
      "taxrate2": "0.00",
      "status": "Paid",
      "paymentmethod": "banktransfer",
      "notes": ""
    }
  ]
}
```
### Http Request

`POST http://api.dichvuchothuechodat.top/api/v1/getinvoiceproduct`

### Request Parameters

Parameter | Type | Description | Required
--------- | ---- | ----------- | --------
email | string | Your email | Yes
password | string | Provided by Kdata | Yes
serviceid | int | Service id to generate invoices for | Yes
status | string | Find invoices for a specific status <ul><li>Unpaid - unpaid</li> <li>Paid - paid</li><li>Cancelled - cancelled</li></ul> | No

### Error Responses
Error | Result
----- | ------
Invalid email or password | { "result": "error", "messages": "User not exists"}
Product not exists or Permission denied! | {"result":"error","messages":"Product not exists or Permission denied!"}
