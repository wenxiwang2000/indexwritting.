# 🧬 Marker Gene Selection Criteria

A gene was considered a **high-confidence cluster marker** when it satisfied the following criteria:

| ✅ Metric | Threshold | Interpretation |
|-----------|------------|----------------|
| **avg_log2FC** | > 1 | At least 2-fold enriched in the target cluster |
| **pct.1** | > 0.50 | Expressed in >50% of cells within the cluster |
| **pct.2** | < 0.20 | Expressed in <20% of cells outside the cluster |
| **p_val_adj** | < 0.05 | Statistically significant after multiple-testing correction |

---

# 📖 Marker Statistics Explained

| Column | Meaning | Example |
|----------|----------|----------|
| **p_val** | Raw statistical p-value | Smaller = stronger evidence of differential expression |
| **avg_log2FC** | Average log₂ fold-change between target cluster and all other cells | 5 = ~32× enrichment |
| **pct.1** | Fraction of cells expressing the gene in the target cluster | 0.91 = 91% of cells express the gene |
| **pct.2** | Fraction of cells expressing the gene outside the target cluster | 0.03 = 3% of other cells express the gene |
| **p_val_adj** | Multiple-testing corrected p-value (Bonferroni/FDR) | More reliable significance measure |

---

# 🎯 How to Interpret a Good Marker

| Scenario | Interpretation |
|-----------|-----------|
| 🔥 High avg_log2FC + High pct.1 + Low pct.2 | Excellent cluster-specific marker |
| 🧩 High avg_log2FC + Moderate pct.1 | Marker of a cluster subpopulation |
| 🌍 High pct.1 + High pct.2 | Widely expressed gene; poor marker |
| ⚠️ Low avg_log2FC | Weak enrichment |
| ❌ High p_val_adj | Not statistically significant |

---

# 🏆 Example: Hector (TC013321)

| Metric | Value |
|----------|----------|
| avg_log2FC | 7.18 |
| pct.1 | 0.57 |
| pct.2 | 0.011 |
| p_val_adj | < 0.05 |

### Interpretation

✅ Strongly enriched in Cluster 27

✅ Very low expression outside Cluster 27

✅ Highly specific marker

⚠️ Expressed in only ~57% of Cluster 27 cells

➡️ Therefore, **hector is best interpreted as a marker of a Cluster 27 subpopulation rather than the entire cluster.**

---

# 📚 Literature Support

These thresholds are widely used in single-cell RNA-seq studies and are consistent with default practices in:

| Reference | Contribution |
|------------|------------|
| Satija et al., 2015 (Seurat) | Original Seurat framework |
| Stuart et al., 2019, Cell | Integrated single-cell analysis |
| Hao et al., 2021, Cell | Seurat v4 multimodal analysis |
| Luecken & Theis, 2019, Mol Syst Biol | scRNA-seq best practices |
| Mereu et al., 2020, Nat Biotechnol | Benchmarking scRNA-seq methods |

---

# 💡 Practical Rule of Thumb

A marker is usually considered **high confidence** when:

```text
avg_log2FC > 1
pct.1 > 0.50
pct.2 < 0.20
p_val_adj < 0.05
```

The strongest markers combine:

🟢 High enrichment (avg_log2FC)

🟢 High prevalence within the cluster (pct.1)

🟢 Low prevalence outside the cluster (pct.2)

🟢 Strong statistical support (p_val_adj)
