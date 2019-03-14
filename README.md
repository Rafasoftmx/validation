# validation
PHP simple validation Library.

- Object and Array validation
- $\_FILES validation
- Image validation
- Chaining methods validation: $valid->name("age")->required()->range(100,200);
- Domain and URL exist validation
- Bad Words validation
- Filtering methods
- XSS Clean Data
- Noise Words filtering
- Type-casting/converts strings to int, float or bool(textual booleans)

## properties

- **data**: attach by reference an array to be validate
- **errors**: array of errors generated by the different methods
- **patterns**: patterns used for validate one input in with the function "pattern"
- **uploadFileError**: definition of upload files error in PHP
- **basicTags**: basic tags allowed to filter an input in function "basicTags"
- **es_noiseWords**: A noise word is a word such as the or if that is so common that it is not useful in searches. all this words are removed for cleen an input.
- **badwords_jsfunc**: this list of words/expressions are for determine if input is safe and not contain javascript.
- **badwords_html_tags**: this list of words/expressions are for determine if input is safe and not contain html.
- **badwords_css**: this list of words/expressions are for determine if input is safe and not contain CSS.
- **badwords_sql**: his list of words/expressions are for determine if input is safe and not contain SQL.
- **boolCastingList**: this array is for convert/determine if a string is boolean
```
  [
    "true"=>true,
    "yes"=>true,
    "ok"=>true,
    "si"=>true,
    "sí"=>true,
    "1"=>true,
    "false"=>false,
    "not"=>false,
    "no"=>false,
    "0"=>false
  ];
```

## Methods
- **__toString()**:toString Magic Method, get the errors as string one line per error
- **xssCleanAllData()**: Try to avoid an Cross-site scripting (XSS) atack, clean and sanitize all data array attached by reference, eliminates html/php tags, converts special chars in html entities and normalice spaces to ascii space (32)
- **data(&$data,$xssClean = false)**: attach by reference an array, object or value to the class for validation, be aware that if you modify the data will modify the original values. some functions filter, alter the original values too.
- **name($name)**: sets the name of the field we are validating, and if name match with some element in data array or $\_FILES, this value is going to be validate or filtered
- **value(&$value)**: sets the value by reference to be validate or filtered
- **file($file)**: sets the File element to be validate or filtered. the value is one elemet of array $\_FILES
- **reset()**: reset errors, is useful after some validations like:  $valid->name("productId")->required()->isSuccess() and you need re evaluate
- **errorMessage($message="",$function="")**: function were all errors are set, also you can add a new error
- **isSuccess()**: Determines after validate all fields if has no errors
- **getErrors()**: eturn all errors array or false if no errors
- **displayErrors()**: return all errors in html list
- **printErrors()**: echo list of errors


### validations

