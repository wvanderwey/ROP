To extract the transcript names from gtf

awk -F "transcript_id" '{print $2}' genes.gtf | awk -F "transcript_name" '{print $1}' | sed 's/"//g' | sed 's/;//' >transcripts.txt
