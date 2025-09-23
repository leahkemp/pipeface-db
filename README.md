# Pipeface DB

Minimal and pre-pre-processed variant databases used in the variant annotation component of [pipeface](https://github.com/leahkemp/pipeface).

Download with:

```bash
# revel
wget https://media.githubusercontent.com/media/leahkemp/pipeface-db/main/revel/1.3/new_tabbed_revel_grch38.tsv.gz
wget https://media.githubusercontent.com/media/leahkemp/pipeface-db/main/revel/1.3/new_tabbed_revel_grch38.tsv.gz.tbi

# gnomad
for i in {1..22} X Y; do wget https://github.com/leahkemp/pipeface-db/raw/refs/heads/main/gnomad/4.1.0/gnomad.joint.v4.1.sites.chr${i}.minimal.vcf.gz; done
```

