<a name="locator-class"></a>
## Locator Class

The Locator class allows you to search for UPS Access Point locations.

<a name="locator-class-example"></a>
### Example

```php

    $locatorRequest = new \Ups\Entity\LocatorRequest;
    
    $originAddress = new \Ups\Entity\OriginAddress;
    $address = new \Ups\Entity\AddressKeyFormat;
    $address->setCountryCode('NL');
    $originAddress->setAddressKeyFormat($address);
    
    $geocode = new \Ups\Entity\GeoCode;
    $geocode->setLatitude(52.0000);
    $geocode->setLongitude(4.0000);
    $originAddress->setGeoCode($geocode);
    $locatorRequest->setOriginAddress($originAddress);
    
    $translate = new \Ups\Entity\Translate;
    $translate->setLanguageCode('ENG');
    $locatorRequest->setTranslate($translate);
    
    $acccessPointSearch = new \Ups\Entity\AccessPointSearch;
    $acccessPointSearch->setAccessPointStatus(\Ups\Entity\AccessPointSearch::STATUS_ACTIVE_AVAILABLE);
    
    $locationSearch = new \Ups\Entity\LocationSearchCriteria;
    $locationSearch->setAccessPointSearch($acccessPointSearch);
    $locationSearch->setMaximumListSize(25);
    
    $locatorRequest->setLocationSearchCriteria($locationSearch);
    
    $unitOfMeasurement = new \Ups\Entity\UnitOfMeasurement;
    $unitOfMeasurement->setCode(\Ups\Entity\UnitOfMeasurement::UOM_KM);
    $unitOfMeasurement->setDescription('Kilometers');
    $locatorRequest->setUnitOfMeasurement($unitOfMeasurement);
    
    try {
        // Get the locations
        $locator = $this->getContainer()->get('ups.locator');
        $locations = $locator->getLocations($locatorRequest, \Ups\Locator::OPTION_UPS_ACCESS_POINT_LOCATIONS);
    
        foreach($locations->SearchResults->DropLocation as $location) {
            // Your code here
            var_dump($location);
        }

    } catch (Exception $e) {
        var_dump($e);
    }
```

<a name="locator-class-parameters"></a>
### Parameters

Locator class parameters are:

 * `locatorRequest` Mandatory. locatorRequest object with request details, see example
 * `requestOption` Optional. Type of locations you are searching for.