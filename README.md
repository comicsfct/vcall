# Vcall

A variant calling pipeline based on GATK 3.8.

### How to run it

. Use [Docker](https://www.docker.com/get-started), [udocker](https://github.com/indigo-dc/udocker) or other alternatives.

. Pull the docker image (example using udocker).
```
udocker pull comicspt/vcall:0.2.2
udocker create --name=vcall comicspt/vcall:0.2.2
```

Due to licensing restrictions on GATK 3.8, the docker image does not contain GATK itself. 

Therefore, the first time you use the image you need to install GATK. 

For this, you need to download GATK 3.8 and place the GenomeAnalysisTK.jar in a local folder.

. Install the GATK in the docker image, assuming GenomeAnalysisTK.jar is in /localfolder/ (adapt to your case)
```
udocker run -v /localfolder/:/dockerfolder/: vcall gatk3-register /dockerfolder/GenomeAnalysisTK.jar
```

. Clone the current git
```
git clone https://github.com/comicsfct/vcall.git
```

. Adjust the configuration file config.yaml by changing the appropriate variables:



. The general process to run the pipeline is by running:
```
udocker run -v /localfolder/:/mnt/data vcall snakemake --snakefile /mnt/data/vcall.snake --directory /mnt/data/ -p /mnt/data/output/<analisis_to_make> --cores <n_of_avaliable_cores>
```

| Somatic Variant Calling using Mutect

You need to have files named <sample>.T.read1.fastq.gz (for tumor) and <sample>.N.read1.fastq.gz (for paired normal)

```
udocker run -v /localfolder/:/mnt/data vcall snakemake --snakefile /mnt/data/vcall.snake --directory /mnt/data/ -p /mnt/data/output/<sample>.Normal_VS_Tumor_output.vcf --cores <n_of_avaliable_cores>
```

If all goes well the output will be in /mnt/data/output/<sample>.Normal_VS_Tumor_output.vcf 
  
Logs should be generated in /mnt/data/logs


