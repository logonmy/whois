# Whois: Domain and IP address WHOIS Querying Class

Whois is a PHP class that can perform WHOIS queries on domain names and IP addresses.

# Requirements

* PHP 5.2.0 or newer

# Installation

The preferred method of installation is with Packagist and Composer. Run the following command to install the package and add it as a requirement to your project's composer.json:

`composer require michaelmawhinney/whois`

# Usage

**First include the Whois.php class and namespace.**

```php
<?php

include("Whois.php");

use michaelmawhinney\Whois;

// see example usage below 

?>
```

## Whois::search( )

search( ) — Return a string containing the WHOIS information for a domain name or IP address

### Description

``string Whois::``**``search``**`` ( string ``**``$keyword``**`` )``

Takes an input **string** (domain name or IP address) and returns a string containing the full WHOIS query response.

### Parameters

**``keyword``**

The domain name or IP address to search.

### Return Values

Returns the full WHOIS query response or **FALSE** on failure.

### Errors/Exceptions

An **Exception** will be thrown and **FALSE** returned if any of the following occur:

- **keyword** is not a valid domain name, IPv4 address, or IPv6 address.
- **keyword** is a domain name, and there is no matching WHOIS server.
- **keyword** is a domain name, and there is no entry found on the matching WHOIS server.
- **keyword** is an IPv4 or IPv6 address, and there is no entry found on the matching WHOIS server.
- a WHOIS query to a WHOIS server fails.

### Example

```php
<?php

include("Whois.php");
use michaelmawhinney\Whois;

$domain = "google.com";
$ipv4 = "172.217.7.174";
$ipv6 = "2607:f8b0:4004:800::200e";

try {

    $whois_domain = Whois::search($domain);
    $whois_ipv4 = Whois::search($ipv4);
    $whois_ipv6 = Whois::search($ipv6);

} catch (Exception $e) {

    echo 'Caught exception: ' . $e->getMessage() . "\n";

}

// In this example, $whois_domain, $whois_ipv4, and $whois_ipv6
// each contain the WHOIS response in a string.

?>
```

## Whois::root( )

root( ) — Returns the root domain name of a given domain name

### Description

``string Whois::``**``root``**`` ( string ``**``$domain``**`` )``

Takes an input **string** (domain name) and returns a string containing the root domain of the provided domain.

### Parameters

**``domain``**

The domain name to parse. *Note that a valid domain name is assumed; no validation is performed on the provided parameter.*

### Return Values

Returns the root domain.

### Example

```php
<?php

include("Whois.php");
use michaelmawhinney\Whois;

$root_domain = Whois::root("mail.google.com");       // google.com
$root_domain = Whois::root("www.google.co.uk");      // google.co.uk
$root_domain = Whois::root("www.example.govt.nz");   // example.govt.nz
$root_domain = Whois::root("subdomain.example.xyz"); // example.xyz

?>
```
