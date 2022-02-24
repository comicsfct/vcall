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

. Adjust the configuration file config.yaml by changing the appropriate variables:

:warning: still in development :construction:



5. In Command Prompt type:
```
udocker run -v </your_directory/>:/mnt/share vcall snakemake --snakefile /mnt/share/vcall-pipe.snake -p /mnt/share/repo/example_dataset/output/<analisis_to_make> --cores <n_of_avaliable_cores>
```

| Analysis_to_make:

> For comparation between Tumor and Normal reads:
```
/{your_read}.Normal_VS_Tumor_output.vcf 
```
> For Analisis of Copy-number variantes:
```
/{your_read}.my_reference.cnn
```
> For Annotation:
```
/{your_read}.exome_seq_final.vcf.gz
```
6. Then collect your output-file:
```
Output dir example:
/mnt/share/repo/example_dataset/output/T.vcf
```

Caution: you cannot use the same container several times simultaneously. 
If you're going to run several times the same image, you need to run each in their own separate container:
```
udocker run -v </your_directory/>:/mnt/share jpmatos/vcall:0.2.2 snakemake --snakefile /mnt/share/vcall-pipe.snake -p /mnt/share/repo/example_dataset/output/<analisis_to_make> --cores <n_of_avaliable_cores>
```


:warning: still in development :construction:

