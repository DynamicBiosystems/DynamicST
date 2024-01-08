### DynamicST introduction

---

DynamicST is a set of analysis pipelines that process DynaSpatail data with brightfield images. DynamicST allows users to map the whole transcriptome in  fresh frozen (FF) tissues.

### Install DynamicST 1.0.0

----

Dowload DynamicST from [here](https://github.com/DynamicBiosystems/DynamicEX/releases/tag/v1.0.0).

```shell
# download DynamicST.tar.gz

mkdir DynamicST

tar -zxf DynamicST.tar.gz -C DynamicST

Prepend the DynamicST directory to your $PATH. This will allow you to invoke the DynamicST command.
```

### Manual

---

#### params

---

- mkref
  - --forceall: Force the execution of the selected (or the first) rule and all rules it is dependent on regardless of already created output.
  - --dryrun : Do not execute anything, and display what would be done. If you have a very large workflow, use --dryrun --quiet to just print a summary of the DAG of jobs.
  - --genomeName: output dir, used to build genome
  - --fasta: path to FASTA file containing your genome reference
  - --gtf: Path to genes GTF file containing annotated genes for your genome reference
  - --threads: Number of threads used during STAR genome index generation. Defaults to 8
- count
  - --sample: Sample name of each batch,required
  - --id: Final sample name,required
  - --inputdir: raw data path,required
  - --image: Single H&E brightfield image
  - --CBcoordinate: Barcode coordinate file for automatic tissue detection
  - --alignment: Alignment file produced by the manual alignment step
  - --gtf: genome annotation file,required
  - --transcriptome: Path of folder containing transcriptome reference,required
  - --outputdir: output file name,default ./
  - --CBposition: position of Cell Barcode(s) on the barcode read(0-base).default:0_0_0_7 0_38_0_45
  - --UMIposition: position of the UMI on the barcode read, same as CBposition(0-base).default:0_46_0_57
  - --cores: set max cores the pipeline may request at one time.;default 16


#### Quick start

---

- mkref

```shell
wget ftp://ftp.ensembl.org/pub/release-99/fasta/homo_sapiens/dna/Homo_sapiens.GRCh38.dna.primary_assembly.fa.gz
wget ftp://ftp.ensembl.org/pub/release-99/gtf/homo_sapiens/Homo_sapiens.GRCh38.99.gtf.gz

gunzip Homo_sapiens.GRCh38.dna.primary_assembly.fa.gz
gunzip Homo_sapiens.GRCh38.99.gtf.gz

DynamicST mkref \
 --genome_name Homo_sapiens_GRCh38 \
 --fasta Homo_sapiens.GRCh38.dna.primary_assembly.fa \
 --gtf Homo_sapiens.GRCh38.99.gtf
```

- count

```shell
#The input folder must contain fastq files, with the same file format as sampleName_S1_L001_R1_001.fastq.gz
DynamicST count --sample sampleName --id sampleName --inputdir rawdata/ --gtf Homo_sapiens.GRCh38.99.gtf --transcriptome Homo_sapiens_GRCh38  --image HE.tif --CBcoordinate barcode_coordinate.txt --alignment alignment.json --outputdir result
```

The detailed documentation of the web_summary.html in the results can be found at [summary](https://github.com/DynamicBiosystems/DynamicEX/blob/main/doc/web_summary.md).

### About

---

DynamicST is developed by dynamic-biosystems Co., Ltd. The official website is [www.dynamic-biosystems](http://www.dynamic-biosystems.com/).





