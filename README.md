# Vcall
A variantcalling pipeline.
:warning: still in development :construction:

### How to run it

1. Have [Docker](https://www.docker.com/get-started) installed (absolutely necessary if you wat to rebuild the docker).
1b. Use [udocker](https://github.com/indigo-dc/udocker) instead - this is what is available in our servers, do this is what will be mentioned in the examples.

2. Open Command Prompt

3. In Command Prompt type: 

```
udocker pull jpmatos/vcall:0.2.2 (or other tag)
udocker create vcall jpmatos/vcall:0.2.2
```

4. Config the config_docker.yaml by changing 'Dir_settings:', 'Settings:' and 'Threads':

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

But remember to delete the containers when you finish, otherwise udocker will start occupying a lot of disk space.


:warning: still in development :construction:

