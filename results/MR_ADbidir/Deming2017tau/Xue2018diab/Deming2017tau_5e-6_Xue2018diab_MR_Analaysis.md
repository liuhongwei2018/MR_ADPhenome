---
title: "Mendelian Randomization Analysis"
author: "Dr. Shea Andrews"
date: "2020-09-27"
output:
  html_document:
    df_print: paged
    keep_md: true
    toc: true
    number_sections: false
    toc_depth: 4
    toc_float:
      collapsed: false
      smooth_scroll: false
params:
  rwd: NA
  exposure.code: NA
  Exposure: NA
  exposure.snps: NA
  outcome.code: NA
  Outcome: NA
  outcome.snps: NA
  proxy.snps: NA
  harmonized.dat: NA
  p.threshold: NA
  r2.threshold: NA
  kb.threshold: NA
  mrpresso_global: NA
  mrpresso_global_wo_outliers: NA
  power: NA
  out: NA
editor_options:
  chunk_output_type: console
---






## Instrumental Variables
**SNP Inclusion:** SNPS associated with at a p-value threshold of p < 5e-6 were included in this analysis.
<br>

**LD Clumping:** For standard two sample MR it is important to ensure that the instruments for the exposure are independent. LD clumping was performed in PLINK using the EUR samples from the 1000 Genomes Project to estimate LD between SNPs, and, amongst SNPs that have an LD above a given threshold, retain only the SNP with the lowest p-value. A clumping window of 10^{4}, r2 of 0.001 and significance level of 1 was used for the index and secondary SNPs.
<br>

**Proxy SNPs:** Where SNPs were not available in the outcome GWAS, the EUR thousand genomes was queried to identify potential proxy SNPs that are in linkage disequilibrium (r2 > 0.8) of the missing SNP.
<br>

### Exposure: CSF Tau
`#r exposure.blurb`
<br>

**Table 1:** Independent SNPs associated with CSF Tau
<div data-pagedtable="false">
  <script data-pagedtable-source type="application/json">
{"columns":[{"label":["SNP"],"name":[1],"type":["chr"],"align":["left"]},{"label":["CHROM"],"name":[2],"type":["dbl"],"align":["right"]},{"label":["POS"],"name":[3],"type":["dbl"],"align":["right"]},{"label":["REF"],"name":[4],"type":["chr"],"align":["left"]},{"label":["ALT"],"name":[5],"type":["chr"],"align":["left"]},{"label":["AF"],"name":[6],"type":["dbl"],"align":["right"]},{"label":["BETA"],"name":[7],"type":["dbl"],"align":["right"]},{"label":["SE"],"name":[8],"type":["dbl"],"align":["right"]},{"label":["Z"],"name":[9],"type":["dbl"],"align":["right"]},{"label":["P"],"name":[10],"type":["dbl"],"align":["right"]},{"label":["N"],"name":[11],"type":["dbl"],"align":["right"]},{"label":["TRAIT"],"name":[12],"type":["chr"],"align":["left"]}],"data":[{"1":"rs10800664","2":"1","3":"199959856","4":"C","5":"T","6":"0.4182820","7":"-0.02591","8":"0.005653","9":"-4.583407","10":"4.770e-06","11":"3146","12":"CSF_tau"},{"1":"rs4674842","2":"2","3":"224880514","4":"T","5":"G","6":"0.3079300","7":"-0.03081","8":"0.006491","9":"-4.746572","10":"2.158e-06","11":"3146","12":"CSF_tau"},{"1":"rs35055419","2":"3","3":"190663557","4":"T","5":"C","6":"0.3498150","7":"0.04004","8":"0.006006","9":"6.666667","10":"3.071e-11","11":"3146","12":"CSF_tau"},{"1":"rs7737716","2":"5","3":"118217474","4":"C","5":"T","6":"0.1334780","7":"0.04066","8":"0.008535","9":"4.763913","10":"1.984e-06","11":"3146","12":"CSF_tau"},{"1":"rs13255475","2":"8","3":"121468076","4":"T","5":"C","6":"0.6631540","7":"0.02793","8":"0.006049","9":"4.617290","10":"4.032e-06","11":"3146","12":"CSF_tau"},{"1":"rs624290","2":"9","3":"3928115","4":"C","5":"T","6":"0.8932200","7":"0.04421","8":"0.009094","9":"4.861450","10":"1.223e-06","11":"3146","12":"CSF_tau"},{"1":"rs769449","2":"19","3":"45410002","4":"G","5":"A","6":"0.0998545","7":"0.07821","8":"0.006911","9":"11.316741","10":"4.054e-29","11":"3146","12":"CSF_tau"},{"1":"rs1513737","2":"21","3":"24166144","4":"T","5":"C","6":"0.5373410","7":"-0.02597","8":"0.005620","9":"-4.621000","10":"3.986e-06","11":"3146","12":"CSF_tau"}],"options":{"columns":{"min":{},"max":[10]},"rows":{"min":[10],"max":[10]},"pages":{}}}
  </script>
