Volume Types
===========

Plugins can supply custom asset volume types by supplying a class that implements `craft\base\VolumeInterface` and `craft\base\VolumeTrait`.

As a convenience, you can extend `craft\base\Volume`, which provides a base volume type implementation, optimized for [Flysystem](https://flysystem.thephpleague.com/) adapters.

You can refer to Craft’s own volume classes for examples. They are located in `vendor/craftcms/cms/src/volumes/`.

## Registering Custom Volume Types

Once you have created your volume class, you will need to register it with the Volumes service, so Craft will know about it when populating the list of available volume types: 

```php
<?php
namespace ns\prefix;

use craft\events\RegisterComponentTypesEvent;
use craft\services\Volumes;

class Plugin extends \craft\base\Plugin
{
    public function init()
    {
        Event::on(Volumes::class, Volumes::EVENT_REGISTER_VOLUME_TYPES, function(RegisterComponentTypesEvent $event) {
            $event->types[] = MyVolume::class;
        });

        // ...
    }

    // ...
}
```