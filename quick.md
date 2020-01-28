# Quickstart


- [Install Filepicker](#install-sample)
- [Server Requirements](#server-sample-requirements)

## Install Filepicker

- Lorem Ipsum is simply dummy text of the printing and typesetting industry. Lorem Ipsum has been the industry's standard dummy text ever since the 1500s, 

- when an unknown printer took a galley of type and scrambled it to make a type specimen book. It has survived not only five centuries, but also the leap into electronic typesetting,

-  remaining essentially unchanged. It was popularised in the 1960s with the release of Letraset sheets containing Lorem Ipsum passages,

> Notice: Make sure the `files` directory has read/write permissions (`0777`). <br>
> If you use [Composer](https://getcomposer.org/), run `composer install`.

### Server Requirements

Filepicker has a few requirements:

- PHP 5.3.3+
- [Fileinfo](https://php.net/manual/ro/book.fileinfo.php)
- [GD](http://php.net/manual/en/book.image.php)
- [Exif](http://php.net/manual/en/book.exif.php) 

### Browser Support

sample docs supports the following browsers (desktop & mobile):

- Chrome
- Firefox
- Opera
- Safari*
- MS Edge
- IE10+*

_* and more recently with desktop .._ 

Starting with version 47, Chrome requires a secure connection (SSL) in order to use the camera. Read more [here](https://www.chromium.org/Home/chromium-security/deprecating-powerful-features-on-insecure-origins).

__CSS__

First include the CSS file inside the `<head>` tag. 

```markup
<link rel="stylesheet" href="assets/css/filepicker.css">
```

__HTML__

Next, add the HTML markup.

```markup
<div id="filepicker">
    <!-- The upload button -->
    <input type="file" name="files[]">
    
    <!-- The files list -->
    <ul class="files"></ul>
</div>
```

__JavaScript__

At the bottom of your page right before closing the `<body>` tag add:

```markup
<script src="https://code.jquery.com/jquery-1.12.3.min.js"></script>

```

```javascript
$('#filepicker').filePicker({
    url: 'uploader/index.php',
})
.on('done.filepicker', function (e, data) {
    var list = $('.files');

    // Iterate through the uploaded files
    $.each(data.files, function (i, file) {
        if (file.error) {
            list.append('<li>' + file.name + ' - ' + file.error + '</li>');
        } else {
            list.append('<li>' + file.name + '</li>');
        }
    });
})
.on('fail.filepicker', function () {
    alert('Oops! Something went wrong.');
});
```

> Note: If you already have jQuery in your page, you don't have to include it again.

__PHP__

In your PHP file add:

```php
<?php


// Include composer autoload
require __DIR__.'/../vendor/autoload.php';

$uploader = new Uploader($config = new Config, new ImageManager);
$handler = new Handler($uploader);

// Configuration
$config['debug'] = true;
$config['upload_dir'] = __DIR__.'/../files';
// $config['upload_url'] = 'files';
```

For more examples check the source code in these files: 

- Basic UI: `index.php` 
- Basic Plus UI: `plus.php`
- Basic: `basic.php`
- Avatar: `avatar.php`
- Zero UI: `zero.php`
- `uploader/index.php`