</div>
<br>

### Outcome: Diabetes
`#r outcome.blurb`
<br>

**Table 2:** SNPs associated with CSF Tau avaliable in Diabetes
<div data-pagedtable="false">
  <script data-pagedtable-source type="application/json">
{"columns":[{"label":["SNP"],"name":[1],"type":["chr"],"align":["left"]},{"label":["CHROM"],"name":[2],"type":["dbl"],"align":["right"]},{"label":["POS"],"name":[3],"type":["dbl"],"align":["right"]},{"label":["REF"],"name":[4],"type":["chr"],"align":["left"]},{"label":["ALT"],"name":[5],"type":["chr"],"align":["left"]},{"label":["AF"],"name":[6],"type":["dbl"],"align":["right"]},{"label":["BETA"],"name":[7],"type":["dbl"],"align":["right"]},{"label":["SE"],"name":[8],"type":["dbl"],"align":["right"]},{"label":["Z"],"name":[9],"type":["dbl"],"align":["right"]},{"label":["P"],"name":[10],"type":["dbl"],"align":["right"]},{"label":["N"],"name":[11],"type":["dbl"],"align":["right"]},{"label":["TRAIT"],"name":[12],"type":["chr"],"align":["left"]}],"data":[{"1":"rs10800664","2":"1","3":"199959856","4":"C","5":"T","6":"0.492766","7":"-0.0328","8":"0.0079","9":"-4.1518987","10":"2.965e-05","11":"565271","12":"Type_2_Diabetes"},{"1":"rs4674842","2":"2","3":"224880514","4":"T","5":"G","6":"0.237768","7":"0.0088","8":"0.0092","9":"0.9565217","10":"3.385e-01","11":"572983","12":"Type_2_Diabetes"},{"1":"rs35055419","2":"3","3":"190663557","4":"T","5":"C","6":"0.378476","7":"0.0202","8":"0.0081","9":"2.4938272","10":"1.238e-02","11":"569270","12":"Type_2_Diabetes"},{"1":"rs7737716","2":"5","3":"118217474","4":"C","5":"T","6":"0.126496","7":"-0.0134","8":"0.0119","9":"-1.1260504","10":"2.590e-01","11":"571512","12":"Type_2_Diabetes"},{"1":"rs13255475","2":"8","3":"121468076","4":"T","5":"C","6":"0.686711","7":"0.0025","8":"0.0084","9":"0.2976190","10":"7.640e-01","11":"572914","12":"Type_2_Diabetes"},{"1":"rs624290","2":"9","3":"3928115","4":"C","5":"T","6":"0.907185","7":"-0.0239","8":"0.0135","9":"-1.7703700","10":"7.569e-02","11":"573704","12":"Type_2_Diabetes"},{"1":"rs769449","2":"NA","3":"NA","4":"NA","5":"NA","6":"NA","7":"NA","8":"NA","9":"NA","10":"NA","11":"NA","12":"NA"},{"1":"rs1513737","2":"NA","3":"NA","4":"NA","5":"NA","6":"NA","7":"NA","8":"NA","9":"NA","10":"NA","11":"NA","12":"NA"}],"options":{"columns":{"min":{},"max":[10]},"rows":{"min":[10],"max":[10]},"pages":{}}}
  </script>
</div>
<br>

