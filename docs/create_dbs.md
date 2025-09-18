# Create databases

- [Create databases](#create-databases)
  - [Information](#information)
  - [REVEL](#revel)
    - [1.3](#13)
  - [gnomad](#gnomad)
    - [4.1.0](#410)

## Information

Documentation on creating database files

## REVEL

### 1.3

```bash
# download database
lk0657@gadi-login-03:~:$ curl -o revel-v1.3_all_chromosomes.zip https://zenodo.org/records/7072866/files/revel-v1.3_all_chromosomes.zip?download=1
  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
100  636M  100  636M    0     0  7480k      0  0:01:27  0:01:27 --:--:-- 10.2M

# uncompress
lk0657@gadi-login-03:~:$ unzip revel-v1.3_all_chromosomes.zip
Archive:  revel-v1.3_all_chromosomes.zip
  inflating: revel_with_transcript_ids

# tabix-process
# convert from comma seperated to tab seperated
lk0657@gadi-login-03:~:$ cat revel_with_transcript_ids | tr "," "\t" > tabbed_revel.tsv
lk0657@gadi-login-03:~:$ sed '1s/.*/#&/' tabbed_revel.tsv > new_tabbed_revel.tsv

# recompress
lk0657@gadi-login-03:~:$ module load htslib/1.16
lk0657@gadi-login-03:~:$ bgzip new_tabbed_revel.tsv

# process for GRCh38
lk0657@gadi-login-03:~:$ zgrep -h -v ^#chr new_tabbed_revel.tsv.gz | awk '$3 != "." ' | sort -k1,1 -k3,3n - | cat h - > new_tabbed_revel_grch38.tsv
lk0657@gadi-login-03:~:$ tabix -f -s 1 -b 3 -e 3 new_tabbed_revel_grch38.tsv.gz

# cleanup
lk0657@gadi-login-03:~:$ rm h revel-v1.3_all_chromosomes.zip tabbed_revel.tsv new_tabbed_revel.tsv.gz revel_with_transcript_ids
```

## gnomad

### 4.1.0

```bash
# download database
lk0657@gadi-login-03:~:$ for CHR in {1..22} X Y; do curl -O https://storage.googleapis.com/gcp-public-data--gnomad/release/4.1/vcf/joint/gnomad.joint.v4.1.sites.chr${CHR}.vcf.bgz; done
  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
100 67.1G  100 67.1G    0     0  16.5M      0  1:09:18  1:09:18 --:--:-- 17.8M
  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
100 64.6G  100 64.6G    0     0  23.0M      0  0:47:54  0:47:54 --:--:-- 24.9M
  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
100 52.2G  100 52.2G    0     0  24.4M      0  0:36:26  0:36:26 --:--:-- 25.5M
  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
100 48.0G  100 48.0G    0     0  17.8M      0  0:46:02  0:46:02 --:--:-- 20.2M
  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
100 46.0G  100 46.0G    0     0  20.3M      0  0:38:32  0:38:32 --:--:-- 18.8M
  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
100 44.5G  100 44.5G    0     0  25.0M      0  0:30:19  0:30:19 --:--:-- 25.6M
  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
100 44.2G  100 44.2G    0     0  15.6M      0  0:48:23  0:48:23 --:--:-- 14.4M
  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
100 39.2G  100 39.2G    0     0  20.2M      0  0:33:04  0:33:04 --:--:-- 21.5M
  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
100 35.1G  100 35.1G    0     0  25.3M      0  0:23:43  0:23:43 --:--:-- 26.5M
  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
100 36.4G  100 36.4G    0     0  20.1M      0  0:30:50  0:30:50 --:--:-- 19.4M
  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
100 39.7G  100 39.7G    0     0  20.6M      0  0:32:54  0:32:54 --:--:-- 24.0M
  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
100 38.5G  100 38.5G    0     0  21.1M      0  0:31:03  0:31:03 --:--:-- 21.6M
  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
100 23.8G  100 23.8G    0     0  12.4M      0  0:32:34  0:32:34 --:--:-- 12.2M
  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
100 25.8G  100 25.8G    0     0  21.3M      0  0:20:38  0:20:38 --:--:-- 21.1M
  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
100 25.5G  100 25.5G    0     0  14.4M      0  0:30:09  0:30:09 --:--:-- 12.2M
  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
100 29.4G  100 29.4G    0     0  25.0M      0  0:20:04  0:20:04 --:--:-- 26.0M
  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
100 29.6G  100 29.6G    0     0  18.3M      0  0:27:38  0:27:38 --:--:-- 21.3M
  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
100 19.0G  100 19.0G    0     0  22.2M      0  0:14:37  0:14:37 --:--:-- 23.2M
  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
100 27.0G  100 27.0G    0     0  22.0M      0  0:20:57  0:20:57 --:--:-- 20.8M
  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
100 18.1G  100 18.1G    0     0  25.0M      0  0:12:21  0:12:21 --:--:-- 25.7M
  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
100 11.0G  100 11.0G    0     0  17.9M      0  0:10:30  0:10:30 --:--:-- 16.4M
  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
100 14.5G  100 14.5G    0     0  24.9M      0  0:09:57  0:09:57 --:--:-- 24.7M
  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
100 35.4G  100 35.4G    0     0  22.6M      0  0:26:46  0:26:46 --:--:-- 21.6M
  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
100  777M  100  777M    0     0  23.5M      0  0:00:32  0:00:32 --:--:-- 24.8M

# pair back database
lk0657@gadi-login-03:~:$ cat strip_gnomad.sh
#!/bin/bash

#PBS -P kr68
#PBS -l storage=scratch/kr68
#PBS -q normal
#PBS -l ncpus=1
#PBS -l mem=4gb
#PBS -l walltime=24:00:00
#PBS -l wd

# load modules
module load bcftools/1.21
module load htslib/1.16

# get header
for CHR in {1..22} X Y; do zcat gnomad.joint.v4.1.sites.chr${CHR}.vcf.bgz | head -n2000 | grep -E '##fileformat|##hailversion|##FILTER|##INFO=<ID=AF_joint,|##INFO=<ID=AF_exomes,|##INFO=<ID=AF_genomes,|##INFO=<ID=nhomalt_joint,|##INFO=<ID=nhomalt_exomes,|##INFO=<ID=nhomalt_genomes,|##age_distribution|##contig|#CHROM' > gnomad.joint.v4.1.sites.chr${CHR}.minimal.vcf; done

# subset gnomad database
for CHR in {1..22} X Y; do bcftools query -f '%CHROM\t%POS\t%ID\t%REF\t%ALT\t%QUAL\t%FILTER\tAF_joint=%INFO/AF_joint\;AF_exomes=%INFO/AF_exomes\;AF_genomes=%INFO/AF_genomes\;nhomalt_joint=%INFO/nhomalt_joint\;nhomalt_exomes=%INFO/nhomalt_exomes\;nhomalt_genomes=%INFO/nhomalt_genomes\n' gnomad.joint.v4.1.sites.chr${CHR}.vcf.bgz >> gnomad.joint.v4.1.sites.chr${CHR}.minimal.vcf; done

# compress
for CHR in {1..22} X Y; do bgzip gnomad.joint.v4.1.sites.chr${CHR}.minimal.vcf; done
lk0657@gadi-login-03:~:$ qsub strip_gnomad.sh
149926982.gadi-pbs
```

