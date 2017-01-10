# Support
## Add cancel request
Adds a Cancellation Request

```curl
$ch = curl_init();
curl_setopt($ch, CURLOPT_URL, 'http://api.dichvuchothuechodat.top/api/v1/cancelrequest');
curl_setopt($ch, CURLOPT_POST, 1);
curl_setopt($ch, CURLOPT_POSTFIELDS,
    http_build_query(
        array(
        	'email'		 	=> 'lanpt@kdata.vn',
        	'password'   	=> '$2y$10$vWkQJ45jOC47ujpxxu6eWesZNodJnbqD.K.vlsUNYb9pl3',
        	'serviceid'    	=> '171',
        	'reason'		=> 'Customer Request'
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
  "serviceid": "171",
  "userid": "3"
}
```

### Http Request

`POST http://api.dichvuchothuechodat.top/api/v1/cancelrequest`

### Request Parameters
Parameter | Type | Description | Required
--------- | ---- | ----------- | --------
email | string | Your email | Yes
password | string | Provided by Kdata | Yes
serviceid | int | The Service ID to cancel | Yes
reason | string | The customer reason for cancellation | Yes

### Response Parameters
Parameter | Type | Description
--------- | ---- | -----------
result | string | The result of the operation: success or error
serviceid | int | The id of the service the request was for
userid | int | The id of the user the service belongs to

### Error Responses
Error | Result
----- | ------
Invalid email or password | { "result": "error", "messages": "User not exists"}
Service id of another account | {"result":"error","messages":"Permission denied!"}