**Table 3:** Proxy SNPs for Diabetes
<div data-pagedtable="false">
  <script data-pagedtable-source type="application/json">
{"columns":[{"label":["proxy.outcome"],"name":[1],"type":["lgl"],"align":["right"]},{"label":["target_snp"],"name":[2],"type":["chr"],"align":["left"]},{"label":["proxy_snp"],"name":[3],"type":["lgl"],"align":["right"]},{"label":["ld.r2"],"name":[4],"type":["lgl"],"align":["right"]},{"label":["Dprime"],"name":[5],"type":["lgl"],"align":["right"]},{"label":["ref.proxy"],"name":[6],"type":["lgl"],"align":["right"]},{"label":["alt.proxy"],"name":[7],"type":["lgl"],"align":["right"]},{"label":["CHROM"],"name":[8],"type":["lgl"],"align":["right"]},{"label":["POS"],"name":[9],"type":["lgl"],"align":["right"]},{"label":["ALT.proxy"],"name":[10],"type":["lgl"],"align":["right"]},{"label":["REF.proxy"],"name":[11],"type":["lgl"],"align":["right"]},{"label":["AF"],"name":[12],"type":["lgl"],"align":["right"]},{"label":["BETA"],"name":[13],"type":["lgl"],"align":["right"]},{"label":["SE"],"name":[14],"type":["lgl"],"align":["right"]},{"label":["P"],"name":[15],"type":["lgl"],"align":["right"]},{"label":["N"],"name":[16],"type":["lgl"],"align":["right"]},{"label":["ref"],"name":[17],"type":["lgl"],"align":["right"]},{"label":["alt"],"name":[18],"type":["lgl"],"align":["right"]},{"label":["ALT"],"name":[19],"type":["lgl"],"align":["right"]},{"label":["REF"],"name":[20],"type":["lgl"],"align":["right"]},{"label":["PHASE"],"name":[21],"type":["lgl"],"align":["right"]}],"data":[{"1":"NA","2":"rs769449","3":"NA","4":"NA","5":"NA","6":"NA","7":"NA","8":"NA","9":"NA","10":"NA","11":"NA","12":"NA","13":"NA","14":"NA","15":"NA","16":"NA","17":"NA","18":"NA","19":"NA","20":"NA","21":"NA"},{"1":"NA","2":"rs1513737","3":"NA","4":"NA","5":"NA","6":"NA","7":"NA","8":"NA","9":"NA","10":"NA","11":"NA","12":"NA","13":"NA","14":"NA","15":"NA","16":"NA","17":"NA","18":"NA","19":"NA","20":"NA","21":"NA"}],"options":{"columns":{"min":{},"max":[10]},"rows":{"min":[10],"max":[10]},"pages":{}}}
  </script>
</div>
<br>

## Data harmonization
Harmonize the exposure and outcome datasets so that the effect of a SNP on the exposure and the effect of that SNP on the outcome correspond to the same allele. The harmonise_data function from the TwoSampleMR package can be used to perform the harmonization step, by default it try's to infer the forward strand alleles using allele frequency information.
<br>

