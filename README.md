# CAPLibpp
C++ library to process NOAA CAP XML Files.
This library is designed to process NOAA CAP feeds as found at https://alerts.weather.gov/.

## Installation
It depends on Boost, curlpp, libcurl, and cmake.

```bash
mkdir build
cd build
cmake ..
make
```
## Tests
This project uses the Google Test framework.  Install that to run the tests.

```bash
mkdir build
cd build
cmake ..
make
cd tests
./caplibpp_unit_test
```

## Usage
See the main.cpp file under src.

## Contributing
Feel free! For anything major please open an issue first before issuing a pull

## License
[MIT](https://choosealicense.com/licenses/mit/)
