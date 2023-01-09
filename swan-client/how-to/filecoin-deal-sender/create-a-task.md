# Create a Task

You can create three different kinds of tasks using the `car.json` or `car.csv`

## **Private Task**

You can directly send deals to miners by creating a private task

```shell
./swan-client task --input-dir [json_or_csv_absolute_path] --out-dir [output_files_dir] --miners [storage_provider_id1,storage_provider_id2,...]

OPTIONS:
   --name value                          task name
   --input-dir value, -i value           absolute path where the json or csv format source files
   --out-dir value, -o value             directory where target files will be in (default: "/tmp/tasks")
   --auto-bid                            send the auto-bid task (default: false)
   --manual-bid                          send the manual-bid task (default: false)
   --miners value                        miners is required when sending private tasks (pass comma separated array of minerIDs)
   --dataset value                       curated dataset
   --description value, -d value         task description
   --max-copy-number value, --max value  max copy numbers when sending auto-bid or manual-bid task (default: 1)

```

**Files generated after this step:**

* `[task-name]-metadata.json`: contains `Uuid` and `Deals` for storage providers to import deals.

## Auto-bid Task

```shell
./swan-client task --input-dir [json_or_csv_absolute_path] --out-dir [output_files_dir] --auto-bid true --max-copy-number 5


OPTIONS:
   --name value                          task name
   --input-dir value, -i value           absolute path where the json or csv format source files
   --out-dir value, -o value             directory where target files will be in (default: "/tmp/tasks")
   --auto-bid                            send the auto-bid task (default: false)
   --manual-bid                          send the manual-bid task (default: false)
   --miners value                        miners is required when sending private tasks (pass comma separated array of minerIDs)
   --dataset value                       curated dataset
   --description value, -d value         task description
   --max-copy-number value, --max value  max copy numbers when sending auto-bid or manual-bid task (default: 1)

```

**Files generated after this step:**

* `[task-name]-metadata.json`: contains `Uuid` and `Deals` for storage providers to import deals.

## Manual-bid Task

You can create manual-bid tasks on the Swan Platform. And each storage provider can apply this task from the Swan Platform. After that, you can send deals to the storage providers.

### **1) Create manulal-bid task:**

```shell
./swan-client task --input-dir [json_or_csv_absolute_path] --out-dir [output_files_dir] --manual-bid true --max-copy-number 5


OPTIONS:
   --name value                          task name
   --input-dir value, -i value           absolute path where the json or csv format source files
   --out-dir value, -o value             directory where target files will be in (default: "/tmp/tasks")
   --auto-bid                            send the auto-bid task (default: false)
   --manual-bid                          send the manual-bid task (default: false)
   --miners value                        miners is required when sending private tasks (pass comma separated array of minerIDs)
   --dataset value                       curated dataset
   --description value, -d value         task description
   --max-copy-number value, --max value  max copy numbers when sending auto-bid or manual-bid task (default: 1)
```

**Files generated after this step:**

* `[task-name]-metadata.json`: contains the `Uuid`, source file information, and CAR file information.

### **2) Send deals to the storage providers:**

```shell
./swan-client deal --json [path]/[task-name]-metadata.json -out-dir [output_files_dir] -miners [storage_provider_id1,storage_provider_id2,... ]

OPTIONS:
   --csv value                the CSV file path of deal metadata
   --json value               the JSON file path of deal metadata
   --out-dir value, -o value  directory where target files will in (default: "/tmp/tasks")
   --miners value             miners is required when sending manual-bid task (pass comma separated array of minerIDs)

```

**Files generated after this step:**

* `[task-name]-deals.json`: `Deals`information updated based on `[task-name]-metadata.json` generated in the previous steps.

***
