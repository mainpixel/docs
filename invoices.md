
# Invoices 
- [Invoice states](#invoice-states)
- [Invoice text variables](#invoice-text-variables)
- [List all invoices](#list-all-invoices)
- [Show invoice](#show-invoice)
- [Create concept invoice](#create-invoice)
- [Send invoice by email](#change-invoice-state) 
- [Change invoice state](#change-state) 
- [Download invoice is PDF](#download-invoice) 


You can manage all invoices by our API. Because it has many data entries is split by multiple functions. Please read documentation below. 

<a name="invoice-states"></a>
## Invoice states

Each invoice has his own state. Like `Concept invoice` or `Open invoice`. You can change a invoice but not backwards. Because after sending an invoice, the open invoice becomes a administration invoiceID.

<table class="table table-bordered">
	<thead>
		<tr>
			<td>State</td>
			<td>System Hex Color</td>
			<td>Description</td>
			<td>Deletable</td>
		</tr>
	</thead>
	<tbody>
		<tr><td>1</td><td style="color:#808c9f;">#808c9f</td><td>Concept</td><td>yes</td></tr>
		<tr><td>2</td><td style="color:#eac85d;">#eac85d</td><td>Scheduled into sending queue (send date in the future)</td><td>no</td></tr>
		<tr><td>3</td><td style="color:#eac85d;">#eac85d</td><td>Open - Invoice has been send.</td><td>no</td></tr> 
		<tr><td>4</td><td style="color:#ed6c44;">#ed6c44</td><td>First Reminder</td><td>no</td></tr>
		<tr><td>5</td><td style="color:#ed6c44;">#ed6c44</td><td>Second Reminder</td><td>no</td></tr>
		<tr><td>6</td><td style="color:#ed6c44;">#ed6c44</td><td>Third Reminder</td><td>no</td></tr>
		<tr><td>7</td><td style="color:#4daf7c;">#4daf7c</td><td>Payed</td><td>no</td></tr>
		<tr><td>8</td><td style="color:#4daf7c;">#4daf7c</td><td>Credited invoice</td><td>no</td></tr>
		<tr><td>9</td><td style="color:#000000;">#000000</td><td>Not collectable invoice</td><td>no</td></tr>
	</tbody>
</table>

<a name="invoice-text-variables"></a>
## Invoice text variables

You can use text variables for a intro, footer or email text. `eg. {invoiceID}` the system replaces this tag with active Invoice number. 

<table class="table table-bordered">
	<thead>
		<tr>
			<td>Short Code</td>
			<td>Description</td>
		</tr>
	</thead>
	<tbody>
		<tr><td>{invoice.id}</td><td>Concept</td></tr>
		<tr><td>{total.price}</td><td>Sending Queue</td></tr>
		<tr><td>{pay.date}</td><td>Pay before</td></tr>
		<tr><td>{contact.name}</td><td>Person or Company name</td></tr>
	</tbody>
</table>

<a name="list-all-invoices"></a>
## List all Invoices


**Laravel API Example**     
`use Mainpixel\Api\Types\Finance\Invoices;`    

```php
public function index(Send $send) {
    $list = $send->list();
    return view('pages.invoices',['list'=>$list]);
}
```

**cURL Example**
```curl
curl -X GET -H "token: {YOUR-API-KEY}" http://account.mainpixel.io/api/v1/hosting/containers
```

**Result JSON**

```json
{
    0 : {
	    "protected" : {
	    "status" : "1/2/3/4/5/6/7/8/9",
	    "invoiceID" : "F{Y}{M}001",
        "identifier" : "UNIQUE-CONTAINER-ID",
		...
    },
    
    1 : {
		"protected" : {
	    "status" : "1/2/3/4/5/6/7/8/9",
	    "invoiceID" : "F{Y}{M}001",
        "identifier" : "UNIQUE-CONTAINER-ID",
		...   
    }
   
}
```

<a name="show-invoice"></a>
## Show Invoice

**Laravel API Example**     
`use Mainpixel\Api\Types\Finance\Invoices`    

```php
public function show($invoiceID,Invoices $invoices) {
    $show = $invoices->show([
        'identifier' => '{YOUR-INVOICE-ID}'
    ]);
}
```

**cURL Example**
```curl
curl -X GET -H "token: {YOUR-API-KEY}" http://account.mainpixel.io/api/v1/finance/invoices/{YOUR-INVOICE-ID}
```

**Result JSON**

```json
{
    "protected" : {
	    "status" : "1/2/3/4/5/6/7/8/9",
	    "invoiceID" : "F{Y}{M}001",
        "identifier" : "UNIQUE-CONTAINER-ID",
        "dates" : {
	        "created_at" : "UNIX-TIMESTAMP",
	        "updated_at" : "UNIX-TIMESTAMP",
	        "inv_send" : "UNIX-TIMESTAMP",
	        "inv_reminder1" : "UNIX-TIMESTAMP",
	        "inv_reminder2" : "UNIX-TIMESTAMP",
	        "inv_reminder3" : "UNIX-TIMESTAMP"
        },
        "from" : {
	        "comapny" : "",
	        "..." : "..."
        },
        "next_invoiceID" : "Next unique invoice ID (only status 1)"
    },
    "products" : {
    	...    
    },
    "log" : {
	    [
		    "time" : "UNIX-TIMESTAMP",
		    "message" : "Added invoice by user: xxxx"
	    ]
    },
    "to" : {
	    "company" : "",
	    "street" : "",
	    ...
    },
    "data" : {
	    "auto_reminder" : "yes/no",
	    "characteristic" : "Invoice for eg. webservices.",
	    "intro" : "Intro text",
	    "footer" : "Footer text"
    }
}
```



<a name="send-invoice"></a>
## Send a invoice

<table class="table table-bordered">
	<thead>
		<tr>
			<td>Name</td>
			<td>Type</td>
			<td>Description</td>
			<td>Required</td>
		</tr>
	</thead>
	<tbody>
		<tr><td>identifier</td><td>string</td><td>Invoice unique ID</td><td>yes</td></tr>
		<tr><td>method</td><td>string</td><td>Choose to send per 'email' or download as 'pdf'</td><td>yes</td></tr>
		<tr><td>send_date</td><td>timestamp</td><td>Define only if you want to sends in the future</td><td>no</td></tr>
		<tr><td>message</td><td>string</td><td>Define when you want a custom e-mail message instead the default profile message. May be HTML.</td><td>no</td></tr>
	</tbody>
</table>

**Laravel API Example**     
`use Mainpixel\Api\Types\Finance\Send`    

```php
public function SendMailToMyCustomer($invoiceID,Send $send) {
    $job = $send->add([
        'identifier' => $invoiceID,
        'method' => '{EMAIL/PDF}',
        'date' => '01-01-2017',
        'message' => 'Hello, here a new invoice for you...'
    ]);
    
    // On 'method'; PDF
    return response()->make(base64_decode($job['pdf']), 200, [
        'Content-Type' => 'application/pdf',
        'Content-Disposition' => 'attachment; filename="Test.pdf"'
    ]);
}
```

**cURL Example**
```curl
curl -X POST -H "token: {YOUR-API-KEY}" http://account.mainpixel.io/api/v1/finance/send/{YOUR-INVOICE-ID}
```

**Result JSON (on method: email)**

```json
{
   "status" : "success/error", 
   "message" : "Success/Error message." 
}
```

**Result JSON (on method: pdf)**

```json
{
    "pdf" : "base64 encoded hash."
}
```

<a name="change-state"></a>
## Change invoice state

<table class="table table-bordered">
	<thead>
		<tr>
			<td>Name</td>
			<td>Type</td>
			<td>Description</td>
			<td>Required</td>
		</tr>
	</thead>
	<tbody>
		<tr><td>identifier</td><td>string</td><td>Invoice unique ID</td><td>yes</td></tr>
		<tr><td>state</td><td>integer</td><td>See <a href="#invoice-states">state scheme</a> for more information about states.</td><td>yes</td></tr>
		<tr><td>date</td><td>timestamp</td><td>Add pay date</td><td>yes (state 7 & 8)</td></tr>
	</tbody>
</table>

**Laravel API Example**     
`use Mainpixel\Api\Types\Finance\Send`    

```php
public function ChangeState($invoiceID,Send $send) {
    $show = $invoices->add([
        'identifier' => '{YOUR-INVOICE-ID}',
        'state' => 1/2/3/4/5/6/7/8
    ]);
}
```

**cURL Example**
```curl
curl -X POST -H "token: {YOUR-API-KEY}" http://account.mainpixel.io/api/v1/finance/send/{YOUR-INVOICE-ID}
```

**Result JSON**

```json
{
   "status" : "success/error", 
   "message" : "Success/Error message." 
}
```

<a name="download-invoice"></a>
## Download invoice as pdf

This function returns a base64 string. You can decode and return it as you want. Like a download or save the file elsewhere.

**Laravel API Example**     
`use Mainpixel\Api\Types\Finance\Send`    

```php
public function DownloadInvoice($invoiceID,Send $send) {
    $show = $invoices->show([
        'identifier' => '{YOUR-INVOICE-ID}',
    ]);
}
```

**cURL Example**
```curl
curl -X GET -H "token: {YOUR-API-KEY}" http://account.mainpixel.io/api/v1/finance/send/{YOUR-INVOICE-ID}
```

**Result JSON**

```json
{
    "pdf" : "base64 encoded hash."
}
```

