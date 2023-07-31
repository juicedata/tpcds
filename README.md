# Spark SQL TPCDS Tests
## build spark-sql-perf
```shell
cd spark-sql-perf
sbt 'set test in assembly := {}' clean assembly
```
## run tpcds

Modify the parameters in script `run.sh` before run it.

If you want to also save table metadata to hive. Use `--enableHive true` for tpcds benchmark.

```shell
./run.sh
```

After the benchmark success. 
The result will be printed the console and save to $location/results.

# NNBench
## 1. Local Benchmark
- **create**

  ```shell
  hadoop jar juicefs-hadoop.jar nnbench create -files 10000 -baseDir jfs://{JFS_NAME}/tmp/benchmarks/NNBench -local
  ```

  This command will create 10000 empty files

- **open**

  ```shell
  hadoop jar juicefs-hadoop.jar nnbench open -files 10000 -baseDir jfs://{JFS_NAME}/tmp/benchmarks/NNBench -local
  ```

  This command will open 10000 files without reading data

- **rename**

  ```shell
  hadoop jar juicefs-hadoop.jar nnbench rename -files 10000 -baseDir jfs://{JFS_NAME}/tmp/benchmarks/NNBench -local
  ```

- **delete**

  ```shell
  hadoop jar juicefs-hadoop.jar nnbench delete -files 10000 -baseDir jfs://{JFS_NAME}/tmp/benchmarks/NNBench -local
  ```

## 2. Distributed Benchmark

The following command will start the MapReduce distributed task to test the metadata and IO performance. During the test, it is necessary to ensure that the cluster has sufficient resources to start the required map tasks.

#### Metadata

- **create**

  ```shell
  hadoop jar juicefs-hadoop.jar nnbench create -maps 10 -threads 10 -files 1000 -baseDir jfs://{JFS_NAME}/tmp/benchmarks/NNBench
  ```

  10 map task, each has 10 threads, each thread create 1000 empty file. 100000 files in total

- **open**

  ```shell
  hadoop jar juicefs-hadoop.jar nnbench open -maps 10 -threads 10 -files 1000 -baseDir jfs://{JFS_NAME}/tmp/benchmarks/NNBench
  ```

  10 map task, each has 10 threads, each thread open 1000 file. 100000 files in total

- **rename**

  ```shell
  hadoop jar juicefs-hadoop.jar nnbench rename -maps 10 -threads 10 -files 1000 -baseDir jfs://{JFS_NAME}/tmp/benchmarks/NNBench
  ```

  10 map task, each has 10 threads, each thread rename 1000 file. 100000 files in total

- **delete**

  ```shell
  hadoop jar juicefs-hadoop.jar nnbench delete -maps 10 -threads 10 -files 1000 -baseDir jfs://{JFS_NAME}/tmp/benchmarks/NNBench
  ```

  10 map task, each has 10 threads, each thread delete 1000 file. 100000 files in total