**Table 4:** Harmonized CSF Tau and Diabetes datasets
<div data-pagedtable="false">
  <script data-pagedtable-source type="application/json">
{"columns":[{"label":["SNP"],"name":[1],"type":["chr"],"align":["left"]},{"label":["effect_allele.exposure"],"name":[2],"type":["chr"],"align":["left"]},{"label":["other_allele.exposure"],"name":[3],"type":["chr"],"align":["left"]},{"label":["effect_allele.outcome"],"name":[4],"type":["chr"],"align":["left"]},{"label":["other_allele.outcome"],"name":[5],"type":["chr"],"align":["left"]},{"label":["beta.exposure"],"name":[6],"type":["dbl"],"align":["right"]},{"label":["beta.outcome"],"name":[7],"type":["dbl"],"align":["right"]},{"label":["eaf.exposure"],"name":[8],"type":["dbl"],"align":["right"]},{"label":["eaf.outcome"],"name":[9],"type":["dbl"],"align":["right"]},{"label":["remove"],"name":[10],"type":["lgl"],"align":["right"]},{"label":["palindromic"],"name":[11],"type":["lgl"],"align":["right"]},{"label":["ambiguous"],"name":[12],"type":["lgl"],"align":["right"]},{"label":["id.outcome"],"name":[13],"type":["chr"],"align":["left"]},{"label":["chr.outcome"],"name":[14],"type":["dbl"],"align":["right"]},{"label":["pos.outcome"],"name":[15],"type":["dbl"],"align":["right"]},{"label":["se.outcome"],"name":[16],"type":["dbl"],"align":["right"]},{"label":["z.outcome"],"name":[17],"type":["dbl"],"align":["right"]},{"label":["pval.outcome"],"name":[18],"type":["dbl"],"align":["right"]},{"label":["samplesize.outcome"],"name":[19],"type":["dbl"],"align":["right"]},{"label":["outcome"],"name":[20],"type":["chr"],"align":["left"]},{"label":["mr_keep.outcome"],"name":[21],"type":["lgl"],"align":["right"]},{"label":["pval_origin.outcome"],"name":[22],"type":["chr"],"align":["left"]},{"label":["chr.exposure"],"name":[23],"type":["dbl"],"align":["right"]},{"label":["pos.exposure"],"name":[24],"type":["dbl"],"align":["right"]},{"label":["se.exposure"],"name":[25],"type":["dbl"],"align":["right"]},{"label":["z.exposure"],"name":[26],"type":["dbl"],"align":["right"]},{"label":["pval.exposure"],"name":[27],"type":["dbl"],"align":["right"]},{"label":["samplesize.exposure"],"name":[28],"type":["dbl"],"align":["right"]},{"label":["exposure"],"name":[29],"type":["chr"],"align":["left"]},{"label":["mr_keep.exposure"],"name":[30],"type":["lgl"],"align":["right"]},{"label":["pval_origin.exposure"],"name":[31],"type":["chr"],"align":["left"]},{"label":["id.exposure"],"name":[32],"type":["chr"],"align":["left"]},{"label":["action"],"name":[33],"type":["dbl"],"align":["right"]},{"label":["mr_keep"],"name":[34],"type":["lgl"],"align":["right"]},{"label":["pt"],"name":[35],"type":["dbl"],"align":["right"]},{"label":["pleitropy_keep"],"name":[36],"type":["lgl"],"align":["right"]},{"label":["mrpresso_RSSobs"],"name":[37],"type":["dbl"],"align":["right"]},{"label":["mrpresso_pval"],"name":[38],"type":["dbl"],"align":["right"]},{"label":["mrpresso_keep"],"name":[39],"type":["lgl"],"align":["right"]}],"data":[{"1":"rs10800664","2":"T","3":"C","4":"T","5":"C","6":"-0.02591","7":"-0.0328","8":"0.418282","9":"0.492766","10":"FALSE","11":"FALSE","12":"FALSE","13":"qsrNdA","14":"1","15":"199959856","16":"0.0079","17":"-4.1518987","18":"2.965e-05","19":"565271","20":"Xue2018diab","21":"TRUE","22":"reported","23":"1","24":"199959856","25":"0.005653","26":"-4.583407","27":"4.770e-06","28":"3146","29":"Deming2017tau","30":"TRUE","31":"reported","32":"VQ4LV8","33":"2","34":"TRUE","35":"5e-06","36":"TRUE","37":"1.064344e-03","38":"0.0006","39":"FALSE"},{"1":"rs13255475","2":"C","3":"T","4":"C","5":"T","6":"0.02793","7":"0.0025","8":"0.663154","9":"0.686711","10":"FALSE","11":"FALSE","12":"FALSE","13":"qsrNdA","14":"8","15":"121468076","16":"0.0084","17":"0.2976190","18":"7.640e-01","19":"572914","20":"Xue2018diab","21":"TRUE","22":"reported","23":"8","24":"121468076","25":"0.006049","26":"4.617290","27":"4.032e-06","28":"3146","29":"Deming2017tau","30":"TRUE","31":"reported","32":"VQ4LV8","33":"2","34":"TRUE","35":"5e-06","36":"TRUE","37":"7.930193e-06","38":"1.0000","39":"TRUE"},{"1":"rs35055419","2":"C","3":"T","4":"C","5":"T","6":"0.04004","7":"0.0202","8":"0.349815","9":"0.378476","10":"FALSE","11":"FALSE","12":"FALSE","13":"qsrNdA","14":"3","15":"190663557","16":"0.0081","17":"2.4938272","18":"1.238e-02","19":"569270","20":"Xue2018diab","21":"TRUE","22":"reported","23":"3","24":"190663557","25":"0.006006","26":"6.666667","27":"3.071e-11","28":"3146","29":"Deming2017tau","30":"TRUE","31":"reported","32":"VQ4LV8","33":"2","34":"TRUE","35":"5e-06","36":"TRUE","37":"3.583371e-04","38":"0.3318","39":"TRUE"},{"1":"rs4674842","2":"G","3":"T","4":"G","5":"T","6":"-0.03081","7":"0.0088","8":"0.307930","9":"0.237768","10":"FALSE","11":"FALSE","12":"FALSE","13":"qsrNdA","14":"2","15":"224880514","16":"0.0092","17":"0.9565217","18":"3.385e-01","19":"572983","20":"Xue2018diab","21":"TRUE","22":"reported","23":"2","24":"224880514","25":"0.006491","26":"-4.746572","27":"2.158e-06","28":"3146","29":"Deming2017tau","30":"TRUE","31":"reported","32":"VQ4LV8","33":"2","34":"TRUE","35":"5e-06","36":"TRUE","37":"2.742241e-04","38":"0.4854","39":"TRUE"},{"1":"rs624290","2":"T","3":"C","4":"T","5":"C","6":"0.04421","7":"-0.0239","8":"0.893220","9":"0.907185","10":"FALSE","11":"FALSE","12":"FALSE","13":"qsrNdA","14":"9","15":"3928115","16":"0.0135","17":"-1.7703700","18":"7.569e-02","19":"573704","20":"Xue2018diab","21":"TRUE","22":"reported","23":"9","24":"3928115","25":"0.009094","26":"4.861450","27":"1.223e-06","28":"3146","29":"Deming2017tau","30":"TRUE","31":"reported","32":"VQ4LV8","33":"2","34":"TRUE","35":"5e-06","36":"TRUE","37":"1.340621e-03","38":"0.0870","39":"TRUE"},{"1":"rs7737716","2":"T","3":"C","4":"T","5":"C","6":"0.04066","7":"-0.0134","8":"0.133478","9":"0.126496","10":"FALSE","11":"FALSE","12":"FALSE","13":"qsrNdA","14":"5","15":"118217474","16":"0.0119","17":"-1.1260504","18":"2.590e-01","19":"571512","20":"Xue2018diab","21":"TRUE","22":"reported","23":"5","24":"118217474","25":"0.008535","26":"4.763913","27":"1.984e-06","28":"3146","29":"Deming2017tau","30":"TRUE","31":"reported","32":"VQ4LV8","33":"2","34":"TRUE","35":"5e-06","36":"TRUE","37":"5.805024e-04","38":"0.3246","39":"TRUE"}],"options":{"columns":{"min":{},"max":[10]},"rows":{"min":[10],"max":[10]},"pages":{}}}
  </script>
