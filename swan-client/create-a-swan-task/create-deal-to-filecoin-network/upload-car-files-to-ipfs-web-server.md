# Upload Car files to ipfs/web server



After the car files are generated, you need to copy the files to a web-server manually, or you can upload the files to local ipfs server.

If you decide to upload the files to local ipfs server:

```
python3 swan_cli.py upload --input-dir [input_file_dir]
```

The output will be like:

```
INFO:root:Uploading car file [car_file]
INFO:root:Car file [car_file] uploaded: http://127.0.0.1:8080/ipfs/QmPrQPfGCAHwYXDZDdmLXieoxZP5JtwQuZMUEGuspKFZKQ
```
