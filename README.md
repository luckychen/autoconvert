
Illumina idat to gtc AutoConvert Executable at Linux 
======

This is a slightly modified version of Illumina AutoConvert.exe which convert .idat to .gtc file, the purpose of this project is running AutoConvert with mono at linux platform. 

This method is based on project <a href="https://github.com/freeseek/gtc2vcf">Harverd GTC2VCF</a>
Please be awared that AutoConvert is developed by Illumina, and Illumina DO NOT recommend to run AutoConvert like this.

pre request:
=====

Using ubuntu as example
```
sudo apt install wget gzip unzip samtools mono-devel libgdiplus
sudo apt install liblzma-dev libbz2-dev libgsl-dev 
```
To convert the idat file to GTC file, using the following command:
```
mono $HOME/bin/autoconvert/AutoConvert.exe $path_to_idat_folder $path_to_output_folder $manifest_file $egt_file
```
Assume that idat file is stored at ../gtc/4281452309_R01C01 folder, and the manifest file is Human610-Quadv1_H.bpm the cluster file is Human610-Quad_v1_H.egt

```
mono AutoConvert.exe ../gtc/4281452309_R01C01/4281452309_R01C01_Grn.idat ../gtc/4281452309_R01C01 ../gtc/Human610-Quadv1_H.bpm ../gtc/Human610-Quad_v1_H.egt
```
The GTC file will be generated at the same folder 

Convert the GTC file to VCF file
======

This part is according to <a href="https://github.com/Illumina/GTCtoVCF">GTC to VFC project</a>  

Firstly do:

```
git clone https://github.com/Illumina/GTCtoVCF.git
```
Then do the installtion of python modules:

```
pip install pysam
pip install pyvcf

```
after that do the Reference genome file download, I named the file nipm.fasta:
We should also using samtools to do the index
```
./download_reference.sh nipm.fasta
samtools faidx nipm.fasta
```
Then using the python script provided to complete the transfer
```
python gtc_to_vcf.py --gtc-paths ../gtc/4281452309_R01C01 --manifest-file ../gtc/Human610-Quadv1_H.bpm --genome-fasta-file ./nipm.fasta --output-vcf-path ../gtc/4281452309_R01C0

```