</div>
<br>

SNPs that genome-wide significant in the outcome GWAS are likely pleitorpic and should be removed from analysis. Additionaly remove variants within the APOE locus by exclude variants 1MB either side of APOE e4 (rs429358 = 19:45411941, GRCh37.p13)
<br>


**Table 5:** SNPs that were genome-wide significant in the Diabetes GWAS
<div data-pagedtable="false">
  <script data-pagedtable-source type="application/json">
{"columns":[{"label":["SNP"],"name":[1],"type":["chr"],"align":["left"]},{"label":["chr.outcome"],"name":[2],"type":["dbl"],"align":["right"]},{"label":["pos.outcome"],"name":[3],"type":["dbl"],"align":["right"]},{"label":["pval.exposure"],"name":[4],"type":["dbl"],"align":["right"]},{"label":["pval.outcome"],"name":[5],"type":["dbl"],"align":["right"]}],"data":[],"options":{"columns":{"min":{},"max":[10]},"rows":{"min":[10],"max":[10]},"pages":{}}}
  </script>
</div>
<br>


## Instrument Strength
To ensure that the first assumption of MR is not violated (Non-zero effect assumption), the genetic variants selected should be robustly associated with the exposure. Weak instruments, where the variance in the exposure explained by the the instruments is a small portion of the total variance, may result in poor precission and accuracy of the causal effect estiamte. The strength of an instrument can be evaluated using the F statistic, if F is less than 10, this is an indication of weak instrument.


```
## Parsed with column specification:
## cols(
##   .default = col_double(),
##   exposure = col_character(),
##   outcome = col_character(),
##   method = col_character(),
##   outliers_removed = col_logical(),
##   logistic = col_logical(),
##   beta = col_logical()
## )
```

```
## See spec(...) for full column specifications.
```

<div data-pagedtable="false">
  <script data-pagedtable-source type="application/json">
{"columns":[{"label":["outliers_removed"],"name":[1],"type":["lgl"],"align":["right"]},{"label":["pve.exposure"],"name":[2],"type":["dbl"],"align":["right"]},{"label":["F"],"name":[3],"type":["dbl"],"align":["right"]},{"label":["Alpha"],"name":[4],"type":["dbl"],"align":["right"]},{"label":["NCP"],"name":[5],"type":["dbl"],"align":["right"]},{"label":["Power"],"name":[6],"type":["dbl"],"align":["right"]}],"data":[{"1":"FALSE","2":"0.04832568","3":"26.56621","4":"0.05","5":"4.917971301","6":"0.60169009"},{"1":"TRUE","2":"0.04124302","3":"27.01479","4":"0.05","5":"0.006746456","6":"0.05077317"}],"options":{"columns":{"min":{},"max":[10]},"rows":{"min":[10],"max":[10]},"pages":{}}}
  </script>
</div>

##  MR Results
To obtain an overall estimate of causal effect, the SNP-exposure and SNP-outcome coefficients were combined in 1) a fixed-effects meta-analysis using an inverse-variance weighted approach (IVW); 2) a Weighted Median approach; 3) Weighted Mode approach and 4) Egger Regression.


