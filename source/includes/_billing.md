# Billing
## ApplyCredit

Applies the Client's Credit to an invoice

```curl
$ch = curl_init();
curl_setopt($ch, CURLOPT_URL, 'http://api.dichvuchothuechodat.top/api/v1/applycredit');
curl_setopt($ch, CURLOPT_POST, 1);
curl_setopt($ch, CURLOPT_POSTFIELDS,
    http_build_query(
        array(
            'email'         => 'lanpt@kdata.vn',
            'password'      => '$2y$10$vWkQJ45jOC47ujpxxu6eWesZNodJnbqD.K.vlsUNYb9pl3',
            'invoiceid'     => '171'
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
  "amount": 450000,
  "invoicepaid": "true"
}
```

### Http Request

`POST http://api.dichvuchothuechodat.top/api/v1/applycredit`

### Request Parameters

Parameter | Type | Description | Required
--------- | ---- | ----------- | --------
email | string | Your email | Yes
password | string | Provided by Kdata | Yes
invoiceid | int | The ID of the invoice to apply credit | Yes

### Response Parameters
Parameter | Type | Description
--------- | ---- | -----------
result | string | The result of the operation: success or error
invoiceid | int | The id of the invoice the credit has been applied to
amount | float | The amount of credit applied
invoicepaid | string |  true/false string

### Error Responses
Possible error condition response include:

Error | Result
----- | ------
Invalid email or password | { "result": "error", "messages": "User not exists"}
Credit amount exceeds customer credit balance | {"result": "error","message": "Amount exceeds customer credit balance"}
Invoice Not in Unpaid Status | {"result":"error","message":"Invoice Not in Unpaid Status"}
Invoice id of another accoun | {"result":"error","messages":"Permission denied!"}