- **required()**: heck if some required parameter is present otherwise the field is not valid
- **pattern($name)**: determines if a input string is valid if pass regex, the regex used is an element of array $patterns  
- **customPattern($pattern)**:determines if a input string is valid if pass regex, the regex to evaluate are sended as parameter in "$pattern" between '/^(' and ')$/u'
- **min($minVal)**: Determine if the provided numeric value is higher or equal to a specific value
- **max($maxVal)**: Determine if the provided numeric value is lower or equal to a specific value
- **range($min,$max)**: Determine if the provided numeric value is between  a specific range
- **minLen($length)**: Determine if the provided string length is more or equal to a specific value
- **maxLen($length)**: Determine if the provided string length is lower or equal to a specific value
- **rangeLen($min,$max)**: Determine if the provided string length is between  a specific range
- **exactLen($length)**: Determine if the provided string length is equal to a specific value
- **maxWords($num,$delimiter= " ")**: Determine if the provided string has space separated words and the counted words are lower or equal to a specific value
- **minWords($num,$delimiter= " ")**: Determine if the provided string has space separated words and the counted words are more or equal to a specific value
- **exactWords($num,$delimiter= " ")**: Determine if the provided string has delimiter separated words and the counted words are exact to specific number
- **rangeWords($min,$max,$delimiter= " ")**: Determine if the provided string has space separated words and the counted words are is between a specific range
- **equal($value)**: Determine if the provided value is equal than the specified value (text or number)
- **beginsWith($list)**: Determine if the provided string begins with one of specified element of list. the list is comma separated string
- **contains($list)**: Determine if the provided string contains one of specified element of list. the list is comma separated string
- **notContains($list)**: Determine if the provided string NOT contains one of specified element of list. the list is comma separated string
- **maxSize($size)**: Determines if the uploaded file is less or equal than the specified max file size in bytes
- **minSize($size)**: Determines if the uploaded file is more or equal than the specified min file size in bytes
- **rangeSize($min, $max)**: Determines if the uploaded file is between than the specified range file size in bytes
- **validMime($list)**: Determines the file mime type(finfo_open and finfo_file) and checks if is allowed in the list. the list must contain the mime type strings complete or partial. the list is comma separated string,
- **validImage($extList= "",$minDimensions= "",$maxDimensions= "",$minSize=null,$maxSize=null)**:Determines the file is image, checks extension vs mime type, max-min dimensions one or both, max-min file size one or both
- **ext($list)**: Determines if the extension in the name of file is allowed in the provided list
- **urlExists($AcceptedHttpCodes ="")**: Determines if an URL exist getting the content and verifying if has no error, http code examples test in https://httpstat.us/
- **domainExists()**: Determines if an Domain exist
- **validIp()**: Determine if the provided text value is a valid IP address
- **validIpv4()**: Determine if the provided value is a valid IPv4 address
- **validIpv6()**: Determine if the provided value is a valid IPv6 address
- **validName()**: Determine if the input is a valid human name
- **validDate($format = null)**: Determine if the provided input is a valid date (ISO 8601), format date ('Y-m-d') or datetime ('Y-m-d H:i:s')
- **badwords($filter = "")**: determines if string contains not allowed words. the list of badwords ara taken from arrays: $badwords_jsfunc, $badwords_html_tags, $badwords_css and $badwords_sql
- **textPatterns($maxpercentPatterns = 60)**: Tries to determine if the provided value not contain patterns like: repetitive chars, repetitive patterns, Ascending numbers, descendant numbers, qwerty patterns

### Filters

- **xssClean()**: try to avoid an Cross-site scripting (XSS) atack filtering single value. clean and sanitize the value, eliminates html/php tags, converts special chars in html entities and normalice spaces to ascii space (32)
- **trim()**: Strip whitespace (or other characters) from the beginning and end of a string value
- **upper()**: Make a string value uppercase
- **lower()**: Make a string value lowercase
- **cleanPunctuation()**: Filter string value cleaning/deleting most common Punctuation signs
- **urlEncode()**: Filter/Sanitize the string by urlencoding characters
- **htmlEncode()**: Filter/Sanitize the string by converting HTML characters to their HTML entities
- **cleanMail()**: Filter/Sanitize the string by removing illegal characters from emails
- **cleanNumber()**: Filter/Sanitize the string by removing illegal characters from numbers
- **cleanFloat()**: Filter/Sanitize the string by removing illegal characters from float numbers
- **basicTags()**: Filter/Strip HTML and PHP tags except the defined basic tags in array "$basicTags"
- **convertTo($type)**: cast/converts the string value to int, float or bool. in the case of bool casting uses the array $boolCastingList to determine the value
- **Format a number with grouped thousands**: numberFormat($decimals = 0,$dec_point = ".",$thousands_sep = ",")
- **replaceMsWord()**: Convert MS Word special characters to web safe characters. [“, ”, ‘, ’, –, …] => [", ", ', ', -, ...]
- **urlWebSlug()**: converts a string text in a url slug, for example, the title of some article can be escaped for add it in to URL. eg. text: "Title tag optimization guide" becomes: title-tag-optimization-guide and you can use like: www.some.com/title-tag-optimization-guide/
- **cleanNoiseWords($text,$sortByAppearances = true)**: Return filtered string value cleaning/deleting all words found in the array $es_noiseWords

### Quick Extra Methods

- **is_int($value)**: Check if the $value is a int number
- **is_float($value)**: Check if the $value is a float number
- **is_alpha($value)**: Check if the $value only contanis alphabetic chars. shorcut to 'patternCheck("alpha",$value)'
- **is_words($value)**: Check if the $value only contanis alphabetic chars including spaces. shorcut to 'patternCheck("words",$value)'
- **is_alphanum($value)**: Check if the $value only contanis alphabetic chars including numbers. shorcut to 'patternCheck("alphanum",$value)'
- **is_url($value)**: Check if the $value well formatted URL (Uniform Resource Locator)
- **is_bool($value)**: Check if the $value is bool, including tel values in array "$boolCastingList"
- **is_email($value)**: Check if the $value well formatted email address







