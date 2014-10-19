---
title: CakePHP RequestHandler Extended
date: 2009-01-29 11:00:00
categories:
  - CakePHP
  - PHP
tags:
  - components
  - extending cakephp component
---

A CakePHP component which extends built-in `RequestHandler` component by adding some useful geolocation information. It requires MaxMind WebService license key to work properly.

Save it with the name `request_handler_ext.php` into your application components directory under controllers.

You can call the following methods within your controller (e.g. `$this->RequestHandlerExt->methodName()`):

| Method                      | Returns                          |
|-----------------------------|----------------------------------|
| getClientCountryCode()      | ISO 3166 Two-letter Country Code |
| getClientRegionCode()       | Region Code                      |
| getClientCity()             | City                             |
| getClientPostalCode()       | Postal Code                      |
| getClientLatitude()         | Latitude                         |
| getClientLongitude()        | Longitude                        |
| getClientMetropolitanCode() | Metropolitan Code                |
| getClientAreaCode()         | Area Code                        |
| getClientIsp()              | ISP                              |
| getClientOrganization()     | Organization                     |


```php request_handler_ext.php
<?php
/**
 * Extends RequestHandler component by adding some useful geolocation information.
 * 
 * Requires MaxMind WebService license key to work properly
 *
 * @copyright     2009 Erhan Abay
 * @package       app
 * @subpackage    app.controllers.components
 * @version       $Revision$
 * @lastmodified  $Date$
 */

App::import('Component', 'RequestHandler');

class RequestHandlerExtComponent extends RequestHandlerComponent
{
	/**
	 * Required to query MaxMind WebService
	 *
	 * Provide your own key by replacing XXXXX.
	 */
	const MM_LICENSE_KEY = 'XXXXXX';
	
	public function startup(&$controller)
	{
		parent::startup(&$controller);
		$this->controller =& $controller;
	}
	
	/**
	 * Searches key value in array returned by function getGeoLocation()
	 *
	 * @param string $name Name of the method
	 * @param unknown_type $arguments Not used, required not to give error
	 * @return string if key found
	 *         null else
	 */
	public function __call($name, $raw = false)
	{
		$var = Inflector::underscore(preg_replace('/getClient/i', '', $name));
		$geo_location = (array)$this->getGeoLocation($raw);
		
		return array_key_exists($var, $geo_location) ? $geo_location[$var] : null;
	}
  
	/**
	 * Queries to the MaxMind WebService and returns an array of information
	 *
	 * @param bool $raw
	 * @return null if IP address is local
	 *         bool false if webservice returns error code
	 *         string if $raw is set true
	 *         array else
	 */
  public function getGeoLocation($raw = false)
  {
  	if ($this->isLocalIP()) {
  		return null;
  	}
  	
  	if ($this->controller->Session->check('User.GeoLocation')) {
  		return $raw ? $this->controller->Session->read('User.GeoLocation.raw') : $this->controller->Session->read('User.GeoLocation');
  	}
  	
    App::import('HttpSocket');
    
    $http = new HttpSocket();
    
    /*
     * Returns in order:
     * 
     * 0  ISO 3166 Two-letter Country Code,
     * 1  Region Code,
     * 2  City,
     * 3  Postal Code,
     * 4  Latitude,
     * 5  Longitude,
     * 6  Metropolitan Code,
     * 7  Area Code,
     * 8  ISP,
     * 9  Organization,
     * 10 Error code
     */
    $result = $http->get('http://geoip1.maxmind.com/f', array(
      'l' => self::MM_LICENSE_KEY,
      'i' => $this->getClientIP()
    ));
    
    $values = explode(',', $result);
    
    if (isset($values[10])) {
      return false;
    }
    
    if ($raw) {
    	return $result;
    }
    
    $keys = array('country_code', 'region_code', 'city', 'postal_code', 'latitude', 'longitude', 'metropolitan_code', 'area_code', 'isp', 'organization');
    $data = array_combine($keys, $values);
    $data['coords'] = $values[4].','.$values[5];
    $data['raw'] = $result;
    $this->controller->Session->write('User.GeoLocation', $data);
    
    return $data;
  }
  
  /**
   * Detects whether IP address is local or not 
   *
   * @param string $ip IP address to check
   * @return bool
   */
  public function isLocalIP($ip = null) {
  	$ip = is_null($ip) ? $this->getClientIP() : $ip;
  	
  	$regex = '/(192\.168\.[0-9]{1,3}\.[0-9]{1,3})';
  	$regex .= '|(10\.[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3})';
  	$regex .= '|(172\.0?([1][6-9])Â¦([2][0-9])Â¦([3][0-1])\.[0-9]{1,3}\.[0-9]{1,3})';
  	$regex .= '|(127\.0\.0\.1)/';
  	
  	return (bool)preg_match($regex, $ip);
  }
}
```
