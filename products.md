# Products
- [List all products](#list-all-product)
- [Show a product](#show-product)
- [Store a product](#store-product)
- [Update a product](#update-product)
- [Destroy a product](#destroy-product)

During the building process of Mainpixel we took a whole new concept together. We wanted to issolate each website/platform from eachother. So we builded a container management platform where each website/platform is hosted in a seperate Product. Those Products can be automatically moved arround all connected nodes for the best performance and scalability solution.

<a name="list-all-Products"></a>
## List all Products


**Laravel API Example**     
`use Mainpixel\Api\Types\Sales\Products;`    

```php
public function index(Products $products) {
    $list = $products->list();
}
```

**cURL Example**
```curl
curl -X GET -H "token: {YOUR-API-KEY}" http://account.mainpixel.io/api/v1/sales\products
```

**Result JSON**

```json
{
    "0" : {
        "protected" : {
            "identifier" : "UNIQUE-CONTAINER-ID",
            "created_at" : "UNIX-TIMESTAMP",
            "updated_at" : "UNIX-TIMESTAMP",
            "dns_general_state" : "DOMAINS-DNS-STATE (true/false)"
        },
        "data" : {
            "general" : {
              "name" : "CONTAINER-NAME",
              "type" : "TYPE (like: wordpress, magento, laravel etc..)",
              "note" : "NOTE",
              "php" : "PHP-VERSION (default 7)"
            }
        },
        "domains" : {
            "0" : {
                "DOMAIN-ID" : "DOMAIN-INCL-TLD"
            },                                                    
        },
        "amount" : {
            "domains" : "NUMBER-OF-DOMAINS",
            "email" : "NUMBER-OF-EMAIL-ACCOUNTS/FORWARDERS/CATCHALLS",
            "databases" : "NUMBER-OF-DATABASES"
        },
    },
    "1" : {
        
    }
}
```

<a name="show-Product"></a>
## Show Product

**Laravel API Example**     
`use Mainpixel\Api\Types\Sales\Products;`    

```php
public function show($containerID,Products $products) {
    $show = $products->show([
        'identifier' => '{YOUR-CONTAINER-ID}'
    ]);
}
```

**cURL Example**
```curl
curl -X GET -H "token: {YOUR-API-KEY}" http://account.mainpixel.io/api/v1/sales\products/{YOUR-CONTAINER-ID}
```

**Result JSON**

```json
{
    "protected" : {
        "identifier" : "UNIQUE-CONTAINER-ID",
        "created_at" : "UNIX-TIMESTAMP",
        "updated_at" : "UNIX-TIMESTAMP",
    },
    "data" : {
        "general" : {
          "name" : "CONTAINER-NAME",
          "type" : "TYPE (like: wordpress, magento, laravel etc..)",
          "note" : "NOTE",
          "php" : "PHP-VERSION (default 7)"
        }
    },
}
```

<a name="store-Product"></a>
## Store Product

**Laravel API Example**     
`use Mainpixel\Api\Types\Sales\Products;`    

```php
public function store($containerID,Products $products) {
    $show = $products->add([
        'identifier' => 'CONTAINER-IDENTIFIER',
        'data' => [
            'general' => [
                'name' => 'CONTAINER-NAME',
                'type' => 'TYPE (like: wordpress, magento, laravel etc..)',
                'note' => 'NOTE',
                'php' => 'PHP-VERSION'
            ],
        ]
    ]);
}
```

**cURL Example**
```curl
curl -X POST -H "token: {YOUR-API-KEY}" 
	-H "Content-Type: multipart/form-data; boundary=----WebKitFormBoundary7MA4YWxkTrZu0gW" 
	-F "identifier=577ff4ef83ceea105f184bb5" 
	-F "data[general][name]=Test" 
	-F "data[general][type]=MAGENTO" 
	-F "data[general][note]=test" 
	-F "data[general][php]=7" 
	http://account.mainpixel.io/api/v1/sales\products/?identifier=577ff4ef83ceea105f184bb5
```

**Result JSON**

```json
{
    "status" : "error/success",
    "message" : "RETURNED-MESSAGE",
}
```

<a name="update-Product"></a>
## Update Product

**Laravel API Example**     
`use Mainpixel\Api\Types\Sales\Products;`    

```php
public function update($containerID,Products $products) {
    $show = $products->update([
        'identifier' => 'CONTAINER-IDENTIFIER',
        'data' => [
            'general' => [
                'name' => 'CONTAINER-NAME',
                'type' => 'TYPE (like: wordpress, magento, laravel etc..)',
                'note' => 'NOTE',
                'php' => 'PHP-VERSION'
            ],
        ]
    ]);
}
```

**cURL Example**
```curl
curl -X PUT -H "token: {YOUR-API-TOKEN}" 
	-H "Content-Type: application/x-www-form-urlencoded" 
	-d 'identifier=577ff4ef83ceea105f184bb5&data[general][name]=TESTCONTAINER&data[general][type]=MAGENTO&data[general][note]=NOTE&data[general][php]=7' 
	http://account.mainpixel.io/api/v1/sales\products/{CONTAINER-ID}
```

**Result JSON**

```json
{
    "status" : "error/success",
    "message" : "RETURNED-MESSAGE",
}
```

<a name="destroy-Product"></a>
## Destroy Product

**Laravel API Example**     
`use Mainpixel\Api\Types\Sales\Products;`    

```php
public function destroy($containerID,Products $products) {
    $show = $products->remove([
        'identifier' => 'CONTAINER-IDENTIFIER',
    ]);
}
```

**cURL Example**
```curl
curl -X DELETE -H "token: 5730440bc41f31a4528b4575" 
	http://account.mainpixel.io/api/v1/sales\products/577ff4ef83ceea105f184bb5
```

**Result JSON**

```json
{
    "status" : "error/success",
    "message" : "RETURNED-MESSAGE",
}
```
