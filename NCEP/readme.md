NCEP Implementation of Pangu-Weather model using GDAS data as ICs

This repository provides scripts to run pangu-weather using GDAS products as inputs. Scripts include:
- `gdas_utility.py`: a Python script designed to download NCEP Global Data Assimilation System (GDAS) data from NOAA S3 bucket (or NOMADS), and prepare input data for pangu-weather.

## Prerequisites and Installation

To install the package, run the following commands:

```bash
conda create --name mlwp python=3.10
```

```bash
conda activate mlwp
```

```bash
pip install dm-tree boto3 xarray netcdf4 pygrib
```

```bash
conda install --channel conda-forge cartopy
```


Additionally, the utility uses the `wgrib2` library for extracting specific variables from the GDAS data. You can download and install `wgrib2` from [here](http://www.cpc.ncep.noaa.gov/products/wesley/wgrib2/). Make sure it is included in the system PATH.

## Usage

To use the utility, follow these steps:

Clone the NOAA-EMC Pangu-Weather repository:

```bash   
git clone https://github.com/LinlinCui-NOAA/Pangu-Weather.git
```

```bash
cd Pangu-Weather/NCEP
```

## GDAS Utility

To download and prepare GDAS data, use the following command:

```bash
python3 gdas_utility.py yyyymmddhh yyyymmddhh --level 13 --source s3 --output /directory/to/output --download /directory/to/download --keep no
```

#### Arguments (required):

- `yyyymmddhh`: Start datetime
- `yyyymmddhh`: End datetime

#### Arguments (optional):

- `-l or --level`: [13, 37], represents the number of pressure levels (default: 13)
- `-s or --source`: [s3, nomads], represents the source to download GDAS data (default: "s3")
- `-o or --output`: /directory/to/output, represents the directory to output netcdf file (default: "current directory")
- `-d or --download`: /directory/to/download, represents the download directory for grib2 files (default: "current directory")
- `-k or --keep`: [yes, no], specifies whether to keep downloaded data after processing (default: "no")

Example usage with options:

```bash
python3 gdas_utility.py 2023060600 2023060606 -o /path/to/output -d /path/to/download
```
