# Submission to NCBI Using Aspera Connect Command Line

This repository demonstrates how to submit raw sequencing reads to NCBI SRA using Aspera Connect via the command line.

## 1. Prepare metadata

1. Go to the [SRA Submission Portal](https://submit.ncbi.nlm.nih.gov/subs/sra/) and click **New Submission**.
2. Verify your credentials and click **Continue**.
3. Complete all required information and metadata files.

## 2. Connect to Aspera-connect

1. Connect to your HPC cluster.
2. Download the Aspera Connect client using the following command:

   ```bash
   wget https://d3gcli72yxqn2z.cloudfront.net/downloads/connect/latest/bin/ibm-aspera-connect_4.2.12.780_linux_x86_64.tar.gz
``` 
3. Unzip the folder:
 
 ```bash
 tar -zxvf ibm-aspera-connect_4.2.12.780_linux_x86_64.tar.gz
```
4. Install Aspera Connect:
```bash
./ibm-aspera-connect_4.2.12.780_linux_x86_64.sh
```
5. Download the ```aspera.openssh``` key given in  ```NCBI submission portal``` and make sure it has the proper permission:

```bash
chmod 600 <path-to-aspera.openssh>
```
## 3. Preparing raw-data files
1. Create a new directory, preferably named after the temporary submission ID (e.g., ```SUB14915373```):
```bash
mkdir SUB14915373
cd SUB14915373
```
2. Copy all the ```fastq.gz``` files to this directory
```ba
sh
cp /path/to/your/fastq/files/*.fastq.gz .
```
3. Upload the files using the ```ascp``` command:
```bash
ascp -i /path/to/aspera.openssh -QT -v -k1 -d /path/to/SUB14915373 subasp@upload.ncbi.nlm.nih.gov:uploads/your_email_w3RSBObO

```

### Replace:

<path-to-aspera.openssh> with the actual path to your aspera.openssh key.
/path/to/SUB14915373 with the full path to your submission directory.
your_email_w3RSBObO with the upload directory provided by NCBI.

## 4. Finalize submission
once the files are uploaded, wait for 10 minutes for the upload to be shown on the NCBI submission portal click on the ```Request preload folder```, you should see folder having the raw fastq.gz files,
select the folder and click on ``` Autofinish submission``` then ```Continue```. 