[**IVW**](https://doi.org/10.1002/gepi.21758) is equivalent to a weighted regression of the SNP-outcome coefficients on the SNP-exposure coefficients with the intercept constrained to zero. This method assumes that all variants are valid instrumental variables based on the Mendelian randomization assumptions. The causal estimate of the IVW analysis expresses the causal increase in the outcome (or log odds of the outcome for a binary outcome) per unit change in the exposure. [**Weighted median MR**](https://doi.org/10.1002/gepi.21965) allows for 50% of the instrumental variables to be invalid. [**MR-Egger regression**](https://doi.org/10.1093/ije/dyw220) allows all the instrumental variables to be subject to direct effects (i.e. horizontal pleiotropy), with the intercept representing bias in the causal estimate due to pleiotropy and the slope representing the causal estimate. [**Weighted Mode**](https://doi.org/10.1093/ije/dyx102) gives consistent estimates as the sample size increases if a plurality (or weighted plurality) of the genetic variants are valid instruments.
<br>



Table 6 presents the MR causal estimates of genetically predicted CSF Tau on Diabetes.
<br>

**Table 6** MR causaul estimates for CSF Tau on Diabetes
<div data-pagedtable="false">
  <script data-pagedtable-source type="application/json">
{"columns":[{"label":["id.exposure"],"name":[1],"type":["chr"],"align":["left"]},{"label":["id.outcome"],"name":[2],"type":["chr"],"align":["left"]},{"label":["outcome"],"name":[3],"type":["fctr"],"align":["left"]},{"label":["exposure"],"name":[4],"type":["fctr"],"align":["left"]},{"label":["method"],"name":[5],"type":["fctr"],"align":["left"]},{"label":["nsnp"],"name":[6],"type":["int"],"align":["right"]},{"label":["b"],"name":[7],"type":["dbl"],"align":["right"]},{"label":["se"],"name":[8],"type":["dbl"],"align":["right"]},{"label":["pval"],"name":[9],"type":["dbl"],"align":["right"]}],"data":[{"1":"VQ4LV8","2":"qsrNdA","3":"Xue2018diab","4":"Deming2017tau","5":"Inverse variance weighted (fixed effects)","6":"6","7":"0.17637739","8":"0.1119000","9":"0.1149786"},{"1":"VQ4LV8","2":"qsrNdA","3":"Xue2018diab","4":"Deming2017tau","5":"Weighted median","6":"6","7":"0.02134708","8":"0.1901805","9":"0.9106280"},{"1":"VQ4LV8","2":"qsrNdA","3":"Xue2018diab","4":"Deming2017tau","5":"Weighted mode","6":"6","7":"-0.24787831","8":"0.3132904","9":"0.4646814"},{"1":"VQ4LV8","2":"qsrNdA","3":"Xue2018diab","4":"Deming2017tau","5":"MR Egger","6":"6","7":"-1.23062071","8":"1.2742589","9":"0.3888565"}],"options":{"columns":{"min":{},"max":[10]},"rows":{"min":[10],"max":[10]},"pages":{}}}
  </script>
</div>
<br>

Figure 1 illustrates the SNP-specific associations with CSF Tau versus the association in Diabetes and the corresponding MR estimates.
<br>

<div class="figure" style="text-align: center">
<img src="/sc/arion/projects/LOAD/shea/Projects/MR_ADPhenome/results/MR_ADbidir/Deming2017tau/Xue2018diab/Deming2017tau_5e-6_Xue2018diab_MR_Analaysis_files/figure-html/scatter_plot-1.png" alt="Fig. 1: Scatterplot of SNP effects for the association of the Exposure on the Outcome"  />
<p class="caption">Fig. 1: Scatterplot of SNP effects for the association of the Exposure on the Outcome</p>
</div>
<br>


## Pleiotropy
A Cochrans Q heterogeneity test can be used to formaly assesse for the presence of heterogenity (Table 7), with excessive heterogeneity indicating that there is a meaningful violation of at least one of the MR assumptions.
these assumptions..
<br>

**Table 7:** Heterogenity Tests
<div data-pagedtable="false">
  <script data-pagedtable-source type="application/json">
{"columns":[{"label":["id.exposure"],"name":[1],"type":["chr"],"align":["left"]},{"label":["id.outcome"],"name":[2],"type":["chr"],"align":["left"]},{"label":["outcome"],"name":[3],"type":["fctr"],"align":["left"]},{"label":["exposure"],"name":[4],"type":["fctr"],"align":["left"]},{"label":["method"],"name":[5],"type":["fctr"],"align":["left"]},{"label":["Q"],"name":[6],"type":["dbl"],"align":["right"]},{"label":["Q_df"],"name":[7],"type":["dbl"],"align":["right"]},{"label":["Q_pval"],"name":[8],"type":["dbl"],"align":["right"]}],"data":[{"1":"VQ4LV8","2":"qsrNdA","3":"Xue2018diab","4":"Deming2017tau","5":"MR Egger","6":"20.02880","7":"4","8":"4.929036e-04"},{"1":"VQ4LV8","2":"qsrNdA","3":"Xue2018diab","4":"Deming2017tau","5":"Inverse variance weighted","6":"26.37873","7":"5","8":"7.534103e-05"}],"options":{"columns":{"min":{},"max":[10]},"rows":{"min":[10],"max":[10]},"pages":{}}}
  </script>
</div>
<br>

Figure 2 shows a funnel plot displaying the MR estimates of individual genetic variants against their precession. Aysmmetry in the funnel plot may arrise due to some genetic variants having unusally strong effects on the outcome, which is indicative of directional pleiotropy.
<br>

<div class="figure" style="text-align: center">
<img src="/sc/arion/projects/LOAD/shea/Projects/MR_ADPhenome/results/MR_ADbidir/Deming2017tau/Xue2018diab/Deming2017tau_5e-6_Xue2018diab_MR_Analaysis_files/figure-html/funnel_plot-1.png" alt="Fig. 2: Funnel plot of the MR causal estimates against their precession"  />
<p class="caption">Fig. 2: Funnel plot of the MR causal estimates against their precession</p>
</div>
<br>

Figure 3 shows a [Radial Plots](https://github.com/WSpiller/RadialMR) can be used to visualize influential data points with large contributions to Cochran's Q Statistic that may bias causal effect estimates.



<div class="figure" style="text-align: center">
<img src="/sc/arion/projects/LOAD/shea/Projects/MR_ADPhenome/results/MR_ADbidir/Deming2017tau/Xue2018diab/Deming2017tau_5e-6_Xue2018diab_MR_Analaysis_files/figure-html/Radial_Plot-1.png" alt="Fig. 4: Radial Plot showing influential data points using Radial IVW"  />
<p class="caption">Fig. 4: Radial Plot showing influential data points using Radial IVW</p>
</div>
<br>

The intercept of the MR-Regression model captures the average pleitropic affect across all genetic variants (Table 8).
<br>

**Table 8:** MR Egger test for directional pleitropy
<div data-pagedtable="false">
  <script data-pagedtable-source type="application/json">
{"columns":[{"label":["id.exposure"],"name":[1],"type":["chr"],"align":["left"]},{"label":["id.outcome"],"name":[2],"type":["chr"],"align":["left"]},{"label":["outcome"],"name":[3],"type":["fctr"],"align":["left"]},{"label":["exposure"],"name":[4],"type":["fctr"],"align":["left"]},{"label":["egger_intercept"],"name":[5],"type":["dbl"],"align":["right"]},{"label":["se"],"name":[6],"type":["dbl"],"align":["right"]},{"label":["pval"],"name":[7],"type":["dbl"],"align":["right"]}],"data":[{"1":"VQ4LV8","2":"qsrNdA","3":"Xue2018diab","4":"Deming2017tau","5":"0.04853841","6":"0.04310212","7":"0.3231024"}],"options":{"columns":{"min":{},"max":[10]},"rows":{"min":[10],"max":[10]},"pages":{}}}
  </script>
</div>
<br>

Pleiotropy was also assesed using Mendelian Randomization Pleiotropy RESidual Sum and Outlier [(MR-PRESSO)](https://doi.org/10.1038/s41588-018-0099-7), that allows for the evlation of evaluation of horizontal pleiotropy in a standared MR model (Table 9). MR-PRESSO performs a global test for detection of horizontal pleiotropy and correction of pleiotropy via outlier removal (Table 10).
<br>

**Table 9:** MR-PRESSO Global Test for pleitropy
<div data-pagedtable="false">
  <script data-pagedtable-source type="application/json">
{"columns":[{"label":["id.exposure"],"name":[1],"type":["chr"],"align":["left"]},{"label":["id.outcome"],"name":[2],"type":["chr"],"align":["left"]},{"label":["outcome"],"name":[3],"type":["chr"],"align":["left"]},{"label":["exposure"],"name":[4],"type":["chr"],"align":["left"]},{"label":["pt"],"name":[5],"type":["dbl"],"align":["right"]},{"label":["outliers_removed"],"name":[6],"type":["lgl"],"align":["right"]},{"label":["n_outliers"],"name":[7],"type":["dbl"],"align":["right"]},{"label":["RSSobs"],"name":[8],"type":["dbl"],"align":["right"]},{"label":["pval"],"name":[9],"type":["dbl"],"align":["right"]}],"data":[{"1":"VQ4LV8","2":"qsrNdA","3":"Xue2018diab","4":"Deming2017tau","5":"5e-06","6":"FALSE","7":"1","8":"37.32321","9":"2e-04"}],"options":{"columns":{"min":{},"max":[10]},"rows":{"min":[10],"max":[10]},"pages":{}}}
  </script>
</div>
<br>


**Table 10:** MR Estimates after MR-PRESSO outlier removal
<div data-pagedtable="false">
  <script data-pagedtable-source type="application/json">
{"columns":[{"label":["id.exposure"],"name":[1],"type":["chr"],"align":["left"]},{"label":["id.outcome"],"name":[2],"type":["chr"],"align":["left"]},{"label":["outcome"],"name":[3],"type":["fctr"],"align":["left"]},{"label":["exposure"],"name":[4],"type":["fctr"],"align":["left"]},{"label":["method"],"name":[5],"type":["fctr"],"align":["left"]},{"label":["nsnp"],"name":[6],"type":["int"],"align":["right"]},{"label":["b"],"name":[7],"type":["dbl"],"align":["right"]},{"label":["se"],"name":[8],"type":["dbl"],"align":["right"]},{"label":["pval"],"name":[9],"type":["dbl"],"align":["right"]}],"data":[{"1":"VQ4LV8","2":"qsrNdA","3":"Xue2018diab","4":"Deming2017tau","5":"Inverse variance weighted (fixed effects)","6":"5","7":"0.00678176","8":"0.1202942","9":"0.9550419"},{"1":"VQ4LV8","2":"qsrNdA","3":"Xue2018diab","4":"Deming2017tau","5":"Weighted median","6":"5","7":"-0.08038311","8":"0.1645260","9":"0.6251435"},{"1":"VQ4LV8","2":"qsrNdA","3":"Xue2018diab","4":"Deming2017tau","5":"Weighted mode","6":"5","7":"-0.31695963","8":"0.4086175","9":"0.4812407"},{"1":"VQ4LV8","2":"qsrNdA","3":"Xue2018diab","4":"Deming2017tau","5":"MR Egger","6":"5","7":"-0.00551361","8":"1.3956167","9":"0.9970959"}],"options":{"columns":{"min":{},"max":[10]},"rows":{"min":[10],"max":[10]},"pages":{}}}
  </script>
</div>
<br>

<div class="figure" style="text-align: center">
<img src="/sc/arion/projects/LOAD/shea/Projects/MR_ADPhenome/results/MR_ADbidir/Deming2017tau/Xue2018diab/Deming2017tau_5e-6_Xue2018diab_MR_Analaysis_files/figure-html/scatter_plot_outlier-1.png" alt="Fig. 5: Scatterplot of SNP effects for the association of the Exposure on the Outcome after outlier removal"  />
<p class="caption">Fig. 5: Scatterplot of SNP effects for the association of the Exposure on the Outcome after outlier removal</p>
</div>
<br>

**Table 11:** Heterogenity Tests after outlier removal
<div data-pagedtable="false">
  <script data-pagedtable-source type="application/json">
{"columns":[{"label":["id.exposure"],"name":[1],"type":["chr"],"align":["left"]},{"label":["id.outcome"],"name":[2],"type":["chr"],"align":["left"]},{"label":["outcome"],"name":[3],"type":["fctr"],"align":["left"]},{"label":["exposure"],"name":[4],"type":["fctr"],"align":["left"]},{"label":["method"],"name":[5],"type":["fctr"],"align":["left"]},{"label":["Q"],"name":[6],"type":["dbl"],"align":["right"]},{"label":["Q_df"],"name":[7],"type":["dbl"],"align":["right"]},{"label":["Q_pval"],"name":[8],"type":["dbl"],"align":["right"]}],"data":[{"1":"VQ4LV8","2":"qsrNdA","3":"Xue2018diab","4":"Deming2017tau","5":"MR Egger","6":"11.62140","7":"3","8":"0.008799294"},{"1":"VQ4LV8","2":"qsrNdA","3":"Xue2018diab","4":"Deming2017tau","5":"Inverse variance weighted","6":"11.62171","7":"4","8":"0.020397637"}],"options":{"columns":{"min":{},"max":[10]},"rows":{"min":[10],"max":[10]},"pages":{}}}
  </script>
</div>
<br>

**Table 12:** MR Egger test for directional pleitropy after outlier removal
<div data-pagedtable="false">
  <script data-pagedtable-source type="application/json">
{"columns":[{"label":["id.exposure"],"name":[1],"type":["chr"],"align":["left"]},{"label":["id.outcome"],"name":[2],"type":["chr"],"align":["left"]},{"label":["outcome"],"name":[3],"type":["fctr"],"align":["left"]},{"label":["exposure"],"name":[4],"type":["fctr"],"align":["left"]},{"label":["egger_intercept"],"name":[5],"type":["dbl"],"align":["right"]},{"label":["se"],"name":[6],"type":["dbl"],"align":["right"]},{"label":["pval"],"name":[7],"type":["dbl"],"align":["right"]}],"data":[{"1":"VQ4LV8","2":"qsrNdA","3":"Xue2018diab","4":"Deming2017tau","5":"0.0004472379","6":"0.05002901","7":"0.9934286"}],"options":{"columns":{"min":{},"max":[10]},"rows":{"min":[10],"max":[10]},"pages":{}}}
  </script>
</div>
<br>
