# Powerimage
Powerimage is a dynamic image handler for laravel.

The workflow is really easy:
- Create a image (image will be optimize)
- Now you have easy on-demand image manipulation like /uploads/images/foobar.jpg?w=200 (filecache will be used)
- Delete image if you don't need more

It contains two packages:
- [approached/laravel-image-optimizer](https://github.com/approached/laravel-image-optimizer)
- [thephpleague/glide](https://github.com/thephpleague/glide)

## Installation

Install packages for image optimizing:
```bash
$ sudo apt-get install optipng jpegoptim
```

Add packages:
```bash
$ composer require alcodo/powerimage
```

After updating composer, add the ServiceProvider to the providers array in config/app.php
```php
'providers' => [
        ...
        Alcodo\PowerImage\ServiceProvider::class,
    ],
```

## Usage

1. Add image via fileupload in controller:
```php
    use DispatchesJobs;

    public function store(Request $request)
    {
        $imageupload = $request->file('imageupload');
        $image = new CreateImage($imageupload, null, 'gallery/');
        $filepath = $this->dispatch($image);
    }
```
Make sure that you use **DispatchesJobs**!

2.Now you have follow filepath ''/uploads/images/gallery/example.jpg'' for the image.
You can have now easy on-demand image manipulation via http [quick-reference](http://glide.thephpleague.com/1.0/api/quick-reference/).

Example:  ''/uploads/images/gallery/example.jpg?w=500&blur=5''

3. Delete image
```php
    use DispatchesJobs;

    public function destroy(Request $request)
    {
        $job = new DeleteImage($request->get($filepath));
        $this->dispatch($job);
    }
```
All cached files will be deleted too.

## License

The MIT License (MIT). Please see [LICENSE](https://github.com/alcodo/powerimage/blob/master/LICENSE) for more information.
