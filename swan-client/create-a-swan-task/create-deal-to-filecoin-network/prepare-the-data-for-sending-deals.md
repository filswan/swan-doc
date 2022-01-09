# Prepare the data for sending deals

#### **Generate Car files using Lotus (option 1)**

```
python3 swan_cli.py car --input-dir [input_files_dir] --out-dir [car_files_output_dir] 
```

{% hint style="warning" %}
Note: The input dir and out dir shall only be in format of Absolute Path.
{% endhint %}

The output will be like:

```
INFO:root:Generating car file from: [input_file_dir]/ubuntu-15.04-server-i386.iso.tar
INFO:root:car file Generated: [car_files_output_dir]/ubuntu-15.04-server-i386.iso.tar.car, piece cid: baga6ea4seaqbpggkuxz7gpkm2wf3734gkyna3vb4p7bm3qcbl4gb4jgh22vj2pi, piece size: 15.88 GiB
INFO:root:Generating data CID....
INFO:root:Data CID: bafykbzacebbq4g73e4he32ahyynnamrft2tva2jyjt5fsxfqv76anptmyoajw
INFO:root:Car files output dir: [car_files_output_dir]
INFO:root:Please upload car files to web server or ipfs server.
```

If _--out-dir_ is not provided, then the output directory for the car files will be: _output\_dir_ (specified in the configuration file) + random\_uuid

e.g. : /tmp/tasks/7f33a9d6-47d0-4635-b152-5e380733bf09

**Generate Car files without using Lotus (option 2)**

To use the generation locally, make sure go is available before starting.

Generate car files using golang

```
python3 swan_cli.py gocar --input-dir [input_files_dir] --out-dir [car_files_output_dir] 
```

For example,

```
python3 swan_cli.py gocar --input-dir ../encryption --out-dir ../gocar
```

Meanwhile, a car.csv and a manifest.csv with the detail information of the corresponding car files will be generated in the same output directory.

Credits should be given to filedrive-team. More information can be found in [https://github.com/filedrive-team/go-graphsplit](https://github.com/filedrive-team/go-graphsplit).

