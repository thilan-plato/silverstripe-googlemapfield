# Silverstripe Google Map Field

A Silverstripe form field that allows users to select locations using Google Maps API. Compatible with both Silverstripe 4 and 5.

## Features

- Interactive Google Maps integration
- Search functionality using Google Geocoding API
- Saves latitude/longitude coordinates to DataObject fields
- Configurable map options and field names
- Compatible with both Silverstripe 4 and 5

## Requirements

- PHP 7.4 or higher
- Silverstripe Framework 4.0 or higher (including Silverstripe 5)
- Google Maps API key

## Installation

1. Install via Composer:
```bash
composer require betterbrief/silverstripe-googlemapfield
```

2. Add your Google Maps API key to your configuration:

```yaml
# app/_config/googlemapfield.yml
BetterBrief\GoogleMapField:
  default_options:
    api_key: 'your-google-maps-api-key-here'
```

## Usage

### Basic Usage

```php
use BetterBrief\GoogleMapField;

class MyDataObject extends DataObject
{
    private static $db = [
        'Latitude' => 'Decimal(10,8)',
        'Longitude' => 'Decimal(11,8)',
        'Zoom' => 'Int',
        'Bounds' => 'Text'
    ];

    public function getCMSFields()
    {
        $fields = parent::getCMSFields();
        
        $fields->addFieldToTab('Root.Main', 
            GoogleMapField::create(
                $this,
                'Location',
                [
                    'api_key' => 'your-api-key',
                    'show_search_box' => true
                ]
            )
        );
        
        return $fields;
    }
}
```

### Configuration Options

The field accepts various configuration options:

```php
GoogleMapField::create($this, 'Location', [
    'api_key' => 'your-google-maps-api-key',
    'show_search_box' => true,
    'field_names' => [
        'Latitude' => 'Latitude',
        'Longitude' => 'Longitude', 
        'Zoom' => 'Zoom',
        'Bounds' => 'Bounds'
    ],
    'map' => [
        'zoom' => 14
    ],
    'default_field_values' => [
        'Latitude' => 30,
        'Longitude' => 0
    ]
]);
```

### Custom Field Names

You can customize the database field names:

```php
GoogleMapField::create($this, 'Location', [
    'field_names' => [
        'Latitude' => 'MyLatitudeField',
        'Longitude' => 'MyLongitudeField',
        'Zoom' => 'MyZoomField',
        'Bounds' => 'MyBoundsField'
    ]
]);
```

## Silverstripe 4 vs 5 Compatibility

This module is designed to work with both Silverstripe 4 and 5:

- **PHP Requirements**: PHP 7.4+ (required for Silverstripe 5)
- **Framework Support**: Silverstripe Framework 4.0+ and 5.0+
- **CMS Integration**: Supports both SS4 and SS5 CMS interfaces
- **JavaScript**: Compatible with both versions' event systems

## Configuration

### Global Configuration

You can set default options globally in your configuration:

```yaml
# app/_config/googlemapfield.yml
BetterBrief\GoogleMapField:
  default_options:
    api_key: 'your-google-maps-api-key'
    show_search_box: true
    field_names:
      Latitude: 'Latitude'
      Longitude: 'Longitude'
      Zoom: 'Zoom'
      Bounds: 'Bounds'
    map:
      zoom: 14
    default_field_values:
      Latitude: 30
      Longitude: 0
```

### Extending the Field

You can extend the field to add custom functionality:

```php
class MyGoogleMapField extends GoogleMapField
{
    public function updateGoogleMapsParams(&$params)
    {
        // Add custom parameters to Google Maps API call
        $params['libraries'] = 'places';
    }
}
```

## License

BSD License

## Contributing

Contributions are welcome! Please ensure your code is compatible with both Silverstripe 4 and 5.

## Changelog

### 3.0.0
- Added Silverstripe 5 compatibility
- Updated PHP requirement to 7.4+
- Enhanced JavaScript for modern CMS integration
- Improved form change detection for both SS4 and SS5