## examples

### Basic Usage
In this example we going to validate one field setting a name and pass the value.
the name is show in the error and the values pass by reference to evaluate.
```
// post data example
$_POST = ["age"=>"18"];

$valid = new validation();//our validator

$valid->name("age value post")->value($_POST["age"])->pattern("int"); // simple validation

var_dump($valid->isSuccess()); // check if is valid

$_POST = ["age"=>"a"];
$valid->name("my age ")->value($_POST["age"])->pattern("int"); // simple validation

var_dump($valid->isSuccess()); //in this case return false
var_dump($valid->getErrors()); // return false array of errors


bool(true)
bool(false)
array(1) {
  [0]=>
  string(40) "Field format my age  not valid.(pattern)"
}
```

### Setting the name of field

the method "name" is used for set the name of the field shown in error messages, but it is the "key" of array of data ir $\_FILES also sets the actual value to validate or firter.
e.g.

##### using the name as key

```
// post data example
$_POST = [
	"age"=>"18",
	"name" => 'Rafael Antonio',
];

$valid = new validation();//our validator
$valid->data($_POST); // assigning by reference all array data to evaluate

$valid->name("age")->pattern("int");
$valid->name("name")->pattern("words");

print "<pre>";
var_dump($valid->isSuccess());
print "</pre>";
echo $valid->displayErrors();

```

##### using the name as text to show in messages, needs to set the value manually

```
// post data example
$_POST = [
	"age"=>"18",
	"name" => 'Rafael Antonio',
];

$valid = new validation();//our validator

$valid->name("age of user")->value($_POST["age"])->pattern("int");
$valid->name("name of user")->value($_POST["name"])->pattern("int");// make error

print "<pre>";
var_dump($valid->isSuccess());
print "</pre>";
echo $valid->displayErrors();
```

### validation assigning all array data
in these case we pass all data array by reference to validate, and use the method "name($name)" to determine the key of array to evaluate


```
// post data example
$_POST = [
	"age"=>"18",
	"name" => 'Rafael Antoño',
	"bool" => 'yes',
	"int" => '56',
	"float" => '95.3',
	"mail" => 'max_carnage@gmail.co'
];

$valid = new validation();//our validator

$valid->data($_POST); // assigning all array data to evaluate

$valid->name("age")->pattern("int"); // simple validation only pass the name as 'key' to evaluate

print "<pre>";
var_dump($valid->isSuccess()); // check if is valid return "bool(true)"
print "</pre>";
```

### validation assigning all data in a object

in these case we pass all object properties by reference to validate, and use the method "name($name)" to determine the properties of object to evaluate

```
//example of object data
class usr
{
	public  $id = 0;
	public	$age = '18';
	public  $mail = 'max_carnage@gmail.co';
	public  $name = 'Rafael Antoño';
	public  $rol = 'admin';
	public  $enabled = false;

}//EOC

$usr = new usr(); // instance of object

$valid = new validation();//our validator

$valid->data($usr); // assigning all data to evaluate

$valid->name("age")->pattern("int"); // simple validation only pass the name as property to evaluate

print "<pre>";
var_dump($valid->isSuccess()); // check if is valid
print "</pre>";
```

### validating $\_FILES array

the same like in previous examples but in this case we use method "file($file)" to set the value
```
// FILES data example
$_FILES = [
    "file1" => [
            "name" => 'MyFile.txt', //(comes from the browser, so treat as tainted)
            "type" => 'text/plain', // (not sure where it gets this from - assume the browser, so treat as tainted)
            "tmp_name" => '/tmp/php/php1h4j1o', //(could be anywhere on your system, depending on your config settings, but the user has no control, so this isn't tainted)
            "error" => 'UPLOAD_ERR_OK', // (= 0)
            "size" => '123'   //(the size in bytes)
        ]
];


$valid = new validation();//our validator

$valid->data($usr); // assigning all data to evaluate

$valid->name("my file")->value($_FILES["file1"])->required(); // simple validation if exist or not
$valid->name("file1")->required(); // in this sentence we only pass the "key" and the class find the value in the $_FILES array

print "<pre>";
var_dump($valid->isSuccess()); // check if is valid
print "</pre>";
```
### get list of errors

