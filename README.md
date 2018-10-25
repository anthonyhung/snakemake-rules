
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

    [Wed Oct 24 21:35:47 2018]
    rule unzip:
        input: fqgz/sam01-rep1-lane1.fastq.gz
        output: fq/sam01-rep1-lane1.fastq
        jobid: 0

    [Wed Oct 24 21:35:47 2018]
    Finished job 0.
    1 of 1 steps (100%) done
    Complete log: /home/jdb-work/repos/snakemake-rules/.snakemake/log/2018-10-24T213547.368585.snakemake.log

``` bash
ls 01/fq
```

    sam01-rep1-lane1.fastq

``` bash
snakemake -s 01/Snakefile
```

    Building DAG of jobs...
    Nothing to be done.
    Complete log: /home/jdb-work/repos/snakemake-rules/.snakemake/log/2018-10-24T213547.665335.snakemake.log

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

    [Wed Oct 24 21:35:48 2018]
    rule unzip:
        input: fqgz/sam4-rep1.fastq.gz
        output: fq/sam4-rep1.fastq
        jobid: 8
        wildcards: sample=4, replicate=1

    [Wed Oct 24 21:35:48 2018]
    Finished job 8.
    1 of 9 steps (11%) done

    [Wed Oct 24 21:35:48 2018]
    rule unzip:
        input: fqgz/sam3-rep2.fastq.gz
        output: fq/sam3-rep2.fastq
        jobid: 1
        wildcards: sample=3, replicate=2

    [Wed Oct 24 21:35:48 2018]
    Finished job 1.
    2 of 9 steps (22%) done

    [Wed Oct 24 21:35:48 2018]
    rule unzip:
        input: fqgz/sam4-rep2.fastq.gz
        output: fq/sam4-rep2.fastq
        jobid: 3
        wildcards: sample=4, replicate=2

    [Wed Oct 24 21:35:48 2018]
    Finished job 3.
    3 of 9 steps (33%) done

    [Wed Oct 24 21:35:48 2018]
    rule unzip:
        input: fqgz/sam3-rep1.fastq.gz
        output: fq/sam3-rep1.fastq
        jobid: 4
        wildcards: sample=3, replicate=1

    [Wed Oct 24 21:35:48 2018]
    Finished job 4.
    4 of 9 steps (44%) done

    [Wed Oct 24 21:35:48 2018]
    rule unzip:
        input: fqgz/sam1-rep2.fastq.gz
        output: fq/sam1-rep2.fastq
        jobid: 2
        wildcards: sample=1, replicate=2

    [Wed Oct 24 21:35:48 2018]
    Finished job 2.
    5 of 9 steps (56%) done

    [Wed Oct 24 21:35:48 2018]
    rule unzip:
        input: fqgz/sam2-rep1.fastq.gz
        output: fq/sam2-rep1.fastq
        jobid: 5
        wildcards: sample=2, replicate=1

    [Wed Oct 24 21:35:48 2018]
    Finished job 5.
    6 of 9 steps (67%) done

    [Wed Oct 24 21:35:48 2018]
    rule unzip:
        input: fqgz/sam1-rep1.fastq.gz
        output: fq/sam1-rep1.fastq
        jobid: 7
        wildcards: sample=1, replicate=1

    [Wed Oct 24 21:35:48 2018]
    Finished job 7.
    7 of 9 steps (78%) done

    [Wed Oct 24 21:35:48 2018]
    rule unzip:
        input: fqgz/sam2-rep2.fastq.gz
        output: fq/sam2-rep2.fastq
        jobid: 6
        wildcards: sample=2, replicate=2

    [Wed Oct 24 21:35:48 2018]
    Finished job 6.
    8 of 9 steps (89%) done

    [Wed Oct 24 21:35:48 2018]
    localrule all:
        input: fq/sam1-rep1.fastq, fq/sam1-rep2.fastq, fq/sam2-rep1.fastq, fq/sam2-rep2.fastq, fq/sam3-rep1.fastq, fq/sam3-rep2.fastq, fq/sam4-rep1.fastq, fq/sam4-rep2.fastq
        jobid: 0

    [Wed Oct 24 21:35:48 2018]
    Finished job 0.
    9 of 9 steps (100%) done
    Complete log: /home/jdb-work/repos/snakemake-rules/.snakemake/log/2018-10-24T213548.249929.snakemake.log

