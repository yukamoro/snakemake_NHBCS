# snakemake

Run:

snakemake -s /home/vklepacc/software/repos/snakemake_workflows/run.snakefile \
    --configfile config.yaml --cluster-config cluster.yaml \
    --cluster "mksub -l nodes={cluster.nodes}:ppn={cluster.ppn} -l walltime={cluster.walltime}  -o output/logs/{rule}-%j.o -e output/logs/{rule}-%j.e" \
    --jobs 16 --latency-wait 15
