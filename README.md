# &#128663; `openalpr` - Automated license plate reader
This repository is a fork of the [primary repository](http://github.com/openalpr/openalpr) with minor modifications to run on Raspian Buster and Ubuntu 18+ with OpenCV. The [Open Horizon](http://github.com/dcmartin/open-horizon) _service_ [`alpr`](http://github.com/dcmartin/open-horizon/tree/master/alpr/README.md)  utilizes this repository to build Docker containers.  Please refer to the [Dockerfile](http://github.com/dcmartin/open-horizon/tree/master/alpr/Dockerfile) for details.

## About
OpenALPR is an open source *Automatic License Plate Recognition* library written in C++ with bindings in C#, Java, Node.js, Go, and Python.  The library analyzes images and video streams to identify license plates.  The output is the text representation of any license plate characters.

Check out a live online demo here: [http://www.openalpr.com/demo-image.html](http://www.openalpr.com/demo-image.html)

## Installation
Outside of use in building the [`alpr`](http://github.com/dcmartin/open-horizon/tree/master/alpr/README.md) _service_, see [The Easy Way](https://github.com/openalpr/openalpr/wiki/Compilation-instructions-(Ubuntu-Linux)#the-easy-way) for installation on Debian LINUX.

&#9995; Remember to specify **`http://github.com/dcmartin/openalpr.git`** as the repository.

## Usage
OpenALPR includes a command line utility: `alpr`.  Options may be specified for a variety of needs:

### `alpr` options
 + `-c``--country` _country code_ - Either `us` for USA or `eu` for Europe; default: `us`
 + `--config` _config file_ - Path to the `openalpr.conf` file
 + `-n``--topn` _integer_ - Maximum possible plates to return; default: `10`
 + `--seek` _milliseconds_ -  Seek to the specified millisecond in a video file; default: `0`
 + `-p``--pattern` _pattern code_ - Pattern to match (e.g. `H7*`) for plate; default: _none_
 + `--clock` _on/off_ -  Measure the total time to process image and all plates; default: `off`
 + `-j``--json` - Output recognition results in JSON format; default: _false_

## Example
After successfully building the `alpr` executable  use the shell script [alpranno.sh](example/alpranno.sh) to annotate the original image with all detected license plates, for example:

```
% cd example
% ../src/build/alpr --json ea7the.jpg | tee ea7the.json | jq '.'
{
  "version":2,
  "data_type":"alpr_results",
  "epoch_time":1583029314644,
  "img_width":636,
  "img_height":358,
  "processing_time_ms":250.124680,
  "regions_of_interest":[{"x":0,"y":0,"width":636,"height":358}],
  "results":[
    {
      "plate":"EA7THE",
        "confidence":91.147400,
        "matches_template":0,
        "plate_index":0,
        "region":"",
        "region_confidence":0,
        "processing_time_ms":63.775341,
        "requested_topn":10,
        "coordinates":[{"x":206,"y":163},{"x":391,"y":161},{"x":394,"y":245},{"x":207,"y":248}],
        "candidates":[
          {"plate":"EA7THE","confidence":91.147400,"matches_template":0},
          {"plate":"EA7TBE","confidence":81.818542,"matches_template":0},
          {"plate":"EA7TRE","confidence":79.659111,"matches_template":0},        
          {"plate":"EA7TE","confidence":79.018761,"matches_template":0},
          {"plate":"EA7T8E","confidence":78.560219,"matches_template":0},
          {"plate":"EA7IHE","confidence":78.108887,"matches_template":0},
          {"plate":"EA7HE","confidence":78.106224,"matches_template":0},
          {"plate":"EA7TME","confidence":78.101746,"matches_template":0},
          {"plate":"EA7THB","confidence":77.812828,"matches_template":0},
          {"plate":"EA7TH6","confidence":76.512367,"matches_template":0}
      ]
    }
  ]
}
```

# `alpranno.sh` script

The script requires [ImageMagick](https://imagemagick.org/index.php) and [`jq`](https://stedolan.github.io/jq/) software; to install on Debian LINUX: 

```
sudo apt update -qq -y && apt install -qq -y imagemagick jq
```

Use the the shell script to annotate the image; for example:

```
% ./alpranno.sh ea7the
ea7the-alpr.jpg
```


### Output
![](example/ea7the-alpr.jpg?raw=true "EA7THE")

# Changelog & Releases

Releases are based on Semantic Versioning, and use the format
of ``MAJOR.MINOR.PATCH``. In a nutshell, the version will be incremented
based on the following:

- ``MAJOR``: Incompatible or major changes.
- ``MINOR``: Backwards-compatible new features and enhancements.
- ``PATCH``: Backwards-compatible bugfixes and package updates.

# Authors & contributors

David C Martin (github@dcmartin.com)