``` bash
ls 02/fq
```

    sam01-rep1-lane1.fastq

``` bash
snakemake -s 02/Snakefile
```

    Building DAG of jobs...
    Nothing to be done.
    Complete log: /home/jdb-work/repos/snakemake-rules/.snakemake/log/2018-10-24T213548.651744.snakemake.log

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

    [Wed Oct 24 21:35:49 2018]
    rule unzip:
        input: fqgz/sam2-rep2.fastq.gz
        output: fq/sam2-rep2.fastq
        jobid: 5
        wildcards: sample=2, replicate=2

    [Wed Oct 24 21:35:49 2018]
    Finished job 5.
    1 of 10 steps (10%) done

    [Wed Oct 24 21:35:49 2018]
    rule unzip:
        input: fqgz/sam1-rep1.fastq.gz
        output: fq/sam1-rep1.fastq
        jobid: 7
        wildcards: sample=1, replicate=1

    [Wed Oct 24 21:35:49 2018]
    Finished job 7.
    2 of 10 steps (20%) done

    [Wed Oct 24 21:35:49 2018]
    rule unzip:
        input: fqgz/sam3-rep1.fastq.gz
        output: fq/sam3-rep1.fastq
        jobid: 3
        wildcards: sample=3, replicate=1

    [Wed Oct 24 21:35:49 2018]
    Finished job 3.
    3 of 10 steps (30%) done

    [Wed Oct 24 21:35:49 2018]
    rule unzip:
        input: fqgz/sam3-rep2.fastq.gz
        output: fq/sam3-rep2.fastq
        jobid: 2
        wildcards: sample=3, replicate=2

    [Wed Oct 24 21:35:49 2018]
    Finished job 2.
    4 of 10 steps (40%) done

    [Wed Oct 24 21:35:49 2018]
    rule unzip:
        input: fqgz/sam2-rep1.fastq.gz
        output: fq/sam2-rep1.fastq
        jobid: 8
        wildcards: sample=2, replicate=1

    [Wed Oct 24 21:35:49 2018]
    Finished job 8.
    5 of 10 steps (50%) done

    [Wed Oct 24 21:35:49 2018]
    rule unzip:
        input: fqgz/sam1-rep2.fastq.gz
        output: fq/sam1-rep2.fastq
        jobid: 9
        wildcards: sample=1, replicate=2

    [Wed Oct 24 21:35:49 2018]
    Finished job 9.
    6 of 10 steps (60%) done

    [Wed Oct 24 21:35:49 2018]
    rule unzip:
        input: fqgz/sam4-rep1.fastq.gz
        output: fq/sam4-rep1.fastq
        jobid: 4
        wildcards: sample=4, replicate=1

    [Wed Oct 24 21:35:49 2018]
    Finished job 4.
    7 of 10 steps (70%) done

    [Wed Oct 24 21:35:49 2018]
    rule unzip:
        input: fqgz/sam4-rep2.fastq.gz
        output: fq/sam4-rep2.fastq
        jobid: 6
        wildcards: sample=4, replicate=2

    [Wed Oct 24 21:35:49 2018]
    Finished job 6.
    8 of 10 steps (80%) done

    [Wed Oct 24 21:35:49 2018]
    rule combine:
        input: fq/sam1-rep1.fastq, fq/sam1-rep2.fastq, fq/sam2-rep1.fastq, fq/sam2-rep2.fastq, fq/sam3-rep1.fastq, fq/sam3-rep2.fastq, fq/sam4-rep1.fastq, fq/sam4-rep2.fastq
        output: fq/combined.fastq
        jobid: 1

    [Wed Oct 24 21:35:49 2018]
    Finished job 1.
    9 of 10 steps (90%) done

    [Wed Oct 24 21:35:49 2018]
    localrule all:
        input: fq/combined.fastq
        jobid: 0

    [Wed Oct 24 21:35:49 2018]
    Finished job 0.
    10 of 10 steps (100%) done
    Complete log: /home/jdb-work/repos/snakemake-rules/.snakemake/log/2018-10-24T213549.410469.snakemake.log

``` bash
ls 03/fq
```

    sam01-rep1-lane1.fastq