you can access to the array directly:
```
print "<pre>";
var_dump($valid->errors);
print "</pre>";
```

or with the functions:

```
print "<pre>";
var_dump($valid->getErrors()); //get the array if the validation has errors or false if not
print "</pre>";

echo $valid->displayErrors();// get HTML list

$valid->printErrors();// print error list separated by "<br/>"
```
### chaining methods for validate
you can validate some input for various methods and filtering in the same line:

```
$valid->name("age")->cleanNumber()->pattern("int")->max(8)->min(3)->required();
```

### clean data

you can clean all data at one using method "xssCleanAllData()", it try to avoid an Cross-site scripting (XSS) atack, eliminates html/php tags, converts special chars in html entities and normalice spaces to ascii space (32),

```
$valid->data($_POST);
$valid->xssCleanAllData();
```
or

```
$valid->data($_POST,true);
```

if you onli want to clean single value you can use:

```
$valid->name("personAddress")->xssClean();
```

### cheack success validations and get errors

```
$valid = new validation();//our validator

$_POST = [
	"name"=>"Rafael Antonio",
	"last"=>"Torres Romero"
];


$valid->data($_POST);

$valid->name("name")->minLen(5);
$valid->name("name")->maxLen(90);
$valid->name("name")->exactLen(14);
$valid->name("last")->rangeLen(5,9); //get error


print "<pre>";
var_dump($valid->isSuccess());// if no error TRUE otherwise FALSE
print "</pre>";

echo $valid->displayErrors();// get html list

print "<pre>";
var_dump($valid->getErrors()); // get array of errors
print "</pre>";

print "<pre>";
$valid->printErrors(); // echo every error in array
print "</pre>";
```

## set of validations

### required
check the value is if not null or empty string
```
$valid = new validation();//our validator

$_POST = [
	"usr"=>"my-us3r_n4m3"
];


$valid->data($_POST);

$valid->name("usr")->required(); // any lowercase letter (a-z), number (0-9), an underscore, or a hyphen from 3 to 16 chars
$valid->name("noData")->required();

print "<pre>";
var_dump($valid->isSuccess());
print "</pre>";
echo $valid->displayErrors();

```
### patterns

```
$valid = new validation();//our validator

$_POST = [
"query"=>"/?id=1&data=some-data_x", //uri
"urldir"=>"ftp://aeneas.mit.edu/some.html#one?id=1&data=some", //url
"text"=>"someText", //alpha
"text2"=>"Some Text",//words
"text3"=>"3000Text",//alphanum
"num"=>"15",//int
"num2"=>"15.16",//float
"telephone"=>"(55)57-35-89-36",//tel
"text4"=>"some text -.,;:!%&()?+'°#/@",//text    leters,space and -.,;:!"%&()?+'°#/@
"filename"=>"Californication.mp3",//file
"foldername"=>"Peppers",//folder
"personAddress"=>"Charles W. Anderson (Dear Mr. Ambassador) Department of State 2050 Washington, DC 20521-2050",//address     leters,space and .,()°-
"date1"=>"01-05-2019",//date_dmy
"date2"=>"2019-01-05",//date_ymd
];


$valid->data($_POST);

$valid->name("query")->pattern("querystring");
$valid->name("urldir")->pattern("url");
$valid->name("text")->pattern("alpha");
$valid->name("text2")->pattern("words");
$valid->name("text3")->pattern("alphanum");
$valid->name("num")->pattern("int");
$valid->name("num2")->pattern("float");
$valid->name("num2")->pattern("float");
$valid->name("telephone")->pattern("tel");
$valid->name("text4")->pattern("text");
$valid->name("filename")->pattern("file");
$valid->name("foldername")->pattern("folder");
$valid->name("personAddress")->pattern("address");
$valid->name("date1")->pattern("date_dmy");
$valid->name("date2")->pattern("date_ymd");

print "<pre>";
var_dump($valid->isSuccess());
print "</pre>";
echo $valid->displayErrors();
```
### customPattern
```
$valid = new validation();//our validator

$_POST = [
	"myData"=>"my-us3r_n4m3"// Username
];


$valid->data($_POST);

$valid->name("myData")->customPattern("^[a-z0-9_-]{3,16}$"); // any lowercase letter (a-z), number (0-9), an underscore, or a hyphen from 3 to 16 chars


print "<pre>";
var_dump($valid->isSuccess());
print "</pre>";
echo $valid->displayErrors();
```
### Determine if the provided numeric value is min, max or equal to a specific value


 ```
 $valid = new validation();//our validator

 $_POST = [
 	"age"=>"18",
 	"age2"=>"6"
 ];


 $valid->data($_POST);

 $valid->name("age")->required()->min(10)->max(15); //shows an error
 $valid->name("age2")->required()->min(1);// >= 1
 $valid->name("age2")->required()->max(10); // <= 10
 $valid->name("age2")->required()->equal(6); // == 6
 $valid->name("age2")->required()->range(100,200); // >= 1 , <= 10


 print "<pre>";
 var_dump($valid->isSuccess());
 print "</pre>";
 echo $valid->displayErrors();
```

