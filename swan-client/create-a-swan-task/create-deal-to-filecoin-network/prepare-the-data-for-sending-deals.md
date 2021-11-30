# Prepare the data for sending deals

#### **Generate Car files using Lotus (option 1)**

```
python3 swan_cli.py car --input-dir [input_files_dir] --out-dir [car_files_output_dir] 
```

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