``` bash
snakemake -s 03/Snakefile
```

    Building DAG of jobs...
    Nothing to be done.
    Complete log: /home/jdb-work/repos/snakemake-rules/.snakemake/log/2018-10-24T213549.813875.snakemake.log

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

    [Wed Oct 24 21:35:50 2018]
    rule unzip:
        input: fqgz/sam4-rep1.fastq.gz, fqgz/sam4-rep2.fastq.gz
        output: fq/sam4.fastq
        jobid: 2
        wildcards: sample=4

    [Wed Oct 24 21:35:50 2018]
    Finished job 2.
    1 of 5 steps (20%) done

    [Wed Oct 24 21:35:50 2018]
    rule unzip:
        input: fqgz/sam1-rep1.fastq.gz, fqgz/sam1-rep2.fastq.gz
        output: fq/sam1.fastq
        jobid: 4
        wildcards: sample=1

    [Wed Oct 24 21:35:50 2018]
    Finished job 4.
    2 of 5 steps (40%) done

    [Wed Oct 24 21:35:50 2018]
    rule unzip:
        input: fqgz/sam3-rep1.fastq.gz, fqgz/sam3-rep2.fastq.gz
        output: fq/sam3.fastq
        jobid: 3
        wildcards: sample=3

    [Wed Oct 24 21:35:50 2018]
    Finished job 3.
    3 of 5 steps (60%) done

    [Wed Oct 24 21:35:50 2018]
    rule unzip:
        input: fqgz/sam2-rep1.fastq.gz, fqgz/sam2-rep2.fastq.gz
        output: fq/sam2.fastq
        jobid: 1
        wildcards: sample=2

    [Wed Oct 24 21:35:50 2018]
    Finished job 1.
    4 of 5 steps (80%) done

    [Wed Oct 24 21:35:50 2018]
    localrule all:
        input: fq/sam1.fastq, fq/sam2.fastq, fq/sam3.fastq, fq/sam4.fastq
        jobid: 0

    [Wed Oct 24 21:35:50 2018]
    Finished job 0.
    5 of 5 steps (100%) done
    Complete log: /home/jdb-work/repos/snakemake-rules/.snakemake/log/2018-10-24T213550.391328.snakemake.log

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
    Complete log: /home/jdb-work/repos/snakemake-rules/.snakemake/log/2018-10-24T213550.738192.snakemake.log

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

    [Wed Oct 24 21:35:51 2018]
    rule unzip:
        input: fqgz/sam2-rep2-lane7.fastq.gz, fqgz/sam2-rep2-lane8.fastq.gz
        output: fq/sam2-rep2.fastq
        jobid: 6
        wildcards: sample=2, replicate=2

    [Wed Oct 24 21:35:51 2018]
    Finished job 6.
    1 of 9 steps (11%) done

    [Wed Oct 24 21:35:51 2018]
    rule unzip:
        input: fqgz/sam3-rep1-lane3.fastq.gz, fqgz/sam3-rep1-lane7.fastq.gz
        output: fq/sam3-rep1.fastq
        jobid: 7
        wildcards: sample=3, replicate=1

    [Wed Oct 24 21:35:51 2018]
    Finished job 7.
    2 of 9 steps (22%) done

    [Wed Oct 24 21:35:51 2018]
    rule unzip:
        input: fqgz/sam4-rep1-lane5.fastq.gz, fqgz/sam4-rep1-lane2.fastq.gz
        output: fq/sam4-rep1.fastq
        jobid: 3
        wildcards: sample=4, replicate=1

    [Wed Oct 24 21:35:51 2018]
    Finished job 3.
    3 of 9 steps (33%) done

    [Wed Oct 24 21:35:51 2018]
    rule unzip:
        input: fqgz/sam2-rep1-lane3.fastq.gz, fqgz/sam2-rep1-lane8.fastq.gz
        output: fq/sam2-rep1.fastq
        jobid: 1
        wildcards: sample=2, replicate=1

    [Wed Oct 24 21:35:51 2018]
    Finished job 1.
    4 of 9 steps (44%) done

    [Wed Oct 24 21:35:51 2018]
    rule unzip:
        input: fqgz/sam1-rep2-lane4.fastq.gz, fqgz/sam1-rep2-lane2.fastq.gz
        output: fq/sam1-rep2.fastq
        jobid: 8
        wildcards: sample=1, replicate=2

    [Wed Oct 24 21:35:51 2018]
    Finished job 8.
    5 of 9 steps (56%) done

    [Wed Oct 24 21:35:51 2018]
    rule unzip:
        input: fqgz/sam3-rep2-lane7.fastq.gz, fqgz/sam3-rep2-lane1.fastq.gz
        output: fq/sam3-rep2.fastq
        jobid: 5
        wildcards: sample=3, replicate=2

    [Wed Oct 24 21:35:51 2018]
    Finished job 5.
    6 of 9 steps (67%) done

    [Wed Oct 24 21:35:51 2018]
    rule unzip:
        input: fqgz/sam4-rep2-lane1.fastq.gz, fqgz/sam4-rep2-lane6.fastq.gz
        output: fq/sam4-rep2.fastq
        jobid: 2
        wildcards: sample=4, replicate=2

    [Wed Oct 24 21:35:51 2018]
    Finished job 2.
    7 of 9 steps (78%) done

    [Wed Oct 24 21:35:51 2018]
    rule unzip:
        input: fqgz/sam1-rep1-lane5.fastq.gz, fqgz/sam1-rep1-lane1.fastq.gz
        output: fq/sam1-rep1.fastq
        jobid: 4
        wildcards: sample=1, replicate=1

    [Wed Oct 24 21:35:51 2018]
    Finished job 4.
    8 of 9 steps (89%) done

    [Wed Oct 24 21:35:51 2018]
    localrule all:
        input: fq/sam1-rep1.fastq, fq/sam1-rep2.fastq, fq/sam2-rep1.fastq, fq/sam2-rep2.fastq, fq/sam3-rep1.fastq, fq/sam3-rep2.fastq, fq/sam4-rep1.fastq, fq/sam4-rep2.fastq
        jobid: 0

    [Wed Oct 24 21:35:51 2018]
    Finished job 0.
    9 of 9 steps (100%) done
    Complete log: /home/jdb-work/repos/snakemake-rules/.snakemake/log/2018-10-24T213551.361153.snakemake.log

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
    Complete log: /home/jdb-work/repos/snakemake-rules/.snakemake/log/2018-10-24T213551.793075.snakemake.log

