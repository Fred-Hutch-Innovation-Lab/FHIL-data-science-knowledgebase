---
title: Cell types
parent: Biology
---

These definitions reflect my understanding of common celltypes encountered in this field. It is not necessarily true, and these direct relationships are not necessarily how cells exist in reality, but it is a mostly accurate heuristic. For convenience and consistency, you should try to use the main name of the celltype listed here (not aliases). This will make data more easily interpretable across projects.

There is a formal (and intimidating) cell ontology maintained [here](https://obofoundry.org/ontology/cl.html). This should be the de-facto reference, but it is very verbose and hard to work with. This local DAG handles the most common use cases and aliases, but consult the reference for updates. 

## Aliases and subsets

```yaml
{% include celltype_DAG.yaml %}
```

## Marker genes

Finding cannonical marker genes is harder than it should be given the concept. In reality there doesn't seem to be a de-facto set of 'cannonical' marker genes for most cells. Many publications use slightly different sets. It can be challenging to currate an accurate set, and inevitably someone will ask (what about gene ASDFSDAF). Your best bet is to spend a little time collecting literature for genes specific niche cells in your dataset, but mostly relying on larger atlas datasets for tried-and-true markers of common cells. A few resources to get you started:

[cellxgene's cell guide](https://cellxgene.cziscience.com/cellguide) uses it's database to calculate computational markers, and has a section for 'cannonical markers' from the [Human Reference Atlas](https://doi.org/10.1038/s41556-021-00788-6).

I previously made an effort to catalog marker genes. This is a little out of data and not super well curated, but may serve as a starting point. See the `data` folder of this repo for a csv of this.

<div style="overflow-x: auto; max-width: 100%; overflow-y: auto; max-height: 300px; border: 1px solid #ccc; padding: 8px;">
  
<!-- | Gene symbol    | aliases | expression level | celltype | relative to (celltype) | tissue | species | condition | assay | confidence | date added | reference | notes |
|---------|---------|------------------|----------|------------------------|--------|---------|-----------|-------|------------|------------|-----------|-------|
{% for row in site.data.celltype_markers %}
| {{ row.gene_symbol }} | {{ row.aliases }} | {{ row.expression_level }} | {{ row.celltype }} | {{ row['relative to (celltype)'] }} | {{ row.tissue }} | {{ row.species }} | {{ row.condition }} | {{ row.assay }} | {{ row.confidence }} | {{ row['date added'] }} | {{ row.reference }} | {{ row.notes }} |
{% endfor %} -->


<table>
  {% for row in site.data.celltype_markers %}
    {% if forloop.first %}
    <tr>
      {% for pair in row %}
        <th>{{ pair[0] }}</th>
      {% endfor %}
    </tr>
    {% endif %}

    {% tablerow pair in row %}
      {{ pair[1] }}
    {% endtablerow %}
  {% endfor %}
</table>

</div>
