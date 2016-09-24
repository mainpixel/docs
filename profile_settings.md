# Profile Settings 
- [Introduction](#introduction) 
- [Get profile settings](#get-profile-settings) 

Because each profile has a huge set of settings. So we build a special API class for it! Just only to display the settings of the active profile it can't be changed from here.
You can give a specific app with the request like; 'invoice' it returns automatically the general and invoice settings.

<a name="get-profile-settings"></a>
## Get profile settings


**Laravel API Example**     
`use Mainpixel\Api\Types\Settings;`    

```php
public function index(Settings $settings) {
    $settings = $settings->show([
	    'identifier' => 'finance/crm/service...'
    ]);
    
    ...
}
```

**cURL Example**
```curl
curl -X GET -H "token: {YOUR-API-KEY}" http://account.mainpixel.io/api/v1/settings
```

**Result JSON**

```json
{
    "general" : {
	    "timezone" : "Europe/Amsterdam",
	    "dateformat" : "dd-mm-yy",
	    "datetimeformat" : "dd-mm-yy hh:mm:ss",
    },
    
    "data" : {
	    "color" : "",
	    "auto_mail" : true,
	    "from" : [],
	    ... 
    }
   
}
``` 