Group on an unknown variable (generated input files)
----------------------------------------------------

``` bash
bash 06/setup.sh
ls 06/fqgz
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
    sam4-rep1-lane5.fastq.gz
    sam4-rep2-lane1.fastq.gz
    sam4-rep2-lane6.fastq.gz

![dag](06/06.png)

``` bash
snakemake -s 06/Snakefile
```

    Building DAG of jobs...
    Using shell: /bin/bash
    Provided cores: 1
    Rules claiming more threads will be scaled down.
    Job counts:
        count   jobs
        1   all
        8   group
        16  unzip
        25

    [Wed Oct 24 21:35:52 2018]
    rule unzip:
        input: fqgz/sam1-rep1-lane1.fastq.gz
        output: fq/sam1-rep1-lane1.fastq
        jobid: 24
        wildcards: filename=sam1-rep1-lane1

    [Wed Oct 24 21:35:52 2018]
    Finished job 24.
    1 of 25 steps (4%) done

    [Wed Oct 24 21:35:52 2018]
    rule unzip:
        input: fqgz/sam2-rep2-lane8.fastq.gz
        output: fq/sam2-rep2-lane8.fastq
        jobid: 20
        wildcards: filename=sam2-rep2-lane8

    [Wed Oct 24 21:35:52 2018]
    Finished job 20.
    2 of 25 steps (8%) done

    [Wed Oct 24 21:35:52 2018]
    rule unzip:
        input: fqgz/sam3-rep2-lane7.fastq.gz
        output: fq/sam3-rep2-lane7.fastq
        jobid: 12
        wildcards: filename=sam3-rep2-lane7

    [Wed Oct 24 21:35:52 2018]
    Finished job 12.
    3 of 25 steps (12%) done

    [Wed Oct 24 21:35:52 2018]
    rule unzip:
        input: fqgz/sam4-rep2-lane6.fastq.gz
        output: fq/sam4-rep2-lane6.fastq
        jobid: 9
        wildcards: filename=sam4-rep2-lane6

    [Wed Oct 24 21:35:52 2018]
    Finished job 9.
    4 of 25 steps (16%) done

    [Wed Oct 24 21:35:52 2018]
    rule unzip:
        input: fqgz/sam2-rep1-lane3.fastq.gz
        output: fq/sam2-rep1-lane3.fastq
        jobid: 21
        wildcards: filename=sam2-rep1-lane3

    [Wed Oct 24 21:35:52 2018]
    Finished job 21.
    5 of 25 steps (20%) done

    [Wed Oct 24 21:35:52 2018]
    rule unzip:
        input: fqgz/sam4-rep2-lane1.fastq.gz
        output: fq/sam4-rep2-lane1.fastq
        jobid: 10
        wildcards: filename=sam4-rep2-lane1

    [Wed Oct 24 21:35:52 2018]
    Finished job 10.
    6 of 25 steps (24%) done

    [Wed Oct 24 21:35:52 2018]
    rule group:
        input: fq/sam4-rep2-lane1.fastq, fq/sam4-rep2-lane6.fastq
        output: fq-group/sam4-rep2.fastq
        jobid: 1
        wildcards: sample=4, replicate=2

    [Wed Oct 24 21:35:52 2018]
    Finished job 1.
    7 of 25 steps (28%) done

    [Wed Oct 24 21:35:52 2018]
    rule unzip:
        input: fqgz/sam1-rep2-lane2.fastq.gz
        output: fq/sam1-rep2-lane2.fastq
        jobid: 16
        wildcards: filename=sam1-rep2-lane2

    [Wed Oct 24 21:35:52 2018]
    Finished job 16.
    8 of 25 steps (32%) done

    [Wed Oct 24 21:35:52 2018]
    rule unzip:
        input: fqgz/sam1-rep1-lane5.fastq.gz
        output: fq/sam1-rep1-lane5.fastq
        jobid: 23
        wildcards: filename=sam1-rep1-lane5

    [Wed Oct 24 21:35:52 2018]
    Finished job 23.
    9 of 25 steps (36%) done

    [Wed Oct 24 21:35:52 2018]
    rule group:
        input: fq/sam1-rep1-lane5.fastq, fq/sam1-rep1-lane1.fastq
        output: fq-group/sam1-rep1.fastq
        jobid: 8
        wildcards: sample=1, replicate=1

    [Wed Oct 24 21:35:52 2018]
    Finished job 8.
    10 of 25 steps (40%) done

    [Wed Oct 24 21:35:53 2018]
    rule unzip:
        input: fqgz/sam3-rep2-lane1.fastq.gz
        output: fq/sam3-rep2-lane1.fastq
        jobid: 11
        wildcards: filename=sam3-rep2-lane1

    [Wed Oct 24 21:35:53 2018]
    Finished job 11.
    11 of 25 steps (44%) done

    [Wed Oct 24 21:35:53 2018]
    rule group:
        input: fq/sam3-rep2-lane7.fastq, fq/sam3-rep2-lane1.fastq
        output: fq-group/sam3-rep2.fastq
        jobid: 2
        wildcards: sample=3, replicate=2

    [Wed Oct 24 21:35:53 2018]
    Finished job 2.
    12 of 25 steps (48%) done

    [Wed Oct 24 21:35:53 2018]
    rule unzip:
        input: fqgz/sam4-rep1-lane5.fastq.gz
        output: fq/sam4-rep1-lane5.fastq
        jobid: 13
        wildcards: filename=sam4-rep1-lane5

    [Wed Oct 24 21:35:53 2018]
    Finished job 13.
    13 of 25 steps (52%) done

    [Wed Oct 24 21:35:53 2018]
    rule unzip:
        input: fqgz/sam3-rep1-lane3.fastq.gz
        output: fq/sam3-rep1-lane3.fastq
        jobid: 17
        wildcards: filename=sam3-rep1-lane3

    [Wed Oct 24 21:35:53 2018]
    Finished job 17.
    14 of 25 steps (56%) done

    [Wed Oct 24 21:35:53 2018]
    rule unzip:
        input: fqgz/sam3-rep1-lane7.fastq.gz
        output: fq/sam3-rep1-lane7.fastq
        jobid: 18
        wildcards: filename=sam3-rep1-lane7

    [Wed Oct 24 21:35:53 2018]
    Finished job 18.
    15 of 25 steps (60%) done

    [Wed Oct 24 21:35:53 2018]
    rule group:
        input: fq/sam3-rep1-lane3.fastq, fq/sam3-rep1-lane7.fastq
        output: fq-group/sam3-rep1.fastq
        jobid: 5
        wildcards: sample=3, replicate=1

    [Wed Oct 24 21:35:53 2018]
    Finished job 5.
    16 of 25 steps (64%) done

    [Wed Oct 24 21:35:53 2018]
    rule unzip:
        input: fqgz/sam1-rep2-lane4.fastq.gz
        output: fq/sam1-rep2-lane4.fastq
        jobid: 15
        wildcards: filename=sam1-rep2-lane4

    [Wed Oct 24 21:35:53 2018]
    Finished job 15.
    17 of 25 steps (68%) done

    [Wed Oct 24 21:35:53 2018]
    rule group:
        input: fq/sam1-rep2-lane4.fastq, fq/sam1-rep2-lane2.fastq
        output: fq-group/sam1-rep2.fastq
        jobid: 4
        wildcards: sample=1, replicate=2

    [Wed Oct 24 21:35:53 2018]
    Finished job 4.
    18 of 25 steps (72%) done

    [Wed Oct 24 21:35:53 2018]
    rule unzip:
        input: fqgz/sam2-rep1-lane8.fastq.gz
        output: fq/sam2-rep1-lane8.fastq
        jobid: 22
        wildcards: filename=sam2-rep1-lane8

    [Wed Oct 24 21:35:53 2018]
    Finished job 22.
    19 of 25 steps (76%) done

    [Wed Oct 24 21:35:53 2018]
    rule group:
        input: fq/sam2-rep1-lane3.fastq, fq/sam2-rep1-lane8.fastq
        output: fq-group/sam2-rep1.fastq
        jobid: 7
        wildcards: sample=2, replicate=1

    [Wed Oct 24 21:35:53 2018]
    Finished job 7.
    20 of 25 steps (80%) done

    [Wed Oct 24 21:35:54 2018]
    rule unzip:
        input: fqgz/sam2-rep2-lane7.fastq.gz
        output: fq/sam2-rep2-lane7.fastq
        jobid: 19
        wildcards: filename=sam2-rep2-lane7

    [Wed Oct 24 21:35:54 2018]
    Finished job 19.
    21 of 25 steps (84%) done

    [Wed Oct 24 21:35:54 2018]
    rule group:
        input: fq/sam2-rep2-lane7.fastq, fq/sam2-rep2-lane8.fastq
        output: fq-group/sam2-rep2.fastq
        jobid: 6
        wildcards: sample=2, replicate=2

    [Wed Oct 24 21:35:54 2018]
    Finished job 6.
    22 of 25 steps (88%) done

    [Wed Oct 24 21:35:54 2018]
    rule unzip:
        input: fqgz/sam4-rep1-lane2.fastq.gz
        output: fq/sam4-rep1-lane2.fastq
        jobid: 14
        wildcards: filename=sam4-rep1-lane2

    [Wed Oct 24 21:35:54 2018]
    Finished job 14.
    23 of 25 steps (92%) done

    [Wed Oct 24 21:35:54 2018]
    rule group:
        input: fq/sam4-rep1-lane5.fastq, fq/sam4-rep1-lane2.fastq
        output: fq-group/sam4-rep1.fastq
        jobid: 3
        wildcards: sample=4, replicate=1

    [Wed Oct 24 21:35:54 2018]
    Finished job 3.
    24 of 25 steps (96%) done

    [Wed Oct 24 21:35:54 2018]
    localrule all:
        input: fq-group/sam1-rep1.fastq, fq-group/sam1-rep2.fastq, fq-group/sam2-rep1.fastq, fq-group/sam2-rep2.fastq, fq-group/sam3-rep1.fastq, fq-group/sam3-rep2.fastq, fq-group/sam4-rep1.fastq, fq-group/sam4-rep2.fastq
        jobid: 0

    [Wed Oct 24 21:35:54 2018]
    Finished job 0.
    25 of 25 steps (100%) done
    Complete log: /home/jdb-work/repos/snakemake-rules/.snakemake/log/2018-10-24T213552.631318.snakemake.log

``` bash
ls 06/fq-group
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
snakemake -s 06/Snakefile
```

    Building DAG of jobs...
    Nothing to be done.
    Complete log: /home/jdb-work/repos/snakemake-rules/.snakemake/log/2018-10-24T213555.092257.snakemake.log
