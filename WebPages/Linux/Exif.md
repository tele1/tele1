



# How fast check exif in terminal ?


```
$ strings  picture.jpeg | grep exif
 <rdf:Description xmlns:exif='http://ns.adobe.com/exif/1.0/'>
  <exif:XResolution>72</exif:XResolution>
  <exif:YResolution>72</exif:YResolution>
  <exif:ResolutionUnit>Cal</exif:ResolutionUnit>
  <exif:Software>Google</exif:Software>
  <exif:YCbCrSubSampling>YCbCr4:2:0</exif:YCbCrSubSampling>
  <exif:ExifVersion>Exif w wersji 2.2</exif:ExifVersion>
  <exif:FlashPixVersion>FlashPix w wersji 1.0</exif:FlashPixVersion>
  <exif:ColorSpace>B
 65535)</exif:ColorSpace>
  <exif:PixelXDimension>1024</exif:PixelXDimension>
  <exif:PixelYDimension>768</exif:PixelYDimension>
```

Or better way

```
grep': strings * | grep -i exif
```


#Remove all exif from files inside this folder.

```
exiftool -all= *
```
