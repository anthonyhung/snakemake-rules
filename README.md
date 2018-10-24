
-   [snakemake-rules](#snakemake-rules)
    -   [1 to 1](#to-1)
    -   [Many to many](#many-to-many)
    -   [Many to one](#many-to-one)
    -   [Group on a known variable](#group-on-a-known-variable)
    -   [Group on an unknown variable (stable input files)](#group-on-an-unknown-variable-stable-input-files)
    -   [Group on an unknown variable (generated input files)](#group-on-an-unknown-variable-generated-input-files)

<!-- README.md is generated from README.Rmd. Please edit that file -->
snakemake-rules
===============

1 to 1
------

``` bash
bash 01/setup.sh
ls 01/fqgz
```

    sam01-rep1-lane1.fastq.gz

![dag](01/01.png)

``` bash
snakemake -s 01/Snakefile
```

    Building DAG of jobs...
    Using shell: /bin/bash
    Provided cores: 1
    Rules claiming more threads will be scaled down.
    Job counts:
        count   jobs
        1   unzip
        1

    [Wed Oct 24 17:29:45 2018]
    rule unzip:
        input: fqgz/sam01-rep1-lane1.fastq.gz
        output: fq/sam01-rep1-lane1.fastq
        jobid: 0

    [Wed Oct 24 17:29:45 2018]
    Finished job 0.
    1 of 1 steps (100%) done
    Complete log: /home/jdb-work/repos/snakemake-rules/.snakemake/log/2018-10-24T172945.718681.snakemake.log

``` bash
ls 01/fq
```

    sam01-rep1-lane1.fastq

``` bash
snakemake -s 01/Snakefile
```

    Building DAG of jobs...
    Nothing to be done.
    Complete log: /home/jdb-work/repos/snakemake-rules/.snakemake/log/2018-10-24T172946.202164.snakemake.log

Many to many
------------

``` bash
bash 02/setup.sh
ls 02/fqgz
```

    sam1-rep1.fastq.gz
    sam1-rep2.fastq.gz
    sam2-rep1.fastq.gz
    sam2-rep2.fastq.gz
    sam3-rep1.fastq.gz
    sam3-rep2.fastq.gz
    sam4-rep1.fastq.gz
    sam4-rep2.fastq.gz
    sam5-rep1.fastq.gz
    sam5-rep2.fastq.gz

![dag](02/02.png)

``` bash
snakemake -s 02/Snakefile
```

    Building DAG of jobs...
    Using shell: /bin/bash
    Provided cores: 1
    Rules claiming more threads will be scaled down.
    Job counts:
        count   jobs
        1   all
        8   unzip
        9

    [Wed Oct 24 17:29:46 2018]
    rule unzip:
        input: fqgz/sam4-rep2.fastq.gz
        output: fq/sam4-rep2.fastq
        jobid: 6
        wildcards: sample=4, replicate=2

    [Wed Oct 24 17:29:46 2018]
    Finished job 6.
    1 of 9 steps (11%) done

    [Wed Oct 24 17:29:46 2018]
    rule unzip:
        input: fqgz/sam3-rep2.fastq.gz
        output: fq/sam3-rep2.fastq
        jobid: 2
        wildcards: sample=3, replicate=2

    [Wed Oct 24 17:29:46 2018]
    Finished job 2.
    2 of 9 steps (22%) done

    [Wed Oct 24 17:29:46 2018]
    rule unzip:
        input: fqgz/sam2-rep1.fastq.gz
        output: fq/sam2-rep1.fastq
        jobid: 4
        wildcards: sample=2, replicate=1

    [Wed Oct 24 17:29:46 2018]
    Finished job 4.
    3 of 9 steps (33%) done

    [Wed Oct 24 17:29:46 2018]
    rule unzip:
        input: fqgz/sam1-rep2.fastq.gz
        output: fq/sam1-rep2.fastq
        jobid: 7
        wildcards: sample=1, replicate=2

    [Wed Oct 24 17:29:46 2018]
    Finished job 7.
    4 of 9 steps (44%) done

    [Wed Oct 24 17:29:46 2018]
    rule unzip:
        input: fqgz/sam1-rep1.fastq.gz
        output: fq/sam1-rep1.fastq
        jobid: 3
        wildcards: sample=1, replicate=1

    [Wed Oct 24 17:29:46 2018]
    Finished job 3.
    5 of 9 steps (56%) done

    [Wed Oct 24 17:29:46 2018]
    rule unzip:
        input: fqgz/sam3-rep1.fastq.gz
        output: fq/sam3-rep1.fastq
        jobid: 1
        wildcards: sample=3, replicate=1

    [Wed Oct 24 17:29:46 2018]
    Finished job 1.
    6 of 9 steps (67%) done

    [Wed Oct 24 17:29:46 2018]
    rule unzip:
        input: fqgz/sam2-rep2.fastq.gz
        output: fq/sam2-rep2.fastq
        jobid: 8
        wildcards: sample=2, replicate=2

    [Wed Oct 24 17:29:46 2018]
    Finished job 8.
    7 of 9 steps (78%) done

    [Wed Oct 24 17:29:46 2018]
    rule unzip:
        input: fqgz/sam4-rep1.fastq.gz
        output: fq/sam4-rep1.fastq
        jobid: 5
        wildcards: sample=4, replicate=1

    [Wed Oct 24 17:29:46 2018]
    Finished job 5.
    8 of 9 steps (89%) done

    [Wed Oct 24 17:29:47 2018]
    localrule all:
        input: fq/sam1-rep1.fastq, fq/sam1-rep2.fastq, fq/sam2-rep1.fastq, fq/sam2-rep2.fastq, fq/sam3-rep1.fastq, fq/sam3-rep2.fastq, fq/sam4-rep1.fastq, fq/sam4-rep2.fastq
        jobid: 0

    [Wed Oct 24 17:29:47 2018]
    Finished job 0.
    9 of 9 steps (100%) done
    Complete log: /home/jdb-work/repos/snakemake-rules/.snakemake/log/2018-10-24T172946.851350.snakemake.log

``` bash
ls 02/fq
```

    sam01-rep1-lane1.fastq

``` bash
snakemake -s 02/Snakefile
```

    Building DAG of jobs...
    Nothing to be done.
    Complete log: /home/jdb-work/repos/snakemake-rules/.snakemake/log/2018-10-24T172947.272275.snakemake.log

Many to one
-----------

``` bash
bash 03/setup.sh
ls 03/fqgz
```

    sam1-rep1.fastq.gz
    sam1-rep2.fastq.gz
    sam2-rep1.fastq.gz
    sam2-rep2.fastq.gz
    sam3-rep1.fastq.gz
    sam3-rep2.fastq.gz
    sam4-rep1.fastq.gz
    sam4-rep2.fastq.gz
    sam5-rep1.fastq.gz
    sam5-rep2.fastq.gz

![dag](03/03.png)

``` bash
snakemake -s 03/Snakefile
```

    Building DAG of jobs...
    Using shell: /bin/bash
    Provided cores: 1
    Rules claiming more threads will be scaled down.
    Job counts:
        count   jobs
        1   all
        1   combine
        8   unzip
        10

    [Wed Oct 24 17:29:48 2018]
    rule unzip:
        input: fqgz/sam4-rep1.fastq.gz
        output: fq/sam4-rep1.fastq
        jobid: 2
        wildcards: sample=4, replicate=1

    [Wed Oct 24 17:29:48 2018]
    Finished job 2.
    1 of 10 steps (10%) done

    [Wed Oct 24 17:29:48 2018]
    rule unzip:
        input: fqgz/sam1-rep2.fastq.gz
        output: fq/sam1-rep2.fastq
        jobid: 4
        wildcards: sample=1, replicate=2

    [Wed Oct 24 17:29:48 2018]
    Finished job 4.
    2 of 10 steps (20%) done

    [Wed Oct 24 17:29:48 2018]
    rule unzip:
        input: fqgz/sam2-rep1.fastq.gz
        output: fq/sam2-rep1.fastq
        jobid: 8
        wildcards: sample=2, replicate=1

    [Wed Oct 24 17:29:48 2018]
    Finished job 8.
    3 of 10 steps (30%) done

    [Wed Oct 24 17:29:48 2018]
    rule unzip:
        input: fqgz/sam3-rep2.fastq.gz
        output: fq/sam3-rep2.fastq
        jobid: 9
        wildcards: sample=3, replicate=2

    [Wed Oct 24 17:29:48 2018]
    Finished job 9.
    4 of 10 steps (40%) done

    [Wed Oct 24 17:29:48 2018]
    rule unzip:
        input: fqgz/sam4-rep2.fastq.gz
        output: fq/sam4-rep2.fastq
        jobid: 3
        wildcards: sample=4, replicate=2

    [Wed Oct 24 17:29:48 2018]
    Finished job 3.
    5 of 10 steps (50%) done

    [Wed Oct 24 17:29:48 2018]
    rule unzip:
        input: fqgz/sam2-rep2.fastq.gz
        output: fq/sam2-rep2.fastq
        jobid: 5
        wildcards: sample=2, replicate=2

    [Wed Oct 24 17:29:48 2018]
    Finished job 5.
    6 of 10 steps (60%) done

    [Wed Oct 24 17:29:48 2018]
    rule unzip:
        input: fqgz/sam1-rep1.fastq.gz
        output: fq/sam1-rep1.fastq
        jobid: 6
        wildcards: sample=1, replicate=1

    [Wed Oct 24 17:29:48 2018]
    Finished job 6.
    7 of 10 steps (70%) done

    [Wed Oct 24 17:29:48 2018]
    rule unzip:
        input: fqgz/sam3-rep1.fastq.gz
        output: fq/sam3-rep1.fastq
        jobid: 7
        wildcards: sample=3, replicate=1

    [Wed Oct 24 17:29:48 2018]
    Finished job 7.
    8 of 10 steps (80%) done

    [Wed Oct 24 17:29:48 2018]
    rule combine:
        input: fq/sam1-rep1.fastq, fq/sam1-rep2.fastq, fq/sam2-rep1.fastq, fq/sam2-rep2.fastq, fq/sam3-rep1.fastq, fq/sam3-rep2.fastq, fq/sam4-rep1.fastq, fq/sam4-rep2.fastq
        output: fq/combined.fastq
        jobid: 1

    [Wed Oct 24 17:29:48 2018]
    Finished job 1.
    9 of 10 steps (90%) done

    [Wed Oct 24 17:29:48 2018]
    localrule all:
        input: fq/combined.fastq
        jobid: 0

    [Wed Oct 24 17:29:48 2018]
    Finished job 0.
    10 of 10 steps (100%) done
    Complete log: /home/jdb-work/repos/snakemake-rules/.snakemake/log/2018-10-24T172947.992801.snakemake.log

``` bash
ls 03/fq
```

    sam01-rep1-lane1.fastq

``` bash
snakemake -s 03/Snakefile
```

    Building DAG of jobs...
    Nothing to be done.
    Complete log: /home/jdb-work/repos/snakemake-rules/.snakemake/log/2018-10-24T172948.411504.snakemake.log

Group on a known variable
-------------------------

``` bash
bash 04/setup.sh
ls 04/fqgz
```

    sam1-rep1.fastq.gz
    sam1-rep2.fastq.gz
    sam2-rep1.fastq.gz
    sam2-rep2.fastq.gz
    sam3-rep1.fastq.gz
    sam3-rep2.fastq.gz
    sam4-rep1.fastq.gz
    sam4-rep2.fastq.gz
    sam5-rep1.fastq.gz
    sam5-rep2.fastq.gz

![dag](04/04.png)

``` bash
snakemake -s 04/Snakefile
```

    Building DAG of jobs...
    Using shell: /bin/bash
    Provided cores: 1
    Rules claiming more threads will be scaled down.
    Job counts:
        count   jobs
        1   all
        4   unzip
        5

    [Wed Oct 24 17:29:49 2018]
    rule unzip:
        input: fqgz/sam3-rep1.fastq.gz, fqgz/sam3-rep2.fastq.gz
        output: fq/sam3.fastq
        jobid: 2
        wildcards: sample=3

    [Wed Oct 24 17:29:49 2018]
    Finished job 2.
    1 of 5 steps (20%) done

    [Wed Oct 24 17:29:49 2018]
    rule unzip:
        input: fqgz/sam4-rep1.fastq.gz, fqgz/sam4-rep2.fastq.gz
        output: fq/sam4.fastq
        jobid: 4
        wildcards: sample=4

    [Wed Oct 24 17:29:49 2018]
    Finished job 4.
    2 of 5 steps (40%) done

    [Wed Oct 24 17:29:49 2018]
    rule unzip:
        input: fqgz/sam2-rep1.fastq.gz, fqgz/sam2-rep2.fastq.gz
        output: fq/sam2.fastq
        jobid: 3
        wildcards: sample=2

    [Wed Oct 24 17:29:49 2018]
    Finished job 3.
    3 of 5 steps (60%) done

    [Wed Oct 24 17:29:49 2018]
    rule unzip:
        input: fqgz/sam1-rep1.fastq.gz, fqgz/sam1-rep2.fastq.gz
        output: fq/sam1.fastq
        jobid: 1
        wildcards: sample=1

    [Wed Oct 24 17:29:49 2018]
    Finished job 1.
    4 of 5 steps (80%) done

    [Wed Oct 24 17:29:49 2018]
    localrule all:
        input: fq/sam1.fastq, fq/sam2.fastq, fq/sam3.fastq, fq/sam4.fastq
        jobid: 0

    [Wed Oct 24 17:29:49 2018]
    Finished job 0.
    5 of 5 steps (100%) done
    Complete log: /home/jdb-work/repos/snakemake-rules/.snakemake/log/2018-10-24T172949.050242.snakemake.log

``` bash
ls 04/fq
```

    1.fastq
    2.fastq
    3.fastq
    4.fastq
    sam01-rep1-lane1.fastq

``` bash
snakemake -s 04/Snakefile
```

    Building DAG of jobs...
    Nothing to be done.
    Complete log: /home/jdb-work/repos/snakemake-rules/.snakemake/log/2018-10-24T172949.395285.snakemake.log

Group on an unknown variable (stable input files)
-------------------------------------------------

``` bash
bash 05/setup.sh
ls 05/fqgz
```

    sam1-rep1-lane1.fastq.gz
    sam1-rep1-lane5.fastq.gz
    sam1-rep2-lane2.fastq.gz
    sam1-rep2-lane4.fastq.gz
    sam2-rep1-lane3.fastq.gz
    sam2-rep1-lane8.fastq.gz
    sam2-rep2-lane7.fastq.gz
    sam2-rep2-lane8.fastq.gz
    sam3-rep1-lane3.fastq.gz
    sam3-rep1-lane7.fastq.gz
    sam3-rep2-lane1.fastq.gz
    sam3-rep2-lane7.fastq.gz
    sam4-rep1-lane2.fastq.gz
    sam4-rep2-lane1.fastq.gz
    sam4-rep2-lane6.fastq.gz

![dag](05/05.png)

``` bash
snakemake -s 05/Snakefile
```

    Building DAG of jobs...
    Using shell: /bin/bash
    Provided cores: 1
    Rules claiming more threads will be scaled down.
    Job counts:
        count   jobs
        1   all
        8   unzip
        9

    [Wed Oct 24 17:29:50 2018]
    rule unzip:
        input: fqgz/sam3-rep1-lane3.fastq.gz, fqgz/sam3-rep1-lane7.fastq.gz
        output: fq/sam3-rep1.fastq
        jobid: 4
        wildcards: sample=3, replicate=1

    [Wed Oct 24 17:29:50 2018]
    Finished job 4.
    1 of 9 steps (11%) done

    [Wed Oct 24 17:29:50 2018]
    rule unzip:
        input: fqgz/sam2-rep1-lane3.fastq.gz, fqgz/sam2-rep1-lane8.fastq.gz
        output: fq/sam2-rep1.fastq
        jobid: 3
        wildcards: sample=2, replicate=1

    [Wed Oct 24 17:29:50 2018]
    Finished job 3.
    2 of 9 steps (22%) done

    [Wed Oct 24 17:29:50 2018]
    rule unzip:
        input: fqgz/sam1-rep2-lane4.fastq.gz, fqgz/sam1-rep2-lane2.fastq.gz
        output: fq/sam1-rep2.fastq
        jobid: 5
        wildcards: sample=1, replicate=2

    [Wed Oct 24 17:29:50 2018]
    Finished job 5.
    3 of 9 steps (33%) done

    [Wed Oct 24 17:29:50 2018]
    rule unzip:
        input: fqgz/sam4-rep2-lane1.fastq.gz, fqgz/sam4-rep2-lane6.fastq.gz
        output: fq/sam4-rep2.fastq
        jobid: 8
        wildcards: sample=4, replicate=2

    [Wed Oct 24 17:29:50 2018]
    Finished job 8.
    4 of 9 steps (44%) done

    [Wed Oct 24 17:29:50 2018]
    rule unzip:
        input: fqgz/sam4-rep1-lane2.fastq.gz
        output: fq/sam4-rep1.fastq
        jobid: 7
        wildcards: sample=4, replicate=1

    [Wed Oct 24 17:29:50 2018]
    Finished job 7.
    5 of 9 steps (56%) done

    [Wed Oct 24 17:29:50 2018]
    rule unzip:
        input: fqgz/sam2-rep2-lane7.fastq.gz, fqgz/sam2-rep2-lane8.fastq.gz
        output: fq/sam2-rep2.fastq
        jobid: 2
        wildcards: sample=2, replicate=2

    [Wed Oct 24 17:29:50 2018]
    Finished job 2.
    6 of 9 steps (67%) done

    [Wed Oct 24 17:29:50 2018]
    rule unzip:
        input: fqgz/sam1-rep1-lane5.fastq.gz, fqgz/sam1-rep1-lane1.fastq.gz
        output: fq/sam1-rep1.fastq
        jobid: 1
        wildcards: sample=1, replicate=1

    [Wed Oct 24 17:29:50 2018]
    Finished job 1.
    7 of 9 steps (78%) done

    [Wed Oct 24 17:29:50 2018]
    rule unzip:
        input: fqgz/sam3-rep2-lane7.fastq.gz, fqgz/sam3-rep2-lane1.fastq.gz
        output: fq/sam3-rep2.fastq
        jobid: 6
        wildcards: sample=3, replicate=2

    [Wed Oct 24 17:29:50 2018]
    Finished job 6.
    8 of 9 steps (89%) done

    [Wed Oct 24 17:29:50 2018]
    localrule all:
        input: fq/sam1-rep1.fastq, fq/sam1-rep2.fastq, fq/sam2-rep1.fastq, fq/sam2-rep2.fastq, fq/sam3-rep1.fastq, fq/sam3-rep2.fastq, fq/sam4-rep1.fastq, fq/sam4-rep2.fastq
        jobid: 0

    [Wed Oct 24 17:29:50 2018]
    Finished job 0.
    9 of 9 steps (100%) done
    Complete log: /home/jdb-work/repos/snakemake-rules/.snakemake/log/2018-10-24T172950.052096.snakemake.log

``` bash
ls 05/fq
```

    sam1-rep1.fastq
    sam1-rep2.fastq
    sam2-rep1.fastq
    sam2-rep2.fastq
    sam3-rep1.fastq
    sam3-rep2.fastq
    sam4-rep1.fastq
    sam4-rep2.fastq

``` bash
snakemake -s 05/Snakefile
```

    Building DAG of jobs...
    Nothing to be done.
    Complete log: /home/jdb-work/repos/snakemake-rules/.snakemake/log/2018-10-24T172950.502017.snakemake.log

Group on an unknown variable (generated input files)
----------------------------------------------------
