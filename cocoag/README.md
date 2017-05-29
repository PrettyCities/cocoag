CocoaG
======

Automate code coverage badge creation in Python 3.

# Requirements
- Existing github project
- Tests written using the pytest package
- AWS S3 credentials to upload images to a bucket

# Install
`pip install cocoag`

# Configuration
CocoaG uses a configuration file called `.cocoag.cfg`. 
This file should be located in your user's root directory: `~/.cocoag.cfg`.

If this is your first time running CocoaG or you don't already have a `.cocoag.cfg` in your root directory,
run the following command and CocoaG will generate a template configuration file for you.

`cocoag --init`

Open the generated file in your favorite text editor and update the following configuration variables:

#### general
`package_root`: Path to the CocoaG python package. This should be automatically configured for you.
Do **not** change it.

`svg_output_file_name`: The name of the output coverage badge. This is defaulted to `cocoag.svg`,
however you may change it if you desire. 

Note that CocoaG writes this file to the `package_root` directory.
The resulting image is overwritten during each run. To view all output images, refer to your s3 bucket. 

#### logging
`enable_logging`: Whether logging should be enabled or not.

Potential values: `True`, `False`.

*Note: You can ignore the following variables if you set `enable_logging` to `False`.
If you choose to enable logging, the following logging variables must be properly configured.*


`log_level`: The level at which you wish to log.

Potential values: Default values outlined in the 
[Python 3 Documentation](https://docs.python.org/3/howto/logging.html#when-to-use-logging).

`logging_output_file`: The file where logs should be saved.
  
Potential values: Path to a file.

#### project
`root_dir`: The root directory of the project on which you would like to run CocoaG.

Potential values: Path to a directory.

`sub_directories`: Paths off the root directory for which you would like to generate coverage badges.

For example, given the following directory structure...

```
├── cocoag
│   ├── LICENSE
│   ├── README.md
│   ├── __init__.py
│   ├── configuration
│   │   ├── __init__.py
│   │   ├── config.py
│   │   └── default_cocoag.cfg
│   ├── generator
│   │   ├── README.md
│   │   ├── __init__.py
│   │   ├── coverage_generator.py
│   │   ├── test
│   │   └── utils
│   └── s3
│       ├── README.md
│       ├── __init__.py
│       ├── s3_client.py
│       └── test
```

if you set the `root_dir` to `path/to/cocoag`, setting subdirectories to

```
subdirectories =
    generator
    s3
```

will generate coverage badges for the `generator` and `s3` directories respectively.

Note that the directories you provide must have tests written.
 
#### s3
`bucket`: The name of the bucket to which you would like to save the generated coverage badges.

Potential values: Any valid s3 bucket name.

`access_key`: An AWS access key that has permissions to write to the specified s3 bucket.

Potential values: Any valid AWS access key.

`secret_access_key`: The secret access key associated with the access key provided above.

Potential values: Any valid secret access key.

# Usage
Simply run the `cocoag` command from anywhere in a directory in a package that has CocoaG installed.