### Determine if the provided string length is min, max or equal to a specific value
```
$valid = new validation();//our validator

$_POST = [
	"name"=>"Rafael Antonio",
	"last"=>"Torres Romero"
];


$valid->data($_POST);

$valid->name("name")->minLen(5);
$valid->name("name")->maxLen(90);
$valid->name("name")->exactLen(14);
$valid->name("last")->rangeLen(5,9); // show error




print "<pre>";
var_dump($valid->isSuccess());
print "</pre>";
echo $valid->displayErrors();
```



### Determine if a string has character separated words and the counted words are min, max or equal to a specific value
```
$valid = new validation();//our validator

$_POST = [
	"text1"=>"Lorem ipsum dolor sit amet, consectetur adipiscing elit.",
	"text2"=>"Nunc-et-quam-nec-risus-tempor-sodales-porta-at-mauris."
];


$valid->data($_POST);

$valid->name("text1")->minWords(5);
$valid->name("text1")->maxWords(90);
$valid->name("text2")->exactWords(10,"-");//define "-" a delimiter
$valid->name("text2")->rangeWords(5,9,"-"); // show error




print "<pre>";
var_dump($valid->isSuccess());
print "</pre>";
echo $valid->displayErrors();
```


### Determine if a string or number are equal than the provided value
```

$valid = new validation();//our validator

$_POST = [
	"age"=>"36",
	"name"=>"Rafael"
];


$valid->data($_POST);

$valid->name("age")->equal(36);
$valid->name("name")->equal("rafael");// shows error because case sensitive


print "<pre>";
var_dump($valid->isSuccess());
print "</pre>";
echo $valid->displayErrors();
```


### Determine if a string starts with some element in predefined comma separated list
```
$valid = new validation();//our validator


$_POST = [
	"text"=>"Lorem ipsum dolor sit amet, consectetur adipiscing elit.",
	"text2"=>"ipsum dolor sit amet, consectetur adipiscing elit.",
	"text3"=>"dolor sit amet, consectetur adipiscing elit.",
	"text4"=>"sit amet, consectetur adipiscing elit.",
	"name"=>"Rafael Antonio Torres Romero"
];


$valid->data($_POST);

$valid->name("text")->beginsWith("Lorem,ipsum,dolor");
$valid->name("text2")->beginsWith("Lorem,ipsum,dolor");
$valid->name("text3")->beginsWith("Lorem,ipsum,dolor");
$valid->name("text4")->beginsWith("Lorem,ipsum,dolor");// shows error
$valid->name("name")->beginsWith("rafael");// shows error because case sensitive


print "<pre>";
var_dump($valid->isSuccess());
print "</pre>";
echo $valid->displayErrors();
```


### Determine if a string contains or not some element in predefined comma separated list
```
$valid = new validation();//our validator


$_POST = [
	"text"=>"Lorem ipsum dolor sit amet, consectetur adipiscing elit.",
	"name"=>"Rafael Antonio Torres Romero"
];


$valid->data($_POST);

$valid->name("text")->contains("Lorem,ipsum,dolor");
$valid->name("name")->contains("Lorem,ipsum,dolor");// shows error
$valid->name("name")->contains("torres");// shows error because case sensitive
$valid->name("name")->notContains("Lorem,ipsum,dolor");// the opposite, NOT contains


print "<pre>";
var_dump($valid->isSuccess());
print "</pre>";
echo $valid->displayErrors();
```


### Determine if a Upload file size is min, max or in range size


