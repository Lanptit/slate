# Order
## Add order
Adds an order to a client.

```curl
$ch = curl_init();
curl_setopt($ch, CURLOPT_URL, 'http://api.dichvuchothuechodat.top/api/v1/addorder');
curl_setopt($ch, CURLOPT_POST, 1);
curl_setopt($ch, CURLOPT_POSTFIELDS,
    http_build_query(
        array(
        	'email'		 	=> 'lanpt@kdata.vn',
        	'password'   	=> '$2y$10$vWkQJ45jOC47ujpxxu6eWesZNodJnbqD.K.vlsUNYb9pl3',
        	'product'    	=> 'VPS 01',
        	'billingcycle' 	=> 'monthly',
        	'os'			=> 'centos 6.x',
        	'extraIp'		=> '3'
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
  "orderid": 170,
  "productids": "171",
  "addonids": "",
  "domainids": "",
  "invoiceid": 171
}
```

### Http Request

`POST http://api.dichvuchothuechodat.top/api/v1/addorder`

### Request Parameters

Parameter | Type | Description | Required
--------- | ---- | ----------- | --------
email | string | Your email | Yes
password | string | Provided by Kdata | Yes
product | string | VPS package name <ul><li>VPS mini</li><li>VPS 01</li><li>VPS 02</li><li>VPS 03</li><li>VPS 04</li><li>VPS 05</li></ul>| Yes
billingcycle | string | Billing cycles of the products | Yes
os | string | | Yes
cpu | string | | No
hdd | string | | No
ram | string | | No
extraIp | integer | Only get the value from 1 to 5 | No
hostname | string | The hostname of server for VPS order | No
rootpw | string | | No
ns1prefix | string | The first nameserver prefix for the VPS. Eg. ns1 in ns1.hostname.com | No
ns2prefix | string | The second nameserver prefix for the VPS. Eg. ns2 in ns2.hostname.com | No

### Response Parameters
Parameter | Type | Description
--------- | ---- | -----------
result | string | The result of the operation: success or error
orderid | int | The Order ID for the created order
productids | string | The Product/Service ID created by the order
addonids | string | The Addon ID created by the order
domainids | string | The domain ID created by the order
invoiceid | int | The invoice ID created for the order

### Error Responses
Error | Result
----- | ------
Invalid email or password | { "result": "error", "messages": "User not exists"}
Given Client product is not found in the database. | {"result":"error","messages":"Product not exists"}
Unable to add order when client status is Closed | {"result":"error","message":"Unable to add order when client status is Closed"}


## Get product
Obtain a list of Client Purchased Products matching the provided criteria


```curl
$ch = curl_init();
curl_setopt($ch, CURLOPT_URL, 'http://api.dichvuchothuechodat.top/api/v1/getproduct');
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
  "result": "success",
  "serviceid": "171",
  "product": {
    "serviceid": "171",
    "regdate": "2017-01-06",
    "nextduedate": "2017-01-06",
    "status": "Pending",
    "domain": "",
    "dedicatedip": "",
    "assignedips": "",
    "billingcycle": "Monthly",
    "username": "",
    "password": "",
    "os": "Centos 6.x 64Bit",
    "cpu": "2 Core",
    "ram": "1GB",
    "hdd": "40G",
    "Extra ip": "3"
  }
}
```

### Http Request

`POST http://api.dichvuchothuechodat.top/api/v1/getproduct`

### Request Parameters

Parameter | Type | Description | Required
--------- | ---- | ----------- | --------
email | string | Your email | Yes
password | string | Provided by Kdata | Yes
serviceid | int | The specific service id to obtain the details for | Yes

### Response Parameters
Parameter | Type | Description
--------- | ---- | -----------
result | string | The result of the operation: success or error
serviceid | int | The specific service id searched for
product | array | The product returned matching the criteria passed

### Error Responses
Error | Result
----- | ------
Invalid email or password | { "result": "error", "messages": "User not exists"}
Service id of another account | {"result":"error","messages":"Permission denied!"}
