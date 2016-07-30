This is internal document. Use it in case you are planing to prepare gene annotations for a new organism. Note human and mouse annotations are already prepared. 

To extract the transcript names from gtf:

```
awk -F "transcript_id" '{print $2}' genes.gtf | awk -F "transcript_name" '{print $1}' | sed 's/"//g' | sed 's/;//' >transcripts.txt
```

To extract gene names from gtf:

```
awk -F "gene_id" '{print $2}' genes.gtf | awk -F "gene_name" '{print $1}' | sed 's/"//g' | sed 's/;//' >genes.txt
```

Merge them into a single file:

```
paste genes.txt transcripts.txt | awk '{print $1","$2}' >genes_transcripts.txt
```