```
// in these case the values to validate is an element of the array $_FILES that is HTTP File Upload variable in php
// and not is required use the function $valid->data(); to pass the values. it search automatically

$valid = new validation();//our validator

// FILES data example
$_FILES = [
    "file1" => [
            "name" => 'bg.jpg', //(comes from the browser, so treat as tainted)
            "type" => 'text/plain', // (not sure where it gets this from - assume the browser, so treat as tainted)
            "tmp_name" => 'bg.jpg', //(could be anywhere on your system, depending on your config settings, but the user has no control, so this isn't tainted)
            "error" => 'UPLOAD_ERR_OK', // (= 0)
            "size" => '446000'   //(the size in bytes)
        ]
];


$valid->name("file1")->minSize(100000);// the size in bytes
$valid->name("file1")->maxSize("600000");
$valid->name("file1")->rangeSize(100000,600000);
$valid->name("file1")->maxSize("321000");// shows error

print "<pre>";
var_dump($valid->isSuccess());
print "</pre>";
echo $valid->displayErrors();
```


### Upload file mime types and images file validation
```
$valid = new validation();//our validator

// FILES data example
$_FILES = [
    "file1" => [
            "name" => 'bg.jpg', //(comes from the browser, so treat as tainted)
            "type" => 'text/plain', // (not sure where it gets this from - assume the browser, so treat as tainted)
            "tmp_name" => 'bg.jpg', //(could be anywhere on your system, depending on your config settings, but the user has no control, so this isn't tainted)
            "error" => 'UPLOAD_ERR_OK', // (= 0)
            "size" => '446000'   //(the size in bytes)
        ]
];


$valid->name("file1")->validMime("text/plain,text/html,image/jpeg,image/png,audio/ogg,video/mp4"); //you can use a complete mime type string in the list
$valid->name("file1")->validMime("text/p,text/h,image/,audio/,video/");// you can use a partial mime type string in the list
//valid extension in file and image file (open the image and gets the extension in base to mime type)
$valid->name("file1")->validImage("jpg,gif,png");
//check dimensions of image (width x height)
//min, max
$valid->name("file1")->validImage("jpg,gif,png","500x300","2000x1500");
//just min dimensions
$valid->name("file1")->validImage("","500x300");
//just max dimensions
$valid->name("file1")->validImage("","","2000x1500");
//file size min, max
$valid->name("file1")->validImage("jpg,gif,png","500x300","2000x1500",100000,600000);//full options
//just min size
$valid->name("file1")->validImage("","","",100000);
//just max size
$valid->name("file1")->validImage("","","","",600000);


print "<pre>";
var_dump($valid->isSuccess());
print "</pre>";
echo $valid->displayErrors();
```


### simple validation file extension

```
$valid = new validation();//our validator

// FILES data example
$_FILES = [
    "file1" => [
            "name" => 'bg.jpg', //(comes from the browser, so treat as tainted)
            "type" => 'text/plain', // (not sure where it gets this from - assume the browser, so treat as tainted)
            "tmp_name" => 'bg.jpg', //(could be anywhere on your system, depending on your config settings, but the user has no control, so this isn't tainted)
            "error" => 'UPLOAD_ERR_OK', // (= 0)
            "size" => '446000'   //(the size in bytes)
        ]
];


$valid->name("file1")->ext("jpg,gif,png");// simple validation extension



print "<pre>";
var_dump($valid->isSuccess());
print "</pre>";
echo $valid->displayErrors();
```


### check if url exist
```
// http code examples test in https://httpstat.us/

$valid = new validation();//our validator

$_POST = [
	"page"=>"https://www.rafasoft.me/",
	"page2"=>"https://httpstat.us/201",
	"page3"=>"https://httpstat.us/205",
	"page4"=>"https://httpstat.us/302",
	"page5"=>"https://httpstat.us/403",
	"video"=>"https://www.youtube.com/watch?v=drQ9y6WkgdQ",
	"imagen"=>"http://dlanham.com/art/falsealarm/preview.jpg"
];


$valid->data($_POST);


$valid->name("page")->urlExists();// by default only the code 200 is take as valid
$valid->name("page2")->urlExists("201,205,302,403");// but you can add extra http status codes to take as valid
$valid->name("page3")->urlExists("201,205,302,403");
$valid->name("page4")->urlExists("201,205,302,403");
$valid->name("page5")->urlExists("201,205,302,403");
$valid->name("video")->urlExists("301");
$valid->name("imagen")->urlExists();



print "<pre>";
var_dump($valid->isSuccess());
print "</pre>";
echo $valid->displayErrors();
```



