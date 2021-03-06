# Audio File Thumbnail Generator for Spatie's Laravel Media Library

This audio image generator generates thumbnails for audio files uploaded through Spatie's Media Library, just as it already does for image, video, and PDF formats.
Thumbnails of a mono waveform of the whole audio file are generated using ffmpeg's `waveform` converter. It uses the same [PHP FFMpeg package](https://packagist.org/packages/php-ffmpeg/php-ffmpeg) that is used for the video formats already supported by Media Library, so there are no additional dependencies.

## Installation & configuration
Install Spatie's Media Library (version 9.1.0 or later) in your project. This will generate a config file in `config/media-library.php`. Add the audio waveform generator to the list of generators in the `image_generators` section, including optionally setting default `width`, `height`, `foreground` and `background` properties (default values shown):

```php
'image_generators' => [
    ...,
    Synchro\MediaLibrary\Conversions\ImageGenerators\AudioWaveform::class => [
        'width' => 2048,
        'height' => 2048,
        'foreground' => '#113554',
        'background' => '#CBE2F4',
    ]
],
```

These parameters are optional - you can leave them out if you're happy with the defaults.

## Thumbnail colours
The waveform is drawn in the foreground colour, over the background colour. Both should be specified using standard HTML 6-digit hex values passed through the media library config, as above.

## Thumbnail sizing
The base size of the thumbnails can be set via the media library config, as shown above. The default is 2048 x 2048 pixels, neutral values chosen because audio files have no inherent size or aspect ratio. This is quite large, but since the images are very simple, they will compress very well in PNG format.
This size doesn't directly affect the thumbnails delivered to clients because media library itself generates scaled-down versions to match client requests, however, it does have a direct effect on the aspect ratio of the thumbnails, so if you want a 16:9 ratio, change the height to `1152`, or `1536` for 4:3. 

## Supported formats

* `aiff`
* `flac`
* `m4a`
* `mp3`
* `mp4`
* `ogg`
* `wav`
* `wma`

## Running tests
Tests are written in pest, so to run the test suite, install dev dependencies (`composer install --dev`) and then run `./vendor/bin/pest`. There are also configurations for phpcs, psalm, and phpstan to check code style and type coverage, or run all of them using `composer test`.