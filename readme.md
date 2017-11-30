# compressor-head

This is a python based web application hosted on Google App Engine. By using
this app one can compress/resize an image before downloading it. This saves the
user data that otherwise needs to be downloaded. Being run on Google App Engine
the conversion is fast. Also I have used the memcache library which speeds up
the process if same image is being retrived by multiple users.

## Usage

_URL_ -
`http://compressor-head.appspot.com/image/?image_url=[IMAGE_URL]&width=[WIDTH]&height=[HEIGHT]&format=[FORMAT]`

where

    *IMAGE_URL* is the URL of the image which is to be compressed.
    *WIDTH* is the desired width.
    *HEIGHT* is the desired height.
    *FORMAT* is the desired image format (Supported formats - JPEG, PNG and WEBP).

Both WIDTH and HEIGHT should be positive integers. Both WIDTH and HEIGHT cannot
be zero. If one of the two is zero it will scale that non-zero dimention and the
other dimention will be scaled such that the aspect ratio remains the same. If
both are not zero, both dimentions will scale accordingly which might change the
aspect ratio of the image.

#### Usage example

Sample Image URL - http://compressor-head.appspot.com/image\
This is a `5.8 MB JPEG` image. Dimention `5649×3684`\
![](http://compressor-head.appspot.com/image)

To resize the image -

* Resize (Width) :
  `http://compressor-head.appspot.com/image/?image_url=http://compressor-head.appspot.com/image&width=500&height=0&format=jpeg`\
  ![](http://compressor-head.appspot.com/image/?image_url=http://compressor-head.appspot.com/image&width=500&height=0&format=jpeg)\
  This will return an image `37 KB JPEG` image with dimentions `500x326`

* Resize (Height) :
  `http://compressor-head.appspot.com/image/?image_url=http://compressor-head.appspot.com/image&width=0&height=250&format=png`\
  ![](http://compressor-head.appspot.com/image/?image_url=http://compressor-head.appspot.com/image&width=0&height=250&format=png)\
  This will return an image `164 KB PNG` image with dimentions `383x250`

* Resize (Width & Height) :
  `http://compressor-head.appspot.com/image/?image_url=http://compressor-head.appspot.com/image&width=500&height=350&format=jpeg`\
  ![](http://compressor-head.appspot.com/image/?image_url=http://compressor-head.appspot.com/image&width=500&height=350&format=jpeg)\
  This will return an image `41 KB JPEG` image with dimentions `500x350` You can
  also use the `WEBP` format. I haven't used it here because GitHub doesnot
  render WEBPs. A sample WEBP conversion of this conversion can be found
  [here](http://compressor-head.appspot.com/image/?image_url=http://compressor-head.appspot.com/image&width=500&height=350&format=webp).

## Deploying compressor-head on Google Cloud Engine

Pre-requisites: git and python2.7

* Create a cloud engine project on https://console.cloud.google.com
* Download Google Cloud SDK from https://cloud.google.com/sdk/docs/
* Update Google Cloud SDK components by running `gcloud components update`
* run `gcloud init` and select the cloud engine project created at the beginning
  when prompted
* Install python component `gcloud components install app-engine-python`
* Clone compressor-head repo `git clone
  https://github.com/jboss-outreach/compressor-head`
* run `gcloud app deploy app.yaml index.yaml` inside cloned project
* app will be live at http://[YOUR_PROJECT_ID].appspot.com

## Author

[@m-murad](https://github.com/m-murad)

## Refrence

[Google App Engine (Python): Images API](https://cloud.google.com/appengine/docs/standard/python/refdocs/google.appengine.api.images.html)\
[Google App Engine (Python): Memcache API](https://cloud.google.com/appengine/docs/standard/python/refdocs/google.appengine.api.memcache.html)\
[Google App Engine (Python): URL downloading API](https://cloud.google.com/appengine/docs/standard/python/refdocs/google.appengine.api.urlfetch.html)\
[Vinay Sajip: logging](http://www.red-dove.com/python_logging.html)\
[The Webapp2 Maintainers: webapp2](https://cloud.google.com/appengine/docs/standard/python/refdocs/google.appengine.api.images.html)

## License

[Apache Version 2.0](http://compressor-head.appspot.com/license)
