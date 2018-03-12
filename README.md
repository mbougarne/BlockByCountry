# BlockByCountry
Block visitors based on their countries IPs Address.

### USAGE
Sample as it is, a small php code that restrict visitors by country, attach it to your web app header file or at top of each page you want to block visitors from some countries:

```php

  # GET the visitor IP
  $clientIP  = $_SERVER['REMOTE_ADDR']; 

  # Send request to IP INFO DB & GET details
  $ipinfoDB   = file_get_contents("http://ipinfo.io/{$clientIP}"); 

  # Decode the JSON data
  $IPdetails = json_decode($ipinfoDB); 

  # Blocked countries code e.g:
  $blockedCountries = array(

      'MA', # Morocco
      'PK', # Pakistan
      'US', # United State 
      'IN', # India 
      'RU' # Russia 
  );

  # Allowed IPs - White list yours or any other IP e.g:
  $allowedIPS       = array(
      '0.0.0.1', # YOUR IP 
      '0.0.0.2' # Your client IP 
  );

  # GET the country code from the IP INFO Database e.g: MA - (Morocco)
  $clientCountry    = $details->country;

  # Check if visitor country is blocked
  if(in_array($clientCountry, $blockedCountries)){

      # If the visitor country is blocked => Check If its IP is in white list
      if(!in_array($clientIP, $allowedIPS)){

          # If country is blocked and IP not allowed => Then redirect
          header("Location: http://php.net/");
          exit();

      }
  }

```
