
# Webcontainers 
- [List all webcontainers](#list-all-webcontainers)
- [Show a webcontainers](#show-webcontainer)
- [Store a webcontainers](#store-webcontainer)
- [Update a webcontainers](#update-webcontainer)
- [Destroy a webcontainers](#destroy-webcontainer)

During the building process of Mainpixel we took a whole new concept together. We wanted to issolate each website/platform from eachother. So we builded a container management platform where each website/platform is hosted in a seperate webcontainer. Those webcontainers can be automatically moved arround all connected nodes for the best performance and scalability solution.

<a name="list-all-webcontainers"></a>
## List all webcontainers


**Laravel API Example**     
`use Mainpixel\Api\Types\Hosting\Containers;`    

```php
public function index(Containers $containers) {
    $list = $containers->list();
}
```

**cURL Example**
```curl
curl -X GET -H "token: {YOUR-API-KEY}" http://account.mainpixel.io/api/v1/hosting/containers
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

<a name="show-webcontainer"></a>
## Show Webcontainer

**Laravel API Example**     
`use Mainpixel\Api\Types\Hosting\Containers;`    

```php
public function show($containerID,Containers $containers) {
    $show = $containers->show([
        'identifier' => '{YOUR-CONTAINER-ID}'
    ]);
}
```

**cURL Example**
```curl
curl -X GET -H "token: {YOUR-API-KEY}" http://account.mainpixel.io/api/v1/hosting/containers/{YOUR-CONTAINER-ID}
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

<a name="store-webcontainer"></a>
## Store Webcontainer

**Laravel API Example**     
`use Mainpixel\Api\Types\Hosting\Containers;`    

```php
public function store($containerID,Containers $containers) {
    $show = $containers->add([
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
	http://account.mainpixel.io/api/v1/hosting/containers/?identifier=577ff4ef83ceea105f184bb5
```

**Result JSON**

```json
{
    "status" : "error/success",
    "message" : "RETURNED-MESSAGE",
}
```

<a name="update-webcontainer"></a>
## Update Webcontainer

**Laravel API Example**     
`use Mainpixel\Api\Types\Hosting\Containers;`    

```php
public function update($containerID,Containers $containers) {
    $show = $containers->update([
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
	http://account.mainpixel.io/api/v1/hosting/containers/{CONTAINER-ID}
```

**Result JSON**

```json
{
    "status" : "error/success",
    "message" : "RETURNED-MESSAGE",
}
```

<a name="destroy-webcontainer"></a>
## Destroy Webcontainer

**Laravel API Example**     
`use Mainpixel\Api\Types\Hosting\Containers;`    

```php
public function destroy($containerID,Containers $containers) {
    $show = $containers->remove([
        'identifier' => 'CONTAINER-IDENTIFIER',
    ]);
}
```

**cURL Example**
```curl
curl -X DELETE -H "token: 5730440bc41f31a4528b4575" 
	http://account.mainpixel.io/api/v1/hosting/containers/577ff4ef83ceea105f184bb5
```

**Result JSON**

```json
{
    "status" : "error/success",
    "message" : "RETURNED-MESSAGE",
}
```