### check if domain exist
```
// https://www.expireddomains.net/backorder-expired-domains/ for testing

$valid = new validation();//our validator

$_POST = [
	"page"=>"https://www.rafasoft.me/",
	"page2"=>"www.youtube.com/",
	"page3"=>"google.com",
	"page4"=>"LiveDrive.mx",
	"page5"=>"Azerbaijan.mx"
];


$valid->data($_POST);


$valid->name("page")->domainExists();
$valid->name("page2")->domainExists();
$valid->name("page3")->domainExists();
$valid->name("page4")->domainExists();// not exist
$valid->name("page5")->domainExists();// not exist




print "<pre>";
var_dump($valid->isSuccess());
print "</pre>";
echo $valid->displayErrors();
```


### validating ip, date
```
$valid = new validation();//our validator



$_POST = [
	"ip"=>"127.0.0.1",
	"ipv4"=>"19.117.63.126",
	"ipv6"=>"2001:0db8:85a3:08d3:1319:8a2e:0370:7334",
	"date1"=>"2019-03-07", //('Y-m-d') or datetime ('Y-m-d H:i:s')
	"date2"=>"2000-01-20 16:15:00",
	"date3"=>"20/01/2000 10:18:36", // custom format d/m/Y H:i:s, http://php.net/manual/en/datetime.createfromformat.php
];


$valid->data($_POST);


$valid->name("ip")->validIp();
$valid->name("ipv4")->validIpv4();
$valid->name("ipv6")->validIpv6();



$valid->name("date1")->validDate();
$valid->name("date2")->validDate();
$valid->name("date3")->validDate("d/m/Y H:i:s");// custom format


print "<pre>";
var_dump($valid->isSuccess());
print "</pre>";
echo $valid->displayErrors();
```


### validating human name, bad words, text patterns
```
$valid = new validation();//our validator



$_POST = [
	"name"=>"Rafael ántoño's-II",

	"text"=>"Lorem ipsum dolor sit amet, consectetur adipiscing elit.",

	"text_js"=>"document.getElementById(id); setTimeout(later, wait); alert();",
	"text_css"=>"-webkit-text-size-adjust: none; box-sizing: border-box;",
	"text_html"=>"some imput <h1     >some text</h1       > <div></div>",
	"text_sql"=>"select              *              from        table  ",

	"text_patterns1"=>"AAAAAAAAAAAAsAAAAAAAAAdAAAAAAAAAfAAAAA",
	"text_patterns2"=>"asdasdasdasdasdasdasdasd",
	"text_patterns3"=>"asdfghjklasdfghjkl",
	"text_patterns4"=>"1234567890 1234567890 1234567890 1234567890",
	"text_patterns5"=>"abcdefghijklm",
	"text_patterns6"=>"0987654321 0987654321 0987654321 0987654321",
	"text_patterns7"=>"............0000000000000007777777777777",
	"text_patterns8"=>"rafarafarafarafarafarafarafarafarafarafa"
];


$valid->data($_POST);


$valid->name("name")->validName();



$valid->name("text")->badwords("js,html,css,sql");// or "", or "all" as parameter is the same effect, validates all defined bad words (not aloowed)

$valid->name("text_js")->badwords("js,html");// just validates js and html bad words
$valid->name("text_css")->badwords("css,js");
$valid->name("text_html")->badwords("html");
$valid->name("text_sql")->badwords("sql");


$valid->name("text_patterns1")->textPatterns();//check for patterns, for example in passwords or to avoid include garbage information
$valid->name("text_patterns2")->textPatterns();
$valid->name("text_patterns3")->textPatterns();
$valid->name("text_patterns4")->textPatterns();
$valid->name("text_patterns5")->textPatterns();
$valid->name("text_patterns6")->textPatterns();
$valid->name("text_patterns7")->textPatterns(30);// it can be more strict, setting the max percentage of the string that can have one patterns, by default is 60%
$valid->name("text_patterns8")->textPatterns();


print "<pre>";
var_dump($valid->isSuccess());
print "</pre>";
echo $valid->displayErrors();
```


