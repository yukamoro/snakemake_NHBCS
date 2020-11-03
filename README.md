# Snakemake

- [ ] change name of .yaml files?
- [ ] double check submission syntax

Run:

```sh
snakemake -s /home/vklepacc/software/repos/snakemake_workflows/run.snakefile \
    --configfile config.yaml --cluster-config cluster.yaml \
    --cluster "mksub -l nodes={cluster.nodes}:ppn={cluster.ppn} -l walltime={cluster.walltime} -l mem_free={cluster.memory} -o output/logs/{rule}-%j.o -e output/logs/{rule}-%j.e" \
    --jobs 16 --latency-wait 15
```

## Notes

- Need to make sure paths in config are actually used in snakemake rules
- Probably run two separate workflows, one for single and one for paired
- Can use symlinks for raw files. For example:
  
  ```sh
  ln -s /path/to/files/*_single.fastq.gz workflows/single/

  ln -s /path/to/files/*_paired.fastq.gz workflows/paired/
  ```

- this doesn't actually copy files. Can also do this from a file list:

    ```sh
    cat list_of_singles.txt | xargs -n1 -I{} ln -s {} workflows/single/
    ```
