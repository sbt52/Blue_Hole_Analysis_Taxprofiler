## Command Executed
To reproduce this analysis, the following command was executed. This specifically utilizes Kraken2 for classification and Krona for visualization, while managing hardware constraints through a local config.

\`\`\`bash
nextflow run nf-core/taxprofiler \
    -profile docker \
    -c local.config \
    --input samplesheet.csv \
    --databases databases.csv \
    --outdir ./results \
    --run_kraken2 \
    --run_krona \
    --run_profile_standardisation \
    --kraken2_save_reads \
    -resume
\`\`\`

### **What these parameters do:**
| Parameter | Why we used it |
| :--- | :--- |
| `-profile docker` | Ensures all software (Kraken2, Krona, etc.) runs in a controlled "container" so results are identical on any machine. |
| `-c local.config` | **Critical:** Overrides high default memory (36GB) to fit within the Mac's 16GB RAM. |
| `--run_kraken2` | Activates the primary taxonomic classifier. |
| `--run_krona` | Generates the interactive hierarchical pie charts. |
| `--run_profile_standardisation` | Uses TAXPASTA to turn messy outputs into the standardized tables we used for the final report. |
| `--kraken2_save_reads` | Saves the actual DNA sequences that matched specific taxa for further validation. |
| `-resume` | Efficiently restarts the pipeline from the last successful step if interrupted. |