## filters
```
$valid = new validation();//our validator



$_POST = [
	"name"=>"          <h3>Rafael antonio</h3>        ",
	"text"=>"   Lorem ipsum ¡dolor! sit amet, ¿consectetur? adipiscing elit....    ",
	"url"=>"Lorem ipsum/dolor sit amet/consectetur.html?adipiscing=elit....&data=3659-",
	"html"=>"<h3>title</h3>",
	"mail"=>"rafasoft ° @gm.com",	// note the space and °
	"number"=>"num123",
	"float"=>"123.156 num",
	"html2"=>"<h3>title</h3><camvas></camvas><script></script>",
	"boolText"=>"yes",
	"intText"=>"1568",
	"floatNum"=>"1568.3698",
	"big_num"=>"15683698.69856",
	"ms Word text"=>"some “text” ‘example’… ",
	"url slug"=>"Lorem ipsum ¡dolor! sit amet, ¿consectetur? adipiscing elit....",
];


$valid->data($_POST);

echo ("<h3>Before filter:</h3>");
print '<textarea cols="150" rows="20">';
 print_r($_POST);
print '</textarea>';

$valid->name("name")->xssClean();
$valid->name("name")->lower();
$valid->name("text")->upper();
$valid->name("text")->trim();
$valid->name("text")->cleanPunctuation();
$valid->name("url")->urlEncode();//encode special char for url
$valid->name("html")->htmlEncode();//encode special char for html
$valid->name("mail")->cleanMail();//delete not allowed chars for mail
$valid->name("number")->cleanNumber();
$valid->name("float")->cleanFloat();
$valid->name("html2")->basicTags();
$valid->name("boolText")->convertTo("bool");//becomes a php bool
$valid->name("intText")->convertTo("int");//becomes a php int
$valid->name("floatNum")->convertTo("float"); //becomes a php float
$valid->name("big_num")->numberFormat(2,"-","/"); // numberFormat(); defaults: decimals = 0 , dec_point = "." , $thousands_sep = ","
$valid->name("ms Word text")->replaceMsWord();// replace some ms word chars into standard ones: “” ‘’…  to "" '' ...
$valid->name("url slug")->urlWebSlug();//converts string in a URL slug, delete extra chars and replace space into -

echo ("<h3>after filter:</h3>");
print '<textarea cols="150" rows="20">';
 print_r($_POST);
print '</textarea>';
```


### clean Noise Words
```
$valid = new validation();//our validator

$_POST = [
	"text"=>"Cada año en la ciudad de Ginebra, Suiza, se lleva a cabo una de las mayores exposiciones de automóviles en todo el mundo, donde los mayores fabricantes, y otros más nuevos, presentan sus nuevos vehículos y conceptos visionarios. Este año el Salón del Automóvil de Ginebra ha estado protagonizado por los automóviles eléctricos.",

];

$usefulWords = $valid->cleanNoiseWords($_POST["text"],false);// No sort
$usefulWords2 = $valid->cleanNoiseWords($_POST["text"]);// sorted by word count

print "<pre>";
var_dump($_POST["text"]);
var_dump($usefulWords);
var_dump($usefulWords2);

print "</pre>";
```


## extra methods to cheack sigle values


```
print "<pre>";
// bools
echo "\nbools:\n\n";
var_dump(validation::is_bool("true"));
var_dump(validation::is_bool("1"));
var_dump(validation::is_bool("yes"));
var_dump(validation::is_bool("ok"));
var_dump(validation::is_bool("sí"));
var_dump(validation::is_bool("no"));
var_dump(validation::is_bool(1));
var_dump(validation::is_bool(""));//false, it is not bool just empty string

echo "\nnumbers:\n\n";
var_dump(validation::is_int(5.8));//false, is float
var_dump(validation::is_int(5));
var_dump(validation::is_float(5));//true
var_dump(validation::is_float(5.0));//true

echo "\nchars:\n\n";
var_dump(validation::is_alpha("asdadasd"));//only chars, not spaces not number not punctuation
var_dump(validation::is_words("Cada año en la ciudad de Ginebra Suiza")); //only chars and spaces, not number not punctuation
var_dump(validation::is_alphanum("555345asdadasd"));//only chars and numbers,  not space not punctuation
var_dump(validation::is_url("https://www.google.com/webhp?hl=es-419&ictx=2&sa=X&ved=0ahUKEwiCmbSCrfHgAhUQT6wKHf6XBz8QPQgH"));
var_dump(validation::is_email("rafasoft@gm.com"));


print "</pre>";
```
