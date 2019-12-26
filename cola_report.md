cola Report for recount2:SRP043162
==================

**Date**: 2019-12-26 00:19:26 CET, **cola version**: 1.3.2

----------------------------------------------------------------

<style type='text/css'>

body, td, th {
   font-family: Arial,Helvetica,sans-serif;
   background-color: white;
   font-size: 13px;
  max-width: 800px;
  margin: auto;
  margin-left:210px;
  padding: 0px 10px 0px 10px;
  border-left: 1px solid #EEEEEE;
  line-height: 150%;
}

tt, code, pre {
   font-family: 'DejaVu Sans Mono', 'Droid Sans Mono', 'Lucida Console', Consolas, Monaco, 

monospace;
}

h1 {
   font-size:2.2em;
}

h2 {
   font-size:1.8em;
}

h3 {
   font-size:1.4em;
}

h4 {
   font-size:1.0em;
}

h5 {
   font-size:0.9em;
}

h6 {
   font-size:0.8em;
}

a {
  text-decoration: none;
  color: #0366d6;
}

a:hover {
  text-decoration: underline;
}

a:visited {
   color: #0366d6;
}

pre, img {
  max-width: 100%;
}
pre {
  overflow-x: auto;
}
pre code {
   display: block; padding: 0.5em;
}

code {
  font-size: 92%;
  border: 1px solid #ccc;
}

code[class] {
  background-color: #F8F8F8;
}

table, td, th {
  border: 1px solid #ccc;
}

blockquote {
   color:#666666;
   margin:0;
   padding-left: 1em;
   border-left: 0.5em #EEE solid;
}

hr {
   height: 0px;
   border-bottom: none;
   border-top-width: thin;
   border-top-style: dotted;
   border-top-color: #999999;
}

@media print {
   * {
      background: transparent !important;
      color: black !important;
      filter:none !important;
      -ms-filter: none !important;
   }

   body {
      font-size:12pt;
      max-width:100%;
   }

   a, a:visited {
      text-decoration: underline;
   }

   hr {
      visibility: hidden;
      page-break-before: always;
   }

   pre, blockquote {
      padding-right: 1em;
      page-break-inside: avoid;
   }

   tr, img {
      page-break-inside: avoid;
   }

   img {
      max-width: 100% !important;
   }

   @page :left {
      margin: 15mm 20mm 15mm 10mm;
   }

   @page :right {
      margin: 15mm 10mm 15mm 20mm;
   }

   p, h2, h3 {
      orphans: 3; widows: 3;
   }

   h2, h3 {
      page-break-after: avoid;
   }
}
</style>




## Summary





All available functions which can be applied to this `res_list` object:


```r
res_list
```

```
#> A 'ConsensusPartitionList' object with 24 methods.
#>   On a matrix with 15680 rows and 53 columns.
#>   Top rows are extracted by 'SD, CV, MAD, ATC' methods.
#>   Subgroups are detected by 'hclust, kmeans, skmeans, pam, mclust, NMF' method.
#>   Number of partitions are tried for k = 2, 3, 4, 5, 6.
#>   Performed in total 30000 partitions by row resampling.
#> 
#> Following methods can be applied to this 'ConsensusPartitionList' object:
#>  [1] "cola_report"           "collect_classes"       "collect_plots"         "collect_stats"        
#>  [5] "colnames"              "functional_enrichment" "get_anno_col"          "get_anno"             
#>  [9] "get_classes"           "get_matrix"            "get_membership"        "get_stats"            
#> [13] "is_best_k"             "is_stable_k"           "ncol"                  "nrow"                 
#> [17] "rownames"              "show"                  "suggest_best_k"        "test_to_known_factors"
#> [21] "top_rows_heatmap"      "top_rows_overlap"     
#> 
#> You can get result for a single method by, e.g. object["SD", "hclust"] or object["SD:hclust"]
#> or a subset of methods by object[c("SD", "CV")], c("hclust", "kmeans")]
```

The call of `run_all_consensus_partition_methods()` was:


```
#> run_all_consensus_partition_methods(data = mat, mc.cores = 4)
```

Dimension of the input matrix:


```r
mat = get_matrix(res_list)
dim(mat)
```

```
#> [1] 15680    53
```

### Density distribution

The density distribution for each sample is visualized as in one column in the
following heatmap. The clustering is based on the distance which is the
Kolmogorov-Smirnov statistic between two distributions.




```r
library(ComplexHeatmap)
densityHeatmap(mat, ylab = "value", cluster_columns = TRUE, show_column_names = FALSE,
    mc.cores = 4)
```

![plot of chunk density-heatmap](figure_cola/density-heatmap-1.png)





### Suggest the best k



Folowing table shows the best `k` (number of partitions) for each combination
of top-value methods and partition methods. Clicking on the method name in
the table goes to the section for a single combination of methods.

[The cola vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/cola.html#toc_13)
explains the definition of the metrics used for determining the best
number of partitions.


```r
suggest_best_k(res_list)
```


|                            | The best k| 1-PAC| Mean silhouette| Concordance|   |Optional k |
|:---------------------------|----------:|-----:|---------------:|-----------:|:--|:----------|
|[SD:mclust](#SD-mclust)     |          2| 1.000|           0.951|       0.963|** |           |
|[SD:NMF](#SD-NMF)           |          2| 1.000|           0.956|       0.981|** |           |
|[CV:NMF](#CV-NMF)           |          2| 1.000|           0.953|       0.981|** |           |
|[MAD:skmeans](#MAD-skmeans) |          2| 1.000|           0.982|       0.987|** |           |
|[MAD:mclust](#MAD-mclust)   |          2| 1.000|           0.951|       0.969|** |           |
|[MAD:NMF](#MAD-NMF)         |          2| 1.000|           0.956|       0.982|** |           |
|[ATC:pam](#ATC-pam)         |          3| 1.000|           0.976|       0.991|** |2          |
|[ATC:skmeans](#ATC-skmeans) |          6| 0.976|           0.927|       0.960|** |2,3,5      |
|[ATC:NMF](#ATC-NMF)         |          3| 0.963|           0.946|       0.978|** |           |
|[MAD:hclust](#MAD-hclust)   |          2| 0.960|           0.955|       0.979|** |           |
|[SD:skmeans](#SD-skmeans)   |          3| 0.953|           0.930|       0.966|** |2          |
|[CV:skmeans](#CV-skmeans)   |          2| 0.922|           0.934|       0.973|*  |           |
|[ATC:kmeans](#ATC-kmeans)   |          3| 0.900|           0.903|       0.962|   |           |
|[MAD:pam](#MAD-pam)         |          3| 0.833|           0.889|       0.939|   |           |
|[SD:pam](#SD-pam)           |          2| 0.710|           0.875|       0.926|   |           |
|[SD:hclust](#SD-hclust)     |          3| 0.630|           0.776|       0.891|   |           |
|[SD:kmeans](#SD-kmeans)     |          3| 0.576|           0.875|       0.909|   |           |
|[MAD:kmeans](#MAD-kmeans)   |          3| 0.563|           0.853|       0.899|   |           |
|[ATC:hclust](#ATC-hclust)   |          3| 0.505|           0.739|       0.830|   |           |
|[CV:pam](#CV-pam)           |          2| 0.429|           0.743|       0.846|   |           |
|[ATC:mclust](#ATC-mclust)   |          3| 0.418|           0.723|       0.841|   |           |
|[CV:hclust](#CV-hclust)     |          4| 0.390|           0.591|       0.785|   |           |
|[CV:mclust](#CV-mclust)     |          3| 0.374|           0.739|       0.831|   |           |
|[CV:kmeans](#CV-kmeans)     |          4| 0.331|           0.557|       0.711|   |           |

\*\*: 1-PAC > 0.95, \*: 1-PAC > 0.9




### CDF of consensus matrices

Cumulative distribution function curves of consensus matrix for all methods.




```r
collect_plots(res_list, fun = plot_ecdf)
```

![plot of chunk collect-plots](figure_cola/collect-plots-1.png)



### Consensus heatmap

Consensus heatmaps for all methods. ([What is a consensus heatmap?](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/cola.html#toc_9))


<style type='text/css'>



.ui-helper-hidden {
	display: none;
}
.ui-helper-hidden-accessible {
	border: 0;
	clip: rect(0 0 0 0);
	height: 1px;
	margin: -1px;
	overflow: hidden;
	padding: 0;
	position: absolute;
	width: 1px;
}
.ui-helper-reset {
	margin: 0;
	padding: 0;
	border: 0;
	outline: 0;
	line-height: 1.3;
	text-decoration: none;
	font-size: 100%;
	list-style: none;
}
.ui-helper-clearfix:before,
.ui-helper-clearfix:after {
	content: "";
	display: table;
	border-collapse: collapse;
}
.ui-helper-clearfix:after {
	clear: both;
}
.ui-helper-zfix {
	width: 100%;
	height: 100%;
	top: 0;
	left: 0;
	position: absolute;
	opacity: 0;
	filter:Alpha(Opacity=0); 
}

.ui-front {
	z-index: 100;
}



.ui-state-disabled {
	cursor: default !important;
	pointer-events: none;
}



.ui-icon {
	display: inline-block;
	vertical-align: middle;
	margin-top: -.25em;
	position: relative;
	text-indent: -99999px;
	overflow: hidden;
	background-repeat: no-repeat;
}

.ui-widget-icon-block {
	left: 50%;
	margin-left: -8px;
	display: block;
}




.ui-widget-overlay {
	position: fixed;
	top: 0;
	left: 0;
	width: 100%;
	height: 100%;
}
.ui-accordion .ui-accordion-header {
	display: block;
	cursor: pointer;
	position: relative;
	margin: 2px 0 0 0;
	padding: .5em .5em .5em .7em;
	font-size: 100%;
}
.ui-accordion .ui-accordion-content {
	padding: 1em 2.2em;
	border-top: 0;
	overflow: auto;
}
.ui-autocomplete {
	position: absolute;
	top: 0;
	left: 0;
	cursor: default;
}
.ui-menu {
	list-style: none;
	padding: 0;
	margin: 0;
	display: block;
	outline: 0;
}
.ui-menu .ui-menu {
	position: absolute;
}
.ui-menu .ui-menu-item {
	margin: 0;
	cursor: pointer;
	
	list-style-image: url("data:image/gif;base64,R0lGODlhAQABAIAAAAAAAP///yH5BAEAAAAALAAAAAABAAEAAAIBRAA7");
}
.ui-menu .ui-menu-item-wrapper {
	position: relative;
	padding: 3px 1em 3px .4em;
}
.ui-menu .ui-menu-divider {
	margin: 5px 0;
	height: 0;
	font-size: 0;
	line-height: 0;
	border-width: 1px 0 0 0;
}
.ui-menu .ui-state-focus,
.ui-menu .ui-state-active {
	margin: -1px;
}


.ui-menu-icons {
	position: relative;
}
.ui-menu-icons .ui-menu-item-wrapper {
	padding-left: 2em;
}


.ui-menu .ui-icon {
	position: absolute;
	top: 0;
	bottom: 0;
	left: .2em;
	margin: auto 0;
}


.ui-menu .ui-menu-icon {
	left: auto;
	right: 0;
}
.ui-button {
	padding: .4em 1em;
	display: inline-block;
	position: relative;
	line-height: normal;
	margin-right: .1em;
	cursor: pointer;
	vertical-align: middle;
	text-align: center;
	-webkit-user-select: none;
	-moz-user-select: none;
	-ms-user-select: none;
	user-select: none;

	
	overflow: visible;
}

.ui-button,
.ui-button:link,
.ui-button:visited,
.ui-button:hover,
.ui-button:active {
	text-decoration: none;
}


.ui-button-icon-only {
	width: 2em;
	box-sizing: border-box;
	text-indent: -9999px;
	white-space: nowrap;
}


input.ui-button.ui-button-icon-only {
	text-indent: 0;
}


.ui-button-icon-only .ui-icon {
	position: absolute;
	top: 50%;
	left: 50%;
	margin-top: -8px;
	margin-left: -8px;
}

.ui-button.ui-icon-notext .ui-icon {
	padding: 0;
	width: 2.1em;
	height: 2.1em;
	text-indent: -9999px;
	white-space: nowrap;

}

input.ui-button.ui-icon-notext .ui-icon {
	width: auto;
	height: auto;
	text-indent: 0;
	white-space: normal;
	padding: .4em 1em;
}



input.ui-button::-moz-focus-inner,
button.ui-button::-moz-focus-inner {
	border: 0;
	padding: 0;
}
.ui-controlgroup {
	vertical-align: middle;
	display: inline-block;
}
.ui-controlgroup > .ui-controlgroup-item {
	float: left;
	margin-left: 0;
	margin-right: 0;
}
.ui-controlgroup > .ui-controlgroup-item:focus,
.ui-controlgroup > .ui-controlgroup-item.ui-visual-focus {
	z-index: 9999;
}
.ui-controlgroup-vertical > .ui-controlgroup-item {
	display: block;
	float: none;
	width: 100%;
	margin-top: 0;
	margin-bottom: 0;
	text-align: left;
}
.ui-controlgroup-vertical .ui-controlgroup-item {
	box-sizing: border-box;
}
.ui-controlgroup .ui-controlgroup-label {
	padding: .4em 1em;
}
.ui-controlgroup .ui-controlgroup-label span {
	font-size: 80%;
}
.ui-controlgroup-horizontal .ui-controlgroup-label + .ui-controlgroup-item {
	border-left: none;
}
.ui-controlgroup-vertical .ui-controlgroup-label + .ui-controlgroup-item {
	border-top: none;
}
.ui-controlgroup-horizontal .ui-controlgroup-label.ui-widget-content {
	border-right: none;
}
.ui-controlgroup-vertical .ui-controlgroup-label.ui-widget-content {
	border-bottom: none;
}


.ui-controlgroup-vertical .ui-spinner-input {

	
	width: 75%;
	width: calc( 100% - 2.4em );
}
.ui-controlgroup-vertical .ui-spinner .ui-spinner-up {
	border-top-style: solid;
}

.ui-checkboxradio-label .ui-icon-background {
	box-shadow: inset 1px 1px 1px #ccc;
	border-radius: .12em;
	border: none;
}
.ui-checkboxradio-radio-label .ui-icon-background {
	width: 16px;
	height: 16px;
	border-radius: 1em;
	overflow: visible;
	border: none;
}
.ui-checkboxradio-radio-label.ui-checkboxradio-checked .ui-icon,
.ui-checkboxradio-radio-label.ui-checkboxradio-checked:hover .ui-icon {
	background-image: none;
	width: 8px;
	height: 8px;
	border-width: 4px;
	border-style: solid;
}
.ui-checkboxradio-disabled {
	pointer-events: none;
}
.ui-datepicker {
	width: 17em;
	padding: .2em .2em 0;
	display: none;
}
.ui-datepicker .ui-datepicker-header {
	position: relative;
	padding: .2em 0;
}
.ui-datepicker .ui-datepicker-prev,
.ui-datepicker .ui-datepicker-next {
	position: absolute;
	top: 2px;
	width: 1.8em;
	height: 1.8em;
}
.ui-datepicker .ui-datepicker-prev-hover,
.ui-datepicker .ui-datepicker-next-hover {
	top: 1px;
}
.ui-datepicker .ui-datepicker-prev {
	left: 2px;
}
.ui-datepicker .ui-datepicker-next {
	right: 2px;
}
.ui-datepicker .ui-datepicker-prev-hover {
	left: 1px;
}
.ui-datepicker .ui-datepicker-next-hover {
	right: 1px;
}
.ui-datepicker .ui-datepicker-prev span,
.ui-datepicker .ui-datepicker-next span {
	display: block;
	position: absolute;
	left: 50%;
	margin-left: -8px;
	top: 50%;
	margin-top: -8px;
}
.ui-datepicker .ui-datepicker-title {
	margin: 0 2.3em;
	line-height: 1.8em;
	text-align: center;
}
.ui-datepicker .ui-datepicker-title select {
	font-size: 1em;
	margin: 1px 0;
}
.ui-datepicker select.ui-datepicker-month,
.ui-datepicker select.ui-datepicker-year {
	width: 45%;
}
.ui-datepicker table {
	width: 100%;
	font-size: .9em;
	border-collapse: collapse;
	margin: 0 0 .4em;
}
.ui-datepicker th {
	padding: .7em .3em;
	text-align: center;
	font-weight: bold;
	border: 0;
}
.ui-datepicker td {
	border: 0;
	padding: 1px;
}
.ui-datepicker td span,
.ui-datepicker td a {
	display: block;
	padding: .2em;
	text-align: right;
	text-decoration: none;
}
.ui-datepicker .ui-datepicker-buttonpane {
	background-image: none;
	margin: .7em 0 0 0;
	padding: 0 .2em;
	border-left: 0;
	border-right: 0;
	border-bottom: 0;
}
.ui-datepicker .ui-datepicker-buttonpane button {
	float: right;
	margin: .5em .2em .4em;
	cursor: pointer;
	padding: .2em .6em .3em .6em;
	width: auto;
	overflow: visible;
}
.ui-datepicker .ui-datepicker-buttonpane button.ui-datepicker-current {
	float: left;
}


.ui-datepicker.ui-datepicker-multi {
	width: auto;
}
.ui-datepicker-multi .ui-datepicker-group {
	float: left;
}
.ui-datepicker-multi .ui-datepicker-group table {
	width: 95%;
	margin: 0 auto .4em;
}
.ui-datepicker-multi-2 .ui-datepicker-group {
	width: 50%;
}
.ui-datepicker-multi-3 .ui-datepicker-group {
	width: 33.3%;
}
.ui-datepicker-multi-4 .ui-datepicker-group {
	width: 25%;
}
.ui-datepicker-multi .ui-datepicker-group-last .ui-datepicker-header,
.ui-datepicker-multi .ui-datepicker-group-middle .ui-datepicker-header {
	border-left-width: 0;
}
.ui-datepicker-multi .ui-datepicker-buttonpane {
	clear: left;
}
.ui-datepicker-row-break {
	clear: both;
	width: 100%;
	font-size: 0;
}


.ui-datepicker-rtl {
	direction: rtl;
}
.ui-datepicker-rtl .ui-datepicker-prev {
	right: 2px;
	left: auto;
}
.ui-datepicker-rtl .ui-datepicker-next {
	left: 2px;
	right: auto;
}
.ui-datepicker-rtl .ui-datepicker-prev:hover {
	right: 1px;
	left: auto;
}
.ui-datepicker-rtl .ui-datepicker-next:hover {
	left: 1px;
	right: auto;
}
.ui-datepicker-rtl .ui-datepicker-buttonpane {
	clear: right;
}
.ui-datepicker-rtl .ui-datepicker-buttonpane button {
	float: left;
}
.ui-datepicker-rtl .ui-datepicker-buttonpane button.ui-datepicker-current,
.ui-datepicker-rtl .ui-datepicker-group {
	float: right;
}
.ui-datepicker-rtl .ui-datepicker-group-last .ui-datepicker-header,
.ui-datepicker-rtl .ui-datepicker-group-middle .ui-datepicker-header {
	border-right-width: 0;
	border-left-width: 1px;
}


.ui-datepicker .ui-icon {
	display: block;
	text-indent: -99999px;
	overflow: hidden;
	background-repeat: no-repeat;
	left: .5em;
	top: .3em;
}
.ui-dialog {
	position: absolute;
	top: 0;
	left: 0;
	padding: .2em;
	outline: 0;
}
.ui-dialog .ui-dialog-titlebar {
	padding: .4em 1em;
	position: relative;
}
.ui-dialog .ui-dialog-title {
	float: left;
	margin: .1em 0;
	white-space: nowrap;
	width: 90%;
	overflow: hidden;
	text-overflow: ellipsis;
}
.ui-dialog .ui-dialog-titlebar-close {
	position: absolute;
	right: .3em;
	top: 50%;
	width: 20px;
	margin: -10px 0 0 0;
	padding: 1px;
	height: 20px;
}
.ui-dialog .ui-dialog-content {
	position: relative;
	border: 0;
	padding: .5em 1em;
	background: none;
	overflow: auto;
}
.ui-dialog .ui-dialog-buttonpane {
	text-align: left;
	border-width: 1px 0 0 0;
	background-image: none;
	margin-top: .5em;
	padding: .3em 1em .5em .4em;
}
.ui-dialog .ui-dialog-buttonpane .ui-dialog-buttonset {
	float: right;
}
.ui-dialog .ui-dialog-buttonpane button {
	margin: .5em .4em .5em 0;
	cursor: pointer;
}
.ui-dialog .ui-resizable-n {
	height: 2px;
	top: 0;
}
.ui-dialog .ui-resizable-e {
	width: 2px;
	right: 0;
}
.ui-dialog .ui-resizable-s {
	height: 2px;
	bottom: 0;
}
.ui-dialog .ui-resizable-w {
	width: 2px;
	left: 0;
}
.ui-dialog .ui-resizable-se,
.ui-dialog .ui-resizable-sw,
.ui-dialog .ui-resizable-ne,
.ui-dialog .ui-resizable-nw {
	width: 7px;
	height: 7px;
}
.ui-dialog .ui-resizable-se {
	right: 0;
	bottom: 0;
}
.ui-dialog .ui-resizable-sw {
	left: 0;
	bottom: 0;
}
.ui-dialog .ui-resizable-ne {
	right: 0;
	top: 0;
}
.ui-dialog .ui-resizable-nw {
	left: 0;
	top: 0;
}
.ui-draggable .ui-dialog-titlebar {
	cursor: move;
}
.ui-draggable-handle {
	-ms-touch-action: none;
	touch-action: none;
}
.ui-resizable {
	position: relative;
}
.ui-resizable-handle {
	position: absolute;
	font-size: 0.1px;
	display: block;
	-ms-touch-action: none;
	touch-action: none;
}
.ui-resizable-disabled .ui-resizable-handle,
.ui-resizable-autohide .ui-resizable-handle {
	display: none;
}
.ui-resizable-n {
	cursor: n-resize;
	height: 7px;
	width: 100%;
	top: -5px;
	left: 0;
}
.ui-resizable-s {
	cursor: s-resize;
	height: 7px;
	width: 100%;
	bottom: -5px;
	left: 0;
}
.ui-resizable-e {
	cursor: e-resize;
	width: 7px;
	right: -5px;
	top: 0;
	height: 100%;
}
.ui-resizable-w {
	cursor: w-resize;
	width: 7px;
	left: -5px;
	top: 0;
	height: 100%;
}
.ui-resizable-se {
	cursor: se-resize;
	width: 12px;
	height: 12px;
	right: 1px;
	bottom: 1px;
}
.ui-resizable-sw {
	cursor: sw-resize;
	width: 9px;
	height: 9px;
	left: -5px;
	bottom: -5px;
}
.ui-resizable-nw {
	cursor: nw-resize;
	width: 9px;
	height: 9px;
	left: -5px;
	top: -5px;
}
.ui-resizable-ne {
	cursor: ne-resize;
	width: 9px;
	height: 9px;
	right: -5px;
	top: -5px;
}
.ui-progressbar {
	height: 2em;
	text-align: left;
	overflow: hidden;
}
.ui-progressbar .ui-progressbar-value {
	margin: -1px;
	height: 100%;
}
.ui-progressbar .ui-progressbar-overlay {
	background: url("data:image/gif;base64,R0lGODlhKAAoAIABAAAAAP///yH/C05FVFNDQVBFMi4wAwEAAAAh+QQJAQABACwAAAAAKAAoAAACkYwNqXrdC52DS06a7MFZI+4FHBCKoDeWKXqymPqGqxvJrXZbMx7Ttc+w9XgU2FB3lOyQRWET2IFGiU9m1frDVpxZZc6bfHwv4c1YXP6k1Vdy292Fb6UkuvFtXpvWSzA+HycXJHUXiGYIiMg2R6W459gnWGfHNdjIqDWVqemH2ekpObkpOlppWUqZiqr6edqqWQAAIfkECQEAAQAsAAAAACgAKAAAApSMgZnGfaqcg1E2uuzDmmHUBR8Qil95hiPKqWn3aqtLsS18y7G1SzNeowWBENtQd+T1JktP05nzPTdJZlR6vUxNWWjV+vUWhWNkWFwxl9VpZRedYcflIOLafaa28XdsH/ynlcc1uPVDZxQIR0K25+cICCmoqCe5mGhZOfeYSUh5yJcJyrkZWWpaR8doJ2o4NYq62lAAACH5BAkBAAEALAAAAAAoACgAAAKVDI4Yy22ZnINRNqosw0Bv7i1gyHUkFj7oSaWlu3ovC8GxNso5fluz3qLVhBVeT/Lz7ZTHyxL5dDalQWPVOsQWtRnuwXaFTj9jVVh8pma9JjZ4zYSj5ZOyma7uuolffh+IR5aW97cHuBUXKGKXlKjn+DiHWMcYJah4N0lYCMlJOXipGRr5qdgoSTrqWSq6WFl2ypoaUAAAIfkECQEAAQAsAAAAACgAKAAAApaEb6HLgd/iO7FNWtcFWe+ufODGjRfoiJ2akShbueb0wtI50zm02pbvwfWEMWBQ1zKGlLIhskiEPm9R6vRXxV4ZzWT2yHOGpWMyorblKlNp8HmHEb/lCXjcW7bmtXP8Xt229OVWR1fod2eWqNfHuMjXCPkIGNileOiImVmCOEmoSfn3yXlJWmoHGhqp6ilYuWYpmTqKUgAAIfkECQEAAQAsAAAAACgAKAAAApiEH6kb58biQ3FNWtMFWW3eNVcojuFGfqnZqSebuS06w5V80/X02pKe8zFwP6EFWOT1lDFk8rGERh1TTNOocQ61Hm4Xm2VexUHpzjymViHrFbiELsefVrn6XKfnt2Q9G/+Xdie499XHd2g4h7ioOGhXGJboGAnXSBnoBwKYyfioubZJ2Hn0RuRZaflZOil56Zp6iioKSXpUAAAh+QQJAQABACwAAAAAKAAoAAACkoQRqRvnxuI7kU1a1UU5bd5tnSeOZXhmn5lWK3qNTWvRdQxP8qvaC+/yaYQzXO7BMvaUEmJRd3TsiMAgswmNYrSgZdYrTX6tSHGZO73ezuAw2uxuQ+BbeZfMxsexY35+/Qe4J1inV0g4x3WHuMhIl2jXOKT2Q+VU5fgoSUI52VfZyfkJGkha6jmY+aaYdirq+lQAACH5BAkBAAEALAAAAAAoACgAAAKWBIKpYe0L3YNKToqswUlvznigd4wiR4KhZrKt9Upqip61i9E3vMvxRdHlbEFiEXfk9YARYxOZZD6VQ2pUunBmtRXo1Lf8hMVVcNl8JafV38aM2/Fu5V16Bn63r6xt97j09+MXSFi4BniGFae3hzbH9+hYBzkpuUh5aZmHuanZOZgIuvbGiNeomCnaxxap2upaCZsq+1kAACH5BAkBAAEALAAAAAAoACgAAAKXjI8By5zf4kOxTVrXNVlv1X0d8IGZGKLnNpYtm8Lr9cqVeuOSvfOW79D9aDHizNhDJidFZhNydEahOaDH6nomtJjp1tutKoNWkvA6JqfRVLHU/QUfau9l2x7G54d1fl995xcIGAdXqMfBNadoYrhH+Mg2KBlpVpbluCiXmMnZ2Sh4GBqJ+ckIOqqJ6LmKSllZmsoq6wpQAAAh+QQJAQABACwAAAAAKAAoAAAClYx/oLvoxuJDkU1a1YUZbJ59nSd2ZXhWqbRa2/gF8Gu2DY3iqs7yrq+xBYEkYvFSM8aSSObE+ZgRl1BHFZNr7pRCavZ5BW2142hY3AN/zWtsmf12p9XxxFl2lpLn1rseztfXZjdIWIf2s5dItwjYKBgo9yg5pHgzJXTEeGlZuenpyPmpGQoKOWkYmSpaSnqKileI2FAAACH5BAkBAAEALAAAAAAoACgAAAKVjB+gu+jG4kORTVrVhRlsnn2dJ3ZleFaptFrb+CXmO9OozeL5VfP99HvAWhpiUdcwkpBH3825AwYdU8xTqlLGhtCosArKMpvfa1mMRae9VvWZfeB2XfPkeLmm18lUcBj+p5dnN8jXZ3YIGEhYuOUn45aoCDkp16hl5IjYJvjWKcnoGQpqyPlpOhr3aElaqrq56Bq7VAAAOw==");
	height: 100%;
	filter: alpha(opacity=25); 
	opacity: 0.25;
}
.ui-progressbar-indeterminate .ui-progressbar-value {
	background-image: none;
}
.ui-selectable {
	-ms-touch-action: none;
	touch-action: none;
}
.ui-selectable-helper {
	position: absolute;
	z-index: 100;
	border: 1px dotted black;
}
.ui-selectmenu-menu {
	padding: 0;
	margin: 0;
	position: absolute;
	top: 0;
	left: 0;
	display: none;
}
.ui-selectmenu-menu .ui-menu {
	overflow: auto;
	overflow-x: hidden;
	padding-bottom: 1px;
}
.ui-selectmenu-menu .ui-menu .ui-selectmenu-optgroup {
	font-size: 1em;
	font-weight: bold;
	line-height: 1.5;
	padding: 2px 0.4em;
	margin: 0.5em 0 0 0;
	height: auto;
	border: 0;
}
.ui-selectmenu-open {
	display: block;
}
.ui-selectmenu-text {
	display: block;
	margin-right: 20px;
	overflow: hidden;
	text-overflow: ellipsis;
}
.ui-selectmenu-button.ui-button {
	text-align: left;
	white-space: nowrap;
	width: 14em;
}
.ui-selectmenu-icon.ui-icon {
	float: right;
	margin-top: 0;
}
.ui-slider {
	position: relative;
	text-align: left;
}
.ui-slider .ui-slider-handle {
	position: absolute;
	z-index: 2;
	width: 1.2em;
	height: 1.2em;
	cursor: default;
	-ms-touch-action: none;
	touch-action: none;
}
.ui-slider .ui-slider-range {
	position: absolute;
	z-index: 1;
	font-size: .7em;
	display: block;
	border: 0;
	background-position: 0 0;
}


.ui-slider.ui-state-disabled .ui-slider-handle,
.ui-slider.ui-state-disabled .ui-slider-range {
	filter: inherit;
}

.ui-slider-horizontal {
	height: .8em;
}
.ui-slider-horizontal .ui-slider-handle {
	top: -.3em;
	margin-left: -.6em;
}
.ui-slider-horizontal .ui-slider-range {
	top: 0;
	height: 100%;
}
.ui-slider-horizontal .ui-slider-range-min {
	left: 0;
}
.ui-slider-horizontal .ui-slider-range-max {
	right: 0;
}

.ui-slider-vertical {
	width: .8em;
	height: 100px;
}
.ui-slider-vertical .ui-slider-handle {
	left: -.3em;
	margin-left: 0;
	margin-bottom: -.6em;
}
.ui-slider-vertical .ui-slider-range {
	left: 0;
	width: 100%;
}
.ui-slider-vertical .ui-slider-range-min {
	bottom: 0;
}
.ui-slider-vertical .ui-slider-range-max {
	top: 0;
}
.ui-sortable-handle {
	-ms-touch-action: none;
	touch-action: none;
}
.ui-spinner {
	position: relative;
	display: inline-block;
	overflow: hidden;
	padding: 0;
	vertical-align: middle;
}
.ui-spinner-input {
	border: none;
	background: none;
	color: inherit;
	padding: .222em 0;
	margin: .2em 0;
	vertical-align: middle;
	margin-left: .4em;
	margin-right: 2em;
}
.ui-spinner-button {
	width: 1.6em;
	height: 50%;
	font-size: .5em;
	padding: 0;
	margin: 0;
	text-align: center;
	position: absolute;
	cursor: default;
	display: block;
	overflow: hidden;
	right: 0;
}

.ui-spinner a.ui-spinner-button {
	border-top-style: none;
	border-bottom-style: none;
	border-right-style: none;
}
.ui-spinner-up {
	top: 0;
}
.ui-spinner-down {
	bottom: 0;
}
.ui-tabs {
	position: relative;
	padding: .2em;
}
.ui-tabs .ui-tabs-nav {
	margin: 0;
	padding: .2em .2em 0;
}
.ui-tabs .ui-tabs-nav li {
	list-style: none;
	float: left;
	position: relative;
	top: 0;
	margin: 1px .2em 0 0;
	border-bottom-width: 0;
	padding: 0;
	white-space: nowrap;
}
.ui-tabs .ui-tabs-nav .ui-tabs-anchor {
	float: left;
	padding: .5em 1em;
	text-decoration: none;
}
.ui-tabs .ui-tabs-nav li.ui-tabs-active {
	margin-bottom: -1px;
	padding-bottom: 1px;
}
.ui-tabs .ui-tabs-nav li.ui-tabs-active .ui-tabs-anchor,
.ui-tabs .ui-tabs-nav li.ui-state-disabled .ui-tabs-anchor,
.ui-tabs .ui-tabs-nav li.ui-tabs-loading .ui-tabs-anchor {
	cursor: text;
}
.ui-tabs-collapsible .ui-tabs-nav li.ui-tabs-active .ui-tabs-anchor {
	cursor: pointer;
}
.ui-tabs .ui-tabs-panel {
	display: block;
	border-width: 0;
	padding: 1em 1.4em;
	background: none;
}
.ui-tooltip {
	padding: 8px;
	position: absolute;
	z-index: 9999;
	max-width: 300px;
}
body .ui-tooltip {
	border-width: 2px;
}

.ui-widget {
	font-family: Arial,Helvetica,sans-serif;
	font-size: 1em;
}
.ui-widget .ui-widget {
	font-size: 1em;
}
.ui-widget input,
.ui-widget select,
.ui-widget textarea,
.ui-widget button {
	font-family: Arial,Helvetica,sans-serif;
	font-size: 1em;
}
.ui-widget.ui-widget-content {
	border: 1px solid #c5c5c5;
}
.ui-widget-content {
	border: 1px solid #dddddd;
	background: #ffffff;
	color: #333333;
}
.ui-widget-content a {
	color: #333333;
}
.ui-widget-header {
	border: 1px solid #dddddd;
	background: #e9e9e9;
	color: #333333;
	font-weight: bold;
}
.ui-widget-header a {
	color: #333333;
}


.ui-state-default,
.ui-widget-content .ui-state-default,
.ui-widget-header .ui-state-default,
.ui-button,


html .ui-button.ui-state-disabled:hover,
html .ui-button.ui-state-disabled:active {
	border: 1px solid #c5c5c5;
	background: #f6f6f6;
	font-weight: normal;
	color: #454545;
}
.ui-state-default a,
.ui-state-default a:link,
.ui-state-default a:visited,
a.ui-button,
a:link.ui-button,
a:visited.ui-button,
.ui-button {
	color: #454545;
	text-decoration: none;
}
.ui-state-hover,
.ui-widget-content .ui-state-hover,
.ui-widget-header .ui-state-hover,
.ui-state-focus,
.ui-widget-content .ui-state-focus,
.ui-widget-header .ui-state-focus,
.ui-button:hover,
.ui-button:focus {
	border: 1px solid #cccccc;
	background: #ededed;
	font-weight: normal;
	color: #2b2b2b;
}
.ui-state-hover a,
.ui-state-hover a:hover,
.ui-state-hover a:link,
.ui-state-hover a:visited,
.ui-state-focus a,
.ui-state-focus a:hover,
.ui-state-focus a:link,
.ui-state-focus a:visited,
a.ui-button:hover,
a.ui-button:focus {
	color: #2b2b2b;
	text-decoration: none;
}

.ui-visual-focus {
	box-shadow: 0 0 3px 1px rgb(94, 158, 214);
}
.ui-state-active,
.ui-widget-content .ui-state-active,
.ui-widget-header .ui-state-active,
a.ui-button:active,
.ui-button:active,
.ui-button.ui-state-active:hover {
	border: 1px solid #003eff;
	background: #007fff;
	font-weight: normal;
	color: #ffffff;
}
.ui-icon-background,
.ui-state-active .ui-icon-background {
	border: #003eff;
	background-color: #ffffff;
}
.ui-state-active a,
.ui-state-active a:link,
.ui-state-active a:visited {
	color: #ffffff;
	text-decoration: none;
}


.ui-state-highlight,
.ui-widget-content .ui-state-highlight,
.ui-widget-header .ui-state-highlight {
	border: 1px solid #dad55e;
	background: #fffa90;
	color: #777620;
}
.ui-state-checked {
	border: 1px solid #dad55e;
	background: #fffa90;
}
.ui-state-highlight a,
.ui-widget-content .ui-state-highlight a,
.ui-widget-header .ui-state-highlight a {
	color: #777620;
}
.ui-state-error,
.ui-widget-content .ui-state-error,
.ui-widget-header .ui-state-error {
	border: 1px solid #f1a899;
	background: #fddfdf;
	color: #5f3f3f;
}
.ui-state-error a,
.ui-widget-content .ui-state-error a,
.ui-widget-header .ui-state-error a {
	color: #5f3f3f;
}
.ui-state-error-text,
.ui-widget-content .ui-state-error-text,
.ui-widget-header .ui-state-error-text {
	color: #5f3f3f;
}
.ui-priority-primary,
.ui-widget-content .ui-priority-primary,
.ui-widget-header .ui-priority-primary {
	font-weight: bold;
}
.ui-priority-secondary,
.ui-widget-content .ui-priority-secondary,
.ui-widget-header .ui-priority-secondary {
	opacity: .7;
	filter:Alpha(Opacity=70); 
	font-weight: normal;
}
.ui-state-disabled,
.ui-widget-content .ui-state-disabled,
.ui-widget-header .ui-state-disabled {
	opacity: .35;
	filter:Alpha(Opacity=35); 
	background-image: none;
}
.ui-state-disabled .ui-icon {
	filter:Alpha(Opacity=35); 
}




.ui-icon {
	width: 16px;
	height: 16px;
}
.ui-icon,
.ui-widget-content .ui-icon {
	background-image: url("images/ui-icons_444444_256x240.png");
}
.ui-widget-header .ui-icon {
	background-image: url("images/ui-icons_444444_256x240.png");
}
.ui-state-hover .ui-icon,
.ui-state-focus .ui-icon,
.ui-button:hover .ui-icon,
.ui-button:focus .ui-icon {
	background-image: url("images/ui-icons_555555_256x240.png");
}
.ui-state-active .ui-icon,
.ui-button:active .ui-icon {
	background-image: url("images/ui-icons_ffffff_256x240.png");
}
.ui-state-highlight .ui-icon,
.ui-button .ui-state-highlight.ui-icon {
	background-image: url("images/ui-icons_777620_256x240.png");
}
.ui-state-error .ui-icon,
.ui-state-error-text .ui-icon {
	background-image: url("images/ui-icons_cc0000_256x240.png");
}
.ui-button .ui-icon {
	background-image: url("images/ui-icons_777777_256x240.png");
}


.ui-icon-blank { background-position: 16px 16px; }
.ui-icon-caret-1-n { background-position: 0 0; }
.ui-icon-caret-1-ne { background-position: -16px 0; }
.ui-icon-caret-1-e { background-position: -32px 0; }
.ui-icon-caret-1-se { background-position: -48px 0; }
.ui-icon-caret-1-s { background-position: -65px 0; }
.ui-icon-caret-1-sw { background-position: -80px 0; }
.ui-icon-caret-1-w { background-position: -96px 0; }
.ui-icon-caret-1-nw { background-position: -112px 0; }
.ui-icon-caret-2-n-s { background-position: -128px 0; }
.ui-icon-caret-2-e-w { background-position: -144px 0; }
.ui-icon-triangle-1-n { background-position: 0 -16px; }
.ui-icon-triangle-1-ne { background-position: -16px -16px; }
.ui-icon-triangle-1-e { background-position: -32px -16px; }
.ui-icon-triangle-1-se { background-position: -48px -16px; }
.ui-icon-triangle-1-s { background-position: -65px -16px; }
.ui-icon-triangle-1-sw { background-position: -80px -16px; }
.ui-icon-triangle-1-w { background-position: -96px -16px; }
.ui-icon-triangle-1-nw { background-position: -112px -16px; }
.ui-icon-triangle-2-n-s { background-position: -128px -16px; }
.ui-icon-triangle-2-e-w { background-position: -144px -16px; }
.ui-icon-arrow-1-n { background-position: 0 -32px; }
.ui-icon-arrow-1-ne { background-position: -16px -32px; }
.ui-icon-arrow-1-e { background-position: -32px -32px; }
.ui-icon-arrow-1-se { background-position: -48px -32px; }
.ui-icon-arrow-1-s { background-position: -65px -32px; }
.ui-icon-arrow-1-sw { background-position: -80px -32px; }
.ui-icon-arrow-1-w { background-position: -96px -32px; }
.ui-icon-arrow-1-nw { background-position: -112px -32px; }
.ui-icon-arrow-2-n-s { background-position: -128px -32px; }
.ui-icon-arrow-2-ne-sw { background-position: -144px -32px; }
.ui-icon-arrow-2-e-w { background-position: -160px -32px; }
.ui-icon-arrow-2-se-nw { background-position: -176px -32px; }
.ui-icon-arrowstop-1-n { background-position: -192px -32px; }
.ui-icon-arrowstop-1-e { background-position: -208px -32px; }
.ui-icon-arrowstop-1-s { background-position: -224px -32px; }
.ui-icon-arrowstop-1-w { background-position: -240px -32px; }
.ui-icon-arrowthick-1-n { background-position: 1px -48px; }
.ui-icon-arrowthick-1-ne { background-position: -16px -48px; }
.ui-icon-arrowthick-1-e { background-position: -32px -48px; }
.ui-icon-arrowthick-1-se { background-position: -48px -48px; }
.ui-icon-arrowthick-1-s { background-position: -64px -48px; }
.ui-icon-arrowthick-1-sw { background-position: -80px -48px; }
.ui-icon-arrowthick-1-w { background-position: -96px -48px; }
.ui-icon-arrowthick-1-nw { background-position: -112px -48px; }
.ui-icon-arrowthick-2-n-s { background-position: -128px -48px; }
.ui-icon-arrowthick-2-ne-sw { background-position: -144px -48px; }
.ui-icon-arrowthick-2-e-w { background-position: -160px -48px; }
.ui-icon-arrowthick-2-se-nw { background-position: -176px -48px; }
.ui-icon-arrowthickstop-1-n { background-position: -192px -48px; }
.ui-icon-arrowthickstop-1-e { background-position: -208px -48px; }
.ui-icon-arrowthickstop-1-s { background-position: -224px -48px; }
.ui-icon-arrowthickstop-1-w { background-position: -240px -48px; }
.ui-icon-arrowreturnthick-1-w { background-position: 0 -64px; }
.ui-icon-arrowreturnthick-1-n { background-position: -16px -64px; }
.ui-icon-arrowreturnthick-1-e { background-position: -32px -64px; }
.ui-icon-arrowreturnthick-1-s { background-position: -48px -64px; }
.ui-icon-arrowreturn-1-w { background-position: -64px -64px; }
.ui-icon-arrowreturn-1-n { background-position: -80px -64px; }
.ui-icon-arrowreturn-1-e { background-position: -96px -64px; }
.ui-icon-arrowreturn-1-s { background-position: -112px -64px; }
.ui-icon-arrowrefresh-1-w { background-position: -128px -64px; }
.ui-icon-arrowrefresh-1-n { background-position: -144px -64px; }
.ui-icon-arrowrefresh-1-e { background-position: -160px -64px; }
.ui-icon-arrowrefresh-1-s { background-position: -176px -64px; }
.ui-icon-arrow-4 { background-position: 0 -80px; }
.ui-icon-arrow-4-diag { background-position: -16px -80px; }
.ui-icon-extlink { background-position: -32px -80px; }
.ui-icon-newwin { background-position: -48px -80px; }
.ui-icon-refresh { background-position: -64px -80px; }
.ui-icon-shuffle { background-position: -80px -80px; }
.ui-icon-transfer-e-w { background-position: -96px -80px; }
.ui-icon-transferthick-e-w { background-position: -112px -80px; }
.ui-icon-folder-collapsed { background-position: 0 -96px; }
.ui-icon-folder-open { background-position: -16px -96px; }
.ui-icon-document { background-position: -32px -96px; }
.ui-icon-document-b { background-position: -48px -96px; }
.ui-icon-note { background-position: -64px -96px; }
.ui-icon-mail-closed { background-position: -80px -96px; }
.ui-icon-mail-open { background-position: -96px -96px; }
.ui-icon-suitcase { background-position: -112px -96px; }
.ui-icon-comment { background-position: -128px -96px; }
.ui-icon-person { background-position: -144px -96px; }
.ui-icon-print { background-position: -160px -96px; }
.ui-icon-trash { background-position: -176px -96px; }
.ui-icon-locked { background-position: -192px -96px; }
.ui-icon-unlocked { background-position: -208px -96px; }
.ui-icon-bookmark { background-position: -224px -96px; }
.ui-icon-tag { background-position: -240px -96px; }
.ui-icon-home { background-position: 0 -112px; }
.ui-icon-flag { background-position: -16px -112px; }
.ui-icon-calendar { background-position: -32px -112px; }
.ui-icon-cart { background-position: -48px -112px; }
.ui-icon-pencil { background-position: -64px -112px; }
.ui-icon-clock { background-position: -80px -112px; }
.ui-icon-disk { background-position: -96px -112px; }
.ui-icon-calculator { background-position: -112px -112px; }
.ui-icon-zoomin { background-position: -128px -112px; }
.ui-icon-zoomout { background-position: -144px -112px; }
.ui-icon-search { background-position: -160px -112px; }
.ui-icon-wrench { background-position: -176px -112px; }
.ui-icon-gear { background-position: -192px -112px; }
.ui-icon-heart { background-position: -208px -112px; }
.ui-icon-star { background-position: -224px -112px; }
.ui-icon-link { background-position: -240px -112px; }
.ui-icon-cancel { background-position: 0 -128px; }
.ui-icon-plus { background-position: -16px -128px; }
.ui-icon-plusthick { background-position: -32px -128px; }
.ui-icon-minus { background-position: -48px -128px; }
.ui-icon-minusthick { background-position: -64px -128px; }
.ui-icon-close { background-position: -80px -128px; }
.ui-icon-closethick { background-position: -96px -128px; }
.ui-icon-key { background-position: -112px -128px; }
.ui-icon-lightbulb { background-position: -128px -128px; }
.ui-icon-scissors { background-position: -144px -128px; }
.ui-icon-clipboard { background-position: -160px -128px; }
.ui-icon-copy { background-position: -176px -128px; }
.ui-icon-contact { background-position: -192px -128px; }
.ui-icon-image { background-position: -208px -128px; }
.ui-icon-video { background-position: -224px -128px; }
.ui-icon-script { background-position: -240px -128px; }
.ui-icon-alert { background-position: 0 -144px; }
.ui-icon-info { background-position: -16px -144px; }
.ui-icon-notice { background-position: -32px -144px; }
.ui-icon-help { background-position: -48px -144px; }
.ui-icon-check { background-position: -64px -144px; }
.ui-icon-bullet { background-position: -80px -144px; }
.ui-icon-radio-on { background-position: -96px -144px; }
.ui-icon-radio-off { background-position: -112px -144px; }
.ui-icon-pin-w { background-position: -128px -144px; }
.ui-icon-pin-s { background-position: -144px -144px; }
.ui-icon-play { background-position: 0 -160px; }
.ui-icon-pause { background-position: -16px -160px; }
.ui-icon-seek-next { background-position: -32px -160px; }
.ui-icon-seek-prev { background-position: -48px -160px; }
.ui-icon-seek-end { background-position: -64px -160px; }
.ui-icon-seek-start { background-position: -80px -160px; }

.ui-icon-seek-first { background-position: -80px -160px; }
.ui-icon-stop { background-position: -96px -160px; }
.ui-icon-eject { background-position: -112px -160px; }
.ui-icon-volume-off { background-position: -128px -160px; }
.ui-icon-volume-on { background-position: -144px -160px; }
.ui-icon-power { background-position: 0 -176px; }
.ui-icon-signal-diag { background-position: -16px -176px; }
.ui-icon-signal { background-position: -32px -176px; }
.ui-icon-battery-0 { background-position: -48px -176px; }
.ui-icon-battery-1 { background-position: -64px -176px; }
.ui-icon-battery-2 { background-position: -80px -176px; }
.ui-icon-battery-3 { background-position: -96px -176px; }
.ui-icon-circle-plus { background-position: 0 -192px; }
.ui-icon-circle-minus { background-position: -16px -192px; }
.ui-icon-circle-close { background-position: -32px -192px; }
.ui-icon-circle-triangle-e { background-position: -48px -192px; }
.ui-icon-circle-triangle-s { background-position: -64px -192px; }
.ui-icon-circle-triangle-w { background-position: -80px -192px; }
.ui-icon-circle-triangle-n { background-position: -96px -192px; }
.ui-icon-circle-arrow-e { background-position: -112px -192px; }
.ui-icon-circle-arrow-s { background-position: -128px -192px; }
.ui-icon-circle-arrow-w { background-position: -144px -192px; }
.ui-icon-circle-arrow-n { background-position: -160px -192px; }
.ui-icon-circle-zoomin { background-position: -176px -192px; }
.ui-icon-circle-zoomout { background-position: -192px -192px; }
.ui-icon-circle-check { background-position: -208px -192px; }
.ui-icon-circlesmall-plus { background-position: 0 -208px; }
.ui-icon-circlesmall-minus { background-position: -16px -208px; }
.ui-icon-circlesmall-close { background-position: -32px -208px; }
.ui-icon-squaresmall-plus { background-position: -48px -208px; }
.ui-icon-squaresmall-minus { background-position: -64px -208px; }
.ui-icon-squaresmall-close { background-position: -80px -208px; }
.ui-icon-grip-dotted-vertical { background-position: 0 -224px; }
.ui-icon-grip-dotted-horizontal { background-position: -16px -224px; }
.ui-icon-grip-solid-vertical { background-position: -32px -224px; }
.ui-icon-grip-solid-horizontal { background-position: -48px -224px; }
.ui-icon-gripsmall-diagonal-se { background-position: -64px -224px; }
.ui-icon-grip-diagonal-se { background-position: -80px -224px; }





.ui-corner-all,
.ui-corner-top,
.ui-corner-left,
.ui-corner-tl {
	border-top-left-radius: 3px;
}
.ui-corner-all,
.ui-corner-top,
.ui-corner-right,
.ui-corner-tr {
	border-top-right-radius: 3px;
}
.ui-corner-all,
.ui-corner-bottom,
.ui-corner-left,
.ui-corner-bl {
	border-bottom-left-radius: 3px;
}
.ui-corner-all,
.ui-corner-bottom,
.ui-corner-right,
.ui-corner-br {
	border-bottom-right-radius: 3px;
}


.ui-widget-overlay {
	background: #aaaaaa;
	opacity: .3;
	filter: Alpha(Opacity=30); 
}
.ui-widget-shadow {
	-webkit-box-shadow: 0px 0px 5px #666666;
	box-shadow: 0px 0px 5px #666666;
} 
</style>
<script src='js/jquery-1.12.4.js'></script>
<script src='js/jquery-ui.js'></script>

<script>
$( function() {
	$( '#tabs-collect-consensus-heatmap' ).tabs();
} );
</script>
<div id='tabs-collect-consensus-heatmap'>
<ul>
<li><a href='#tab-collect-consensus-heatmap-1'>k = 2</a></li>
<li><a href='#tab-collect-consensus-heatmap-2'>k = 3</a></li>
<li><a href='#tab-collect-consensus-heatmap-3'>k = 4</a></li>
<li><a href='#tab-collect-consensus-heatmap-4'>k = 5</a></li>
<li><a href='#tab-collect-consensus-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-collect-consensus-heatmap-1'>
<pre><code class="r">collect_plots(res_list, k = 2, fun = consensus_heatmap, mc.cores = 4)
</code></pre>

<p><img src="figure_cola/tab-collect-consensus-heatmap-1-1.png" alt="plot of chunk tab-collect-consensus-heatmap-1"/></p>

</div>
<div id='tab-collect-consensus-heatmap-2'>
<pre><code class="r">collect_plots(res_list, k = 3, fun = consensus_heatmap, mc.cores = 4)
</code></pre>

<p><img src="figure_cola/tab-collect-consensus-heatmap-2-1.png" alt="plot of chunk tab-collect-consensus-heatmap-2"/></p>

</div>
<div id='tab-collect-consensus-heatmap-3'>
<pre><code class="r">collect_plots(res_list, k = 4, fun = consensus_heatmap, mc.cores = 4)
</code></pre>

<p><img src="figure_cola/tab-collect-consensus-heatmap-3-1.png" alt="plot of chunk tab-collect-consensus-heatmap-3"/></p>

</div>
<div id='tab-collect-consensus-heatmap-4'>
<pre><code class="r">collect_plots(res_list, k = 5, fun = consensus_heatmap, mc.cores = 4)
</code></pre>

<p><img src="figure_cola/tab-collect-consensus-heatmap-4-1.png" alt="plot of chunk tab-collect-consensus-heatmap-4"/></p>

</div>
<div id='tab-collect-consensus-heatmap-5'>
<pre><code class="r">collect_plots(res_list, k = 6, fun = consensus_heatmap, mc.cores = 4)
</code></pre>

<p><img src="figure_cola/tab-collect-consensus-heatmap-5-1.png" alt="plot of chunk tab-collect-consensus-heatmap-5"/></p>

</div>
</div>



### Membership heatmap

Membership heatmaps for all methods. ([What is a membership heatmap?](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/cola.html#toc_12))


<script>
$( function() {
	$( '#tabs-collect-membership-heatmap' ).tabs();
} );
</script>
<div id='tabs-collect-membership-heatmap'>
<ul>
<li><a href='#tab-collect-membership-heatmap-1'>k = 2</a></li>
<li><a href='#tab-collect-membership-heatmap-2'>k = 3</a></li>
<li><a href='#tab-collect-membership-heatmap-3'>k = 4</a></li>
<li><a href='#tab-collect-membership-heatmap-4'>k = 5</a></li>
<li><a href='#tab-collect-membership-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-collect-membership-heatmap-1'>
<pre><code class="r">collect_plots(res_list, k = 2, fun = membership_heatmap, mc.cores = 4)
</code></pre>

<p><img src="figure_cola/tab-collect-membership-heatmap-1-1.png" alt="plot of chunk tab-collect-membership-heatmap-1"/></p>

</div>
<div id='tab-collect-membership-heatmap-2'>
<pre><code class="r">collect_plots(res_list, k = 3, fun = membership_heatmap, mc.cores = 4)
</code></pre>

<p><img src="figure_cola/tab-collect-membership-heatmap-2-1.png" alt="plot of chunk tab-collect-membership-heatmap-2"/></p>

</div>
<div id='tab-collect-membership-heatmap-3'>
<pre><code class="r">collect_plots(res_list, k = 4, fun = membership_heatmap, mc.cores = 4)
</code></pre>

<p><img src="figure_cola/tab-collect-membership-heatmap-3-1.png" alt="plot of chunk tab-collect-membership-heatmap-3"/></p>

</div>
<div id='tab-collect-membership-heatmap-4'>
<pre><code class="r">collect_plots(res_list, k = 5, fun = membership_heatmap, mc.cores = 4)
</code></pre>

<p><img src="figure_cola/tab-collect-membership-heatmap-4-1.png" alt="plot of chunk tab-collect-membership-heatmap-4"/></p>

</div>
<div id='tab-collect-membership-heatmap-5'>
<pre><code class="r">collect_plots(res_list, k = 6, fun = membership_heatmap, mc.cores = 4)
</code></pre>

<p><img src="figure_cola/tab-collect-membership-heatmap-5-1.png" alt="plot of chunk tab-collect-membership-heatmap-5"/></p>

</div>
</div>



### Signature heatmap

Signature heatmaps for all methods. ([What is a signature heatmap?](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/cola.html#toc_22))


Note in following heatmaps, rows are scaled.



<script>
$( function() {
	$( '#tabs-collect-get-signatures' ).tabs();
} );
</script>
<div id='tabs-collect-get-signatures'>
<ul>
<li><a href='#tab-collect-get-signatures-1'>k = 2</a></li>
<li><a href='#tab-collect-get-signatures-2'>k = 3</a></li>
<li><a href='#tab-collect-get-signatures-3'>k = 4</a></li>
<li><a href='#tab-collect-get-signatures-4'>k = 5</a></li>
<li><a href='#tab-collect-get-signatures-5'>k = 6</a></li>
</ul>
<div id='tab-collect-get-signatures-1'>
<pre><code class="r">collect_plots(res_list, k = 2, fun = get_signatures, mc.cores = 4)
</code></pre>

<p><img src="figure_cola/tab-collect-get-signatures-1-1.png" alt="plot of chunk tab-collect-get-signatures-1"/></p>

</div>
<div id='tab-collect-get-signatures-2'>
<pre><code class="r">collect_plots(res_list, k = 3, fun = get_signatures, mc.cores = 4)
</code></pre>

<p><img src="figure_cola/tab-collect-get-signatures-2-1.png" alt="plot of chunk tab-collect-get-signatures-2"/></p>

</div>
<div id='tab-collect-get-signatures-3'>
<pre><code class="r">collect_plots(res_list, k = 4, fun = get_signatures, mc.cores = 4)
</code></pre>

<p><img src="figure_cola/tab-collect-get-signatures-3-1.png" alt="plot of chunk tab-collect-get-signatures-3"/></p>

</div>
<div id='tab-collect-get-signatures-4'>
<pre><code class="r">collect_plots(res_list, k = 5, fun = get_signatures, mc.cores = 4)
</code></pre>

<p><img src="figure_cola/tab-collect-get-signatures-4-1.png" alt="plot of chunk tab-collect-get-signatures-4"/></p>

</div>
<div id='tab-collect-get-signatures-5'>
<pre><code class="r">collect_plots(res_list, k = 6, fun = get_signatures, mc.cores = 4)
</code></pre>

<p><img src="figure_cola/tab-collect-get-signatures-5-1.png" alt="plot of chunk tab-collect-get-signatures-5"/></p>

</div>
</div>



### Statistics table

The statistics used for measuring the stability of consensus partitioning.
([How are they
defined?](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/cola.html#toc_13))


<script>
$( function() {
	$( '#tabs-get-stats-from-consensus-partition-list' ).tabs();
} );
</script>
<div id='tabs-get-stats-from-consensus-partition-list'>
<ul>
<li><a href='#tab-get-stats-from-consensus-partition-list-1'>k = 2</a></li>
<li><a href='#tab-get-stats-from-consensus-partition-list-2'>k = 3</a></li>
<li><a href='#tab-get-stats-from-consensus-partition-list-3'>k = 4</a></li>
<li><a href='#tab-get-stats-from-consensus-partition-list-4'>k = 5</a></li>
<li><a href='#tab-get-stats-from-consensus-partition-list-5'>k = 6</a></li>
</ul>
<div id='tab-get-stats-from-consensus-partition-list-1'>
<pre><code class="r">get_stats(res_list, k = 2)
</code></pre>

<pre><code>#&gt;             k 1-PAC mean_silhouette concordance area_increased  Rand Jaccard
#&gt; SD:NMF      2 1.000           0.956       0.981          0.406 0.586   0.586
#&gt; CV:NMF      2 1.000           0.953       0.981          0.418 0.570   0.570
#&gt; MAD:NMF     2 1.000           0.956       0.982          0.424 0.570   0.570
#&gt; ATC:NMF     2 0.882           0.906       0.965          0.328 0.688   0.688
#&gt; SD:skmeans  2 1.000           0.991       0.995          0.471 0.531   0.531
#&gt; CV:skmeans  2 0.922           0.934       0.973          0.501 0.499   0.499
#&gt; MAD:skmeans 2 1.000           0.982       0.987          0.472 0.531   0.531
#&gt; ATC:skmeans 2 1.000           0.980       0.991          0.510 0.491   0.491
#&gt; SD:mclust   2 1.000           0.951       0.963          0.265 0.766   0.766
#&gt; CV:mclust   2 0.820           0.896       0.959          0.245 0.795   0.795
#&gt; MAD:mclust  2 1.000           0.951       0.969          0.264 0.766   0.766
#&gt; ATC:mclust  2 0.403           0.849       0.845          0.431 0.543   0.543
#&gt; SD:kmeans   2 0.742           0.822       0.907          0.379 0.586   0.586
#&gt; CV:kmeans   2 0.333           0.730       0.840          0.394 0.543   0.543
#&gt; MAD:kmeans  2 0.420           0.837       0.888          0.439 0.531   0.531
#&gt; ATC:kmeans  2 0.813           0.833       0.925          0.480 0.505   0.505
#&gt; SD:pam      2 0.710           0.875       0.926          0.487 0.512   0.512
#&gt; CV:pam      2 0.429           0.743       0.846          0.468 0.543   0.543
#&gt; MAD:pam     2 0.418           0.606       0.797          0.453 0.505   0.505
#&gt; ATC:pam     2 0.958           0.936       0.974          0.508 0.491   0.491
#&gt; SD:hclust   2 0.858           0.955       0.979          0.262 0.766   0.766
#&gt; CV:hclust   2 0.637           0.855       0.943          0.286 0.766   0.766
#&gt; MAD:hclust  2 0.960           0.955       0.979          0.262 0.766   0.766
#&gt; ATC:hclust  2 0.362           0.687       0.793          0.438 0.570   0.570
</code></pre>

</div>
<div id='tab-get-stats-from-consensus-partition-list-2'>
<pre><code class="r">get_stats(res_list, k = 3)
</code></pre>

<pre><code>#&gt;             k 1-PAC mean_silhouette concordance area_increased  Rand Jaccard
#&gt; SD:NMF      3 0.808           0.855       0.941          0.608 0.669   0.476
#&gt; CV:NMF      3 0.740           0.822       0.926          0.578 0.705   0.510
#&gt; MAD:NMF     3 0.732           0.837       0.929          0.551 0.660   0.460
#&gt; ATC:NMF     3 0.963           0.946       0.978          0.791 0.627   0.492
#&gt; SD:skmeans  3 0.953           0.930       0.966          0.439 0.791   0.607
#&gt; CV:skmeans  3 0.544           0.801       0.871          0.351 0.714   0.483
#&gt; MAD:skmeans 3 0.816           0.912       0.961          0.436 0.743   0.537
#&gt; ATC:skmeans 3 0.975           0.939       0.976          0.318 0.768   0.558
#&gt; SD:mclust   3 0.376           0.702       0.820          1.101 0.721   0.635
#&gt; CV:mclust   3 0.374           0.739       0.831          0.850 0.840   0.800
#&gt; MAD:mclust  3 0.665           0.816       0.904          1.227 0.634   0.523
#&gt; ATC:mclust  3 0.418           0.723       0.841          0.450 0.669   0.453
#&gt; SD:kmeans   3 0.576           0.875       0.909          0.574 0.594   0.411
#&gt; CV:kmeans   3 0.255           0.533       0.682          0.494 0.746   0.576
#&gt; MAD:kmeans  3 0.563           0.853       0.899          0.396 0.586   0.372
#&gt; ATC:kmeans  3 0.900           0.903       0.962          0.299 0.726   0.528
#&gt; SD:pam      3 0.636           0.765       0.876          0.363 0.759   0.558
#&gt; CV:pam      3 0.469           0.727       0.846          0.200 0.910   0.834
#&gt; MAD:pam     3 0.833           0.889       0.939          0.469 0.704   0.478
#&gt; ATC:pam     3 1.000           0.976       0.991          0.214 0.878   0.755
#&gt; SD:hclust   3 0.630           0.776       0.891          0.866 0.826   0.773
#&gt; CV:hclust   3 0.708           0.802       0.933          0.366 0.878   0.841
#&gt; MAD:hclust  3 0.477           0.635       0.851          0.892 0.826   0.773
#&gt; ATC:hclust  3 0.505           0.739       0.830          0.398 0.734   0.542
</code></pre>

</div>
<div id='tab-get-stats-from-consensus-partition-list-3'>
<pre><code class="r">get_stats(res_list, k = 4)
</code></pre>

<pre><code>#&gt;             k 1-PAC mean_silhouette concordance area_increased  Rand Jaccard
#&gt; SD:NMF      4 0.649           0.700       0.848         0.1092 0.838   0.584
#&gt; CV:NMF      4 0.587           0.626       0.793         0.1341 0.816   0.525
#&gt; MAD:NMF     4 0.633           0.721       0.843         0.1167 0.853   0.615
#&gt; ATC:NMF     4 0.503           0.619       0.811         0.1690 0.713   0.427
#&gt; SD:skmeans  4 0.781           0.833       0.890         0.1170 0.866   0.618
#&gt; CV:skmeans  4 0.743           0.801       0.884         0.1234 0.882   0.655
#&gt; MAD:skmeans 4 0.726           0.768       0.871         0.1149 0.839   0.556
#&gt; ATC:skmeans 4 0.865           0.938       0.950         0.1006 0.896   0.701
#&gt; SD:mclust   4 0.442           0.455       0.756         0.2213 0.830   0.657
#&gt; CV:mclust   4 0.491           0.547       0.780         0.4708 0.642   0.455
#&gt; MAD:mclust  4 0.669           0.698       0.853         0.2223 0.816   0.568
#&gt; ATC:mclust  4 0.514           0.375       0.648         0.1433 0.774   0.479
#&gt; SD:kmeans   4 0.550           0.379       0.730         0.1707 0.925   0.815
#&gt; CV:kmeans   4 0.331           0.557       0.711         0.1700 0.764   0.503
#&gt; MAD:kmeans  4 0.607           0.576       0.762         0.1516 0.939   0.838
#&gt; ATC:kmeans  4 0.734           0.716       0.794         0.1463 0.902   0.747
#&gt; SD:pam      4 0.712           0.779       0.889         0.0838 0.945   0.836
#&gt; CV:pam      4 0.481           0.446       0.725         0.1741 0.766   0.535
#&gt; MAD:pam     4 0.824           0.803       0.914         0.1142 0.866   0.631
#&gt; ATC:pam     4 0.859           0.872       0.936         0.1672 0.852   0.630
#&gt; SD:hclust   4 0.587           0.623       0.781         0.1640 0.686   0.491
#&gt; CV:hclust   4 0.390           0.591       0.785         0.6554 0.680   0.503
#&gt; MAD:hclust  4 0.487           0.673       0.789         0.2840 0.710   0.526
#&gt; ATC:hclust  4 0.597           0.721       0.785         0.1327 1.000   1.000
</code></pre>

</div>
<div id='tab-get-stats-from-consensus-partition-list-4'>
<pre><code class="r">get_stats(res_list, k = 5)
</code></pre>

<pre><code>#&gt;             k 1-PAC mean_silhouette concordance area_increased  Rand Jaccard
#&gt; SD:NMF      5 0.828           0.876       0.932         0.0901 0.885   0.611
#&gt; CV:NMF      5 0.745           0.651       0.841         0.0677 0.845   0.495
#&gt; MAD:NMF     5 0.858           0.864       0.930         0.0806 0.902   0.657
#&gt; ATC:NMF     5 0.539           0.547       0.762         0.0961 0.797   0.464
#&gt; SD:skmeans  5 0.846           0.788       0.905         0.0578 0.946   0.783
#&gt; CV:skmeans  5 0.755           0.735       0.860         0.0611 0.903   0.638
#&gt; MAD:skmeans 5 0.843           0.801       0.904         0.0603 0.907   0.651
#&gt; ATC:skmeans 5 0.934           0.919       0.940         0.0765 0.930   0.741
#&gt; SD:mclust   5 0.447           0.532       0.695         0.0759 0.845   0.567
#&gt; CV:mclust   5 0.576           0.607       0.767         0.1396 0.820   0.501
#&gt; MAD:mclust  5 0.607           0.542       0.733         0.0714 0.925   0.723
#&gt; ATC:mclust  5 0.586           0.498       0.607         0.0864 0.765   0.388
#&gt; SD:kmeans   5 0.656           0.743       0.811         0.0992 0.811   0.496
#&gt; CV:kmeans   5 0.539           0.753       0.793         0.1076 0.838   0.529
#&gt; MAD:kmeans  5 0.662           0.678       0.793         0.0888 0.845   0.552
#&gt; ATC:kmeans  5 0.847           0.920       0.923         0.0946 0.881   0.615
#&gt; SD:pam      5 0.768           0.801       0.891         0.0396 0.972   0.900
#&gt; CV:pam      5 0.597           0.664       0.849         0.0970 0.829   0.550
#&gt; MAD:pam     5 0.785           0.648       0.822         0.0357 0.950   0.818
#&gt; ATC:pam     5 0.953           0.932       0.971         0.0310 0.991   0.968
#&gt; SD:hclust   5 0.549           0.718       0.765         0.1018 0.991   0.973
#&gt; CV:hclust   5 0.498           0.496       0.744         0.0776 0.862   0.632
#&gt; MAD:hclust  5 0.539           0.516       0.771         0.0778 0.982   0.947
#&gt; ATC:hclust  5 0.795           0.690       0.858         0.0920 0.935   0.800
</code></pre>

</div>
<div id='tab-get-stats-from-consensus-partition-list-5'>
<pre><code class="r">get_stats(res_list, k = 6)
</code></pre>

<pre><code>#&gt;             k 1-PAC mean_silhouette concordance area_increased  Rand Jaccard
#&gt; SD:NMF      6 0.718           0.591       0.799         0.0395 0.904   0.599
#&gt; CV:NMF      6 0.813           0.732       0.870         0.0426 0.884   0.518
#&gt; MAD:NMF     6 0.709           0.592       0.791         0.0326 0.919   0.649
#&gt; ATC:NMF     6 0.564           0.515       0.728         0.0394 0.893   0.639
#&gt; SD:skmeans  6 0.795           0.713       0.830         0.0406 0.978   0.887
#&gt; CV:skmeans  6 0.770           0.634       0.782         0.0396 0.946   0.738
#&gt; MAD:skmeans 6 0.804           0.715       0.831         0.0389 0.966   0.836
#&gt; ATC:skmeans 6 0.976           0.927       0.960         0.0318 0.974   0.873
#&gt; SD:mclust   6 0.598           0.557       0.652         0.0661 0.818   0.385
#&gt; CV:mclust   6 0.563           0.533       0.714         0.0448 0.869   0.517
#&gt; MAD:mclust  6 0.651           0.615       0.723         0.0390 0.903   0.591
#&gt; ATC:mclust  6 0.765           0.760       0.843         0.0620 0.900   0.587
#&gt; SD:kmeans   6 0.716           0.710       0.788         0.0517 1.000   1.000
#&gt; CV:kmeans   6 0.665           0.681       0.751         0.0575 0.993   0.966
#&gt; MAD:kmeans  6 0.704           0.716       0.798         0.0494 0.988   0.945
#&gt; ATC:kmeans  6 0.843           0.840       0.874         0.0454 1.000   1.000
#&gt; SD:pam      6 0.788           0.787       0.882         0.0531 0.935   0.758
#&gt; CV:pam      6 0.667           0.638       0.846         0.0647 0.930   0.755
#&gt; MAD:pam     6 0.891           0.747       0.883         0.0337 0.954   0.811
#&gt; ATC:pam     6 0.839           0.866       0.927         0.0768 0.909   0.671
#&gt; SD:hclust   6 0.616           0.393       0.755         0.1282 0.740   0.419
#&gt; CV:hclust   6 0.510           0.456       0.731         0.0358 0.907   0.728
#&gt; MAD:hclust  6 0.542           0.538       0.721         0.0579 0.940   0.820
#&gt; ATC:hclust  6 0.814           0.665       0.792         0.0489 0.933   0.752
</code></pre>

</div>
</div>

Following heatmap plots the partition for each combination of methods and the
lightness correspond to the silhouette scores for samples in each method. On
top the consensus subgroup is inferred from all methods by taking the mean
silhouette scores as weight.


<script>
$( function() {
	$( '#tabs-collect-stats-from-consensus-partition-list' ).tabs();
} );
</script>
<div id='tabs-collect-stats-from-consensus-partition-list'>
<ul>
<li><a href='#tab-collect-stats-from-consensus-partition-list-1'>k = 2</a></li>
<li><a href='#tab-collect-stats-from-consensus-partition-list-2'>k = 3</a></li>
<li><a href='#tab-collect-stats-from-consensus-partition-list-3'>k = 4</a></li>
<li><a href='#tab-collect-stats-from-consensus-partition-list-4'>k = 5</a></li>
<li><a href='#tab-collect-stats-from-consensus-partition-list-5'>k = 6</a></li>
</ul>
<div id='tab-collect-stats-from-consensus-partition-list-1'>
<pre><code class="r">collect_stats(res_list, k = 2)
</code></pre>

<p><img src="figure_cola/tab-collect-stats-from-consensus-partition-list-1-1.png" alt="plot of chunk tab-collect-stats-from-consensus-partition-list-1"/></p>

</div>
<div id='tab-collect-stats-from-consensus-partition-list-2'>
<pre><code class="r">collect_stats(res_list, k = 3)
</code></pre>

<p><img src="figure_cola/tab-collect-stats-from-consensus-partition-list-2-1.png" alt="plot of chunk tab-collect-stats-from-consensus-partition-list-2"/></p>

</div>
<div id='tab-collect-stats-from-consensus-partition-list-3'>
<pre><code class="r">collect_stats(res_list, k = 4)
</code></pre>

<p><img src="figure_cola/tab-collect-stats-from-consensus-partition-list-3-1.png" alt="plot of chunk tab-collect-stats-from-consensus-partition-list-3"/></p>

</div>
<div id='tab-collect-stats-from-consensus-partition-list-4'>
<pre><code class="r">collect_stats(res_list, k = 5)
</code></pre>

<p><img src="figure_cola/tab-collect-stats-from-consensus-partition-list-4-1.png" alt="plot of chunk tab-collect-stats-from-consensus-partition-list-4"/></p>

</div>
<div id='tab-collect-stats-from-consensus-partition-list-5'>
<pre><code class="r">collect_stats(res_list, k = 6)
</code></pre>

<p><img src="figure_cola/tab-collect-stats-from-consensus-partition-list-5-1.png" alt="plot of chunk tab-collect-stats-from-consensus-partition-list-5"/></p>

</div>
</div>

### Partition from all methods



Collect partitions from all methods:


<script>
$( function() {
	$( '#tabs-collect-classes-from-consensus-partition-list' ).tabs();
} );
</script>
<div id='tabs-collect-classes-from-consensus-partition-list'>
<ul>
<li><a href='#tab-collect-classes-from-consensus-partition-list-1'>k = 2</a></li>
<li><a href='#tab-collect-classes-from-consensus-partition-list-2'>k = 3</a></li>
<li><a href='#tab-collect-classes-from-consensus-partition-list-3'>k = 4</a></li>
<li><a href='#tab-collect-classes-from-consensus-partition-list-4'>k = 5</a></li>
<li><a href='#tab-collect-classes-from-consensus-partition-list-5'>k = 6</a></li>
</ul>
<div id='tab-collect-classes-from-consensus-partition-list-1'>
<pre><code class="r">collect_classes(res_list, k = 2)
</code></pre>

<p><img src="figure_cola/tab-collect-classes-from-consensus-partition-list-1-1.png" alt="plot of chunk tab-collect-classes-from-consensus-partition-list-1"/></p>

</div>
<div id='tab-collect-classes-from-consensus-partition-list-2'>
<pre><code class="r">collect_classes(res_list, k = 3)
</code></pre>

<p><img src="figure_cola/tab-collect-classes-from-consensus-partition-list-2-1.png" alt="plot of chunk tab-collect-classes-from-consensus-partition-list-2"/></p>

</div>
<div id='tab-collect-classes-from-consensus-partition-list-3'>
<pre><code class="r">collect_classes(res_list, k = 4)
</code></pre>

<p><img src="figure_cola/tab-collect-classes-from-consensus-partition-list-3-1.png" alt="plot of chunk tab-collect-classes-from-consensus-partition-list-3"/></p>

</div>
<div id='tab-collect-classes-from-consensus-partition-list-4'>
<pre><code class="r">collect_classes(res_list, k = 5)
</code></pre>

<p><img src="figure_cola/tab-collect-classes-from-consensus-partition-list-4-1.png" alt="plot of chunk tab-collect-classes-from-consensus-partition-list-4"/></p>

</div>
<div id='tab-collect-classes-from-consensus-partition-list-5'>
<pre><code class="r">collect_classes(res_list, k = 6)
</code></pre>

<p><img src="figure_cola/tab-collect-classes-from-consensus-partition-list-5-1.png" alt="plot of chunk tab-collect-classes-from-consensus-partition-list-5"/></p>

</div>
</div>



### Top rows overlap


Overlap of top rows from different top-row methods:


<script>
$( function() {
	$( '#tabs-top-rows-overlap-by-euler' ).tabs();
} );
</script>
<div id='tabs-top-rows-overlap-by-euler'>
<ul>
<li><a href='#tab-top-rows-overlap-by-euler-1'>top_n = 1000</a></li>
<li><a href='#tab-top-rows-overlap-by-euler-2'>top_n = 2000</a></li>
<li><a href='#tab-top-rows-overlap-by-euler-3'>top_n = 3000</a></li>
<li><a href='#tab-top-rows-overlap-by-euler-4'>top_n = 4000</a></li>
<li><a href='#tab-top-rows-overlap-by-euler-5'>top_n = 5000</a></li>
</ul>
<div id='tab-top-rows-overlap-by-euler-1'>
<pre><code class="r">top_rows_overlap(res_list, top_n = 1000, method = &quot;euler&quot;)
</code></pre>

<p><img src="figure_cola/tab-top-rows-overlap-by-euler-1-1.png" alt="plot of chunk tab-top-rows-overlap-by-euler-1"/></p>

</div>
<div id='tab-top-rows-overlap-by-euler-2'>
<pre><code class="r">top_rows_overlap(res_list, top_n = 2000, method = &quot;euler&quot;)
</code></pre>

<p><img src="figure_cola/tab-top-rows-overlap-by-euler-2-1.png" alt="plot of chunk tab-top-rows-overlap-by-euler-2"/></p>

</div>
<div id='tab-top-rows-overlap-by-euler-3'>
<pre><code class="r">top_rows_overlap(res_list, top_n = 3000, method = &quot;euler&quot;)
</code></pre>

<p><img src="figure_cola/tab-top-rows-overlap-by-euler-3-1.png" alt="plot of chunk tab-top-rows-overlap-by-euler-3"/></p>

</div>
<div id='tab-top-rows-overlap-by-euler-4'>
<pre><code class="r">top_rows_overlap(res_list, top_n = 4000, method = &quot;euler&quot;)
</code></pre>

<p><img src="figure_cola/tab-top-rows-overlap-by-euler-4-1.png" alt="plot of chunk tab-top-rows-overlap-by-euler-4"/></p>

</div>
<div id='tab-top-rows-overlap-by-euler-5'>
<pre><code class="r">top_rows_overlap(res_list, top_n = 5000, method = &quot;euler&quot;)
</code></pre>

<p><img src="figure_cola/tab-top-rows-overlap-by-euler-5-1.png" alt="plot of chunk tab-top-rows-overlap-by-euler-5"/></p>

</div>
</div>

Also visualize the correspondance of rankings between different top-row methods:


<script>
$( function() {
	$( '#tabs-top-rows-overlap-by-correspondance' ).tabs();
} );
</script>
<div id='tabs-top-rows-overlap-by-correspondance'>
<ul>
<li><a href='#tab-top-rows-overlap-by-correspondance-1'>top_n = 1000</a></li>
<li><a href='#tab-top-rows-overlap-by-correspondance-2'>top_n = 2000</a></li>
<li><a href='#tab-top-rows-overlap-by-correspondance-3'>top_n = 3000</a></li>
<li><a href='#tab-top-rows-overlap-by-correspondance-4'>top_n = 4000</a></li>
<li><a href='#tab-top-rows-overlap-by-correspondance-5'>top_n = 5000</a></li>
</ul>
<div id='tab-top-rows-overlap-by-correspondance-1'>
<pre><code class="r">top_rows_overlap(res_list, top_n = 1000, method = &quot;correspondance&quot;)
</code></pre>

<p><img src="figure_cola/tab-top-rows-overlap-by-correspondance-1-1.png" alt="plot of chunk tab-top-rows-overlap-by-correspondance-1"/></p>

</div>
<div id='tab-top-rows-overlap-by-correspondance-2'>
<pre><code class="r">top_rows_overlap(res_list, top_n = 2000, method = &quot;correspondance&quot;)
</code></pre>

<p><img src="figure_cola/tab-top-rows-overlap-by-correspondance-2-1.png" alt="plot of chunk tab-top-rows-overlap-by-correspondance-2"/></p>

</div>
<div id='tab-top-rows-overlap-by-correspondance-3'>
<pre><code class="r">top_rows_overlap(res_list, top_n = 3000, method = &quot;correspondance&quot;)
</code></pre>

<p><img src="figure_cola/tab-top-rows-overlap-by-correspondance-3-1.png" alt="plot of chunk tab-top-rows-overlap-by-correspondance-3"/></p>

</div>
<div id='tab-top-rows-overlap-by-correspondance-4'>
<pre><code class="r">top_rows_overlap(res_list, top_n = 4000, method = &quot;correspondance&quot;)
</code></pre>

<p><img src="figure_cola/tab-top-rows-overlap-by-correspondance-4-1.png" alt="plot of chunk tab-top-rows-overlap-by-correspondance-4"/></p>

</div>
<div id='tab-top-rows-overlap-by-correspondance-5'>
<pre><code class="r">top_rows_overlap(res_list, top_n = 5000, method = &quot;correspondance&quot;)
</code></pre>

<p><img src="figure_cola/tab-top-rows-overlap-by-correspondance-5-1.png" alt="plot of chunk tab-top-rows-overlap-by-correspondance-5"/></p>

</div>
</div>


Heatmaps of the top rows:



<script>
$( function() {
	$( '#tabs-top-rows-heatmap' ).tabs();
} );
</script>
<div id='tabs-top-rows-heatmap'>
<ul>
<li><a href='#tab-top-rows-heatmap-1'>top_n = 1000</a></li>
<li><a href='#tab-top-rows-heatmap-2'>top_n = 2000</a></li>
<li><a href='#tab-top-rows-heatmap-3'>top_n = 3000</a></li>
<li><a href='#tab-top-rows-heatmap-4'>top_n = 4000</a></li>
<li><a href='#tab-top-rows-heatmap-5'>top_n = 5000</a></li>
</ul>
<div id='tab-top-rows-heatmap-1'>
<pre><code class="r">top_rows_heatmap(res_list, top_n = 1000)
</code></pre>

<p><img src="figure_cola/tab-top-rows-heatmap-1-1.png" alt="plot of chunk tab-top-rows-heatmap-1"/></p>

</div>
<div id='tab-top-rows-heatmap-2'>
<pre><code class="r">top_rows_heatmap(res_list, top_n = 2000)
</code></pre>

<p><img src="figure_cola/tab-top-rows-heatmap-2-1.png" alt="plot of chunk tab-top-rows-heatmap-2"/></p>

</div>
<div id='tab-top-rows-heatmap-3'>
<pre><code class="r">top_rows_heatmap(res_list, top_n = 3000)
</code></pre>

<p><img src="figure_cola/tab-top-rows-heatmap-3-1.png" alt="plot of chunk tab-top-rows-heatmap-3"/></p>

</div>
<div id='tab-top-rows-heatmap-4'>
<pre><code class="r">top_rows_heatmap(res_list, top_n = 4000)
</code></pre>

<p><img src="figure_cola/tab-top-rows-heatmap-4-1.png" alt="plot of chunk tab-top-rows-heatmap-4"/></p>

</div>
<div id='tab-top-rows-heatmap-5'>
<pre><code class="r">top_rows_heatmap(res_list, top_n = 5000)
</code></pre>

<p><img src="figure_cola/tab-top-rows-heatmap-5-1.png" alt="plot of chunk tab-top-rows-heatmap-5"/></p>

</div>
</div>



 
## Results for each method


---------------------------------------------------




### SD:hclust






The object with results only for a single top-value method and a single partition method 
can be extracted as:

```r
res = res_list["SD", "hclust"]
# you can also extract it by
# res = res_list["SD:hclust"]
```

A summary of `res` and all the functions that can be applied to it:

```r
res
```

```
#> A 'ConsensusPartition' object with k = 2, 3, 4, 5, 6.
#>   On a matrix with 15680 rows and 53 columns.
#>   Top rows (1000, 2000, 3000, 4000, 5000) are extracted by 'SD' method.
#>   Subgroups are detected by 'hclust' method.
#>   Performed in total 1250 partitions by row resampling.
#>   Best k for subgroups seems to be 3.
#> 
#> Following methods can be applied to this 'ConsensusPartition' object:
#>  [1] "cola_report"             "collect_classes"         "collect_plots"          
#>  [4] "collect_stats"           "colnames"                "compare_signatures"     
#>  [7] "consensus_heatmap"       "dimension_reduction"     "functional_enrichment"  
#> [10] "get_anno_col"            "get_anno"                "get_classes"            
#> [13] "get_consensus"           "get_matrix"              "get_membership"         
#> [16] "get_param"               "get_signatures"          "get_stats"              
#> [19] "is_best_k"               "is_stable_k"             "membership_heatmap"     
#> [22] "ncol"                    "nrow"                    "plot_ecdf"              
#> [25] "rownames"                "select_partition_number" "show"                   
#> [28] "suggest_best_k"          "test_to_known_factors"
```

`collect_plots()` function collects all the plots made from `res` for all `k` (number of partitions)
into one single page to provide an easy and fast comparison between different `k`.

```r
collect_plots(res)
```

![plot of chunk SD-hclust-collect-plots](figure_cola/SD-hclust-collect-plots-1.png)

The plots are:

- The first row: a plot of the ECDF (empirical cumulative distribution
  function) curves of the consensus matrix for each `k` and the heatmap of
  predicted classes for each `k`.
- The second row: heatmaps of the consensus matrix for each `k`.
- The third row: heatmaps of the membership matrix for each `k`.
- The fouth row: heatmaps of the signatures for each `k`.

All the plots in panels can be made by individual functions and they are
plotted later in this section.

`select_partition_number()` produces several plots showing different
statistics for choosing "optimized" `k`. There are following statistics:

- ECDF curves of the consensus matrix for each `k`;
- 1-PAC. [The PAC
  score](https://en.wikipedia.org/wiki/Consensus_clustering#Over-interpretation_potential_of_consensus_clustering)
  measures the proportion of the ambiguous subgrouping.
- Mean silhouette score.
- Concordance. The mean probability of fiting the consensus class ids in all
  partitions.
- Area increased. Denote $A_k$ as the area under the ECDF curve for current
  `k`, the area increased is defined as $A_k - A_{k-1}$.
- Rand index. The percent of pairs of samples that are both in a same cluster
  or both are not in a same cluster in the partition of k and k-1.
- Jaccard index. The ratio of pairs of samples are both in a same cluster in
  the partition of k and k-1 and the pairs of samples are both in a same
  cluster in the partition k or k-1.

The detailed explanations of these statistics can be found in [the _cola_
vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/cola.html#toc_13).

Generally speaking, lower PAC score, higher mean silhouette score or higher
concordance corresponds to better partition. Rand index and Jaccard index
measure how similar the current partition is compared to partition with `k-1`.
If they are too similar, we won't accept `k` is better than `k-1`.

```r
select_partition_number(res)
```

![plot of chunk SD-hclust-select-partition-number](figure_cola/SD-hclust-select-partition-number-1.png)

The numeric values for all these statistics can be obtained by `get_stats()`.

```r
get_stats(res)
```

```
#>   k 1-PAC mean_silhouette concordance area_increased  Rand Jaccard
#> 2 2 0.858           0.955       0.979          0.262 0.766   0.766
#> 3 3 0.630           0.776       0.891          0.866 0.826   0.773
#> 4 4 0.587           0.623       0.781          0.164 0.686   0.491
#> 5 5 0.549           0.718       0.765          0.102 0.991   0.973
#> 6 6 0.616           0.393       0.755          0.128 0.740   0.419
```

`suggest_best_k()` suggests the best $k$ based on these statistics. The rules are as follows:

- All $k$ with Jaccard index larger than 0.95 are removed because increasing
  $k$ does not provide enough extra information. If all $k$ are removed, it is
  marked as no subgroup is detected.
- For all $k$ with 1-PAC score larger than 0.9, the maximal $k$ is taken as
  the best $k$, and other $k$ are marked as optional $k$.
- If it does not fit the second rule. The $k$ with the maximal vote of the
  highest 1-PAC score, highest mean silhouette, and highest concordance is
  taken as the best $k$.

```r
suggest_best_k(res)
```

```
#> [1] 3
```


Following shows the table of the partitions (You need to click the **show/hide
code output** link to see it). The membership matrix (columns with name `p*`)
is inferred by
[`clue::cl_consensus()`](https://www.rdocumentation.org/link/cl_consensus?package=clue)
function with the `SE` method. Basically the value in the membership matrix
represents the probability to belong to a certain group. The finall class
label for an item is determined with the group with highest probability it
belongs to.

In `get_classes()` function, the entropy is calculated from the membership
matrix and the silhouette score is calculated from the consensus matrix.



<script>
$( function() {
	$( '#tabs-SD-hclust-get-classes' ).tabs();
} );
</script>
<div id='tabs-SD-hclust-get-classes'>
<ul>
<li><a href='#tab-SD-hclust-get-classes-1'>k = 2</a></li>
<li><a href='#tab-SD-hclust-get-classes-2'>k = 3</a></li>
<li><a href='#tab-SD-hclust-get-classes-3'>k = 4</a></li>
<li><a href='#tab-SD-hclust-get-classes-4'>k = 5</a></li>
<li><a href='#tab-SD-hclust-get-classes-5'>k = 6</a></li>
</ul>

<div id='tab-SD-hclust-get-classes-1'>
<p><a id='tab-SD-hclust-get-classes-1-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 2), get_membership(res, k = 2))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2
#&gt; SRR1383358     2  0.0000      0.974 0.000 1.000
#&gt; SRR1383360     2  0.8144      0.694 0.252 0.748
#&gt; SRR1383359     2  0.0000      0.974 0.000 1.000
#&gt; SRR1383362     1  0.0000      1.000 1.000 0.000
#&gt; SRR1383361     2  0.0000      0.974 0.000 1.000
#&gt; SRR1383363     2  0.0000      0.974 0.000 1.000
#&gt; SRR1383364     2  0.0000      0.974 0.000 1.000
#&gt; SRR1383365     2  0.0000      0.974 0.000 1.000
#&gt; SRR1383366     2  0.0000      0.974 0.000 1.000
#&gt; SRR1383367     2  0.0000      0.974 0.000 1.000
#&gt; SRR1383368     2  0.8144      0.694 0.252 0.748
#&gt; SRR1383369     2  0.0000      0.974 0.000 1.000
#&gt; SRR1383370     2  0.0000      0.974 0.000 1.000
#&gt; SRR1383371     2  0.0000      0.974 0.000 1.000
#&gt; SRR1383372     2  0.0000      0.974 0.000 1.000
#&gt; SRR1383373     2  0.0000      0.974 0.000 1.000
#&gt; SRR1383374     2  0.0000      0.974 0.000 1.000
#&gt; SRR1383375     1  0.0000      1.000 1.000 0.000
#&gt; SRR1383376     2  0.0000      0.974 0.000 1.000
#&gt; SRR1383377     2  0.0000      0.974 0.000 1.000
#&gt; SRR1383378     2  0.2948      0.932 0.052 0.948
#&gt; SRR1383379     2  0.0000      0.974 0.000 1.000
#&gt; SRR1383380     2  0.0000      0.974 0.000 1.000
#&gt; SRR1383381     2  0.0000      0.974 0.000 1.000
#&gt; SRR1383382     1  0.0000      1.000 1.000 0.000
#&gt; SRR1383383     2  0.0000      0.974 0.000 1.000
#&gt; SRR1383385     1  0.0000      1.000 1.000 0.000
#&gt; SRR1383384     2  0.0000      0.974 0.000 1.000
#&gt; SRR1383386     2  0.8144      0.694 0.252 0.748
#&gt; SRR1383387     2  0.0000      0.974 0.000 1.000
#&gt; SRR1383389     2  0.0000      0.974 0.000 1.000
#&gt; SRR1383391     2  0.0000      0.974 0.000 1.000
#&gt; SRR1383388     2  0.0938      0.966 0.012 0.988
#&gt; SRR1383392     2  0.0000      0.974 0.000 1.000
#&gt; SRR1383390     2  0.0000      0.974 0.000 1.000
#&gt; SRR1383394     2  0.0000      0.974 0.000 1.000
#&gt; SRR1383393     1  0.0000      1.000 1.000 0.000
#&gt; SRR1383396     2  0.2948      0.932 0.052 0.948
#&gt; SRR1383395     2  0.0000      0.974 0.000 1.000
#&gt; SRR1383399     2  0.0000      0.974 0.000 1.000
#&gt; SRR1383400     1  0.0000      1.000 1.000 0.000
#&gt; SRR1383397     2  0.0000      0.974 0.000 1.000
#&gt; SRR1383401     2  0.0000      0.974 0.000 1.000
#&gt; SRR1383398     2  0.0000      0.974 0.000 1.000
#&gt; SRR1383402     2  0.0000      0.974 0.000 1.000
#&gt; SRR1383404     2  0.8144      0.694 0.252 0.748
#&gt; SRR1383403     1  0.0000      1.000 1.000 0.000
#&gt; SRR1383405     2  0.0000      0.974 0.000 1.000
#&gt; SRR1383406     2  0.0938      0.966 0.012 0.988
#&gt; SRR1383407     2  0.0000      0.974 0.000 1.000
#&gt; SRR1383408     2  0.0000      0.974 0.000 1.000
#&gt; SRR1383409     2  0.0000      0.974 0.000 1.000
#&gt; SRR1383410     2  0.0000      0.974 0.000 1.000
</code></pre>

<script>
$('#tab-SD-hclust-get-classes-1-a').parent().next().next().hide();
$('#tab-SD-hclust-get-classes-1-a').click(function(){
  $('#tab-SD-hclust-get-classes-1-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-SD-hclust-get-classes-2'>
<p><a id='tab-SD-hclust-get-classes-2-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 3), get_membership(res, k = 3))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3
#&gt; SRR1383358     2  0.6168      0.455 0.000 0.588 0.412
#&gt; SRR1383360     2  0.5138      0.669 0.252 0.748 0.000
#&gt; SRR1383359     3  0.2066      0.889 0.000 0.060 0.940
#&gt; SRR1383362     1  0.0000      1.000 1.000 0.000 0.000
#&gt; SRR1383361     2  0.6168      0.455 0.000 0.588 0.412
#&gt; SRR1383363     2  0.6192      0.438 0.000 0.580 0.420
#&gt; SRR1383364     3  0.0000      0.895 0.000 0.000 1.000
#&gt; SRR1383365     2  0.6168      0.455 0.000 0.588 0.412
#&gt; SRR1383366     2  0.6168      0.455 0.000 0.588 0.412
#&gt; SRR1383367     2  0.6168      0.455 0.000 0.588 0.412
#&gt; SRR1383368     2  0.5138      0.669 0.252 0.748 0.000
#&gt; SRR1383369     3  0.4346      0.724 0.000 0.184 0.816
#&gt; SRR1383370     2  0.6168      0.455 0.000 0.588 0.412
#&gt; SRR1383371     3  0.0000      0.895 0.000 0.000 1.000
#&gt; SRR1383372     2  0.6168      0.455 0.000 0.588 0.412
#&gt; SRR1383373     2  0.6168      0.455 0.000 0.588 0.412
#&gt; SRR1383374     2  0.6140      0.468 0.000 0.596 0.404
#&gt; SRR1383375     1  0.0000      1.000 1.000 0.000 0.000
#&gt; SRR1383376     2  0.0000      0.838 0.000 1.000 0.000
#&gt; SRR1383377     2  0.1411      0.831 0.000 0.964 0.036
#&gt; SRR1383378     2  0.1860      0.819 0.052 0.948 0.000
#&gt; SRR1383379     2  0.0000      0.838 0.000 1.000 0.000
#&gt; SRR1383380     2  0.0000      0.838 0.000 1.000 0.000
#&gt; SRR1383381     3  0.1163      0.913 0.000 0.028 0.972
#&gt; SRR1383382     1  0.0000      1.000 1.000 0.000 0.000
#&gt; SRR1383383     2  0.0424      0.836 0.000 0.992 0.008
#&gt; SRR1383385     1  0.0000      1.000 1.000 0.000 0.000
#&gt; SRR1383384     2  0.0000      0.838 0.000 1.000 0.000
#&gt; SRR1383386     2  0.5138      0.669 0.252 0.748 0.000
#&gt; SRR1383387     2  0.0000      0.838 0.000 1.000 0.000
#&gt; SRR1383389     2  0.1289      0.832 0.000 0.968 0.032
#&gt; SRR1383391     2  0.0000      0.838 0.000 1.000 0.000
#&gt; SRR1383388     2  0.0592      0.835 0.012 0.988 0.000
#&gt; SRR1383392     2  0.1411      0.831 0.000 0.964 0.036
#&gt; SRR1383390     2  0.0000      0.838 0.000 1.000 0.000
#&gt; SRR1383394     2  0.0000      0.838 0.000 1.000 0.000
#&gt; SRR1383393     1  0.0000      1.000 1.000 0.000 0.000
#&gt; SRR1383396     2  0.1860      0.819 0.052 0.948 0.000
#&gt; SRR1383395     2  0.1411      0.831 0.000 0.964 0.036
#&gt; SRR1383399     3  0.1163      0.913 0.000 0.028 0.972
#&gt; SRR1383400     1  0.0000      1.000 1.000 0.000 0.000
#&gt; SRR1383397     2  0.0000      0.838 0.000 1.000 0.000
#&gt; SRR1383401     2  0.0424      0.836 0.000 0.992 0.008
#&gt; SRR1383398     2  0.0000      0.838 0.000 1.000 0.000
#&gt; SRR1383402     2  0.0000      0.838 0.000 1.000 0.000
#&gt; SRR1383404     2  0.5138      0.669 0.252 0.748 0.000
#&gt; SRR1383403     1  0.0000      1.000 1.000 0.000 0.000
#&gt; SRR1383405     2  0.0000      0.838 0.000 1.000 0.000
#&gt; SRR1383406     2  0.0592      0.835 0.012 0.988 0.000
#&gt; SRR1383407     2  0.1289      0.832 0.000 0.968 0.032
#&gt; SRR1383408     2  0.0000      0.838 0.000 1.000 0.000
#&gt; SRR1383409     2  0.0000      0.838 0.000 1.000 0.000
#&gt; SRR1383410     2  0.1411      0.831 0.000 0.964 0.036
</code></pre>

<script>
$('#tab-SD-hclust-get-classes-2-a').parent().next().next().hide();
$('#tab-SD-hclust-get-classes-2-a').click(function(){
  $('#tab-SD-hclust-get-classes-2-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-SD-hclust-get-classes-3'>
<p><a id='tab-SD-hclust-get-classes-3-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 4), get_membership(res, k = 4))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4
#&gt; SRR1383358     3  0.0000      0.619 0.000 0.000 1.000 0.000
#&gt; SRR1383360     3  0.7791     -0.238 0.252 0.276 0.468 0.004
#&gt; SRR1383359     3  0.7681     -0.401 0.000 0.344 0.432 0.224
#&gt; SRR1383362     1  0.1059      0.984 0.972 0.016 0.000 0.012
#&gt; SRR1383361     3  0.0000      0.619 0.000 0.000 1.000 0.000
#&gt; SRR1383363     3  0.0336      0.615 0.000 0.000 0.992 0.008
#&gt; SRR1383364     4  0.0592      0.970 0.000 0.000 0.016 0.984
#&gt; SRR1383365     3  0.0000      0.619 0.000 0.000 1.000 0.000
#&gt; SRR1383366     3  0.0000      0.619 0.000 0.000 1.000 0.000
#&gt; SRR1383367     3  0.0000      0.619 0.000 0.000 1.000 0.000
#&gt; SRR1383368     2  0.7799      0.490 0.252 0.400 0.348 0.000
#&gt; SRR1383369     3  0.5028     -0.233 0.000 0.004 0.596 0.400
#&gt; SRR1383370     3  0.0000      0.619 0.000 0.000 1.000 0.000
#&gt; SRR1383371     4  0.0592      0.970 0.000 0.000 0.016 0.984
#&gt; SRR1383372     3  0.0000      0.619 0.000 0.000 1.000 0.000
#&gt; SRR1383373     3  0.0000      0.619 0.000 0.000 1.000 0.000
#&gt; SRR1383374     3  0.0336      0.612 0.000 0.008 0.992 0.000
#&gt; SRR1383375     1  0.0000      0.988 1.000 0.000 0.000 0.000
#&gt; SRR1383376     2  0.4790      0.897 0.000 0.620 0.380 0.000
#&gt; SRR1383377     3  0.5119     -0.409 0.000 0.440 0.556 0.004
#&gt; SRR1383378     2  0.6014      0.841 0.052 0.588 0.360 0.000
#&gt; SRR1383379     2  0.4730      0.898 0.000 0.636 0.364 0.000
#&gt; SRR1383380     2  0.4730      0.898 0.000 0.636 0.364 0.000
#&gt; SRR1383381     4  0.1635      0.970 0.000 0.008 0.044 0.948
#&gt; SRR1383382     1  0.1059      0.984 0.972 0.016 0.000 0.012
#&gt; SRR1383383     2  0.4830      0.879 0.000 0.608 0.392 0.000
#&gt; SRR1383385     1  0.0000      0.988 1.000 0.000 0.000 0.000
#&gt; SRR1383384     2  0.4804      0.895 0.000 0.616 0.384 0.000
#&gt; SRR1383386     2  0.7799      0.490 0.252 0.400 0.348 0.000
#&gt; SRR1383387     2  0.4730      0.898 0.000 0.636 0.364 0.000
#&gt; SRR1383389     3  0.5088     -0.387 0.000 0.424 0.572 0.004
#&gt; SRR1383391     2  0.4804      0.895 0.000 0.616 0.384 0.000
#&gt; SRR1383388     2  0.5159      0.892 0.012 0.624 0.364 0.000
#&gt; SRR1383392     3  0.5080     -0.373 0.000 0.420 0.576 0.004
#&gt; SRR1383390     2  0.4804      0.895 0.000 0.616 0.384 0.000
#&gt; SRR1383394     2  0.4790      0.897 0.000 0.620 0.380 0.000
#&gt; SRR1383393     1  0.0000      0.988 1.000 0.000 0.000 0.000
#&gt; SRR1383396     2  0.6014      0.841 0.052 0.588 0.360 0.000
#&gt; SRR1383395     3  0.5119     -0.409 0.000 0.440 0.556 0.004
#&gt; SRR1383399     4  0.1635      0.970 0.000 0.008 0.044 0.948
#&gt; SRR1383400     1  0.1059      0.984 0.972 0.016 0.000 0.012
#&gt; SRR1383397     2  0.4730      0.898 0.000 0.636 0.364 0.000
#&gt; SRR1383401     2  0.4830      0.879 0.000 0.608 0.392 0.000
#&gt; SRR1383398     2  0.4730      0.898 0.000 0.636 0.364 0.000
#&gt; SRR1383402     2  0.4804      0.895 0.000 0.616 0.384 0.000
#&gt; SRR1383404     2  0.7799      0.490 0.252 0.400 0.348 0.000
#&gt; SRR1383403     1  0.0000      0.988 1.000 0.000 0.000 0.000
#&gt; SRR1383405     2  0.4730      0.898 0.000 0.636 0.364 0.000
#&gt; SRR1383406     2  0.5159      0.892 0.012 0.624 0.364 0.000
#&gt; SRR1383407     3  0.5088     -0.387 0.000 0.424 0.572 0.004
#&gt; SRR1383408     2  0.4804      0.895 0.000 0.616 0.384 0.000
#&gt; SRR1383409     2  0.4804      0.895 0.000 0.616 0.384 0.000
#&gt; SRR1383410     3  0.5080     -0.373 0.000 0.420 0.576 0.004
</code></pre>

<script>
$('#tab-SD-hclust-get-classes-3-a').parent().next().next().hide();
$('#tab-SD-hclust-get-classes-3-a').click(function(){
  $('#tab-SD-hclust-get-classes-3-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-SD-hclust-get-classes-4'>
<p><a id='tab-SD-hclust-get-classes-4-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 5), get_membership(res, k = 5))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4    p5
#&gt; SRR1383358     3  0.0000      0.696 0.000 0.000 1.000 0.000 0.000
#&gt; SRR1383360     3  0.8118      0.199 0.248 0.192 0.416 0.144 0.000
#&gt; SRR1383359     3  0.6886     -0.150 0.000 0.236 0.428 0.328 0.008
#&gt; SRR1383362     4  0.4443      1.000 0.472 0.004 0.000 0.524 0.000
#&gt; SRR1383361     3  0.0000      0.696 0.000 0.000 1.000 0.000 0.000
#&gt; SRR1383363     3  0.0290      0.693 0.000 0.000 0.992 0.000 0.008
#&gt; SRR1383364     5  0.0162      0.970 0.000 0.000 0.004 0.000 0.996
#&gt; SRR1383365     3  0.0000      0.696 0.000 0.000 1.000 0.000 0.000
#&gt; SRR1383366     3  0.0794      0.678 0.000 0.028 0.972 0.000 0.000
#&gt; SRR1383367     3  0.0000      0.696 0.000 0.000 1.000 0.000 0.000
#&gt; SRR1383368     2  0.6792      0.555 0.248 0.508 0.228 0.016 0.000
#&gt; SRR1383369     3  0.4331     -0.090 0.000 0.004 0.596 0.000 0.400
#&gt; SRR1383370     3  0.0000      0.696 0.000 0.000 1.000 0.000 0.000
#&gt; SRR1383371     5  0.0162      0.970 0.000 0.000 0.004 0.000 0.996
#&gt; SRR1383372     3  0.0000      0.696 0.000 0.000 1.000 0.000 0.000
#&gt; SRR1383373     3  0.0000      0.696 0.000 0.000 1.000 0.000 0.000
#&gt; SRR1383374     3  0.0290      0.691 0.000 0.008 0.992 0.000 0.000
#&gt; SRR1383375     1  0.0000      1.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1383376     2  0.3837      0.874 0.000 0.692 0.308 0.000 0.000
#&gt; SRR1383377     3  0.6050      0.149 0.000 0.360 0.512 0.128 0.000
#&gt; SRR1383378     2  0.5129      0.834 0.052 0.684 0.248 0.016 0.000
#&gt; SRR1383379     2  0.3480      0.879 0.000 0.752 0.248 0.000 0.000
#&gt; SRR1383380     2  0.3480      0.879 0.000 0.752 0.248 0.000 0.000
#&gt; SRR1383381     5  0.1278      0.970 0.000 0.020 0.016 0.004 0.960
#&gt; SRR1383382     4  0.4443      1.000 0.472 0.004 0.000 0.524 0.000
#&gt; SRR1383383     2  0.4029      0.863 0.000 0.680 0.316 0.004 0.000
#&gt; SRR1383385     1  0.0000      1.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1383384     2  0.3857      0.871 0.000 0.688 0.312 0.000 0.000
#&gt; SRR1383386     2  0.6792      0.555 0.248 0.508 0.228 0.016 0.000
#&gt; SRR1383387     2  0.3508      0.880 0.000 0.748 0.252 0.000 0.000
#&gt; SRR1383389     3  0.5972      0.224 0.000 0.300 0.560 0.140 0.000
#&gt; SRR1383391     2  0.4108      0.873 0.000 0.684 0.308 0.008 0.000
#&gt; SRR1383388     2  0.3990      0.872 0.012 0.740 0.244 0.004 0.000
#&gt; SRR1383392     3  0.5864      0.233 0.000 0.300 0.572 0.128 0.000
#&gt; SRR1383390     2  0.4108      0.873 0.000 0.684 0.308 0.008 0.000
#&gt; SRR1383394     2  0.3837      0.874 0.000 0.692 0.308 0.000 0.000
#&gt; SRR1383393     1  0.0000      1.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1383396     2  0.5129      0.834 0.052 0.684 0.248 0.016 0.000
#&gt; SRR1383395     3  0.6050      0.149 0.000 0.360 0.512 0.128 0.000
#&gt; SRR1383399     5  0.1278      0.970 0.000 0.020 0.016 0.004 0.960
#&gt; SRR1383400     4  0.4443      1.000 0.472 0.004 0.000 0.524 0.000
#&gt; SRR1383397     2  0.3480      0.879 0.000 0.752 0.248 0.000 0.000
#&gt; SRR1383401     2  0.4029      0.863 0.000 0.680 0.316 0.004 0.000
#&gt; SRR1383398     2  0.3480      0.879 0.000 0.752 0.248 0.000 0.000
#&gt; SRR1383402     2  0.3857      0.871 0.000 0.688 0.312 0.000 0.000
#&gt; SRR1383404     2  0.6792      0.555 0.248 0.508 0.228 0.016 0.000
#&gt; SRR1383403     1  0.0000      1.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1383405     2  0.3508      0.880 0.000 0.748 0.252 0.000 0.000
#&gt; SRR1383406     2  0.3990      0.872 0.012 0.740 0.244 0.004 0.000
#&gt; SRR1383407     3  0.5972      0.224 0.000 0.300 0.560 0.140 0.000
#&gt; SRR1383408     2  0.4108      0.873 0.000 0.684 0.308 0.008 0.000
#&gt; SRR1383409     2  0.4108      0.873 0.000 0.684 0.308 0.008 0.000
#&gt; SRR1383410     3  0.5864      0.233 0.000 0.300 0.572 0.128 0.000
</code></pre>

<script>
$('#tab-SD-hclust-get-classes-4-a').parent().next().next().hide();
$('#tab-SD-hclust-get-classes-4-a').click(function(){
  $('#tab-SD-hclust-get-classes-4-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-SD-hclust-get-classes-5'>
<p><a id='tab-SD-hclust-get-classes-5-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 6), get_membership(res, k = 6))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4    p5    p6
#&gt; SRR1383358     2  0.3930    0.12699 0.000 0.576 0.420 0.000 0.004 0.000
#&gt; SRR1383360     4  0.4956   -0.09882 0.072 0.332 0.000 0.592 0.000 0.004
#&gt; SRR1383359     3  0.0146    0.00000 0.000 0.004 0.996 0.000 0.000 0.000
#&gt; SRR1383362     6  0.0000    1.00000 0.000 0.000 0.000 0.000 0.000 1.000
#&gt; SRR1383361     2  0.3930    0.12699 0.000 0.576 0.420 0.000 0.004 0.000
#&gt; SRR1383363     2  0.4123    0.11676 0.000 0.568 0.420 0.000 0.012 0.000
#&gt; SRR1383364     5  0.0000    0.74794 0.000 0.000 0.000 0.000 1.000 0.000
#&gt; SRR1383365     2  0.3930    0.12699 0.000 0.576 0.420 0.000 0.004 0.000
#&gt; SRR1383366     2  0.5141    0.01743 0.000 0.504 0.420 0.072 0.004 0.000
#&gt; SRR1383367     2  0.3930    0.12699 0.000 0.576 0.420 0.000 0.004 0.000
#&gt; SRR1383368     4  0.1946    0.55432 0.072 0.012 0.000 0.912 0.000 0.004
#&gt; SRR1383369     5  0.5967   -0.40202 0.000 0.224 0.372 0.000 0.404 0.000
#&gt; SRR1383370     2  0.3930    0.12699 0.000 0.576 0.420 0.000 0.004 0.000
#&gt; SRR1383371     5  0.0000    0.74794 0.000 0.000 0.000 0.000 1.000 0.000
#&gt; SRR1383372     2  0.3930    0.12699 0.000 0.576 0.420 0.000 0.004 0.000
#&gt; SRR1383373     2  0.3930    0.12699 0.000 0.576 0.420 0.000 0.004 0.000
#&gt; SRR1383374     2  0.3915    0.13484 0.000 0.584 0.412 0.000 0.004 0.000
#&gt; SRR1383375     1  0.0000    1.00000 1.000 0.000 0.000 0.000 0.000 0.000
#&gt; SRR1383376     2  0.3789   -0.00739 0.000 0.584 0.000 0.416 0.000 0.000
#&gt; SRR1383377     2  0.3309   -0.05265 0.000 0.720 0.000 0.280 0.000 0.000
#&gt; SRR1383378     4  0.2597    0.66787 0.000 0.176 0.000 0.824 0.000 0.000
#&gt; SRR1383379     4  0.3499    0.70287 0.000 0.320 0.000 0.680 0.000 0.000
#&gt; SRR1383380     4  0.3499    0.70287 0.000 0.320 0.000 0.680 0.000 0.000
#&gt; SRR1383381     5  0.1086    0.74813 0.000 0.012 0.012 0.012 0.964 0.000
#&gt; SRR1383382     6  0.0000    1.00000 0.000 0.000 0.000 0.000 0.000 1.000
#&gt; SRR1383383     2  0.4076    0.01599 0.000 0.592 0.012 0.396 0.000 0.000
#&gt; SRR1383385     1  0.0000    1.00000 1.000 0.000 0.000 0.000 0.000 0.000
#&gt; SRR1383384     2  0.3789   -0.00129 0.000 0.584 0.000 0.416 0.000 0.000
#&gt; SRR1383386     4  0.1946    0.55432 0.072 0.012 0.000 0.912 0.000 0.004
#&gt; SRR1383387     4  0.3515    0.69802 0.000 0.324 0.000 0.676 0.000 0.000
#&gt; SRR1383389     2  0.0713    0.39878 0.000 0.972 0.000 0.028 0.000 0.000
#&gt; SRR1383391     2  0.3789   -0.00183 0.000 0.584 0.000 0.416 0.000 0.000
#&gt; SRR1383388     4  0.3221    0.71244 0.000 0.264 0.000 0.736 0.000 0.000
#&gt; SRR1383392     2  0.0632    0.39806 0.000 0.976 0.000 0.024 0.000 0.000
#&gt; SRR1383390     2  0.3774    0.01221 0.000 0.592 0.000 0.408 0.000 0.000
#&gt; SRR1383394     2  0.3789   -0.00739 0.000 0.584 0.000 0.416 0.000 0.000
#&gt; SRR1383393     1  0.0000    1.00000 1.000 0.000 0.000 0.000 0.000 0.000
#&gt; SRR1383396     4  0.2597    0.66787 0.000 0.176 0.000 0.824 0.000 0.000
#&gt; SRR1383395     2  0.3309   -0.05265 0.000 0.720 0.000 0.280 0.000 0.000
#&gt; SRR1383399     5  0.1086    0.74813 0.000 0.012 0.012 0.012 0.964 0.000
#&gt; SRR1383400     6  0.0000    1.00000 0.000 0.000 0.000 0.000 0.000 1.000
#&gt; SRR1383397     4  0.3499    0.70287 0.000 0.320 0.000 0.680 0.000 0.000
#&gt; SRR1383401     2  0.4076    0.01599 0.000 0.592 0.012 0.396 0.000 0.000
#&gt; SRR1383398     4  0.3499    0.70287 0.000 0.320 0.000 0.680 0.000 0.000
#&gt; SRR1383402     2  0.3789   -0.00129 0.000 0.584 0.000 0.416 0.000 0.000
#&gt; SRR1383404     4  0.1946    0.55432 0.072 0.012 0.000 0.912 0.000 0.004
#&gt; SRR1383403     1  0.0000    1.00000 1.000 0.000 0.000 0.000 0.000 0.000
#&gt; SRR1383405     4  0.3515    0.69802 0.000 0.324 0.000 0.676 0.000 0.000
#&gt; SRR1383406     4  0.3221    0.71244 0.000 0.264 0.000 0.736 0.000 0.000
#&gt; SRR1383407     2  0.0713    0.39878 0.000 0.972 0.000 0.028 0.000 0.000
#&gt; SRR1383408     2  0.3774    0.01221 0.000 0.592 0.000 0.408 0.000 0.000
#&gt; SRR1383409     2  0.3789   -0.00183 0.000 0.584 0.000 0.416 0.000 0.000
#&gt; SRR1383410     2  0.0632    0.39806 0.000 0.976 0.000 0.024 0.000 0.000
</code></pre>

<script>
$('#tab-SD-hclust-get-classes-5-a').parent().next().next().hide();
$('#tab-SD-hclust-get-classes-5-a').click(function(){
  $('#tab-SD-hclust-get-classes-5-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>
</div>

Heatmaps for the consensus matrix. It visualizes the probability of two
samples to be in a same group.



<script>
$( function() {
	$( '#tabs-SD-hclust-consensus-heatmap' ).tabs();
} );
</script>
<div id='tabs-SD-hclust-consensus-heatmap'>
<ul>
<li><a href='#tab-SD-hclust-consensus-heatmap-1'>k = 2</a></li>
<li><a href='#tab-SD-hclust-consensus-heatmap-2'>k = 3</a></li>
<li><a href='#tab-SD-hclust-consensus-heatmap-3'>k = 4</a></li>
<li><a href='#tab-SD-hclust-consensus-heatmap-4'>k = 5</a></li>
<li><a href='#tab-SD-hclust-consensus-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-SD-hclust-consensus-heatmap-1'>
<pre><code class="r">consensus_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-SD-hclust-consensus-heatmap-1-1.png" alt="plot of chunk tab-SD-hclust-consensus-heatmap-1"/></p>

</div>
<div id='tab-SD-hclust-consensus-heatmap-2'>
<pre><code class="r">consensus_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-SD-hclust-consensus-heatmap-2-1.png" alt="plot of chunk tab-SD-hclust-consensus-heatmap-2"/></p>

</div>
<div id='tab-SD-hclust-consensus-heatmap-3'>
<pre><code class="r">consensus_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-SD-hclust-consensus-heatmap-3-1.png" alt="plot of chunk tab-SD-hclust-consensus-heatmap-3"/></p>

</div>
<div id='tab-SD-hclust-consensus-heatmap-4'>
<pre><code class="r">consensus_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-SD-hclust-consensus-heatmap-4-1.png" alt="plot of chunk tab-SD-hclust-consensus-heatmap-4"/></p>

</div>
<div id='tab-SD-hclust-consensus-heatmap-5'>
<pre><code class="r">consensus_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-SD-hclust-consensus-heatmap-5-1.png" alt="plot of chunk tab-SD-hclust-consensus-heatmap-5"/></p>

</div>
</div>

Heatmaps for the membership of samples in all partitions to see how consistent they are:




<script>
$( function() {
	$( '#tabs-SD-hclust-membership-heatmap' ).tabs();
} );
</script>
<div id='tabs-SD-hclust-membership-heatmap'>
<ul>
<li><a href='#tab-SD-hclust-membership-heatmap-1'>k = 2</a></li>
<li><a href='#tab-SD-hclust-membership-heatmap-2'>k = 3</a></li>
<li><a href='#tab-SD-hclust-membership-heatmap-3'>k = 4</a></li>
<li><a href='#tab-SD-hclust-membership-heatmap-4'>k = 5</a></li>
<li><a href='#tab-SD-hclust-membership-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-SD-hclust-membership-heatmap-1'>
<pre><code class="r">membership_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-SD-hclust-membership-heatmap-1-1.png" alt="plot of chunk tab-SD-hclust-membership-heatmap-1"/></p>

</div>
<div id='tab-SD-hclust-membership-heatmap-2'>
<pre><code class="r">membership_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-SD-hclust-membership-heatmap-2-1.png" alt="plot of chunk tab-SD-hclust-membership-heatmap-2"/></p>

</div>
<div id='tab-SD-hclust-membership-heatmap-3'>
<pre><code class="r">membership_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-SD-hclust-membership-heatmap-3-1.png" alt="plot of chunk tab-SD-hclust-membership-heatmap-3"/></p>

</div>
<div id='tab-SD-hclust-membership-heatmap-4'>
<pre><code class="r">membership_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-SD-hclust-membership-heatmap-4-1.png" alt="plot of chunk tab-SD-hclust-membership-heatmap-4"/></p>

</div>
<div id='tab-SD-hclust-membership-heatmap-5'>
<pre><code class="r">membership_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-SD-hclust-membership-heatmap-5-1.png" alt="plot of chunk tab-SD-hclust-membership-heatmap-5"/></p>

</div>
</div>

As soon as we have had the classes for columns, we can look for signatures
which are significantly different between classes which can be candidate marks
for certain classes. Following are the heatmaps for signatures.



Signature heatmaps where rows are scaled:



<script>
$( function() {
	$( '#tabs-SD-hclust-get-signatures' ).tabs();
} );
</script>
<div id='tabs-SD-hclust-get-signatures'>
<ul>
<li><a href='#tab-SD-hclust-get-signatures-1'>k = 2</a></li>
<li><a href='#tab-SD-hclust-get-signatures-2'>k = 3</a></li>
<li><a href='#tab-SD-hclust-get-signatures-3'>k = 4</a></li>
<li><a href='#tab-SD-hclust-get-signatures-4'>k = 5</a></li>
<li><a href='#tab-SD-hclust-get-signatures-5'>k = 6</a></li>
</ul>
<div id='tab-SD-hclust-get-signatures-1'>
<pre><code class="r">get_signatures(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-SD-hclust-get-signatures-1-1.png" alt="plot of chunk tab-SD-hclust-get-signatures-1"/></p>

</div>
<div id='tab-SD-hclust-get-signatures-2'>
<pre><code class="r">get_signatures(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-SD-hclust-get-signatures-2-1.png" alt="plot of chunk tab-SD-hclust-get-signatures-2"/></p>

</div>
<div id='tab-SD-hclust-get-signatures-3'>
<pre><code class="r">get_signatures(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-SD-hclust-get-signatures-3-1.png" alt="plot of chunk tab-SD-hclust-get-signatures-3"/></p>

</div>
<div id='tab-SD-hclust-get-signatures-4'>
<pre><code class="r">get_signatures(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-SD-hclust-get-signatures-4-1.png" alt="plot of chunk tab-SD-hclust-get-signatures-4"/></p>

</div>
<div id='tab-SD-hclust-get-signatures-5'>
<pre><code class="r">get_signatures(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-SD-hclust-get-signatures-5-1.png" alt="plot of chunk tab-SD-hclust-get-signatures-5"/></p>

</div>
</div>



Signature heatmaps where rows are not scaled:


<script>
$( function() {
	$( '#tabs-SD-hclust-get-signatures-no-scale' ).tabs();
} );
</script>
<div id='tabs-SD-hclust-get-signatures-no-scale'>
<ul>
<li><a href='#tab-SD-hclust-get-signatures-no-scale-1'>k = 2</a></li>
<li><a href='#tab-SD-hclust-get-signatures-no-scale-2'>k = 3</a></li>
<li><a href='#tab-SD-hclust-get-signatures-no-scale-3'>k = 4</a></li>
<li><a href='#tab-SD-hclust-get-signatures-no-scale-4'>k = 5</a></li>
<li><a href='#tab-SD-hclust-get-signatures-no-scale-5'>k = 6</a></li>
</ul>
<div id='tab-SD-hclust-get-signatures-no-scale-1'>
<pre><code class="r">get_signatures(res, k = 2, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-SD-hclust-get-signatures-no-scale-1-1.png" alt="plot of chunk tab-SD-hclust-get-signatures-no-scale-1"/></p>

</div>
<div id='tab-SD-hclust-get-signatures-no-scale-2'>
<pre><code class="r">get_signatures(res, k = 3, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-SD-hclust-get-signatures-no-scale-2-1.png" alt="plot of chunk tab-SD-hclust-get-signatures-no-scale-2"/></p>

</div>
<div id='tab-SD-hclust-get-signatures-no-scale-3'>
<pre><code class="r">get_signatures(res, k = 4, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-SD-hclust-get-signatures-no-scale-3-1.png" alt="plot of chunk tab-SD-hclust-get-signatures-no-scale-3"/></p>

</div>
<div id='tab-SD-hclust-get-signatures-no-scale-4'>
<pre><code class="r">get_signatures(res, k = 5, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-SD-hclust-get-signatures-no-scale-4-1.png" alt="plot of chunk tab-SD-hclust-get-signatures-no-scale-4"/></p>

</div>
<div id='tab-SD-hclust-get-signatures-no-scale-5'>
<pre><code class="r">get_signatures(res, k = 6, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-SD-hclust-get-signatures-no-scale-5-1.png" alt="plot of chunk tab-SD-hclust-get-signatures-no-scale-5"/></p>

</div>
</div>



Compare the overlap of signatures from different k:

```r
compare_signatures(res)
```

![plot of chunk SD-hclust-signature_compare](figure_cola/SD-hclust-signature_compare-1.png)

`get_signature()` returns a data frame invisibly. TO get the list of signatures, the function
call should be assigned to a variable explicitly. In following code, if `plot` argument is set
to `FALSE`, no heatmap is plotted while only the differential analysis is performed.

```r
# code only for demonstration
tb = get_signature(res, k = ..., plot = FALSE)
```

An example of the output of `tb` is:

```
#>   which_row         fdr    mean_1    mean_2 scaled_mean_1 scaled_mean_2 km
#> 1        38 0.042760348  8.373488  9.131774    -0.5533452     0.5164555  1
#> 2        40 0.018707592  7.106213  8.469186    -0.6173731     0.5762149  1
#> 3        55 0.019134737 10.221463 11.207825    -0.6159697     0.5749050  1
#> 4        59 0.006059896  5.921854  7.869574    -0.6899429     0.6439467  1
#> 5        60 0.018055526  8.928898 10.211722    -0.6204761     0.5791110  1
#> 6        98 0.009384629 15.714769 14.887706     0.6635654    -0.6193277  2
...
```

The columns in `tb` are:

1. `which_row`: row indices corresponding to the input matrix.
2. `fdr`: FDR for the differential test. 
3. `mean_x`: The mean value in group x.
4. `scaled_mean_x`: The mean value in group x after rows are scaled.
5. `km`: Row groups if k-means clustering is applied to rows.



UMAP plot which shows how samples are separated.


<script>
$( function() {
	$( '#tabs-SD-hclust-dimension-reduction' ).tabs();
} );
</script>
<div id='tabs-SD-hclust-dimension-reduction'>
<ul>
<li><a href='#tab-SD-hclust-dimension-reduction-1'>k = 2</a></li>
<li><a href='#tab-SD-hclust-dimension-reduction-2'>k = 3</a></li>
<li><a href='#tab-SD-hclust-dimension-reduction-3'>k = 4</a></li>
<li><a href='#tab-SD-hclust-dimension-reduction-4'>k = 5</a></li>
<li><a href='#tab-SD-hclust-dimension-reduction-5'>k = 6</a></li>
</ul>
<div id='tab-SD-hclust-dimension-reduction-1'>
<pre><code class="r">dimension_reduction(res, k = 2, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-SD-hclust-dimension-reduction-1-1.png" alt="plot of chunk tab-SD-hclust-dimension-reduction-1"/></p>

</div>
<div id='tab-SD-hclust-dimension-reduction-2'>
<pre><code class="r">dimension_reduction(res, k = 3, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-SD-hclust-dimension-reduction-2-1.png" alt="plot of chunk tab-SD-hclust-dimension-reduction-2"/></p>

</div>
<div id='tab-SD-hclust-dimension-reduction-3'>
<pre><code class="r">dimension_reduction(res, k = 4, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-SD-hclust-dimension-reduction-3-1.png" alt="plot of chunk tab-SD-hclust-dimension-reduction-3"/></p>

</div>
<div id='tab-SD-hclust-dimension-reduction-4'>
<pre><code class="r">dimension_reduction(res, k = 5, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-SD-hclust-dimension-reduction-4-1.png" alt="plot of chunk tab-SD-hclust-dimension-reduction-4"/></p>

</div>
<div id='tab-SD-hclust-dimension-reduction-5'>
<pre><code class="r">dimension_reduction(res, k = 6, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-SD-hclust-dimension-reduction-5-1.png" alt="plot of chunk tab-SD-hclust-dimension-reduction-5"/></p>

</div>
</div>


Following heatmap shows how subgroups are split when increasing `k`:

```r
collect_classes(res)
```

![plot of chunk SD-hclust-collect-classes](figure_cola/SD-hclust-collect-classes-1.png)


If matrix rows can be associated to genes, consider to use `functional_enrichment(res,
...)` to perform function enrichment for the signature genes. See [this vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/functional_enrichment.html) for more detailed explanations.


 

---------------------------------------------------




### SD:kmeans






The object with results only for a single top-value method and a single partition method 
can be extracted as:

```r
res = res_list["SD", "kmeans"]
# you can also extract it by
# res = res_list["SD:kmeans"]
```

A summary of `res` and all the functions that can be applied to it:

```r
res
```

```
#> A 'ConsensusPartition' object with k = 2, 3, 4, 5, 6.
#>   On a matrix with 15680 rows and 53 columns.
#>   Top rows (1000, 2000, 3000, 4000, 5000) are extracted by 'SD' method.
#>   Subgroups are detected by 'kmeans' method.
#>   Performed in total 1250 partitions by row resampling.
#>   Best k for subgroups seems to be 3.
#> 
#> Following methods can be applied to this 'ConsensusPartition' object:
#>  [1] "cola_report"             "collect_classes"         "collect_plots"          
#>  [4] "collect_stats"           "colnames"                "compare_signatures"     
#>  [7] "consensus_heatmap"       "dimension_reduction"     "functional_enrichment"  
#> [10] "get_anno_col"            "get_anno"                "get_classes"            
#> [13] "get_consensus"           "get_matrix"              "get_membership"         
#> [16] "get_param"               "get_signatures"          "get_stats"              
#> [19] "is_best_k"               "is_stable_k"             "membership_heatmap"     
#> [22] "ncol"                    "nrow"                    "plot_ecdf"              
#> [25] "rownames"                "select_partition_number" "show"                   
#> [28] "suggest_best_k"          "test_to_known_factors"
```

`collect_plots()` function collects all the plots made from `res` for all `k` (number of partitions)
into one single page to provide an easy and fast comparison between different `k`.

```r
collect_plots(res)
```

![plot of chunk SD-kmeans-collect-plots](figure_cola/SD-kmeans-collect-plots-1.png)

The plots are:

- The first row: a plot of the ECDF (empirical cumulative distribution
  function) curves of the consensus matrix for each `k` and the heatmap of
  predicted classes for each `k`.
- The second row: heatmaps of the consensus matrix for each `k`.
- The third row: heatmaps of the membership matrix for each `k`.
- The fouth row: heatmaps of the signatures for each `k`.

All the plots in panels can be made by individual functions and they are
plotted later in this section.

`select_partition_number()` produces several plots showing different
statistics for choosing "optimized" `k`. There are following statistics:

- ECDF curves of the consensus matrix for each `k`;
- 1-PAC. [The PAC
  score](https://en.wikipedia.org/wiki/Consensus_clustering#Over-interpretation_potential_of_consensus_clustering)
  measures the proportion of the ambiguous subgrouping.
- Mean silhouette score.
- Concordance. The mean probability of fiting the consensus class ids in all
  partitions.
- Area increased. Denote $A_k$ as the area under the ECDF curve for current
  `k`, the area increased is defined as $A_k - A_{k-1}$.
- Rand index. The percent of pairs of samples that are both in a same cluster
  or both are not in a same cluster in the partition of k and k-1.
- Jaccard index. The ratio of pairs of samples are both in a same cluster in
  the partition of k and k-1 and the pairs of samples are both in a same
  cluster in the partition k or k-1.

The detailed explanations of these statistics can be found in [the _cola_
vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/cola.html#toc_13).

Generally speaking, lower PAC score, higher mean silhouette score or higher
concordance corresponds to better partition. Rand index and Jaccard index
measure how similar the current partition is compared to partition with `k-1`.
If they are too similar, we won't accept `k` is better than `k-1`.

```r
select_partition_number(res)
```

![plot of chunk SD-kmeans-select-partition-number](figure_cola/SD-kmeans-select-partition-number-1.png)

The numeric values for all these statistics can be obtained by `get_stats()`.

```r
get_stats(res)
```

```
#>   k 1-PAC mean_silhouette concordance area_increased  Rand Jaccard
#> 2 2 0.742           0.822       0.907         0.3787 0.586   0.586
#> 3 3 0.576           0.875       0.909         0.5740 0.594   0.411
#> 4 4 0.550           0.379       0.730         0.1707 0.925   0.815
#> 5 5 0.656           0.743       0.811         0.0992 0.811   0.496
#> 6 6 0.716           0.710       0.788         0.0517 1.000   1.000
```

`suggest_best_k()` suggests the best $k$ based on these statistics. The rules are as follows:

- All $k$ with Jaccard index larger than 0.95 are removed because increasing
  $k$ does not provide enough extra information. If all $k$ are removed, it is
  marked as no subgroup is detected.
- For all $k$ with 1-PAC score larger than 0.9, the maximal $k$ is taken as
  the best $k$, and other $k$ are marked as optional $k$.
- If it does not fit the second rule. The $k$ with the maximal vote of the
  highest 1-PAC score, highest mean silhouette, and highest concordance is
  taken as the best $k$.

```r
suggest_best_k(res)
```

```
#> [1] 3
```


Following shows the table of the partitions (You need to click the **show/hide
code output** link to see it). The membership matrix (columns with name `p*`)
is inferred by
[`clue::cl_consensus()`](https://www.rdocumentation.org/link/cl_consensus?package=clue)
function with the `SE` method. Basically the value in the membership matrix
represents the probability to belong to a certain group. The finall class
label for an item is determined with the group with highest probability it
belongs to.

In `get_classes()` function, the entropy is calculated from the membership
matrix and the silhouette score is calculated from the consensus matrix.



<script>
$( function() {
	$( '#tabs-SD-kmeans-get-classes' ).tabs();
} );
</script>
<div id='tabs-SD-kmeans-get-classes'>
<ul>
<li><a href='#tab-SD-kmeans-get-classes-1'>k = 2</a></li>
<li><a href='#tab-SD-kmeans-get-classes-2'>k = 3</a></li>
<li><a href='#tab-SD-kmeans-get-classes-3'>k = 4</a></li>
<li><a href='#tab-SD-kmeans-get-classes-4'>k = 5</a></li>
<li><a href='#tab-SD-kmeans-get-classes-5'>k = 6</a></li>
</ul>

<div id='tab-SD-kmeans-get-classes-1'>
<p><a id='tab-SD-kmeans-get-classes-1-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 2), get_membership(res, k = 2))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2
#&gt; SRR1383358     2  0.2778      0.927 0.048 0.952
#&gt; SRR1383360     1  0.9922      0.400 0.552 0.448
#&gt; SRR1383359     2  0.2778      0.927 0.048 0.952
#&gt; SRR1383362     1  0.0672      0.768 0.992 0.008
#&gt; SRR1383361     2  0.2778      0.927 0.048 0.952
#&gt; SRR1383363     2  0.2778      0.927 0.048 0.952
#&gt; SRR1383364     2  0.3879      0.906 0.076 0.924
#&gt; SRR1383365     2  0.2778      0.927 0.048 0.952
#&gt; SRR1383366     2  0.1843      0.930 0.028 0.972
#&gt; SRR1383367     2  0.2778      0.927 0.048 0.952
#&gt; SRR1383368     1  0.9209      0.600 0.664 0.336
#&gt; SRR1383369     2  0.2778      0.927 0.048 0.952
#&gt; SRR1383370     2  0.2778      0.927 0.048 0.952
#&gt; SRR1383371     2  0.3879      0.906 0.076 0.924
#&gt; SRR1383372     2  0.2778      0.927 0.048 0.952
#&gt; SRR1383373     2  0.2778      0.927 0.048 0.952
#&gt; SRR1383374     2  0.1633      0.930 0.024 0.976
#&gt; SRR1383375     1  0.1843      0.780 0.972 0.028
#&gt; SRR1383376     2  0.0938      0.936 0.012 0.988
#&gt; SRR1383377     2  0.0938      0.936 0.012 0.988
#&gt; SRR1383378     2  0.8763      0.409 0.296 0.704
#&gt; SRR1383379     2  0.9209      0.280 0.336 0.664
#&gt; SRR1383380     1  0.9977      0.422 0.528 0.472
#&gt; SRR1383381     2  0.3114      0.915 0.056 0.944
#&gt; SRR1383382     1  0.1414      0.778 0.980 0.020
#&gt; SRR1383383     2  0.0672      0.937 0.008 0.992
#&gt; SRR1383385     1  0.1633      0.779 0.976 0.024
#&gt; SRR1383384     2  0.0938      0.936 0.012 0.988
#&gt; SRR1383386     1  0.2423      0.780 0.960 0.040
#&gt; SRR1383387     2  0.0938      0.936 0.012 0.988
#&gt; SRR1383389     2  0.1633      0.935 0.024 0.976
#&gt; SRR1383391     2  0.0672      0.937 0.008 0.992
#&gt; SRR1383388     1  0.9710      0.559 0.600 0.400
#&gt; SRR1383392     2  0.0672      0.936 0.008 0.992
#&gt; SRR1383390     2  0.0672      0.937 0.008 0.992
#&gt; SRR1383394     2  0.0938      0.936 0.012 0.988
#&gt; SRR1383393     1  0.1843      0.780 0.972 0.028
#&gt; SRR1383396     1  0.9866      0.473 0.568 0.432
#&gt; SRR1383395     2  0.0938      0.936 0.012 0.988
#&gt; SRR1383399     2  0.3114      0.915 0.056 0.944
#&gt; SRR1383400     1  0.1414      0.778 0.980 0.020
#&gt; SRR1383397     2  0.1414      0.932 0.020 0.980
#&gt; SRR1383401     2  0.0376      0.937 0.004 0.996
#&gt; SRR1383398     1  0.9977      0.422 0.528 0.472
#&gt; SRR1383402     2  0.0938      0.936 0.012 0.988
#&gt; SRR1383404     1  0.7883      0.699 0.764 0.236
#&gt; SRR1383403     1  0.1633      0.779 0.976 0.024
#&gt; SRR1383405     2  0.0938      0.936 0.012 0.988
#&gt; SRR1383406     2  0.8081      0.549 0.248 0.752
#&gt; SRR1383407     2  0.1633      0.935 0.024 0.976
#&gt; SRR1383408     2  0.0672      0.937 0.008 0.992
#&gt; SRR1383409     2  0.0672      0.937 0.008 0.992
#&gt; SRR1383410     2  0.0672      0.936 0.008 0.992
</code></pre>

<script>
$('#tab-SD-kmeans-get-classes-1-a').parent().next().next().hide();
$('#tab-SD-kmeans-get-classes-1-a').click(function(){
  $('#tab-SD-kmeans-get-classes-1-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-SD-kmeans-get-classes-2'>
<p><a id='tab-SD-kmeans-get-classes-2-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 3), get_membership(res, k = 3))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3
#&gt; SRR1383358     3  0.2261      0.936 0.000 0.068 0.932
#&gt; SRR1383360     3  0.7001      0.728 0.084 0.200 0.716
#&gt; SRR1383359     3  0.2261      0.936 0.000 0.068 0.932
#&gt; SRR1383362     1  0.1399      0.913 0.968 0.004 0.028
#&gt; SRR1383361     3  0.2261      0.936 0.000 0.068 0.932
#&gt; SRR1383363     3  0.2261      0.936 0.000 0.068 0.932
#&gt; SRR1383364     3  0.1399      0.907 0.004 0.028 0.968
#&gt; SRR1383365     3  0.2261      0.936 0.000 0.068 0.932
#&gt; SRR1383366     3  0.4346      0.845 0.000 0.184 0.816
#&gt; SRR1383367     3  0.2537      0.934 0.000 0.080 0.920
#&gt; SRR1383368     3  0.4443      0.865 0.084 0.052 0.864
#&gt; SRR1383369     3  0.1860      0.927 0.000 0.052 0.948
#&gt; SRR1383370     3  0.2537      0.934 0.000 0.080 0.920
#&gt; SRR1383371     3  0.1525      0.911 0.004 0.032 0.964
#&gt; SRR1383372     3  0.2537      0.934 0.000 0.080 0.920
#&gt; SRR1383373     3  0.2261      0.936 0.000 0.068 0.932
#&gt; SRR1383374     3  0.2537      0.934 0.000 0.080 0.920
#&gt; SRR1383375     1  0.1267      0.917 0.972 0.004 0.024
#&gt; SRR1383376     2  0.0892      0.905 0.000 0.980 0.020
#&gt; SRR1383377     2  0.2165      0.892 0.000 0.936 0.064
#&gt; SRR1383378     2  0.3896      0.886 0.008 0.864 0.128
#&gt; SRR1383379     2  0.0237      0.897 0.004 0.996 0.000
#&gt; SRR1383380     2  0.1774      0.877 0.024 0.960 0.016
#&gt; SRR1383381     3  0.4409      0.799 0.004 0.172 0.824
#&gt; SRR1383382     1  0.1399      0.913 0.968 0.004 0.028
#&gt; SRR1383383     2  0.3686      0.879 0.000 0.860 0.140
#&gt; SRR1383385     1  0.1267      0.916 0.972 0.004 0.024
#&gt; SRR1383384     2  0.2066      0.908 0.000 0.940 0.060
#&gt; SRR1383386     1  0.6483      0.315 0.600 0.392 0.008
#&gt; SRR1383387     2  0.0424      0.901 0.000 0.992 0.008
#&gt; SRR1383389     2  0.4346      0.840 0.000 0.816 0.184
#&gt; SRR1383391     2  0.3340      0.891 0.000 0.880 0.120
#&gt; SRR1383388     2  0.1482      0.882 0.020 0.968 0.012
#&gt; SRR1383392     2  0.2711      0.902 0.000 0.912 0.088
#&gt; SRR1383390     2  0.3619      0.881 0.000 0.864 0.136
#&gt; SRR1383394     2  0.0892      0.905 0.000 0.980 0.020
#&gt; SRR1383393     1  0.1267      0.917 0.972 0.004 0.024
#&gt; SRR1383396     2  0.4277      0.880 0.016 0.852 0.132
#&gt; SRR1383395     2  0.2165      0.892 0.000 0.936 0.064
#&gt; SRR1383399     3  0.4409      0.799 0.004 0.172 0.824
#&gt; SRR1383400     1  0.1399      0.913 0.968 0.004 0.028
#&gt; SRR1383397     2  0.0237      0.897 0.004 0.996 0.000
#&gt; SRR1383401     2  0.3879      0.871 0.000 0.848 0.152
#&gt; SRR1383398     2  0.1774      0.877 0.024 0.960 0.016
#&gt; SRR1383402     2  0.2066      0.908 0.000 0.940 0.060
#&gt; SRR1383404     2  0.5541      0.606 0.252 0.740 0.008
#&gt; SRR1383403     1  0.1267      0.916 0.972 0.004 0.024
#&gt; SRR1383405     2  0.0424      0.901 0.000 0.992 0.008
#&gt; SRR1383406     2  0.0237      0.897 0.004 0.996 0.000
#&gt; SRR1383407     2  0.5529      0.661 0.000 0.704 0.296
#&gt; SRR1383408     2  0.3619      0.881 0.000 0.864 0.136
#&gt; SRR1383409     2  0.3412      0.889 0.000 0.876 0.124
#&gt; SRR1383410     2  0.2066      0.908 0.000 0.940 0.060
</code></pre>

<script>
$('#tab-SD-kmeans-get-classes-2-a').parent().next().next().hide();
$('#tab-SD-kmeans-get-classes-2-a').click(function(){
  $('#tab-SD-kmeans-get-classes-2-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-SD-kmeans-get-classes-3'>
<p><a id='tab-SD-kmeans-get-classes-3-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 4), get_membership(res, k = 4))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4
#&gt; SRR1383358     3  0.0804     0.8277 0.000 0.008 0.980 0.012
#&gt; SRR1383360     3  0.7139     0.5578 0.052 0.248 0.624 0.076
#&gt; SRR1383359     3  0.1256     0.8255 0.000 0.008 0.964 0.028
#&gt; SRR1383362     1  0.0000     0.8958 1.000 0.000 0.000 0.000
#&gt; SRR1383361     3  0.1767     0.8337 0.000 0.012 0.944 0.044
#&gt; SRR1383363     3  0.1576     0.8351 0.000 0.004 0.948 0.048
#&gt; SRR1383364     3  0.4250     0.6984 0.000 0.000 0.724 0.276
#&gt; SRR1383365     3  0.1042     0.8276 0.000 0.008 0.972 0.020
#&gt; SRR1383366     3  0.3612     0.7853 0.000 0.100 0.856 0.044
#&gt; SRR1383367     3  0.1975     0.8312 0.000 0.016 0.936 0.048
#&gt; SRR1383368     3  0.5456     0.7376 0.080 0.056 0.784 0.080
#&gt; SRR1383369     3  0.4283     0.7177 0.000 0.004 0.740 0.256
#&gt; SRR1383370     3  0.1975     0.8312 0.000 0.016 0.936 0.048
#&gt; SRR1383371     3  0.4250     0.6984 0.000 0.000 0.724 0.276
#&gt; SRR1383372     3  0.1975     0.8312 0.000 0.016 0.936 0.048
#&gt; SRR1383373     3  0.1489     0.8348 0.000 0.004 0.952 0.044
#&gt; SRR1383374     3  0.2335     0.8278 0.000 0.020 0.920 0.060
#&gt; SRR1383375     1  0.4776     0.9162 0.772 0.040 0.004 0.184
#&gt; SRR1383376     2  0.5548    -0.1366 0.000 0.628 0.032 0.340
#&gt; SRR1383377     2  0.5457     0.2458 0.000 0.728 0.088 0.184
#&gt; SRR1383378     2  0.6265    -0.4928 0.000 0.500 0.056 0.444
#&gt; SRR1383379     2  0.0188     0.3920 0.000 0.996 0.004 0.000
#&gt; SRR1383380     2  0.3236     0.3533 0.004 0.856 0.004 0.136
#&gt; SRR1383381     3  0.5861     0.4488 0.000 0.032 0.492 0.476
#&gt; SRR1383382     1  0.0000     0.8958 1.000 0.000 0.000 0.000
#&gt; SRR1383383     2  0.6452    -0.6415 0.000 0.472 0.068 0.460
#&gt; SRR1383385     1  0.4562     0.9149 0.764 0.028 0.000 0.208
#&gt; SRR1383384     2  0.6087    -0.3960 0.000 0.540 0.048 0.412
#&gt; SRR1383386     2  0.6929    -0.0841 0.416 0.492 0.008 0.084
#&gt; SRR1383387     2  0.2611     0.3546 0.000 0.896 0.008 0.096
#&gt; SRR1383389     4  0.7081     0.7217 0.000 0.352 0.136 0.512
#&gt; SRR1383391     2  0.6376    -0.5375 0.000 0.504 0.064 0.432
#&gt; SRR1383388     2  0.2164     0.3730 0.004 0.924 0.004 0.068
#&gt; SRR1383392     2  0.6757    -0.3640 0.000 0.524 0.100 0.376
#&gt; SRR1383390     2  0.6447    -0.5945 0.000 0.484 0.068 0.448
#&gt; SRR1383394     2  0.5548    -0.1366 0.000 0.628 0.032 0.340
#&gt; SRR1383393     1  0.4776     0.9162 0.772 0.040 0.004 0.184
#&gt; SRR1383396     2  0.6055    -0.1113 0.004 0.604 0.048 0.344
#&gt; SRR1383395     2  0.5457     0.2458 0.000 0.728 0.088 0.184
#&gt; SRR1383399     3  0.5861     0.4488 0.000 0.032 0.492 0.476
#&gt; SRR1383400     1  0.0000     0.8958 1.000 0.000 0.000 0.000
#&gt; SRR1383397     2  0.0336     0.3919 0.000 0.992 0.000 0.008
#&gt; SRR1383401     4  0.6452     0.4790 0.000 0.464 0.068 0.468
#&gt; SRR1383398     2  0.3236     0.3533 0.004 0.856 0.004 0.136
#&gt; SRR1383402     2  0.6016    -0.3818 0.000 0.544 0.044 0.412
#&gt; SRR1383404     2  0.5548     0.2800 0.168 0.740 0.008 0.084
#&gt; SRR1383403     1  0.4562     0.9149 0.764 0.028 0.000 0.208
#&gt; SRR1383405     2  0.2611     0.3546 0.000 0.896 0.008 0.096
#&gt; SRR1383406     2  0.0376     0.3915 0.000 0.992 0.004 0.004
#&gt; SRR1383407     4  0.7344     0.6677 0.000 0.316 0.180 0.504
#&gt; SRR1383408     2  0.6447    -0.5945 0.000 0.484 0.068 0.448
#&gt; SRR1383409     2  0.6376    -0.5375 0.000 0.504 0.064 0.432
#&gt; SRR1383410     2  0.6067    -0.2647 0.000 0.572 0.052 0.376
</code></pre>

<script>
$('#tab-SD-kmeans-get-classes-3-a').parent().next().next().hide();
$('#tab-SD-kmeans-get-classes-3-a').click(function(){
  $('#tab-SD-kmeans-get-classes-3-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-SD-kmeans-get-classes-4'>
<p><a id='tab-SD-kmeans-get-classes-4-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 5), get_membership(res, k = 5))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4    p5
#&gt; SRR1383358     3  0.0740      0.919 0.000 0.004 0.980 0.008 0.008
#&gt; SRR1383360     3  0.4134      0.745 0.012 0.012 0.808 0.132 0.036
#&gt; SRR1383359     3  0.2074      0.872 0.000 0.004 0.920 0.016 0.060
#&gt; SRR1383362     1  0.2873      0.848 0.856 0.000 0.000 0.016 0.128
#&gt; SRR1383361     3  0.0510      0.932 0.000 0.016 0.984 0.000 0.000
#&gt; SRR1383363     3  0.0703      0.934 0.000 0.024 0.976 0.000 0.000
#&gt; SRR1383364     5  0.4025      0.800 0.000 0.008 0.292 0.000 0.700
#&gt; SRR1383365     3  0.1901      0.880 0.000 0.004 0.928 0.012 0.056
#&gt; SRR1383366     3  0.1569      0.914 0.000 0.012 0.948 0.032 0.008
#&gt; SRR1383367     3  0.0703      0.934 0.000 0.024 0.976 0.000 0.000
#&gt; SRR1383368     3  0.3507      0.824 0.012 0.024 0.864 0.064 0.036
#&gt; SRR1383369     5  0.4280      0.776 0.000 0.004 0.312 0.008 0.676
#&gt; SRR1383370     3  0.0865      0.933 0.000 0.024 0.972 0.004 0.000
#&gt; SRR1383371     5  0.4025      0.800 0.000 0.008 0.292 0.000 0.700
#&gt; SRR1383372     3  0.0703      0.934 0.000 0.024 0.976 0.000 0.000
#&gt; SRR1383373     3  0.0703      0.934 0.000 0.024 0.976 0.000 0.000
#&gt; SRR1383374     3  0.0992      0.926 0.000 0.024 0.968 0.000 0.008
#&gt; SRR1383375     1  0.2681      0.866 0.876 0.000 0.004 0.108 0.012
#&gt; SRR1383376     2  0.4267      0.596 0.000 0.736 0.004 0.232 0.028
#&gt; SRR1383377     4  0.6278      0.521 0.000 0.292 0.040 0.584 0.084
#&gt; SRR1383378     2  0.4140      0.627 0.000 0.792 0.012 0.148 0.048
#&gt; SRR1383379     4  0.3430      0.712 0.000 0.220 0.000 0.776 0.004
#&gt; SRR1383380     4  0.4358      0.685 0.052 0.108 0.000 0.800 0.040
#&gt; SRR1383381     5  0.6126      0.731 0.000 0.196 0.120 0.040 0.644
#&gt; SRR1383382     1  0.2873      0.848 0.856 0.000 0.000 0.016 0.128
#&gt; SRR1383383     2  0.1179      0.770 0.000 0.964 0.016 0.004 0.016
#&gt; SRR1383385     1  0.2927      0.868 0.868 0.000 0.000 0.092 0.040
#&gt; SRR1383384     2  0.2935      0.756 0.000 0.876 0.012 0.088 0.024
#&gt; SRR1383386     4  0.7273      0.204 0.332 0.164 0.004 0.460 0.040
#&gt; SRR1383387     4  0.4836      0.565 0.000 0.356 0.000 0.612 0.032
#&gt; SRR1383389     2  0.3553      0.695 0.000 0.852 0.048 0.072 0.028
#&gt; SRR1383391     2  0.2177      0.768 0.000 0.908 0.008 0.080 0.004
#&gt; SRR1383388     4  0.4733      0.652 0.028 0.196 0.004 0.744 0.028
#&gt; SRR1383392     2  0.5473      0.573 0.000 0.692 0.048 0.208 0.052
#&gt; SRR1383390     2  0.0981      0.774 0.000 0.972 0.008 0.012 0.008
#&gt; SRR1383394     2  0.4267      0.596 0.000 0.736 0.004 0.232 0.028
#&gt; SRR1383393     1  0.2681      0.866 0.876 0.000 0.004 0.108 0.012
#&gt; SRR1383396     2  0.5842      0.227 0.008 0.572 0.012 0.352 0.056
#&gt; SRR1383395     4  0.6278      0.521 0.000 0.292 0.040 0.584 0.084
#&gt; SRR1383399     5  0.6126      0.731 0.000 0.196 0.120 0.040 0.644
#&gt; SRR1383400     1  0.2873      0.848 0.856 0.000 0.000 0.016 0.128
#&gt; SRR1383397     4  0.3430      0.712 0.000 0.220 0.000 0.776 0.004
#&gt; SRR1383401     2  0.1278      0.769 0.000 0.960 0.020 0.004 0.016
#&gt; SRR1383398     4  0.4358      0.685 0.052 0.108 0.000 0.800 0.040
#&gt; SRR1383402     2  0.2935      0.756 0.000 0.876 0.012 0.088 0.024
#&gt; SRR1383404     4  0.6217      0.577 0.120 0.188 0.004 0.648 0.040
#&gt; SRR1383403     1  0.2927      0.868 0.868 0.000 0.000 0.092 0.040
#&gt; SRR1383405     4  0.4836      0.565 0.000 0.356 0.000 0.612 0.032
#&gt; SRR1383406     4  0.3242      0.712 0.000 0.216 0.000 0.784 0.000
#&gt; SRR1383407     2  0.4005      0.684 0.000 0.828 0.056 0.072 0.044
#&gt; SRR1383408     2  0.0981      0.774 0.000 0.972 0.008 0.012 0.008
#&gt; SRR1383409     2  0.2177      0.768 0.000 0.908 0.008 0.080 0.004
#&gt; SRR1383410     2  0.5188      0.584 0.000 0.708 0.032 0.208 0.052
</code></pre>

<script>
$('#tab-SD-kmeans-get-classes-4-a').parent().next().next().hide();
$('#tab-SD-kmeans-get-classes-4-a').click(function(){
  $('#tab-SD-kmeans-get-classes-4-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-SD-kmeans-get-classes-5'>
<p><a id='tab-SD-kmeans-get-classes-5-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 6), get_membership(res, k = 6))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4    p5 p6
#&gt; SRR1383358     3  0.1844      0.871 0.000 0.004 0.924 0.000 0.024 NA
#&gt; SRR1383360     3  0.5024      0.673 0.012 0.008 0.740 0.060 0.052 NA
#&gt; SRR1383359     3  0.3863      0.766 0.000 0.008 0.796 0.004 0.100 NA
#&gt; SRR1383362     1  0.3727      0.745 0.612 0.000 0.000 0.000 0.000 NA
#&gt; SRR1383361     3  0.0260      0.902 0.000 0.008 0.992 0.000 0.000 NA
#&gt; SRR1383363     3  0.0405      0.902 0.000 0.008 0.988 0.000 0.000 NA
#&gt; SRR1383364     5  0.2668      0.828 0.000 0.000 0.168 0.000 0.828 NA
#&gt; SRR1383365     3  0.3497      0.788 0.000 0.004 0.820 0.004 0.100 NA
#&gt; SRR1383366     3  0.1527      0.892 0.000 0.012 0.948 0.012 0.008 NA
#&gt; SRR1383367     3  0.0405      0.902 0.000 0.008 0.988 0.000 0.000 NA
#&gt; SRR1383368     3  0.4513      0.700 0.012 0.008 0.768 0.032 0.040 NA
#&gt; SRR1383369     5  0.3715      0.792 0.000 0.000 0.188 0.000 0.764 NA
#&gt; SRR1383370     3  0.0551      0.902 0.000 0.008 0.984 0.000 0.004 NA
#&gt; SRR1383371     5  0.2668      0.828 0.000 0.000 0.168 0.000 0.828 NA
#&gt; SRR1383372     3  0.0260      0.902 0.000 0.008 0.992 0.000 0.000 NA
#&gt; SRR1383373     3  0.0260      0.902 0.000 0.008 0.992 0.000 0.000 NA
#&gt; SRR1383374     3  0.1251      0.889 0.000 0.024 0.956 0.000 0.008 NA
#&gt; SRR1383375     1  0.1672      0.773 0.932 0.000 0.000 0.016 0.004 NA
#&gt; SRR1383376     2  0.4990      0.587 0.000 0.676 0.004 0.220 0.016 NA
#&gt; SRR1383377     4  0.6699      0.523 0.008 0.136 0.016 0.572 0.068 NA
#&gt; SRR1383378     2  0.5860      0.505 0.016 0.672 0.012 0.128 0.044 NA
#&gt; SRR1383379     4  0.1812      0.712 0.000 0.080 0.000 0.912 0.000 NA
#&gt; SRR1383380     4  0.4866      0.659 0.116 0.040 0.000 0.752 0.032 NA
#&gt; SRR1383381     5  0.5751      0.751 0.008 0.132 0.064 0.008 0.676 NA
#&gt; SRR1383382     1  0.3727      0.745 0.612 0.000 0.000 0.000 0.000 NA
#&gt; SRR1383383     2  0.2159      0.739 0.000 0.904 0.012 0.000 0.012 NA
#&gt; SRR1383385     1  0.1875      0.784 0.928 0.000 0.000 0.020 0.032 NA
#&gt; SRR1383384     2  0.3988      0.723 0.000 0.808 0.016 0.080 0.020 NA
#&gt; SRR1383386     4  0.7626      0.420 0.180 0.108 0.012 0.508 0.044 NA
#&gt; SRR1383387     4  0.4813      0.560 0.000 0.220 0.000 0.680 0.012 NA
#&gt; SRR1383389     2  0.4435      0.667 0.000 0.780 0.044 0.040 0.024 NA
#&gt; SRR1383391     2  0.2252      0.743 0.000 0.900 0.016 0.072 0.000 NA
#&gt; SRR1383388     4  0.5489      0.616 0.044 0.120 0.008 0.708 0.020 NA
#&gt; SRR1383392     2  0.6405      0.548 0.000 0.580 0.024 0.192 0.040 NA
#&gt; SRR1383390     2  0.1121      0.746 0.000 0.964 0.016 0.008 0.004 NA
#&gt; SRR1383394     2  0.4990      0.587 0.000 0.676 0.004 0.220 0.016 NA
#&gt; SRR1383393     1  0.1672      0.773 0.932 0.000 0.000 0.016 0.004 NA
#&gt; SRR1383396     2  0.7492      0.143 0.048 0.472 0.008 0.244 0.052 NA
#&gt; SRR1383395     4  0.6699      0.523 0.008 0.136 0.016 0.572 0.068 NA
#&gt; SRR1383399     5  0.5751      0.751 0.008 0.132 0.064 0.008 0.676 NA
#&gt; SRR1383400     1  0.3727      0.745 0.612 0.000 0.000 0.000 0.000 NA
#&gt; SRR1383397     4  0.1753      0.711 0.000 0.084 0.000 0.912 0.000 NA
#&gt; SRR1383401     2  0.2159      0.739 0.000 0.904 0.012 0.000 0.012 NA
#&gt; SRR1383398     4  0.4866      0.659 0.116 0.040 0.000 0.752 0.032 NA
#&gt; SRR1383402     2  0.3949      0.722 0.000 0.808 0.012 0.084 0.020 NA
#&gt; SRR1383404     4  0.7125      0.517 0.112 0.108 0.012 0.576 0.044 NA
#&gt; SRR1383403     1  0.1875      0.784 0.928 0.000 0.000 0.020 0.032 NA
#&gt; SRR1383405     4  0.4813      0.560 0.000 0.220 0.000 0.680 0.012 NA
#&gt; SRR1383406     4  0.1812      0.712 0.000 0.080 0.000 0.912 0.000 NA
#&gt; SRR1383407     2  0.4738      0.656 0.000 0.760 0.044 0.040 0.036 NA
#&gt; SRR1383408     2  0.1121      0.748 0.000 0.964 0.016 0.008 0.004 NA
#&gt; SRR1383409     2  0.2252      0.743 0.000 0.900 0.016 0.072 0.000 NA
#&gt; SRR1383410     2  0.6405      0.548 0.000 0.580 0.024 0.192 0.040 NA
</code></pre>

<script>
$('#tab-SD-kmeans-get-classes-5-a').parent().next().next().hide();
$('#tab-SD-kmeans-get-classes-5-a').click(function(){
  $('#tab-SD-kmeans-get-classes-5-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>
</div>

Heatmaps for the consensus matrix. It visualizes the probability of two
samples to be in a same group.



<script>
$( function() {
	$( '#tabs-SD-kmeans-consensus-heatmap' ).tabs();
} );
</script>
<div id='tabs-SD-kmeans-consensus-heatmap'>
<ul>
<li><a href='#tab-SD-kmeans-consensus-heatmap-1'>k = 2</a></li>
<li><a href='#tab-SD-kmeans-consensus-heatmap-2'>k = 3</a></li>
<li><a href='#tab-SD-kmeans-consensus-heatmap-3'>k = 4</a></li>
<li><a href='#tab-SD-kmeans-consensus-heatmap-4'>k = 5</a></li>
<li><a href='#tab-SD-kmeans-consensus-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-SD-kmeans-consensus-heatmap-1'>
<pre><code class="r">consensus_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-SD-kmeans-consensus-heatmap-1-1.png" alt="plot of chunk tab-SD-kmeans-consensus-heatmap-1"/></p>

</div>
<div id='tab-SD-kmeans-consensus-heatmap-2'>
<pre><code class="r">consensus_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-SD-kmeans-consensus-heatmap-2-1.png" alt="plot of chunk tab-SD-kmeans-consensus-heatmap-2"/></p>

</div>
<div id='tab-SD-kmeans-consensus-heatmap-3'>
<pre><code class="r">consensus_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-SD-kmeans-consensus-heatmap-3-1.png" alt="plot of chunk tab-SD-kmeans-consensus-heatmap-3"/></p>

</div>
<div id='tab-SD-kmeans-consensus-heatmap-4'>
<pre><code class="r">consensus_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-SD-kmeans-consensus-heatmap-4-1.png" alt="plot of chunk tab-SD-kmeans-consensus-heatmap-4"/></p>

</div>
<div id='tab-SD-kmeans-consensus-heatmap-5'>
<pre><code class="r">consensus_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-SD-kmeans-consensus-heatmap-5-1.png" alt="plot of chunk tab-SD-kmeans-consensus-heatmap-5"/></p>

</div>
</div>

Heatmaps for the membership of samples in all partitions to see how consistent they are:




<script>
$( function() {
	$( '#tabs-SD-kmeans-membership-heatmap' ).tabs();
} );
</script>
<div id='tabs-SD-kmeans-membership-heatmap'>
<ul>
<li><a href='#tab-SD-kmeans-membership-heatmap-1'>k = 2</a></li>
<li><a href='#tab-SD-kmeans-membership-heatmap-2'>k = 3</a></li>
<li><a href='#tab-SD-kmeans-membership-heatmap-3'>k = 4</a></li>
<li><a href='#tab-SD-kmeans-membership-heatmap-4'>k = 5</a></li>
<li><a href='#tab-SD-kmeans-membership-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-SD-kmeans-membership-heatmap-1'>
<pre><code class="r">membership_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-SD-kmeans-membership-heatmap-1-1.png" alt="plot of chunk tab-SD-kmeans-membership-heatmap-1"/></p>

</div>
<div id='tab-SD-kmeans-membership-heatmap-2'>
<pre><code class="r">membership_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-SD-kmeans-membership-heatmap-2-1.png" alt="plot of chunk tab-SD-kmeans-membership-heatmap-2"/></p>

</div>
<div id='tab-SD-kmeans-membership-heatmap-3'>
<pre><code class="r">membership_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-SD-kmeans-membership-heatmap-3-1.png" alt="plot of chunk tab-SD-kmeans-membership-heatmap-3"/></p>

</div>
<div id='tab-SD-kmeans-membership-heatmap-4'>
<pre><code class="r">membership_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-SD-kmeans-membership-heatmap-4-1.png" alt="plot of chunk tab-SD-kmeans-membership-heatmap-4"/></p>

</div>
<div id='tab-SD-kmeans-membership-heatmap-5'>
<pre><code class="r">membership_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-SD-kmeans-membership-heatmap-5-1.png" alt="plot of chunk tab-SD-kmeans-membership-heatmap-5"/></p>

</div>
</div>

As soon as we have had the classes for columns, we can look for signatures
which are significantly different between classes which can be candidate marks
for certain classes. Following are the heatmaps for signatures.



Signature heatmaps where rows are scaled:



<script>
$( function() {
	$( '#tabs-SD-kmeans-get-signatures' ).tabs();
} );
</script>
<div id='tabs-SD-kmeans-get-signatures'>
<ul>
<li><a href='#tab-SD-kmeans-get-signatures-1'>k = 2</a></li>
<li><a href='#tab-SD-kmeans-get-signatures-2'>k = 3</a></li>
<li><a href='#tab-SD-kmeans-get-signatures-3'>k = 4</a></li>
<li><a href='#tab-SD-kmeans-get-signatures-4'>k = 5</a></li>
<li><a href='#tab-SD-kmeans-get-signatures-5'>k = 6</a></li>
</ul>
<div id='tab-SD-kmeans-get-signatures-1'>
<pre><code class="r">get_signatures(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-SD-kmeans-get-signatures-1-1.png" alt="plot of chunk tab-SD-kmeans-get-signatures-1"/></p>

</div>
<div id='tab-SD-kmeans-get-signatures-2'>
<pre><code class="r">get_signatures(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-SD-kmeans-get-signatures-2-1.png" alt="plot of chunk tab-SD-kmeans-get-signatures-2"/></p>

</div>
<div id='tab-SD-kmeans-get-signatures-3'>
<pre><code class="r">get_signatures(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-SD-kmeans-get-signatures-3-1.png" alt="plot of chunk tab-SD-kmeans-get-signatures-3"/></p>

</div>
<div id='tab-SD-kmeans-get-signatures-4'>
<pre><code class="r">get_signatures(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-SD-kmeans-get-signatures-4-1.png" alt="plot of chunk tab-SD-kmeans-get-signatures-4"/></p>

</div>
<div id='tab-SD-kmeans-get-signatures-5'>
<pre><code class="r">get_signatures(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-SD-kmeans-get-signatures-5-1.png" alt="plot of chunk tab-SD-kmeans-get-signatures-5"/></p>

</div>
</div>



Signature heatmaps where rows are not scaled:


<script>
$( function() {
	$( '#tabs-SD-kmeans-get-signatures-no-scale' ).tabs();
} );
</script>
<div id='tabs-SD-kmeans-get-signatures-no-scale'>
<ul>
<li><a href='#tab-SD-kmeans-get-signatures-no-scale-1'>k = 2</a></li>
<li><a href='#tab-SD-kmeans-get-signatures-no-scale-2'>k = 3</a></li>
<li><a href='#tab-SD-kmeans-get-signatures-no-scale-3'>k = 4</a></li>
<li><a href='#tab-SD-kmeans-get-signatures-no-scale-4'>k = 5</a></li>
<li><a href='#tab-SD-kmeans-get-signatures-no-scale-5'>k = 6</a></li>
</ul>
<div id='tab-SD-kmeans-get-signatures-no-scale-1'>
<pre><code class="r">get_signatures(res, k = 2, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-SD-kmeans-get-signatures-no-scale-1-1.png" alt="plot of chunk tab-SD-kmeans-get-signatures-no-scale-1"/></p>

</div>
<div id='tab-SD-kmeans-get-signatures-no-scale-2'>
<pre><code class="r">get_signatures(res, k = 3, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-SD-kmeans-get-signatures-no-scale-2-1.png" alt="plot of chunk tab-SD-kmeans-get-signatures-no-scale-2"/></p>

</div>
<div id='tab-SD-kmeans-get-signatures-no-scale-3'>
<pre><code class="r">get_signatures(res, k = 4, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-SD-kmeans-get-signatures-no-scale-3-1.png" alt="plot of chunk tab-SD-kmeans-get-signatures-no-scale-3"/></p>

</div>
<div id='tab-SD-kmeans-get-signatures-no-scale-4'>
<pre><code class="r">get_signatures(res, k = 5, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-SD-kmeans-get-signatures-no-scale-4-1.png" alt="plot of chunk tab-SD-kmeans-get-signatures-no-scale-4"/></p>

</div>
<div id='tab-SD-kmeans-get-signatures-no-scale-5'>
<pre><code class="r">get_signatures(res, k = 6, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-SD-kmeans-get-signatures-no-scale-5-1.png" alt="plot of chunk tab-SD-kmeans-get-signatures-no-scale-5"/></p>

</div>
</div>



Compare the overlap of signatures from different k:

```r
compare_signatures(res)
```

![plot of chunk SD-kmeans-signature_compare](figure_cola/SD-kmeans-signature_compare-1.png)

`get_signature()` returns a data frame invisibly. TO get the list of signatures, the function
call should be assigned to a variable explicitly. In following code, if `plot` argument is set
to `FALSE`, no heatmap is plotted while only the differential analysis is performed.

```r
# code only for demonstration
tb = get_signature(res, k = ..., plot = FALSE)
```

An example of the output of `tb` is:

```
#>   which_row         fdr    mean_1    mean_2 scaled_mean_1 scaled_mean_2 km
#> 1        38 0.042760348  8.373488  9.131774    -0.5533452     0.5164555  1
#> 2        40 0.018707592  7.106213  8.469186    -0.6173731     0.5762149  1
#> 3        55 0.019134737 10.221463 11.207825    -0.6159697     0.5749050  1
#> 4        59 0.006059896  5.921854  7.869574    -0.6899429     0.6439467  1
#> 5        60 0.018055526  8.928898 10.211722    -0.6204761     0.5791110  1
#> 6        98 0.009384629 15.714769 14.887706     0.6635654    -0.6193277  2
...
```

The columns in `tb` are:

1. `which_row`: row indices corresponding to the input matrix.
2. `fdr`: FDR for the differential test. 
3. `mean_x`: The mean value in group x.
4. `scaled_mean_x`: The mean value in group x after rows are scaled.
5. `km`: Row groups if k-means clustering is applied to rows.



UMAP plot which shows how samples are separated.


<script>
$( function() {
	$( '#tabs-SD-kmeans-dimension-reduction' ).tabs();
} );
</script>
<div id='tabs-SD-kmeans-dimension-reduction'>
<ul>
<li><a href='#tab-SD-kmeans-dimension-reduction-1'>k = 2</a></li>
<li><a href='#tab-SD-kmeans-dimension-reduction-2'>k = 3</a></li>
<li><a href='#tab-SD-kmeans-dimension-reduction-3'>k = 4</a></li>
<li><a href='#tab-SD-kmeans-dimension-reduction-4'>k = 5</a></li>
<li><a href='#tab-SD-kmeans-dimension-reduction-5'>k = 6</a></li>
</ul>
<div id='tab-SD-kmeans-dimension-reduction-1'>
<pre><code class="r">dimension_reduction(res, k = 2, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-SD-kmeans-dimension-reduction-1-1.png" alt="plot of chunk tab-SD-kmeans-dimension-reduction-1"/></p>

</div>
<div id='tab-SD-kmeans-dimension-reduction-2'>
<pre><code class="r">dimension_reduction(res, k = 3, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-SD-kmeans-dimension-reduction-2-1.png" alt="plot of chunk tab-SD-kmeans-dimension-reduction-2"/></p>

</div>
<div id='tab-SD-kmeans-dimension-reduction-3'>
<pre><code class="r">dimension_reduction(res, k = 4, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-SD-kmeans-dimension-reduction-3-1.png" alt="plot of chunk tab-SD-kmeans-dimension-reduction-3"/></p>

</div>
<div id='tab-SD-kmeans-dimension-reduction-4'>
<pre><code class="r">dimension_reduction(res, k = 5, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-SD-kmeans-dimension-reduction-4-1.png" alt="plot of chunk tab-SD-kmeans-dimension-reduction-4"/></p>

</div>
<div id='tab-SD-kmeans-dimension-reduction-5'>
<pre><code class="r">dimension_reduction(res, k = 6, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-SD-kmeans-dimension-reduction-5-1.png" alt="plot of chunk tab-SD-kmeans-dimension-reduction-5"/></p>

</div>
</div>


Following heatmap shows how subgroups are split when increasing `k`:

```r
collect_classes(res)
```

![plot of chunk SD-kmeans-collect-classes](figure_cola/SD-kmeans-collect-classes-1.png)


If matrix rows can be associated to genes, consider to use `functional_enrichment(res,
...)` to perform function enrichment for the signature genes. See [this vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/functional_enrichment.html) for more detailed explanations.


 

---------------------------------------------------




### SD:skmeans**






The object with results only for a single top-value method and a single partition method 
can be extracted as:

```r
res = res_list["SD", "skmeans"]
# you can also extract it by
# res = res_list["SD:skmeans"]
```

A summary of `res` and all the functions that can be applied to it:

```r
res
```

```
#> A 'ConsensusPartition' object with k = 2, 3, 4, 5, 6.
#>   On a matrix with 15680 rows and 53 columns.
#>   Top rows (1000, 2000, 3000, 4000, 5000) are extracted by 'SD' method.
#>   Subgroups are detected by 'skmeans' method.
#>   Performed in total 1250 partitions by row resampling.
#>   Best k for subgroups seems to be 3.
#> 
#> Following methods can be applied to this 'ConsensusPartition' object:
#>  [1] "cola_report"             "collect_classes"         "collect_plots"          
#>  [4] "collect_stats"           "colnames"                "compare_signatures"     
#>  [7] "consensus_heatmap"       "dimension_reduction"     "functional_enrichment"  
#> [10] "get_anno_col"            "get_anno"                "get_classes"            
#> [13] "get_consensus"           "get_matrix"              "get_membership"         
#> [16] "get_param"               "get_signatures"          "get_stats"              
#> [19] "is_best_k"               "is_stable_k"             "membership_heatmap"     
#> [22] "ncol"                    "nrow"                    "plot_ecdf"              
#> [25] "rownames"                "select_partition_number" "show"                   
#> [28] "suggest_best_k"          "test_to_known_factors"
```

`collect_plots()` function collects all the plots made from `res` for all `k` (number of partitions)
into one single page to provide an easy and fast comparison between different `k`.

```r
collect_plots(res)
```

![plot of chunk SD-skmeans-collect-plots](figure_cola/SD-skmeans-collect-plots-1.png)

The plots are:

- The first row: a plot of the ECDF (empirical cumulative distribution
  function) curves of the consensus matrix for each `k` and the heatmap of
  predicted classes for each `k`.
- The second row: heatmaps of the consensus matrix for each `k`.
- The third row: heatmaps of the membership matrix for each `k`.
- The fouth row: heatmaps of the signatures for each `k`.

All the plots in panels can be made by individual functions and they are
plotted later in this section.

`select_partition_number()` produces several plots showing different
statistics for choosing "optimized" `k`. There are following statistics:

- ECDF curves of the consensus matrix for each `k`;
- 1-PAC. [The PAC
  score](https://en.wikipedia.org/wiki/Consensus_clustering#Over-interpretation_potential_of_consensus_clustering)
  measures the proportion of the ambiguous subgrouping.
- Mean silhouette score.
- Concordance. The mean probability of fiting the consensus class ids in all
  partitions.
- Area increased. Denote $A_k$ as the area under the ECDF curve for current
  `k`, the area increased is defined as $A_k - A_{k-1}$.
- Rand index. The percent of pairs of samples that are both in a same cluster
  or both are not in a same cluster in the partition of k and k-1.
- Jaccard index. The ratio of pairs of samples are both in a same cluster in
  the partition of k and k-1 and the pairs of samples are both in a same
  cluster in the partition k or k-1.

The detailed explanations of these statistics can be found in [the _cola_
vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/cola.html#toc_13).

Generally speaking, lower PAC score, higher mean silhouette score or higher
concordance corresponds to better partition. Rand index and Jaccard index
measure how similar the current partition is compared to partition with `k-1`.
If they are too similar, we won't accept `k` is better than `k-1`.

```r
select_partition_number(res)
```

![plot of chunk SD-skmeans-select-partition-number](figure_cola/SD-skmeans-select-partition-number-1.png)

The numeric values for all these statistics can be obtained by `get_stats()`.

```r
get_stats(res)
```

```
#>   k 1-PAC mean_silhouette concordance area_increased  Rand Jaccard
#> 2 2 1.000           0.991       0.995         0.4712 0.531   0.531
#> 3 3 0.953           0.930       0.966         0.4388 0.791   0.607
#> 4 4 0.781           0.833       0.890         0.1170 0.866   0.618
#> 5 5 0.846           0.788       0.905         0.0578 0.946   0.783
#> 6 6 0.795           0.713       0.830         0.0406 0.978   0.887
```

`suggest_best_k()` suggests the best $k$ based on these statistics. The rules are as follows:

- All $k$ with Jaccard index larger than 0.95 are removed because increasing
  $k$ does not provide enough extra information. If all $k$ are removed, it is
  marked as no subgroup is detected.
- For all $k$ with 1-PAC score larger than 0.9, the maximal $k$ is taken as
  the best $k$, and other $k$ are marked as optional $k$.
- If it does not fit the second rule. The $k$ with the maximal vote of the
  highest 1-PAC score, highest mean silhouette, and highest concordance is
  taken as the best $k$.

```r
suggest_best_k(res)
```

```
#> [1] 3
#> attr(,"optional")
#> [1] 2
```

There is also optional best $k$ = 2 that is worth to check.

Following shows the table of the partitions (You need to click the **show/hide
code output** link to see it). The membership matrix (columns with name `p*`)
is inferred by
[`clue::cl_consensus()`](https://www.rdocumentation.org/link/cl_consensus?package=clue)
function with the `SE` method. Basically the value in the membership matrix
represents the probability to belong to a certain group. The finall class
label for an item is determined with the group with highest probability it
belongs to.

In `get_classes()` function, the entropy is calculated from the membership
matrix and the silhouette score is calculated from the consensus matrix.



<script>
$( function() {
	$( '#tabs-SD-skmeans-get-classes' ).tabs();
} );
</script>
<div id='tabs-SD-skmeans-get-classes'>
<ul>
<li><a href='#tab-SD-skmeans-get-classes-1'>k = 2</a></li>
<li><a href='#tab-SD-skmeans-get-classes-2'>k = 3</a></li>
<li><a href='#tab-SD-skmeans-get-classes-3'>k = 4</a></li>
<li><a href='#tab-SD-skmeans-get-classes-4'>k = 5</a></li>
<li><a href='#tab-SD-skmeans-get-classes-5'>k = 6</a></li>
</ul>

<div id='tab-SD-skmeans-get-classes-1'>
<p><a id='tab-SD-skmeans-get-classes-1-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 2), get_membership(res, k = 2))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2
#&gt; SRR1383358     2  0.0000      0.992 0.000 1.000
#&gt; SRR1383360     1  0.0376      0.996 0.996 0.004
#&gt; SRR1383359     2  0.0000      0.992 0.000 1.000
#&gt; SRR1383362     1  0.0000      1.000 1.000 0.000
#&gt; SRR1383361     2  0.0000      0.992 0.000 1.000
#&gt; SRR1383363     2  0.0000      0.992 0.000 1.000
#&gt; SRR1383364     2  0.0000      0.992 0.000 1.000
#&gt; SRR1383365     2  0.0000      0.992 0.000 1.000
#&gt; SRR1383366     2  0.0000      0.992 0.000 1.000
#&gt; SRR1383367     2  0.0000      0.992 0.000 1.000
#&gt; SRR1383368     1  0.0376      0.996 0.996 0.004
#&gt; SRR1383369     2  0.0000      0.992 0.000 1.000
#&gt; SRR1383370     2  0.0000      0.992 0.000 1.000
#&gt; SRR1383371     2  0.0000      0.992 0.000 1.000
#&gt; SRR1383372     2  0.0000      0.992 0.000 1.000
#&gt; SRR1383373     2  0.0000      0.992 0.000 1.000
#&gt; SRR1383374     2  0.0000      0.992 0.000 1.000
#&gt; SRR1383375     1  0.0000      1.000 1.000 0.000
#&gt; SRR1383376     2  0.0376      0.991 0.004 0.996
#&gt; SRR1383377     2  0.2948      0.950 0.052 0.948
#&gt; SRR1383378     1  0.0000      1.000 1.000 0.000
#&gt; SRR1383379     1  0.0000      1.000 1.000 0.000
#&gt; SRR1383380     1  0.0000      1.000 1.000 0.000
#&gt; SRR1383381     2  0.0000      0.992 0.000 1.000
#&gt; SRR1383382     1  0.0000      1.000 1.000 0.000
#&gt; SRR1383383     2  0.0000      0.992 0.000 1.000
#&gt; SRR1383385     1  0.0000      1.000 1.000 0.000
#&gt; SRR1383384     2  0.0376      0.991 0.004 0.996
#&gt; SRR1383386     1  0.0000      1.000 1.000 0.000
#&gt; SRR1383387     2  0.3274      0.944 0.060 0.940
#&gt; SRR1383389     2  0.0000      0.992 0.000 1.000
#&gt; SRR1383391     2  0.0376      0.991 0.004 0.996
#&gt; SRR1383388     1  0.0000      1.000 1.000 0.000
#&gt; SRR1383392     2  0.0000      0.992 0.000 1.000
#&gt; SRR1383390     2  0.0376      0.991 0.004 0.996
#&gt; SRR1383394     2  0.0376      0.991 0.004 0.996
#&gt; SRR1383393     1  0.0000      1.000 1.000 0.000
#&gt; SRR1383396     1  0.0000      1.000 1.000 0.000
#&gt; SRR1383395     2  0.2948      0.950 0.052 0.948
#&gt; SRR1383399     2  0.0000      0.992 0.000 1.000
#&gt; SRR1383400     1  0.0000      1.000 1.000 0.000
#&gt; SRR1383397     1  0.0000      1.000 1.000 0.000
#&gt; SRR1383401     2  0.0000      0.992 0.000 1.000
#&gt; SRR1383398     1  0.0000      1.000 1.000 0.000
#&gt; SRR1383402     2  0.0376      0.991 0.004 0.996
#&gt; SRR1383404     1  0.0000      1.000 1.000 0.000
#&gt; SRR1383403     1  0.0000      1.000 1.000 0.000
#&gt; SRR1383405     2  0.3274      0.944 0.060 0.940
#&gt; SRR1383406     1  0.0000      1.000 1.000 0.000
#&gt; SRR1383407     2  0.0000      0.992 0.000 1.000
#&gt; SRR1383408     2  0.0376      0.991 0.004 0.996
#&gt; SRR1383409     2  0.0376      0.991 0.004 0.996
#&gt; SRR1383410     2  0.0000      0.992 0.000 1.000
</code></pre>

<script>
$('#tab-SD-skmeans-get-classes-1-a').parent().next().next().hide();
$('#tab-SD-skmeans-get-classes-1-a').click(function(){
  $('#tab-SD-skmeans-get-classes-1-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-SD-skmeans-get-classes-2'>
<p><a id='tab-SD-skmeans-get-classes-2-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 3), get_membership(res, k = 3))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3
#&gt; SRR1383358     3  0.0000      0.994 0.000 0.000 1.000
#&gt; SRR1383360     1  0.5835      0.512 0.660 0.000 0.340
#&gt; SRR1383359     3  0.0000      0.994 0.000 0.000 1.000
#&gt; SRR1383362     1  0.0000      0.918 1.000 0.000 0.000
#&gt; SRR1383361     3  0.0000      0.994 0.000 0.000 1.000
#&gt; SRR1383363     3  0.0000      0.994 0.000 0.000 1.000
#&gt; SRR1383364     3  0.0000      0.994 0.000 0.000 1.000
#&gt; SRR1383365     3  0.0000      0.994 0.000 0.000 1.000
#&gt; SRR1383366     3  0.0892      0.976 0.000 0.020 0.980
#&gt; SRR1383367     3  0.0000      0.994 0.000 0.000 1.000
#&gt; SRR1383368     1  0.5621      0.570 0.692 0.000 0.308
#&gt; SRR1383369     3  0.0000      0.994 0.000 0.000 1.000
#&gt; SRR1383370     3  0.0000      0.994 0.000 0.000 1.000
#&gt; SRR1383371     3  0.0000      0.994 0.000 0.000 1.000
#&gt; SRR1383372     3  0.0000      0.994 0.000 0.000 1.000
#&gt; SRR1383373     3  0.0000      0.994 0.000 0.000 1.000
#&gt; SRR1383374     3  0.0000      0.994 0.000 0.000 1.000
#&gt; SRR1383375     1  0.0000      0.918 1.000 0.000 0.000
#&gt; SRR1383376     2  0.0000      0.981 0.000 1.000 0.000
#&gt; SRR1383377     2  0.0237      0.980 0.000 0.996 0.004
#&gt; SRR1383378     1  0.5397      0.598 0.720 0.280 0.000
#&gt; SRR1383379     1  0.2878      0.867 0.904 0.096 0.000
#&gt; SRR1383380     1  0.1031      0.910 0.976 0.024 0.000
#&gt; SRR1383381     3  0.1399      0.968 0.004 0.028 0.968
#&gt; SRR1383382     1  0.0000      0.918 1.000 0.000 0.000
#&gt; SRR1383383     2  0.0892      0.976 0.000 0.980 0.020
#&gt; SRR1383385     1  0.0000      0.918 1.000 0.000 0.000
#&gt; SRR1383384     2  0.0000      0.981 0.000 1.000 0.000
#&gt; SRR1383386     1  0.0000      0.918 1.000 0.000 0.000
#&gt; SRR1383387     2  0.0000      0.981 0.000 1.000 0.000
#&gt; SRR1383389     2  0.2945      0.912 0.004 0.908 0.088
#&gt; SRR1383391     2  0.0592      0.979 0.000 0.988 0.012
#&gt; SRR1383388     1  0.0000      0.918 1.000 0.000 0.000
#&gt; SRR1383392     2  0.0000      0.981 0.000 1.000 0.000
#&gt; SRR1383390     2  0.0892      0.976 0.000 0.980 0.020
#&gt; SRR1383394     2  0.0000      0.981 0.000 1.000 0.000
#&gt; SRR1383393     1  0.0000      0.918 1.000 0.000 0.000
#&gt; SRR1383396     1  0.0000      0.918 1.000 0.000 0.000
#&gt; SRR1383395     2  0.0237      0.980 0.000 0.996 0.004
#&gt; SRR1383399     3  0.1399      0.968 0.004 0.028 0.968
#&gt; SRR1383400     1  0.0000      0.918 1.000 0.000 0.000
#&gt; SRR1383397     1  0.5291      0.662 0.732 0.268 0.000
#&gt; SRR1383401     2  0.0892      0.976 0.000 0.980 0.020
#&gt; SRR1383398     1  0.1031      0.910 0.976 0.024 0.000
#&gt; SRR1383402     2  0.0000      0.981 0.000 1.000 0.000
#&gt; SRR1383404     1  0.0000      0.918 1.000 0.000 0.000
#&gt; SRR1383403     1  0.0000      0.918 1.000 0.000 0.000
#&gt; SRR1383405     2  0.0000      0.981 0.000 1.000 0.000
#&gt; SRR1383406     1  0.3038      0.861 0.896 0.104 0.000
#&gt; SRR1383407     2  0.2878      0.907 0.000 0.904 0.096
#&gt; SRR1383408     2  0.0892      0.976 0.000 0.980 0.020
#&gt; SRR1383409     2  0.0592      0.979 0.000 0.988 0.012
#&gt; SRR1383410     2  0.0000      0.981 0.000 1.000 0.000
</code></pre>

<script>
$('#tab-SD-skmeans-get-classes-2-a').parent().next().next().hide();
$('#tab-SD-skmeans-get-classes-2-a').click(function(){
  $('#tab-SD-skmeans-get-classes-2-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-SD-skmeans-get-classes-3'>
<p><a id='tab-SD-skmeans-get-classes-3-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 4), get_membership(res, k = 4))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4
#&gt; SRR1383358     3  0.0000      0.925 0.000 0.000 1.000 0.000
#&gt; SRR1383360     1  0.3975      0.703 0.760 0.000 0.240 0.000
#&gt; SRR1383359     3  0.0000      0.925 0.000 0.000 1.000 0.000
#&gt; SRR1383362     1  0.0000      0.948 1.000 0.000 0.000 0.000
#&gt; SRR1383361     3  0.0000      0.925 0.000 0.000 1.000 0.000
#&gt; SRR1383363     3  0.0000      0.925 0.000 0.000 1.000 0.000
#&gt; SRR1383364     3  0.2469      0.862 0.000 0.000 0.892 0.108
#&gt; SRR1383365     3  0.0000      0.925 0.000 0.000 1.000 0.000
#&gt; SRR1383366     3  0.0592      0.915 0.000 0.000 0.984 0.016
#&gt; SRR1383367     3  0.0000      0.925 0.000 0.000 1.000 0.000
#&gt; SRR1383368     1  0.3172      0.796 0.840 0.000 0.160 0.000
#&gt; SRR1383369     3  0.0817      0.914 0.000 0.000 0.976 0.024
#&gt; SRR1383370     3  0.0000      0.925 0.000 0.000 1.000 0.000
#&gt; SRR1383371     3  0.2469      0.862 0.000 0.000 0.892 0.108
#&gt; SRR1383372     3  0.0000      0.925 0.000 0.000 1.000 0.000
#&gt; SRR1383373     3  0.0000      0.925 0.000 0.000 1.000 0.000
#&gt; SRR1383374     3  0.0000      0.925 0.000 0.000 1.000 0.000
#&gt; SRR1383375     1  0.0000      0.948 1.000 0.000 0.000 0.000
#&gt; SRR1383376     2  0.4250      0.694 0.000 0.724 0.000 0.276
#&gt; SRR1383377     4  0.0469      0.816 0.000 0.012 0.000 0.988
#&gt; SRR1383378     2  0.3356      0.709 0.176 0.824 0.000 0.000
#&gt; SRR1383379     4  0.3015      0.852 0.024 0.092 0.000 0.884
#&gt; SRR1383380     4  0.3219      0.799 0.164 0.000 0.000 0.836
#&gt; SRR1383381     3  0.6949      0.440 0.004 0.336 0.548 0.112
#&gt; SRR1383382     1  0.0000      0.948 1.000 0.000 0.000 0.000
#&gt; SRR1383383     2  0.0592      0.844 0.000 0.984 0.000 0.016
#&gt; SRR1383385     1  0.0000      0.948 1.000 0.000 0.000 0.000
#&gt; SRR1383384     2  0.2216      0.842 0.000 0.908 0.000 0.092
#&gt; SRR1383386     1  0.0000      0.948 1.000 0.000 0.000 0.000
#&gt; SRR1383387     4  0.2530      0.838 0.000 0.112 0.000 0.888
#&gt; SRR1383389     2  0.2469      0.789 0.000 0.892 0.000 0.108
#&gt; SRR1383391     2  0.1716      0.850 0.000 0.936 0.000 0.064
#&gt; SRR1383388     4  0.4985      0.216 0.468 0.000 0.000 0.532
#&gt; SRR1383392     2  0.4193      0.696 0.000 0.732 0.000 0.268
#&gt; SRR1383390     2  0.0000      0.848 0.000 1.000 0.000 0.000
#&gt; SRR1383394     2  0.4250      0.694 0.000 0.724 0.000 0.276
#&gt; SRR1383393     1  0.0000      0.948 1.000 0.000 0.000 0.000
#&gt; SRR1383396     1  0.1474      0.903 0.948 0.052 0.000 0.000
#&gt; SRR1383395     4  0.0469      0.816 0.000 0.012 0.000 0.988
#&gt; SRR1383399     3  0.6949      0.440 0.004 0.336 0.548 0.112
#&gt; SRR1383400     1  0.0000      0.948 1.000 0.000 0.000 0.000
#&gt; SRR1383397     4  0.2805      0.847 0.012 0.100 0.000 0.888
#&gt; SRR1383401     2  0.0592      0.844 0.000 0.984 0.000 0.016
#&gt; SRR1383398     4  0.3219      0.799 0.164 0.000 0.000 0.836
#&gt; SRR1383402     2  0.2216      0.842 0.000 0.908 0.000 0.092
#&gt; SRR1383404     1  0.0000      0.948 1.000 0.000 0.000 0.000
#&gt; SRR1383403     1  0.0000      0.948 1.000 0.000 0.000 0.000
#&gt; SRR1383405     4  0.2530      0.838 0.000 0.112 0.000 0.888
#&gt; SRR1383406     4  0.3015      0.852 0.024 0.092 0.000 0.884
#&gt; SRR1383407     2  0.2469      0.789 0.000 0.892 0.000 0.108
#&gt; SRR1383408     2  0.0000      0.848 0.000 1.000 0.000 0.000
#&gt; SRR1383409     2  0.1716      0.850 0.000 0.936 0.000 0.064
#&gt; SRR1383410     2  0.4193      0.696 0.000 0.732 0.000 0.268
</code></pre>

<script>
$('#tab-SD-skmeans-get-classes-3-a').parent().next().next().hide();
$('#tab-SD-skmeans-get-classes-3-a').click(function(){
  $('#tab-SD-skmeans-get-classes-3-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-SD-skmeans-get-classes-4'>
<p><a id='tab-SD-skmeans-get-classes-4-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 5), get_membership(res, k = 5))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4    p5
#&gt; SRR1383358     3  0.0510     0.9788 0.000 0.000 0.984 0.000 0.016
#&gt; SRR1383360     1  0.4437     0.1607 0.532 0.000 0.464 0.000 0.004
#&gt; SRR1383359     3  0.1478     0.9255 0.000 0.000 0.936 0.000 0.064
#&gt; SRR1383362     1  0.0000     0.9046 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1383361     3  0.0000     0.9857 0.000 0.000 1.000 0.000 0.000
#&gt; SRR1383363     3  0.0162     0.9855 0.000 0.000 0.996 0.000 0.004
#&gt; SRR1383364     5  0.2773     0.6812 0.000 0.000 0.164 0.000 0.836
#&gt; SRR1383365     3  0.0510     0.9788 0.000 0.000 0.984 0.000 0.016
#&gt; SRR1383366     3  0.0486     0.9755 0.000 0.004 0.988 0.004 0.004
#&gt; SRR1383367     3  0.0000     0.9857 0.000 0.000 1.000 0.000 0.000
#&gt; SRR1383368     1  0.2732     0.7584 0.840 0.000 0.160 0.000 0.000
#&gt; SRR1383369     5  0.4291     0.1140 0.000 0.000 0.464 0.000 0.536
#&gt; SRR1383370     3  0.0000     0.9857 0.000 0.000 1.000 0.000 0.000
#&gt; SRR1383371     5  0.2891     0.6727 0.000 0.000 0.176 0.000 0.824
#&gt; SRR1383372     3  0.0000     0.9857 0.000 0.000 1.000 0.000 0.000
#&gt; SRR1383373     3  0.0162     0.9855 0.000 0.000 0.996 0.000 0.004
#&gt; SRR1383374     3  0.0162     0.9842 0.000 0.004 0.996 0.000 0.000
#&gt; SRR1383375     1  0.0324     0.9045 0.992 0.000 0.000 0.004 0.004
#&gt; SRR1383376     2  0.1041     0.8531 0.000 0.964 0.000 0.032 0.004
#&gt; SRR1383377     4  0.2629     0.8140 0.000 0.004 0.000 0.860 0.136
#&gt; SRR1383378     2  0.6830     0.0928 0.360 0.396 0.000 0.004 0.240
#&gt; SRR1383379     4  0.0865     0.8852 0.004 0.024 0.000 0.972 0.000
#&gt; SRR1383380     4  0.1195     0.8792 0.028 0.000 0.000 0.960 0.012
#&gt; SRR1383381     5  0.0854     0.6768 0.004 0.008 0.012 0.000 0.976
#&gt; SRR1383382     1  0.0000     0.9046 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1383383     2  0.2179     0.8278 0.000 0.896 0.000 0.004 0.100
#&gt; SRR1383385     1  0.0451     0.9035 0.988 0.000 0.000 0.008 0.004
#&gt; SRR1383384     2  0.0000     0.8644 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1383386     1  0.0162     0.9042 0.996 0.000 0.000 0.004 0.000
#&gt; SRR1383387     4  0.2583     0.8324 0.000 0.132 0.000 0.864 0.004
#&gt; SRR1383389     2  0.4744     0.1440 0.000 0.508 0.000 0.016 0.476
#&gt; SRR1383391     2  0.0404     0.8651 0.000 0.988 0.000 0.000 0.012
#&gt; SRR1383388     4  0.4081     0.5682 0.296 0.004 0.000 0.696 0.004
#&gt; SRR1383392     2  0.1597     0.8505 0.000 0.940 0.000 0.048 0.012
#&gt; SRR1383390     2  0.1270     0.8549 0.000 0.948 0.000 0.000 0.052
#&gt; SRR1383394     2  0.1041     0.8531 0.000 0.964 0.000 0.032 0.004
#&gt; SRR1383393     1  0.0324     0.9045 0.992 0.000 0.000 0.004 0.004
#&gt; SRR1383396     1  0.3242     0.6850 0.784 0.000 0.000 0.000 0.216
#&gt; SRR1383395     4  0.2583     0.8175 0.000 0.004 0.000 0.864 0.132
#&gt; SRR1383399     5  0.0854     0.6768 0.004 0.008 0.012 0.000 0.976
#&gt; SRR1383400     1  0.0000     0.9046 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1383397     4  0.0703     0.8844 0.000 0.024 0.000 0.976 0.000
#&gt; SRR1383401     2  0.2286     0.8227 0.000 0.888 0.000 0.004 0.108
#&gt; SRR1383398     4  0.1195     0.8792 0.028 0.000 0.000 0.960 0.012
#&gt; SRR1383402     2  0.0162     0.8640 0.000 0.996 0.000 0.004 0.000
#&gt; SRR1383404     1  0.0290     0.9029 0.992 0.000 0.000 0.008 0.000
#&gt; SRR1383403     1  0.0451     0.9035 0.988 0.000 0.000 0.008 0.004
#&gt; SRR1383405     4  0.2583     0.8324 0.000 0.132 0.000 0.864 0.004
#&gt; SRR1383406     4  0.1026     0.8851 0.004 0.024 0.000 0.968 0.004
#&gt; SRR1383407     5  0.4830    -0.2935 0.000 0.488 0.000 0.020 0.492
#&gt; SRR1383408     2  0.1043     0.8588 0.000 0.960 0.000 0.000 0.040
#&gt; SRR1383409     2  0.0404     0.8651 0.000 0.988 0.000 0.000 0.012
#&gt; SRR1383410     2  0.1597     0.8505 0.000 0.940 0.000 0.048 0.012
</code></pre>

<script>
$('#tab-SD-skmeans-get-classes-4-a').parent().next().next().hide();
$('#tab-SD-skmeans-get-classes-4-a').click(function(){
  $('#tab-SD-skmeans-get-classes-4-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-SD-skmeans-get-classes-5'>
<p><a id='tab-SD-skmeans-get-classes-5-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 6), get_membership(res, k = 6))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4    p5    p6
#&gt; SRR1383358     3  0.1349      0.924 0.000 0.000 0.940 0.000 0.056 0.004
#&gt; SRR1383360     1  0.5159      0.115 0.476 0.000 0.456 0.004 0.004 0.060
#&gt; SRR1383359     3  0.2631      0.816 0.000 0.000 0.840 0.000 0.152 0.008
#&gt; SRR1383362     1  0.0000      0.813 1.000 0.000 0.000 0.000 0.000 0.000
#&gt; SRR1383361     3  0.0146      0.953 0.000 0.000 0.996 0.000 0.000 0.004
#&gt; SRR1383363     3  0.1092      0.942 0.000 0.000 0.960 0.000 0.020 0.020
#&gt; SRR1383364     5  0.1327      0.866 0.000 0.000 0.064 0.000 0.936 0.000
#&gt; SRR1383365     3  0.1866      0.897 0.000 0.000 0.908 0.000 0.084 0.008
#&gt; SRR1383366     3  0.0520      0.953 0.000 0.000 0.984 0.000 0.008 0.008
#&gt; SRR1383367     3  0.0692      0.948 0.000 0.000 0.976 0.000 0.004 0.020
#&gt; SRR1383368     1  0.4286      0.601 0.712 0.000 0.224 0.000 0.004 0.060
#&gt; SRR1383369     5  0.3215      0.690 0.000 0.000 0.240 0.000 0.756 0.004
#&gt; SRR1383370     3  0.0692      0.948 0.000 0.000 0.976 0.000 0.004 0.020
#&gt; SRR1383371     5  0.1757      0.861 0.000 0.000 0.076 0.000 0.916 0.008
#&gt; SRR1383372     3  0.0291      0.954 0.000 0.000 0.992 0.000 0.004 0.004
#&gt; SRR1383373     3  0.0291      0.954 0.000 0.000 0.992 0.000 0.004 0.004
#&gt; SRR1383374     3  0.0291      0.953 0.000 0.004 0.992 0.000 0.000 0.004
#&gt; SRR1383375     1  0.2331      0.803 0.888 0.000 0.000 0.032 0.000 0.080
#&gt; SRR1383376     2  0.3500      0.610 0.000 0.768 0.000 0.028 0.000 0.204
#&gt; SRR1383377     4  0.4520      0.557 0.000 0.000 0.000 0.520 0.032 0.448
#&gt; SRR1383378     6  0.6902      0.471 0.160 0.372 0.000 0.000 0.084 0.384
#&gt; SRR1383379     4  0.0935      0.768 0.000 0.004 0.000 0.964 0.000 0.032
#&gt; SRR1383380     4  0.2048      0.750 0.000 0.000 0.000 0.880 0.000 0.120
#&gt; SRR1383381     5  0.0405      0.837 0.000 0.004 0.000 0.000 0.988 0.008
#&gt; SRR1383382     1  0.0000      0.813 1.000 0.000 0.000 0.000 0.000 0.000
#&gt; SRR1383383     2  0.3618      0.432 0.000 0.768 0.000 0.000 0.040 0.192
#&gt; SRR1383385     1  0.2436      0.800 0.880 0.000 0.000 0.032 0.000 0.088
#&gt; SRR1383384     2  0.1387      0.667 0.000 0.932 0.000 0.000 0.000 0.068
#&gt; SRR1383386     1  0.1682      0.795 0.928 0.000 0.000 0.020 0.000 0.052
#&gt; SRR1383387     4  0.4804      0.636 0.000 0.112 0.000 0.656 0.000 0.232
#&gt; SRR1383389     6  0.5680      0.722 0.000 0.292 0.000 0.000 0.192 0.516
#&gt; SRR1383391     2  0.1245      0.649 0.000 0.952 0.000 0.016 0.000 0.032
#&gt; SRR1383388     4  0.3534      0.633 0.124 0.000 0.000 0.800 0.000 0.076
#&gt; SRR1383392     2  0.3881      0.435 0.000 0.600 0.000 0.004 0.000 0.396
#&gt; SRR1383390     2  0.3171      0.433 0.000 0.784 0.000 0.000 0.012 0.204
#&gt; SRR1383394     2  0.3500      0.610 0.000 0.768 0.000 0.028 0.000 0.204
#&gt; SRR1383393     1  0.2384      0.802 0.884 0.000 0.000 0.032 0.000 0.084
#&gt; SRR1383396     1  0.5452      0.285 0.560 0.008 0.000 0.008 0.084 0.340
#&gt; SRR1383395     4  0.4520      0.557 0.000 0.000 0.000 0.520 0.032 0.448
#&gt; SRR1383399     5  0.0405      0.837 0.000 0.004 0.000 0.000 0.988 0.008
#&gt; SRR1383400     1  0.0000      0.813 1.000 0.000 0.000 0.000 0.000 0.000
#&gt; SRR1383397     4  0.1010      0.767 0.000 0.004 0.000 0.960 0.000 0.036
#&gt; SRR1383401     2  0.3916      0.430 0.000 0.752 0.000 0.000 0.064 0.184
#&gt; SRR1383398     4  0.2048      0.750 0.000 0.000 0.000 0.880 0.000 0.120
#&gt; SRR1383402     2  0.1444      0.667 0.000 0.928 0.000 0.000 0.000 0.072
#&gt; SRR1383404     1  0.1921      0.791 0.916 0.000 0.000 0.032 0.000 0.052
#&gt; SRR1383403     1  0.2436      0.800 0.880 0.000 0.000 0.032 0.000 0.088
#&gt; SRR1383405     4  0.4804      0.636 0.000 0.112 0.000 0.656 0.000 0.232
#&gt; SRR1383406     4  0.0000      0.764 0.000 0.000 0.000 1.000 0.000 0.000
#&gt; SRR1383407     6  0.5646      0.716 0.000 0.264 0.000 0.000 0.204 0.532
#&gt; SRR1383408     2  0.2912      0.485 0.000 0.816 0.000 0.000 0.012 0.172
#&gt; SRR1383409     2  0.1245      0.649 0.000 0.952 0.000 0.016 0.000 0.032
#&gt; SRR1383410     2  0.3881      0.435 0.000 0.600 0.000 0.004 0.000 0.396
</code></pre>

<script>
$('#tab-SD-skmeans-get-classes-5-a').parent().next().next().hide();
$('#tab-SD-skmeans-get-classes-5-a').click(function(){
  $('#tab-SD-skmeans-get-classes-5-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>
</div>

Heatmaps for the consensus matrix. It visualizes the probability of two
samples to be in a same group.



<script>
$( function() {
	$( '#tabs-SD-skmeans-consensus-heatmap' ).tabs();
} );
</script>
<div id='tabs-SD-skmeans-consensus-heatmap'>
<ul>
<li><a href='#tab-SD-skmeans-consensus-heatmap-1'>k = 2</a></li>
<li><a href='#tab-SD-skmeans-consensus-heatmap-2'>k = 3</a></li>
<li><a href='#tab-SD-skmeans-consensus-heatmap-3'>k = 4</a></li>
<li><a href='#tab-SD-skmeans-consensus-heatmap-4'>k = 5</a></li>
<li><a href='#tab-SD-skmeans-consensus-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-SD-skmeans-consensus-heatmap-1'>
<pre><code class="r">consensus_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-SD-skmeans-consensus-heatmap-1-1.png" alt="plot of chunk tab-SD-skmeans-consensus-heatmap-1"/></p>

</div>
<div id='tab-SD-skmeans-consensus-heatmap-2'>
<pre><code class="r">consensus_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-SD-skmeans-consensus-heatmap-2-1.png" alt="plot of chunk tab-SD-skmeans-consensus-heatmap-2"/></p>

</div>
<div id='tab-SD-skmeans-consensus-heatmap-3'>
<pre><code class="r">consensus_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-SD-skmeans-consensus-heatmap-3-1.png" alt="plot of chunk tab-SD-skmeans-consensus-heatmap-3"/></p>

</div>
<div id='tab-SD-skmeans-consensus-heatmap-4'>
<pre><code class="r">consensus_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-SD-skmeans-consensus-heatmap-4-1.png" alt="plot of chunk tab-SD-skmeans-consensus-heatmap-4"/></p>

</div>
<div id='tab-SD-skmeans-consensus-heatmap-5'>
<pre><code class="r">consensus_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-SD-skmeans-consensus-heatmap-5-1.png" alt="plot of chunk tab-SD-skmeans-consensus-heatmap-5"/></p>

</div>
</div>

Heatmaps for the membership of samples in all partitions to see how consistent they are:




<script>
$( function() {
	$( '#tabs-SD-skmeans-membership-heatmap' ).tabs();
} );
</script>
<div id='tabs-SD-skmeans-membership-heatmap'>
<ul>
<li><a href='#tab-SD-skmeans-membership-heatmap-1'>k = 2</a></li>
<li><a href='#tab-SD-skmeans-membership-heatmap-2'>k = 3</a></li>
<li><a href='#tab-SD-skmeans-membership-heatmap-3'>k = 4</a></li>
<li><a href='#tab-SD-skmeans-membership-heatmap-4'>k = 5</a></li>
<li><a href='#tab-SD-skmeans-membership-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-SD-skmeans-membership-heatmap-1'>
<pre><code class="r">membership_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-SD-skmeans-membership-heatmap-1-1.png" alt="plot of chunk tab-SD-skmeans-membership-heatmap-1"/></p>

</div>
<div id='tab-SD-skmeans-membership-heatmap-2'>
<pre><code class="r">membership_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-SD-skmeans-membership-heatmap-2-1.png" alt="plot of chunk tab-SD-skmeans-membership-heatmap-2"/></p>

</div>
<div id='tab-SD-skmeans-membership-heatmap-3'>
<pre><code class="r">membership_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-SD-skmeans-membership-heatmap-3-1.png" alt="plot of chunk tab-SD-skmeans-membership-heatmap-3"/></p>

</div>
<div id='tab-SD-skmeans-membership-heatmap-4'>
<pre><code class="r">membership_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-SD-skmeans-membership-heatmap-4-1.png" alt="plot of chunk tab-SD-skmeans-membership-heatmap-4"/></p>

</div>
<div id='tab-SD-skmeans-membership-heatmap-5'>
<pre><code class="r">membership_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-SD-skmeans-membership-heatmap-5-1.png" alt="plot of chunk tab-SD-skmeans-membership-heatmap-5"/></p>

</div>
</div>

As soon as we have had the classes for columns, we can look for signatures
which are significantly different between classes which can be candidate marks
for certain classes. Following are the heatmaps for signatures.



Signature heatmaps where rows are scaled:



<script>
$( function() {
	$( '#tabs-SD-skmeans-get-signatures' ).tabs();
} );
</script>
<div id='tabs-SD-skmeans-get-signatures'>
<ul>
<li><a href='#tab-SD-skmeans-get-signatures-1'>k = 2</a></li>
<li><a href='#tab-SD-skmeans-get-signatures-2'>k = 3</a></li>
<li><a href='#tab-SD-skmeans-get-signatures-3'>k = 4</a></li>
<li><a href='#tab-SD-skmeans-get-signatures-4'>k = 5</a></li>
<li><a href='#tab-SD-skmeans-get-signatures-5'>k = 6</a></li>
</ul>
<div id='tab-SD-skmeans-get-signatures-1'>
<pre><code class="r">get_signatures(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-SD-skmeans-get-signatures-1-1.png" alt="plot of chunk tab-SD-skmeans-get-signatures-1"/></p>

</div>
<div id='tab-SD-skmeans-get-signatures-2'>
<pre><code class="r">get_signatures(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-SD-skmeans-get-signatures-2-1.png" alt="plot of chunk tab-SD-skmeans-get-signatures-2"/></p>

</div>
<div id='tab-SD-skmeans-get-signatures-3'>
<pre><code class="r">get_signatures(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-SD-skmeans-get-signatures-3-1.png" alt="plot of chunk tab-SD-skmeans-get-signatures-3"/></p>

</div>
<div id='tab-SD-skmeans-get-signatures-4'>
<pre><code class="r">get_signatures(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-SD-skmeans-get-signatures-4-1.png" alt="plot of chunk tab-SD-skmeans-get-signatures-4"/></p>

</div>
<div id='tab-SD-skmeans-get-signatures-5'>
<pre><code class="r">get_signatures(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-SD-skmeans-get-signatures-5-1.png" alt="plot of chunk tab-SD-skmeans-get-signatures-5"/></p>

</div>
</div>



Signature heatmaps where rows are not scaled:


<script>
$( function() {
	$( '#tabs-SD-skmeans-get-signatures-no-scale' ).tabs();
} );
</script>
<div id='tabs-SD-skmeans-get-signatures-no-scale'>
<ul>
<li><a href='#tab-SD-skmeans-get-signatures-no-scale-1'>k = 2</a></li>
<li><a href='#tab-SD-skmeans-get-signatures-no-scale-2'>k = 3</a></li>
<li><a href='#tab-SD-skmeans-get-signatures-no-scale-3'>k = 4</a></li>
<li><a href='#tab-SD-skmeans-get-signatures-no-scale-4'>k = 5</a></li>
<li><a href='#tab-SD-skmeans-get-signatures-no-scale-5'>k = 6</a></li>
</ul>
<div id='tab-SD-skmeans-get-signatures-no-scale-1'>
<pre><code class="r">get_signatures(res, k = 2, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-SD-skmeans-get-signatures-no-scale-1-1.png" alt="plot of chunk tab-SD-skmeans-get-signatures-no-scale-1"/></p>

</div>
<div id='tab-SD-skmeans-get-signatures-no-scale-2'>
<pre><code class="r">get_signatures(res, k = 3, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-SD-skmeans-get-signatures-no-scale-2-1.png" alt="plot of chunk tab-SD-skmeans-get-signatures-no-scale-2"/></p>

</div>
<div id='tab-SD-skmeans-get-signatures-no-scale-3'>
<pre><code class="r">get_signatures(res, k = 4, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-SD-skmeans-get-signatures-no-scale-3-1.png" alt="plot of chunk tab-SD-skmeans-get-signatures-no-scale-3"/></p>

</div>
<div id='tab-SD-skmeans-get-signatures-no-scale-4'>
<pre><code class="r">get_signatures(res, k = 5, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-SD-skmeans-get-signatures-no-scale-4-1.png" alt="plot of chunk tab-SD-skmeans-get-signatures-no-scale-4"/></p>

</div>
<div id='tab-SD-skmeans-get-signatures-no-scale-5'>
<pre><code class="r">get_signatures(res, k = 6, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-SD-skmeans-get-signatures-no-scale-5-1.png" alt="plot of chunk tab-SD-skmeans-get-signatures-no-scale-5"/></p>

</div>
</div>



Compare the overlap of signatures from different k:

```r
compare_signatures(res)
```

![plot of chunk SD-skmeans-signature_compare](figure_cola/SD-skmeans-signature_compare-1.png)

`get_signature()` returns a data frame invisibly. TO get the list of signatures, the function
call should be assigned to a variable explicitly. In following code, if `plot` argument is set
to `FALSE`, no heatmap is plotted while only the differential analysis is performed.

```r
# code only for demonstration
tb = get_signature(res, k = ..., plot = FALSE)
```

An example of the output of `tb` is:

```
#>   which_row         fdr    mean_1    mean_2 scaled_mean_1 scaled_mean_2 km
#> 1        38 0.042760348  8.373488  9.131774    -0.5533452     0.5164555  1
#> 2        40 0.018707592  7.106213  8.469186    -0.6173731     0.5762149  1
#> 3        55 0.019134737 10.221463 11.207825    -0.6159697     0.5749050  1
#> 4        59 0.006059896  5.921854  7.869574    -0.6899429     0.6439467  1
#> 5        60 0.018055526  8.928898 10.211722    -0.6204761     0.5791110  1
#> 6        98 0.009384629 15.714769 14.887706     0.6635654    -0.6193277  2
...
```

The columns in `tb` are:

1. `which_row`: row indices corresponding to the input matrix.
2. `fdr`: FDR for the differential test. 
3. `mean_x`: The mean value in group x.
4. `scaled_mean_x`: The mean value in group x after rows are scaled.
5. `km`: Row groups if k-means clustering is applied to rows.



UMAP plot which shows how samples are separated.


<script>
$( function() {
	$( '#tabs-SD-skmeans-dimension-reduction' ).tabs();
} );
</script>
<div id='tabs-SD-skmeans-dimension-reduction'>
<ul>
<li><a href='#tab-SD-skmeans-dimension-reduction-1'>k = 2</a></li>
<li><a href='#tab-SD-skmeans-dimension-reduction-2'>k = 3</a></li>
<li><a href='#tab-SD-skmeans-dimension-reduction-3'>k = 4</a></li>
<li><a href='#tab-SD-skmeans-dimension-reduction-4'>k = 5</a></li>
<li><a href='#tab-SD-skmeans-dimension-reduction-5'>k = 6</a></li>
</ul>
<div id='tab-SD-skmeans-dimension-reduction-1'>
<pre><code class="r">dimension_reduction(res, k = 2, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-SD-skmeans-dimension-reduction-1-1.png" alt="plot of chunk tab-SD-skmeans-dimension-reduction-1"/></p>

</div>
<div id='tab-SD-skmeans-dimension-reduction-2'>
<pre><code class="r">dimension_reduction(res, k = 3, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-SD-skmeans-dimension-reduction-2-1.png" alt="plot of chunk tab-SD-skmeans-dimension-reduction-2"/></p>

</div>
<div id='tab-SD-skmeans-dimension-reduction-3'>
<pre><code class="r">dimension_reduction(res, k = 4, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-SD-skmeans-dimension-reduction-3-1.png" alt="plot of chunk tab-SD-skmeans-dimension-reduction-3"/></p>

</div>
<div id='tab-SD-skmeans-dimension-reduction-4'>
<pre><code class="r">dimension_reduction(res, k = 5, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-SD-skmeans-dimension-reduction-4-1.png" alt="plot of chunk tab-SD-skmeans-dimension-reduction-4"/></p>

</div>
<div id='tab-SD-skmeans-dimension-reduction-5'>
<pre><code class="r">dimension_reduction(res, k = 6, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-SD-skmeans-dimension-reduction-5-1.png" alt="plot of chunk tab-SD-skmeans-dimension-reduction-5"/></p>

</div>
</div>


Following heatmap shows how subgroups are split when increasing `k`:

```r
collect_classes(res)
```

![plot of chunk SD-skmeans-collect-classes](figure_cola/SD-skmeans-collect-classes-1.png)


If matrix rows can be associated to genes, consider to use `functional_enrichment(res,
...)` to perform function enrichment for the signature genes. See [this vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/functional_enrichment.html) for more detailed explanations.


 

---------------------------------------------------




### SD:pam






The object with results only for a single top-value method and a single partition method 
can be extracted as:

```r
res = res_list["SD", "pam"]
# you can also extract it by
# res = res_list["SD:pam"]
```

A summary of `res` and all the functions that can be applied to it:

```r
res
```

```
#> A 'ConsensusPartition' object with k = 2, 3, 4, 5, 6.
#>   On a matrix with 15680 rows and 53 columns.
#>   Top rows (1000, 2000, 3000, 4000, 5000) are extracted by 'SD' method.
#>   Subgroups are detected by 'pam' method.
#>   Performed in total 1250 partitions by row resampling.
#>   Best k for subgroups seems to be 2.
#> 
#> Following methods can be applied to this 'ConsensusPartition' object:
#>  [1] "cola_report"             "collect_classes"         "collect_plots"          
#>  [4] "collect_stats"           "colnames"                "compare_signatures"     
#>  [7] "consensus_heatmap"       "dimension_reduction"     "functional_enrichment"  
#> [10] "get_anno_col"            "get_anno"                "get_classes"            
#> [13] "get_consensus"           "get_matrix"              "get_membership"         
#> [16] "get_param"               "get_signatures"          "get_stats"              
#> [19] "is_best_k"               "is_stable_k"             "membership_heatmap"     
#> [22] "ncol"                    "nrow"                    "plot_ecdf"              
#> [25] "rownames"                "select_partition_number" "show"                   
#> [28] "suggest_best_k"          "test_to_known_factors"
```

`collect_plots()` function collects all the plots made from `res` for all `k` (number of partitions)
into one single page to provide an easy and fast comparison between different `k`.

```r
collect_plots(res)
```

![plot of chunk SD-pam-collect-plots](figure_cola/SD-pam-collect-plots-1.png)

The plots are:

- The first row: a plot of the ECDF (empirical cumulative distribution
  function) curves of the consensus matrix for each `k` and the heatmap of
  predicted classes for each `k`.
- The second row: heatmaps of the consensus matrix for each `k`.
- The third row: heatmaps of the membership matrix for each `k`.
- The fouth row: heatmaps of the signatures for each `k`.

All the plots in panels can be made by individual functions and they are
plotted later in this section.

`select_partition_number()` produces several plots showing different
statistics for choosing "optimized" `k`. There are following statistics:

- ECDF curves of the consensus matrix for each `k`;
- 1-PAC. [The PAC
  score](https://en.wikipedia.org/wiki/Consensus_clustering#Over-interpretation_potential_of_consensus_clustering)
  measures the proportion of the ambiguous subgrouping.
- Mean silhouette score.
- Concordance. The mean probability of fiting the consensus class ids in all
  partitions.
- Area increased. Denote $A_k$ as the area under the ECDF curve for current
  `k`, the area increased is defined as $A_k - A_{k-1}$.
- Rand index. The percent of pairs of samples that are both in a same cluster
  or both are not in a same cluster in the partition of k and k-1.
- Jaccard index. The ratio of pairs of samples are both in a same cluster in
  the partition of k and k-1 and the pairs of samples are both in a same
  cluster in the partition k or k-1.

The detailed explanations of these statistics can be found in [the _cola_
vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/cola.html#toc_13).

Generally speaking, lower PAC score, higher mean silhouette score or higher
concordance corresponds to better partition. Rand index and Jaccard index
measure how similar the current partition is compared to partition with `k-1`.
If they are too similar, we won't accept `k` is better than `k-1`.

```r
select_partition_number(res)
```

![plot of chunk SD-pam-select-partition-number](figure_cola/SD-pam-select-partition-number-1.png)

The numeric values for all these statistics can be obtained by `get_stats()`.

```r
get_stats(res)
```

```
#>   k 1-PAC mean_silhouette concordance area_increased  Rand Jaccard
#> 2 2 0.710           0.875       0.926         0.4866 0.512   0.512
#> 3 3 0.636           0.765       0.876         0.3628 0.759   0.558
#> 4 4 0.712           0.779       0.889         0.0838 0.945   0.836
#> 5 5 0.768           0.801       0.891         0.0396 0.972   0.900
#> 6 6 0.788           0.787       0.882         0.0531 0.935   0.758
```

`suggest_best_k()` suggests the best $k$ based on these statistics. The rules are as follows:

- All $k$ with Jaccard index larger than 0.95 are removed because increasing
  $k$ does not provide enough extra information. If all $k$ are removed, it is
  marked as no subgroup is detected.
- For all $k$ with 1-PAC score larger than 0.9, the maximal $k$ is taken as
  the best $k$, and other $k$ are marked as optional $k$.
- If it does not fit the second rule. The $k$ with the maximal vote of the
  highest 1-PAC score, highest mean silhouette, and highest concordance is
  taken as the best $k$.

```r
suggest_best_k(res)
```

```
#> [1] 2
```


Following shows the table of the partitions (You need to click the **show/hide
code output** link to see it). The membership matrix (columns with name `p*`)
is inferred by
[`clue::cl_consensus()`](https://www.rdocumentation.org/link/cl_consensus?package=clue)
function with the `SE` method. Basically the value in the membership matrix
represents the probability to belong to a certain group. The finall class
label for an item is determined with the group with highest probability it
belongs to.

In `get_classes()` function, the entropy is calculated from the membership
matrix and the silhouette score is calculated from the consensus matrix.



<script>
$( function() {
	$( '#tabs-SD-pam-get-classes' ).tabs();
} );
</script>
<div id='tabs-SD-pam-get-classes'>
<ul>
<li><a href='#tab-SD-pam-get-classes-1'>k = 2</a></li>
<li><a href='#tab-SD-pam-get-classes-2'>k = 3</a></li>
<li><a href='#tab-SD-pam-get-classes-3'>k = 4</a></li>
<li><a href='#tab-SD-pam-get-classes-4'>k = 5</a></li>
<li><a href='#tab-SD-pam-get-classes-5'>k = 6</a></li>
</ul>

<div id='tab-SD-pam-get-classes-1'>
<p><a id='tab-SD-pam-get-classes-1-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 2), get_membership(res, k = 2))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2
#&gt; SRR1383358     2  0.1184      0.942 0.016 0.984
#&gt; SRR1383360     2  0.6247      0.867 0.156 0.844
#&gt; SRR1383359     2  0.0000      0.942 0.000 1.000
#&gt; SRR1383362     1  0.9661      0.245 0.608 0.392
#&gt; SRR1383361     2  0.1414      0.942 0.020 0.980
#&gt; SRR1383363     2  0.1414      0.942 0.020 0.980
#&gt; SRR1383364     2  0.7219      0.791 0.200 0.800
#&gt; SRR1383365     2  0.0000      0.942 0.000 1.000
#&gt; SRR1383366     2  0.0000      0.942 0.000 1.000
#&gt; SRR1383367     2  0.1414      0.942 0.020 0.980
#&gt; SRR1383368     2  0.6438      0.861 0.164 0.836
#&gt; SRR1383369     2  0.0000      0.942 0.000 1.000
#&gt; SRR1383370     2  0.0000      0.942 0.000 1.000
#&gt; SRR1383371     2  0.4161      0.909 0.084 0.916
#&gt; SRR1383372     2  0.1414      0.942 0.020 0.980
#&gt; SRR1383373     2  0.1414      0.942 0.020 0.980
#&gt; SRR1383374     2  0.0000      0.942 0.000 1.000
#&gt; SRR1383375     1  0.0000      0.906 1.000 0.000
#&gt; SRR1383376     1  0.4022      0.911 0.920 0.080
#&gt; SRR1383377     2  0.7056      0.781 0.192 0.808
#&gt; SRR1383378     1  0.0938      0.909 0.988 0.012
#&gt; SRR1383379     1  0.9323      0.432 0.652 0.348
#&gt; SRR1383380     1  0.3431      0.916 0.936 0.064
#&gt; SRR1383381     1  0.3274      0.916 0.940 0.060
#&gt; SRR1383382     1  0.0000      0.906 1.000 0.000
#&gt; SRR1383383     1  0.3274      0.916 0.940 0.060
#&gt; SRR1383385     1  0.0000      0.906 1.000 0.000
#&gt; SRR1383384     1  0.3733      0.915 0.928 0.072
#&gt; SRR1383386     1  0.0000      0.906 1.000 0.000
#&gt; SRR1383387     1  0.4161      0.910 0.916 0.084
#&gt; SRR1383389     1  0.3274      0.916 0.940 0.060
#&gt; SRR1383391     1  0.3584      0.915 0.932 0.068
#&gt; SRR1383388     1  0.0000      0.906 1.000 0.000
#&gt; SRR1383392     2  0.0000      0.942 0.000 1.000
#&gt; SRR1383390     1  0.3274      0.916 0.940 0.060
#&gt; SRR1383394     1  0.6148      0.861 0.848 0.152
#&gt; SRR1383393     1  0.0000      0.906 1.000 0.000
#&gt; SRR1383396     1  0.0000      0.906 1.000 0.000
#&gt; SRR1383395     2  0.6048      0.839 0.148 0.852
#&gt; SRR1383399     1  0.3274      0.916 0.940 0.060
#&gt; SRR1383400     1  0.0000      0.906 1.000 0.000
#&gt; SRR1383397     2  0.3879      0.912 0.076 0.924
#&gt; SRR1383401     1  0.3431      0.916 0.936 0.064
#&gt; SRR1383398     1  0.3879      0.912 0.924 0.076
#&gt; SRR1383402     1  0.6247      0.857 0.844 0.156
#&gt; SRR1383404     1  0.0000      0.906 1.000 0.000
#&gt; SRR1383403     1  0.0000      0.906 1.000 0.000
#&gt; SRR1383405     1  0.7950      0.769 0.760 0.240
#&gt; SRR1383406     1  0.5842      0.872 0.860 0.140
#&gt; SRR1383407     1  0.9635      0.398 0.612 0.388
#&gt; SRR1383408     1  0.3584      0.915 0.932 0.068
#&gt; SRR1383409     1  0.3584      0.915 0.932 0.068
#&gt; SRR1383410     2  0.0000      0.942 0.000 1.000
</code></pre>

<script>
$('#tab-SD-pam-get-classes-1-a').parent().next().next().hide();
$('#tab-SD-pam-get-classes-1-a').click(function(){
  $('#tab-SD-pam-get-classes-1-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-SD-pam-get-classes-2'>
<p><a id='tab-SD-pam-get-classes-2-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 3), get_membership(res, k = 3))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3
#&gt; SRR1383358     3  0.0000      0.959 0.000 0.000 1.000
#&gt; SRR1383360     3  0.4047      0.832 0.148 0.004 0.848
#&gt; SRR1383359     3  0.0424      0.954 0.000 0.008 0.992
#&gt; SRR1383362     1  0.6867      0.345 0.636 0.028 0.336
#&gt; SRR1383361     3  0.0000      0.959 0.000 0.000 1.000
#&gt; SRR1383363     3  0.0000      0.959 0.000 0.000 1.000
#&gt; SRR1383364     3  0.1765      0.926 0.040 0.004 0.956
#&gt; SRR1383365     3  0.0000      0.959 0.000 0.000 1.000
#&gt; SRR1383366     3  0.2356      0.903 0.000 0.072 0.928
#&gt; SRR1383367     3  0.0000      0.959 0.000 0.000 1.000
#&gt; SRR1383368     3  0.5058      0.718 0.244 0.000 0.756
#&gt; SRR1383369     3  0.0592      0.953 0.000 0.012 0.988
#&gt; SRR1383370     3  0.0424      0.954 0.000 0.008 0.992
#&gt; SRR1383371     3  0.0237      0.957 0.004 0.000 0.996
#&gt; SRR1383372     3  0.0747      0.949 0.000 0.016 0.984
#&gt; SRR1383373     3  0.0000      0.959 0.000 0.000 1.000
#&gt; SRR1383374     3  0.0000      0.959 0.000 0.000 1.000
#&gt; SRR1383375     1  0.0000      0.788 1.000 0.000 0.000
#&gt; SRR1383376     2  0.1711      0.837 0.032 0.960 0.008
#&gt; SRR1383377     2  0.5882      0.442 0.000 0.652 0.348
#&gt; SRR1383378     1  0.4902      0.768 0.844 0.092 0.064
#&gt; SRR1383379     2  0.5216      0.645 0.260 0.740 0.000
#&gt; SRR1383380     1  0.4953      0.732 0.808 0.176 0.016
#&gt; SRR1383381     1  0.6470      0.739 0.760 0.148 0.092
#&gt; SRR1383382     1  0.1163      0.776 0.972 0.028 0.000
#&gt; SRR1383383     1  0.6431      0.739 0.760 0.156 0.084
#&gt; SRR1383385     1  0.0424      0.786 0.992 0.008 0.000
#&gt; SRR1383384     1  0.6540      0.426 0.584 0.408 0.008
#&gt; SRR1383386     1  0.0000      0.788 1.000 0.000 0.000
#&gt; SRR1383387     2  0.1163      0.838 0.028 0.972 0.000
#&gt; SRR1383389     1  0.6351      0.737 0.760 0.168 0.072
#&gt; SRR1383391     1  0.6925      0.333 0.532 0.452 0.016
#&gt; SRR1383388     1  0.0592      0.787 0.988 0.012 0.000
#&gt; SRR1383392     2  0.1529      0.842 0.000 0.960 0.040
#&gt; SRR1383390     1  0.6283      0.735 0.760 0.176 0.064
#&gt; SRR1383394     2  0.1585      0.838 0.028 0.964 0.008
#&gt; SRR1383393     1  0.0237      0.788 0.996 0.004 0.000
#&gt; SRR1383396     1  0.0000      0.788 1.000 0.000 0.000
#&gt; SRR1383395     2  0.3038      0.807 0.000 0.896 0.104
#&gt; SRR1383399     1  0.6470      0.739 0.760 0.148 0.092
#&gt; SRR1383400     1  0.1163      0.776 0.972 0.028 0.000
#&gt; SRR1383397     2  0.4075      0.806 0.048 0.880 0.072
#&gt; SRR1383401     2  0.6742      0.363 0.316 0.656 0.028
#&gt; SRR1383398     2  0.4172      0.803 0.104 0.868 0.028
#&gt; SRR1383402     2  0.5884      0.484 0.272 0.716 0.012
#&gt; SRR1383404     1  0.0237      0.788 0.996 0.004 0.000
#&gt; SRR1383403     1  0.0237      0.788 0.996 0.004 0.000
#&gt; SRR1383405     2  0.1337      0.842 0.016 0.972 0.012
#&gt; SRR1383406     2  0.2599      0.839 0.016 0.932 0.052
#&gt; SRR1383407     1  0.8963      0.313 0.468 0.128 0.404
#&gt; SRR1383408     1  0.5450      0.705 0.760 0.228 0.012
#&gt; SRR1383409     1  0.7661      0.288 0.504 0.452 0.044
#&gt; SRR1383410     2  0.1529      0.842 0.000 0.960 0.040
</code></pre>

<script>
$('#tab-SD-pam-get-classes-2-a').parent().next().next().hide();
$('#tab-SD-pam-get-classes-2-a').click(function(){
  $('#tab-SD-pam-get-classes-2-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-SD-pam-get-classes-3'>
<p><a id='tab-SD-pam-get-classes-3-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 4), get_membership(res, k = 4))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4
#&gt; SRR1383358     3  0.0000      0.956 0.000 0.000 1.000 0.000
#&gt; SRR1383360     3  0.3928      0.834 0.056 0.084 0.852 0.008
#&gt; SRR1383359     3  0.0000      0.956 0.000 0.000 1.000 0.000
#&gt; SRR1383362     1  0.0188      0.864 0.996 0.004 0.000 0.000
#&gt; SRR1383361     3  0.0000      0.956 0.000 0.000 1.000 0.000
#&gt; SRR1383363     3  0.0000      0.956 0.000 0.000 1.000 0.000
#&gt; SRR1383364     3  0.1743      0.915 0.004 0.056 0.940 0.000
#&gt; SRR1383365     3  0.0000      0.956 0.000 0.000 1.000 0.000
#&gt; SRR1383366     3  0.2530      0.854 0.000 0.000 0.888 0.112
#&gt; SRR1383367     3  0.0000      0.956 0.000 0.000 1.000 0.000
#&gt; SRR1383368     3  0.3224      0.845 0.120 0.016 0.864 0.000
#&gt; SRR1383369     3  0.0376      0.954 0.004 0.004 0.992 0.000
#&gt; SRR1383370     3  0.1389      0.929 0.000 0.000 0.952 0.048
#&gt; SRR1383371     3  0.0376      0.954 0.004 0.004 0.992 0.000
#&gt; SRR1383372     3  0.1474      0.923 0.000 0.052 0.948 0.000
#&gt; SRR1383373     3  0.0000      0.956 0.000 0.000 1.000 0.000
#&gt; SRR1383374     3  0.0000      0.956 0.000 0.000 1.000 0.000
#&gt; SRR1383375     2  0.3447      0.765 0.128 0.852 0.000 0.020
#&gt; SRR1383376     4  0.2973      0.809 0.000 0.144 0.000 0.856
#&gt; SRR1383377     4  0.4454      0.457 0.000 0.000 0.308 0.692
#&gt; SRR1383378     2  0.0000      0.812 0.000 1.000 0.000 0.000
#&gt; SRR1383379     4  0.3102      0.778 0.064 0.024 0.016 0.896
#&gt; SRR1383380     2  0.3528      0.744 0.000 0.808 0.000 0.192
#&gt; SRR1383381     2  0.0188      0.812 0.004 0.996 0.000 0.000
#&gt; SRR1383382     1  0.0188      0.864 0.996 0.004 0.000 0.000
#&gt; SRR1383383     2  0.0188      0.812 0.000 0.996 0.000 0.004
#&gt; SRR1383385     1  0.6280      0.427 0.604 0.316 0.000 0.080
#&gt; SRR1383384     2  0.3726      0.609 0.000 0.788 0.000 0.212
#&gt; SRR1383386     2  0.3105      0.778 0.120 0.868 0.000 0.012
#&gt; SRR1383387     4  0.1940      0.819 0.000 0.076 0.000 0.924
#&gt; SRR1383389     2  0.0188      0.812 0.000 0.996 0.000 0.004
#&gt; SRR1383391     2  0.5228      0.474 0.000 0.696 0.036 0.268
#&gt; SRR1383388     2  0.3833      0.772 0.072 0.848 0.000 0.080
#&gt; SRR1383392     4  0.3105      0.810 0.000 0.140 0.004 0.856
#&gt; SRR1383390     2  0.0188      0.812 0.000 0.996 0.000 0.004
#&gt; SRR1383394     4  0.2973      0.809 0.000 0.144 0.000 0.856
#&gt; SRR1383393     2  0.3828      0.767 0.068 0.848 0.000 0.084
#&gt; SRR1383396     2  0.3047      0.779 0.116 0.872 0.000 0.012
#&gt; SRR1383395     4  0.0188      0.789 0.000 0.000 0.004 0.996
#&gt; SRR1383399     2  0.0188      0.812 0.004 0.996 0.000 0.000
#&gt; SRR1383400     1  0.0188      0.864 0.996 0.004 0.000 0.000
#&gt; SRR1383397     4  0.0592      0.801 0.000 0.016 0.000 0.984
#&gt; SRR1383401     4  0.5295      0.214 0.000 0.488 0.008 0.504
#&gt; SRR1383398     4  0.1867      0.754 0.000 0.072 0.000 0.928
#&gt; SRR1383402     4  0.5070      0.401 0.000 0.416 0.004 0.580
#&gt; SRR1383404     2  0.3224      0.777 0.120 0.864 0.000 0.016
#&gt; SRR1383403     2  0.5594      0.626 0.192 0.716 0.000 0.092
#&gt; SRR1383405     4  0.1940      0.819 0.000 0.076 0.000 0.924
#&gt; SRR1383406     4  0.1406      0.796 0.000 0.016 0.024 0.960
#&gt; SRR1383407     2  0.4964      0.352 0.000 0.616 0.380 0.004
#&gt; SRR1383408     2  0.0921      0.802 0.000 0.972 0.000 0.028
#&gt; SRR1383409     2  0.6015      0.419 0.000 0.652 0.080 0.268
#&gt; SRR1383410     4  0.3105      0.810 0.000 0.140 0.004 0.856
</code></pre>

<script>
$('#tab-SD-pam-get-classes-3-a').parent().next().next().hide();
$('#tab-SD-pam-get-classes-3-a').click(function(){
  $('#tab-SD-pam-get-classes-3-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-SD-pam-get-classes-4'>
<p><a id='tab-SD-pam-get-classes-4-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 5), get_membership(res, k = 5))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4    p5
#&gt; SRR1383358     3  0.0000      0.952 0.000 0.000 1.000 0.000 0.000
#&gt; SRR1383360     3  0.2450      0.888 0.000 0.052 0.900 0.000 0.048
#&gt; SRR1383359     3  0.0000      0.952 0.000 0.000 1.000 0.000 0.000
#&gt; SRR1383362     1  0.1671      1.000 0.924 0.000 0.000 0.000 0.076
#&gt; SRR1383361     3  0.0000      0.952 0.000 0.000 1.000 0.000 0.000
#&gt; SRR1383363     3  0.0000      0.952 0.000 0.000 1.000 0.000 0.000
#&gt; SRR1383364     3  0.3572      0.849 0.076 0.068 0.844 0.000 0.012
#&gt; SRR1383365     3  0.0000      0.952 0.000 0.000 1.000 0.000 0.000
#&gt; SRR1383366     3  0.1671      0.891 0.000 0.000 0.924 0.076 0.000
#&gt; SRR1383367     3  0.0000      0.952 0.000 0.000 1.000 0.000 0.000
#&gt; SRR1383368     3  0.2886      0.829 0.000 0.008 0.844 0.000 0.148
#&gt; SRR1383369     3  0.1587      0.934 0.008 0.020 0.952 0.008 0.012
#&gt; SRR1383370     3  0.0510      0.946 0.000 0.000 0.984 0.016 0.000
#&gt; SRR1383371     3  0.2354      0.906 0.076 0.008 0.904 0.000 0.012
#&gt; SRR1383372     3  0.1043      0.933 0.000 0.040 0.960 0.000 0.000
#&gt; SRR1383373     3  0.0000      0.952 0.000 0.000 1.000 0.000 0.000
#&gt; SRR1383374     3  0.0000      0.952 0.000 0.000 1.000 0.000 0.000
#&gt; SRR1383375     2  0.2773      0.771 0.000 0.836 0.000 0.000 0.164
#&gt; SRR1383376     4  0.2648      0.792 0.000 0.152 0.000 0.848 0.000
#&gt; SRR1383377     4  0.4088      0.435 0.000 0.000 0.304 0.688 0.008
#&gt; SRR1383378     2  0.0324      0.812 0.000 0.992 0.000 0.004 0.004
#&gt; SRR1383379     4  0.2623      0.758 0.000 0.004 0.016 0.884 0.096
#&gt; SRR1383380     2  0.3530      0.727 0.000 0.784 0.000 0.204 0.012
#&gt; SRR1383381     2  0.2069      0.798 0.076 0.912 0.000 0.000 0.012
#&gt; SRR1383382     1  0.1671      1.000 0.924 0.000 0.000 0.000 0.076
#&gt; SRR1383383     2  0.0290      0.812 0.000 0.992 0.000 0.008 0.000
#&gt; SRR1383385     5  0.1877      0.971 0.012 0.000 0.000 0.064 0.924
#&gt; SRR1383384     2  0.3274      0.598 0.000 0.780 0.000 0.220 0.000
#&gt; SRR1383386     2  0.3098      0.776 0.000 0.836 0.000 0.016 0.148
#&gt; SRR1383387     4  0.1478      0.806 0.000 0.064 0.000 0.936 0.000
#&gt; SRR1383389     2  0.0290      0.812 0.000 0.992 0.000 0.008 0.000
#&gt; SRR1383391     2  0.4161      0.484 0.000 0.704 0.016 0.280 0.000
#&gt; SRR1383388     2  0.3365      0.777 0.000 0.836 0.000 0.044 0.120
#&gt; SRR1383392     4  0.3060      0.797 0.000 0.128 0.024 0.848 0.000
#&gt; SRR1383390     2  0.0290      0.812 0.000 0.992 0.000 0.008 0.000
#&gt; SRR1383394     4  0.2690      0.789 0.000 0.156 0.000 0.844 0.000
#&gt; SRR1383393     5  0.2144      0.941 0.000 0.020 0.000 0.068 0.912
#&gt; SRR1383396     2  0.2886      0.776 0.000 0.844 0.000 0.008 0.148
#&gt; SRR1383395     4  0.0566      0.772 0.000 0.000 0.004 0.984 0.012
#&gt; SRR1383399     2  0.2069      0.798 0.076 0.912 0.000 0.000 0.012
#&gt; SRR1383400     1  0.1671      1.000 0.924 0.000 0.000 0.000 0.076
#&gt; SRR1383397     4  0.0000      0.780 0.000 0.000 0.000 1.000 0.000
#&gt; SRR1383401     4  0.4448      0.223 0.000 0.480 0.004 0.516 0.000
#&gt; SRR1383398     4  0.2006      0.743 0.000 0.072 0.000 0.916 0.012
#&gt; SRR1383402     4  0.4242      0.360 0.000 0.428 0.000 0.572 0.000
#&gt; SRR1383404     2  0.3098      0.776 0.000 0.836 0.000 0.016 0.148
#&gt; SRR1383403     5  0.1877      0.971 0.012 0.000 0.000 0.064 0.924
#&gt; SRR1383405     4  0.1478      0.806 0.000 0.064 0.000 0.936 0.000
#&gt; SRR1383406     4  0.1638      0.761 0.000 0.004 0.064 0.932 0.000
#&gt; SRR1383407     2  0.4264      0.366 0.000 0.620 0.376 0.004 0.000
#&gt; SRR1383408     2  0.1043      0.801 0.000 0.960 0.000 0.040 0.000
#&gt; SRR1383409     2  0.4780      0.448 0.000 0.672 0.048 0.280 0.000
#&gt; SRR1383410     4  0.3060      0.797 0.000 0.128 0.024 0.848 0.000
</code></pre>

<script>
$('#tab-SD-pam-get-classes-4-a').parent().next().next().hide();
$('#tab-SD-pam-get-classes-4-a').click(function(){
  $('#tab-SD-pam-get-classes-4-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-SD-pam-get-classes-5'>
<p><a id='tab-SD-pam-get-classes-5-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 6), get_membership(res, k = 6))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4    p5 p6
#&gt; SRR1383358     3  0.0000      0.964 0.000 0.000 1.000 0.000 0.000  0
#&gt; SRR1383360     3  0.1007      0.933 0.044 0.000 0.956 0.000 0.000  0
#&gt; SRR1383359     3  0.0000      0.964 0.000 0.000 1.000 0.000 0.000  0
#&gt; SRR1383362     6  0.0000      1.000 0.000 0.000 0.000 0.000 0.000  1
#&gt; SRR1383361     3  0.0000      0.964 0.000 0.000 1.000 0.000 0.000  0
#&gt; SRR1383363     3  0.0000      0.964 0.000 0.000 1.000 0.000 0.000  0
#&gt; SRR1383364     5  0.0000      0.971 0.000 0.000 0.000 0.000 1.000  0
#&gt; SRR1383365     3  0.0000      0.964 0.000 0.000 1.000 0.000 0.000  0
#&gt; SRR1383366     3  0.0000      0.964 0.000 0.000 1.000 0.000 0.000  0
#&gt; SRR1383367     3  0.0000      0.964 0.000 0.000 1.000 0.000 0.000  0
#&gt; SRR1383368     3  0.3261      0.795 0.072 0.104 0.824 0.000 0.000  0
#&gt; SRR1383369     3  0.2418      0.873 0.000 0.016 0.884 0.008 0.092  0
#&gt; SRR1383370     3  0.0363      0.957 0.000 0.000 0.988 0.012 0.000  0
#&gt; SRR1383371     5  0.1141      0.911 0.000 0.000 0.052 0.000 0.948  0
#&gt; SRR1383372     3  0.1720      0.897 0.000 0.040 0.928 0.032 0.000  0
#&gt; SRR1383373     3  0.0000      0.964 0.000 0.000 1.000 0.000 0.000  0
#&gt; SRR1383374     3  0.0000      0.964 0.000 0.000 1.000 0.000 0.000  0
#&gt; SRR1383375     2  0.2300      0.692 0.144 0.856 0.000 0.000 0.000  0
#&gt; SRR1383376     4  0.2260      0.739 0.000 0.140 0.000 0.860 0.000  0
#&gt; SRR1383377     4  0.4168      0.508 0.048 0.000 0.256 0.696 0.000  0
#&gt; SRR1383378     2  0.1444      0.778 0.000 0.928 0.000 0.072 0.000  0
#&gt; SRR1383379     4  0.2377      0.723 0.024 0.076 0.008 0.892 0.000  0
#&gt; SRR1383380     2  0.4075      0.660 0.076 0.740 0.000 0.184 0.000  0
#&gt; SRR1383381     5  0.0000      0.971 0.000 0.000 0.000 0.000 1.000  0
#&gt; SRR1383382     6  0.0000      1.000 0.000 0.000 0.000 0.000 0.000  1
#&gt; SRR1383383     2  0.1444      0.778 0.000 0.928 0.000 0.072 0.000  0
#&gt; SRR1383385     1  0.0000      0.950 1.000 0.000 0.000 0.000 0.000  0
#&gt; SRR1383384     2  0.3126      0.640 0.000 0.752 0.000 0.248 0.000  0
#&gt; SRR1383386     2  0.2857      0.708 0.072 0.856 0.000 0.072 0.000  0
#&gt; SRR1383387     4  0.0000      0.770 0.000 0.000 0.000 1.000 0.000  0
#&gt; SRR1383389     2  0.1444      0.778 0.000 0.928 0.000 0.072 0.000  0
#&gt; SRR1383391     2  0.3717      0.421 0.000 0.616 0.000 0.384 0.000  0
#&gt; SRR1383388     2  0.2795      0.709 0.044 0.856 0.000 0.100 0.000  0
#&gt; SRR1383392     4  0.2618      0.750 0.000 0.116 0.024 0.860 0.000  0
#&gt; SRR1383390     2  0.1444      0.778 0.000 0.928 0.000 0.072 0.000  0
#&gt; SRR1383394     4  0.2300      0.735 0.000 0.144 0.000 0.856 0.000  0
#&gt; SRR1383393     1  0.1657      0.900 0.928 0.016 0.000 0.056 0.000  0
#&gt; SRR1383396     2  0.1946      0.734 0.072 0.912 0.000 0.012 0.004  0
#&gt; SRR1383395     4  0.1501      0.735 0.076 0.000 0.000 0.924 0.000  0
#&gt; SRR1383399     5  0.0000      0.971 0.000 0.000 0.000 0.000 1.000  0
#&gt; SRR1383400     6  0.0000      1.000 0.000 0.000 0.000 0.000 0.000  1
#&gt; SRR1383397     4  0.1444      0.738 0.072 0.000 0.000 0.928 0.000  0
#&gt; SRR1383401     2  0.6016      0.131 0.000 0.404 0.000 0.244 0.352  0
#&gt; SRR1383398     4  0.2966      0.702 0.076 0.076 0.000 0.848 0.000  0
#&gt; SRR1383402     4  0.3684      0.323 0.000 0.372 0.000 0.628 0.000  0
#&gt; SRR1383404     2  0.2857      0.708 0.072 0.856 0.000 0.072 0.000  0
#&gt; SRR1383403     1  0.0000      0.950 1.000 0.000 0.000 0.000 0.000  0
#&gt; SRR1383405     4  0.0000      0.770 0.000 0.000 0.000 1.000 0.000  0
#&gt; SRR1383406     4  0.4670      0.264 0.036 0.004 0.412 0.548 0.000  0
#&gt; SRR1383407     2  0.2747      0.735 0.000 0.860 0.096 0.044 0.000  0
#&gt; SRR1383408     2  0.1814      0.771 0.000 0.900 0.000 0.100 0.000  0
#&gt; SRR1383409     2  0.3717      0.421 0.000 0.616 0.000 0.384 0.000  0
#&gt; SRR1383410     4  0.2618      0.750 0.000 0.116 0.024 0.860 0.000  0
</code></pre>

<script>
$('#tab-SD-pam-get-classes-5-a').parent().next().next().hide();
$('#tab-SD-pam-get-classes-5-a').click(function(){
  $('#tab-SD-pam-get-classes-5-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>
</div>

Heatmaps for the consensus matrix. It visualizes the probability of two
samples to be in a same group.



<script>
$( function() {
	$( '#tabs-SD-pam-consensus-heatmap' ).tabs();
} );
</script>
<div id='tabs-SD-pam-consensus-heatmap'>
<ul>
<li><a href='#tab-SD-pam-consensus-heatmap-1'>k = 2</a></li>
<li><a href='#tab-SD-pam-consensus-heatmap-2'>k = 3</a></li>
<li><a href='#tab-SD-pam-consensus-heatmap-3'>k = 4</a></li>
<li><a href='#tab-SD-pam-consensus-heatmap-4'>k = 5</a></li>
<li><a href='#tab-SD-pam-consensus-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-SD-pam-consensus-heatmap-1'>
<pre><code class="r">consensus_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-SD-pam-consensus-heatmap-1-1.png" alt="plot of chunk tab-SD-pam-consensus-heatmap-1"/></p>

</div>
<div id='tab-SD-pam-consensus-heatmap-2'>
<pre><code class="r">consensus_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-SD-pam-consensus-heatmap-2-1.png" alt="plot of chunk tab-SD-pam-consensus-heatmap-2"/></p>

</div>
<div id='tab-SD-pam-consensus-heatmap-3'>
<pre><code class="r">consensus_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-SD-pam-consensus-heatmap-3-1.png" alt="plot of chunk tab-SD-pam-consensus-heatmap-3"/></p>

</div>
<div id='tab-SD-pam-consensus-heatmap-4'>
<pre><code class="r">consensus_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-SD-pam-consensus-heatmap-4-1.png" alt="plot of chunk tab-SD-pam-consensus-heatmap-4"/></p>

</div>
<div id='tab-SD-pam-consensus-heatmap-5'>
<pre><code class="r">consensus_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-SD-pam-consensus-heatmap-5-1.png" alt="plot of chunk tab-SD-pam-consensus-heatmap-5"/></p>

</div>
</div>

Heatmaps for the membership of samples in all partitions to see how consistent they are:




<script>
$( function() {
	$( '#tabs-SD-pam-membership-heatmap' ).tabs();
} );
</script>
<div id='tabs-SD-pam-membership-heatmap'>
<ul>
<li><a href='#tab-SD-pam-membership-heatmap-1'>k = 2</a></li>
<li><a href='#tab-SD-pam-membership-heatmap-2'>k = 3</a></li>
<li><a href='#tab-SD-pam-membership-heatmap-3'>k = 4</a></li>
<li><a href='#tab-SD-pam-membership-heatmap-4'>k = 5</a></li>
<li><a href='#tab-SD-pam-membership-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-SD-pam-membership-heatmap-1'>
<pre><code class="r">membership_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-SD-pam-membership-heatmap-1-1.png" alt="plot of chunk tab-SD-pam-membership-heatmap-1"/></p>

</div>
<div id='tab-SD-pam-membership-heatmap-2'>
<pre><code class="r">membership_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-SD-pam-membership-heatmap-2-1.png" alt="plot of chunk tab-SD-pam-membership-heatmap-2"/></p>

</div>
<div id='tab-SD-pam-membership-heatmap-3'>
<pre><code class="r">membership_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-SD-pam-membership-heatmap-3-1.png" alt="plot of chunk tab-SD-pam-membership-heatmap-3"/></p>

</div>
<div id='tab-SD-pam-membership-heatmap-4'>
<pre><code class="r">membership_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-SD-pam-membership-heatmap-4-1.png" alt="plot of chunk tab-SD-pam-membership-heatmap-4"/></p>

</div>
<div id='tab-SD-pam-membership-heatmap-5'>
<pre><code class="r">membership_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-SD-pam-membership-heatmap-5-1.png" alt="plot of chunk tab-SD-pam-membership-heatmap-5"/></p>

</div>
</div>

As soon as we have had the classes for columns, we can look for signatures
which are significantly different between classes which can be candidate marks
for certain classes. Following are the heatmaps for signatures.



Signature heatmaps where rows are scaled:



<script>
$( function() {
	$( '#tabs-SD-pam-get-signatures' ).tabs();
} );
</script>
<div id='tabs-SD-pam-get-signatures'>
<ul>
<li><a href='#tab-SD-pam-get-signatures-1'>k = 2</a></li>
<li><a href='#tab-SD-pam-get-signatures-2'>k = 3</a></li>
<li><a href='#tab-SD-pam-get-signatures-3'>k = 4</a></li>
<li><a href='#tab-SD-pam-get-signatures-4'>k = 5</a></li>
<li><a href='#tab-SD-pam-get-signatures-5'>k = 6</a></li>
</ul>
<div id='tab-SD-pam-get-signatures-1'>
<pre><code class="r">get_signatures(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-SD-pam-get-signatures-1-1.png" alt="plot of chunk tab-SD-pam-get-signatures-1"/></p>

</div>
<div id='tab-SD-pam-get-signatures-2'>
<pre><code class="r">get_signatures(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-SD-pam-get-signatures-2-1.png" alt="plot of chunk tab-SD-pam-get-signatures-2"/></p>

</div>
<div id='tab-SD-pam-get-signatures-3'>
<pre><code class="r">get_signatures(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-SD-pam-get-signatures-3-1.png" alt="plot of chunk tab-SD-pam-get-signatures-3"/></p>

</div>
<div id='tab-SD-pam-get-signatures-4'>
<pre><code class="r">get_signatures(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-SD-pam-get-signatures-4-1.png" alt="plot of chunk tab-SD-pam-get-signatures-4"/></p>

</div>
<div id='tab-SD-pam-get-signatures-5'>
<pre><code class="r">get_signatures(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-SD-pam-get-signatures-5-1.png" alt="plot of chunk tab-SD-pam-get-signatures-5"/></p>

</div>
</div>



Signature heatmaps where rows are not scaled:


<script>
$( function() {
	$( '#tabs-SD-pam-get-signatures-no-scale' ).tabs();
} );
</script>
<div id='tabs-SD-pam-get-signatures-no-scale'>
<ul>
<li><a href='#tab-SD-pam-get-signatures-no-scale-1'>k = 2</a></li>
<li><a href='#tab-SD-pam-get-signatures-no-scale-2'>k = 3</a></li>
<li><a href='#tab-SD-pam-get-signatures-no-scale-3'>k = 4</a></li>
<li><a href='#tab-SD-pam-get-signatures-no-scale-4'>k = 5</a></li>
<li><a href='#tab-SD-pam-get-signatures-no-scale-5'>k = 6</a></li>
</ul>
<div id='tab-SD-pam-get-signatures-no-scale-1'>
<pre><code class="r">get_signatures(res, k = 2, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-SD-pam-get-signatures-no-scale-1-1.png" alt="plot of chunk tab-SD-pam-get-signatures-no-scale-1"/></p>

</div>
<div id='tab-SD-pam-get-signatures-no-scale-2'>
<pre><code class="r">get_signatures(res, k = 3, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-SD-pam-get-signatures-no-scale-2-1.png" alt="plot of chunk tab-SD-pam-get-signatures-no-scale-2"/></p>

</div>
<div id='tab-SD-pam-get-signatures-no-scale-3'>
<pre><code class="r">get_signatures(res, k = 4, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-SD-pam-get-signatures-no-scale-3-1.png" alt="plot of chunk tab-SD-pam-get-signatures-no-scale-3"/></p>

</div>
<div id='tab-SD-pam-get-signatures-no-scale-4'>
<pre><code class="r">get_signatures(res, k = 5, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-SD-pam-get-signatures-no-scale-4-1.png" alt="plot of chunk tab-SD-pam-get-signatures-no-scale-4"/></p>

</div>
<div id='tab-SD-pam-get-signatures-no-scale-5'>
<pre><code class="r">get_signatures(res, k = 6, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-SD-pam-get-signatures-no-scale-5-1.png" alt="plot of chunk tab-SD-pam-get-signatures-no-scale-5"/></p>

</div>
</div>



Compare the overlap of signatures from different k:

```r
compare_signatures(res)
```

![plot of chunk SD-pam-signature_compare](figure_cola/SD-pam-signature_compare-1.png)

`get_signature()` returns a data frame invisibly. TO get the list of signatures, the function
call should be assigned to a variable explicitly. In following code, if `plot` argument is set
to `FALSE`, no heatmap is plotted while only the differential analysis is performed.

```r
# code only for demonstration
tb = get_signature(res, k = ..., plot = FALSE)
```

An example of the output of `tb` is:

```
#>   which_row         fdr    mean_1    mean_2 scaled_mean_1 scaled_mean_2 km
#> 1        38 0.042760348  8.373488  9.131774    -0.5533452     0.5164555  1
#> 2        40 0.018707592  7.106213  8.469186    -0.6173731     0.5762149  1
#> 3        55 0.019134737 10.221463 11.207825    -0.6159697     0.5749050  1
#> 4        59 0.006059896  5.921854  7.869574    -0.6899429     0.6439467  1
#> 5        60 0.018055526  8.928898 10.211722    -0.6204761     0.5791110  1
#> 6        98 0.009384629 15.714769 14.887706     0.6635654    -0.6193277  2
...
```

The columns in `tb` are:

1. `which_row`: row indices corresponding to the input matrix.
2. `fdr`: FDR for the differential test. 
3. `mean_x`: The mean value in group x.
4. `scaled_mean_x`: The mean value in group x after rows are scaled.
5. `km`: Row groups if k-means clustering is applied to rows.



UMAP plot which shows how samples are separated.


<script>
$( function() {
	$( '#tabs-SD-pam-dimension-reduction' ).tabs();
} );
</script>
<div id='tabs-SD-pam-dimension-reduction'>
<ul>
<li><a href='#tab-SD-pam-dimension-reduction-1'>k = 2</a></li>
<li><a href='#tab-SD-pam-dimension-reduction-2'>k = 3</a></li>
<li><a href='#tab-SD-pam-dimension-reduction-3'>k = 4</a></li>
<li><a href='#tab-SD-pam-dimension-reduction-4'>k = 5</a></li>
<li><a href='#tab-SD-pam-dimension-reduction-5'>k = 6</a></li>
</ul>
<div id='tab-SD-pam-dimension-reduction-1'>
<pre><code class="r">dimension_reduction(res, k = 2, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-SD-pam-dimension-reduction-1-1.png" alt="plot of chunk tab-SD-pam-dimension-reduction-1"/></p>

</div>
<div id='tab-SD-pam-dimension-reduction-2'>
<pre><code class="r">dimension_reduction(res, k = 3, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-SD-pam-dimension-reduction-2-1.png" alt="plot of chunk tab-SD-pam-dimension-reduction-2"/></p>

</div>
<div id='tab-SD-pam-dimension-reduction-3'>
<pre><code class="r">dimension_reduction(res, k = 4, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-SD-pam-dimension-reduction-3-1.png" alt="plot of chunk tab-SD-pam-dimension-reduction-3"/></p>

</div>
<div id='tab-SD-pam-dimension-reduction-4'>
<pre><code class="r">dimension_reduction(res, k = 5, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-SD-pam-dimension-reduction-4-1.png" alt="plot of chunk tab-SD-pam-dimension-reduction-4"/></p>

</div>
<div id='tab-SD-pam-dimension-reduction-5'>
<pre><code class="r">dimension_reduction(res, k = 6, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-SD-pam-dimension-reduction-5-1.png" alt="plot of chunk tab-SD-pam-dimension-reduction-5"/></p>

</div>
</div>


Following heatmap shows how subgroups are split when increasing `k`:

```r
collect_classes(res)
```

![plot of chunk SD-pam-collect-classes](figure_cola/SD-pam-collect-classes-1.png)


If matrix rows can be associated to genes, consider to use `functional_enrichment(res,
...)` to perform function enrichment for the signature genes. See [this vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/functional_enrichment.html) for more detailed explanations.


 

---------------------------------------------------




### SD:mclust**






The object with results only for a single top-value method and a single partition method 
can be extracted as:

```r
res = res_list["SD", "mclust"]
# you can also extract it by
# res = res_list["SD:mclust"]
```

A summary of `res` and all the functions that can be applied to it:

```r
res
```

```
#> A 'ConsensusPartition' object with k = 2, 3, 4, 5, 6.
#>   On a matrix with 15680 rows and 53 columns.
#>   Top rows (1000, 2000, 3000, 4000, 5000) are extracted by 'SD' method.
#>   Subgroups are detected by 'mclust' method.
#>   Performed in total 1250 partitions by row resampling.
#>   Best k for subgroups seems to be 2.
#> 
#> Following methods can be applied to this 'ConsensusPartition' object:
#>  [1] "cola_report"             "collect_classes"         "collect_plots"          
#>  [4] "collect_stats"           "colnames"                "compare_signatures"     
#>  [7] "consensus_heatmap"       "dimension_reduction"     "functional_enrichment"  
#> [10] "get_anno_col"            "get_anno"                "get_classes"            
#> [13] "get_consensus"           "get_matrix"              "get_membership"         
#> [16] "get_param"               "get_signatures"          "get_stats"              
#> [19] "is_best_k"               "is_stable_k"             "membership_heatmap"     
#> [22] "ncol"                    "nrow"                    "plot_ecdf"              
#> [25] "rownames"                "select_partition_number" "show"                   
#> [28] "suggest_best_k"          "test_to_known_factors"
```

`collect_plots()` function collects all the plots made from `res` for all `k` (number of partitions)
into one single page to provide an easy and fast comparison between different `k`.

```r
collect_plots(res)
```

![plot of chunk SD-mclust-collect-plots](figure_cola/SD-mclust-collect-plots-1.png)

The plots are:

- The first row: a plot of the ECDF (empirical cumulative distribution
  function) curves of the consensus matrix for each `k` and the heatmap of
  predicted classes for each `k`.
- The second row: heatmaps of the consensus matrix for each `k`.
- The third row: heatmaps of the membership matrix for each `k`.
- The fouth row: heatmaps of the signatures for each `k`.

All the plots in panels can be made by individual functions and they are
plotted later in this section.

`select_partition_number()` produces several plots showing different
statistics for choosing "optimized" `k`. There are following statistics:

- ECDF curves of the consensus matrix for each `k`;
- 1-PAC. [The PAC
  score](https://en.wikipedia.org/wiki/Consensus_clustering#Over-interpretation_potential_of_consensus_clustering)
  measures the proportion of the ambiguous subgrouping.
- Mean silhouette score.
- Concordance. The mean probability of fiting the consensus class ids in all
  partitions.
- Area increased. Denote $A_k$ as the area under the ECDF curve for current
  `k`, the area increased is defined as $A_k - A_{k-1}$.
- Rand index. The percent of pairs of samples that are both in a same cluster
  or both are not in a same cluster in the partition of k and k-1.
- Jaccard index. The ratio of pairs of samples are both in a same cluster in
  the partition of k and k-1 and the pairs of samples are both in a same
  cluster in the partition k or k-1.

The detailed explanations of these statistics can be found in [the _cola_
vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/cola.html#toc_13).

Generally speaking, lower PAC score, higher mean silhouette score or higher
concordance corresponds to better partition. Rand index and Jaccard index
measure how similar the current partition is compared to partition with `k-1`.
If they are too similar, we won't accept `k` is better than `k-1`.

```r
select_partition_number(res)
```

![plot of chunk SD-mclust-select-partition-number](figure_cola/SD-mclust-select-partition-number-1.png)

The numeric values for all these statistics can be obtained by `get_stats()`.

```r
get_stats(res)
```

```
#>   k 1-PAC mean_silhouette concordance area_increased  Rand Jaccard
#> 2 2 1.000           0.951       0.963         0.2654 0.766   0.766
#> 3 3 0.376           0.702       0.820         1.1014 0.721   0.635
#> 4 4 0.442           0.455       0.756         0.2213 0.830   0.657
#> 5 5 0.447           0.532       0.695         0.0759 0.845   0.567
#> 6 6 0.598           0.557       0.652         0.0661 0.818   0.385
```

`suggest_best_k()` suggests the best $k$ based on these statistics. The rules are as follows:

- All $k$ with Jaccard index larger than 0.95 are removed because increasing
  $k$ does not provide enough extra information. If all $k$ are removed, it is
  marked as no subgroup is detected.
- For all $k$ with 1-PAC score larger than 0.9, the maximal $k$ is taken as
  the best $k$, and other $k$ are marked as optional $k$.
- If it does not fit the second rule. The $k$ with the maximal vote of the
  highest 1-PAC score, highest mean silhouette, and highest concordance is
  taken as the best $k$.

```r
suggest_best_k(res)
```

```
#> [1] 2
```


Following shows the table of the partitions (You need to click the **show/hide
code output** link to see it). The membership matrix (columns with name `p*`)
is inferred by
[`clue::cl_consensus()`](https://www.rdocumentation.org/link/cl_consensus?package=clue)
function with the `SE` method. Basically the value in the membership matrix
represents the probability to belong to a certain group. The finall class
label for an item is determined with the group with highest probability it
belongs to.

In `get_classes()` function, the entropy is calculated from the membership
matrix and the silhouette score is calculated from the consensus matrix.



<script>
$( function() {
	$( '#tabs-SD-mclust-get-classes' ).tabs();
} );
</script>
<div id='tabs-SD-mclust-get-classes'>
<ul>
<li><a href='#tab-SD-mclust-get-classes-1'>k = 2</a></li>
<li><a href='#tab-SD-mclust-get-classes-2'>k = 3</a></li>
<li><a href='#tab-SD-mclust-get-classes-3'>k = 4</a></li>
<li><a href='#tab-SD-mclust-get-classes-4'>k = 5</a></li>
<li><a href='#tab-SD-mclust-get-classes-5'>k = 6</a></li>
</ul>

<div id='tab-SD-mclust-get-classes-1'>
<p><a id='tab-SD-mclust-get-classes-1-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 2), get_membership(res, k = 2))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2
#&gt; SRR1383358     2  0.2043      0.959 0.032 0.968
#&gt; SRR1383360     2  0.4161      0.939 0.084 0.916
#&gt; SRR1383359     2  0.2043      0.959 0.032 0.968
#&gt; SRR1383362     1  0.0938      0.991 0.988 0.012
#&gt; SRR1383361     2  0.0000      0.960 0.000 1.000
#&gt; SRR1383363     2  0.1414      0.960 0.020 0.980
#&gt; SRR1383364     2  0.2043      0.959 0.032 0.968
#&gt; SRR1383365     2  0.2043      0.959 0.032 0.968
#&gt; SRR1383366     2  0.0000      0.960 0.000 1.000
#&gt; SRR1383367     2  0.0000      0.960 0.000 1.000
#&gt; SRR1383368     2  0.3584      0.947 0.068 0.932
#&gt; SRR1383369     2  0.2043      0.959 0.032 0.968
#&gt; SRR1383370     2  0.0000      0.960 0.000 1.000
#&gt; SRR1383371     2  0.2043      0.959 0.032 0.968
#&gt; SRR1383372     2  0.0000      0.960 0.000 1.000
#&gt; SRR1383373     2  0.0000      0.960 0.000 1.000
#&gt; SRR1383374     2  0.0376      0.961 0.004 0.996
#&gt; SRR1383375     1  0.0000      0.994 1.000 0.000
#&gt; SRR1383376     2  0.0000      0.960 0.000 1.000
#&gt; SRR1383377     2  0.4562      0.935 0.096 0.904
#&gt; SRR1383378     2  0.3431      0.949 0.064 0.936
#&gt; SRR1383379     2  0.4161      0.939 0.084 0.916
#&gt; SRR1383380     2  0.4562      0.935 0.096 0.904
#&gt; SRR1383381     2  0.2043      0.959 0.032 0.968
#&gt; SRR1383382     1  0.0938      0.991 0.988 0.012
#&gt; SRR1383383     2  0.1414      0.960 0.020 0.980
#&gt; SRR1383385     1  0.0000      0.994 1.000 0.000
#&gt; SRR1383384     2  0.0000      0.960 0.000 1.000
#&gt; SRR1383386     2  0.9170      0.586 0.332 0.668
#&gt; SRR1383387     2  0.3431      0.942 0.064 0.936
#&gt; SRR1383389     2  0.0000      0.960 0.000 1.000
#&gt; SRR1383391     2  0.0000      0.960 0.000 1.000
#&gt; SRR1383388     2  0.4161      0.939 0.084 0.916
#&gt; SRR1383392     2  0.0000      0.960 0.000 1.000
#&gt; SRR1383390     2  0.0000      0.960 0.000 1.000
#&gt; SRR1383394     2  0.0000      0.960 0.000 1.000
#&gt; SRR1383393     1  0.0000      0.994 1.000 0.000
#&gt; SRR1383396     2  0.4161      0.939 0.084 0.916
#&gt; SRR1383395     2  0.4562      0.935 0.096 0.904
#&gt; SRR1383399     2  0.2043      0.959 0.032 0.968
#&gt; SRR1383400     1  0.0938      0.991 0.988 0.012
#&gt; SRR1383397     2  0.4562      0.935 0.096 0.904
#&gt; SRR1383401     2  0.1843      0.959 0.028 0.972
#&gt; SRR1383398     2  0.4562      0.935 0.096 0.904
#&gt; SRR1383402     2  0.0000      0.960 0.000 1.000
#&gt; SRR1383404     2  0.4161      0.939 0.084 0.916
#&gt; SRR1383403     1  0.0000      0.994 1.000 0.000
#&gt; SRR1383405     2  0.3431      0.942 0.064 0.936
#&gt; SRR1383406     2  0.4161      0.939 0.084 0.916
#&gt; SRR1383407     2  0.0000      0.960 0.000 1.000
#&gt; SRR1383408     2  0.0000      0.960 0.000 1.000
#&gt; SRR1383409     2  0.0000      0.960 0.000 1.000
#&gt; SRR1383410     2  0.0000      0.960 0.000 1.000
</code></pre>

<script>
$('#tab-SD-mclust-get-classes-1-a').parent().next().next().hide();
$('#tab-SD-mclust-get-classes-1-a').click(function(){
  $('#tab-SD-mclust-get-classes-1-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-SD-mclust-get-classes-2'>
<p><a id='tab-SD-mclust-get-classes-2-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 3), get_membership(res, k = 3))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3
#&gt; SRR1383358     3  0.2625     0.7896 0.000 0.084 0.916
#&gt; SRR1383360     2  0.5938     0.6131 0.020 0.732 0.248
#&gt; SRR1383359     3  0.1411     0.7964 0.000 0.036 0.964
#&gt; SRR1383362     1  0.1399     0.9667 0.968 0.004 0.028
#&gt; SRR1383361     3  0.6309    -0.0826 0.000 0.496 0.504
#&gt; SRR1383363     3  0.5465     0.5563 0.000 0.288 0.712
#&gt; SRR1383364     3  0.0592     0.7897 0.012 0.000 0.988
#&gt; SRR1383365     3  0.3267     0.7712 0.000 0.116 0.884
#&gt; SRR1383366     2  0.5835     0.5811 0.000 0.660 0.340
#&gt; SRR1383367     2  0.6026     0.4430 0.000 0.624 0.376
#&gt; SRR1383368     2  0.7016     0.6648 0.156 0.728 0.116
#&gt; SRR1383369     3  0.0661     0.7919 0.008 0.004 0.988
#&gt; SRR1383370     2  0.5835     0.5249 0.000 0.660 0.340
#&gt; SRR1383371     3  0.0592     0.7897 0.012 0.000 0.988
#&gt; SRR1383372     2  0.5988     0.4677 0.000 0.632 0.368
#&gt; SRR1383373     3  0.5706     0.5228 0.000 0.320 0.680
#&gt; SRR1383374     2  0.5835     0.5305 0.000 0.660 0.340
#&gt; SRR1383375     1  0.1289     0.9668 0.968 0.000 0.032
#&gt; SRR1383376     2  0.2625     0.7595 0.000 0.916 0.084
#&gt; SRR1383377     2  0.8513     0.4732 0.140 0.596 0.264
#&gt; SRR1383378     2  0.4172     0.7304 0.104 0.868 0.028
#&gt; SRR1383379     2  0.5267     0.7096 0.140 0.816 0.044
#&gt; SRR1383380     2  0.8513     0.4732 0.140 0.596 0.264
#&gt; SRR1383381     3  0.0592     0.7897 0.012 0.000 0.988
#&gt; SRR1383382     1  0.1399     0.9667 0.968 0.004 0.028
#&gt; SRR1383383     2  0.3340     0.7505 0.000 0.880 0.120
#&gt; SRR1383385     1  0.2711     0.9578 0.912 0.000 0.088
#&gt; SRR1383384     2  0.2625     0.7595 0.000 0.916 0.084
#&gt; SRR1383386     2  0.5508     0.6796 0.188 0.784 0.028
#&gt; SRR1383387     2  0.2806     0.7493 0.032 0.928 0.040
#&gt; SRR1383389     2  0.4654     0.7033 0.000 0.792 0.208
#&gt; SRR1383391     2  0.2625     0.7595 0.000 0.916 0.084
#&gt; SRR1383388     2  0.4469     0.7239 0.120 0.852 0.028
#&gt; SRR1383392     2  0.2959     0.7528 0.000 0.900 0.100
#&gt; SRR1383390     2  0.2625     0.7595 0.000 0.916 0.084
#&gt; SRR1383394     2  0.2625     0.7595 0.000 0.916 0.084
#&gt; SRR1383393     1  0.2711     0.9578 0.912 0.000 0.088
#&gt; SRR1383396     2  0.4469     0.7239 0.120 0.852 0.028
#&gt; SRR1383395     2  0.8513     0.4732 0.140 0.596 0.264
#&gt; SRR1383399     3  0.0592     0.7897 0.012 0.000 0.988
#&gt; SRR1383400     1  0.1399     0.9667 0.968 0.004 0.028
#&gt; SRR1383397     2  0.7613     0.5628 0.116 0.680 0.204
#&gt; SRR1383401     2  0.3816     0.7481 0.000 0.852 0.148
#&gt; SRR1383398     2  0.8513     0.4732 0.140 0.596 0.264
#&gt; SRR1383402     2  0.2625     0.7595 0.000 0.916 0.084
#&gt; SRR1383404     2  0.4469     0.7239 0.120 0.852 0.028
#&gt; SRR1383403     1  0.2711     0.9578 0.912 0.000 0.088
#&gt; SRR1383405     2  0.4217     0.7289 0.032 0.868 0.100
#&gt; SRR1383406     2  0.4345     0.7219 0.136 0.848 0.016
#&gt; SRR1383407     2  0.5591     0.5880 0.000 0.696 0.304
#&gt; SRR1383408     2  0.2625     0.7595 0.000 0.916 0.084
#&gt; SRR1383409     2  0.2625     0.7595 0.000 0.916 0.084
#&gt; SRR1383410     2  0.2625     0.7595 0.000 0.916 0.084
</code></pre>

<script>
$('#tab-SD-mclust-get-classes-2-a').parent().next().next().hide();
$('#tab-SD-mclust-get-classes-2-a').click(function(){
  $('#tab-SD-mclust-get-classes-2-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-SD-mclust-get-classes-3'>
<p><a id='tab-SD-mclust-get-classes-3-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 4), get_membership(res, k = 4))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4
#&gt; SRR1383358     3  0.0921     0.7704 0.000 0.028 0.972 0.000
#&gt; SRR1383360     2  0.8007     0.2379 0.016 0.480 0.224 0.280
#&gt; SRR1383359     3  0.1059     0.7734 0.000 0.016 0.972 0.012
#&gt; SRR1383362     1  0.2799     0.8807 0.884 0.008 0.000 0.108
#&gt; SRR1383361     3  0.5838     0.2313 0.000 0.444 0.524 0.032
#&gt; SRR1383363     3  0.5339     0.3727 0.000 0.384 0.600 0.016
#&gt; SRR1383364     3  0.0469     0.7682 0.000 0.000 0.988 0.012
#&gt; SRR1383365     3  0.1488     0.7700 0.000 0.032 0.956 0.012
#&gt; SRR1383366     3  0.6395    -0.1497 0.000 0.464 0.472 0.064
#&gt; SRR1383367     2  0.5862    -0.2124 0.000 0.484 0.484 0.032
#&gt; SRR1383368     2  0.8047     0.2582 0.024 0.500 0.208 0.268
#&gt; SRR1383369     3  0.1174     0.7731 0.000 0.020 0.968 0.012
#&gt; SRR1383370     2  0.5746     0.0437 0.000 0.572 0.396 0.032
#&gt; SRR1383371     3  0.0469     0.7682 0.000 0.000 0.988 0.012
#&gt; SRR1383372     2  0.5615    -0.0640 0.004 0.556 0.424 0.016
#&gt; SRR1383373     3  0.5300     0.3492 0.000 0.408 0.580 0.012
#&gt; SRR1383374     2  0.4748     0.3376 0.000 0.716 0.268 0.016
#&gt; SRR1383375     1  0.2868     0.9080 0.864 0.000 0.000 0.136
#&gt; SRR1383376     2  0.4667     0.4340 0.000 0.796 0.108 0.096
#&gt; SRR1383377     4  0.6311     0.3589 0.004 0.456 0.048 0.492
#&gt; SRR1383378     2  0.4313     0.2450 0.004 0.736 0.000 0.260
#&gt; SRR1383379     4  0.4795     0.7603 0.000 0.292 0.012 0.696
#&gt; SRR1383380     4  0.3402     0.7107 0.004 0.164 0.000 0.832
#&gt; SRR1383381     3  0.0469     0.7698 0.000 0.000 0.988 0.012
#&gt; SRR1383382     1  0.2469     0.8851 0.892 0.000 0.000 0.108
#&gt; SRR1383383     2  0.2469     0.5244 0.000 0.892 0.108 0.000
#&gt; SRR1383385     1  0.2704     0.9101 0.876 0.000 0.000 0.124
#&gt; SRR1383384     2  0.2611     0.5154 0.000 0.896 0.096 0.008
#&gt; SRR1383386     2  0.5131     0.1583 0.028 0.692 0.000 0.280
#&gt; SRR1383387     2  0.6332    -0.3728 0.000 0.532 0.064 0.404
#&gt; SRR1383389     2  0.1913     0.5089 0.000 0.940 0.040 0.020
#&gt; SRR1383391     2  0.0000     0.5014 0.000 1.000 0.000 0.000
#&gt; SRR1383388     4  0.5510     0.4370 0.016 0.480 0.000 0.504
#&gt; SRR1383392     2  0.5356     0.3919 0.000 0.728 0.200 0.072
#&gt; SRR1383390     2  0.0336     0.5056 0.000 0.992 0.008 0.000
#&gt; SRR1383394     2  0.4786     0.4303 0.000 0.788 0.108 0.104
#&gt; SRR1383393     1  0.2868     0.9080 0.864 0.000 0.000 0.136
#&gt; SRR1383396     2  0.4551     0.2238 0.004 0.724 0.004 0.268
#&gt; SRR1383395     2  0.5336    -0.4530 0.004 0.500 0.004 0.492
#&gt; SRR1383399     3  0.0469     0.7698 0.000 0.000 0.988 0.012
#&gt; SRR1383400     1  0.2469     0.8851 0.892 0.000 0.000 0.108
#&gt; SRR1383397     4  0.4857     0.7399 0.000 0.324 0.008 0.668
#&gt; SRR1383401     2  0.5233     0.3453 0.000 0.648 0.332 0.020
#&gt; SRR1383398     4  0.3402     0.7107 0.004 0.164 0.000 0.832
#&gt; SRR1383402     2  0.4669     0.4352 0.000 0.796 0.104 0.100
#&gt; SRR1383404     2  0.4908     0.1488 0.016 0.692 0.000 0.292
#&gt; SRR1383403     1  0.2704     0.9101 0.876 0.000 0.000 0.124
#&gt; SRR1383405     2  0.6102    -0.3867 0.000 0.532 0.048 0.420
#&gt; SRR1383406     4  0.4795     0.7603 0.000 0.292 0.012 0.696
#&gt; SRR1383407     2  0.5364     0.1933 0.000 0.652 0.320 0.028
#&gt; SRR1383408     2  0.1637     0.5229 0.000 0.940 0.060 0.000
#&gt; SRR1383409     2  0.1637     0.5229 0.000 0.940 0.060 0.000
#&gt; SRR1383410     2  0.5371     0.3935 0.000 0.732 0.188 0.080
</code></pre>

<script>
$('#tab-SD-mclust-get-classes-3-a').parent().next().next().hide();
$('#tab-SD-mclust-get-classes-3-a').click(function(){
  $('#tab-SD-mclust-get-classes-3-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-SD-mclust-get-classes-4'>
<p><a id='tab-SD-mclust-get-classes-4-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 5), get_membership(res, k = 5))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4    p5
#&gt; SRR1383358     5  0.2824     0.7818 0.000 0.032 0.096 0.000 0.872
#&gt; SRR1383360     3  0.9019     0.4844 0.112 0.208 0.432 0.132 0.116
#&gt; SRR1383359     5  0.2535     0.7830 0.000 0.032 0.076 0.000 0.892
#&gt; SRR1383362     1  0.0000     0.7782 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1383361     3  0.6761    -0.2516 0.000 0.268 0.380 0.000 0.352
#&gt; SRR1383363     5  0.6422     0.3496 0.000 0.180 0.360 0.000 0.460
#&gt; SRR1383364     5  0.0771     0.7732 0.000 0.004 0.020 0.000 0.976
#&gt; SRR1383365     5  0.2974     0.7620 0.000 0.052 0.080 0.000 0.868
#&gt; SRR1383366     2  0.6449     0.4526 0.000 0.640 0.112 0.088 0.160
#&gt; SRR1383367     3  0.7008    -0.0934 0.000 0.348 0.372 0.008 0.272
#&gt; SRR1383368     3  0.8933     0.4908 0.116 0.236 0.428 0.124 0.096
#&gt; SRR1383369     5  0.0000     0.7782 0.000 0.000 0.000 0.000 1.000
#&gt; SRR1383370     2  0.6650     0.1620 0.000 0.456 0.360 0.008 0.176
#&gt; SRR1383371     5  0.0609     0.7715 0.000 0.000 0.020 0.000 0.980
#&gt; SRR1383372     2  0.7729     0.1145 0.000 0.428 0.228 0.072 0.272
#&gt; SRR1383373     5  0.5664     0.4719 0.000 0.200 0.168 0.000 0.632
#&gt; SRR1383374     2  0.6808     0.4183 0.000 0.576 0.236 0.068 0.120
#&gt; SRR1383375     1  0.6183     0.8191 0.596 0.012 0.164 0.228 0.000
#&gt; SRR1383376     2  0.0404     0.6313 0.000 0.988 0.012 0.000 0.000
#&gt; SRR1383377     4  0.5184     0.6450 0.000 0.260 0.008 0.668 0.064
#&gt; SRR1383378     3  0.6504     0.4167 0.008 0.292 0.520 0.180 0.000
#&gt; SRR1383379     4  0.3855     0.7343 0.004 0.240 0.000 0.748 0.008
#&gt; SRR1383380     4  0.1671     0.6821 0.000 0.076 0.000 0.924 0.000
#&gt; SRR1383381     5  0.3492     0.7285 0.000 0.016 0.188 0.000 0.796
#&gt; SRR1383382     1  0.0000     0.7782 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1383383     2  0.2127     0.6567 0.000 0.892 0.108 0.000 0.000
#&gt; SRR1383385     1  0.5856     0.8249 0.604 0.000 0.172 0.224 0.000
#&gt; SRR1383384     2  0.0162     0.6382 0.000 0.996 0.004 0.000 0.000
#&gt; SRR1383386     3  0.8069     0.3604 0.152 0.216 0.436 0.196 0.000
#&gt; SRR1383387     2  0.4900    -0.2782 0.000 0.512 0.000 0.464 0.024
#&gt; SRR1383389     2  0.6118     0.4909 0.000 0.620 0.256 0.080 0.044
#&gt; SRR1383391     2  0.2798     0.6478 0.000 0.852 0.140 0.008 0.000
#&gt; SRR1383388     4  0.7996    -0.2145 0.096 0.212 0.324 0.368 0.000
#&gt; SRR1383392     2  0.3011     0.6059 0.000 0.876 0.012 0.076 0.036
#&gt; SRR1383390     2  0.2230     0.6536 0.000 0.884 0.116 0.000 0.000
#&gt; SRR1383394     2  0.1942     0.6241 0.000 0.920 0.012 0.068 0.000
#&gt; SRR1383393     1  0.6663     0.8111 0.576 0.012 0.164 0.232 0.016
#&gt; SRR1383396     3  0.7648     0.4211 0.084 0.272 0.460 0.184 0.000
#&gt; SRR1383395     4  0.4492     0.6549 0.000 0.296 0.004 0.680 0.020
#&gt; SRR1383399     5  0.3132     0.7422 0.000 0.008 0.172 0.000 0.820
#&gt; SRR1383400     1  0.0000     0.7782 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1383397     4  0.3366     0.7386 0.000 0.232 0.000 0.768 0.000
#&gt; SRR1383401     2  0.5449     0.6112 0.000 0.724 0.136 0.076 0.064
#&gt; SRR1383398     4  0.1671     0.6821 0.000 0.076 0.000 0.924 0.000
#&gt; SRR1383402     2  0.0566     0.6325 0.000 0.984 0.012 0.004 0.000
#&gt; SRR1383404     3  0.7964     0.3270 0.116 0.216 0.436 0.232 0.000
#&gt; SRR1383403     1  0.5856     0.8249 0.604 0.000 0.172 0.224 0.000
#&gt; SRR1383405     2  0.4562    -0.3511 0.000 0.496 0.000 0.496 0.008
#&gt; SRR1383406     4  0.3855     0.7343 0.004 0.240 0.000 0.748 0.008
#&gt; SRR1383407     2  0.6590     0.2156 0.000 0.476 0.360 0.012 0.152
#&gt; SRR1383408     2  0.2230     0.6554 0.000 0.884 0.116 0.000 0.000
#&gt; SRR1383409     2  0.2127     0.6555 0.000 0.892 0.108 0.000 0.000
#&gt; SRR1383410     2  0.3011     0.6059 0.000 0.876 0.012 0.076 0.036
</code></pre>

<script>
$('#tab-SD-mclust-get-classes-4-a').parent().next().next().hide();
$('#tab-SD-mclust-get-classes-4-a').click(function(){
  $('#tab-SD-mclust-get-classes-4-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-SD-mclust-get-classes-5'>
<p><a id='tab-SD-mclust-get-classes-5-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 6), get_membership(res, k = 6))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4    p5    p6
#&gt; SRR1383358     5  0.4286      0.742 0.012 0.012 0.352 0.000 0.624 0.000
#&gt; SRR1383360     1  0.4863      0.588 0.612 0.004 0.324 0.056 0.004 0.000
#&gt; SRR1383359     5  0.3566      0.740 0.004 0.012 0.220 0.004 0.760 0.000
#&gt; SRR1383362     6  0.0458      1.000 0.016 0.000 0.000 0.000 0.000 0.984
#&gt; SRR1383361     3  0.1501      0.690 0.000 0.000 0.924 0.000 0.076 0.000
#&gt; SRR1383363     3  0.3632      0.286 0.012 0.012 0.756 0.000 0.220 0.000
#&gt; SRR1383364     5  0.1556      0.707 0.000 0.000 0.080 0.000 0.920 0.000
#&gt; SRR1383365     5  0.4394      0.626 0.012 0.012 0.392 0.000 0.584 0.000
#&gt; SRR1383366     3  0.4287      0.583 0.000 0.156 0.748 0.084 0.012 0.000
#&gt; SRR1383367     3  0.0363      0.761 0.000 0.000 0.988 0.000 0.012 0.000
#&gt; SRR1383368     1  0.5011      0.617 0.616 0.000 0.308 0.064 0.004 0.008
#&gt; SRR1383369     5  0.3672      0.773 0.008 0.000 0.276 0.004 0.712 0.000
#&gt; SRR1383370     3  0.0458      0.772 0.000 0.016 0.984 0.000 0.000 0.000
#&gt; SRR1383371     5  0.1556      0.707 0.000 0.000 0.080 0.000 0.920 0.000
#&gt; SRR1383372     3  0.1500      0.762 0.000 0.000 0.936 0.052 0.012 0.000
#&gt; SRR1383373     3  0.3531      0.167 0.000 0.000 0.672 0.000 0.328 0.000
#&gt; SRR1383374     3  0.3292      0.658 0.000 0.120 0.824 0.052 0.004 0.000
#&gt; SRR1383375     2  0.8189     -0.431 0.104 0.332 0.000 0.168 0.080 0.316
#&gt; SRR1383376     2  0.3927      0.511 0.000 0.644 0.344 0.012 0.000 0.000
#&gt; SRR1383377     4  0.4543      0.684 0.000 0.224 0.080 0.692 0.004 0.000
#&gt; SRR1383378     1  0.3308      0.794 0.836 0.012 0.088 0.064 0.000 0.000
#&gt; SRR1383379     4  0.4286      0.667 0.108 0.148 0.000 0.740 0.000 0.004
#&gt; SRR1383380     4  0.0000      0.629 0.000 0.000 0.000 1.000 0.000 0.000
#&gt; SRR1383381     5  0.3817      0.676 0.000 0.000 0.432 0.000 0.568 0.000
#&gt; SRR1383382     6  0.0458      1.000 0.016 0.000 0.000 0.000 0.000 0.984
#&gt; SRR1383383     2  0.4109      0.479 0.012 0.576 0.412 0.000 0.000 0.000
#&gt; SRR1383385     2  0.8208     -0.437 0.124 0.332 0.000 0.144 0.080 0.320
#&gt; SRR1383384     2  0.3747      0.501 0.000 0.604 0.396 0.000 0.000 0.000
#&gt; SRR1383386     1  0.3161      0.791 0.864 0.016 0.036 0.064 0.000 0.020
#&gt; SRR1383387     4  0.5057      0.475 0.016 0.472 0.032 0.476 0.000 0.004
#&gt; SRR1383389     3  0.3430      0.660 0.012 0.096 0.832 0.056 0.004 0.000
#&gt; SRR1383391     2  0.4335      0.437 0.000 0.508 0.472 0.020 0.000 0.000
#&gt; SRR1383388     1  0.4642      0.589 0.680 0.056 0.004 0.252 0.000 0.008
#&gt; SRR1383392     2  0.5239      0.479 0.000 0.560 0.348 0.084 0.008 0.000
#&gt; SRR1383390     2  0.3823      0.482 0.000 0.564 0.436 0.000 0.000 0.000
#&gt; SRR1383394     2  0.4433      0.508 0.000 0.616 0.344 0.040 0.000 0.000
#&gt; SRR1383393     2  0.8189     -0.431 0.104 0.332 0.000 0.168 0.080 0.316
#&gt; SRR1383396     1  0.3487      0.798 0.836 0.024 0.056 0.080 0.000 0.004
#&gt; SRR1383395     4  0.4226      0.690 0.000 0.264 0.040 0.692 0.004 0.000
#&gt; SRR1383399     5  0.3774      0.708 0.000 0.000 0.408 0.000 0.592 0.000
#&gt; SRR1383400     6  0.0458      1.000 0.016 0.000 0.000 0.000 0.000 0.984
#&gt; SRR1383397     4  0.2806      0.718 0.016 0.136 0.000 0.844 0.000 0.004
#&gt; SRR1383401     2  0.5595      0.427 0.012 0.488 0.416 0.076 0.008 0.000
#&gt; SRR1383398     4  0.0000      0.629 0.000 0.000 0.000 1.000 0.000 0.000
#&gt; SRR1383402     2  0.4193      0.513 0.000 0.624 0.352 0.024 0.000 0.000
#&gt; SRR1383404     1  0.3109      0.795 0.864 0.016 0.040 0.068 0.000 0.012
#&gt; SRR1383403     2  0.8208     -0.437 0.124 0.332 0.000 0.144 0.080 0.320
#&gt; SRR1383405     4  0.4995      0.483 0.016 0.472 0.028 0.480 0.000 0.004
#&gt; SRR1383406     4  0.3663      0.712 0.040 0.180 0.000 0.776 0.000 0.004
#&gt; SRR1383407     3  0.0458      0.772 0.000 0.016 0.984 0.000 0.000 0.000
#&gt; SRR1383408     2  0.3810      0.487 0.000 0.572 0.428 0.000 0.000 0.000
#&gt; SRR1383409     2  0.3823      0.482 0.000 0.564 0.436 0.000 0.000 0.000
#&gt; SRR1383410     2  0.5126      0.483 0.000 0.568 0.344 0.084 0.004 0.000
</code></pre>

<script>
$('#tab-SD-mclust-get-classes-5-a').parent().next().next().hide();
$('#tab-SD-mclust-get-classes-5-a').click(function(){
  $('#tab-SD-mclust-get-classes-5-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>
</div>

Heatmaps for the consensus matrix. It visualizes the probability of two
samples to be in a same group.



<script>
$( function() {
	$( '#tabs-SD-mclust-consensus-heatmap' ).tabs();
} );
</script>
<div id='tabs-SD-mclust-consensus-heatmap'>
<ul>
<li><a href='#tab-SD-mclust-consensus-heatmap-1'>k = 2</a></li>
<li><a href='#tab-SD-mclust-consensus-heatmap-2'>k = 3</a></li>
<li><a href='#tab-SD-mclust-consensus-heatmap-3'>k = 4</a></li>
<li><a href='#tab-SD-mclust-consensus-heatmap-4'>k = 5</a></li>
<li><a href='#tab-SD-mclust-consensus-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-SD-mclust-consensus-heatmap-1'>
<pre><code class="r">consensus_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-SD-mclust-consensus-heatmap-1-1.png" alt="plot of chunk tab-SD-mclust-consensus-heatmap-1"/></p>

</div>
<div id='tab-SD-mclust-consensus-heatmap-2'>
<pre><code class="r">consensus_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-SD-mclust-consensus-heatmap-2-1.png" alt="plot of chunk tab-SD-mclust-consensus-heatmap-2"/></p>

</div>
<div id='tab-SD-mclust-consensus-heatmap-3'>
<pre><code class="r">consensus_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-SD-mclust-consensus-heatmap-3-1.png" alt="plot of chunk tab-SD-mclust-consensus-heatmap-3"/></p>

</div>
<div id='tab-SD-mclust-consensus-heatmap-4'>
<pre><code class="r">consensus_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-SD-mclust-consensus-heatmap-4-1.png" alt="plot of chunk tab-SD-mclust-consensus-heatmap-4"/></p>

</div>
<div id='tab-SD-mclust-consensus-heatmap-5'>
<pre><code class="r">consensus_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-SD-mclust-consensus-heatmap-5-1.png" alt="plot of chunk tab-SD-mclust-consensus-heatmap-5"/></p>

</div>
</div>

Heatmaps for the membership of samples in all partitions to see how consistent they are:




<script>
$( function() {
	$( '#tabs-SD-mclust-membership-heatmap' ).tabs();
} );
</script>
<div id='tabs-SD-mclust-membership-heatmap'>
<ul>
<li><a href='#tab-SD-mclust-membership-heatmap-1'>k = 2</a></li>
<li><a href='#tab-SD-mclust-membership-heatmap-2'>k = 3</a></li>
<li><a href='#tab-SD-mclust-membership-heatmap-3'>k = 4</a></li>
<li><a href='#tab-SD-mclust-membership-heatmap-4'>k = 5</a></li>
<li><a href='#tab-SD-mclust-membership-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-SD-mclust-membership-heatmap-1'>
<pre><code class="r">membership_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-SD-mclust-membership-heatmap-1-1.png" alt="plot of chunk tab-SD-mclust-membership-heatmap-1"/></p>

</div>
<div id='tab-SD-mclust-membership-heatmap-2'>
<pre><code class="r">membership_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-SD-mclust-membership-heatmap-2-1.png" alt="plot of chunk tab-SD-mclust-membership-heatmap-2"/></p>

</div>
<div id='tab-SD-mclust-membership-heatmap-3'>
<pre><code class="r">membership_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-SD-mclust-membership-heatmap-3-1.png" alt="plot of chunk tab-SD-mclust-membership-heatmap-3"/></p>

</div>
<div id='tab-SD-mclust-membership-heatmap-4'>
<pre><code class="r">membership_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-SD-mclust-membership-heatmap-4-1.png" alt="plot of chunk tab-SD-mclust-membership-heatmap-4"/></p>

</div>
<div id='tab-SD-mclust-membership-heatmap-5'>
<pre><code class="r">membership_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-SD-mclust-membership-heatmap-5-1.png" alt="plot of chunk tab-SD-mclust-membership-heatmap-5"/></p>

</div>
</div>

As soon as we have had the classes for columns, we can look for signatures
which are significantly different between classes which can be candidate marks
for certain classes. Following are the heatmaps for signatures.



Signature heatmaps where rows are scaled:



<script>
$( function() {
	$( '#tabs-SD-mclust-get-signatures' ).tabs();
} );
</script>
<div id='tabs-SD-mclust-get-signatures'>
<ul>
<li><a href='#tab-SD-mclust-get-signatures-1'>k = 2</a></li>
<li><a href='#tab-SD-mclust-get-signatures-2'>k = 3</a></li>
<li><a href='#tab-SD-mclust-get-signatures-3'>k = 4</a></li>
<li><a href='#tab-SD-mclust-get-signatures-4'>k = 5</a></li>
<li><a href='#tab-SD-mclust-get-signatures-5'>k = 6</a></li>
</ul>
<div id='tab-SD-mclust-get-signatures-1'>
<pre><code class="r">get_signatures(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-SD-mclust-get-signatures-1-1.png" alt="plot of chunk tab-SD-mclust-get-signatures-1"/></p>

</div>
<div id='tab-SD-mclust-get-signatures-2'>
<pre><code class="r">get_signatures(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-SD-mclust-get-signatures-2-1.png" alt="plot of chunk tab-SD-mclust-get-signatures-2"/></p>

</div>
<div id='tab-SD-mclust-get-signatures-3'>
<pre><code class="r">get_signatures(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-SD-mclust-get-signatures-3-1.png" alt="plot of chunk tab-SD-mclust-get-signatures-3"/></p>

</div>
<div id='tab-SD-mclust-get-signatures-4'>
<pre><code class="r">get_signatures(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-SD-mclust-get-signatures-4-1.png" alt="plot of chunk tab-SD-mclust-get-signatures-4"/></p>

</div>
<div id='tab-SD-mclust-get-signatures-5'>
<pre><code class="r">get_signatures(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-SD-mclust-get-signatures-5-1.png" alt="plot of chunk tab-SD-mclust-get-signatures-5"/></p>

</div>
</div>



Signature heatmaps where rows are not scaled:


<script>
$( function() {
	$( '#tabs-SD-mclust-get-signatures-no-scale' ).tabs();
} );
</script>
<div id='tabs-SD-mclust-get-signatures-no-scale'>
<ul>
<li><a href='#tab-SD-mclust-get-signatures-no-scale-1'>k = 2</a></li>
<li><a href='#tab-SD-mclust-get-signatures-no-scale-2'>k = 3</a></li>
<li><a href='#tab-SD-mclust-get-signatures-no-scale-3'>k = 4</a></li>
<li><a href='#tab-SD-mclust-get-signatures-no-scale-4'>k = 5</a></li>
<li><a href='#tab-SD-mclust-get-signatures-no-scale-5'>k = 6</a></li>
</ul>
<div id='tab-SD-mclust-get-signatures-no-scale-1'>
<pre><code class="r">get_signatures(res, k = 2, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-SD-mclust-get-signatures-no-scale-1-1.png" alt="plot of chunk tab-SD-mclust-get-signatures-no-scale-1"/></p>

</div>
<div id='tab-SD-mclust-get-signatures-no-scale-2'>
<pre><code class="r">get_signatures(res, k = 3, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-SD-mclust-get-signatures-no-scale-2-1.png" alt="plot of chunk tab-SD-mclust-get-signatures-no-scale-2"/></p>

</div>
<div id='tab-SD-mclust-get-signatures-no-scale-3'>
<pre><code class="r">get_signatures(res, k = 4, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-SD-mclust-get-signatures-no-scale-3-1.png" alt="plot of chunk tab-SD-mclust-get-signatures-no-scale-3"/></p>

</div>
<div id='tab-SD-mclust-get-signatures-no-scale-4'>
<pre><code class="r">get_signatures(res, k = 5, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-SD-mclust-get-signatures-no-scale-4-1.png" alt="plot of chunk tab-SD-mclust-get-signatures-no-scale-4"/></p>

</div>
<div id='tab-SD-mclust-get-signatures-no-scale-5'>
<pre><code class="r">get_signatures(res, k = 6, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-SD-mclust-get-signatures-no-scale-5-1.png" alt="plot of chunk tab-SD-mclust-get-signatures-no-scale-5"/></p>

</div>
</div>



Compare the overlap of signatures from different k:

```r
compare_signatures(res)
```

![plot of chunk SD-mclust-signature_compare](figure_cola/SD-mclust-signature_compare-1.png)

`get_signature()` returns a data frame invisibly. TO get the list of signatures, the function
call should be assigned to a variable explicitly. In following code, if `plot` argument is set
to `FALSE`, no heatmap is plotted while only the differential analysis is performed.

```r
# code only for demonstration
tb = get_signature(res, k = ..., plot = FALSE)
```

An example of the output of `tb` is:

```
#>   which_row         fdr    mean_1    mean_2 scaled_mean_1 scaled_mean_2 km
#> 1        38 0.042760348  8.373488  9.131774    -0.5533452     0.5164555  1
#> 2        40 0.018707592  7.106213  8.469186    -0.6173731     0.5762149  1
#> 3        55 0.019134737 10.221463 11.207825    -0.6159697     0.5749050  1
#> 4        59 0.006059896  5.921854  7.869574    -0.6899429     0.6439467  1
#> 5        60 0.018055526  8.928898 10.211722    -0.6204761     0.5791110  1
#> 6        98 0.009384629 15.714769 14.887706     0.6635654    -0.6193277  2
...
```

The columns in `tb` are:

1. `which_row`: row indices corresponding to the input matrix.
2. `fdr`: FDR for the differential test. 
3. `mean_x`: The mean value in group x.
4. `scaled_mean_x`: The mean value in group x after rows are scaled.
5. `km`: Row groups if k-means clustering is applied to rows.



UMAP plot which shows how samples are separated.


<script>
$( function() {
	$( '#tabs-SD-mclust-dimension-reduction' ).tabs();
} );
</script>
<div id='tabs-SD-mclust-dimension-reduction'>
<ul>
<li><a href='#tab-SD-mclust-dimension-reduction-1'>k = 2</a></li>
<li><a href='#tab-SD-mclust-dimension-reduction-2'>k = 3</a></li>
<li><a href='#tab-SD-mclust-dimension-reduction-3'>k = 4</a></li>
<li><a href='#tab-SD-mclust-dimension-reduction-4'>k = 5</a></li>
<li><a href='#tab-SD-mclust-dimension-reduction-5'>k = 6</a></li>
</ul>
<div id='tab-SD-mclust-dimension-reduction-1'>
<pre><code class="r">dimension_reduction(res, k = 2, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-SD-mclust-dimension-reduction-1-1.png" alt="plot of chunk tab-SD-mclust-dimension-reduction-1"/></p>

</div>
<div id='tab-SD-mclust-dimension-reduction-2'>
<pre><code class="r">dimension_reduction(res, k = 3, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-SD-mclust-dimension-reduction-2-1.png" alt="plot of chunk tab-SD-mclust-dimension-reduction-2"/></p>

</div>
<div id='tab-SD-mclust-dimension-reduction-3'>
<pre><code class="r">dimension_reduction(res, k = 4, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-SD-mclust-dimension-reduction-3-1.png" alt="plot of chunk tab-SD-mclust-dimension-reduction-3"/></p>

</div>
<div id='tab-SD-mclust-dimension-reduction-4'>
<pre><code class="r">dimension_reduction(res, k = 5, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-SD-mclust-dimension-reduction-4-1.png" alt="plot of chunk tab-SD-mclust-dimension-reduction-4"/></p>

</div>
<div id='tab-SD-mclust-dimension-reduction-5'>
<pre><code class="r">dimension_reduction(res, k = 6, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-SD-mclust-dimension-reduction-5-1.png" alt="plot of chunk tab-SD-mclust-dimension-reduction-5"/></p>

</div>
</div>


Following heatmap shows how subgroups are split when increasing `k`:

```r
collect_classes(res)
```

![plot of chunk SD-mclust-collect-classes](figure_cola/SD-mclust-collect-classes-1.png)


If matrix rows can be associated to genes, consider to use `functional_enrichment(res,
...)` to perform function enrichment for the signature genes. See [this vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/functional_enrichment.html) for more detailed explanations.


 

---------------------------------------------------




### SD:NMF**






The object with results only for a single top-value method and a single partition method 
can be extracted as:

```r
res = res_list["SD", "NMF"]
# you can also extract it by
# res = res_list["SD:NMF"]
```

A summary of `res` and all the functions that can be applied to it:

```r
res
```

```
#> A 'ConsensusPartition' object with k = 2, 3, 4, 5, 6.
#>   On a matrix with 15680 rows and 53 columns.
#>   Top rows (1000, 2000, 3000, 4000, 5000) are extracted by 'SD' method.
#>   Subgroups are detected by 'NMF' method.
#>   Performed in total 1250 partitions by row resampling.
#>   Best k for subgroups seems to be 2.
#> 
#> Following methods can be applied to this 'ConsensusPartition' object:
#>  [1] "cola_report"             "collect_classes"         "collect_plots"          
#>  [4] "collect_stats"           "colnames"                "compare_signatures"     
#>  [7] "consensus_heatmap"       "dimension_reduction"     "functional_enrichment"  
#> [10] "get_anno_col"            "get_anno"                "get_classes"            
#> [13] "get_consensus"           "get_matrix"              "get_membership"         
#> [16] "get_param"               "get_signatures"          "get_stats"              
#> [19] "is_best_k"               "is_stable_k"             "membership_heatmap"     
#> [22] "ncol"                    "nrow"                    "plot_ecdf"              
#> [25] "rownames"                "select_partition_number" "show"                   
#> [28] "suggest_best_k"          "test_to_known_factors"
```

`collect_plots()` function collects all the plots made from `res` for all `k` (number of partitions)
into one single page to provide an easy and fast comparison between different `k`.

```r
collect_plots(res)
```

![plot of chunk SD-NMF-collect-plots](figure_cola/SD-NMF-collect-plots-1.png)

The plots are:

- The first row: a plot of the ECDF (empirical cumulative distribution
  function) curves of the consensus matrix for each `k` and the heatmap of
  predicted classes for each `k`.
- The second row: heatmaps of the consensus matrix for each `k`.
- The third row: heatmaps of the membership matrix for each `k`.
- The fouth row: heatmaps of the signatures for each `k`.

All the plots in panels can be made by individual functions and they are
plotted later in this section.

`select_partition_number()` produces several plots showing different
statistics for choosing "optimized" `k`. There are following statistics:

- ECDF curves of the consensus matrix for each `k`;
- 1-PAC. [The PAC
  score](https://en.wikipedia.org/wiki/Consensus_clustering#Over-interpretation_potential_of_consensus_clustering)
  measures the proportion of the ambiguous subgrouping.
- Mean silhouette score.
- Concordance. The mean probability of fiting the consensus class ids in all
  partitions.
- Area increased. Denote $A_k$ as the area under the ECDF curve for current
  `k`, the area increased is defined as $A_k - A_{k-1}$.
- Rand index. The percent of pairs of samples that are both in a same cluster
  or both are not in a same cluster in the partition of k and k-1.
- Jaccard index. The ratio of pairs of samples are both in a same cluster in
  the partition of k and k-1 and the pairs of samples are both in a same
  cluster in the partition k or k-1.

The detailed explanations of these statistics can be found in [the _cola_
vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/cola.html#toc_13).

Generally speaking, lower PAC score, higher mean silhouette score or higher
concordance corresponds to better partition. Rand index and Jaccard index
measure how similar the current partition is compared to partition with `k-1`.
If they are too similar, we won't accept `k` is better than `k-1`.

```r
select_partition_number(res)
```

![plot of chunk SD-NMF-select-partition-number](figure_cola/SD-NMF-select-partition-number-1.png)

The numeric values for all these statistics can be obtained by `get_stats()`.

```r
get_stats(res)
```

```
#>   k 1-PAC mean_silhouette concordance area_increased  Rand Jaccard
#> 2 2 1.000           0.956       0.981         0.4061 0.586   0.586
#> 3 3 0.808           0.855       0.941         0.6075 0.669   0.476
#> 4 4 0.649           0.700       0.848         0.1092 0.838   0.584
#> 5 5 0.828           0.876       0.932         0.0901 0.885   0.611
#> 6 6 0.718           0.591       0.799         0.0395 0.904   0.599
```

`suggest_best_k()` suggests the best $k$ based on these statistics. The rules are as follows:

- All $k$ with Jaccard index larger than 0.95 are removed because increasing
  $k$ does not provide enough extra information. If all $k$ are removed, it is
  marked as no subgroup is detected.
- For all $k$ with 1-PAC score larger than 0.9, the maximal $k$ is taken as
  the best $k$, and other $k$ are marked as optional $k$.
- If it does not fit the second rule. The $k$ with the maximal vote of the
  highest 1-PAC score, highest mean silhouette, and highest concordance is
  taken as the best $k$.

```r
suggest_best_k(res)
```

```
#> [1] 2
```


Following shows the table of the partitions (You need to click the **show/hide
code output** link to see it). The membership matrix (columns with name `p*`)
is inferred by
[`clue::cl_consensus()`](https://www.rdocumentation.org/link/cl_consensus?package=clue)
function with the `SE` method. Basically the value in the membership matrix
represents the probability to belong to a certain group. The finall class
label for an item is determined with the group with highest probability it
belongs to.

In `get_classes()` function, the entropy is calculated from the membership
matrix and the silhouette score is calculated from the consensus matrix.



<script>
$( function() {
	$( '#tabs-SD-NMF-get-classes' ).tabs();
} );
</script>
<div id='tabs-SD-NMF-get-classes'>
<ul>
<li><a href='#tab-SD-NMF-get-classes-1'>k = 2</a></li>
<li><a href='#tab-SD-NMF-get-classes-2'>k = 3</a></li>
<li><a href='#tab-SD-NMF-get-classes-3'>k = 4</a></li>
<li><a href='#tab-SD-NMF-get-classes-4'>k = 5</a></li>
<li><a href='#tab-SD-NMF-get-classes-5'>k = 6</a></li>
</ul>

<div id='tab-SD-NMF-get-classes-1'>
<p><a id='tab-SD-NMF-get-classes-1-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 2), get_membership(res, k = 2))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2
#&gt; SRR1383358     2  0.0000      0.992 0.000 1.000
#&gt; SRR1383360     1  0.8713      0.609 0.708 0.292
#&gt; SRR1383359     2  0.0000      0.992 0.000 1.000
#&gt; SRR1383362     1  0.0000      0.948 1.000 0.000
#&gt; SRR1383361     2  0.0000      0.992 0.000 1.000
#&gt; SRR1383363     2  0.0000      0.992 0.000 1.000
#&gt; SRR1383364     2  0.0000      0.992 0.000 1.000
#&gt; SRR1383365     2  0.0000      0.992 0.000 1.000
#&gt; SRR1383366     2  0.0000      0.992 0.000 1.000
#&gt; SRR1383367     2  0.0000      0.992 0.000 1.000
#&gt; SRR1383368     1  0.0938      0.942 0.988 0.012
#&gt; SRR1383369     2  0.0000      0.992 0.000 1.000
#&gt; SRR1383370     2  0.0000      0.992 0.000 1.000
#&gt; SRR1383371     2  0.0000      0.992 0.000 1.000
#&gt; SRR1383372     2  0.0000      0.992 0.000 1.000
#&gt; SRR1383373     2  0.0000      0.992 0.000 1.000
#&gt; SRR1383374     2  0.0000      0.992 0.000 1.000
#&gt; SRR1383375     1  0.0000      0.948 1.000 0.000
#&gt; SRR1383376     2  0.0000      0.992 0.000 1.000
#&gt; SRR1383377     2  0.0000      0.992 0.000 1.000
#&gt; SRR1383378     2  0.8267      0.621 0.260 0.740
#&gt; SRR1383379     2  0.1633      0.967 0.024 0.976
#&gt; SRR1383380     1  0.3114      0.910 0.944 0.056
#&gt; SRR1383381     2  0.0000      0.992 0.000 1.000
#&gt; SRR1383382     1  0.0000      0.948 1.000 0.000
#&gt; SRR1383383     2  0.0000      0.992 0.000 1.000
#&gt; SRR1383385     1  0.0000      0.948 1.000 0.000
#&gt; SRR1383384     2  0.0000      0.992 0.000 1.000
#&gt; SRR1383386     1  0.0000      0.948 1.000 0.000
#&gt; SRR1383387     2  0.0000      0.992 0.000 1.000
#&gt; SRR1383389     2  0.0000      0.992 0.000 1.000
#&gt; SRR1383391     2  0.0000      0.992 0.000 1.000
#&gt; SRR1383388     1  0.0000      0.948 1.000 0.000
#&gt; SRR1383392     2  0.0000      0.992 0.000 1.000
#&gt; SRR1383390     2  0.0000      0.992 0.000 1.000
#&gt; SRR1383394     2  0.0000      0.992 0.000 1.000
#&gt; SRR1383393     1  0.0000      0.948 1.000 0.000
#&gt; SRR1383396     1  0.1414      0.937 0.980 0.020
#&gt; SRR1383395     2  0.0000      0.992 0.000 1.000
#&gt; SRR1383399     2  0.0000      0.992 0.000 1.000
#&gt; SRR1383400     1  0.0000      0.948 1.000 0.000
#&gt; SRR1383397     2  0.0000      0.992 0.000 1.000
#&gt; SRR1383401     2  0.0000      0.992 0.000 1.000
#&gt; SRR1383398     1  0.9209      0.521 0.664 0.336
#&gt; SRR1383402     2  0.0000      0.992 0.000 1.000
#&gt; SRR1383404     1  0.0000      0.948 1.000 0.000
#&gt; SRR1383403     1  0.0000      0.948 1.000 0.000
#&gt; SRR1383405     2  0.0000      0.992 0.000 1.000
#&gt; SRR1383406     2  0.0000      0.992 0.000 1.000
#&gt; SRR1383407     2  0.0000      0.992 0.000 1.000
#&gt; SRR1383408     2  0.0000      0.992 0.000 1.000
#&gt; SRR1383409     2  0.0000      0.992 0.000 1.000
#&gt; SRR1383410     2  0.0000      0.992 0.000 1.000
</code></pre>

<script>
$('#tab-SD-NMF-get-classes-1-a').parent().next().next().hide();
$('#tab-SD-NMF-get-classes-1-a').click(function(){
  $('#tab-SD-NMF-get-classes-1-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-SD-NMF-get-classes-2'>
<p><a id='tab-SD-NMF-get-classes-2-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 3), get_membership(res, k = 3))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3
#&gt; SRR1383358     3  0.0000     0.9327 0.000 0.000 1.000
#&gt; SRR1383360     1  0.5070     0.6931 0.772 0.004 0.224
#&gt; SRR1383359     3  0.0000     0.9327 0.000 0.000 1.000
#&gt; SRR1383362     1  0.0000     0.9496 1.000 0.000 0.000
#&gt; SRR1383361     3  0.0000     0.9327 0.000 0.000 1.000
#&gt; SRR1383363     3  0.0000     0.9327 0.000 0.000 1.000
#&gt; SRR1383364     3  0.0000     0.9327 0.000 0.000 1.000
#&gt; SRR1383365     3  0.0000     0.9327 0.000 0.000 1.000
#&gt; SRR1383366     2  0.5968     0.3959 0.000 0.636 0.364
#&gt; SRR1383367     3  0.0000     0.9327 0.000 0.000 1.000
#&gt; SRR1383368     1  0.0000     0.9496 1.000 0.000 0.000
#&gt; SRR1383369     3  0.0000     0.9327 0.000 0.000 1.000
#&gt; SRR1383370     3  0.4887     0.6899 0.000 0.228 0.772
#&gt; SRR1383371     3  0.0000     0.9327 0.000 0.000 1.000
#&gt; SRR1383372     3  0.0000     0.9327 0.000 0.000 1.000
#&gt; SRR1383373     3  0.0000     0.9327 0.000 0.000 1.000
#&gt; SRR1383374     3  0.2878     0.8568 0.000 0.096 0.904
#&gt; SRR1383375     1  0.0000     0.9496 1.000 0.000 0.000
#&gt; SRR1383376     2  0.0000     0.9191 0.000 1.000 0.000
#&gt; SRR1383377     2  0.1163     0.9075 0.000 0.972 0.028
#&gt; SRR1383378     2  0.6193     0.5515 0.292 0.692 0.016
#&gt; SRR1383379     2  0.0000     0.9191 0.000 1.000 0.000
#&gt; SRR1383380     2  0.3619     0.8035 0.136 0.864 0.000
#&gt; SRR1383381     3  0.0000     0.9327 0.000 0.000 1.000
#&gt; SRR1383382     1  0.0000     0.9496 1.000 0.000 0.000
#&gt; SRR1383383     2  0.5058     0.6611 0.000 0.756 0.244
#&gt; SRR1383385     1  0.0000     0.9496 1.000 0.000 0.000
#&gt; SRR1383384     2  0.0237     0.9194 0.000 0.996 0.004
#&gt; SRR1383386     1  0.0000     0.9496 1.000 0.000 0.000
#&gt; SRR1383387     2  0.0000     0.9191 0.000 1.000 0.000
#&gt; SRR1383389     2  0.6295     0.0996 0.000 0.528 0.472
#&gt; SRR1383391     2  0.0424     0.9186 0.000 0.992 0.008
#&gt; SRR1383388     2  0.0747     0.9133 0.016 0.984 0.000
#&gt; SRR1383392     2  0.0237     0.9194 0.000 0.996 0.004
#&gt; SRR1383390     2  0.1163     0.9092 0.000 0.972 0.028
#&gt; SRR1383394     2  0.0000     0.9191 0.000 1.000 0.000
#&gt; SRR1383393     1  0.0000     0.9496 1.000 0.000 0.000
#&gt; SRR1383396     1  0.0000     0.9496 1.000 0.000 0.000
#&gt; SRR1383395     2  0.0424     0.9179 0.000 0.992 0.008
#&gt; SRR1383399     3  0.0000     0.9327 0.000 0.000 1.000
#&gt; SRR1383400     1  0.0000     0.9496 1.000 0.000 0.000
#&gt; SRR1383397     2  0.0000     0.9191 0.000 1.000 0.000
#&gt; SRR1383401     3  0.6252     0.1356 0.000 0.444 0.556
#&gt; SRR1383398     2  0.1643     0.8925 0.044 0.956 0.000
#&gt; SRR1383402     2  0.0237     0.9194 0.000 0.996 0.004
#&gt; SRR1383404     1  0.5397     0.5767 0.720 0.280 0.000
#&gt; SRR1383403     1  0.0000     0.9496 1.000 0.000 0.000
#&gt; SRR1383405     2  0.0000     0.9191 0.000 1.000 0.000
#&gt; SRR1383406     2  0.0000     0.9191 0.000 1.000 0.000
#&gt; SRR1383407     3  0.3412     0.8326 0.000 0.124 0.876
#&gt; SRR1383408     2  0.0747     0.9156 0.000 0.984 0.016
#&gt; SRR1383409     2  0.0892     0.9137 0.000 0.980 0.020
#&gt; SRR1383410     2  0.0237     0.9194 0.000 0.996 0.004
</code></pre>

<script>
$('#tab-SD-NMF-get-classes-2-a').parent().next().next().hide();
$('#tab-SD-NMF-get-classes-2-a').click(function(){
  $('#tab-SD-NMF-get-classes-2-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-SD-NMF-get-classes-3'>
<p><a id='tab-SD-NMF-get-classes-3-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 4), get_membership(res, k = 4))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4
#&gt; SRR1383358     3  0.0000      0.804 0.000 0.000 1.000 0.000
#&gt; SRR1383360     1  0.5573      0.166 0.528 0.008 0.456 0.008
#&gt; SRR1383359     3  0.0188      0.805 0.000 0.004 0.996 0.000
#&gt; SRR1383362     1  0.3356      0.730 0.824 0.000 0.000 0.176
#&gt; SRR1383361     3  0.1118      0.801 0.000 0.036 0.964 0.000
#&gt; SRR1383363     3  0.0376      0.806 0.004 0.004 0.992 0.000
#&gt; SRR1383364     3  0.3172      0.759 0.160 0.000 0.840 0.000
#&gt; SRR1383365     3  0.0188      0.805 0.000 0.004 0.996 0.000
#&gt; SRR1383366     3  0.5497      0.195 0.000 0.460 0.524 0.016
#&gt; SRR1383367     3  0.1389      0.796 0.000 0.048 0.952 0.000
#&gt; SRR1383368     1  0.4071      0.712 0.832 0.000 0.064 0.104
#&gt; SRR1383369     3  0.0336      0.804 0.008 0.000 0.992 0.000
#&gt; SRR1383370     3  0.3975      0.643 0.000 0.240 0.760 0.000
#&gt; SRR1383371     3  0.2921      0.769 0.140 0.000 0.860 0.000
#&gt; SRR1383372     3  0.3399      0.786 0.092 0.040 0.868 0.000
#&gt; SRR1383373     3  0.0592      0.805 0.000 0.016 0.984 0.000
#&gt; SRR1383374     3  0.5143      0.237 0.004 0.456 0.540 0.000
#&gt; SRR1383375     4  0.1716      0.737 0.064 0.000 0.000 0.936
#&gt; SRR1383376     2  0.0188      0.872 0.000 0.996 0.000 0.004
#&gt; SRR1383377     4  0.4957      0.590 0.000 0.320 0.012 0.668
#&gt; SRR1383378     1  0.4624      0.389 0.660 0.340 0.000 0.000
#&gt; SRR1383379     2  0.3219      0.755 0.000 0.836 0.000 0.164
#&gt; SRR1383380     4  0.2469      0.777 0.000 0.108 0.000 0.892
#&gt; SRR1383381     3  0.3836      0.748 0.168 0.000 0.816 0.016
#&gt; SRR1383382     1  0.3311      0.731 0.828 0.000 0.000 0.172
#&gt; SRR1383383     2  0.5280      0.666 0.156 0.748 0.096 0.000
#&gt; SRR1383385     4  0.0921      0.771 0.028 0.000 0.000 0.972
#&gt; SRR1383384     2  0.0188      0.872 0.004 0.996 0.000 0.000
#&gt; SRR1383386     1  0.3356      0.730 0.824 0.000 0.000 0.176
#&gt; SRR1383387     2  0.0921      0.866 0.000 0.972 0.000 0.028
#&gt; SRR1383389     2  0.5999      0.302 0.404 0.552 0.044 0.000
#&gt; SRR1383391     2  0.0592      0.869 0.016 0.984 0.000 0.000
#&gt; SRR1383388     2  0.1635      0.857 0.008 0.948 0.000 0.044
#&gt; SRR1383392     2  0.0469      0.871 0.000 0.988 0.000 0.012
#&gt; SRR1383390     2  0.1978      0.836 0.068 0.928 0.004 0.000
#&gt; SRR1383394     2  0.0336      0.872 0.000 0.992 0.000 0.008
#&gt; SRR1383393     4  0.0921      0.771 0.028 0.000 0.000 0.972
#&gt; SRR1383396     1  0.3250      0.655 0.888 0.016 0.024 0.072
#&gt; SRR1383395     4  0.4914      0.608 0.000 0.312 0.012 0.676
#&gt; SRR1383399     3  0.3836      0.748 0.168 0.000 0.816 0.016
#&gt; SRR1383400     1  0.3311      0.731 0.828 0.000 0.000 0.172
#&gt; SRR1383397     2  0.4331      0.540 0.000 0.712 0.000 0.288
#&gt; SRR1383401     2  0.6936      0.338 0.144 0.564 0.292 0.000
#&gt; SRR1383398     4  0.2921      0.764 0.000 0.140 0.000 0.860
#&gt; SRR1383402     2  0.0000      0.872 0.000 1.000 0.000 0.000
#&gt; SRR1383404     1  0.7313      0.358 0.464 0.380 0.000 0.156
#&gt; SRR1383403     4  0.0921      0.771 0.028 0.000 0.000 0.972
#&gt; SRR1383405     2  0.0921      0.866 0.000 0.972 0.000 0.028
#&gt; SRR1383406     2  0.3356      0.732 0.000 0.824 0.000 0.176
#&gt; SRR1383407     3  0.7426      0.229 0.168 0.416 0.416 0.000
#&gt; SRR1383408     2  0.0817      0.865 0.024 0.976 0.000 0.000
#&gt; SRR1383409     2  0.0188      0.872 0.004 0.996 0.000 0.000
#&gt; SRR1383410     2  0.0469      0.871 0.000 0.988 0.000 0.012
</code></pre>

<script>
$('#tab-SD-NMF-get-classes-3-a').parent().next().next().hide();
$('#tab-SD-NMF-get-classes-3-a').click(function(){
  $('#tab-SD-NMF-get-classes-3-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-SD-NMF-get-classes-4'>
<p><a id='tab-SD-NMF-get-classes-4-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 5), get_membership(res, k = 5))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4    p5
#&gt; SRR1383358     3  0.0404      0.953 0.000 0.000 0.988 0.000 0.012
#&gt; SRR1383360     3  0.2536      0.842 0.128 0.004 0.868 0.000 0.000
#&gt; SRR1383359     3  0.0290      0.954 0.000 0.000 0.992 0.000 0.008
#&gt; SRR1383362     1  0.0404      0.873 0.988 0.000 0.000 0.012 0.000
#&gt; SRR1383361     3  0.0000      0.953 0.000 0.000 1.000 0.000 0.000
#&gt; SRR1383363     3  0.0404      0.953 0.000 0.000 0.988 0.000 0.012
#&gt; SRR1383364     5  0.1124      0.893 0.000 0.000 0.036 0.004 0.960
#&gt; SRR1383365     3  0.0290      0.954 0.000 0.000 0.992 0.000 0.008
#&gt; SRR1383366     3  0.0880      0.936 0.000 0.032 0.968 0.000 0.000
#&gt; SRR1383367     3  0.0000      0.953 0.000 0.000 1.000 0.000 0.000
#&gt; SRR1383368     1  0.2127      0.804 0.892 0.000 0.108 0.000 0.000
#&gt; SRR1383369     3  0.2074      0.882 0.000 0.000 0.896 0.000 0.104
#&gt; SRR1383370     3  0.0290      0.950 0.000 0.008 0.992 0.000 0.000
#&gt; SRR1383371     5  0.1341      0.880 0.000 0.000 0.056 0.000 0.944
#&gt; SRR1383372     3  0.1018      0.945 0.000 0.016 0.968 0.000 0.016
#&gt; SRR1383373     3  0.0290      0.954 0.000 0.000 0.992 0.000 0.008
#&gt; SRR1383374     3  0.2773      0.775 0.000 0.164 0.836 0.000 0.000
#&gt; SRR1383375     4  0.1571      0.864 0.060 0.000 0.000 0.936 0.004
#&gt; SRR1383376     2  0.0693      0.927 0.000 0.980 0.000 0.008 0.012
#&gt; SRR1383377     4  0.3762      0.677 0.000 0.244 0.004 0.748 0.004
#&gt; SRR1383378     1  0.4197      0.728 0.776 0.148 0.000 0.000 0.076
#&gt; SRR1383379     2  0.2488      0.858 0.000 0.872 0.004 0.124 0.000
#&gt; SRR1383380     4  0.0290      0.880 0.000 0.008 0.000 0.992 0.000
#&gt; SRR1383381     5  0.0566      0.907 0.000 0.000 0.004 0.012 0.984
#&gt; SRR1383382     1  0.0000      0.875 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1383383     5  0.2424      0.849 0.000 0.132 0.000 0.000 0.868
#&gt; SRR1383385     4  0.0963      0.882 0.036 0.000 0.000 0.964 0.000
#&gt; SRR1383384     2  0.0794      0.923 0.000 0.972 0.000 0.000 0.028
#&gt; SRR1383386     1  0.0290      0.874 0.992 0.000 0.000 0.008 0.000
#&gt; SRR1383387     2  0.1251      0.916 0.000 0.956 0.008 0.036 0.000
#&gt; SRR1383389     5  0.2464      0.875 0.016 0.096 0.000 0.000 0.888
#&gt; SRR1383391     2  0.1124      0.918 0.004 0.960 0.000 0.000 0.036
#&gt; SRR1383388     2  0.1117      0.920 0.016 0.964 0.000 0.020 0.000
#&gt; SRR1383392     2  0.0960      0.924 0.000 0.972 0.016 0.008 0.004
#&gt; SRR1383390     2  0.2574      0.852 0.012 0.876 0.000 0.000 0.112
#&gt; SRR1383394     2  0.0912      0.927 0.000 0.972 0.000 0.016 0.012
#&gt; SRR1383393     4  0.1041      0.882 0.032 0.000 0.000 0.964 0.004
#&gt; SRR1383396     5  0.1808      0.896 0.040 0.020 0.000 0.004 0.936
#&gt; SRR1383395     4  0.3366      0.726 0.000 0.212 0.004 0.784 0.000
#&gt; SRR1383399     5  0.0566      0.907 0.000 0.000 0.004 0.012 0.984
#&gt; SRR1383400     1  0.0000      0.875 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1383397     2  0.3928      0.596 0.000 0.700 0.004 0.296 0.000
#&gt; SRR1383401     5  0.0609      0.907 0.000 0.020 0.000 0.000 0.980
#&gt; SRR1383398     4  0.0404      0.879 0.000 0.012 0.000 0.988 0.000
#&gt; SRR1383402     2  0.0955      0.924 0.000 0.968 0.000 0.004 0.028
#&gt; SRR1383404     1  0.3967      0.644 0.724 0.264 0.000 0.012 0.000
#&gt; SRR1383403     4  0.0963      0.882 0.036 0.000 0.000 0.964 0.000
#&gt; SRR1383405     2  0.1251      0.916 0.000 0.956 0.008 0.036 0.000
#&gt; SRR1383406     2  0.2516      0.843 0.000 0.860 0.000 0.140 0.000
#&gt; SRR1383407     5  0.3086      0.788 0.004 0.180 0.000 0.000 0.816
#&gt; SRR1383408     2  0.1608      0.898 0.000 0.928 0.000 0.000 0.072
#&gt; SRR1383409     2  0.1043      0.918 0.000 0.960 0.000 0.000 0.040
#&gt; SRR1383410     2  0.0727      0.926 0.000 0.980 0.004 0.012 0.004
</code></pre>

<script>
$('#tab-SD-NMF-get-classes-4-a').parent().next().next().hide();
$('#tab-SD-NMF-get-classes-4-a').click(function(){
  $('#tab-SD-NMF-get-classes-4-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-SD-NMF-get-classes-5'>
<p><a id='tab-SD-NMF-get-classes-5-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 6), get_membership(res, k = 6))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4    p5    p6
#&gt; SRR1383358     3  0.0777     0.8705 0.000 0.004 0.972 0.000 0.024 0.000
#&gt; SRR1383360     3  0.4844     0.6353 0.000 0.200 0.680 0.008 0.000 0.112
#&gt; SRR1383359     3  0.1082     0.8681 0.000 0.040 0.956 0.000 0.004 0.000
#&gt; SRR1383362     6  0.0146     0.8927 0.004 0.000 0.000 0.000 0.000 0.996
#&gt; SRR1383361     3  0.0937     0.8718 0.000 0.040 0.960 0.000 0.000 0.000
#&gt; SRR1383363     3  0.1334     0.8732 0.000 0.032 0.948 0.000 0.020 0.000
#&gt; SRR1383364     5  0.1480     0.7521 0.000 0.040 0.020 0.000 0.940 0.000
#&gt; SRR1383365     3  0.1010     0.8694 0.000 0.036 0.960 0.000 0.004 0.000
#&gt; SRR1383366     3  0.0632     0.8724 0.000 0.000 0.976 0.024 0.000 0.000
#&gt; SRR1383367     3  0.0909     0.8716 0.000 0.012 0.968 0.020 0.000 0.000
#&gt; SRR1383368     6  0.3536     0.6282 0.000 0.008 0.252 0.004 0.000 0.736
#&gt; SRR1383369     3  0.4838     0.3677 0.000 0.064 0.564 0.000 0.372 0.000
#&gt; SRR1383370     3  0.0622     0.8739 0.000 0.008 0.980 0.012 0.000 0.000
#&gt; SRR1383371     5  0.1644     0.7497 0.000 0.040 0.028 0.000 0.932 0.000
#&gt; SRR1383372     3  0.2743     0.8052 0.000 0.164 0.828 0.000 0.008 0.000
#&gt; SRR1383373     3  0.1010     0.8725 0.000 0.036 0.960 0.000 0.004 0.000
#&gt; SRR1383374     3  0.4514     0.6194 0.000 0.244 0.684 0.068 0.004 0.000
#&gt; SRR1383375     1  0.3895     0.7673 0.800 0.032 0.000 0.000 0.060 0.108
#&gt; SRR1383376     4  0.2454     0.5353 0.000 0.160 0.000 0.840 0.000 0.000
#&gt; SRR1383377     2  0.6106     0.0793 0.236 0.420 0.004 0.340 0.000 0.000
#&gt; SRR1383378     2  0.6721     0.1794 0.000 0.464 0.000 0.292 0.068 0.176
#&gt; SRR1383379     4  0.1141     0.5973 0.052 0.000 0.000 0.948 0.000 0.000
#&gt; SRR1383380     1  0.2510     0.8385 0.872 0.028 0.000 0.100 0.000 0.000
#&gt; SRR1383381     5  0.1082     0.7670 0.000 0.040 0.004 0.000 0.956 0.000
#&gt; SRR1383382     6  0.0000     0.8935 0.000 0.000 0.000 0.000 0.000 1.000
#&gt; SRR1383383     5  0.4855     0.3939 0.000 0.380 0.000 0.064 0.556 0.000
#&gt; SRR1383385     1  0.0458     0.8787 0.984 0.000 0.000 0.000 0.000 0.016
#&gt; SRR1383384     4  0.3482     0.3304 0.000 0.316 0.000 0.684 0.000 0.000
#&gt; SRR1383386     6  0.1657     0.8522 0.016 0.000 0.000 0.056 0.000 0.928
#&gt; SRR1383387     4  0.0547     0.5988 0.000 0.020 0.000 0.980 0.000 0.000
#&gt; SRR1383389     2  0.3420     0.1465 0.000 0.776 0.000 0.012 0.204 0.008
#&gt; SRR1383391     4  0.3547     0.3561 0.000 0.332 0.000 0.668 0.000 0.000
#&gt; SRR1383388     4  0.3689     0.5143 0.048 0.152 0.004 0.792 0.004 0.000
#&gt; SRR1383392     2  0.4488     0.2006 0.000 0.548 0.032 0.420 0.000 0.000
#&gt; SRR1383390     2  0.5009     0.1710 0.000 0.536 0.000 0.388 0.076 0.000
#&gt; SRR1383394     4  0.1814     0.5781 0.000 0.100 0.000 0.900 0.000 0.000
#&gt; SRR1383393     1  0.1944     0.8620 0.924 0.016 0.000 0.000 0.024 0.036
#&gt; SRR1383396     5  0.4791     0.5534 0.052 0.328 0.000 0.000 0.612 0.008
#&gt; SRR1383395     4  0.6082    -0.1934 0.272 0.360 0.000 0.368 0.000 0.000
#&gt; SRR1383399     5  0.1082     0.7683 0.000 0.040 0.004 0.000 0.956 0.000
#&gt; SRR1383400     6  0.0000     0.8935 0.000 0.000 0.000 0.000 0.000 1.000
#&gt; SRR1383397     4  0.2630     0.5481 0.064 0.064 0.000 0.872 0.000 0.000
#&gt; SRR1383401     5  0.3950     0.6138 0.000 0.276 0.000 0.028 0.696 0.000
#&gt; SRR1383398     1  0.3193     0.8021 0.824 0.052 0.000 0.124 0.000 0.000
#&gt; SRR1383402     4  0.3101     0.4625 0.000 0.244 0.000 0.756 0.000 0.000
#&gt; SRR1383404     4  0.5194     0.2732 0.060 0.016 0.000 0.596 0.004 0.324
#&gt; SRR1383403     1  0.0146     0.8783 0.996 0.004 0.000 0.000 0.000 0.000
#&gt; SRR1383405     4  0.1863     0.5551 0.000 0.104 0.000 0.896 0.000 0.000
#&gt; SRR1383406     4  0.3564     0.4895 0.196 0.020 0.004 0.776 0.004 0.000
#&gt; SRR1383407     2  0.3457     0.3071 0.000 0.808 0.004 0.052 0.136 0.000
#&gt; SRR1383408     2  0.4407    -0.0338 0.000 0.496 0.000 0.480 0.024 0.000
#&gt; SRR1383409     4  0.3198     0.4589 0.000 0.260 0.000 0.740 0.000 0.000
#&gt; SRR1383410     2  0.3991     0.1332 0.000 0.524 0.004 0.472 0.000 0.000
</code></pre>

<script>
$('#tab-SD-NMF-get-classes-5-a').parent().next().next().hide();
$('#tab-SD-NMF-get-classes-5-a').click(function(){
  $('#tab-SD-NMF-get-classes-5-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>
</div>

Heatmaps for the consensus matrix. It visualizes the probability of two
samples to be in a same group.



<script>
$( function() {
	$( '#tabs-SD-NMF-consensus-heatmap' ).tabs();
} );
</script>
<div id='tabs-SD-NMF-consensus-heatmap'>
<ul>
<li><a href='#tab-SD-NMF-consensus-heatmap-1'>k = 2</a></li>
<li><a href='#tab-SD-NMF-consensus-heatmap-2'>k = 3</a></li>
<li><a href='#tab-SD-NMF-consensus-heatmap-3'>k = 4</a></li>
<li><a href='#tab-SD-NMF-consensus-heatmap-4'>k = 5</a></li>
<li><a href='#tab-SD-NMF-consensus-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-SD-NMF-consensus-heatmap-1'>
<pre><code class="r">consensus_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-SD-NMF-consensus-heatmap-1-1.png" alt="plot of chunk tab-SD-NMF-consensus-heatmap-1"/></p>

</div>
<div id='tab-SD-NMF-consensus-heatmap-2'>
<pre><code class="r">consensus_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-SD-NMF-consensus-heatmap-2-1.png" alt="plot of chunk tab-SD-NMF-consensus-heatmap-2"/></p>

</div>
<div id='tab-SD-NMF-consensus-heatmap-3'>
<pre><code class="r">consensus_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-SD-NMF-consensus-heatmap-3-1.png" alt="plot of chunk tab-SD-NMF-consensus-heatmap-3"/></p>

</div>
<div id='tab-SD-NMF-consensus-heatmap-4'>
<pre><code class="r">consensus_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-SD-NMF-consensus-heatmap-4-1.png" alt="plot of chunk tab-SD-NMF-consensus-heatmap-4"/></p>

</div>
<div id='tab-SD-NMF-consensus-heatmap-5'>
<pre><code class="r">consensus_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-SD-NMF-consensus-heatmap-5-1.png" alt="plot of chunk tab-SD-NMF-consensus-heatmap-5"/></p>

</div>
</div>

Heatmaps for the membership of samples in all partitions to see how consistent they are:




<script>
$( function() {
	$( '#tabs-SD-NMF-membership-heatmap' ).tabs();
} );
</script>
<div id='tabs-SD-NMF-membership-heatmap'>
<ul>
<li><a href='#tab-SD-NMF-membership-heatmap-1'>k = 2</a></li>
<li><a href='#tab-SD-NMF-membership-heatmap-2'>k = 3</a></li>
<li><a href='#tab-SD-NMF-membership-heatmap-3'>k = 4</a></li>
<li><a href='#tab-SD-NMF-membership-heatmap-4'>k = 5</a></li>
<li><a href='#tab-SD-NMF-membership-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-SD-NMF-membership-heatmap-1'>
<pre><code class="r">membership_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-SD-NMF-membership-heatmap-1-1.png" alt="plot of chunk tab-SD-NMF-membership-heatmap-1"/></p>

</div>
<div id='tab-SD-NMF-membership-heatmap-2'>
<pre><code class="r">membership_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-SD-NMF-membership-heatmap-2-1.png" alt="plot of chunk tab-SD-NMF-membership-heatmap-2"/></p>

</div>
<div id='tab-SD-NMF-membership-heatmap-3'>
<pre><code class="r">membership_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-SD-NMF-membership-heatmap-3-1.png" alt="plot of chunk tab-SD-NMF-membership-heatmap-3"/></p>

</div>
<div id='tab-SD-NMF-membership-heatmap-4'>
<pre><code class="r">membership_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-SD-NMF-membership-heatmap-4-1.png" alt="plot of chunk tab-SD-NMF-membership-heatmap-4"/></p>

</div>
<div id='tab-SD-NMF-membership-heatmap-5'>
<pre><code class="r">membership_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-SD-NMF-membership-heatmap-5-1.png" alt="plot of chunk tab-SD-NMF-membership-heatmap-5"/></p>

</div>
</div>

As soon as we have had the classes for columns, we can look for signatures
which are significantly different between classes which can be candidate marks
for certain classes. Following are the heatmaps for signatures.



Signature heatmaps where rows are scaled:



<script>
$( function() {
	$( '#tabs-SD-NMF-get-signatures' ).tabs();
} );
</script>
<div id='tabs-SD-NMF-get-signatures'>
<ul>
<li><a href='#tab-SD-NMF-get-signatures-1'>k = 2</a></li>
<li><a href='#tab-SD-NMF-get-signatures-2'>k = 3</a></li>
<li><a href='#tab-SD-NMF-get-signatures-3'>k = 4</a></li>
<li><a href='#tab-SD-NMF-get-signatures-4'>k = 5</a></li>
<li><a href='#tab-SD-NMF-get-signatures-5'>k = 6</a></li>
</ul>
<div id='tab-SD-NMF-get-signatures-1'>
<pre><code class="r">get_signatures(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-SD-NMF-get-signatures-1-1.png" alt="plot of chunk tab-SD-NMF-get-signatures-1"/></p>

</div>
<div id='tab-SD-NMF-get-signatures-2'>
<pre><code class="r">get_signatures(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-SD-NMF-get-signatures-2-1.png" alt="plot of chunk tab-SD-NMF-get-signatures-2"/></p>

</div>
<div id='tab-SD-NMF-get-signatures-3'>
<pre><code class="r">get_signatures(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-SD-NMF-get-signatures-3-1.png" alt="plot of chunk tab-SD-NMF-get-signatures-3"/></p>

</div>
<div id='tab-SD-NMF-get-signatures-4'>
<pre><code class="r">get_signatures(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-SD-NMF-get-signatures-4-1.png" alt="plot of chunk tab-SD-NMF-get-signatures-4"/></p>

</div>
<div id='tab-SD-NMF-get-signatures-5'>
<pre><code class="r">get_signatures(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-SD-NMF-get-signatures-5-1.png" alt="plot of chunk tab-SD-NMF-get-signatures-5"/></p>

</div>
</div>



Signature heatmaps where rows are not scaled:


<script>
$( function() {
	$( '#tabs-SD-NMF-get-signatures-no-scale' ).tabs();
} );
</script>
<div id='tabs-SD-NMF-get-signatures-no-scale'>
<ul>
<li><a href='#tab-SD-NMF-get-signatures-no-scale-1'>k = 2</a></li>
<li><a href='#tab-SD-NMF-get-signatures-no-scale-2'>k = 3</a></li>
<li><a href='#tab-SD-NMF-get-signatures-no-scale-3'>k = 4</a></li>
<li><a href='#tab-SD-NMF-get-signatures-no-scale-4'>k = 5</a></li>
<li><a href='#tab-SD-NMF-get-signatures-no-scale-5'>k = 6</a></li>
</ul>
<div id='tab-SD-NMF-get-signatures-no-scale-1'>
<pre><code class="r">get_signatures(res, k = 2, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-SD-NMF-get-signatures-no-scale-1-1.png" alt="plot of chunk tab-SD-NMF-get-signatures-no-scale-1"/></p>

</div>
<div id='tab-SD-NMF-get-signatures-no-scale-2'>
<pre><code class="r">get_signatures(res, k = 3, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-SD-NMF-get-signatures-no-scale-2-1.png" alt="plot of chunk tab-SD-NMF-get-signatures-no-scale-2"/></p>

</div>
<div id='tab-SD-NMF-get-signatures-no-scale-3'>
<pre><code class="r">get_signatures(res, k = 4, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-SD-NMF-get-signatures-no-scale-3-1.png" alt="plot of chunk tab-SD-NMF-get-signatures-no-scale-3"/></p>

</div>
<div id='tab-SD-NMF-get-signatures-no-scale-4'>
<pre><code class="r">get_signatures(res, k = 5, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-SD-NMF-get-signatures-no-scale-4-1.png" alt="plot of chunk tab-SD-NMF-get-signatures-no-scale-4"/></p>

</div>
<div id='tab-SD-NMF-get-signatures-no-scale-5'>
<pre><code class="r">get_signatures(res, k = 6, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-SD-NMF-get-signatures-no-scale-5-1.png" alt="plot of chunk tab-SD-NMF-get-signatures-no-scale-5"/></p>

</div>
</div>



Compare the overlap of signatures from different k:

```r
compare_signatures(res)
```

![plot of chunk SD-NMF-signature_compare](figure_cola/SD-NMF-signature_compare-1.png)

`get_signature()` returns a data frame invisibly. TO get the list of signatures, the function
call should be assigned to a variable explicitly. In following code, if `plot` argument is set
to `FALSE`, no heatmap is plotted while only the differential analysis is performed.

```r
# code only for demonstration
tb = get_signature(res, k = ..., plot = FALSE)
```

An example of the output of `tb` is:

```
#>   which_row         fdr    mean_1    mean_2 scaled_mean_1 scaled_mean_2 km
#> 1        38 0.042760348  8.373488  9.131774    -0.5533452     0.5164555  1
#> 2        40 0.018707592  7.106213  8.469186    -0.6173731     0.5762149  1
#> 3        55 0.019134737 10.221463 11.207825    -0.6159697     0.5749050  1
#> 4        59 0.006059896  5.921854  7.869574    -0.6899429     0.6439467  1
#> 5        60 0.018055526  8.928898 10.211722    -0.6204761     0.5791110  1
#> 6        98 0.009384629 15.714769 14.887706     0.6635654    -0.6193277  2
...
```

The columns in `tb` are:

1. `which_row`: row indices corresponding to the input matrix.
2. `fdr`: FDR for the differential test. 
3. `mean_x`: The mean value in group x.
4. `scaled_mean_x`: The mean value in group x after rows are scaled.
5. `km`: Row groups if k-means clustering is applied to rows.



UMAP plot which shows how samples are separated.


<script>
$( function() {
	$( '#tabs-SD-NMF-dimension-reduction' ).tabs();
} );
</script>
<div id='tabs-SD-NMF-dimension-reduction'>
<ul>
<li><a href='#tab-SD-NMF-dimension-reduction-1'>k = 2</a></li>
<li><a href='#tab-SD-NMF-dimension-reduction-2'>k = 3</a></li>
<li><a href='#tab-SD-NMF-dimension-reduction-3'>k = 4</a></li>
<li><a href='#tab-SD-NMF-dimension-reduction-4'>k = 5</a></li>
<li><a href='#tab-SD-NMF-dimension-reduction-5'>k = 6</a></li>
</ul>
<div id='tab-SD-NMF-dimension-reduction-1'>
<pre><code class="r">dimension_reduction(res, k = 2, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-SD-NMF-dimension-reduction-1-1.png" alt="plot of chunk tab-SD-NMF-dimension-reduction-1"/></p>

</div>
<div id='tab-SD-NMF-dimension-reduction-2'>
<pre><code class="r">dimension_reduction(res, k = 3, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-SD-NMF-dimension-reduction-2-1.png" alt="plot of chunk tab-SD-NMF-dimension-reduction-2"/></p>

</div>
<div id='tab-SD-NMF-dimension-reduction-3'>
<pre><code class="r">dimension_reduction(res, k = 4, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-SD-NMF-dimension-reduction-3-1.png" alt="plot of chunk tab-SD-NMF-dimension-reduction-3"/></p>

</div>
<div id='tab-SD-NMF-dimension-reduction-4'>
<pre><code class="r">dimension_reduction(res, k = 5, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-SD-NMF-dimension-reduction-4-1.png" alt="plot of chunk tab-SD-NMF-dimension-reduction-4"/></p>

</div>
<div id='tab-SD-NMF-dimension-reduction-5'>
<pre><code class="r">dimension_reduction(res, k = 6, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-SD-NMF-dimension-reduction-5-1.png" alt="plot of chunk tab-SD-NMF-dimension-reduction-5"/></p>

</div>
</div>


Following heatmap shows how subgroups are split when increasing `k`:

```r
collect_classes(res)
```

![plot of chunk SD-NMF-collect-classes](figure_cola/SD-NMF-collect-classes-1.png)


If matrix rows can be associated to genes, consider to use `functional_enrichment(res,
...)` to perform function enrichment for the signature genes. See [this vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/functional_enrichment.html) for more detailed explanations.


 

---------------------------------------------------




### CV:hclust






The object with results only for a single top-value method and a single partition method 
can be extracted as:

```r
res = res_list["CV", "hclust"]
# you can also extract it by
# res = res_list["CV:hclust"]
```

A summary of `res` and all the functions that can be applied to it:

```r
res
```

```
#> A 'ConsensusPartition' object with k = 2, 3, 4, 5, 6.
#>   On a matrix with 15680 rows and 53 columns.
#>   Top rows (1000, 2000, 3000, 4000, 5000) are extracted by 'CV' method.
#>   Subgroups are detected by 'hclust' method.
#>   Performed in total 1250 partitions by row resampling.
#>   Best k for subgroups seems to be 4.
#> 
#> Following methods can be applied to this 'ConsensusPartition' object:
#>  [1] "cola_report"             "collect_classes"         "collect_plots"          
#>  [4] "collect_stats"           "colnames"                "compare_signatures"     
#>  [7] "consensus_heatmap"       "dimension_reduction"     "functional_enrichment"  
#> [10] "get_anno_col"            "get_anno"                "get_classes"            
#> [13] "get_consensus"           "get_matrix"              "get_membership"         
#> [16] "get_param"               "get_signatures"          "get_stats"              
#> [19] "is_best_k"               "is_stable_k"             "membership_heatmap"     
#> [22] "ncol"                    "nrow"                    "plot_ecdf"              
#> [25] "rownames"                "select_partition_number" "show"                   
#> [28] "suggest_best_k"          "test_to_known_factors"
```

`collect_plots()` function collects all the plots made from `res` for all `k` (number of partitions)
into one single page to provide an easy and fast comparison between different `k`.

```r
collect_plots(res)
```

![plot of chunk CV-hclust-collect-plots](figure_cola/CV-hclust-collect-plots-1.png)

The plots are:

- The first row: a plot of the ECDF (empirical cumulative distribution
  function) curves of the consensus matrix for each `k` and the heatmap of
  predicted classes for each `k`.
- The second row: heatmaps of the consensus matrix for each `k`.
- The third row: heatmaps of the membership matrix for each `k`.
- The fouth row: heatmaps of the signatures for each `k`.

All the plots in panels can be made by individual functions and they are
plotted later in this section.

`select_partition_number()` produces several plots showing different
statistics for choosing "optimized" `k`. There are following statistics:

- ECDF curves of the consensus matrix for each `k`;
- 1-PAC. [The PAC
  score](https://en.wikipedia.org/wiki/Consensus_clustering#Over-interpretation_potential_of_consensus_clustering)
  measures the proportion of the ambiguous subgrouping.
- Mean silhouette score.
- Concordance. The mean probability of fiting the consensus class ids in all
  partitions.
- Area increased. Denote $A_k$ as the area under the ECDF curve for current
  `k`, the area increased is defined as $A_k - A_{k-1}$.
- Rand index. The percent of pairs of samples that are both in a same cluster
  or both are not in a same cluster in the partition of k and k-1.
- Jaccard index. The ratio of pairs of samples are both in a same cluster in
  the partition of k and k-1 and the pairs of samples are both in a same
  cluster in the partition k or k-1.

The detailed explanations of these statistics can be found in [the _cola_
vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/cola.html#toc_13).

Generally speaking, lower PAC score, higher mean silhouette score or higher
concordance corresponds to better partition. Rand index and Jaccard index
measure how similar the current partition is compared to partition with `k-1`.
If they are too similar, we won't accept `k` is better than `k-1`.

```r
select_partition_number(res)
```

![plot of chunk CV-hclust-select-partition-number](figure_cola/CV-hclust-select-partition-number-1.png)

The numeric values for all these statistics can be obtained by `get_stats()`.

```r
get_stats(res)
```

```
#>   k 1-PAC mean_silhouette concordance area_increased  Rand Jaccard
#> 2 2 0.637           0.855       0.943         0.2862 0.766   0.766
#> 3 3 0.708           0.802       0.933         0.3663 0.878   0.841
#> 4 4 0.390           0.591       0.785         0.6554 0.680   0.503
#> 5 5 0.498           0.496       0.744         0.0776 0.862   0.632
#> 6 6 0.510           0.456       0.731         0.0358 0.907   0.728
```

`suggest_best_k()` suggests the best $k$ based on these statistics. The rules are as follows:

- All $k$ with Jaccard index larger than 0.95 are removed because increasing
  $k$ does not provide enough extra information. If all $k$ are removed, it is
  marked as no subgroup is detected.
- For all $k$ with 1-PAC score larger than 0.9, the maximal $k$ is taken as
  the best $k$, and other $k$ are marked as optional $k$.
- If it does not fit the second rule. The $k$ with the maximal vote of the
  highest 1-PAC score, highest mean silhouette, and highest concordance is
  taken as the best $k$.

```r
suggest_best_k(res)
```

```
#> [1] 4
```


Following shows the table of the partitions (You need to click the **show/hide
code output** link to see it). The membership matrix (columns with name `p*`)
is inferred by
[`clue::cl_consensus()`](https://www.rdocumentation.org/link/cl_consensus?package=clue)
function with the `SE` method. Basically the value in the membership matrix
represents the probability to belong to a certain group. The finall class
label for an item is determined with the group with highest probability it
belongs to.

In `get_classes()` function, the entropy is calculated from the membership
matrix and the silhouette score is calculated from the consensus matrix.



<script>
$( function() {
	$( '#tabs-CV-hclust-get-classes' ).tabs();
} );
</script>
<div id='tabs-CV-hclust-get-classes'>
<ul>
<li><a href='#tab-CV-hclust-get-classes-1'>k = 2</a></li>
<li><a href='#tab-CV-hclust-get-classes-2'>k = 3</a></li>
<li><a href='#tab-CV-hclust-get-classes-3'>k = 4</a></li>
<li><a href='#tab-CV-hclust-get-classes-4'>k = 5</a></li>
<li><a href='#tab-CV-hclust-get-classes-5'>k = 6</a></li>
</ul>

<div id='tab-CV-hclust-get-classes-1'>
<p><a id='tab-CV-hclust-get-classes-1-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 2), get_membership(res, k = 2))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2
#&gt; SRR1383358     2   0.000      0.935 0.000 1.000
#&gt; SRR1383360     2   0.000      0.935 0.000 1.000
#&gt; SRR1383359     2   0.000      0.935 0.000 1.000
#&gt; SRR1383362     1   0.000      0.925 1.000 0.000
#&gt; SRR1383361     2   0.000      0.935 0.000 1.000
#&gt; SRR1383363     2   0.000      0.935 0.000 1.000
#&gt; SRR1383364     2   0.494      0.846 0.108 0.892
#&gt; SRR1383365     2   0.000      0.935 0.000 1.000
#&gt; SRR1383366     2   0.000      0.935 0.000 1.000
#&gt; SRR1383367     2   0.000      0.935 0.000 1.000
#&gt; SRR1383368     2   0.987      0.241 0.432 0.568
#&gt; SRR1383369     2   0.000      0.935 0.000 1.000
#&gt; SRR1383370     2   0.000      0.935 0.000 1.000
#&gt; SRR1383371     2   0.494      0.846 0.108 0.892
#&gt; SRR1383372     2   0.000      0.935 0.000 1.000
#&gt; SRR1383373     2   0.000      0.935 0.000 1.000
#&gt; SRR1383374     2   0.000      0.935 0.000 1.000
#&gt; SRR1383375     1   0.714      0.767 0.804 0.196
#&gt; SRR1383376     2   0.000      0.935 0.000 1.000
#&gt; SRR1383377     2   0.000      0.935 0.000 1.000
#&gt; SRR1383378     2   0.987      0.241 0.432 0.568
#&gt; SRR1383379     2   0.000      0.935 0.000 1.000
#&gt; SRR1383380     2   0.118      0.925 0.016 0.984
#&gt; SRR1383381     2   0.469      0.854 0.100 0.900
#&gt; SRR1383382     1   0.000      0.925 1.000 0.000
#&gt; SRR1383383     2   0.000      0.935 0.000 1.000
#&gt; SRR1383385     1   0.000      0.925 1.000 0.000
#&gt; SRR1383384     2   0.000      0.935 0.000 1.000
#&gt; SRR1383386     2   0.987      0.241 0.432 0.568
#&gt; SRR1383387     2   0.000      0.935 0.000 1.000
#&gt; SRR1383389     2   0.000      0.935 0.000 1.000
#&gt; SRR1383391     2   0.000      0.935 0.000 1.000
#&gt; SRR1383388     2   0.118      0.925 0.016 0.984
#&gt; SRR1383392     2   0.000      0.935 0.000 1.000
#&gt; SRR1383390     2   0.000      0.935 0.000 1.000
#&gt; SRR1383394     2   0.000      0.935 0.000 1.000
#&gt; SRR1383393     1   0.714      0.767 0.804 0.196
#&gt; SRR1383396     2   0.987      0.241 0.432 0.568
#&gt; SRR1383395     2   0.000      0.935 0.000 1.000
#&gt; SRR1383399     2   0.469      0.854 0.100 0.900
#&gt; SRR1383400     1   0.000      0.925 1.000 0.000
#&gt; SRR1383397     2   0.000      0.935 0.000 1.000
#&gt; SRR1383401     2   0.000      0.935 0.000 1.000
#&gt; SRR1383398     2   0.118      0.925 0.016 0.984
#&gt; SRR1383402     2   0.000      0.935 0.000 1.000
#&gt; SRR1383404     2   0.987      0.241 0.432 0.568
#&gt; SRR1383403     1   0.000      0.925 1.000 0.000
#&gt; SRR1383405     2   0.000      0.935 0.000 1.000
#&gt; SRR1383406     2   0.118      0.925 0.016 0.984
#&gt; SRR1383407     2   0.000      0.935 0.000 1.000
#&gt; SRR1383408     2   0.000      0.935 0.000 1.000
#&gt; SRR1383409     2   0.000      0.935 0.000 1.000
#&gt; SRR1383410     2   0.000      0.935 0.000 1.000
</code></pre>

<script>
$('#tab-CV-hclust-get-classes-1-a').parent().next().next().hide();
$('#tab-CV-hclust-get-classes-1-a').click(function(){
  $('#tab-CV-hclust-get-classes-1-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-CV-hclust-get-classes-2'>
<p><a id='tab-CV-hclust-get-classes-2-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 3), get_membership(res, k = 3))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3
#&gt; SRR1383358     2  0.0000     0.9203 0.000 1.000 0.000
#&gt; SRR1383360     2  0.0000     0.9203 0.000 1.000 0.000
#&gt; SRR1383359     2  0.0000     0.9203 0.000 1.000 0.000
#&gt; SRR1383362     1  0.0000     0.8605 1.000 0.000 0.000
#&gt; SRR1383361     2  0.0000     0.9203 0.000 1.000 0.000
#&gt; SRR1383363     2  0.0000     0.9203 0.000 1.000 0.000
#&gt; SRR1383364     3  0.0000     0.6658 0.000 0.000 1.000
#&gt; SRR1383365     2  0.0000     0.9203 0.000 1.000 0.000
#&gt; SRR1383366     2  0.0000     0.9203 0.000 1.000 0.000
#&gt; SRR1383367     2  0.0000     0.9203 0.000 1.000 0.000
#&gt; SRR1383368     2  0.6225     0.2401 0.432 0.568 0.000
#&gt; SRR1383369     2  0.6252     0.0357 0.000 0.556 0.444
#&gt; SRR1383370     2  0.0000     0.9203 0.000 1.000 0.000
#&gt; SRR1383371     3  0.0000     0.6658 0.000 0.000 1.000
#&gt; SRR1383372     2  0.0000     0.9203 0.000 1.000 0.000
#&gt; SRR1383373     2  0.0000     0.9203 0.000 1.000 0.000
#&gt; SRR1383374     2  0.0000     0.9203 0.000 1.000 0.000
#&gt; SRR1383375     1  0.4504     0.6277 0.804 0.196 0.000
#&gt; SRR1383376     2  0.0000     0.9203 0.000 1.000 0.000
#&gt; SRR1383377     2  0.0000     0.9203 0.000 1.000 0.000
#&gt; SRR1383378     2  0.6225     0.2401 0.432 0.568 0.000
#&gt; SRR1383379     2  0.0000     0.9203 0.000 1.000 0.000
#&gt; SRR1383380     2  0.0747     0.9080 0.016 0.984 0.000
#&gt; SRR1383381     3  0.5058     0.6586 0.000 0.244 0.756
#&gt; SRR1383382     1  0.0000     0.8605 1.000 0.000 0.000
#&gt; SRR1383383     2  0.0000     0.9203 0.000 1.000 0.000
#&gt; SRR1383385     1  0.0000     0.8605 1.000 0.000 0.000
#&gt; SRR1383384     2  0.0000     0.9203 0.000 1.000 0.000
#&gt; SRR1383386     2  0.6225     0.2401 0.432 0.568 0.000
#&gt; SRR1383387     2  0.0000     0.9203 0.000 1.000 0.000
#&gt; SRR1383389     2  0.0000     0.9203 0.000 1.000 0.000
#&gt; SRR1383391     2  0.0000     0.9203 0.000 1.000 0.000
#&gt; SRR1383388     2  0.0747     0.9080 0.016 0.984 0.000
#&gt; SRR1383392     2  0.0000     0.9203 0.000 1.000 0.000
#&gt; SRR1383390     2  0.0000     0.9203 0.000 1.000 0.000
#&gt; SRR1383394     2  0.0000     0.9203 0.000 1.000 0.000
#&gt; SRR1383393     1  0.4504     0.6277 0.804 0.196 0.000
#&gt; SRR1383396     2  0.6225     0.2401 0.432 0.568 0.000
#&gt; SRR1383395     2  0.0000     0.9203 0.000 1.000 0.000
#&gt; SRR1383399     3  0.5058     0.6586 0.000 0.244 0.756
#&gt; SRR1383400     1  0.0000     0.8605 1.000 0.000 0.000
#&gt; SRR1383397     2  0.0000     0.9203 0.000 1.000 0.000
#&gt; SRR1383401     2  0.0000     0.9203 0.000 1.000 0.000
#&gt; SRR1383398     2  0.0747     0.9080 0.016 0.984 0.000
#&gt; SRR1383402     2  0.0000     0.9203 0.000 1.000 0.000
#&gt; SRR1383404     2  0.6225     0.2401 0.432 0.568 0.000
#&gt; SRR1383403     1  0.0000     0.8605 1.000 0.000 0.000
#&gt; SRR1383405     2  0.0000     0.9203 0.000 1.000 0.000
#&gt; SRR1383406     2  0.0747     0.9080 0.016 0.984 0.000
#&gt; SRR1383407     2  0.0000     0.9203 0.000 1.000 0.000
#&gt; SRR1383408     2  0.0000     0.9203 0.000 1.000 0.000
#&gt; SRR1383409     2  0.0000     0.9203 0.000 1.000 0.000
#&gt; SRR1383410     2  0.0000     0.9203 0.000 1.000 0.000
</code></pre>

<script>
$('#tab-CV-hclust-get-classes-2-a').parent().next().next().hide();
$('#tab-CV-hclust-get-classes-2-a').click(function(){
  $('#tab-CV-hclust-get-classes-2-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-CV-hclust-get-classes-3'>
<p><a id='tab-CV-hclust-get-classes-3-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 4), get_membership(res, k = 4))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4
#&gt; SRR1383358     4  0.4981    -0.1188 0.000 0.464 0.000 0.536
#&gt; SRR1383360     4  0.1389     0.5736 0.000 0.048 0.000 0.952
#&gt; SRR1383359     4  0.0188     0.5275 0.000 0.004 0.000 0.996
#&gt; SRR1383362     1  0.0000     0.9014 1.000 0.000 0.000 0.000
#&gt; SRR1383361     4  0.4907     0.0417 0.000 0.420 0.000 0.580
#&gt; SRR1383363     2  0.4898     0.4050 0.000 0.584 0.000 0.416
#&gt; SRR1383364     3  0.0000     0.7814 0.000 0.000 1.000 0.000
#&gt; SRR1383365     4  0.4981    -0.1188 0.000 0.464 0.000 0.536
#&gt; SRR1383366     4  0.4804     0.1976 0.000 0.384 0.000 0.616
#&gt; SRR1383367     2  0.4985     0.2727 0.000 0.532 0.000 0.468
#&gt; SRR1383368     4  0.6050     0.2611 0.432 0.044 0.000 0.524
#&gt; SRR1383369     2  0.5478     0.1796 0.000 0.540 0.444 0.016
#&gt; SRR1383370     2  0.4985     0.2727 0.000 0.532 0.000 0.468
#&gt; SRR1383371     3  0.0000     0.7814 0.000 0.000 1.000 0.000
#&gt; SRR1383372     2  0.3400     0.7044 0.000 0.820 0.000 0.180
#&gt; SRR1383373     2  0.3486     0.6972 0.000 0.812 0.000 0.188
#&gt; SRR1383374     2  0.3486     0.7036 0.000 0.812 0.000 0.188
#&gt; SRR1383375     1  0.4482     0.7374 0.804 0.068 0.000 0.128
#&gt; SRR1383376     2  0.2149     0.7476 0.000 0.912 0.000 0.088
#&gt; SRR1383377     4  0.2868     0.6216 0.000 0.136 0.000 0.864
#&gt; SRR1383378     4  0.6926     0.1742 0.432 0.108 0.000 0.460
#&gt; SRR1383379     4  0.4382     0.6304 0.000 0.296 0.000 0.704
#&gt; SRR1383380     4  0.4933     0.6326 0.016 0.296 0.000 0.688
#&gt; SRR1383381     3  0.5217     0.7696 0.000 0.108 0.756 0.136
#&gt; SRR1383382     1  0.0000     0.9014 1.000 0.000 0.000 0.000
#&gt; SRR1383383     2  0.0921     0.7838 0.000 0.972 0.000 0.028
#&gt; SRR1383385     1  0.0000     0.9014 1.000 0.000 0.000 0.000
#&gt; SRR1383384     2  0.3610     0.5998 0.000 0.800 0.000 0.200
#&gt; SRR1383386     4  0.6050     0.2611 0.432 0.044 0.000 0.524
#&gt; SRR1383387     4  0.4406     0.6276 0.000 0.300 0.000 0.700
#&gt; SRR1383389     2  0.0188     0.7866 0.000 0.996 0.000 0.004
#&gt; SRR1383391     2  0.0188     0.7844 0.000 0.996 0.000 0.004
#&gt; SRR1383388     4  0.4957     0.6300 0.016 0.300 0.000 0.684
#&gt; SRR1383392     2  0.2530     0.7654 0.000 0.888 0.000 0.112
#&gt; SRR1383390     2  0.0000     0.7851 0.000 1.000 0.000 0.000
#&gt; SRR1383394     2  0.2149     0.7476 0.000 0.912 0.000 0.088
#&gt; SRR1383393     1  0.4482     0.7374 0.804 0.068 0.000 0.128
#&gt; SRR1383396     4  0.6926     0.1742 0.432 0.108 0.000 0.460
#&gt; SRR1383395     4  0.2868     0.6216 0.000 0.136 0.000 0.864
#&gt; SRR1383399     3  0.5217     0.7696 0.000 0.108 0.756 0.136
#&gt; SRR1383400     1  0.0000     0.9014 1.000 0.000 0.000 0.000
#&gt; SRR1383397     4  0.4382     0.6304 0.000 0.296 0.000 0.704
#&gt; SRR1383401     2  0.0921     0.7838 0.000 0.972 0.000 0.028
#&gt; SRR1383398     4  0.4933     0.6326 0.016 0.296 0.000 0.688
#&gt; SRR1383402     2  0.3610     0.5998 0.000 0.800 0.000 0.200
#&gt; SRR1383404     4  0.6050     0.2611 0.432 0.044 0.000 0.524
#&gt; SRR1383403     1  0.0000     0.9014 1.000 0.000 0.000 0.000
#&gt; SRR1383405     4  0.4406     0.6276 0.000 0.300 0.000 0.700
#&gt; SRR1383406     4  0.4957     0.6300 0.016 0.300 0.000 0.684
#&gt; SRR1383407     2  0.0188     0.7866 0.000 0.996 0.000 0.004
#&gt; SRR1383408     2  0.0000     0.7851 0.000 1.000 0.000 0.000
#&gt; SRR1383409     2  0.0188     0.7844 0.000 0.996 0.000 0.004
#&gt; SRR1383410     2  0.2530     0.7654 0.000 0.888 0.000 0.112
</code></pre>

<script>
$('#tab-CV-hclust-get-classes-3-a').parent().next().next().hide();
$('#tab-CV-hclust-get-classes-3-a').click(function(){
  $('#tab-CV-hclust-get-classes-3-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-CV-hclust-get-classes-4'>
<p><a id='tab-CV-hclust-get-classes-4-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 5), get_membership(res, k = 5))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4    p5
#&gt; SRR1383358     3  0.4434    0.16474 0.008 0.348 0.640 0.004 0.000
#&gt; SRR1383360     3  0.2361    0.47262 0.096 0.012 0.892 0.000 0.000
#&gt; SRR1383359     3  0.4182    0.33820 0.352 0.000 0.644 0.004 0.000
#&gt; SRR1383362     1  0.4242    1.00000 0.572 0.000 0.000 0.428 0.000
#&gt; SRR1383361     3  0.4240    0.25860 0.008 0.304 0.684 0.004 0.000
#&gt; SRR1383363     3  0.4650   -0.17799 0.012 0.468 0.520 0.000 0.000
#&gt; SRR1383364     5  0.0000    0.68271 0.000 0.000 0.000 0.000 1.000
#&gt; SRR1383365     3  0.4434    0.16474 0.008 0.348 0.640 0.004 0.000
#&gt; SRR1383366     3  0.3885    0.34031 0.008 0.268 0.724 0.000 0.000
#&gt; SRR1383367     3  0.4582   -0.01150 0.012 0.416 0.572 0.000 0.000
#&gt; SRR1383368     3  0.5294   -0.08493 0.004 0.040 0.524 0.432 0.000
#&gt; SRR1383369     5  0.6549   -0.03678 0.028 0.428 0.100 0.000 0.444
#&gt; SRR1383370     3  0.4582   -0.01150 0.012 0.416 0.572 0.000 0.000
#&gt; SRR1383371     5  0.0000    0.68271 0.000 0.000 0.000 0.000 1.000
#&gt; SRR1383372     2  0.3957    0.58634 0.008 0.712 0.280 0.000 0.000
#&gt; SRR1383373     2  0.4025    0.57003 0.008 0.700 0.292 0.000 0.000
#&gt; SRR1383374     2  0.4003    0.58332 0.008 0.704 0.288 0.000 0.000
#&gt; SRR1383375     4  0.0510    0.29985 0.000 0.000 0.016 0.984 0.000
#&gt; SRR1383376     2  0.1851    0.76627 0.000 0.912 0.088 0.000 0.000
#&gt; SRR1383377     3  0.3946    0.51175 0.120 0.080 0.800 0.000 0.000
#&gt; SRR1383378     4  0.5768    0.31694 0.012 0.068 0.360 0.560 0.000
#&gt; SRR1383379     3  0.3774    0.57054 0.000 0.296 0.704 0.000 0.000
#&gt; SRR1383380     3  0.4249    0.57056 0.000 0.296 0.688 0.016 0.000
#&gt; SRR1383381     5  0.4738    0.67037 0.032 0.016 0.016 0.180 0.756
#&gt; SRR1383382     1  0.4242    1.00000 0.572 0.000 0.000 0.428 0.000
#&gt; SRR1383383     2  0.0992    0.81664 0.008 0.968 0.024 0.000 0.000
#&gt; SRR1383385     4  0.3242   -0.00567 0.216 0.000 0.000 0.784 0.000
#&gt; SRR1383384     2  0.3109    0.57960 0.000 0.800 0.200 0.000 0.000
#&gt; SRR1383386     3  0.5294   -0.08493 0.004 0.040 0.524 0.432 0.000
#&gt; SRR1383387     3  0.3796    0.56816 0.000 0.300 0.700 0.000 0.000
#&gt; SRR1383389     2  0.0865    0.82135 0.004 0.972 0.024 0.000 0.000
#&gt; SRR1383391     2  0.0162    0.82120 0.000 0.996 0.004 0.000 0.000
#&gt; SRR1383388     3  0.4269    0.56821 0.000 0.300 0.684 0.016 0.000
#&gt; SRR1383392     2  0.2921    0.77304 0.020 0.856 0.124 0.000 0.000
#&gt; SRR1383390     2  0.0000    0.82122 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1383394     2  0.1851    0.76627 0.000 0.912 0.088 0.000 0.000
#&gt; SRR1383393     4  0.0510    0.29985 0.000 0.000 0.016 0.984 0.000
#&gt; SRR1383396     4  0.5768    0.31694 0.012 0.068 0.360 0.560 0.000
#&gt; SRR1383395     3  0.3946    0.51175 0.120 0.080 0.800 0.000 0.000
#&gt; SRR1383399     5  0.4738    0.67037 0.032 0.016 0.016 0.180 0.756
#&gt; SRR1383400     1  0.4242    1.00000 0.572 0.000 0.000 0.428 0.000
#&gt; SRR1383397     3  0.3774    0.57054 0.000 0.296 0.704 0.000 0.000
#&gt; SRR1383401     2  0.0992    0.81664 0.008 0.968 0.024 0.000 0.000
#&gt; SRR1383398     3  0.4249    0.57056 0.000 0.296 0.688 0.016 0.000
#&gt; SRR1383402     2  0.3109    0.57960 0.000 0.800 0.200 0.000 0.000
#&gt; SRR1383404     3  0.5294   -0.08493 0.004 0.040 0.524 0.432 0.000
#&gt; SRR1383403     4  0.3242   -0.00567 0.216 0.000 0.000 0.784 0.000
#&gt; SRR1383405     3  0.3796    0.56816 0.000 0.300 0.700 0.000 0.000
#&gt; SRR1383406     3  0.4269    0.56821 0.000 0.300 0.684 0.016 0.000
#&gt; SRR1383407     2  0.0865    0.82135 0.004 0.972 0.024 0.000 0.000
#&gt; SRR1383408     2  0.0000    0.82122 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1383409     2  0.0162    0.82120 0.000 0.996 0.004 0.000 0.000
#&gt; SRR1383410     2  0.2921    0.77304 0.020 0.856 0.124 0.000 0.000
</code></pre>

<script>
$('#tab-CV-hclust-get-classes-4-a').parent().next().next().hide();
$('#tab-CV-hclust-get-classes-4-a').click(function(){
  $('#tab-CV-hclust-get-classes-4-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-CV-hclust-get-classes-5'>
<p><a id='tab-CV-hclust-get-classes-5-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 6), get_membership(res, k = 6))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4    p5    p6
#&gt; SRR1383358     4  0.6037    -0.0336 0.000 0.332 0.220 0.444 0.004 0.000
#&gt; SRR1383360     4  0.0790     0.0222 0.000 0.000 0.032 0.968 0.000 0.000
#&gt; SRR1383359     3  0.4543     0.0000 0.000 0.000 0.584 0.380 0.004 0.032
#&gt; SRR1383362     6  0.0790     1.0000 0.032 0.000 0.000 0.000 0.000 0.968
#&gt; SRR1383361     4  0.5919     0.0422 0.000 0.288 0.216 0.492 0.004 0.000
#&gt; SRR1383363     2  0.5833     0.2233 0.000 0.444 0.192 0.364 0.000 0.000
#&gt; SRR1383364     5  0.3050     0.8342 0.000 0.000 0.236 0.000 0.764 0.000
#&gt; SRR1383365     4  0.6037    -0.0336 0.000 0.332 0.220 0.444 0.004 0.000
#&gt; SRR1383366     4  0.5534     0.0545 0.000 0.248 0.196 0.556 0.000 0.000
#&gt; SRR1383367     4  0.5870    -0.1637 0.000 0.392 0.196 0.412 0.000 0.000
#&gt; SRR1383368     4  0.6329     0.0864 0.332 0.040 0.016 0.512 0.000 0.100
#&gt; SRR1383369     2  0.6039     0.0526 0.000 0.412 0.264 0.000 0.324 0.000
#&gt; SRR1383370     4  0.5870    -0.1637 0.000 0.392 0.196 0.412 0.000 0.000
#&gt; SRR1383371     5  0.3050     0.8342 0.000 0.000 0.236 0.000 0.764 0.000
#&gt; SRR1383372     2  0.4520     0.5828 0.000 0.704 0.128 0.168 0.000 0.000
#&gt; SRR1383373     2  0.4620     0.5690 0.000 0.692 0.132 0.176 0.000 0.000
#&gt; SRR1383374     2  0.4728     0.5771 0.000 0.680 0.144 0.176 0.000 0.000
#&gt; SRR1383375     1  0.4711     0.7419 0.708 0.000 0.004 0.008 0.180 0.100
#&gt; SRR1383376     2  0.1663     0.7123 0.000 0.912 0.000 0.088 0.000 0.000
#&gt; SRR1383377     4  0.2941     0.0872 0.000 0.060 0.048 0.868 0.024 0.000
#&gt; SRR1383378     4  0.8321    -0.2001 0.332 0.052 0.020 0.332 0.164 0.100
#&gt; SRR1383379     4  0.3351     0.3830 0.000 0.288 0.000 0.712 0.000 0.000
#&gt; SRR1383380     4  0.3778     0.3862 0.016 0.288 0.000 0.696 0.000 0.000
#&gt; SRR1383381     5  0.0291     0.8292 0.004 0.000 0.004 0.000 0.992 0.000
#&gt; SRR1383382     6  0.0790     1.0000 0.032 0.000 0.000 0.000 0.000 0.968
#&gt; SRR1383383     2  0.1699     0.7518 0.000 0.936 0.016 0.016 0.032 0.000
#&gt; SRR1383385     1  0.1152     0.7422 0.952 0.000 0.044 0.000 0.000 0.004
#&gt; SRR1383384     2  0.3231     0.5449 0.000 0.784 0.016 0.200 0.000 0.000
#&gt; SRR1383386     4  0.6329     0.0864 0.332 0.040 0.016 0.512 0.000 0.100
#&gt; SRR1383387     4  0.3371     0.3832 0.000 0.292 0.000 0.708 0.000 0.000
#&gt; SRR1383389     2  0.1225     0.7610 0.000 0.952 0.012 0.036 0.000 0.000
#&gt; SRR1383391     2  0.0146     0.7592 0.000 0.996 0.000 0.004 0.000 0.000
#&gt; SRR1383388     4  0.3797     0.3861 0.016 0.292 0.000 0.692 0.000 0.000
#&gt; SRR1383392     2  0.2907     0.7238 0.000 0.828 0.020 0.152 0.000 0.000
#&gt; SRR1383390     2  0.0146     0.7605 0.000 0.996 0.004 0.000 0.000 0.000
#&gt; SRR1383394     2  0.1663     0.7123 0.000 0.912 0.000 0.088 0.000 0.000
#&gt; SRR1383393     1  0.4711     0.7419 0.708 0.000 0.004 0.008 0.180 0.100
#&gt; SRR1383396     4  0.8321    -0.2001 0.332 0.052 0.020 0.332 0.164 0.100
#&gt; SRR1383395     4  0.2941     0.0872 0.000 0.060 0.048 0.868 0.024 0.000
#&gt; SRR1383399     5  0.0291     0.8292 0.004 0.000 0.004 0.000 0.992 0.000
#&gt; SRR1383400     6  0.0790     1.0000 0.032 0.000 0.000 0.000 0.000 0.968
#&gt; SRR1383397     4  0.3351     0.3830 0.000 0.288 0.000 0.712 0.000 0.000
#&gt; SRR1383401     2  0.1699     0.7518 0.000 0.936 0.016 0.016 0.032 0.000
#&gt; SRR1383398     4  0.3778     0.3862 0.016 0.288 0.000 0.696 0.000 0.000
#&gt; SRR1383402     2  0.3231     0.5449 0.000 0.784 0.016 0.200 0.000 0.000
#&gt; SRR1383404     4  0.6329     0.0864 0.332 0.040 0.016 0.512 0.000 0.100
#&gt; SRR1383403     1  0.1152     0.7422 0.952 0.000 0.044 0.000 0.000 0.004
#&gt; SRR1383405     4  0.3371     0.3832 0.000 0.292 0.000 0.708 0.000 0.000
#&gt; SRR1383406     4  0.3797     0.3861 0.016 0.292 0.000 0.692 0.000 0.000
#&gt; SRR1383407     2  0.1225     0.7610 0.000 0.952 0.012 0.036 0.000 0.000
#&gt; SRR1383408     2  0.0146     0.7605 0.000 0.996 0.004 0.000 0.000 0.000
#&gt; SRR1383409     2  0.0146     0.7592 0.000 0.996 0.000 0.004 0.000 0.000
#&gt; SRR1383410     2  0.2907     0.7238 0.000 0.828 0.020 0.152 0.000 0.000
</code></pre>

<script>
$('#tab-CV-hclust-get-classes-5-a').parent().next().next().hide();
$('#tab-CV-hclust-get-classes-5-a').click(function(){
  $('#tab-CV-hclust-get-classes-5-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>
</div>

Heatmaps for the consensus matrix. It visualizes the probability of two
samples to be in a same group.



<script>
$( function() {
	$( '#tabs-CV-hclust-consensus-heatmap' ).tabs();
} );
</script>
<div id='tabs-CV-hclust-consensus-heatmap'>
<ul>
<li><a href='#tab-CV-hclust-consensus-heatmap-1'>k = 2</a></li>
<li><a href='#tab-CV-hclust-consensus-heatmap-2'>k = 3</a></li>
<li><a href='#tab-CV-hclust-consensus-heatmap-3'>k = 4</a></li>
<li><a href='#tab-CV-hclust-consensus-heatmap-4'>k = 5</a></li>
<li><a href='#tab-CV-hclust-consensus-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-CV-hclust-consensus-heatmap-1'>
<pre><code class="r">consensus_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-CV-hclust-consensus-heatmap-1-1.png" alt="plot of chunk tab-CV-hclust-consensus-heatmap-1"/></p>

</div>
<div id='tab-CV-hclust-consensus-heatmap-2'>
<pre><code class="r">consensus_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-CV-hclust-consensus-heatmap-2-1.png" alt="plot of chunk tab-CV-hclust-consensus-heatmap-2"/></p>

</div>
<div id='tab-CV-hclust-consensus-heatmap-3'>
<pre><code class="r">consensus_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-CV-hclust-consensus-heatmap-3-1.png" alt="plot of chunk tab-CV-hclust-consensus-heatmap-3"/></p>

</div>
<div id='tab-CV-hclust-consensus-heatmap-4'>
<pre><code class="r">consensus_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-CV-hclust-consensus-heatmap-4-1.png" alt="plot of chunk tab-CV-hclust-consensus-heatmap-4"/></p>

</div>
<div id='tab-CV-hclust-consensus-heatmap-5'>
<pre><code class="r">consensus_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-CV-hclust-consensus-heatmap-5-1.png" alt="plot of chunk tab-CV-hclust-consensus-heatmap-5"/></p>

</div>
</div>

Heatmaps for the membership of samples in all partitions to see how consistent they are:




<script>
$( function() {
	$( '#tabs-CV-hclust-membership-heatmap' ).tabs();
} );
</script>
<div id='tabs-CV-hclust-membership-heatmap'>
<ul>
<li><a href='#tab-CV-hclust-membership-heatmap-1'>k = 2</a></li>
<li><a href='#tab-CV-hclust-membership-heatmap-2'>k = 3</a></li>
<li><a href='#tab-CV-hclust-membership-heatmap-3'>k = 4</a></li>
<li><a href='#tab-CV-hclust-membership-heatmap-4'>k = 5</a></li>
<li><a href='#tab-CV-hclust-membership-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-CV-hclust-membership-heatmap-1'>
<pre><code class="r">membership_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-CV-hclust-membership-heatmap-1-1.png" alt="plot of chunk tab-CV-hclust-membership-heatmap-1"/></p>

</div>
<div id='tab-CV-hclust-membership-heatmap-2'>
<pre><code class="r">membership_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-CV-hclust-membership-heatmap-2-1.png" alt="plot of chunk tab-CV-hclust-membership-heatmap-2"/></p>

</div>
<div id='tab-CV-hclust-membership-heatmap-3'>
<pre><code class="r">membership_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-CV-hclust-membership-heatmap-3-1.png" alt="plot of chunk tab-CV-hclust-membership-heatmap-3"/></p>

</div>
<div id='tab-CV-hclust-membership-heatmap-4'>
<pre><code class="r">membership_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-CV-hclust-membership-heatmap-4-1.png" alt="plot of chunk tab-CV-hclust-membership-heatmap-4"/></p>

</div>
<div id='tab-CV-hclust-membership-heatmap-5'>
<pre><code class="r">membership_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-CV-hclust-membership-heatmap-5-1.png" alt="plot of chunk tab-CV-hclust-membership-heatmap-5"/></p>

</div>
</div>

As soon as we have had the classes for columns, we can look for signatures
which are significantly different between classes which can be candidate marks
for certain classes. Following are the heatmaps for signatures.



Signature heatmaps where rows are scaled:



<script>
$( function() {
	$( '#tabs-CV-hclust-get-signatures' ).tabs();
} );
</script>
<div id='tabs-CV-hclust-get-signatures'>
<ul>
<li><a href='#tab-CV-hclust-get-signatures-1'>k = 2</a></li>
<li><a href='#tab-CV-hclust-get-signatures-2'>k = 3</a></li>
<li><a href='#tab-CV-hclust-get-signatures-3'>k = 4</a></li>
<li><a href='#tab-CV-hclust-get-signatures-4'>k = 5</a></li>
<li><a href='#tab-CV-hclust-get-signatures-5'>k = 6</a></li>
</ul>
<div id='tab-CV-hclust-get-signatures-1'>
<pre><code class="r">get_signatures(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-CV-hclust-get-signatures-1-1.png" alt="plot of chunk tab-CV-hclust-get-signatures-1"/></p>

</div>
<div id='tab-CV-hclust-get-signatures-2'>
<pre><code class="r">get_signatures(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-CV-hclust-get-signatures-2-1.png" alt="plot of chunk tab-CV-hclust-get-signatures-2"/></p>

</div>
<div id='tab-CV-hclust-get-signatures-3'>
<pre><code class="r">get_signatures(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-CV-hclust-get-signatures-3-1.png" alt="plot of chunk tab-CV-hclust-get-signatures-3"/></p>

</div>
<div id='tab-CV-hclust-get-signatures-4'>
<pre><code class="r">get_signatures(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-CV-hclust-get-signatures-4-1.png" alt="plot of chunk tab-CV-hclust-get-signatures-4"/></p>

</div>
<div id='tab-CV-hclust-get-signatures-5'>
<pre><code class="r">get_signatures(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-CV-hclust-get-signatures-5-1.png" alt="plot of chunk tab-CV-hclust-get-signatures-5"/></p>

</div>
</div>



Signature heatmaps where rows are not scaled:


<script>
$( function() {
	$( '#tabs-CV-hclust-get-signatures-no-scale' ).tabs();
} );
</script>
<div id='tabs-CV-hclust-get-signatures-no-scale'>
<ul>
<li><a href='#tab-CV-hclust-get-signatures-no-scale-1'>k = 2</a></li>
<li><a href='#tab-CV-hclust-get-signatures-no-scale-2'>k = 3</a></li>
<li><a href='#tab-CV-hclust-get-signatures-no-scale-3'>k = 4</a></li>
<li><a href='#tab-CV-hclust-get-signatures-no-scale-4'>k = 5</a></li>
<li><a href='#tab-CV-hclust-get-signatures-no-scale-5'>k = 6</a></li>
</ul>
<div id='tab-CV-hclust-get-signatures-no-scale-1'>
<pre><code class="r">get_signatures(res, k = 2, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-CV-hclust-get-signatures-no-scale-1-1.png" alt="plot of chunk tab-CV-hclust-get-signatures-no-scale-1"/></p>

</div>
<div id='tab-CV-hclust-get-signatures-no-scale-2'>
<pre><code class="r">get_signatures(res, k = 3, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-CV-hclust-get-signatures-no-scale-2-1.png" alt="plot of chunk tab-CV-hclust-get-signatures-no-scale-2"/></p>

</div>
<div id='tab-CV-hclust-get-signatures-no-scale-3'>
<pre><code class="r">get_signatures(res, k = 4, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-CV-hclust-get-signatures-no-scale-3-1.png" alt="plot of chunk tab-CV-hclust-get-signatures-no-scale-3"/></p>

</div>
<div id='tab-CV-hclust-get-signatures-no-scale-4'>
<pre><code class="r">get_signatures(res, k = 5, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-CV-hclust-get-signatures-no-scale-4-1.png" alt="plot of chunk tab-CV-hclust-get-signatures-no-scale-4"/></p>

</div>
<div id='tab-CV-hclust-get-signatures-no-scale-5'>
<pre><code class="r">get_signatures(res, k = 6, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-CV-hclust-get-signatures-no-scale-5-1.png" alt="plot of chunk tab-CV-hclust-get-signatures-no-scale-5"/></p>

</div>
</div>



Compare the overlap of signatures from different k:

```r
compare_signatures(res)
```

![plot of chunk CV-hclust-signature_compare](figure_cola/CV-hclust-signature_compare-1.png)

`get_signature()` returns a data frame invisibly. TO get the list of signatures, the function
call should be assigned to a variable explicitly. In following code, if `plot` argument is set
to `FALSE`, no heatmap is plotted while only the differential analysis is performed.

```r
# code only for demonstration
tb = get_signature(res, k = ..., plot = FALSE)
```

An example of the output of `tb` is:

```
#>   which_row         fdr    mean_1    mean_2 scaled_mean_1 scaled_mean_2 km
#> 1        38 0.042760348  8.373488  9.131774    -0.5533452     0.5164555  1
#> 2        40 0.018707592  7.106213  8.469186    -0.6173731     0.5762149  1
#> 3        55 0.019134737 10.221463 11.207825    -0.6159697     0.5749050  1
#> 4        59 0.006059896  5.921854  7.869574    -0.6899429     0.6439467  1
#> 5        60 0.018055526  8.928898 10.211722    -0.6204761     0.5791110  1
#> 6        98 0.009384629 15.714769 14.887706     0.6635654    -0.6193277  2
...
```

The columns in `tb` are:

1. `which_row`: row indices corresponding to the input matrix.
2. `fdr`: FDR for the differential test. 
3. `mean_x`: The mean value in group x.
4. `scaled_mean_x`: The mean value in group x after rows are scaled.
5. `km`: Row groups if k-means clustering is applied to rows.



UMAP plot which shows how samples are separated.


<script>
$( function() {
	$( '#tabs-CV-hclust-dimension-reduction' ).tabs();
} );
</script>
<div id='tabs-CV-hclust-dimension-reduction'>
<ul>
<li><a href='#tab-CV-hclust-dimension-reduction-1'>k = 2</a></li>
<li><a href='#tab-CV-hclust-dimension-reduction-2'>k = 3</a></li>
<li><a href='#tab-CV-hclust-dimension-reduction-3'>k = 4</a></li>
<li><a href='#tab-CV-hclust-dimension-reduction-4'>k = 5</a></li>
<li><a href='#tab-CV-hclust-dimension-reduction-5'>k = 6</a></li>
</ul>
<div id='tab-CV-hclust-dimension-reduction-1'>
<pre><code class="r">dimension_reduction(res, k = 2, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-CV-hclust-dimension-reduction-1-1.png" alt="plot of chunk tab-CV-hclust-dimension-reduction-1"/></p>

</div>
<div id='tab-CV-hclust-dimension-reduction-2'>
<pre><code class="r">dimension_reduction(res, k = 3, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-CV-hclust-dimension-reduction-2-1.png" alt="plot of chunk tab-CV-hclust-dimension-reduction-2"/></p>

</div>
<div id='tab-CV-hclust-dimension-reduction-3'>
<pre><code class="r">dimension_reduction(res, k = 4, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-CV-hclust-dimension-reduction-3-1.png" alt="plot of chunk tab-CV-hclust-dimension-reduction-3"/></p>

</div>
<div id='tab-CV-hclust-dimension-reduction-4'>
<pre><code class="r">dimension_reduction(res, k = 5, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-CV-hclust-dimension-reduction-4-1.png" alt="plot of chunk tab-CV-hclust-dimension-reduction-4"/></p>

</div>
<div id='tab-CV-hclust-dimension-reduction-5'>
<pre><code class="r">dimension_reduction(res, k = 6, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-CV-hclust-dimension-reduction-5-1.png" alt="plot of chunk tab-CV-hclust-dimension-reduction-5"/></p>

</div>
</div>


Following heatmap shows how subgroups are split when increasing `k`:

```r
collect_classes(res)
```

![plot of chunk CV-hclust-collect-classes](figure_cola/CV-hclust-collect-classes-1.png)


If matrix rows can be associated to genes, consider to use `functional_enrichment(res,
...)` to perform function enrichment for the signature genes. See [this vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/functional_enrichment.html) for more detailed explanations.


 

---------------------------------------------------




### CV:kmeans






The object with results only for a single top-value method and a single partition method 
can be extracted as:

```r
res = res_list["CV", "kmeans"]
# you can also extract it by
# res = res_list["CV:kmeans"]
```

A summary of `res` and all the functions that can be applied to it:

```r
res
```

```
#> A 'ConsensusPartition' object with k = 2, 3, 4, 5, 6.
#>   On a matrix with 15680 rows and 53 columns.
#>   Top rows (1000, 2000, 3000, 4000, 5000) are extracted by 'CV' method.
#>   Subgroups are detected by 'kmeans' method.
#>   Performed in total 1250 partitions by row resampling.
#>   Best k for subgroups seems to be 4.
#> 
#> Following methods can be applied to this 'ConsensusPartition' object:
#>  [1] "cola_report"             "collect_classes"         "collect_plots"          
#>  [4] "collect_stats"           "colnames"                "compare_signatures"     
#>  [7] "consensus_heatmap"       "dimension_reduction"     "functional_enrichment"  
#> [10] "get_anno_col"            "get_anno"                "get_classes"            
#> [13] "get_consensus"           "get_matrix"              "get_membership"         
#> [16] "get_param"               "get_signatures"          "get_stats"              
#> [19] "is_best_k"               "is_stable_k"             "membership_heatmap"     
#> [22] "ncol"                    "nrow"                    "plot_ecdf"              
#> [25] "rownames"                "select_partition_number" "show"                   
#> [28] "suggest_best_k"          "test_to_known_factors"
```

`collect_plots()` function collects all the plots made from `res` for all `k` (number of partitions)
into one single page to provide an easy and fast comparison between different `k`.

```r
collect_plots(res)
```

![plot of chunk CV-kmeans-collect-plots](figure_cola/CV-kmeans-collect-plots-1.png)

The plots are:

- The first row: a plot of the ECDF (empirical cumulative distribution
  function) curves of the consensus matrix for each `k` and the heatmap of
  predicted classes for each `k`.
- The second row: heatmaps of the consensus matrix for each `k`.
- The third row: heatmaps of the membership matrix for each `k`.
- The fouth row: heatmaps of the signatures for each `k`.

All the plots in panels can be made by individual functions and they are
plotted later in this section.

`select_partition_number()` produces several plots showing different
statistics for choosing "optimized" `k`. There are following statistics:

- ECDF curves of the consensus matrix for each `k`;
- 1-PAC. [The PAC
  score](https://en.wikipedia.org/wiki/Consensus_clustering#Over-interpretation_potential_of_consensus_clustering)
  measures the proportion of the ambiguous subgrouping.
- Mean silhouette score.
- Concordance. The mean probability of fiting the consensus class ids in all
  partitions.
- Area increased. Denote $A_k$ as the area under the ECDF curve for current
  `k`, the area increased is defined as $A_k - A_{k-1}$.
- Rand index. The percent of pairs of samples that are both in a same cluster
  or both are not in a same cluster in the partition of k and k-1.
- Jaccard index. The ratio of pairs of samples are both in a same cluster in
  the partition of k and k-1 and the pairs of samples are both in a same
  cluster in the partition k or k-1.

The detailed explanations of these statistics can be found in [the _cola_
vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/cola.html#toc_13).

Generally speaking, lower PAC score, higher mean silhouette score or higher
concordance corresponds to better partition. Rand index and Jaccard index
measure how similar the current partition is compared to partition with `k-1`.
If they are too similar, we won't accept `k` is better than `k-1`.

```r
select_partition_number(res)
```

![plot of chunk CV-kmeans-select-partition-number](figure_cola/CV-kmeans-select-partition-number-1.png)

The numeric values for all these statistics can be obtained by `get_stats()`.

```r
get_stats(res)
```

```
#>   k 1-PAC mean_silhouette concordance area_increased  Rand Jaccard
#> 2 2 0.333           0.730       0.840         0.3939 0.543   0.543
#> 3 3 0.255           0.533       0.682         0.4936 0.746   0.576
#> 4 4 0.331           0.557       0.711         0.1700 0.764   0.503
#> 5 5 0.539           0.753       0.793         0.1076 0.838   0.529
#> 6 6 0.665           0.681       0.751         0.0575 0.993   0.966
```

`suggest_best_k()` suggests the best $k$ based on these statistics. The rules are as follows:

- All $k$ with Jaccard index larger than 0.95 are removed because increasing
  $k$ does not provide enough extra information. If all $k$ are removed, it is
  marked as no subgroup is detected.
- For all $k$ with 1-PAC score larger than 0.9, the maximal $k$ is taken as
  the best $k$, and other $k$ are marked as optional $k$.
- If it does not fit the second rule. The $k$ with the maximal vote of the
  highest 1-PAC score, highest mean silhouette, and highest concordance is
  taken as the best $k$.

```r
suggest_best_k(res)
```

```
#> [1] 4
```


Following shows the table of the partitions (You need to click the **show/hide
code output** link to see it). The membership matrix (columns with name `p*`)
is inferred by
[`clue::cl_consensus()`](https://www.rdocumentation.org/link/cl_consensus?package=clue)
function with the `SE` method. Basically the value in the membership matrix
represents the probability to belong to a certain group. The finall class
label for an item is determined with the group with highest probability it
belongs to.

In `get_classes()` function, the entropy is calculated from the membership
matrix and the silhouette score is calculated from the consensus matrix.



<script>
$( function() {
	$( '#tabs-CV-kmeans-get-classes' ).tabs();
} );
</script>
<div id='tabs-CV-kmeans-get-classes'>
<ul>
<li><a href='#tab-CV-kmeans-get-classes-1'>k = 2</a></li>
<li><a href='#tab-CV-kmeans-get-classes-2'>k = 3</a></li>
<li><a href='#tab-CV-kmeans-get-classes-3'>k = 4</a></li>
<li><a href='#tab-CV-kmeans-get-classes-4'>k = 5</a></li>
<li><a href='#tab-CV-kmeans-get-classes-5'>k = 6</a></li>
</ul>

<div id='tab-CV-kmeans-get-classes-1'>
<p><a id='tab-CV-kmeans-get-classes-1-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 2), get_membership(res, k = 2))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2
#&gt; SRR1383358     2  0.2043      0.860 0.032 0.968
#&gt; SRR1383360     1  0.9850      0.676 0.572 0.428
#&gt; SRR1383359     2  0.2043      0.860 0.032 0.968
#&gt; SRR1383362     1  0.4562      0.696 0.904 0.096
#&gt; SRR1383361     2  0.1633      0.863 0.024 0.976
#&gt; SRR1383363     2  0.2043      0.860 0.032 0.968
#&gt; SRR1383364     2  0.8813      0.548 0.300 0.700
#&gt; SRR1383365     2  0.1633      0.862 0.024 0.976
#&gt; SRR1383366     2  0.4431      0.805 0.092 0.908
#&gt; SRR1383367     2  0.1633      0.863 0.024 0.976
#&gt; SRR1383368     1  0.9552      0.712 0.624 0.376
#&gt; SRR1383369     2  0.4690      0.791 0.100 0.900
#&gt; SRR1383370     2  0.0672      0.867 0.008 0.992
#&gt; SRR1383371     2  0.8813      0.548 0.300 0.700
#&gt; SRR1383372     2  0.0938      0.866 0.012 0.988
#&gt; SRR1383373     2  0.1414      0.864 0.020 0.980
#&gt; SRR1383374     2  0.0000      0.867 0.000 1.000
#&gt; SRR1383375     1  0.5294      0.706 0.880 0.120
#&gt; SRR1383376     2  0.1414      0.863 0.020 0.980
#&gt; SRR1383377     2  0.9044      0.232 0.320 0.680
#&gt; SRR1383378     2  0.4939      0.749 0.108 0.892
#&gt; SRR1383379     1  0.9970      0.624 0.532 0.468
#&gt; SRR1383380     1  0.9850      0.678 0.572 0.428
#&gt; SRR1383381     2  0.8861      0.549 0.304 0.696
#&gt; SRR1383382     1  0.4815      0.700 0.896 0.104
#&gt; SRR1383383     2  0.1414      0.864 0.020 0.980
#&gt; SRR1383385     1  0.4298      0.698 0.912 0.088
#&gt; SRR1383384     2  0.1414      0.863 0.020 0.980
#&gt; SRR1383386     1  0.9460      0.719 0.636 0.364
#&gt; SRR1383387     2  0.8555      0.339 0.280 0.720
#&gt; SRR1383389     2  0.0376      0.868 0.004 0.996
#&gt; SRR1383391     2  0.0672      0.867 0.008 0.992
#&gt; SRR1383388     1  0.9944      0.644 0.544 0.456
#&gt; SRR1383392     2  0.0938      0.865 0.012 0.988
#&gt; SRR1383390     2  0.0672      0.867 0.008 0.992
#&gt; SRR1383394     2  0.1414      0.863 0.020 0.980
#&gt; SRR1383393     1  0.5294      0.706 0.880 0.120
#&gt; SRR1383396     1  0.9833      0.670 0.576 0.424
#&gt; SRR1383395     2  0.9044      0.232 0.320 0.680
#&gt; SRR1383399     2  0.8861      0.549 0.304 0.696
#&gt; SRR1383400     1  0.4815      0.700 0.896 0.104
#&gt; SRR1383397     1  0.9970      0.624 0.532 0.468
#&gt; SRR1383401     2  0.1184      0.865 0.016 0.984
#&gt; SRR1383398     1  0.9850      0.678 0.572 0.428
#&gt; SRR1383402     2  0.1414      0.863 0.020 0.980
#&gt; SRR1383404     1  0.9491      0.717 0.632 0.368
#&gt; SRR1383403     1  0.4298      0.698 0.912 0.088
#&gt; SRR1383405     2  0.8555      0.339 0.280 0.720
#&gt; SRR1383406     1  0.9970      0.624 0.532 0.468
#&gt; SRR1383407     2  0.0376      0.868 0.004 0.996
#&gt; SRR1383408     2  0.0672      0.867 0.008 0.992
#&gt; SRR1383409     2  0.0672      0.867 0.008 0.992
#&gt; SRR1383410     2  0.1414      0.863 0.020 0.980
</code></pre>

<script>
$('#tab-CV-kmeans-get-classes-1-a').parent().next().next().hide();
$('#tab-CV-kmeans-get-classes-1-a').click(function(){
  $('#tab-CV-kmeans-get-classes-1-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-CV-kmeans-get-classes-2'>
<p><a id='tab-CV-kmeans-get-classes-2-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 3), get_membership(res, k = 3))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3
#&gt; SRR1383358     3  0.5623     0.4812 0.004 0.280 0.716
#&gt; SRR1383360     2  0.9400     0.5804 0.264 0.508 0.228
#&gt; SRR1383359     3  0.6664     0.1045 0.008 0.464 0.528
#&gt; SRR1383362     1  0.1753     0.9232 0.952 0.048 0.000
#&gt; SRR1383361     3  0.6518     0.1360 0.004 0.484 0.512
#&gt; SRR1383363     3  0.4629     0.5348 0.004 0.188 0.808
#&gt; SRR1383364     3  0.7749     0.4396 0.072 0.312 0.616
#&gt; SRR1383365     3  0.5553     0.4906 0.004 0.272 0.724
#&gt; SRR1383366     2  0.7141     0.3302 0.032 0.600 0.368
#&gt; SRR1383367     3  0.6516     0.1213 0.004 0.480 0.516
#&gt; SRR1383368     2  0.9569     0.5617 0.280 0.480 0.240
#&gt; SRR1383369     3  0.5553     0.4986 0.004 0.272 0.724
#&gt; SRR1383370     3  0.6505     0.0986 0.004 0.468 0.528
#&gt; SRR1383371     3  0.7749     0.4396 0.072 0.312 0.616
#&gt; SRR1383372     3  0.3500     0.5829 0.004 0.116 0.880
#&gt; SRR1383373     3  0.3112     0.5737 0.004 0.096 0.900
#&gt; SRR1383374     3  0.3038     0.5847 0.000 0.104 0.896
#&gt; SRR1383375     1  0.4615     0.8391 0.836 0.144 0.020
#&gt; SRR1383376     2  0.6495     0.1776 0.004 0.536 0.460
#&gt; SRR1383377     2  0.8148     0.5578 0.100 0.604 0.296
#&gt; SRR1383378     3  0.6369     0.3695 0.016 0.316 0.668
#&gt; SRR1383379     2  0.7677     0.7218 0.204 0.676 0.120
#&gt; SRR1383380     2  0.7639     0.7140 0.256 0.656 0.088
#&gt; SRR1383381     3  0.7749     0.4467 0.076 0.300 0.624
#&gt; SRR1383382     1  0.1753     0.9232 0.952 0.048 0.000
#&gt; SRR1383383     3  0.5024     0.5435 0.004 0.220 0.776
#&gt; SRR1383385     1  0.0892     0.9205 0.980 0.020 0.000
#&gt; SRR1383384     3  0.6235     0.1519 0.000 0.436 0.564
#&gt; SRR1383386     2  0.8132     0.6715 0.304 0.600 0.096
#&gt; SRR1383387     2  0.6793     0.5555 0.036 0.672 0.292
#&gt; SRR1383389     3  0.3267     0.5816 0.000 0.116 0.884
#&gt; SRR1383391     3  0.5325     0.4934 0.004 0.248 0.748
#&gt; SRR1383388     2  0.7872     0.7190 0.236 0.652 0.112
#&gt; SRR1383392     3  0.5497     0.4268 0.000 0.292 0.708
#&gt; SRR1383390     3  0.4931     0.5063 0.000 0.232 0.768
#&gt; SRR1383394     2  0.6495     0.1776 0.004 0.536 0.460
#&gt; SRR1383393     1  0.4615     0.8391 0.836 0.144 0.020
#&gt; SRR1383396     2  0.9321     0.5762 0.224 0.520 0.256
#&gt; SRR1383395     2  0.8148     0.5578 0.100 0.604 0.296
#&gt; SRR1383399     3  0.7749     0.4467 0.076 0.300 0.624
#&gt; SRR1383400     1  0.1753     0.9232 0.952 0.048 0.000
#&gt; SRR1383397     2  0.7677     0.7218 0.204 0.676 0.120
#&gt; SRR1383401     3  0.4172     0.5755 0.004 0.156 0.840
#&gt; SRR1383398     2  0.7639     0.7140 0.256 0.656 0.088
#&gt; SRR1383402     3  0.6235     0.1519 0.000 0.436 0.564
#&gt; SRR1383404     2  0.8132     0.6715 0.304 0.600 0.096
#&gt; SRR1383403     1  0.0892     0.9205 0.980 0.020 0.000
#&gt; SRR1383405     2  0.6793     0.5555 0.036 0.672 0.292
#&gt; SRR1383406     2  0.7613     0.7222 0.204 0.680 0.116
#&gt; SRR1383407     3  0.3267     0.5816 0.000 0.116 0.884
#&gt; SRR1383408     3  0.4931     0.5063 0.000 0.232 0.768
#&gt; SRR1383409     3  0.5098     0.4967 0.000 0.248 0.752
#&gt; SRR1383410     3  0.6008     0.3137 0.000 0.372 0.628
</code></pre>

<script>
$('#tab-CV-kmeans-get-classes-2-a').parent().next().next().hide();
$('#tab-CV-kmeans-get-classes-2-a').click(function(){
  $('#tab-CV-kmeans-get-classes-2-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-CV-kmeans-get-classes-3'>
<p><a id='tab-CV-kmeans-get-classes-3-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 4), get_membership(res, k = 4))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4
#&gt; SRR1383358     2   0.806     -0.167 0.004 0.364 0.320 0.312
#&gt; SRR1383360     4   0.729      0.508 0.036 0.180 0.156 0.628
#&gt; SRR1383359     4   0.801      0.223 0.004 0.292 0.304 0.400
#&gt; SRR1383362     1   0.274      0.839 0.912 0.008 0.040 0.040
#&gt; SRR1383361     4   0.768      0.310 0.004 0.348 0.192 0.456
#&gt; SRR1383363     2   0.804     -0.112 0.004 0.384 0.316 0.296
#&gt; SRR1383364     3   0.390      0.911 0.012 0.156 0.824 0.008
#&gt; SRR1383365     2   0.804     -0.135 0.004 0.380 0.316 0.300
#&gt; SRR1383366     4   0.710      0.458 0.004 0.232 0.180 0.584
#&gt; SRR1383367     4   0.765      0.307 0.004 0.348 0.188 0.460
#&gt; SRR1383368     4   0.810      0.471 0.060 0.204 0.176 0.560
#&gt; SRR1383369     3   0.417      0.842 0.000 0.212 0.776 0.012
#&gt; SRR1383370     4   0.764      0.301 0.004 0.356 0.184 0.456
#&gt; SRR1383371     3   0.390      0.911 0.012 0.156 0.824 0.008
#&gt; SRR1383372     2   0.538      0.305 0.000 0.736 0.176 0.088
#&gt; SRR1383373     2   0.613      0.119 0.000 0.644 0.268 0.088
#&gt; SRR1383374     2   0.436      0.395 0.000 0.812 0.124 0.064
#&gt; SRR1383375     1   0.667      0.687 0.648 0.012 0.124 0.216
#&gt; SRR1383376     2   0.607      0.379 0.008 0.504 0.028 0.460
#&gt; SRR1383377     4   0.533      0.595 0.032 0.124 0.064 0.780
#&gt; SRR1383378     2   0.473      0.636 0.000 0.752 0.032 0.216
#&gt; SRR1383379     4   0.315      0.635 0.072 0.036 0.004 0.888
#&gt; SRR1383380     4   0.376      0.624 0.116 0.004 0.032 0.848
#&gt; SRR1383381     3   0.474      0.890 0.016 0.212 0.760 0.012
#&gt; SRR1383382     1   0.274      0.839 0.912 0.008 0.040 0.040
#&gt; SRR1383383     2   0.511      0.625 0.000 0.740 0.056 0.204
#&gt; SRR1383385     1   0.266      0.835 0.908 0.000 0.036 0.056
#&gt; SRR1383384     2   0.456      0.594 0.000 0.672 0.000 0.328
#&gt; SRR1383386     4   0.478      0.622 0.132 0.032 0.032 0.804
#&gt; SRR1383387     4   0.358      0.498 0.000 0.180 0.004 0.816
#&gt; SRR1383389     2   0.380      0.609 0.004 0.848 0.036 0.112
#&gt; SRR1383391     2   0.516      0.631 0.008 0.752 0.048 0.192
#&gt; SRR1383388     4   0.367      0.636 0.084 0.028 0.020 0.868
#&gt; SRR1383392     2   0.442      0.595 0.000 0.736 0.008 0.256
#&gt; SRR1383390     2   0.422      0.634 0.000 0.792 0.024 0.184
#&gt; SRR1383394     2   0.607      0.379 0.008 0.504 0.028 0.460
#&gt; SRR1383393     1   0.667      0.687 0.648 0.012 0.124 0.216
#&gt; SRR1383396     4   0.687      0.545 0.096 0.164 0.060 0.680
#&gt; SRR1383395     4   0.533      0.595 0.032 0.124 0.064 0.780
#&gt; SRR1383399     3   0.474      0.890 0.016 0.212 0.760 0.012
#&gt; SRR1383400     1   0.274      0.839 0.912 0.008 0.040 0.040
#&gt; SRR1383397     4   0.315      0.635 0.072 0.036 0.004 0.888
#&gt; SRR1383401     2   0.500      0.623 0.000 0.752 0.056 0.192
#&gt; SRR1383398     4   0.376      0.624 0.116 0.004 0.032 0.848
#&gt; SRR1383402     2   0.456      0.594 0.000 0.672 0.000 0.328
#&gt; SRR1383404     4   0.478      0.622 0.132 0.032 0.032 0.804
#&gt; SRR1383403     1   0.266      0.835 0.908 0.000 0.036 0.056
#&gt; SRR1383405     4   0.358      0.498 0.000 0.180 0.004 0.816
#&gt; SRR1383406     4   0.315      0.635 0.072 0.036 0.004 0.888
#&gt; SRR1383407     2   0.380      0.609 0.004 0.848 0.036 0.112
#&gt; SRR1383408     2   0.422      0.634 0.000 0.792 0.024 0.184
#&gt; SRR1383409     2   0.516      0.631 0.008 0.752 0.048 0.192
#&gt; SRR1383410     2   0.470      0.593 0.000 0.676 0.004 0.320
</code></pre>

<script>
$('#tab-CV-kmeans-get-classes-3-a').parent().next().next().hide();
$('#tab-CV-kmeans-get-classes-3-a').click(function(){
  $('#tab-CV-kmeans-get-classes-3-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-CV-kmeans-get-classes-4'>
<p><a id='tab-CV-kmeans-get-classes-4-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 5), get_membership(res, k = 5))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4    p5
#&gt; SRR1383358     3   0.386      0.759 0.004 0.028 0.840 0.064 0.064
#&gt; SRR1383360     3   0.484      0.459 0.016 0.004 0.640 0.332 0.008
#&gt; SRR1383359     3   0.442      0.758 0.016 0.028 0.812 0.088 0.056
#&gt; SRR1383362     1   0.120      0.783 0.956 0.000 0.004 0.040 0.000
#&gt; SRR1383361     3   0.277      0.779 0.000 0.032 0.876 0.092 0.000
#&gt; SRR1383363     3   0.358      0.764 0.000 0.032 0.852 0.060 0.056
#&gt; SRR1383364     5   0.261      0.911 0.004 0.028 0.076 0.000 0.892
#&gt; SRR1383365     3   0.392      0.758 0.004 0.028 0.836 0.068 0.064
#&gt; SRR1383366     3   0.396      0.706 0.004 0.016 0.780 0.192 0.008
#&gt; SRR1383367     3   0.322      0.777 0.000 0.036 0.852 0.108 0.004
#&gt; SRR1383368     3   0.481      0.647 0.028 0.016 0.724 0.224 0.008
#&gt; SRR1383369     5   0.358      0.856 0.000 0.048 0.132 0.000 0.820
#&gt; SRR1383370     3   0.335      0.777 0.000 0.040 0.844 0.112 0.004
#&gt; SRR1383371     5   0.261      0.911 0.004 0.028 0.076 0.000 0.892
#&gt; SRR1383372     3   0.455      0.384 0.000 0.400 0.588 0.000 0.012
#&gt; SRR1383373     3   0.516      0.493 0.000 0.336 0.608 0.000 0.056
#&gt; SRR1383374     3   0.438      0.160 0.000 0.424 0.572 0.000 0.004
#&gt; SRR1383375     1   0.766      0.625 0.476 0.008 0.088 0.296 0.132
#&gt; SRR1383376     2   0.492      0.666 0.004 0.720 0.032 0.220 0.024
#&gt; SRR1383377     4   0.493      0.767 0.024 0.072 0.088 0.784 0.032
#&gt; SRR1383378     2   0.315      0.808 0.000 0.872 0.064 0.048 0.016
#&gt; SRR1383379     4   0.369      0.855 0.000 0.084 0.068 0.836 0.012
#&gt; SRR1383380     4   0.242      0.806 0.020 0.024 0.020 0.920 0.016
#&gt; SRR1383381     5   0.394      0.887 0.012 0.056 0.088 0.012 0.832
#&gt; SRR1383382     1   0.149      0.781 0.948 0.008 0.004 0.040 0.000
#&gt; SRR1383383     2   0.510      0.763 0.004 0.720 0.204 0.028 0.044
#&gt; SRR1383385     1   0.458      0.790 0.788 0.004 0.036 0.120 0.052
#&gt; SRR1383384     2   0.515      0.778 0.000 0.716 0.164 0.108 0.012
#&gt; SRR1383386     4   0.507      0.797 0.028 0.076 0.124 0.760 0.012
#&gt; SRR1383387     4   0.468      0.821 0.000 0.132 0.088 0.764 0.016
#&gt; SRR1383389     2   0.309      0.782 0.000 0.860 0.104 0.004 0.032
#&gt; SRR1383391     2   0.176      0.800 0.004 0.944 0.008 0.024 0.020
#&gt; SRR1383388     4   0.327      0.851 0.000 0.064 0.076 0.856 0.004
#&gt; SRR1383392     2   0.513      0.762 0.000 0.716 0.184 0.084 0.016
#&gt; SRR1383390     2   0.270      0.812 0.000 0.896 0.060 0.024 0.020
#&gt; SRR1383394     2   0.492      0.666 0.004 0.720 0.032 0.220 0.024
#&gt; SRR1383393     1   0.766      0.625 0.476 0.008 0.088 0.296 0.132
#&gt; SRR1383396     4   0.577      0.717 0.000 0.124 0.128 0.696 0.052
#&gt; SRR1383395     4   0.493      0.767 0.024 0.072 0.088 0.784 0.032
#&gt; SRR1383399     5   0.394      0.887 0.012 0.056 0.088 0.012 0.832
#&gt; SRR1383400     1   0.149      0.781 0.948 0.008 0.004 0.040 0.000
#&gt; SRR1383397     4   0.369      0.855 0.000 0.084 0.068 0.836 0.012
#&gt; SRR1383401     2   0.513      0.759 0.004 0.716 0.208 0.028 0.044
#&gt; SRR1383398     4   0.242      0.806 0.020 0.024 0.020 0.920 0.016
#&gt; SRR1383402     2   0.515      0.778 0.000 0.716 0.164 0.108 0.012
#&gt; SRR1383404     4   0.507      0.797 0.028 0.076 0.124 0.760 0.012
#&gt; SRR1383403     1   0.458      0.790 0.788 0.004 0.036 0.120 0.052
#&gt; SRR1383405     4   0.468      0.821 0.000 0.132 0.088 0.764 0.016
#&gt; SRR1383406     4   0.315      0.856 0.000 0.072 0.060 0.864 0.004
#&gt; SRR1383407     2   0.309      0.782 0.000 0.860 0.104 0.004 0.032
#&gt; SRR1383408     2   0.270      0.812 0.000 0.896 0.060 0.024 0.020
#&gt; SRR1383409     2   0.176      0.800 0.004 0.944 0.008 0.024 0.020
#&gt; SRR1383410     2   0.487      0.780 0.000 0.744 0.156 0.084 0.016
</code></pre>

<script>
$('#tab-CV-kmeans-get-classes-4-a').parent().next().next().hide();
$('#tab-CV-kmeans-get-classes-4-a').click(function(){
  $('#tab-CV-kmeans-get-classes-4-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-CV-kmeans-get-classes-5'>
<p><a id='tab-CV-kmeans-get-classes-5-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 6), get_membership(res, k = 6))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4    p5    p6
#&gt; SRR1383358     3  0.2378      0.789 0.028 0.008 0.908 0.024 0.032 0.000
#&gt; SRR1383360     3  0.3385      0.666 0.028 0.004 0.796 0.172 0.000 0.000
#&gt; SRR1383359     3  0.3508      0.757 0.084 0.004 0.840 0.032 0.036 0.004
#&gt; SRR1383362     6  0.0653      0.757 0.004 0.000 0.004 0.012 0.000 0.980
#&gt; SRR1383361     3  0.1639      0.798 0.008 0.008 0.940 0.036 0.008 0.000
#&gt; SRR1383363     3  0.1679      0.792 0.000 0.012 0.936 0.016 0.036 0.000
#&gt; SRR1383364     5  0.1536      0.892 0.000 0.016 0.040 0.000 0.940 0.004
#&gt; SRR1383365     3  0.2638      0.783 0.036 0.016 0.896 0.020 0.032 0.000
#&gt; SRR1383366     3  0.2339      0.778 0.020 0.012 0.896 0.072 0.000 0.000
#&gt; SRR1383367     3  0.1151      0.796 0.000 0.012 0.956 0.032 0.000 0.000
#&gt; SRR1383368     3  0.4216      0.685 0.064 0.016 0.792 0.108 0.004 0.016
#&gt; SRR1383369     5  0.2685      0.855 0.036 0.016 0.068 0.000 0.880 0.000
#&gt; SRR1383370     3  0.1151      0.796 0.000 0.012 0.956 0.032 0.000 0.000
#&gt; SRR1383371     5  0.1536      0.892 0.000 0.016 0.040 0.000 0.940 0.004
#&gt; SRR1383372     3  0.4487      0.369 0.024 0.420 0.552 0.000 0.004 0.000
#&gt; SRR1383373     3  0.5188      0.483 0.048 0.324 0.596 0.000 0.032 0.000
#&gt; SRR1383374     3  0.5501     -0.042 0.088 0.448 0.452 0.000 0.012 0.000
#&gt; SRR1383375     1  0.7473      1.000 0.336 0.000 0.020 0.248 0.068 0.328
#&gt; SRR1383376     2  0.6090      0.455 0.244 0.484 0.000 0.264 0.004 0.004
#&gt; SRR1383377     4  0.5919      0.502 0.296 0.028 0.076 0.580 0.016 0.004
#&gt; SRR1383378     2  0.4126      0.692 0.072 0.796 0.032 0.092 0.008 0.000
#&gt; SRR1383379     4  0.3005      0.706 0.092 0.036 0.016 0.856 0.000 0.000
#&gt; SRR1383380     4  0.3642      0.579 0.160 0.000 0.024 0.796 0.016 0.004
#&gt; SRR1383381     5  0.3859      0.854 0.116 0.056 0.016 0.000 0.804 0.008
#&gt; SRR1383382     6  0.0547      0.757 0.000 0.000 0.000 0.020 0.000 0.980
#&gt; SRR1383383     2  0.5885      0.695 0.148 0.672 0.096 0.040 0.040 0.004
#&gt; SRR1383385     6  0.4717      0.535 0.264 0.000 0.000 0.048 0.020 0.668
#&gt; SRR1383384     2  0.5785      0.708 0.108 0.656 0.100 0.132 0.004 0.000
#&gt; SRR1383386     4  0.5002      0.601 0.080 0.036 0.108 0.748 0.008 0.020
#&gt; SRR1383387     4  0.4009      0.674 0.112 0.076 0.024 0.788 0.000 0.000
#&gt; SRR1383389     2  0.3812      0.701 0.076 0.824 0.056 0.016 0.028 0.000
#&gt; SRR1383391     2  0.3867      0.700 0.140 0.800 0.008 0.028 0.020 0.004
#&gt; SRR1383388     4  0.3029      0.687 0.040 0.028 0.060 0.868 0.004 0.000
#&gt; SRR1383392     2  0.6434      0.681 0.192 0.588 0.100 0.108 0.012 0.000
#&gt; SRR1383390     2  0.1706      0.736 0.004 0.936 0.024 0.032 0.004 0.000
#&gt; SRR1383394     2  0.6090      0.455 0.244 0.484 0.000 0.264 0.004 0.004
#&gt; SRR1383393     1  0.7473      1.000 0.336 0.000 0.020 0.248 0.068 0.328
#&gt; SRR1383396     4  0.6580      0.411 0.144 0.140 0.084 0.600 0.032 0.000
#&gt; SRR1383395     4  0.5919      0.502 0.296 0.028 0.076 0.580 0.016 0.004
#&gt; SRR1383399     5  0.3859      0.854 0.116 0.056 0.016 0.000 0.804 0.008
#&gt; SRR1383400     6  0.0547      0.757 0.000 0.000 0.000 0.020 0.000 0.980
#&gt; SRR1383397     4  0.3005      0.706 0.092 0.036 0.016 0.856 0.000 0.000
#&gt; SRR1383401     2  0.5864      0.694 0.148 0.672 0.100 0.036 0.040 0.004
#&gt; SRR1383398     4  0.3642      0.579 0.160 0.000 0.024 0.796 0.016 0.004
#&gt; SRR1383402     2  0.5785      0.708 0.108 0.656 0.100 0.132 0.004 0.000
#&gt; SRR1383404     4  0.5002      0.601 0.080 0.036 0.108 0.748 0.008 0.020
#&gt; SRR1383403     6  0.4717      0.535 0.264 0.000 0.000 0.048 0.020 0.668
#&gt; SRR1383405     4  0.4009      0.674 0.112 0.076 0.024 0.788 0.000 0.000
#&gt; SRR1383406     4  0.2422      0.698 0.016 0.024 0.056 0.900 0.004 0.000
#&gt; SRR1383407     2  0.3812      0.701 0.076 0.824 0.056 0.016 0.028 0.000
#&gt; SRR1383408     2  0.1706      0.736 0.004 0.936 0.024 0.032 0.004 0.000
#&gt; SRR1383409     2  0.3867      0.700 0.140 0.800 0.008 0.028 0.020 0.004
#&gt; SRR1383410     2  0.6298      0.684 0.192 0.600 0.080 0.116 0.012 0.000
</code></pre>

<script>
$('#tab-CV-kmeans-get-classes-5-a').parent().next().next().hide();
$('#tab-CV-kmeans-get-classes-5-a').click(function(){
  $('#tab-CV-kmeans-get-classes-5-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>
</div>

Heatmaps for the consensus matrix. It visualizes the probability of two
samples to be in a same group.



<script>
$( function() {
	$( '#tabs-CV-kmeans-consensus-heatmap' ).tabs();
} );
</script>
<div id='tabs-CV-kmeans-consensus-heatmap'>
<ul>
<li><a href='#tab-CV-kmeans-consensus-heatmap-1'>k = 2</a></li>
<li><a href='#tab-CV-kmeans-consensus-heatmap-2'>k = 3</a></li>
<li><a href='#tab-CV-kmeans-consensus-heatmap-3'>k = 4</a></li>
<li><a href='#tab-CV-kmeans-consensus-heatmap-4'>k = 5</a></li>
<li><a href='#tab-CV-kmeans-consensus-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-CV-kmeans-consensus-heatmap-1'>
<pre><code class="r">consensus_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-CV-kmeans-consensus-heatmap-1-1.png" alt="plot of chunk tab-CV-kmeans-consensus-heatmap-1"/></p>

</div>
<div id='tab-CV-kmeans-consensus-heatmap-2'>
<pre><code class="r">consensus_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-CV-kmeans-consensus-heatmap-2-1.png" alt="plot of chunk tab-CV-kmeans-consensus-heatmap-2"/></p>

</div>
<div id='tab-CV-kmeans-consensus-heatmap-3'>
<pre><code class="r">consensus_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-CV-kmeans-consensus-heatmap-3-1.png" alt="plot of chunk tab-CV-kmeans-consensus-heatmap-3"/></p>

</div>
<div id='tab-CV-kmeans-consensus-heatmap-4'>
<pre><code class="r">consensus_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-CV-kmeans-consensus-heatmap-4-1.png" alt="plot of chunk tab-CV-kmeans-consensus-heatmap-4"/></p>

</div>
<div id='tab-CV-kmeans-consensus-heatmap-5'>
<pre><code class="r">consensus_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-CV-kmeans-consensus-heatmap-5-1.png" alt="plot of chunk tab-CV-kmeans-consensus-heatmap-5"/></p>

</div>
</div>

Heatmaps for the membership of samples in all partitions to see how consistent they are:




<script>
$( function() {
	$( '#tabs-CV-kmeans-membership-heatmap' ).tabs();
} );
</script>
<div id='tabs-CV-kmeans-membership-heatmap'>
<ul>
<li><a href='#tab-CV-kmeans-membership-heatmap-1'>k = 2</a></li>
<li><a href='#tab-CV-kmeans-membership-heatmap-2'>k = 3</a></li>
<li><a href='#tab-CV-kmeans-membership-heatmap-3'>k = 4</a></li>
<li><a href='#tab-CV-kmeans-membership-heatmap-4'>k = 5</a></li>
<li><a href='#tab-CV-kmeans-membership-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-CV-kmeans-membership-heatmap-1'>
<pre><code class="r">membership_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-CV-kmeans-membership-heatmap-1-1.png" alt="plot of chunk tab-CV-kmeans-membership-heatmap-1"/></p>

</div>
<div id='tab-CV-kmeans-membership-heatmap-2'>
<pre><code class="r">membership_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-CV-kmeans-membership-heatmap-2-1.png" alt="plot of chunk tab-CV-kmeans-membership-heatmap-2"/></p>

</div>
<div id='tab-CV-kmeans-membership-heatmap-3'>
<pre><code class="r">membership_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-CV-kmeans-membership-heatmap-3-1.png" alt="plot of chunk tab-CV-kmeans-membership-heatmap-3"/></p>

</div>
<div id='tab-CV-kmeans-membership-heatmap-4'>
<pre><code class="r">membership_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-CV-kmeans-membership-heatmap-4-1.png" alt="plot of chunk tab-CV-kmeans-membership-heatmap-4"/></p>

</div>
<div id='tab-CV-kmeans-membership-heatmap-5'>
<pre><code class="r">membership_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-CV-kmeans-membership-heatmap-5-1.png" alt="plot of chunk tab-CV-kmeans-membership-heatmap-5"/></p>

</div>
</div>

As soon as we have had the classes for columns, we can look for signatures
which are significantly different between classes which can be candidate marks
for certain classes. Following are the heatmaps for signatures.



Signature heatmaps where rows are scaled:



<script>
$( function() {
	$( '#tabs-CV-kmeans-get-signatures' ).tabs();
} );
</script>
<div id='tabs-CV-kmeans-get-signatures'>
<ul>
<li><a href='#tab-CV-kmeans-get-signatures-1'>k = 2</a></li>
<li><a href='#tab-CV-kmeans-get-signatures-2'>k = 3</a></li>
<li><a href='#tab-CV-kmeans-get-signatures-3'>k = 4</a></li>
<li><a href='#tab-CV-kmeans-get-signatures-4'>k = 5</a></li>
<li><a href='#tab-CV-kmeans-get-signatures-5'>k = 6</a></li>
</ul>
<div id='tab-CV-kmeans-get-signatures-1'>
<pre><code class="r">get_signatures(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-CV-kmeans-get-signatures-1-1.png" alt="plot of chunk tab-CV-kmeans-get-signatures-1"/></p>

</div>
<div id='tab-CV-kmeans-get-signatures-2'>
<pre><code class="r">get_signatures(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-CV-kmeans-get-signatures-2-1.png" alt="plot of chunk tab-CV-kmeans-get-signatures-2"/></p>

</div>
<div id='tab-CV-kmeans-get-signatures-3'>
<pre><code class="r">get_signatures(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-CV-kmeans-get-signatures-3-1.png" alt="plot of chunk tab-CV-kmeans-get-signatures-3"/></p>

</div>
<div id='tab-CV-kmeans-get-signatures-4'>
<pre><code class="r">get_signatures(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-CV-kmeans-get-signatures-4-1.png" alt="plot of chunk tab-CV-kmeans-get-signatures-4"/></p>

</div>
<div id='tab-CV-kmeans-get-signatures-5'>
<pre><code class="r">get_signatures(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-CV-kmeans-get-signatures-5-1.png" alt="plot of chunk tab-CV-kmeans-get-signatures-5"/></p>

</div>
</div>



Signature heatmaps where rows are not scaled:


<script>
$( function() {
	$( '#tabs-CV-kmeans-get-signatures-no-scale' ).tabs();
} );
</script>
<div id='tabs-CV-kmeans-get-signatures-no-scale'>
<ul>
<li><a href='#tab-CV-kmeans-get-signatures-no-scale-1'>k = 2</a></li>
<li><a href='#tab-CV-kmeans-get-signatures-no-scale-2'>k = 3</a></li>
<li><a href='#tab-CV-kmeans-get-signatures-no-scale-3'>k = 4</a></li>
<li><a href='#tab-CV-kmeans-get-signatures-no-scale-4'>k = 5</a></li>
<li><a href='#tab-CV-kmeans-get-signatures-no-scale-5'>k = 6</a></li>
</ul>
<div id='tab-CV-kmeans-get-signatures-no-scale-1'>
<pre><code class="r">get_signatures(res, k = 2, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-CV-kmeans-get-signatures-no-scale-1-1.png" alt="plot of chunk tab-CV-kmeans-get-signatures-no-scale-1"/></p>

</div>
<div id='tab-CV-kmeans-get-signatures-no-scale-2'>
<pre><code class="r">get_signatures(res, k = 3, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-CV-kmeans-get-signatures-no-scale-2-1.png" alt="plot of chunk tab-CV-kmeans-get-signatures-no-scale-2"/></p>

</div>
<div id='tab-CV-kmeans-get-signatures-no-scale-3'>
<pre><code class="r">get_signatures(res, k = 4, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-CV-kmeans-get-signatures-no-scale-3-1.png" alt="plot of chunk tab-CV-kmeans-get-signatures-no-scale-3"/></p>

</div>
<div id='tab-CV-kmeans-get-signatures-no-scale-4'>
<pre><code class="r">get_signatures(res, k = 5, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-CV-kmeans-get-signatures-no-scale-4-1.png" alt="plot of chunk tab-CV-kmeans-get-signatures-no-scale-4"/></p>

</div>
<div id='tab-CV-kmeans-get-signatures-no-scale-5'>
<pre><code class="r">get_signatures(res, k = 6, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-CV-kmeans-get-signatures-no-scale-5-1.png" alt="plot of chunk tab-CV-kmeans-get-signatures-no-scale-5"/></p>

</div>
</div>



Compare the overlap of signatures from different k:

```r
compare_signatures(res)
```

![plot of chunk CV-kmeans-signature_compare](figure_cola/CV-kmeans-signature_compare-1.png)

`get_signature()` returns a data frame invisibly. TO get the list of signatures, the function
call should be assigned to a variable explicitly. In following code, if `plot` argument is set
to `FALSE`, no heatmap is plotted while only the differential analysis is performed.

```r
# code only for demonstration
tb = get_signature(res, k = ..., plot = FALSE)
```

An example of the output of `tb` is:

```
#>   which_row         fdr    mean_1    mean_2 scaled_mean_1 scaled_mean_2 km
#> 1        38 0.042760348  8.373488  9.131774    -0.5533452     0.5164555  1
#> 2        40 0.018707592  7.106213  8.469186    -0.6173731     0.5762149  1
#> 3        55 0.019134737 10.221463 11.207825    -0.6159697     0.5749050  1
#> 4        59 0.006059896  5.921854  7.869574    -0.6899429     0.6439467  1
#> 5        60 0.018055526  8.928898 10.211722    -0.6204761     0.5791110  1
#> 6        98 0.009384629 15.714769 14.887706     0.6635654    -0.6193277  2
...
```

The columns in `tb` are:

1. `which_row`: row indices corresponding to the input matrix.
2. `fdr`: FDR for the differential test. 
3. `mean_x`: The mean value in group x.
4. `scaled_mean_x`: The mean value in group x after rows are scaled.
5. `km`: Row groups if k-means clustering is applied to rows.



UMAP plot which shows how samples are separated.


<script>
$( function() {
	$( '#tabs-CV-kmeans-dimension-reduction' ).tabs();
} );
</script>
<div id='tabs-CV-kmeans-dimension-reduction'>
<ul>
<li><a href='#tab-CV-kmeans-dimension-reduction-1'>k = 2</a></li>
<li><a href='#tab-CV-kmeans-dimension-reduction-2'>k = 3</a></li>
<li><a href='#tab-CV-kmeans-dimension-reduction-3'>k = 4</a></li>
<li><a href='#tab-CV-kmeans-dimension-reduction-4'>k = 5</a></li>
<li><a href='#tab-CV-kmeans-dimension-reduction-5'>k = 6</a></li>
</ul>
<div id='tab-CV-kmeans-dimension-reduction-1'>
<pre><code class="r">dimension_reduction(res, k = 2, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-CV-kmeans-dimension-reduction-1-1.png" alt="plot of chunk tab-CV-kmeans-dimension-reduction-1"/></p>

</div>
<div id='tab-CV-kmeans-dimension-reduction-2'>
<pre><code class="r">dimension_reduction(res, k = 3, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-CV-kmeans-dimension-reduction-2-1.png" alt="plot of chunk tab-CV-kmeans-dimension-reduction-2"/></p>

</div>
<div id='tab-CV-kmeans-dimension-reduction-3'>
<pre><code class="r">dimension_reduction(res, k = 4, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-CV-kmeans-dimension-reduction-3-1.png" alt="plot of chunk tab-CV-kmeans-dimension-reduction-3"/></p>

</div>
<div id='tab-CV-kmeans-dimension-reduction-4'>
<pre><code class="r">dimension_reduction(res, k = 5, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-CV-kmeans-dimension-reduction-4-1.png" alt="plot of chunk tab-CV-kmeans-dimension-reduction-4"/></p>

</div>
<div id='tab-CV-kmeans-dimension-reduction-5'>
<pre><code class="r">dimension_reduction(res, k = 6, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-CV-kmeans-dimension-reduction-5-1.png" alt="plot of chunk tab-CV-kmeans-dimension-reduction-5"/></p>

</div>
</div>


Following heatmap shows how subgroups are split when increasing `k`:

```r
collect_classes(res)
```

![plot of chunk CV-kmeans-collect-classes](figure_cola/CV-kmeans-collect-classes-1.png)


If matrix rows can be associated to genes, consider to use `functional_enrichment(res,
...)` to perform function enrichment for the signature genes. See [this vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/functional_enrichment.html) for more detailed explanations.


 

---------------------------------------------------




### CV:skmeans*






The object with results only for a single top-value method and a single partition method 
can be extracted as:

```r
res = res_list["CV", "skmeans"]
# you can also extract it by
# res = res_list["CV:skmeans"]
```

A summary of `res` and all the functions that can be applied to it:

```r
res
```

```
#> A 'ConsensusPartition' object with k = 2, 3, 4, 5, 6.
#>   On a matrix with 15680 rows and 53 columns.
#>   Top rows (1000, 2000, 3000, 4000, 5000) are extracted by 'CV' method.
#>   Subgroups are detected by 'skmeans' method.
#>   Performed in total 1250 partitions by row resampling.
#>   Best k for subgroups seems to be 2.
#> 
#> Following methods can be applied to this 'ConsensusPartition' object:
#>  [1] "cola_report"             "collect_classes"         "collect_plots"          
#>  [4] "collect_stats"           "colnames"                "compare_signatures"     
#>  [7] "consensus_heatmap"       "dimension_reduction"     "functional_enrichment"  
#> [10] "get_anno_col"            "get_anno"                "get_classes"            
#> [13] "get_consensus"           "get_matrix"              "get_membership"         
#> [16] "get_param"               "get_signatures"          "get_stats"              
#> [19] "is_best_k"               "is_stable_k"             "membership_heatmap"     
#> [22] "ncol"                    "nrow"                    "plot_ecdf"              
#> [25] "rownames"                "select_partition_number" "show"                   
#> [28] "suggest_best_k"          "test_to_known_factors"
```

`collect_plots()` function collects all the plots made from `res` for all `k` (number of partitions)
into one single page to provide an easy and fast comparison between different `k`.

```r
collect_plots(res)
```

![plot of chunk CV-skmeans-collect-plots](figure_cola/CV-skmeans-collect-plots-1.png)

The plots are:

- The first row: a plot of the ECDF (empirical cumulative distribution
  function) curves of the consensus matrix for each `k` and the heatmap of
  predicted classes for each `k`.
- The second row: heatmaps of the consensus matrix for each `k`.
- The third row: heatmaps of the membership matrix for each `k`.
- The fouth row: heatmaps of the signatures for each `k`.

All the plots in panels can be made by individual functions and they are
plotted later in this section.

`select_partition_number()` produces several plots showing different
statistics for choosing "optimized" `k`. There are following statistics:

- ECDF curves of the consensus matrix for each `k`;
- 1-PAC. [The PAC
  score](https://en.wikipedia.org/wiki/Consensus_clustering#Over-interpretation_potential_of_consensus_clustering)
  measures the proportion of the ambiguous subgrouping.
- Mean silhouette score.
- Concordance. The mean probability of fiting the consensus class ids in all
  partitions.
- Area increased. Denote $A_k$ as the area under the ECDF curve for current
  `k`, the area increased is defined as $A_k - A_{k-1}$.
- Rand index. The percent of pairs of samples that are both in a same cluster
  or both are not in a same cluster in the partition of k and k-1.
- Jaccard index. The ratio of pairs of samples are both in a same cluster in
  the partition of k and k-1 and the pairs of samples are both in a same
  cluster in the partition k or k-1.

The detailed explanations of these statistics can be found in [the _cola_
vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/cola.html#toc_13).

Generally speaking, lower PAC score, higher mean silhouette score or higher
concordance corresponds to better partition. Rand index and Jaccard index
measure how similar the current partition is compared to partition with `k-1`.
If they are too similar, we won't accept `k` is better than `k-1`.

```r
select_partition_number(res)
```

![plot of chunk CV-skmeans-select-partition-number](figure_cola/CV-skmeans-select-partition-number-1.png)

The numeric values for all these statistics can be obtained by `get_stats()`.

```r
get_stats(res)
```

```
#>   k 1-PAC mean_silhouette concordance area_increased  Rand Jaccard
#> 2 2 0.922           0.934       0.973         0.5006 0.499   0.499
#> 3 3 0.544           0.801       0.871         0.3505 0.714   0.483
#> 4 4 0.743           0.801       0.884         0.1234 0.882   0.655
#> 5 5 0.755           0.735       0.860         0.0611 0.903   0.638
#> 6 6 0.770           0.634       0.782         0.0396 0.946   0.738
```

`suggest_best_k()` suggests the best $k$ based on these statistics. The rules are as follows:

- All $k$ with Jaccard index larger than 0.95 are removed because increasing
  $k$ does not provide enough extra information. If all $k$ are removed, it is
  marked as no subgroup is detected.
- For all $k$ with 1-PAC score larger than 0.9, the maximal $k$ is taken as
  the best $k$, and other $k$ are marked as optional $k$.
- If it does not fit the second rule. The $k$ with the maximal vote of the
  highest 1-PAC score, highest mean silhouette, and highest concordance is
  taken as the best $k$.

```r
suggest_best_k(res)
```

```
#> [1] 2
```


Following shows the table of the partitions (You need to click the **show/hide
code output** link to see it). The membership matrix (columns with name `p*`)
is inferred by
[`clue::cl_consensus()`](https://www.rdocumentation.org/link/cl_consensus?package=clue)
function with the `SE` method. Basically the value in the membership matrix
represents the probability to belong to a certain group. The finall class
label for an item is determined with the group with highest probability it
belongs to.

In `get_classes()` function, the entropy is calculated from the membership
matrix and the silhouette score is calculated from the consensus matrix.



<script>
$( function() {
	$( '#tabs-CV-skmeans-get-classes' ).tabs();
} );
</script>
<div id='tabs-CV-skmeans-get-classes'>
<ul>
<li><a href='#tab-CV-skmeans-get-classes-1'>k = 2</a></li>
<li><a href='#tab-CV-skmeans-get-classes-2'>k = 3</a></li>
<li><a href='#tab-CV-skmeans-get-classes-3'>k = 4</a></li>
<li><a href='#tab-CV-skmeans-get-classes-4'>k = 5</a></li>
<li><a href='#tab-CV-skmeans-get-classes-5'>k = 6</a></li>
</ul>

<div id='tab-CV-skmeans-get-classes-1'>
<p><a id='tab-CV-skmeans-get-classes-1-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 2), get_membership(res, k = 2))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2
#&gt; SRR1383358     2   0.000      0.974 0.000 1.000
#&gt; SRR1383360     1   0.000      0.967 1.000 0.000
#&gt; SRR1383359     2   0.917      0.471 0.332 0.668
#&gt; SRR1383362     1   0.000      0.967 1.000 0.000
#&gt; SRR1383361     2   0.000      0.974 0.000 1.000
#&gt; SRR1383363     2   0.000      0.974 0.000 1.000
#&gt; SRR1383364     2   0.000      0.974 0.000 1.000
#&gt; SRR1383365     2   0.000      0.974 0.000 1.000
#&gt; SRR1383366     1   0.909      0.532 0.676 0.324
#&gt; SRR1383367     2   0.000      0.974 0.000 1.000
#&gt; SRR1383368     1   0.000      0.967 1.000 0.000
#&gt; SRR1383369     2   0.000      0.974 0.000 1.000
#&gt; SRR1383370     2   0.000      0.974 0.000 1.000
#&gt; SRR1383371     2   0.000      0.974 0.000 1.000
#&gt; SRR1383372     2   0.000      0.974 0.000 1.000
#&gt; SRR1383373     2   0.000      0.974 0.000 1.000
#&gt; SRR1383374     2   0.000      0.974 0.000 1.000
#&gt; SRR1383375     1   0.000      0.967 1.000 0.000
#&gt; SRR1383376     2   0.000      0.974 0.000 1.000
#&gt; SRR1383377     1   0.680      0.782 0.820 0.180
#&gt; SRR1383378     2   0.966      0.352 0.392 0.608
#&gt; SRR1383379     1   0.000      0.967 1.000 0.000
#&gt; SRR1383380     1   0.000      0.967 1.000 0.000
#&gt; SRR1383381     2   0.000      0.974 0.000 1.000
#&gt; SRR1383382     1   0.000      0.967 1.000 0.000
#&gt; SRR1383383     2   0.000      0.974 0.000 1.000
#&gt; SRR1383385     1   0.000      0.967 1.000 0.000
#&gt; SRR1383384     2   0.000      0.974 0.000 1.000
#&gt; SRR1383386     1   0.000      0.967 1.000 0.000
#&gt; SRR1383387     1   0.000      0.967 1.000 0.000
#&gt; SRR1383389     2   0.000      0.974 0.000 1.000
#&gt; SRR1383391     2   0.000      0.974 0.000 1.000
#&gt; SRR1383388     1   0.000      0.967 1.000 0.000
#&gt; SRR1383392     2   0.000      0.974 0.000 1.000
#&gt; SRR1383390     2   0.000      0.974 0.000 1.000
#&gt; SRR1383394     2   0.000      0.974 0.000 1.000
#&gt; SRR1383393     1   0.000      0.967 1.000 0.000
#&gt; SRR1383396     1   0.000      0.967 1.000 0.000
#&gt; SRR1383395     1   0.680      0.782 0.820 0.180
#&gt; SRR1383399     2   0.000      0.974 0.000 1.000
#&gt; SRR1383400     1   0.000      0.967 1.000 0.000
#&gt; SRR1383397     1   0.000      0.967 1.000 0.000
#&gt; SRR1383401     2   0.000      0.974 0.000 1.000
#&gt; SRR1383398     1   0.000      0.967 1.000 0.000
#&gt; SRR1383402     2   0.000      0.974 0.000 1.000
#&gt; SRR1383404     1   0.000      0.967 1.000 0.000
#&gt; SRR1383403     1   0.000      0.967 1.000 0.000
#&gt; SRR1383405     1   0.000      0.967 1.000 0.000
#&gt; SRR1383406     1   0.000      0.967 1.000 0.000
#&gt; SRR1383407     2   0.000      0.974 0.000 1.000
#&gt; SRR1383408     2   0.000      0.974 0.000 1.000
#&gt; SRR1383409     2   0.000      0.974 0.000 1.000
#&gt; SRR1383410     2   0.000      0.974 0.000 1.000
</code></pre>

<script>
$('#tab-CV-skmeans-get-classes-1-a').parent().next().next().hide();
$('#tab-CV-skmeans-get-classes-1-a').click(function(){
  $('#tab-CV-skmeans-get-classes-1-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-CV-skmeans-get-classes-2'>
<p><a id='tab-CV-skmeans-get-classes-2-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 3), get_membership(res, k = 3))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3
#&gt; SRR1383358     3  0.2711      0.806 0.000 0.088 0.912
#&gt; SRR1383360     1  0.4605      0.818 0.796 0.000 0.204
#&gt; SRR1383359     3  0.1643      0.775 0.000 0.044 0.956
#&gt; SRR1383362     1  0.0000      0.901 1.000 0.000 0.000
#&gt; SRR1383361     3  0.2711      0.795 0.000 0.088 0.912
#&gt; SRR1383363     3  0.3267      0.796 0.000 0.116 0.884
#&gt; SRR1383364     3  0.5961      0.768 0.136 0.076 0.788
#&gt; SRR1383365     3  0.3038      0.804 0.000 0.104 0.896
#&gt; SRR1383366     3  0.2537      0.750 0.000 0.080 0.920
#&gt; SRR1383367     3  0.2537      0.806 0.000 0.080 0.920
#&gt; SRR1383368     1  0.1860      0.862 0.948 0.000 0.052
#&gt; SRR1383369     3  0.4702      0.738 0.000 0.212 0.788
#&gt; SRR1383370     3  0.2959      0.794 0.000 0.100 0.900
#&gt; SRR1383371     3  0.5961      0.768 0.136 0.076 0.788
#&gt; SRR1383372     3  0.5988      0.504 0.000 0.368 0.632
#&gt; SRR1383373     3  0.4931      0.724 0.000 0.232 0.768
#&gt; SRR1383374     2  0.5098      0.671 0.000 0.752 0.248
#&gt; SRR1383375     1  0.0000      0.901 1.000 0.000 0.000
#&gt; SRR1383376     2  0.3192      0.821 0.000 0.888 0.112
#&gt; SRR1383377     3  0.8396      0.456 0.196 0.180 0.624
#&gt; SRR1383378     2  0.6096      0.689 0.208 0.752 0.040
#&gt; SRR1383379     1  0.6537      0.780 0.740 0.064 0.196
#&gt; SRR1383380     1  0.5677      0.826 0.792 0.048 0.160
#&gt; SRR1383381     3  0.6128      0.767 0.136 0.084 0.780
#&gt; SRR1383382     1  0.0000      0.901 1.000 0.000 0.000
#&gt; SRR1383383     2  0.2261      0.859 0.000 0.932 0.068
#&gt; SRR1383385     1  0.0000      0.901 1.000 0.000 0.000
#&gt; SRR1383384     2  0.1753      0.857 0.000 0.952 0.048
#&gt; SRR1383386     1  0.0000      0.901 1.000 0.000 0.000
#&gt; SRR1383387     2  0.5680      0.698 0.024 0.764 0.212
#&gt; SRR1383389     2  0.2878      0.846 0.000 0.904 0.096
#&gt; SRR1383391     2  0.2066      0.861 0.000 0.940 0.060
#&gt; SRR1383388     1  0.4233      0.845 0.836 0.004 0.160
#&gt; SRR1383392     2  0.1964      0.856 0.000 0.944 0.056
#&gt; SRR1383390     2  0.2448      0.856 0.000 0.924 0.076
#&gt; SRR1383394     2  0.3192      0.821 0.000 0.888 0.112
#&gt; SRR1383393     1  0.0000      0.901 1.000 0.000 0.000
#&gt; SRR1383396     1  0.0475      0.896 0.992 0.004 0.004
#&gt; SRR1383395     3  0.8396      0.456 0.196 0.180 0.624
#&gt; SRR1383399     3  0.6128      0.767 0.136 0.084 0.780
#&gt; SRR1383400     1  0.0000      0.901 1.000 0.000 0.000
#&gt; SRR1383397     1  0.6673      0.773 0.732 0.068 0.200
#&gt; SRR1383401     2  0.2796      0.846 0.000 0.908 0.092
#&gt; SRR1383398     1  0.5677      0.826 0.792 0.048 0.160
#&gt; SRR1383402     2  0.1753      0.857 0.000 0.952 0.048
#&gt; SRR1383404     1  0.0000      0.901 1.000 0.000 0.000
#&gt; SRR1383403     1  0.0000      0.901 1.000 0.000 0.000
#&gt; SRR1383405     2  0.5680      0.698 0.024 0.764 0.212
#&gt; SRR1383406     1  0.6027      0.815 0.776 0.060 0.164
#&gt; SRR1383407     2  0.2796      0.849 0.000 0.908 0.092
#&gt; SRR1383408     2  0.2448      0.856 0.000 0.924 0.076
#&gt; SRR1383409     2  0.2066      0.861 0.000 0.940 0.060
#&gt; SRR1383410     2  0.1753      0.857 0.000 0.952 0.048
</code></pre>

<script>
$('#tab-CV-skmeans-get-classes-2-a').parent().next().next().hide();
$('#tab-CV-skmeans-get-classes-2-a').click(function(){
  $('#tab-CV-skmeans-get-classes-2-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-CV-skmeans-get-classes-3'>
<p><a id='tab-CV-skmeans-get-classes-3-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 4), get_membership(res, k = 4))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4
#&gt; SRR1383358     3  0.0336      0.814 0.000 0.000 0.992 0.008
#&gt; SRR1383360     1  0.4274      0.831 0.820 0.000 0.108 0.072
#&gt; SRR1383359     3  0.0921      0.813 0.000 0.000 0.972 0.028
#&gt; SRR1383362     1  0.0469      0.965 0.988 0.000 0.000 0.012
#&gt; SRR1383361     3  0.0817      0.812 0.000 0.000 0.976 0.024
#&gt; SRR1383363     3  0.0376      0.814 0.000 0.004 0.992 0.004
#&gt; SRR1383364     3  0.4801      0.767 0.040 0.120 0.808 0.032
#&gt; SRR1383365     3  0.0469      0.814 0.000 0.000 0.988 0.012
#&gt; SRR1383366     3  0.4985      0.108 0.000 0.000 0.532 0.468
#&gt; SRR1383367     3  0.0779      0.814 0.000 0.004 0.980 0.016
#&gt; SRR1383368     1  0.2412      0.903 0.908 0.000 0.084 0.008
#&gt; SRR1383369     3  0.3526      0.790 0.004 0.100 0.864 0.032
#&gt; SRR1383370     3  0.4688      0.710 0.000 0.128 0.792 0.080
#&gt; SRR1383371     3  0.4631      0.773 0.040 0.108 0.820 0.032
#&gt; SRR1383372     3  0.4564      0.571 0.000 0.328 0.672 0.000
#&gt; SRR1383373     3  0.4164      0.666 0.000 0.264 0.736 0.000
#&gt; SRR1383374     2  0.4898      0.315 0.000 0.584 0.416 0.000
#&gt; SRR1383375     1  0.0188      0.965 0.996 0.000 0.000 0.004
#&gt; SRR1383376     2  0.4855      0.450 0.000 0.600 0.000 0.400
#&gt; SRR1383377     4  0.1004      0.943 0.024 0.004 0.000 0.972
#&gt; SRR1383378     2  0.2452      0.771 0.084 0.908 0.004 0.004
#&gt; SRR1383379     4  0.1118      0.951 0.036 0.000 0.000 0.964
#&gt; SRR1383380     4  0.2081      0.939 0.084 0.000 0.000 0.916
#&gt; SRR1383381     3  0.6238      0.647 0.048 0.244 0.676 0.032
#&gt; SRR1383382     1  0.0469      0.965 0.988 0.000 0.000 0.012
#&gt; SRR1383383     2  0.4652      0.648 0.004 0.756 0.220 0.020
#&gt; SRR1383385     1  0.0188      0.965 0.996 0.000 0.000 0.004
#&gt; SRR1383384     2  0.3833      0.793 0.000 0.848 0.080 0.072
#&gt; SRR1383386     1  0.0921      0.958 0.972 0.000 0.000 0.028
#&gt; SRR1383387     4  0.1118      0.931 0.000 0.036 0.000 0.964
#&gt; SRR1383389     2  0.0524      0.810 0.000 0.988 0.004 0.008
#&gt; SRR1383391     2  0.0188      0.813 0.000 0.996 0.000 0.004
#&gt; SRR1383388     4  0.3356      0.822 0.176 0.000 0.000 0.824
#&gt; SRR1383392     2  0.4700      0.769 0.000 0.792 0.084 0.124
#&gt; SRR1383390     2  0.0000      0.813 0.000 1.000 0.000 0.000
#&gt; SRR1383394     2  0.4855      0.450 0.000 0.600 0.000 0.400
#&gt; SRR1383393     1  0.0188      0.965 0.996 0.000 0.000 0.004
#&gt; SRR1383396     1  0.1492      0.930 0.956 0.036 0.004 0.004
#&gt; SRR1383395     4  0.1004      0.943 0.024 0.004 0.000 0.972
#&gt; SRR1383399     3  0.6238      0.647 0.048 0.244 0.676 0.032
#&gt; SRR1383400     1  0.0469      0.965 0.988 0.000 0.000 0.012
#&gt; SRR1383397     4  0.1118      0.951 0.036 0.000 0.000 0.964
#&gt; SRR1383401     2  0.4920      0.630 0.004 0.740 0.228 0.028
#&gt; SRR1383398     4  0.2081      0.939 0.084 0.000 0.000 0.916
#&gt; SRR1383402     2  0.3833      0.793 0.000 0.848 0.080 0.072
#&gt; SRR1383404     1  0.1022      0.956 0.968 0.000 0.000 0.032
#&gt; SRR1383403     1  0.0188      0.965 0.996 0.000 0.000 0.004
#&gt; SRR1383405     4  0.1118      0.931 0.000 0.036 0.000 0.964
#&gt; SRR1383406     4  0.1474      0.949 0.052 0.000 0.000 0.948
#&gt; SRR1383407     2  0.0524      0.810 0.000 0.988 0.004 0.008
#&gt; SRR1383408     2  0.0000      0.813 0.000 1.000 0.000 0.000
#&gt; SRR1383409     2  0.0188      0.813 0.000 0.996 0.000 0.004
#&gt; SRR1383410     2  0.4656      0.768 0.000 0.792 0.072 0.136
</code></pre>

<script>
$('#tab-CV-skmeans-get-classes-3-a').parent().next().next().hide();
$('#tab-CV-skmeans-get-classes-3-a').click(function(){
  $('#tab-CV-skmeans-get-classes-3-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-CV-skmeans-get-classes-4'>
<p><a id='tab-CV-skmeans-get-classes-4-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 5), get_membership(res, k = 5))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4    p5
#&gt; SRR1383358     3  0.1544     0.7777 0.000 0.000 0.932 0.000 0.068
#&gt; SRR1383360     3  0.4658     0.0116 0.484 0.000 0.504 0.012 0.000
#&gt; SRR1383359     3  0.1478     0.7775 0.000 0.000 0.936 0.000 0.064
#&gt; SRR1383362     1  0.0000     0.9218 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1383361     3  0.0404     0.7887 0.000 0.000 0.988 0.000 0.012
#&gt; SRR1383363     3  0.2329     0.7400 0.000 0.000 0.876 0.000 0.124
#&gt; SRR1383364     5  0.1864     0.7528 0.004 0.004 0.068 0.000 0.924
#&gt; SRR1383365     3  0.1410     0.7791 0.000 0.000 0.940 0.000 0.060
#&gt; SRR1383366     3  0.1502     0.7670 0.000 0.000 0.940 0.056 0.004
#&gt; SRR1383367     3  0.0324     0.7887 0.004 0.000 0.992 0.000 0.004
#&gt; SRR1383368     1  0.2280     0.8219 0.880 0.000 0.120 0.000 0.000
#&gt; SRR1383369     5  0.3961     0.6040 0.000 0.028 0.212 0.000 0.760
#&gt; SRR1383370     3  0.0798     0.7859 0.000 0.008 0.976 0.016 0.000
#&gt; SRR1383371     5  0.2112     0.7441 0.004 0.004 0.084 0.000 0.908
#&gt; SRR1383372     3  0.4558     0.5626 0.000 0.324 0.652 0.000 0.024
#&gt; SRR1383373     3  0.5213     0.5627 0.000 0.284 0.640 0.000 0.076
#&gt; SRR1383374     3  0.4356     0.4933 0.000 0.340 0.648 0.000 0.012
#&gt; SRR1383375     1  0.2595     0.8911 0.888 0.000 0.000 0.032 0.080
#&gt; SRR1383376     2  0.4618     0.4772 0.000 0.636 0.004 0.344 0.016
#&gt; SRR1383377     4  0.2414     0.9065 0.000 0.012 0.008 0.900 0.080
#&gt; SRR1383378     2  0.5759     0.4056 0.160 0.616 0.000 0.000 0.224
#&gt; SRR1383379     4  0.0854     0.9314 0.004 0.012 0.008 0.976 0.000
#&gt; SRR1383380     4  0.2122     0.9171 0.032 0.000 0.008 0.924 0.036
#&gt; SRR1383381     5  0.1605     0.7564 0.004 0.012 0.040 0.000 0.944
#&gt; SRR1383382     1  0.0000     0.9218 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1383383     5  0.5548     0.1046 0.000 0.464 0.048 0.008 0.480
#&gt; SRR1383385     1  0.1493     0.9132 0.948 0.000 0.000 0.028 0.024
#&gt; SRR1383384     2  0.3095     0.7390 0.000 0.868 0.092 0.024 0.016
#&gt; SRR1383386     1  0.0451     0.9202 0.988 0.000 0.000 0.008 0.004
#&gt; SRR1383387     4  0.1329     0.9225 0.000 0.032 0.008 0.956 0.004
#&gt; SRR1383389     2  0.3607     0.6013 0.000 0.752 0.004 0.000 0.244
#&gt; SRR1383391     2  0.0963     0.7609 0.000 0.964 0.000 0.000 0.036
#&gt; SRR1383388     4  0.3403     0.8031 0.160 0.000 0.012 0.820 0.008
#&gt; SRR1383392     2  0.3756     0.7307 0.000 0.836 0.096 0.032 0.036
#&gt; SRR1383390     2  0.1270     0.7552 0.000 0.948 0.000 0.000 0.052
#&gt; SRR1383394     2  0.4675     0.4438 0.000 0.620 0.004 0.360 0.016
#&gt; SRR1383393     1  0.2595     0.8911 0.888 0.000 0.000 0.032 0.080
#&gt; SRR1383396     1  0.4009     0.5744 0.684 0.000 0.000 0.004 0.312
#&gt; SRR1383395     4  0.2414     0.9065 0.000 0.012 0.008 0.900 0.080
#&gt; SRR1383399     5  0.1605     0.7564 0.004 0.012 0.040 0.000 0.944
#&gt; SRR1383400     1  0.0000     0.9218 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1383397     4  0.0854     0.9314 0.004 0.012 0.008 0.976 0.000
#&gt; SRR1383401     5  0.5747     0.1863 0.000 0.432 0.064 0.008 0.496
#&gt; SRR1383398     4  0.2122     0.9171 0.032 0.000 0.008 0.924 0.036
#&gt; SRR1383402     2  0.3095     0.7390 0.000 0.868 0.092 0.024 0.016
#&gt; SRR1383404     1  0.0451     0.9202 0.988 0.000 0.000 0.008 0.004
#&gt; SRR1383403     1  0.1493     0.9132 0.948 0.000 0.000 0.028 0.024
#&gt; SRR1383405     4  0.1329     0.9225 0.000 0.032 0.008 0.956 0.004
#&gt; SRR1383406     4  0.1383     0.9286 0.012 0.008 0.012 0.960 0.008
#&gt; SRR1383407     2  0.3579     0.6065 0.000 0.756 0.004 0.000 0.240
#&gt; SRR1383408     2  0.1270     0.7570 0.000 0.948 0.000 0.000 0.052
#&gt; SRR1383409     2  0.0963     0.7609 0.000 0.964 0.000 0.000 0.036
#&gt; SRR1383410     2  0.3201     0.7436 0.000 0.872 0.064 0.036 0.028
</code></pre>

<script>
$('#tab-CV-skmeans-get-classes-4-a').parent().next().next().hide();
$('#tab-CV-skmeans-get-classes-4-a').click(function(){
  $('#tab-CV-skmeans-get-classes-4-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-CV-skmeans-get-classes-5'>
<p><a id='tab-CV-skmeans-get-classes-5-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 6), get_membership(res, k = 6))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4    p5    p6
#&gt; SRR1383358     3  0.1297     0.8074 0.000 0.000 0.948 0.000 0.040 0.012
#&gt; SRR1383360     3  0.4787     0.3934 0.312 0.000 0.624 0.008 0.000 0.056
#&gt; SRR1383359     3  0.0964     0.8133 0.000 0.000 0.968 0.004 0.016 0.012
#&gt; SRR1383362     1  0.0146     0.8645 0.996 0.000 0.000 0.000 0.000 0.004
#&gt; SRR1383361     3  0.0653     0.8138 0.000 0.000 0.980 0.004 0.004 0.012
#&gt; SRR1383363     3  0.1753     0.7785 0.000 0.000 0.912 0.000 0.084 0.004
#&gt; SRR1383364     5  0.0405     0.9370 0.000 0.004 0.008 0.000 0.988 0.000
#&gt; SRR1383365     3  0.1649     0.8039 0.000 0.000 0.932 0.000 0.036 0.032
#&gt; SRR1383366     3  0.1092     0.8093 0.000 0.000 0.960 0.020 0.000 0.020
#&gt; SRR1383367     3  0.0146     0.8129 0.000 0.000 0.996 0.000 0.000 0.004
#&gt; SRR1383368     1  0.3301     0.7956 0.836 0.004 0.084 0.004 0.000 0.072
#&gt; SRR1383369     5  0.2925     0.8101 0.000 0.024 0.104 0.000 0.856 0.016
#&gt; SRR1383370     3  0.0363     0.8119 0.000 0.000 0.988 0.000 0.000 0.012
#&gt; SRR1383371     5  0.0363     0.9358 0.000 0.000 0.012 0.000 0.988 0.000
#&gt; SRR1383372     2  0.5512    -0.1427 0.000 0.460 0.452 0.000 0.032 0.056
#&gt; SRR1383373     3  0.5879     0.1147 0.000 0.400 0.476 0.000 0.088 0.036
#&gt; SRR1383374     3  0.6163    -0.0801 0.000 0.316 0.412 0.000 0.004 0.268
#&gt; SRR1383375     1  0.3703     0.8192 0.796 0.000 0.000 0.008 0.064 0.132
#&gt; SRR1383376     2  0.6126    -0.1343 0.000 0.352 0.000 0.316 0.000 0.332
#&gt; SRR1383377     4  0.3733     0.7596 0.000 0.000 0.004 0.700 0.008 0.288
#&gt; SRR1383378     2  0.5768     0.2886 0.100 0.672 0.004 0.008 0.084 0.132
#&gt; SRR1383379     4  0.1007     0.8209 0.000 0.000 0.000 0.956 0.000 0.044
#&gt; SRR1383380     4  0.3728     0.7882 0.012 0.000 0.008 0.748 0.004 0.228
#&gt; SRR1383381     5  0.0806     0.9321 0.000 0.008 0.000 0.000 0.972 0.020
#&gt; SRR1383382     1  0.0000     0.8646 1.000 0.000 0.000 0.000 0.000 0.000
#&gt; SRR1383383     6  0.6396     0.4400 0.000 0.292 0.012 0.000 0.328 0.368
#&gt; SRR1383385     1  0.2655     0.8389 0.848 0.000 0.000 0.004 0.008 0.140
#&gt; SRR1383384     6  0.5070     0.5419 0.000 0.468 0.024 0.032 0.000 0.476
#&gt; SRR1383386     1  0.1988     0.8445 0.912 0.004 0.004 0.008 0.000 0.072
#&gt; SRR1383387     4  0.2442     0.7711 0.000 0.004 0.000 0.852 0.000 0.144
#&gt; SRR1383389     2  0.3079     0.4327 0.000 0.844 0.004 0.000 0.096 0.056
#&gt; SRR1383391     2  0.1901     0.4222 0.000 0.912 0.000 0.008 0.004 0.076
#&gt; SRR1383388     4  0.3601     0.7711 0.084 0.004 0.016 0.824 0.000 0.072
#&gt; SRR1383392     6  0.4727     0.5497 0.000 0.400 0.024 0.016 0.000 0.560
#&gt; SRR1383390     2  0.1888     0.4095 0.000 0.916 0.004 0.000 0.012 0.068
#&gt; SRR1383394     2  0.6128    -0.1356 0.000 0.348 0.000 0.320 0.000 0.332
#&gt; SRR1383393     1  0.3703     0.8192 0.796 0.000 0.000 0.008 0.064 0.132
#&gt; SRR1383396     1  0.6344     0.4799 0.564 0.048 0.000 0.016 0.252 0.120
#&gt; SRR1383395     4  0.3733     0.7596 0.000 0.000 0.004 0.700 0.008 0.288
#&gt; SRR1383399     5  0.0806     0.9321 0.000 0.008 0.000 0.000 0.972 0.020
#&gt; SRR1383400     1  0.0000     0.8646 1.000 0.000 0.000 0.000 0.000 0.000
#&gt; SRR1383397     4  0.1007     0.8209 0.000 0.000 0.000 0.956 0.000 0.044
#&gt; SRR1383401     6  0.6381     0.4178 0.000 0.276 0.012 0.000 0.344 0.368
#&gt; SRR1383398     4  0.3728     0.7882 0.012 0.000 0.008 0.748 0.004 0.228
#&gt; SRR1383402     6  0.5070     0.5419 0.000 0.468 0.024 0.032 0.000 0.476
#&gt; SRR1383404     1  0.2182     0.8422 0.904 0.004 0.004 0.016 0.000 0.072
#&gt; SRR1383403     1  0.2655     0.8389 0.848 0.000 0.000 0.004 0.008 0.140
#&gt; SRR1383405     4  0.2442     0.7711 0.000 0.004 0.000 0.852 0.000 0.144
#&gt; SRR1383406     4  0.1672     0.8186 0.004 0.000 0.016 0.932 0.000 0.048
#&gt; SRR1383407     2  0.3079     0.4327 0.000 0.844 0.004 0.000 0.096 0.056
#&gt; SRR1383408     2  0.1843     0.3955 0.000 0.912 0.004 0.000 0.004 0.080
#&gt; SRR1383409     2  0.1732     0.4252 0.000 0.920 0.000 0.004 0.004 0.072
#&gt; SRR1383410     6  0.4654     0.5506 0.000 0.400 0.016 0.020 0.000 0.564
</code></pre>

<script>
$('#tab-CV-skmeans-get-classes-5-a').parent().next().next().hide();
$('#tab-CV-skmeans-get-classes-5-a').click(function(){
  $('#tab-CV-skmeans-get-classes-5-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>
</div>

Heatmaps for the consensus matrix. It visualizes the probability of two
samples to be in a same group.



<script>
$( function() {
	$( '#tabs-CV-skmeans-consensus-heatmap' ).tabs();
} );
</script>
<div id='tabs-CV-skmeans-consensus-heatmap'>
<ul>
<li><a href='#tab-CV-skmeans-consensus-heatmap-1'>k = 2</a></li>
<li><a href='#tab-CV-skmeans-consensus-heatmap-2'>k = 3</a></li>
<li><a href='#tab-CV-skmeans-consensus-heatmap-3'>k = 4</a></li>
<li><a href='#tab-CV-skmeans-consensus-heatmap-4'>k = 5</a></li>
<li><a href='#tab-CV-skmeans-consensus-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-CV-skmeans-consensus-heatmap-1'>
<pre><code class="r">consensus_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-CV-skmeans-consensus-heatmap-1-1.png" alt="plot of chunk tab-CV-skmeans-consensus-heatmap-1"/></p>

</div>
<div id='tab-CV-skmeans-consensus-heatmap-2'>
<pre><code class="r">consensus_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-CV-skmeans-consensus-heatmap-2-1.png" alt="plot of chunk tab-CV-skmeans-consensus-heatmap-2"/></p>

</div>
<div id='tab-CV-skmeans-consensus-heatmap-3'>
<pre><code class="r">consensus_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-CV-skmeans-consensus-heatmap-3-1.png" alt="plot of chunk tab-CV-skmeans-consensus-heatmap-3"/></p>

</div>
<div id='tab-CV-skmeans-consensus-heatmap-4'>
<pre><code class="r">consensus_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-CV-skmeans-consensus-heatmap-4-1.png" alt="plot of chunk tab-CV-skmeans-consensus-heatmap-4"/></p>

</div>
<div id='tab-CV-skmeans-consensus-heatmap-5'>
<pre><code class="r">consensus_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-CV-skmeans-consensus-heatmap-5-1.png" alt="plot of chunk tab-CV-skmeans-consensus-heatmap-5"/></p>

</div>
</div>

Heatmaps for the membership of samples in all partitions to see how consistent they are:




<script>
$( function() {
	$( '#tabs-CV-skmeans-membership-heatmap' ).tabs();
} );
</script>
<div id='tabs-CV-skmeans-membership-heatmap'>
<ul>
<li><a href='#tab-CV-skmeans-membership-heatmap-1'>k = 2</a></li>
<li><a href='#tab-CV-skmeans-membership-heatmap-2'>k = 3</a></li>
<li><a href='#tab-CV-skmeans-membership-heatmap-3'>k = 4</a></li>
<li><a href='#tab-CV-skmeans-membership-heatmap-4'>k = 5</a></li>
<li><a href='#tab-CV-skmeans-membership-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-CV-skmeans-membership-heatmap-1'>
<pre><code class="r">membership_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-CV-skmeans-membership-heatmap-1-1.png" alt="plot of chunk tab-CV-skmeans-membership-heatmap-1"/></p>

</div>
<div id='tab-CV-skmeans-membership-heatmap-2'>
<pre><code class="r">membership_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-CV-skmeans-membership-heatmap-2-1.png" alt="plot of chunk tab-CV-skmeans-membership-heatmap-2"/></p>

</div>
<div id='tab-CV-skmeans-membership-heatmap-3'>
<pre><code class="r">membership_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-CV-skmeans-membership-heatmap-3-1.png" alt="plot of chunk tab-CV-skmeans-membership-heatmap-3"/></p>

</div>
<div id='tab-CV-skmeans-membership-heatmap-4'>
<pre><code class="r">membership_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-CV-skmeans-membership-heatmap-4-1.png" alt="plot of chunk tab-CV-skmeans-membership-heatmap-4"/></p>

</div>
<div id='tab-CV-skmeans-membership-heatmap-5'>
<pre><code class="r">membership_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-CV-skmeans-membership-heatmap-5-1.png" alt="plot of chunk tab-CV-skmeans-membership-heatmap-5"/></p>

</div>
</div>

As soon as we have had the classes for columns, we can look for signatures
which are significantly different between classes which can be candidate marks
for certain classes. Following are the heatmaps for signatures.



Signature heatmaps where rows are scaled:



<script>
$( function() {
	$( '#tabs-CV-skmeans-get-signatures' ).tabs();
} );
</script>
<div id='tabs-CV-skmeans-get-signatures'>
<ul>
<li><a href='#tab-CV-skmeans-get-signatures-1'>k = 2</a></li>
<li><a href='#tab-CV-skmeans-get-signatures-2'>k = 3</a></li>
<li><a href='#tab-CV-skmeans-get-signatures-3'>k = 4</a></li>
<li><a href='#tab-CV-skmeans-get-signatures-4'>k = 5</a></li>
<li><a href='#tab-CV-skmeans-get-signatures-5'>k = 6</a></li>
</ul>
<div id='tab-CV-skmeans-get-signatures-1'>
<pre><code class="r">get_signatures(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-CV-skmeans-get-signatures-1-1.png" alt="plot of chunk tab-CV-skmeans-get-signatures-1"/></p>

</div>
<div id='tab-CV-skmeans-get-signatures-2'>
<pre><code class="r">get_signatures(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-CV-skmeans-get-signatures-2-1.png" alt="plot of chunk tab-CV-skmeans-get-signatures-2"/></p>

</div>
<div id='tab-CV-skmeans-get-signatures-3'>
<pre><code class="r">get_signatures(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-CV-skmeans-get-signatures-3-1.png" alt="plot of chunk tab-CV-skmeans-get-signatures-3"/></p>

</div>
<div id='tab-CV-skmeans-get-signatures-4'>
<pre><code class="r">get_signatures(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-CV-skmeans-get-signatures-4-1.png" alt="plot of chunk tab-CV-skmeans-get-signatures-4"/></p>

</div>
<div id='tab-CV-skmeans-get-signatures-5'>
<pre><code class="r">get_signatures(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-CV-skmeans-get-signatures-5-1.png" alt="plot of chunk tab-CV-skmeans-get-signatures-5"/></p>

</div>
</div>



Signature heatmaps where rows are not scaled:


<script>
$( function() {
	$( '#tabs-CV-skmeans-get-signatures-no-scale' ).tabs();
} );
</script>
<div id='tabs-CV-skmeans-get-signatures-no-scale'>
<ul>
<li><a href='#tab-CV-skmeans-get-signatures-no-scale-1'>k = 2</a></li>
<li><a href='#tab-CV-skmeans-get-signatures-no-scale-2'>k = 3</a></li>
<li><a href='#tab-CV-skmeans-get-signatures-no-scale-3'>k = 4</a></li>
<li><a href='#tab-CV-skmeans-get-signatures-no-scale-4'>k = 5</a></li>
<li><a href='#tab-CV-skmeans-get-signatures-no-scale-5'>k = 6</a></li>
</ul>
<div id='tab-CV-skmeans-get-signatures-no-scale-1'>
<pre><code class="r">get_signatures(res, k = 2, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-CV-skmeans-get-signatures-no-scale-1-1.png" alt="plot of chunk tab-CV-skmeans-get-signatures-no-scale-1"/></p>

</div>
<div id='tab-CV-skmeans-get-signatures-no-scale-2'>
<pre><code class="r">get_signatures(res, k = 3, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-CV-skmeans-get-signatures-no-scale-2-1.png" alt="plot of chunk tab-CV-skmeans-get-signatures-no-scale-2"/></p>

</div>
<div id='tab-CV-skmeans-get-signatures-no-scale-3'>
<pre><code class="r">get_signatures(res, k = 4, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-CV-skmeans-get-signatures-no-scale-3-1.png" alt="plot of chunk tab-CV-skmeans-get-signatures-no-scale-3"/></p>

</div>
<div id='tab-CV-skmeans-get-signatures-no-scale-4'>
<pre><code class="r">get_signatures(res, k = 5, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-CV-skmeans-get-signatures-no-scale-4-1.png" alt="plot of chunk tab-CV-skmeans-get-signatures-no-scale-4"/></p>

</div>
<div id='tab-CV-skmeans-get-signatures-no-scale-5'>
<pre><code class="r">get_signatures(res, k = 6, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-CV-skmeans-get-signatures-no-scale-5-1.png" alt="plot of chunk tab-CV-skmeans-get-signatures-no-scale-5"/></p>

</div>
</div>



Compare the overlap of signatures from different k:

```r
compare_signatures(res)
```

![plot of chunk CV-skmeans-signature_compare](figure_cola/CV-skmeans-signature_compare-1.png)

`get_signature()` returns a data frame invisibly. TO get the list of signatures, the function
call should be assigned to a variable explicitly. In following code, if `plot` argument is set
to `FALSE`, no heatmap is plotted while only the differential analysis is performed.

```r
# code only for demonstration
tb = get_signature(res, k = ..., plot = FALSE)
```

An example of the output of `tb` is:

```
#>   which_row         fdr    mean_1    mean_2 scaled_mean_1 scaled_mean_2 km
#> 1        38 0.042760348  8.373488  9.131774    -0.5533452     0.5164555  1
#> 2        40 0.018707592  7.106213  8.469186    -0.6173731     0.5762149  1
#> 3        55 0.019134737 10.221463 11.207825    -0.6159697     0.5749050  1
#> 4        59 0.006059896  5.921854  7.869574    -0.6899429     0.6439467  1
#> 5        60 0.018055526  8.928898 10.211722    -0.6204761     0.5791110  1
#> 6        98 0.009384629 15.714769 14.887706     0.6635654    -0.6193277  2
...
```

The columns in `tb` are:

1. `which_row`: row indices corresponding to the input matrix.
2. `fdr`: FDR for the differential test. 
3. `mean_x`: The mean value in group x.
4. `scaled_mean_x`: The mean value in group x after rows are scaled.
5. `km`: Row groups if k-means clustering is applied to rows.



UMAP plot which shows how samples are separated.


<script>
$( function() {
	$( '#tabs-CV-skmeans-dimension-reduction' ).tabs();
} );
</script>
<div id='tabs-CV-skmeans-dimension-reduction'>
<ul>
<li><a href='#tab-CV-skmeans-dimension-reduction-1'>k = 2</a></li>
<li><a href='#tab-CV-skmeans-dimension-reduction-2'>k = 3</a></li>
<li><a href='#tab-CV-skmeans-dimension-reduction-3'>k = 4</a></li>
<li><a href='#tab-CV-skmeans-dimension-reduction-4'>k = 5</a></li>
<li><a href='#tab-CV-skmeans-dimension-reduction-5'>k = 6</a></li>
</ul>
<div id='tab-CV-skmeans-dimension-reduction-1'>
<pre><code class="r">dimension_reduction(res, k = 2, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-CV-skmeans-dimension-reduction-1-1.png" alt="plot of chunk tab-CV-skmeans-dimension-reduction-1"/></p>

</div>
<div id='tab-CV-skmeans-dimension-reduction-2'>
<pre><code class="r">dimension_reduction(res, k = 3, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-CV-skmeans-dimension-reduction-2-1.png" alt="plot of chunk tab-CV-skmeans-dimension-reduction-2"/></p>

</div>
<div id='tab-CV-skmeans-dimension-reduction-3'>
<pre><code class="r">dimension_reduction(res, k = 4, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-CV-skmeans-dimension-reduction-3-1.png" alt="plot of chunk tab-CV-skmeans-dimension-reduction-3"/></p>

</div>
<div id='tab-CV-skmeans-dimension-reduction-4'>
<pre><code class="r">dimension_reduction(res, k = 5, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-CV-skmeans-dimension-reduction-4-1.png" alt="plot of chunk tab-CV-skmeans-dimension-reduction-4"/></p>

</div>
<div id='tab-CV-skmeans-dimension-reduction-5'>
<pre><code class="r">dimension_reduction(res, k = 6, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-CV-skmeans-dimension-reduction-5-1.png" alt="plot of chunk tab-CV-skmeans-dimension-reduction-5"/></p>

</div>
</div>


Following heatmap shows how subgroups are split when increasing `k`:

```r
collect_classes(res)
```

![plot of chunk CV-skmeans-collect-classes](figure_cola/CV-skmeans-collect-classes-1.png)


If matrix rows can be associated to genes, consider to use `functional_enrichment(res,
...)` to perform function enrichment for the signature genes. See [this vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/functional_enrichment.html) for more detailed explanations.


 

---------------------------------------------------




### CV:pam






The object with results only for a single top-value method and a single partition method 
can be extracted as:

```r
res = res_list["CV", "pam"]
# you can also extract it by
# res = res_list["CV:pam"]
```

A summary of `res` and all the functions that can be applied to it:

```r
res
```

```
#> A 'ConsensusPartition' object with k = 2, 3, 4, 5, 6.
#>   On a matrix with 15680 rows and 53 columns.
#>   Top rows (1000, 2000, 3000, 4000, 5000) are extracted by 'CV' method.
#>   Subgroups are detected by 'pam' method.
#>   Performed in total 1250 partitions by row resampling.
#>   Best k for subgroups seems to be 2.
#> 
#> Following methods can be applied to this 'ConsensusPartition' object:
#>  [1] "cola_report"             "collect_classes"         "collect_plots"          
#>  [4] "collect_stats"           "colnames"                "compare_signatures"     
#>  [7] "consensus_heatmap"       "dimension_reduction"     "functional_enrichment"  
#> [10] "get_anno_col"            "get_anno"                "get_classes"            
#> [13] "get_consensus"           "get_matrix"              "get_membership"         
#> [16] "get_param"               "get_signatures"          "get_stats"              
#> [19] "is_best_k"               "is_stable_k"             "membership_heatmap"     
#> [22] "ncol"                    "nrow"                    "plot_ecdf"              
#> [25] "rownames"                "select_partition_number" "show"                   
#> [28] "suggest_best_k"          "test_to_known_factors"
```

`collect_plots()` function collects all the plots made from `res` for all `k` (number of partitions)
into one single page to provide an easy and fast comparison between different `k`.

```r
collect_plots(res)
```

![plot of chunk CV-pam-collect-plots](figure_cola/CV-pam-collect-plots-1.png)

The plots are:

- The first row: a plot of the ECDF (empirical cumulative distribution
  function) curves of the consensus matrix for each `k` and the heatmap of
  predicted classes for each `k`.
- The second row: heatmaps of the consensus matrix for each `k`.
- The third row: heatmaps of the membership matrix for each `k`.
- The fouth row: heatmaps of the signatures for each `k`.

All the plots in panels can be made by individual functions and they are
plotted later in this section.

`select_partition_number()` produces several plots showing different
statistics for choosing "optimized" `k`. There are following statistics:

- ECDF curves of the consensus matrix for each `k`;
- 1-PAC. [The PAC
  score](https://en.wikipedia.org/wiki/Consensus_clustering#Over-interpretation_potential_of_consensus_clustering)
  measures the proportion of the ambiguous subgrouping.
- Mean silhouette score.
- Concordance. The mean probability of fiting the consensus class ids in all
  partitions.
- Area increased. Denote $A_k$ as the area under the ECDF curve for current
  `k`, the area increased is defined as $A_k - A_{k-1}$.
- Rand index. The percent of pairs of samples that are both in a same cluster
  or both are not in a same cluster in the partition of k and k-1.
- Jaccard index. The ratio of pairs of samples are both in a same cluster in
  the partition of k and k-1 and the pairs of samples are both in a same
  cluster in the partition k or k-1.

The detailed explanations of these statistics can be found in [the _cola_
vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/cola.html#toc_13).

Generally speaking, lower PAC score, higher mean silhouette score or higher
concordance corresponds to better partition. Rand index and Jaccard index
measure how similar the current partition is compared to partition with `k-1`.
If they are too similar, we won't accept `k` is better than `k-1`.

```r
select_partition_number(res)
```

![plot of chunk CV-pam-select-partition-number](figure_cola/CV-pam-select-partition-number-1.png)

The numeric values for all these statistics can be obtained by `get_stats()`.

```r
get_stats(res)
```

```
#>   k 1-PAC mean_silhouette concordance area_increased  Rand Jaccard
#> 2 2 0.429           0.743       0.846         0.4683 0.543   0.543
#> 3 3 0.469           0.727       0.846         0.2001 0.910   0.834
#> 4 4 0.481           0.446       0.725         0.1741 0.766   0.535
#> 5 5 0.597           0.664       0.849         0.0970 0.829   0.550
#> 6 6 0.667           0.638       0.846         0.0647 0.930   0.755
```

`suggest_best_k()` suggests the best $k$ based on these statistics. The rules are as follows:

- All $k$ with Jaccard index larger than 0.95 are removed because increasing
  $k$ does not provide enough extra information. If all $k$ are removed, it is
  marked as no subgroup is detected.
- For all $k$ with 1-PAC score larger than 0.9, the maximal $k$ is taken as
  the best $k$, and other $k$ are marked as optional $k$.
- If it does not fit the second rule. The $k$ with the maximal vote of the
  highest 1-PAC score, highest mean silhouette, and highest concordance is
  taken as the best $k$.

```r
suggest_best_k(res)
```

```
#> [1] 2
```


Following shows the table of the partitions (You need to click the **show/hide
code output** link to see it). The membership matrix (columns with name `p*`)
is inferred by
[`clue::cl_consensus()`](https://www.rdocumentation.org/link/cl_consensus?package=clue)
function with the `SE` method. Basically the value in the membership matrix
represents the probability to belong to a certain group. The finall class
label for an item is determined with the group with highest probability it
belongs to.

In `get_classes()` function, the entropy is calculated from the membership
matrix and the silhouette score is calculated from the consensus matrix.



<script>
$( function() {
	$( '#tabs-CV-pam-get-classes' ).tabs();
} );
</script>
<div id='tabs-CV-pam-get-classes'>
<ul>
<li><a href='#tab-CV-pam-get-classes-1'>k = 2</a></li>
<li><a href='#tab-CV-pam-get-classes-2'>k = 3</a></li>
<li><a href='#tab-CV-pam-get-classes-3'>k = 4</a></li>
<li><a href='#tab-CV-pam-get-classes-4'>k = 5</a></li>
<li><a href='#tab-CV-pam-get-classes-5'>k = 6</a></li>
</ul>

<div id='tab-CV-pam-get-classes-1'>
<p><a id='tab-CV-pam-get-classes-1-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 2), get_membership(res, k = 2))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2
#&gt; SRR1383358     2  0.6712      0.780 0.176 0.824
#&gt; SRR1383360     2  0.6438      0.773 0.164 0.836
#&gt; SRR1383359     2  0.0672      0.791 0.008 0.992
#&gt; SRR1383362     1  0.0672      0.817 0.992 0.008
#&gt; SRR1383361     2  0.5178      0.793 0.116 0.884
#&gt; SRR1383363     2  0.9087      0.706 0.324 0.676
#&gt; SRR1383364     1  0.3274      0.824 0.940 0.060
#&gt; SRR1383365     2  0.8763      0.729 0.296 0.704
#&gt; SRR1383366     2  0.0672      0.788 0.008 0.992
#&gt; SRR1383367     2  0.8861      0.724 0.304 0.696
#&gt; SRR1383368     1  0.9850     -0.263 0.572 0.428
#&gt; SRR1383369     2  0.8861      0.723 0.304 0.696
#&gt; SRR1383370     2  0.0938      0.791 0.012 0.988
#&gt; SRR1383371     2  0.9170      0.697 0.332 0.668
#&gt; SRR1383372     1  0.3274      0.824 0.940 0.060
#&gt; SRR1383373     2  0.9087      0.706 0.324 0.676
#&gt; SRR1383374     2  0.8861      0.723 0.304 0.696
#&gt; SRR1383375     1  0.0376      0.818 0.996 0.004
#&gt; SRR1383376     1  0.9552      0.628 0.624 0.376
#&gt; SRR1383377     2  0.1184      0.792 0.016 0.984
#&gt; SRR1383378     1  0.2778      0.824 0.952 0.048
#&gt; SRR1383379     2  0.3584      0.763 0.068 0.932
#&gt; SRR1383380     1  0.8608      0.658 0.716 0.284
#&gt; SRR1383381     1  0.3274      0.824 0.940 0.060
#&gt; SRR1383382     1  0.0672      0.817 0.992 0.008
#&gt; SRR1383383     1  0.4161      0.815 0.916 0.084
#&gt; SRR1383385     1  0.0672      0.817 0.992 0.008
#&gt; SRR1383384     1  0.8327      0.720 0.736 0.264
#&gt; SRR1383386     1  0.0376      0.818 0.996 0.004
#&gt; SRR1383387     1  0.9552      0.628 0.624 0.376
#&gt; SRR1383389     1  0.3274      0.824 0.940 0.060
#&gt; SRR1383391     1  0.3274      0.824 0.940 0.060
#&gt; SRR1383388     1  0.4815      0.786 0.896 0.104
#&gt; SRR1383392     2  0.0672      0.789 0.008 0.992
#&gt; SRR1383390     1  0.3274      0.824 0.940 0.060
#&gt; SRR1383394     1  0.9552      0.628 0.624 0.376
#&gt; SRR1383393     1  0.0376      0.818 0.996 0.004
#&gt; SRR1383396     1  0.0672      0.819 0.992 0.008
#&gt; SRR1383395     2  0.1184      0.792 0.016 0.984
#&gt; SRR1383399     1  0.3274      0.824 0.940 0.060
#&gt; SRR1383400     1  0.0672      0.817 0.992 0.008
#&gt; SRR1383397     2  0.3431      0.764 0.064 0.936
#&gt; SRR1383401     1  0.4161      0.815 0.916 0.084
#&gt; SRR1383398     1  0.8861      0.638 0.696 0.304
#&gt; SRR1383402     1  0.9522      0.633 0.628 0.372
#&gt; SRR1383404     1  0.5946      0.764 0.856 0.144
#&gt; SRR1383403     1  0.1184      0.817 0.984 0.016
#&gt; SRR1383405     1  0.9552      0.628 0.624 0.376
#&gt; SRR1383406     1  0.9044      0.621 0.680 0.320
#&gt; SRR1383407     1  0.3274      0.824 0.940 0.060
#&gt; SRR1383408     1  0.3274      0.824 0.940 0.060
#&gt; SRR1383409     1  0.3431      0.823 0.936 0.064
#&gt; SRR1383410     1  0.9580      0.625 0.620 0.380
</code></pre>

<script>
$('#tab-CV-pam-get-classes-1-a').parent().next().next().hide();
$('#tab-CV-pam-get-classes-1-a').click(function(){
  $('#tab-CV-pam-get-classes-1-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-CV-pam-get-classes-2'>
<p><a id='tab-CV-pam-get-classes-2-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 3), get_membership(res, k = 3))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3
#&gt; SRR1383358     3  0.4121      0.762 0.000 0.168 0.832
#&gt; SRR1383360     3  0.4799      0.742 0.032 0.132 0.836
#&gt; SRR1383359     3  0.0237      0.755 0.000 0.004 0.996
#&gt; SRR1383362     1  0.0592      0.896 0.988 0.012 0.000
#&gt; SRR1383361     3  0.3192      0.769 0.000 0.112 0.888
#&gt; SRR1383363     3  0.5905      0.677 0.000 0.352 0.648
#&gt; SRR1383364     2  0.0829      0.795 0.012 0.984 0.004
#&gt; SRR1383365     3  0.5497      0.720 0.000 0.292 0.708
#&gt; SRR1383366     3  0.0000      0.752 0.000 0.000 1.000
#&gt; SRR1383367     3  0.5560      0.715 0.000 0.300 0.700
#&gt; SRR1383368     2  0.7329     -0.277 0.032 0.544 0.424
#&gt; SRR1383369     3  0.5560      0.715 0.000 0.300 0.700
#&gt; SRR1383370     3  0.0237      0.755 0.000 0.004 0.996
#&gt; SRR1383371     3  0.6490      0.665 0.012 0.360 0.628
#&gt; SRR1383372     2  0.0592      0.798 0.000 0.988 0.012
#&gt; SRR1383373     3  0.5926      0.676 0.000 0.356 0.644
#&gt; SRR1383374     3  0.5591      0.714 0.000 0.304 0.696
#&gt; SRR1383375     2  0.1289      0.787 0.032 0.968 0.000
#&gt; SRR1383376     2  0.5968      0.643 0.000 0.636 0.364
#&gt; SRR1383377     3  0.0892      0.755 0.000 0.020 0.980
#&gt; SRR1383378     2  0.0424      0.798 0.000 0.992 0.008
#&gt; SRR1383379     3  0.1877      0.732 0.032 0.012 0.956
#&gt; SRR1383380     2  0.5623      0.679 0.004 0.716 0.280
#&gt; SRR1383381     2  0.0592      0.795 0.012 0.988 0.000
#&gt; SRR1383382     1  0.2711      0.940 0.912 0.088 0.000
#&gt; SRR1383383     2  0.2711      0.776 0.000 0.912 0.088
#&gt; SRR1383385     1  0.2625      0.917 0.916 0.084 0.000
#&gt; SRR1383384     2  0.5098      0.719 0.000 0.752 0.248
#&gt; SRR1383386     2  0.1289      0.787 0.032 0.968 0.000
#&gt; SRR1383387     2  0.6899      0.635 0.024 0.612 0.364
#&gt; SRR1383389     2  0.0592      0.798 0.000 0.988 0.012
#&gt; SRR1383391     2  0.0592      0.798 0.000 0.988 0.012
#&gt; SRR1383388     2  0.4217      0.771 0.032 0.868 0.100
#&gt; SRR1383392     3  0.0237      0.752 0.000 0.004 0.996
#&gt; SRR1383390     2  0.0592      0.798 0.000 0.988 0.012
#&gt; SRR1383394     2  0.5968      0.643 0.000 0.636 0.364
#&gt; SRR1383393     2  0.1289      0.787 0.032 0.968 0.000
#&gt; SRR1383396     2  0.0237      0.794 0.004 0.996 0.000
#&gt; SRR1383395     3  0.0424      0.755 0.000 0.008 0.992
#&gt; SRR1383399     2  0.0592      0.795 0.012 0.988 0.000
#&gt; SRR1383400     1  0.2711      0.940 0.912 0.088 0.000
#&gt; SRR1383397     3  0.1877      0.732 0.032 0.012 0.956
#&gt; SRR1383401     2  0.2711      0.776 0.000 0.912 0.088
#&gt; SRR1383398     2  0.5785      0.663 0.004 0.696 0.300
#&gt; SRR1383402     2  0.5948      0.646 0.000 0.640 0.360
#&gt; SRR1383404     2  0.4931      0.755 0.032 0.828 0.140
#&gt; SRR1383403     2  0.6008      0.427 0.372 0.628 0.000
#&gt; SRR1383405     2  0.6899      0.635 0.024 0.612 0.364
#&gt; SRR1383406     2  0.7023      0.631 0.032 0.624 0.344
#&gt; SRR1383407     2  0.0592      0.798 0.000 0.988 0.012
#&gt; SRR1383408     2  0.0592      0.798 0.000 0.988 0.012
#&gt; SRR1383409     2  0.1411      0.795 0.000 0.964 0.036
#&gt; SRR1383410     2  0.6026      0.635 0.000 0.624 0.376
</code></pre>

<script>
$('#tab-CV-pam-get-classes-2-a').parent().next().next().hide();
$('#tab-CV-pam-get-classes-2-a').click(function(){
  $('#tab-CV-pam-get-classes-2-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-CV-pam-get-classes-3'>
<p><a id='tab-CV-pam-get-classes-3-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 4), get_membership(res, k = 4))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4
#&gt; SRR1383358     3  0.4817    0.69924 0.000 0.000 0.612 0.388
#&gt; SRR1383360     4  0.6843   -0.16156 0.012 0.124 0.240 0.624
#&gt; SRR1383359     4  0.4999   -0.56933 0.000 0.000 0.492 0.508
#&gt; SRR1383362     1  0.0000    0.85459 1.000 0.000 0.000 0.000
#&gt; SRR1383361     3  0.4817    0.69924 0.000 0.000 0.612 0.388
#&gt; SRR1383363     3  0.7374    0.57192 0.000 0.164 0.456 0.380
#&gt; SRR1383364     2  0.0336    0.81559 0.000 0.992 0.008 0.000
#&gt; SRR1383365     3  0.4817    0.69924 0.000 0.000 0.612 0.388
#&gt; SRR1383366     4  0.4134   -0.03334 0.000 0.000 0.260 0.740
#&gt; SRR1383367     3  0.4817    0.69924 0.000 0.000 0.612 0.388
#&gt; SRR1383368     2  0.7582   -0.00648 0.012 0.544 0.204 0.240
#&gt; SRR1383369     4  0.4994   -0.53672 0.000 0.000 0.480 0.520
#&gt; SRR1383370     3  0.4898    0.67856 0.000 0.000 0.584 0.416
#&gt; SRR1383371     3  0.7448    0.55407 0.000 0.176 0.452 0.372
#&gt; SRR1383372     2  0.3311    0.69110 0.000 0.828 0.172 0.000
#&gt; SRR1383373     3  0.6597    0.63418 0.000 0.088 0.540 0.372
#&gt; SRR1383374     4  0.4916   -0.43436 0.000 0.000 0.424 0.576
#&gt; SRR1383375     2  0.0804    0.81240 0.012 0.980 0.008 0.000
#&gt; SRR1383376     4  0.5016    0.10062 0.000 0.396 0.004 0.600
#&gt; SRR1383377     4  0.1356    0.26625 0.000 0.008 0.032 0.960
#&gt; SRR1383378     2  0.0000    0.81591 0.000 1.000 0.000 0.000
#&gt; SRR1383379     4  0.3893    0.09943 0.008 0.000 0.196 0.796
#&gt; SRR1383380     2  0.5007    0.45694 0.008 0.636 0.000 0.356
#&gt; SRR1383381     2  0.0336    0.81559 0.000 0.992 0.008 0.000
#&gt; SRR1383382     1  0.1637    0.87558 0.940 0.060 0.000 0.000
#&gt; SRR1383383     2  0.4290    0.62337 0.000 0.772 0.212 0.016
#&gt; SRR1383385     1  0.5781    0.70716 0.584 0.036 0.380 0.000
#&gt; SRR1383384     2  0.3908    0.66742 0.000 0.784 0.004 0.212
#&gt; SRR1383386     2  0.0804    0.81240 0.012 0.980 0.008 0.000
#&gt; SRR1383387     4  0.4936    0.13457 0.000 0.372 0.004 0.624
#&gt; SRR1383389     2  0.0000    0.81591 0.000 1.000 0.000 0.000
#&gt; SRR1383391     2  0.0000    0.81591 0.000 1.000 0.000 0.000
#&gt; SRR1383388     2  0.3598    0.74264 0.012 0.848 0.008 0.132
#&gt; SRR1383392     4  0.4008   -0.06049 0.000 0.000 0.244 0.756
#&gt; SRR1383390     2  0.0000    0.81591 0.000 1.000 0.000 0.000
#&gt; SRR1383394     4  0.4978    0.11926 0.000 0.384 0.004 0.612
#&gt; SRR1383393     2  0.0804    0.81240 0.012 0.980 0.008 0.000
#&gt; SRR1383396     2  0.0336    0.81505 0.008 0.992 0.000 0.000
#&gt; SRR1383395     4  0.1042    0.27511 0.000 0.008 0.020 0.972
#&gt; SRR1383399     2  0.0336    0.81559 0.000 0.992 0.008 0.000
#&gt; SRR1383400     1  0.1637    0.87558 0.940 0.060 0.000 0.000
#&gt; SRR1383397     4  0.3852    0.10031 0.008 0.000 0.192 0.800
#&gt; SRR1383401     2  0.7006    0.32082 0.000 0.580 0.216 0.204
#&gt; SRR1383398     2  0.5220    0.32174 0.008 0.568 0.000 0.424
#&gt; SRR1383402     4  0.5398    0.08042 0.000 0.404 0.016 0.580
#&gt; SRR1383404     2  0.4043    0.71091 0.012 0.812 0.008 0.168
#&gt; SRR1383403     3  0.8534   -0.57547 0.336 0.256 0.380 0.028
#&gt; SRR1383405     4  0.4761    0.13293 0.000 0.372 0.000 0.628
#&gt; SRR1383406     2  0.5236    0.31016 0.008 0.560 0.000 0.432
#&gt; SRR1383407     2  0.0000    0.81591 0.000 1.000 0.000 0.000
#&gt; SRR1383408     2  0.0000    0.81591 0.000 1.000 0.000 0.000
#&gt; SRR1383409     2  0.5167    0.62852 0.000 0.760 0.132 0.108
#&gt; SRR1383410     4  0.7510    0.07467 0.000 0.380 0.184 0.436
</code></pre>

<script>
$('#tab-CV-pam-get-classes-3-a').parent().next().next().hide();
$('#tab-CV-pam-get-classes-3-a').click(function(){
  $('#tab-CV-pam-get-classes-3-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-CV-pam-get-classes-4'>
<p><a id='tab-CV-pam-get-classes-4-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 5), get_membership(res, k = 5))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4    p5
#&gt; SRR1383358     3  0.0162     0.7433 0.000 0.000 0.996 0.004 0.000
#&gt; SRR1383360     3  0.6721     0.4715 0.000 0.164 0.600 0.172 0.064
#&gt; SRR1383359     3  0.2377     0.6837 0.000 0.000 0.872 0.128 0.000
#&gt; SRR1383362     1  0.0000     1.0000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1383361     3  0.0162     0.7433 0.000 0.000 0.996 0.004 0.000
#&gt; SRR1383363     3  0.2719     0.6840 0.000 0.144 0.852 0.004 0.000
#&gt; SRR1383364     2  0.1644     0.8654 0.000 0.940 0.004 0.008 0.048
#&gt; SRR1383365     3  0.0162     0.7433 0.000 0.000 0.996 0.004 0.000
#&gt; SRR1383366     3  0.4060     0.3366 0.000 0.000 0.640 0.360 0.000
#&gt; SRR1383367     3  0.0162     0.7433 0.000 0.000 0.996 0.004 0.000
#&gt; SRR1383368     3  0.5652     0.1565 0.000 0.460 0.472 0.004 0.064
#&gt; SRR1383369     3  0.3274     0.5394 0.000 0.000 0.780 0.220 0.000
#&gt; SRR1383370     3  0.0794     0.7382 0.000 0.000 0.972 0.028 0.000
#&gt; SRR1383371     3  0.3902     0.6579 0.000 0.136 0.808 0.008 0.048
#&gt; SRR1383372     2  0.3039     0.7583 0.000 0.808 0.192 0.000 0.000
#&gt; SRR1383373     3  0.1908     0.7088 0.000 0.092 0.908 0.000 0.000
#&gt; SRR1383374     3  0.4256     0.0970 0.000 0.000 0.564 0.436 0.000
#&gt; SRR1383375     2  0.1638     0.8541 0.000 0.932 0.000 0.004 0.064
#&gt; SRR1383376     4  0.1216     0.6733 0.000 0.020 0.020 0.960 0.000
#&gt; SRR1383377     4  0.0963     0.6689 0.000 0.000 0.036 0.964 0.000
#&gt; SRR1383378     2  0.0000     0.8718 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1383379     4  0.4522     0.0622 0.000 0.000 0.440 0.552 0.008
#&gt; SRR1383380     2  0.4288     0.3926 0.000 0.612 0.000 0.384 0.004
#&gt; SRR1383381     2  0.1644     0.8654 0.000 0.940 0.004 0.008 0.048
#&gt; SRR1383382     1  0.0000     1.0000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1383383     2  0.3715     0.6558 0.000 0.736 0.260 0.004 0.000
#&gt; SRR1383385     5  0.1386     0.9786 0.016 0.032 0.000 0.000 0.952
#&gt; SRR1383384     2  0.3690     0.7164 0.000 0.780 0.020 0.200 0.000
#&gt; SRR1383386     2  0.1638     0.8541 0.000 0.932 0.000 0.004 0.064
#&gt; SRR1383387     4  0.0898     0.6730 0.000 0.008 0.020 0.972 0.000
#&gt; SRR1383389     2  0.0880     0.8736 0.000 0.968 0.032 0.000 0.000
#&gt; SRR1383391     2  0.0880     0.8736 0.000 0.968 0.032 0.000 0.000
#&gt; SRR1383388     2  0.3176     0.8201 0.000 0.856 0.000 0.080 0.064
#&gt; SRR1383392     4  0.3636     0.4797 0.000 0.000 0.272 0.728 0.000
#&gt; SRR1383390     2  0.0880     0.8736 0.000 0.968 0.032 0.000 0.000
#&gt; SRR1383394     4  0.1117     0.6740 0.000 0.016 0.020 0.964 0.000
#&gt; SRR1383393     2  0.1638     0.8541 0.000 0.932 0.000 0.004 0.064
#&gt; SRR1383396     2  0.0324     0.8714 0.000 0.992 0.000 0.004 0.004
#&gt; SRR1383395     4  0.0609     0.6686 0.000 0.000 0.020 0.980 0.000
#&gt; SRR1383399     2  0.1644     0.8654 0.000 0.940 0.004 0.008 0.048
#&gt; SRR1383400     1  0.0000     1.0000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1383397     4  0.4410     0.0639 0.000 0.000 0.440 0.556 0.004
#&gt; SRR1383401     4  0.6678     0.1204 0.000 0.300 0.264 0.436 0.000
#&gt; SRR1383398     4  0.4410     0.0748 0.000 0.440 0.000 0.556 0.004
#&gt; SRR1383402     4  0.2473     0.6478 0.000 0.072 0.032 0.896 0.000
#&gt; SRR1383404     2  0.3558     0.7970 0.000 0.828 0.000 0.108 0.064
#&gt; SRR1383403     5  0.1442     0.9788 0.004 0.032 0.000 0.012 0.952
#&gt; SRR1383405     4  0.0451     0.6672 0.000 0.008 0.004 0.988 0.000
#&gt; SRR1383406     4  0.4557     0.0769 0.000 0.440 0.004 0.552 0.004
#&gt; SRR1383407     2  0.0880     0.8736 0.000 0.968 0.032 0.000 0.000
#&gt; SRR1383408     2  0.0880     0.8736 0.000 0.968 0.032 0.000 0.000
#&gt; SRR1383409     2  0.4890     0.6556 0.000 0.720 0.140 0.140 0.000
#&gt; SRR1383410     4  0.3353     0.5713 0.000 0.008 0.196 0.796 0.000
</code></pre>

<script>
$('#tab-CV-pam-get-classes-4-a').parent().next().next().hide();
$('#tab-CV-pam-get-classes-4-a').click(function(){
  $('#tab-CV-pam-get-classes-4-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-CV-pam-get-classes-5'>
<p><a id='tab-CV-pam-get-classes-5-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 6), get_membership(res, k = 6))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4    p5 p6
#&gt; SRR1383358     3  0.0000     0.7157 0.000 0.000 1.000 0.000 0.000  0
#&gt; SRR1383360     3  0.6434     0.4527 0.108 0.108 0.592 0.180 0.012  0
#&gt; SRR1383359     3  0.2454     0.6203 0.000 0.000 0.840 0.160 0.000  0
#&gt; SRR1383362     6  0.0000     1.0000 0.000 0.000 0.000 0.000 0.000  1
#&gt; SRR1383361     3  0.0000     0.7157 0.000 0.000 1.000 0.000 0.000  0
#&gt; SRR1383363     3  0.3266     0.5248 0.000 0.272 0.728 0.000 0.000  0
#&gt; SRR1383364     5  0.0363     0.9918 0.000 0.012 0.000 0.000 0.988  0
#&gt; SRR1383365     3  0.0146     0.7151 0.000 0.000 0.996 0.004 0.000  0
#&gt; SRR1383366     3  0.3706     0.2663 0.000 0.000 0.620 0.380 0.000  0
#&gt; SRR1383367     3  0.0000     0.7157 0.000 0.000 1.000 0.000 0.000  0
#&gt; SRR1383368     3  0.5667     0.0968 0.108 0.424 0.456 0.000 0.012  0
#&gt; SRR1383369     3  0.3052     0.5097 0.000 0.004 0.780 0.216 0.000  0
#&gt; SRR1383370     3  0.0547     0.7103 0.000 0.000 0.980 0.020 0.000  0
#&gt; SRR1383371     5  0.0363     0.9754 0.000 0.000 0.012 0.000 0.988  0
#&gt; SRR1383372     2  0.3464     0.5298 0.000 0.688 0.312 0.000 0.000  0
#&gt; SRR1383373     3  0.1444     0.6856 0.000 0.072 0.928 0.000 0.000  0
#&gt; SRR1383374     3  0.4377     0.0422 0.000 0.024 0.540 0.436 0.000  0
#&gt; SRR1383375     2  0.2266     0.7937 0.108 0.880 0.000 0.000 0.012  0
#&gt; SRR1383376     4  0.0972     0.6796 0.000 0.008 0.028 0.964 0.000  0
#&gt; SRR1383377     4  0.0777     0.6735 0.004 0.000 0.024 0.972 0.000  0
#&gt; SRR1383378     2  0.0146     0.8177 0.000 0.996 0.000 0.004 0.000  0
#&gt; SRR1383379     4  0.4361     0.0503 0.016 0.004 0.436 0.544 0.000  0
#&gt; SRR1383380     2  0.3862     0.3828 0.004 0.608 0.000 0.388 0.000  0
#&gt; SRR1383381     5  0.0363     0.9918 0.000 0.012 0.000 0.000 0.988  0
#&gt; SRR1383382     6  0.0000     1.0000 0.000 0.000 0.000 0.000 0.000  1
#&gt; SRR1383383     2  0.2006     0.7780 0.000 0.892 0.104 0.004 0.000  0
#&gt; SRR1383385     1  0.0146     0.9780 0.996 0.004 0.000 0.000 0.000  0
#&gt; SRR1383384     2  0.3440     0.6828 0.000 0.776 0.028 0.196 0.000  0
#&gt; SRR1383386     2  0.2266     0.7937 0.108 0.880 0.000 0.000 0.012  0
#&gt; SRR1383387     4  0.0713     0.6800 0.000 0.000 0.028 0.972 0.000  0
#&gt; SRR1383389     2  0.0146     0.8178 0.000 0.996 0.004 0.000 0.000  0
#&gt; SRR1383391     2  0.0146     0.8177 0.000 0.996 0.000 0.004 0.000  0
#&gt; SRR1383388     2  0.3602     0.7706 0.108 0.812 0.000 0.068 0.012  0
#&gt; SRR1383392     4  0.3967     0.3074 0.000 0.012 0.356 0.632 0.000  0
#&gt; SRR1383390     2  0.0146     0.8178 0.000 0.996 0.004 0.000 0.000  0
#&gt; SRR1383394     4  0.0858     0.6803 0.000 0.004 0.028 0.968 0.000  0
#&gt; SRR1383393     2  0.2266     0.7937 0.108 0.880 0.000 0.000 0.012  0
#&gt; SRR1383396     2  0.1007     0.8117 0.044 0.956 0.000 0.000 0.000  0
#&gt; SRR1383395     4  0.0405     0.6707 0.004 0.000 0.008 0.988 0.000  0
#&gt; SRR1383399     5  0.0363     0.9918 0.000 0.012 0.000 0.000 0.988  0
#&gt; SRR1383400     6  0.0000     1.0000 0.000 0.000 0.000 0.000 0.000  1
#&gt; SRR1383397     4  0.4189     0.0543 0.008 0.004 0.436 0.552 0.000  0
#&gt; SRR1383401     2  0.5328    -0.0255 0.000 0.456 0.104 0.440 0.000  0
#&gt; SRR1383398     4  0.3955     0.0468 0.004 0.436 0.000 0.560 0.000  0
#&gt; SRR1383402     4  0.2499     0.6396 0.000 0.072 0.048 0.880 0.000  0
#&gt; SRR1383404     2  0.3813     0.7598 0.108 0.796 0.000 0.084 0.012  0
#&gt; SRR1383403     1  0.0260     0.9780 0.992 0.000 0.000 0.008 0.000  0
#&gt; SRR1383405     4  0.0547     0.6786 0.000 0.000 0.020 0.980 0.000  0
#&gt; SRR1383406     4  0.4189     0.0504 0.004 0.436 0.008 0.552 0.000  0
#&gt; SRR1383407     2  0.0146     0.8178 0.000 0.996 0.004 0.000 0.000  0
#&gt; SRR1383408     2  0.0146     0.8178 0.000 0.996 0.004 0.000 0.000  0
#&gt; SRR1383409     2  0.4634     0.5838 0.000 0.692 0.164 0.144 0.000  0
#&gt; SRR1383410     4  0.3898     0.3426 0.000 0.012 0.336 0.652 0.000  0
</code></pre>

<script>
$('#tab-CV-pam-get-classes-5-a').parent().next().next().hide();
$('#tab-CV-pam-get-classes-5-a').click(function(){
  $('#tab-CV-pam-get-classes-5-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>
</div>

Heatmaps for the consensus matrix. It visualizes the probability of two
samples to be in a same group.



<script>
$( function() {
	$( '#tabs-CV-pam-consensus-heatmap' ).tabs();
} );
</script>
<div id='tabs-CV-pam-consensus-heatmap'>
<ul>
<li><a href='#tab-CV-pam-consensus-heatmap-1'>k = 2</a></li>
<li><a href='#tab-CV-pam-consensus-heatmap-2'>k = 3</a></li>
<li><a href='#tab-CV-pam-consensus-heatmap-3'>k = 4</a></li>
<li><a href='#tab-CV-pam-consensus-heatmap-4'>k = 5</a></li>
<li><a href='#tab-CV-pam-consensus-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-CV-pam-consensus-heatmap-1'>
<pre><code class="r">consensus_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-CV-pam-consensus-heatmap-1-1.png" alt="plot of chunk tab-CV-pam-consensus-heatmap-1"/></p>

</div>
<div id='tab-CV-pam-consensus-heatmap-2'>
<pre><code class="r">consensus_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-CV-pam-consensus-heatmap-2-1.png" alt="plot of chunk tab-CV-pam-consensus-heatmap-2"/></p>

</div>
<div id='tab-CV-pam-consensus-heatmap-3'>
<pre><code class="r">consensus_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-CV-pam-consensus-heatmap-3-1.png" alt="plot of chunk tab-CV-pam-consensus-heatmap-3"/></p>

</div>
<div id='tab-CV-pam-consensus-heatmap-4'>
<pre><code class="r">consensus_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-CV-pam-consensus-heatmap-4-1.png" alt="plot of chunk tab-CV-pam-consensus-heatmap-4"/></p>

</div>
<div id='tab-CV-pam-consensus-heatmap-5'>
<pre><code class="r">consensus_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-CV-pam-consensus-heatmap-5-1.png" alt="plot of chunk tab-CV-pam-consensus-heatmap-5"/></p>

</div>
</div>

Heatmaps for the membership of samples in all partitions to see how consistent they are:




<script>
$( function() {
	$( '#tabs-CV-pam-membership-heatmap' ).tabs();
} );
</script>
<div id='tabs-CV-pam-membership-heatmap'>
<ul>
<li><a href='#tab-CV-pam-membership-heatmap-1'>k = 2</a></li>
<li><a href='#tab-CV-pam-membership-heatmap-2'>k = 3</a></li>
<li><a href='#tab-CV-pam-membership-heatmap-3'>k = 4</a></li>
<li><a href='#tab-CV-pam-membership-heatmap-4'>k = 5</a></li>
<li><a href='#tab-CV-pam-membership-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-CV-pam-membership-heatmap-1'>
<pre><code class="r">membership_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-CV-pam-membership-heatmap-1-1.png" alt="plot of chunk tab-CV-pam-membership-heatmap-1"/></p>

</div>
<div id='tab-CV-pam-membership-heatmap-2'>
<pre><code class="r">membership_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-CV-pam-membership-heatmap-2-1.png" alt="plot of chunk tab-CV-pam-membership-heatmap-2"/></p>

</div>
<div id='tab-CV-pam-membership-heatmap-3'>
<pre><code class="r">membership_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-CV-pam-membership-heatmap-3-1.png" alt="plot of chunk tab-CV-pam-membership-heatmap-3"/></p>

</div>
<div id='tab-CV-pam-membership-heatmap-4'>
<pre><code class="r">membership_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-CV-pam-membership-heatmap-4-1.png" alt="plot of chunk tab-CV-pam-membership-heatmap-4"/></p>

</div>
<div id='tab-CV-pam-membership-heatmap-5'>
<pre><code class="r">membership_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-CV-pam-membership-heatmap-5-1.png" alt="plot of chunk tab-CV-pam-membership-heatmap-5"/></p>

</div>
</div>

As soon as we have had the classes for columns, we can look for signatures
which are significantly different between classes which can be candidate marks
for certain classes. Following are the heatmaps for signatures.



Signature heatmaps where rows are scaled:



<script>
$( function() {
	$( '#tabs-CV-pam-get-signatures' ).tabs();
} );
</script>
<div id='tabs-CV-pam-get-signatures'>
<ul>
<li><a href='#tab-CV-pam-get-signatures-1'>k = 2</a></li>
<li><a href='#tab-CV-pam-get-signatures-2'>k = 3</a></li>
<li><a href='#tab-CV-pam-get-signatures-3'>k = 4</a></li>
<li><a href='#tab-CV-pam-get-signatures-4'>k = 5</a></li>
<li><a href='#tab-CV-pam-get-signatures-5'>k = 6</a></li>
</ul>
<div id='tab-CV-pam-get-signatures-1'>
<pre><code class="r">get_signatures(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-CV-pam-get-signatures-1-1.png" alt="plot of chunk tab-CV-pam-get-signatures-1"/></p>

</div>
<div id='tab-CV-pam-get-signatures-2'>
<pre><code class="r">get_signatures(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-CV-pam-get-signatures-2-1.png" alt="plot of chunk tab-CV-pam-get-signatures-2"/></p>

</div>
<div id='tab-CV-pam-get-signatures-3'>
<pre><code class="r">get_signatures(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-CV-pam-get-signatures-3-1.png" alt="plot of chunk tab-CV-pam-get-signatures-3"/></p>

</div>
<div id='tab-CV-pam-get-signatures-4'>
<pre><code class="r">get_signatures(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-CV-pam-get-signatures-4-1.png" alt="plot of chunk tab-CV-pam-get-signatures-4"/></p>

</div>
<div id='tab-CV-pam-get-signatures-5'>
<pre><code class="r">get_signatures(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-CV-pam-get-signatures-5-1.png" alt="plot of chunk tab-CV-pam-get-signatures-5"/></p>

</div>
</div>



Signature heatmaps where rows are not scaled:


<script>
$( function() {
	$( '#tabs-CV-pam-get-signatures-no-scale' ).tabs();
} );
</script>
<div id='tabs-CV-pam-get-signatures-no-scale'>
<ul>
<li><a href='#tab-CV-pam-get-signatures-no-scale-1'>k = 2</a></li>
<li><a href='#tab-CV-pam-get-signatures-no-scale-2'>k = 3</a></li>
<li><a href='#tab-CV-pam-get-signatures-no-scale-3'>k = 4</a></li>
<li><a href='#tab-CV-pam-get-signatures-no-scale-4'>k = 5</a></li>
<li><a href='#tab-CV-pam-get-signatures-no-scale-5'>k = 6</a></li>
</ul>
<div id='tab-CV-pam-get-signatures-no-scale-1'>
<pre><code class="r">get_signatures(res, k = 2, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-CV-pam-get-signatures-no-scale-1-1.png" alt="plot of chunk tab-CV-pam-get-signatures-no-scale-1"/></p>

</div>
<div id='tab-CV-pam-get-signatures-no-scale-2'>
<pre><code class="r">get_signatures(res, k = 3, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-CV-pam-get-signatures-no-scale-2-1.png" alt="plot of chunk tab-CV-pam-get-signatures-no-scale-2"/></p>

</div>
<div id='tab-CV-pam-get-signatures-no-scale-3'>
<pre><code class="r">get_signatures(res, k = 4, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-CV-pam-get-signatures-no-scale-3-1.png" alt="plot of chunk tab-CV-pam-get-signatures-no-scale-3"/></p>

</div>
<div id='tab-CV-pam-get-signatures-no-scale-4'>
<pre><code class="r">get_signatures(res, k = 5, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-CV-pam-get-signatures-no-scale-4-1.png" alt="plot of chunk tab-CV-pam-get-signatures-no-scale-4"/></p>

</div>
<div id='tab-CV-pam-get-signatures-no-scale-5'>
<pre><code class="r">get_signatures(res, k = 6, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-CV-pam-get-signatures-no-scale-5-1.png" alt="plot of chunk tab-CV-pam-get-signatures-no-scale-5"/></p>

</div>
</div>



Compare the overlap of signatures from different k:

```r
compare_signatures(res)
```

![plot of chunk CV-pam-signature_compare](figure_cola/CV-pam-signature_compare-1.png)

`get_signature()` returns a data frame invisibly. TO get the list of signatures, the function
call should be assigned to a variable explicitly. In following code, if `plot` argument is set
to `FALSE`, no heatmap is plotted while only the differential analysis is performed.

```r
# code only for demonstration
tb = get_signature(res, k = ..., plot = FALSE)
```

An example of the output of `tb` is:

```
#>   which_row         fdr    mean_1    mean_2 scaled_mean_1 scaled_mean_2 km
#> 1        38 0.042760348  8.373488  9.131774    -0.5533452     0.5164555  1
#> 2        40 0.018707592  7.106213  8.469186    -0.6173731     0.5762149  1
#> 3        55 0.019134737 10.221463 11.207825    -0.6159697     0.5749050  1
#> 4        59 0.006059896  5.921854  7.869574    -0.6899429     0.6439467  1
#> 5        60 0.018055526  8.928898 10.211722    -0.6204761     0.5791110  1
#> 6        98 0.009384629 15.714769 14.887706     0.6635654    -0.6193277  2
...
```

The columns in `tb` are:

1. `which_row`: row indices corresponding to the input matrix.
2. `fdr`: FDR for the differential test. 
3. `mean_x`: The mean value in group x.
4. `scaled_mean_x`: The mean value in group x after rows are scaled.
5. `km`: Row groups if k-means clustering is applied to rows.



UMAP plot which shows how samples are separated.


<script>
$( function() {
	$( '#tabs-CV-pam-dimension-reduction' ).tabs();
} );
</script>
<div id='tabs-CV-pam-dimension-reduction'>
<ul>
<li><a href='#tab-CV-pam-dimension-reduction-1'>k = 2</a></li>
<li><a href='#tab-CV-pam-dimension-reduction-2'>k = 3</a></li>
<li><a href='#tab-CV-pam-dimension-reduction-3'>k = 4</a></li>
<li><a href='#tab-CV-pam-dimension-reduction-4'>k = 5</a></li>
<li><a href='#tab-CV-pam-dimension-reduction-5'>k = 6</a></li>
</ul>
<div id='tab-CV-pam-dimension-reduction-1'>
<pre><code class="r">dimension_reduction(res, k = 2, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-CV-pam-dimension-reduction-1-1.png" alt="plot of chunk tab-CV-pam-dimension-reduction-1"/></p>

</div>
<div id='tab-CV-pam-dimension-reduction-2'>
<pre><code class="r">dimension_reduction(res, k = 3, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-CV-pam-dimension-reduction-2-1.png" alt="plot of chunk tab-CV-pam-dimension-reduction-2"/></p>

</div>
<div id='tab-CV-pam-dimension-reduction-3'>
<pre><code class="r">dimension_reduction(res, k = 4, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-CV-pam-dimension-reduction-3-1.png" alt="plot of chunk tab-CV-pam-dimension-reduction-3"/></p>

</div>
<div id='tab-CV-pam-dimension-reduction-4'>
<pre><code class="r">dimension_reduction(res, k = 5, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-CV-pam-dimension-reduction-4-1.png" alt="plot of chunk tab-CV-pam-dimension-reduction-4"/></p>

</div>
<div id='tab-CV-pam-dimension-reduction-5'>
<pre><code class="r">dimension_reduction(res, k = 6, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-CV-pam-dimension-reduction-5-1.png" alt="plot of chunk tab-CV-pam-dimension-reduction-5"/></p>

</div>
</div>


Following heatmap shows how subgroups are split when increasing `k`:

```r
collect_classes(res)
```

![plot of chunk CV-pam-collect-classes](figure_cola/CV-pam-collect-classes-1.png)


If matrix rows can be associated to genes, consider to use `functional_enrichment(res,
...)` to perform function enrichment for the signature genes. See [this vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/functional_enrichment.html) for more detailed explanations.


 

---------------------------------------------------




### CV:mclust






The object with results only for a single top-value method and a single partition method 
can be extracted as:

```r
res = res_list["CV", "mclust"]
# you can also extract it by
# res = res_list["CV:mclust"]
```

A summary of `res` and all the functions that can be applied to it:

```r
res
```

```
#> A 'ConsensusPartition' object with k = 2, 3, 4, 5, 6.
#>   On a matrix with 15680 rows and 53 columns.
#>   Top rows (1000, 2000, 3000, 4000, 5000) are extracted by 'CV' method.
#>   Subgroups are detected by 'mclust' method.
#>   Performed in total 1250 partitions by row resampling.
#>   Best k for subgroups seems to be 3.
#> 
#> Following methods can be applied to this 'ConsensusPartition' object:
#>  [1] "cola_report"             "collect_classes"         "collect_plots"          
#>  [4] "collect_stats"           "colnames"                "compare_signatures"     
#>  [7] "consensus_heatmap"       "dimension_reduction"     "functional_enrichment"  
#> [10] "get_anno_col"            "get_anno"                "get_classes"            
#> [13] "get_consensus"           "get_matrix"              "get_membership"         
#> [16] "get_param"               "get_signatures"          "get_stats"              
#> [19] "is_best_k"               "is_stable_k"             "membership_heatmap"     
#> [22] "ncol"                    "nrow"                    "plot_ecdf"              
#> [25] "rownames"                "select_partition_number" "show"                   
#> [28] "suggest_best_k"          "test_to_known_factors"
```

`collect_plots()` function collects all the plots made from `res` for all `k` (number of partitions)
into one single page to provide an easy and fast comparison between different `k`.

```r
collect_plots(res)
```

![plot of chunk CV-mclust-collect-plots](figure_cola/CV-mclust-collect-plots-1.png)

The plots are:

- The first row: a plot of the ECDF (empirical cumulative distribution
  function) curves of the consensus matrix for each `k` and the heatmap of
  predicted classes for each `k`.
- The second row: heatmaps of the consensus matrix for each `k`.
- The third row: heatmaps of the membership matrix for each `k`.
- The fouth row: heatmaps of the signatures for each `k`.

All the plots in panels can be made by individual functions and they are
plotted later in this section.

`select_partition_number()` produces several plots showing different
statistics for choosing "optimized" `k`. There are following statistics:

- ECDF curves of the consensus matrix for each `k`;
- 1-PAC. [The PAC
  score](https://en.wikipedia.org/wiki/Consensus_clustering#Over-interpretation_potential_of_consensus_clustering)
  measures the proportion of the ambiguous subgrouping.
- Mean silhouette score.
- Concordance. The mean probability of fiting the consensus class ids in all
  partitions.
- Area increased. Denote $A_k$ as the area under the ECDF curve for current
  `k`, the area increased is defined as $A_k - A_{k-1}$.
- Rand index. The percent of pairs of samples that are both in a same cluster
  or both are not in a same cluster in the partition of k and k-1.
- Jaccard index. The ratio of pairs of samples are both in a same cluster in
  the partition of k and k-1 and the pairs of samples are both in a same
  cluster in the partition k or k-1.

The detailed explanations of these statistics can be found in [the _cola_
vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/cola.html#toc_13).

Generally speaking, lower PAC score, higher mean silhouette score or higher
concordance corresponds to better partition. Rand index and Jaccard index
measure how similar the current partition is compared to partition with `k-1`.
If they are too similar, we won't accept `k` is better than `k-1`.

```r
select_partition_number(res)
```

![plot of chunk CV-mclust-select-partition-number](figure_cola/CV-mclust-select-partition-number-1.png)

The numeric values for all these statistics can be obtained by `get_stats()`.

```r
get_stats(res)
```

```
#>   k 1-PAC mean_silhouette concordance area_increased  Rand Jaccard
#> 2 2 0.820           0.896       0.959         0.2446 0.795   0.795
#> 3 3 0.374           0.739       0.831         0.8497 0.840   0.800
#> 4 4 0.491           0.547       0.780         0.4708 0.642   0.455
#> 5 5 0.576           0.607       0.767         0.1396 0.820   0.501
#> 6 6 0.563           0.533       0.714         0.0448 0.869   0.517
```

`suggest_best_k()` suggests the best $k$ based on these statistics. The rules are as follows:

- All $k$ with Jaccard index larger than 0.95 are removed because increasing
  $k$ does not provide enough extra information. If all $k$ are removed, it is
  marked as no subgroup is detected.
- For all $k$ with 1-PAC score larger than 0.9, the maximal $k$ is taken as
  the best $k$, and other $k$ are marked as optional $k$.
- If it does not fit the second rule. The $k$ with the maximal vote of the
  highest 1-PAC score, highest mean silhouette, and highest concordance is
  taken as the best $k$.

```r
suggest_best_k(res)
```

```
#> [1] 3
```


Following shows the table of the partitions (You need to click the **show/hide
code output** link to see it). The membership matrix (columns with name `p*`)
is inferred by
[`clue::cl_consensus()`](https://www.rdocumentation.org/link/cl_consensus?package=clue)
function with the `SE` method. Basically the value in the membership matrix
represents the probability to belong to a certain group. The finall class
label for an item is determined with the group with highest probability it
belongs to.

In `get_classes()` function, the entropy is calculated from the membership
matrix and the silhouette score is calculated from the consensus matrix.



<script>
$( function() {
	$( '#tabs-CV-mclust-get-classes' ).tabs();
} );
</script>
<div id='tabs-CV-mclust-get-classes'>
<ul>
<li><a href='#tab-CV-mclust-get-classes-1'>k = 2</a></li>
<li><a href='#tab-CV-mclust-get-classes-2'>k = 3</a></li>
<li><a href='#tab-CV-mclust-get-classes-3'>k = 4</a></li>
<li><a href='#tab-CV-mclust-get-classes-4'>k = 5</a></li>
<li><a href='#tab-CV-mclust-get-classes-5'>k = 6</a></li>
</ul>

<div id='tab-CV-mclust-get-classes-1'>
<p><a id='tab-CV-mclust-get-classes-1-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 2), get_membership(res, k = 2))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2
#&gt; SRR1383358     2  0.0000      0.955 0.000 1.000
#&gt; SRR1383360     2  0.0376      0.954 0.004 0.996
#&gt; SRR1383359     2  0.0000      0.955 0.000 1.000
#&gt; SRR1383362     1  0.0000      0.936 1.000 0.000
#&gt; SRR1383361     2  0.0000      0.955 0.000 1.000
#&gt; SRR1383363     2  0.0000      0.955 0.000 1.000
#&gt; SRR1383364     2  0.9427      0.437 0.360 0.640
#&gt; SRR1383365     2  0.0000      0.955 0.000 1.000
#&gt; SRR1383366     2  0.0376      0.954 0.004 0.996
#&gt; SRR1383367     2  0.0000      0.955 0.000 1.000
#&gt; SRR1383368     2  0.0376      0.954 0.004 0.996
#&gt; SRR1383369     2  0.0000      0.955 0.000 1.000
#&gt; SRR1383370     2  0.0000      0.955 0.000 1.000
#&gt; SRR1383371     2  0.9427      0.437 0.360 0.640
#&gt; SRR1383372     2  0.0000      0.955 0.000 1.000
#&gt; SRR1383373     2  0.0000      0.955 0.000 1.000
#&gt; SRR1383374     2  0.0000      0.955 0.000 1.000
#&gt; SRR1383375     1  0.8713      0.541 0.708 0.292
#&gt; SRR1383376     2  0.0000      0.955 0.000 1.000
#&gt; SRR1383377     2  0.0376      0.954 0.004 0.996
#&gt; SRR1383378     2  0.0376      0.954 0.004 0.996
#&gt; SRR1383379     2  0.0376      0.954 0.004 0.996
#&gt; SRR1383380     2  0.0376      0.954 0.004 0.996
#&gt; SRR1383381     2  0.9427      0.437 0.360 0.640
#&gt; SRR1383382     1  0.0000      0.936 1.000 0.000
#&gt; SRR1383383     2  0.0000      0.955 0.000 1.000
#&gt; SRR1383385     1  0.0000      0.936 1.000 0.000
#&gt; SRR1383384     2  0.0000      0.955 0.000 1.000
#&gt; SRR1383386     2  0.0376      0.954 0.004 0.996
#&gt; SRR1383387     2  0.0000      0.955 0.000 1.000
#&gt; SRR1383389     2  0.0000      0.955 0.000 1.000
#&gt; SRR1383391     2  0.0000      0.955 0.000 1.000
#&gt; SRR1383388     2  0.0376      0.954 0.004 0.996
#&gt; SRR1383392     2  0.0376      0.954 0.004 0.996
#&gt; SRR1383390     2  0.0000      0.955 0.000 1.000
#&gt; SRR1383394     2  0.0000      0.955 0.000 1.000
#&gt; SRR1383393     2  0.9491      0.424 0.368 0.632
#&gt; SRR1383396     2  0.0376      0.954 0.004 0.996
#&gt; SRR1383395     2  0.0376      0.954 0.004 0.996
#&gt; SRR1383399     2  0.9427      0.437 0.360 0.640
#&gt; SRR1383400     1  0.0000      0.936 1.000 0.000
#&gt; SRR1383397     2  0.0376      0.954 0.004 0.996
#&gt; SRR1383401     2  0.0000      0.955 0.000 1.000
#&gt; SRR1383398     2  0.0376      0.954 0.004 0.996
#&gt; SRR1383402     2  0.0000      0.955 0.000 1.000
#&gt; SRR1383404     2  0.0376      0.954 0.004 0.996
#&gt; SRR1383403     1  0.0000      0.936 1.000 0.000
#&gt; SRR1383405     2  0.0000      0.955 0.000 1.000
#&gt; SRR1383406     2  0.0376      0.954 0.004 0.996
#&gt; SRR1383407     2  0.0000      0.955 0.000 1.000
#&gt; SRR1383408     2  0.0000      0.955 0.000 1.000
#&gt; SRR1383409     2  0.0000      0.955 0.000 1.000
#&gt; SRR1383410     2  0.0000      0.955 0.000 1.000
</code></pre>

<script>
$('#tab-CV-mclust-get-classes-1-a').parent().next().next().hide();
$('#tab-CV-mclust-get-classes-1-a').click(function(){
  $('#tab-CV-mclust-get-classes-1-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-CV-mclust-get-classes-2'>
<p><a id='tab-CV-mclust-get-classes-2-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 3), get_membership(res, k = 3))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3
#&gt; SRR1383358     2  0.4178    0.67156 0.000 0.828 0.172
#&gt; SRR1383360     2  0.4121    0.77975 0.000 0.832 0.168
#&gt; SRR1383359     2  0.4521    0.71286 0.004 0.816 0.180
#&gt; SRR1383362     1  0.0000    0.84724 1.000 0.000 0.000
#&gt; SRR1383361     2  0.1289    0.79865 0.000 0.968 0.032
#&gt; SRR1383363     2  0.4002    0.67220 0.000 0.840 0.160
#&gt; SRR1383364     3  0.8287    1.00000 0.128 0.256 0.616
#&gt; SRR1383365     2  0.4291    0.62745 0.000 0.820 0.180
#&gt; SRR1383366     2  0.3412    0.79430 0.000 0.876 0.124
#&gt; SRR1383367     2  0.0237    0.79568 0.000 0.996 0.004
#&gt; SRR1383368     2  0.4062    0.78163 0.000 0.836 0.164
#&gt; SRR1383369     2  0.7749    0.00619 0.072 0.616 0.312
#&gt; SRR1383370     2  0.0237    0.79395 0.000 0.996 0.004
#&gt; SRR1383371     3  0.8287    1.00000 0.128 0.256 0.616
#&gt; SRR1383372     2  0.5178    0.61313 0.000 0.744 0.256
#&gt; SRR1383373     2  0.6267    0.15022 0.000 0.548 0.452
#&gt; SRR1383374     2  0.1031    0.78987 0.000 0.976 0.024
#&gt; SRR1383375     1  0.6662    0.54820 0.752 0.120 0.128
#&gt; SRR1383376     2  0.2066    0.77910 0.000 0.940 0.060
#&gt; SRR1383377     2  0.3752    0.78910 0.000 0.856 0.144
#&gt; SRR1383378     2  0.2878    0.80156 0.000 0.904 0.096
#&gt; SRR1383379     2  0.4121    0.77975 0.000 0.832 0.168
#&gt; SRR1383380     2  0.4121    0.77975 0.000 0.832 0.168
#&gt; SRR1383381     3  0.8287    1.00000 0.128 0.256 0.616
#&gt; SRR1383382     1  0.0000    0.84724 1.000 0.000 0.000
#&gt; SRR1383383     2  0.1753    0.78435 0.000 0.952 0.048
#&gt; SRR1383385     1  0.0000    0.84724 1.000 0.000 0.000
#&gt; SRR1383384     2  0.2261    0.77512 0.000 0.932 0.068
#&gt; SRR1383386     2  0.4293    0.77964 0.004 0.832 0.164
#&gt; SRR1383387     2  0.3116    0.79847 0.000 0.892 0.108
#&gt; SRR1383389     2  0.5178    0.61313 0.000 0.744 0.256
#&gt; SRR1383391     2  0.4887    0.64396 0.000 0.772 0.228
#&gt; SRR1383388     2  0.4121    0.77975 0.000 0.832 0.168
#&gt; SRR1383392     2  0.0892    0.78953 0.000 0.980 0.020
#&gt; SRR1383390     2  0.5178    0.61313 0.000 0.744 0.256
#&gt; SRR1383394     2  0.0424    0.79714 0.000 0.992 0.008
#&gt; SRR1383393     1  0.7372    0.43110 0.704 0.168 0.128
#&gt; SRR1383396     2  0.4062    0.78163 0.000 0.836 0.164
#&gt; SRR1383395     2  0.3752    0.78910 0.000 0.856 0.144
#&gt; SRR1383399     3  0.8287    1.00000 0.128 0.256 0.616
#&gt; SRR1383400     1  0.0000    0.84724 1.000 0.000 0.000
#&gt; SRR1383397     2  0.4121    0.77975 0.000 0.832 0.168
#&gt; SRR1383401     2  0.1031    0.78863 0.000 0.976 0.024
#&gt; SRR1383398     2  0.4121    0.77975 0.000 0.832 0.168
#&gt; SRR1383402     2  0.2356    0.77286 0.000 0.928 0.072
#&gt; SRR1383404     2  0.4121    0.77975 0.000 0.832 0.168
#&gt; SRR1383403     1  0.0000    0.84724 1.000 0.000 0.000
#&gt; SRR1383405     2  0.2959    0.79962 0.000 0.900 0.100
#&gt; SRR1383406     2  0.4121    0.77975 0.000 0.832 0.168
#&gt; SRR1383407     2  0.5178    0.61313 0.000 0.744 0.256
#&gt; SRR1383408     2  0.5178    0.61313 0.000 0.744 0.256
#&gt; SRR1383409     2  0.5178    0.61313 0.000 0.744 0.256
#&gt; SRR1383410     2  0.0892    0.78953 0.000 0.980 0.020
</code></pre>

<script>
$('#tab-CV-mclust-get-classes-2-a').parent().next().next().hide();
$('#tab-CV-mclust-get-classes-2-a').click(function(){
  $('#tab-CV-mclust-get-classes-2-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-CV-mclust-get-classes-3'>
<p><a id='tab-CV-mclust-get-classes-3-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 4), get_membership(res, k = 4))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4
#&gt; SRR1383358     3  0.5088      0.370 0.000 0.424 0.572 0.004
#&gt; SRR1383360     4  0.4193      0.923 0.000 0.268 0.000 0.732
#&gt; SRR1383359     2  0.7908     -0.387 0.000 0.360 0.336 0.304
#&gt; SRR1383362     1  0.0000      0.892 1.000 0.000 0.000 0.000
#&gt; SRR1383361     2  0.5650     -0.238 0.000 0.544 0.432 0.024
#&gt; SRR1383363     3  0.5080      0.376 0.000 0.420 0.576 0.004
#&gt; SRR1383364     3  0.0000      0.579 0.000 0.000 1.000 0.000
#&gt; SRR1383365     2  0.4857      0.201 0.000 0.668 0.324 0.008
#&gt; SRR1383366     2  0.7583     -0.493 0.000 0.420 0.196 0.384
#&gt; SRR1383367     2  0.5459     -0.224 0.000 0.552 0.432 0.016
#&gt; SRR1383368     4  0.4193      0.923 0.000 0.268 0.000 0.732
#&gt; SRR1383369     2  0.3583      0.478 0.000 0.816 0.180 0.004
#&gt; SRR1383370     2  0.5417     -0.176 0.000 0.572 0.412 0.016
#&gt; SRR1383371     3  0.0000      0.579 0.000 0.000 1.000 0.000
#&gt; SRR1383372     2  0.4193      0.544 0.000 0.732 0.000 0.268
#&gt; SRR1383373     2  0.6661      0.434 0.000 0.604 0.132 0.264
#&gt; SRR1383374     2  0.0592      0.608 0.000 0.984 0.000 0.016
#&gt; SRR1383375     1  0.5100      0.705 0.756 0.076 0.000 0.168
#&gt; SRR1383376     2  0.1474      0.582 0.000 0.948 0.000 0.052
#&gt; SRR1383377     4  0.7281      0.498 0.000 0.412 0.148 0.440
#&gt; SRR1383378     2  0.7748     -0.303 0.000 0.424 0.244 0.332
#&gt; SRR1383379     4  0.4193      0.923 0.000 0.268 0.000 0.732
#&gt; SRR1383380     4  0.4193      0.923 0.000 0.268 0.000 0.732
#&gt; SRR1383381     3  0.0000      0.579 0.000 0.000 1.000 0.000
#&gt; SRR1383382     1  0.0000      0.892 1.000 0.000 0.000 0.000
#&gt; SRR1383383     2  0.0524      0.607 0.000 0.988 0.008 0.004
#&gt; SRR1383385     1  0.0000      0.892 1.000 0.000 0.000 0.000
#&gt; SRR1383384     2  0.0336      0.607 0.000 0.992 0.000 0.008
#&gt; SRR1383386     4  0.4193      0.923 0.000 0.268 0.000 0.732
#&gt; SRR1383387     3  0.7283      0.245 0.000 0.420 0.432 0.148
#&gt; SRR1383389     2  0.4193      0.544 0.000 0.732 0.000 0.268
#&gt; SRR1383391     2  0.4134      0.547 0.000 0.740 0.000 0.260
#&gt; SRR1383388     4  0.4193      0.923 0.000 0.268 0.000 0.732
#&gt; SRR1383392     2  0.0524      0.607 0.000 0.988 0.008 0.004
#&gt; SRR1383390     2  0.4193      0.544 0.000 0.732 0.000 0.268
#&gt; SRR1383394     2  0.1557      0.580 0.000 0.944 0.000 0.056
#&gt; SRR1383393     1  0.5548      0.659 0.716 0.084 0.000 0.200
#&gt; SRR1383396     4  0.4454      0.867 0.000 0.308 0.000 0.692
#&gt; SRR1383395     4  0.7282      0.489 0.000 0.416 0.148 0.436
#&gt; SRR1383399     3  0.0000      0.579 0.000 0.000 1.000 0.000
#&gt; SRR1383400     1  0.0000      0.892 1.000 0.000 0.000 0.000
#&gt; SRR1383397     4  0.4193      0.923 0.000 0.268 0.000 0.732
#&gt; SRR1383401     2  0.0524      0.607 0.000 0.988 0.008 0.004
#&gt; SRR1383398     4  0.4193      0.923 0.000 0.268 0.000 0.732
#&gt; SRR1383402     2  0.0376      0.608 0.000 0.992 0.004 0.004
#&gt; SRR1383404     4  0.4193      0.923 0.000 0.268 0.000 0.732
#&gt; SRR1383403     1  0.0000      0.892 1.000 0.000 0.000 0.000
#&gt; SRR1383405     3  0.7283      0.245 0.000 0.420 0.432 0.148
#&gt; SRR1383406     4  0.4193      0.923 0.000 0.268 0.000 0.732
#&gt; SRR1383407     2  0.4193      0.544 0.000 0.732 0.000 0.268
#&gt; SRR1383408     2  0.4193      0.544 0.000 0.732 0.000 0.268
#&gt; SRR1383409     2  0.4193      0.544 0.000 0.732 0.000 0.268
#&gt; SRR1383410     2  0.0524      0.607 0.000 0.988 0.008 0.004
</code></pre>

<script>
$('#tab-CV-mclust-get-classes-3-a').parent().next().next().hide();
$('#tab-CV-mclust-get-classes-3-a').click(function(){
  $('#tab-CV-mclust-get-classes-3-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-CV-mclust-get-classes-4'>
<p><a id='tab-CV-mclust-get-classes-4-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 5), get_membership(res, k = 5))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4    p5
#&gt; SRR1383358     3  0.4950     0.7301 0.008 0.084 0.760 0.020 0.128
#&gt; SRR1383360     4  0.1043     0.7299 0.000 0.000 0.040 0.960 0.000
#&gt; SRR1383359     3  0.4854     0.6157 0.020 0.040 0.776 0.132 0.032
#&gt; SRR1383362     1  0.0290     0.8976 0.992 0.000 0.008 0.000 0.000
#&gt; SRR1383361     3  0.5079     0.6899 0.000 0.100 0.752 0.044 0.104
#&gt; SRR1383363     3  0.4968     0.7226 0.000 0.096 0.732 0.012 0.160
#&gt; SRR1383364     5  0.0290     0.9169 0.000 0.000 0.008 0.000 0.992
#&gt; SRR1383365     3  0.4750     0.7214 0.020 0.116 0.780 0.012 0.072
#&gt; SRR1383366     4  0.5375     0.2857 0.000 0.044 0.452 0.500 0.004
#&gt; SRR1383367     3  0.5108     0.6605 0.000 0.160 0.728 0.020 0.092
#&gt; SRR1383368     4  0.3912     0.6300 0.020 0.004 0.208 0.768 0.000
#&gt; SRR1383369     3  0.5572     0.5945 0.000 0.204 0.668 0.012 0.116
#&gt; SRR1383370     2  0.6395     0.0846 0.000 0.468 0.416 0.024 0.092
#&gt; SRR1383371     5  0.0290     0.9169 0.000 0.000 0.008 0.000 0.992
#&gt; SRR1383372     2  0.4171     0.0760 0.000 0.604 0.396 0.000 0.000
#&gt; SRR1383373     3  0.5785     0.3387 0.000 0.396 0.520 0.004 0.080
#&gt; SRR1383374     2  0.4157     0.6241 0.000 0.716 0.264 0.020 0.000
#&gt; SRR1383375     1  0.4429     0.7574 0.764 0.000 0.060 0.168 0.008
#&gt; SRR1383376     2  0.4622     0.6204 0.000 0.692 0.264 0.044 0.000
#&gt; SRR1383377     4  0.4659     0.2616 0.000 0.012 0.492 0.496 0.000
#&gt; SRR1383378     4  0.7159     0.2395 0.020 0.100 0.344 0.496 0.040
#&gt; SRR1383379     4  0.0290     0.7276 0.000 0.000 0.008 0.992 0.000
#&gt; SRR1383380     4  0.0290     0.7311 0.000 0.000 0.008 0.992 0.000
#&gt; SRR1383381     5  0.2179     0.8773 0.000 0.000 0.112 0.000 0.888
#&gt; SRR1383382     1  0.0290     0.8976 0.992 0.000 0.008 0.000 0.000
#&gt; SRR1383383     2  0.4387     0.5787 0.000 0.640 0.348 0.012 0.000
#&gt; SRR1383385     1  0.0609     0.8951 0.980 0.000 0.020 0.000 0.000
#&gt; SRR1383384     2  0.3882     0.6497 0.000 0.756 0.224 0.020 0.000
#&gt; SRR1383386     4  0.3176     0.6833 0.064 0.000 0.080 0.856 0.000
#&gt; SRR1383387     4  0.7464     0.3197 0.000 0.280 0.140 0.488 0.092
#&gt; SRR1383389     2  0.4235    -0.0576 0.000 0.576 0.424 0.000 0.000
#&gt; SRR1383391     2  0.2127     0.6104 0.000 0.892 0.108 0.000 0.000
#&gt; SRR1383388     4  0.0880     0.7330 0.000 0.000 0.032 0.968 0.000
#&gt; SRR1383392     2  0.3970     0.6464 0.000 0.752 0.224 0.024 0.000
#&gt; SRR1383390     2  0.1851     0.5843 0.000 0.912 0.088 0.000 0.000
#&gt; SRR1383394     2  0.4713     0.6042 0.000 0.676 0.280 0.044 0.000
#&gt; SRR1383393     1  0.4466     0.7532 0.760 0.000 0.060 0.172 0.008
#&gt; SRR1383396     4  0.4810     0.5762 0.020 0.024 0.264 0.692 0.000
#&gt; SRR1383395     4  0.4294     0.3205 0.000 0.000 0.468 0.532 0.000
#&gt; SRR1383399     5  0.1732     0.9117 0.000 0.000 0.080 0.000 0.920
#&gt; SRR1383400     1  0.0290     0.8976 0.992 0.000 0.008 0.000 0.000
#&gt; SRR1383397     4  0.0609     0.7272 0.000 0.000 0.020 0.980 0.000
#&gt; SRR1383401     3  0.4270     0.3789 0.000 0.320 0.668 0.012 0.000
#&gt; SRR1383398     4  0.0290     0.7311 0.000 0.000 0.008 0.992 0.000
#&gt; SRR1383402     2  0.3882     0.6497 0.000 0.756 0.224 0.020 0.000
#&gt; SRR1383404     4  0.1478     0.7248 0.000 0.000 0.064 0.936 0.000
#&gt; SRR1383403     1  0.0609     0.8951 0.980 0.000 0.020 0.000 0.000
#&gt; SRR1383405     4  0.7590     0.2076 0.000 0.328 0.140 0.440 0.092
#&gt; SRR1383406     4  0.0703     0.7293 0.000 0.000 0.024 0.976 0.000
#&gt; SRR1383407     2  0.3999     0.2258 0.000 0.656 0.344 0.000 0.000
#&gt; SRR1383408     2  0.2179     0.5998 0.000 0.888 0.112 0.000 0.000
#&gt; SRR1383409     2  0.1732     0.5894 0.000 0.920 0.080 0.000 0.000
#&gt; SRR1383410     2  0.3970     0.6464 0.000 0.752 0.224 0.024 0.000
</code></pre>

<script>
$('#tab-CV-mclust-get-classes-4-a').parent().next().next().hide();
$('#tab-CV-mclust-get-classes-4-a').click(function(){
  $('#tab-CV-mclust-get-classes-4-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-CV-mclust-get-classes-5'>
<p><a id='tab-CV-mclust-get-classes-5-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 6), get_membership(res, k = 6))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4    p5    p6
#&gt; SRR1383358     3  0.2380     0.4084 0.000 0.048 0.900 0.000 0.036 0.016
#&gt; SRR1383360     4  0.1984     0.7470 0.000 0.000 0.056 0.912 0.000 0.032
#&gt; SRR1383359     3  0.5717     0.4618 0.000 0.040 0.640 0.208 0.012 0.100
#&gt; SRR1383362     1  0.0000     0.8608 1.000 0.000 0.000 0.000 0.000 0.000
#&gt; SRR1383361     3  0.4708     0.4341 0.000 0.016 0.736 0.156 0.016 0.076
#&gt; SRR1383363     3  0.3406     0.3882 0.000 0.096 0.828 0.000 0.064 0.012
#&gt; SRR1383364     5  0.0790     0.9120 0.000 0.000 0.032 0.000 0.968 0.000
#&gt; SRR1383365     3  0.4428     0.3035 0.000 0.120 0.740 0.000 0.012 0.128
#&gt; SRR1383366     3  0.5443     0.2103 0.000 0.000 0.492 0.384 0.000 0.124
#&gt; SRR1383367     3  0.5439     0.3760 0.000 0.056 0.696 0.140 0.016 0.092
#&gt; SRR1383368     4  0.5310     0.6133 0.024 0.016 0.160 0.688 0.000 0.112
#&gt; SRR1383369     3  0.6331     0.1896 0.000 0.156 0.580 0.000 0.104 0.160
#&gt; SRR1383370     3  0.6697     0.0756 0.000 0.100 0.552 0.108 0.016 0.224
#&gt; SRR1383371     5  0.0790     0.9120 0.000 0.000 0.032 0.000 0.968 0.000
#&gt; SRR1383372     2  0.3073     0.6431 0.000 0.816 0.164 0.000 0.004 0.016
#&gt; SRR1383373     2  0.5460     0.4465 0.000 0.560 0.324 0.000 0.104 0.012
#&gt; SRR1383374     2  0.5937    -0.2923 0.000 0.476 0.204 0.000 0.004 0.316
#&gt; SRR1383375     1  0.6017     0.6872 0.628 0.004 0.020 0.148 0.028 0.172
#&gt; SRR1383376     6  0.6613     0.6777 0.000 0.288 0.228 0.040 0.000 0.444
#&gt; SRR1383377     3  0.5923     0.1549 0.000 0.000 0.428 0.388 0.004 0.180
#&gt; SRR1383378     4  0.6583    -0.0294 0.000 0.112 0.404 0.404 0.000 0.080
#&gt; SRR1383379     4  0.0547     0.7406 0.000 0.000 0.000 0.980 0.000 0.020
#&gt; SRR1383380     4  0.1268     0.7483 0.008 0.000 0.036 0.952 0.000 0.004
#&gt; SRR1383381     5  0.2442     0.8727 0.000 0.004 0.144 0.000 0.852 0.000
#&gt; SRR1383382     1  0.0603     0.8573 0.980 0.000 0.000 0.000 0.004 0.016
#&gt; SRR1383383     3  0.5771    -0.2078 0.000 0.396 0.460 0.000 0.008 0.136
#&gt; SRR1383385     1  0.1219     0.8607 0.948 0.004 0.000 0.000 0.000 0.048
#&gt; SRR1383384     6  0.6063     0.7108 0.000 0.368 0.216 0.004 0.000 0.412
#&gt; SRR1383386     4  0.3466     0.7152 0.060 0.000 0.036 0.836 0.000 0.068
#&gt; SRR1383387     4  0.7132     0.0804 0.000 0.120 0.224 0.492 0.012 0.152
#&gt; SRR1383389     2  0.3329     0.6379 0.000 0.792 0.184 0.000 0.004 0.020
#&gt; SRR1383391     2  0.3907     0.3635 0.000 0.764 0.152 0.000 0.000 0.084
#&gt; SRR1383388     4  0.2152     0.7525 0.012 0.000 0.040 0.912 0.000 0.036
#&gt; SRR1383392     6  0.6035     0.5550 0.000 0.300 0.236 0.000 0.004 0.460
#&gt; SRR1383390     2  0.0692     0.5881 0.000 0.976 0.004 0.000 0.000 0.020
#&gt; SRR1383394     6  0.6628     0.6685 0.000 0.272 0.244 0.040 0.000 0.444
#&gt; SRR1383393     1  0.6017     0.6872 0.628 0.004 0.020 0.148 0.028 0.172
#&gt; SRR1383396     4  0.4938     0.5861 0.008 0.012 0.232 0.676 0.000 0.072
#&gt; SRR1383395     3  0.5799     0.1515 0.000 0.000 0.428 0.392 0.000 0.180
#&gt; SRR1383399     5  0.1957     0.9058 0.000 0.000 0.112 0.000 0.888 0.000
#&gt; SRR1383400     1  0.0603     0.8573 0.980 0.000 0.000 0.000 0.004 0.016
#&gt; SRR1383397     4  0.0547     0.7406 0.000 0.000 0.000 0.980 0.000 0.020
#&gt; SRR1383401     3  0.5707     0.0341 0.000 0.256 0.556 0.000 0.008 0.180
#&gt; SRR1383398     4  0.1152     0.7459 0.000 0.000 0.044 0.952 0.000 0.004
#&gt; SRR1383402     6  0.6053     0.7052 0.000 0.376 0.212 0.004 0.000 0.408
#&gt; SRR1383404     4  0.2803     0.7388 0.012 0.000 0.052 0.872 0.000 0.064
#&gt; SRR1383403     1  0.1219     0.8607 0.948 0.004 0.000 0.000 0.000 0.048
#&gt; SRR1383405     4  0.7163     0.0718 0.000 0.124 0.224 0.488 0.012 0.152
#&gt; SRR1383406     4  0.0692     0.7416 0.000 0.000 0.004 0.976 0.000 0.020
#&gt; SRR1383407     2  0.3037     0.6444 0.000 0.820 0.160 0.000 0.004 0.016
#&gt; SRR1383408     2  0.3017     0.4733 0.000 0.840 0.108 0.000 0.000 0.052
#&gt; SRR1383409     2  0.1265     0.5785 0.000 0.948 0.008 0.000 0.000 0.044
#&gt; SRR1383410     6  0.6127     0.6003 0.000 0.312 0.220 0.004 0.004 0.460
</code></pre>

<script>
$('#tab-CV-mclust-get-classes-5-a').parent().next().next().hide();
$('#tab-CV-mclust-get-classes-5-a').click(function(){
  $('#tab-CV-mclust-get-classes-5-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>
</div>

Heatmaps for the consensus matrix. It visualizes the probability of two
samples to be in a same group.



<script>
$( function() {
	$( '#tabs-CV-mclust-consensus-heatmap' ).tabs();
} );
</script>
<div id='tabs-CV-mclust-consensus-heatmap'>
<ul>
<li><a href='#tab-CV-mclust-consensus-heatmap-1'>k = 2</a></li>
<li><a href='#tab-CV-mclust-consensus-heatmap-2'>k = 3</a></li>
<li><a href='#tab-CV-mclust-consensus-heatmap-3'>k = 4</a></li>
<li><a href='#tab-CV-mclust-consensus-heatmap-4'>k = 5</a></li>
<li><a href='#tab-CV-mclust-consensus-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-CV-mclust-consensus-heatmap-1'>
<pre><code class="r">consensus_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-CV-mclust-consensus-heatmap-1-1.png" alt="plot of chunk tab-CV-mclust-consensus-heatmap-1"/></p>

</div>
<div id='tab-CV-mclust-consensus-heatmap-2'>
<pre><code class="r">consensus_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-CV-mclust-consensus-heatmap-2-1.png" alt="plot of chunk tab-CV-mclust-consensus-heatmap-2"/></p>

</div>
<div id='tab-CV-mclust-consensus-heatmap-3'>
<pre><code class="r">consensus_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-CV-mclust-consensus-heatmap-3-1.png" alt="plot of chunk tab-CV-mclust-consensus-heatmap-3"/></p>

</div>
<div id='tab-CV-mclust-consensus-heatmap-4'>
<pre><code class="r">consensus_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-CV-mclust-consensus-heatmap-4-1.png" alt="plot of chunk tab-CV-mclust-consensus-heatmap-4"/></p>

</div>
<div id='tab-CV-mclust-consensus-heatmap-5'>
<pre><code class="r">consensus_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-CV-mclust-consensus-heatmap-5-1.png" alt="plot of chunk tab-CV-mclust-consensus-heatmap-5"/></p>

</div>
</div>

Heatmaps for the membership of samples in all partitions to see how consistent they are:




<script>
$( function() {
	$( '#tabs-CV-mclust-membership-heatmap' ).tabs();
} );
</script>
<div id='tabs-CV-mclust-membership-heatmap'>
<ul>
<li><a href='#tab-CV-mclust-membership-heatmap-1'>k = 2</a></li>
<li><a href='#tab-CV-mclust-membership-heatmap-2'>k = 3</a></li>
<li><a href='#tab-CV-mclust-membership-heatmap-3'>k = 4</a></li>
<li><a href='#tab-CV-mclust-membership-heatmap-4'>k = 5</a></li>
<li><a href='#tab-CV-mclust-membership-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-CV-mclust-membership-heatmap-1'>
<pre><code class="r">membership_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-CV-mclust-membership-heatmap-1-1.png" alt="plot of chunk tab-CV-mclust-membership-heatmap-1"/></p>

</div>
<div id='tab-CV-mclust-membership-heatmap-2'>
<pre><code class="r">membership_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-CV-mclust-membership-heatmap-2-1.png" alt="plot of chunk tab-CV-mclust-membership-heatmap-2"/></p>

</div>
<div id='tab-CV-mclust-membership-heatmap-3'>
<pre><code class="r">membership_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-CV-mclust-membership-heatmap-3-1.png" alt="plot of chunk tab-CV-mclust-membership-heatmap-3"/></p>

</div>
<div id='tab-CV-mclust-membership-heatmap-4'>
<pre><code class="r">membership_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-CV-mclust-membership-heatmap-4-1.png" alt="plot of chunk tab-CV-mclust-membership-heatmap-4"/></p>

</div>
<div id='tab-CV-mclust-membership-heatmap-5'>
<pre><code class="r">membership_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-CV-mclust-membership-heatmap-5-1.png" alt="plot of chunk tab-CV-mclust-membership-heatmap-5"/></p>

</div>
</div>

As soon as we have had the classes for columns, we can look for signatures
which are significantly different between classes which can be candidate marks
for certain classes. Following are the heatmaps for signatures.



Signature heatmaps where rows are scaled:



<script>
$( function() {
	$( '#tabs-CV-mclust-get-signatures' ).tabs();
} );
</script>
<div id='tabs-CV-mclust-get-signatures'>
<ul>
<li><a href='#tab-CV-mclust-get-signatures-1'>k = 2</a></li>
<li><a href='#tab-CV-mclust-get-signatures-2'>k = 3</a></li>
<li><a href='#tab-CV-mclust-get-signatures-3'>k = 4</a></li>
<li><a href='#tab-CV-mclust-get-signatures-4'>k = 5</a></li>
<li><a href='#tab-CV-mclust-get-signatures-5'>k = 6</a></li>
</ul>
<div id='tab-CV-mclust-get-signatures-1'>
<pre><code class="r">get_signatures(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-CV-mclust-get-signatures-1-1.png" alt="plot of chunk tab-CV-mclust-get-signatures-1"/></p>

</div>
<div id='tab-CV-mclust-get-signatures-2'>
<pre><code class="r">get_signatures(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-CV-mclust-get-signatures-2-1.png" alt="plot of chunk tab-CV-mclust-get-signatures-2"/></p>

</div>
<div id='tab-CV-mclust-get-signatures-3'>
<pre><code class="r">get_signatures(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-CV-mclust-get-signatures-3-1.png" alt="plot of chunk tab-CV-mclust-get-signatures-3"/></p>

</div>
<div id='tab-CV-mclust-get-signatures-4'>
<pre><code class="r">get_signatures(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-CV-mclust-get-signatures-4-1.png" alt="plot of chunk tab-CV-mclust-get-signatures-4"/></p>

</div>
<div id='tab-CV-mclust-get-signatures-5'>
<pre><code class="r">get_signatures(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-CV-mclust-get-signatures-5-1.png" alt="plot of chunk tab-CV-mclust-get-signatures-5"/></p>

</div>
</div>



Signature heatmaps where rows are not scaled:


<script>
$( function() {
	$( '#tabs-CV-mclust-get-signatures-no-scale' ).tabs();
} );
</script>
<div id='tabs-CV-mclust-get-signatures-no-scale'>
<ul>
<li><a href='#tab-CV-mclust-get-signatures-no-scale-1'>k = 2</a></li>
<li><a href='#tab-CV-mclust-get-signatures-no-scale-2'>k = 3</a></li>
<li><a href='#tab-CV-mclust-get-signatures-no-scale-3'>k = 4</a></li>
<li><a href='#tab-CV-mclust-get-signatures-no-scale-4'>k = 5</a></li>
<li><a href='#tab-CV-mclust-get-signatures-no-scale-5'>k = 6</a></li>
</ul>
<div id='tab-CV-mclust-get-signatures-no-scale-1'>
<pre><code class="r">get_signatures(res, k = 2, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-CV-mclust-get-signatures-no-scale-1-1.png" alt="plot of chunk tab-CV-mclust-get-signatures-no-scale-1"/></p>

</div>
<div id='tab-CV-mclust-get-signatures-no-scale-2'>
<pre><code class="r">get_signatures(res, k = 3, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-CV-mclust-get-signatures-no-scale-2-1.png" alt="plot of chunk tab-CV-mclust-get-signatures-no-scale-2"/></p>

</div>
<div id='tab-CV-mclust-get-signatures-no-scale-3'>
<pre><code class="r">get_signatures(res, k = 4, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-CV-mclust-get-signatures-no-scale-3-1.png" alt="plot of chunk tab-CV-mclust-get-signatures-no-scale-3"/></p>

</div>
<div id='tab-CV-mclust-get-signatures-no-scale-4'>
<pre><code class="r">get_signatures(res, k = 5, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-CV-mclust-get-signatures-no-scale-4-1.png" alt="plot of chunk tab-CV-mclust-get-signatures-no-scale-4"/></p>

</div>
<div id='tab-CV-mclust-get-signatures-no-scale-5'>
<pre><code class="r">get_signatures(res, k = 6, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-CV-mclust-get-signatures-no-scale-5-1.png" alt="plot of chunk tab-CV-mclust-get-signatures-no-scale-5"/></p>

</div>
</div>



Compare the overlap of signatures from different k:

```r
compare_signatures(res)
```

![plot of chunk CV-mclust-signature_compare](figure_cola/CV-mclust-signature_compare-1.png)

`get_signature()` returns a data frame invisibly. TO get the list of signatures, the function
call should be assigned to a variable explicitly. In following code, if `plot` argument is set
to `FALSE`, no heatmap is plotted while only the differential analysis is performed.

```r
# code only for demonstration
tb = get_signature(res, k = ..., plot = FALSE)
```

An example of the output of `tb` is:

```
#>   which_row         fdr    mean_1    mean_2 scaled_mean_1 scaled_mean_2 km
#> 1        38 0.042760348  8.373488  9.131774    -0.5533452     0.5164555  1
#> 2        40 0.018707592  7.106213  8.469186    -0.6173731     0.5762149  1
#> 3        55 0.019134737 10.221463 11.207825    -0.6159697     0.5749050  1
#> 4        59 0.006059896  5.921854  7.869574    -0.6899429     0.6439467  1
#> 5        60 0.018055526  8.928898 10.211722    -0.6204761     0.5791110  1
#> 6        98 0.009384629 15.714769 14.887706     0.6635654    -0.6193277  2
...
```

The columns in `tb` are:

1. `which_row`: row indices corresponding to the input matrix.
2. `fdr`: FDR for the differential test. 
3. `mean_x`: The mean value in group x.
4. `scaled_mean_x`: The mean value in group x after rows are scaled.
5. `km`: Row groups if k-means clustering is applied to rows.



UMAP plot which shows how samples are separated.


<script>
$( function() {
	$( '#tabs-CV-mclust-dimension-reduction' ).tabs();
} );
</script>
<div id='tabs-CV-mclust-dimension-reduction'>
<ul>
<li><a href='#tab-CV-mclust-dimension-reduction-1'>k = 2</a></li>
<li><a href='#tab-CV-mclust-dimension-reduction-2'>k = 3</a></li>
<li><a href='#tab-CV-mclust-dimension-reduction-3'>k = 4</a></li>
<li><a href='#tab-CV-mclust-dimension-reduction-4'>k = 5</a></li>
<li><a href='#tab-CV-mclust-dimension-reduction-5'>k = 6</a></li>
</ul>
<div id='tab-CV-mclust-dimension-reduction-1'>
<pre><code class="r">dimension_reduction(res, k = 2, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-CV-mclust-dimension-reduction-1-1.png" alt="plot of chunk tab-CV-mclust-dimension-reduction-1"/></p>

</div>
<div id='tab-CV-mclust-dimension-reduction-2'>
<pre><code class="r">dimension_reduction(res, k = 3, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-CV-mclust-dimension-reduction-2-1.png" alt="plot of chunk tab-CV-mclust-dimension-reduction-2"/></p>

</div>
<div id='tab-CV-mclust-dimension-reduction-3'>
<pre><code class="r">dimension_reduction(res, k = 4, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-CV-mclust-dimension-reduction-3-1.png" alt="plot of chunk tab-CV-mclust-dimension-reduction-3"/></p>

</div>
<div id='tab-CV-mclust-dimension-reduction-4'>
<pre><code class="r">dimension_reduction(res, k = 5, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-CV-mclust-dimension-reduction-4-1.png" alt="plot of chunk tab-CV-mclust-dimension-reduction-4"/></p>

</div>
<div id='tab-CV-mclust-dimension-reduction-5'>
<pre><code class="r">dimension_reduction(res, k = 6, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-CV-mclust-dimension-reduction-5-1.png" alt="plot of chunk tab-CV-mclust-dimension-reduction-5"/></p>

</div>
</div>


Following heatmap shows how subgroups are split when increasing `k`:

```r
collect_classes(res)
```

![plot of chunk CV-mclust-collect-classes](figure_cola/CV-mclust-collect-classes-1.png)


If matrix rows can be associated to genes, consider to use `functional_enrichment(res,
...)` to perform function enrichment for the signature genes. See [this vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/functional_enrichment.html) for more detailed explanations.


 

---------------------------------------------------




### CV:NMF**






The object with results only for a single top-value method and a single partition method 
can be extracted as:

```r
res = res_list["CV", "NMF"]
# you can also extract it by
# res = res_list["CV:NMF"]
```

A summary of `res` and all the functions that can be applied to it:

```r
res
```

```
#> A 'ConsensusPartition' object with k = 2, 3, 4, 5, 6.
#>   On a matrix with 15680 rows and 53 columns.
#>   Top rows (1000, 2000, 3000, 4000, 5000) are extracted by 'CV' method.
#>   Subgroups are detected by 'NMF' method.
#>   Performed in total 1250 partitions by row resampling.
#>   Best k for subgroups seems to be 2.
#> 
#> Following methods can be applied to this 'ConsensusPartition' object:
#>  [1] "cola_report"             "collect_classes"         "collect_plots"          
#>  [4] "collect_stats"           "colnames"                "compare_signatures"     
#>  [7] "consensus_heatmap"       "dimension_reduction"     "functional_enrichment"  
#> [10] "get_anno_col"            "get_anno"                "get_classes"            
#> [13] "get_consensus"           "get_matrix"              "get_membership"         
#> [16] "get_param"               "get_signatures"          "get_stats"              
#> [19] "is_best_k"               "is_stable_k"             "membership_heatmap"     
#> [22] "ncol"                    "nrow"                    "plot_ecdf"              
#> [25] "rownames"                "select_partition_number" "show"                   
#> [28] "suggest_best_k"          "test_to_known_factors"
```

`collect_plots()` function collects all the plots made from `res` for all `k` (number of partitions)
into one single page to provide an easy and fast comparison between different `k`.

```r
collect_plots(res)
```

![plot of chunk CV-NMF-collect-plots](figure_cola/CV-NMF-collect-plots-1.png)

The plots are:

- The first row: a plot of the ECDF (empirical cumulative distribution
  function) curves of the consensus matrix for each `k` and the heatmap of
  predicted classes for each `k`.
- The second row: heatmaps of the consensus matrix for each `k`.
- The third row: heatmaps of the membership matrix for each `k`.
- The fouth row: heatmaps of the signatures for each `k`.

All the plots in panels can be made by individual functions and they are
plotted later in this section.

`select_partition_number()` produces several plots showing different
statistics for choosing "optimized" `k`. There are following statistics:

- ECDF curves of the consensus matrix for each `k`;
- 1-PAC. [The PAC
  score](https://en.wikipedia.org/wiki/Consensus_clustering#Over-interpretation_potential_of_consensus_clustering)
  measures the proportion of the ambiguous subgrouping.
- Mean silhouette score.
- Concordance. The mean probability of fiting the consensus class ids in all
  partitions.
- Area increased. Denote $A_k$ as the area under the ECDF curve for current
  `k`, the area increased is defined as $A_k - A_{k-1}$.
- Rand index. The percent of pairs of samples that are both in a same cluster
  or both are not in a same cluster in the partition of k and k-1.
- Jaccard index. The ratio of pairs of samples are both in a same cluster in
  the partition of k and k-1 and the pairs of samples are both in a same
  cluster in the partition k or k-1.

The detailed explanations of these statistics can be found in [the _cola_
vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/cola.html#toc_13).

Generally speaking, lower PAC score, higher mean silhouette score or higher
concordance corresponds to better partition. Rand index and Jaccard index
measure how similar the current partition is compared to partition with `k-1`.
If they are too similar, we won't accept `k` is better than `k-1`.

```r
select_partition_number(res)
```

![plot of chunk CV-NMF-select-partition-number](figure_cola/CV-NMF-select-partition-number-1.png)

The numeric values for all these statistics can be obtained by `get_stats()`.

```r
get_stats(res)
```

```
#>   k 1-PAC mean_silhouette concordance area_increased  Rand Jaccard
#> 2 2 1.000           0.953       0.981         0.4179 0.570   0.570
#> 3 3 0.740           0.822       0.926         0.5778 0.705   0.510
#> 4 4 0.587           0.626       0.793         0.1341 0.816   0.525
#> 5 5 0.745           0.651       0.841         0.0677 0.845   0.495
#> 6 6 0.813           0.732       0.870         0.0426 0.884   0.518
```

`suggest_best_k()` suggests the best $k$ based on these statistics. The rules are as follows:

- All $k$ with Jaccard index larger than 0.95 are removed because increasing
  $k$ does not provide enough extra information. If all $k$ are removed, it is
  marked as no subgroup is detected.
- For all $k$ with 1-PAC score larger than 0.9, the maximal $k$ is taken as
  the best $k$, and other $k$ are marked as optional $k$.
- If it does not fit the second rule. The $k$ with the maximal vote of the
  highest 1-PAC score, highest mean silhouette, and highest concordance is
  taken as the best $k$.

```r
suggest_best_k(res)
```

```
#> [1] 2
```


Following shows the table of the partitions (You need to click the **show/hide
code output** link to see it). The membership matrix (columns with name `p*`)
is inferred by
[`clue::cl_consensus()`](https://www.rdocumentation.org/link/cl_consensus?package=clue)
function with the `SE` method. Basically the value in the membership matrix
represents the probability to belong to a certain group. The finall class
label for an item is determined with the group with highest probability it
belongs to.

In `get_classes()` function, the entropy is calculated from the membership
matrix and the silhouette score is calculated from the consensus matrix.



<script>
$( function() {
	$( '#tabs-CV-NMF-get-classes' ).tabs();
} );
</script>
<div id='tabs-CV-NMF-get-classes'>
<ul>
<li><a href='#tab-CV-NMF-get-classes-1'>k = 2</a></li>
<li><a href='#tab-CV-NMF-get-classes-2'>k = 3</a></li>
<li><a href='#tab-CV-NMF-get-classes-3'>k = 4</a></li>
<li><a href='#tab-CV-NMF-get-classes-4'>k = 5</a></li>
<li><a href='#tab-CV-NMF-get-classes-5'>k = 6</a></li>
</ul>

<div id='tab-CV-NMF-get-classes-1'>
<p><a id='tab-CV-NMF-get-classes-1-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 2), get_membership(res, k = 2))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2
#&gt; SRR1383358     2  0.0000      0.995 0.000 1.000
#&gt; SRR1383360     1  0.0938      0.935 0.988 0.012
#&gt; SRR1383359     2  0.0000      0.995 0.000 1.000
#&gt; SRR1383362     1  0.0000      0.941 1.000 0.000
#&gt; SRR1383361     2  0.0000      0.995 0.000 1.000
#&gt; SRR1383363     2  0.0000      0.995 0.000 1.000
#&gt; SRR1383364     2  0.1414      0.977 0.020 0.980
#&gt; SRR1383365     2  0.0000      0.995 0.000 1.000
#&gt; SRR1383366     2  0.0000      0.995 0.000 1.000
#&gt; SRR1383367     2  0.0000      0.995 0.000 1.000
#&gt; SRR1383368     1  0.2043      0.921 0.968 0.032
#&gt; SRR1383369     2  0.0000      0.995 0.000 1.000
#&gt; SRR1383370     2  0.0000      0.995 0.000 1.000
#&gt; SRR1383371     2  0.0000      0.995 0.000 1.000
#&gt; SRR1383372     2  0.0000      0.995 0.000 1.000
#&gt; SRR1383373     2  0.0000      0.995 0.000 1.000
#&gt; SRR1383374     2  0.0000      0.995 0.000 1.000
#&gt; SRR1383375     1  0.0000      0.941 1.000 0.000
#&gt; SRR1383376     2  0.0000      0.995 0.000 1.000
#&gt; SRR1383377     2  0.0376      0.992 0.004 0.996
#&gt; SRR1383378     2  0.0000      0.995 0.000 1.000
#&gt; SRR1383379     1  0.9866      0.280 0.568 0.432
#&gt; SRR1383380     1  0.0000      0.941 1.000 0.000
#&gt; SRR1383381     2  0.0000      0.995 0.000 1.000
#&gt; SRR1383382     1  0.0000      0.941 1.000 0.000
#&gt; SRR1383383     2  0.0000      0.995 0.000 1.000
#&gt; SRR1383385     1  0.0000      0.941 1.000 0.000
#&gt; SRR1383384     2  0.0000      0.995 0.000 1.000
#&gt; SRR1383386     1  0.0000      0.941 1.000 0.000
#&gt; SRR1383387     2  0.0000      0.995 0.000 1.000
#&gt; SRR1383389     2  0.0000      0.995 0.000 1.000
#&gt; SRR1383391     2  0.0000      0.995 0.000 1.000
#&gt; SRR1383388     1  0.0938      0.935 0.988 0.012
#&gt; SRR1383392     2  0.0000      0.995 0.000 1.000
#&gt; SRR1383390     2  0.0000      0.995 0.000 1.000
#&gt; SRR1383394     2  0.0000      0.995 0.000 1.000
#&gt; SRR1383393     1  0.0000      0.941 1.000 0.000
#&gt; SRR1383396     1  0.9580      0.420 0.620 0.380
#&gt; SRR1383395     2  0.1184      0.981 0.016 0.984
#&gt; SRR1383399     2  0.0000      0.995 0.000 1.000
#&gt; SRR1383400     1  0.0000      0.941 1.000 0.000
#&gt; SRR1383397     2  0.3879      0.915 0.076 0.924
#&gt; SRR1383401     2  0.0000      0.995 0.000 1.000
#&gt; SRR1383398     1  0.0376      0.940 0.996 0.004
#&gt; SRR1383402     2  0.0000      0.995 0.000 1.000
#&gt; SRR1383404     1  0.0000      0.941 1.000 0.000
#&gt; SRR1383403     1  0.0000      0.941 1.000 0.000
#&gt; SRR1383405     2  0.0000      0.995 0.000 1.000
#&gt; SRR1383406     2  0.2236      0.961 0.036 0.964
#&gt; SRR1383407     2  0.0000      0.995 0.000 1.000
#&gt; SRR1383408     2  0.0000      0.995 0.000 1.000
#&gt; SRR1383409     2  0.0000      0.995 0.000 1.000
#&gt; SRR1383410     2  0.0000      0.995 0.000 1.000
</code></pre>

<script>
$('#tab-CV-NMF-get-classes-1-a').parent().next().next().hide();
$('#tab-CV-NMF-get-classes-1-a').click(function(){
  $('#tab-CV-NMF-get-classes-1-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-CV-NMF-get-classes-2'>
<p><a id='tab-CV-NMF-get-classes-2-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 3), get_membership(res, k = 3))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3
#&gt; SRR1383358     3  0.0000     0.9101 0.000 0.000 1.000
#&gt; SRR1383360     1  0.0475     0.9280 0.992 0.004 0.004
#&gt; SRR1383359     3  0.2165     0.8726 0.000 0.064 0.936
#&gt; SRR1383362     1  0.0000     0.9314 1.000 0.000 0.000
#&gt; SRR1383361     3  0.5882     0.4336 0.000 0.348 0.652
#&gt; SRR1383363     3  0.0000     0.9101 0.000 0.000 1.000
#&gt; SRR1383364     3  0.0000     0.9101 0.000 0.000 1.000
#&gt; SRR1383365     3  0.0000     0.9101 0.000 0.000 1.000
#&gt; SRR1383366     2  0.0000     0.8968 0.000 1.000 0.000
#&gt; SRR1383367     3  0.2537     0.8630 0.000 0.080 0.920
#&gt; SRR1383368     1  0.0000     0.9314 1.000 0.000 0.000
#&gt; SRR1383369     3  0.0000     0.9101 0.000 0.000 1.000
#&gt; SRR1383370     2  0.1411     0.8765 0.000 0.964 0.036
#&gt; SRR1383371     3  0.0000     0.9101 0.000 0.000 1.000
#&gt; SRR1383372     3  0.0237     0.9088 0.000 0.004 0.996
#&gt; SRR1383373     3  0.0000     0.9101 0.000 0.000 1.000
#&gt; SRR1383374     2  0.4399     0.7413 0.000 0.812 0.188
#&gt; SRR1383375     1  0.0000     0.9314 1.000 0.000 0.000
#&gt; SRR1383376     2  0.0000     0.8968 0.000 1.000 0.000
#&gt; SRR1383377     2  0.4931     0.6478 0.000 0.768 0.232
#&gt; SRR1383378     2  0.6062     0.3981 0.000 0.616 0.384
#&gt; SRR1383379     2  0.0000     0.8968 0.000 1.000 0.000
#&gt; SRR1383380     1  0.3752     0.8178 0.856 0.144 0.000
#&gt; SRR1383381     3  0.0000     0.9101 0.000 0.000 1.000
#&gt; SRR1383382     1  0.0000     0.9314 1.000 0.000 0.000
#&gt; SRR1383383     2  0.6305     0.0998 0.000 0.516 0.484
#&gt; SRR1383385     1  0.0000     0.9314 1.000 0.000 0.000
#&gt; SRR1383384     2  0.0000     0.8968 0.000 1.000 0.000
#&gt; SRR1383386     1  0.0000     0.9314 1.000 0.000 0.000
#&gt; SRR1383387     2  0.0000     0.8968 0.000 1.000 0.000
#&gt; SRR1383389     3  0.3816     0.7883 0.000 0.148 0.852
#&gt; SRR1383391     2  0.0000     0.8968 0.000 1.000 0.000
#&gt; SRR1383388     2  0.0892     0.8846 0.020 0.980 0.000
#&gt; SRR1383392     2  0.0000     0.8968 0.000 1.000 0.000
#&gt; SRR1383390     2  0.5810     0.5057 0.000 0.664 0.336
#&gt; SRR1383394     2  0.0000     0.8968 0.000 1.000 0.000
#&gt; SRR1383393     1  0.0000     0.9314 1.000 0.000 0.000
#&gt; SRR1383396     1  0.6047     0.5101 0.680 0.008 0.312
#&gt; SRR1383395     2  0.0592     0.8913 0.000 0.988 0.012
#&gt; SRR1383399     3  0.0000     0.9101 0.000 0.000 1.000
#&gt; SRR1383400     1  0.0000     0.9314 1.000 0.000 0.000
#&gt; SRR1383397     2  0.0000     0.8968 0.000 1.000 0.000
#&gt; SRR1383401     3  0.3116     0.8343 0.000 0.108 0.892
#&gt; SRR1383398     1  0.5760     0.5443 0.672 0.328 0.000
#&gt; SRR1383402     2  0.0000     0.8968 0.000 1.000 0.000
#&gt; SRR1383404     1  0.1031     0.9167 0.976 0.024 0.000
#&gt; SRR1383403     1  0.0000     0.9314 1.000 0.000 0.000
#&gt; SRR1383405     2  0.0000     0.8968 0.000 1.000 0.000
#&gt; SRR1383406     2  0.0000     0.8968 0.000 1.000 0.000
#&gt; SRR1383407     3  0.6026     0.3319 0.000 0.376 0.624
#&gt; SRR1383408     2  0.5216     0.6380 0.000 0.740 0.260
#&gt; SRR1383409     2  0.0892     0.8873 0.000 0.980 0.020
#&gt; SRR1383410     2  0.0000     0.8968 0.000 1.000 0.000
</code></pre>

<script>
$('#tab-CV-NMF-get-classes-2-a').parent().next().next().hide();
$('#tab-CV-NMF-get-classes-2-a').click(function(){
  $('#tab-CV-NMF-get-classes-2-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-CV-NMF-get-classes-3'>
<p><a id='tab-CV-NMF-get-classes-3-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 4), get_membership(res, k = 4))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4
#&gt; SRR1383358     3  0.3688     0.7955 0.000 0.000 0.792 0.208
#&gt; SRR1383360     4  0.4103     0.3075 0.256 0.000 0.000 0.744
#&gt; SRR1383359     3  0.4040     0.7745 0.000 0.000 0.752 0.248
#&gt; SRR1383362     1  0.0000     0.7918 1.000 0.000 0.000 0.000
#&gt; SRR1383361     3  0.6238     0.7248 0.000 0.112 0.652 0.236
#&gt; SRR1383363     3  0.3710     0.8025 0.000 0.004 0.804 0.192
#&gt; SRR1383364     3  0.0000     0.8040 0.000 0.000 1.000 0.000
#&gt; SRR1383365     3  0.3908     0.7939 0.000 0.004 0.784 0.212
#&gt; SRR1383366     4  0.2593     0.7008 0.000 0.104 0.004 0.892
#&gt; SRR1383367     3  0.7506     0.4531 0.000 0.308 0.484 0.208
#&gt; SRR1383368     1  0.1474     0.7680 0.948 0.000 0.000 0.052
#&gt; SRR1383369     3  0.1716     0.8170 0.000 0.000 0.936 0.064
#&gt; SRR1383370     2  0.4839     0.6261 0.000 0.764 0.052 0.184
#&gt; SRR1383371     3  0.0817     0.8125 0.000 0.000 0.976 0.024
#&gt; SRR1383372     2  0.6016     0.2762 0.000 0.544 0.412 0.044
#&gt; SRR1383373     3  0.5773     0.3848 0.000 0.320 0.632 0.048
#&gt; SRR1383374     2  0.2363     0.7271 0.000 0.920 0.024 0.056
#&gt; SRR1383375     1  0.3311     0.7369 0.828 0.000 0.000 0.172
#&gt; SRR1383376     2  0.1118     0.7096 0.000 0.964 0.000 0.036
#&gt; SRR1383377     4  0.1661     0.7278 0.000 0.052 0.004 0.944
#&gt; SRR1383378     2  0.4281     0.6891 0.028 0.792 0.180 0.000
#&gt; SRR1383379     4  0.3942     0.7442 0.000 0.236 0.000 0.764
#&gt; SRR1383380     4  0.4590     0.6729 0.148 0.060 0.000 0.792
#&gt; SRR1383381     3  0.0188     0.8045 0.000 0.000 0.996 0.004
#&gt; SRR1383382     1  0.0000     0.7918 1.000 0.000 0.000 0.000
#&gt; SRR1383383     2  0.4967     0.3297 0.000 0.548 0.452 0.000
#&gt; SRR1383385     1  0.4382     0.6387 0.704 0.000 0.000 0.296
#&gt; SRR1383384     2  0.0188     0.7300 0.000 0.996 0.000 0.004
#&gt; SRR1383386     1  0.0000     0.7918 1.000 0.000 0.000 0.000
#&gt; SRR1383387     2  0.4985    -0.2812 0.000 0.532 0.000 0.468
#&gt; SRR1383389     2  0.4948     0.3243 0.000 0.560 0.440 0.000
#&gt; SRR1383391     2  0.0817     0.7363 0.000 0.976 0.024 0.000
#&gt; SRR1383388     2  0.5345    -0.1778 0.012 0.560 0.000 0.428
#&gt; SRR1383392     2  0.0336     0.7285 0.000 0.992 0.000 0.008
#&gt; SRR1383390     2  0.3123     0.7171 0.000 0.844 0.156 0.000
#&gt; SRR1383394     2  0.3569     0.5013 0.000 0.804 0.000 0.196
#&gt; SRR1383393     1  0.4500     0.6163 0.684 0.000 0.000 0.316
#&gt; SRR1383396     1  0.6305     0.0717 0.480 0.040 0.472 0.008
#&gt; SRR1383395     4  0.1474     0.7301 0.000 0.052 0.000 0.948
#&gt; SRR1383399     3  0.0188     0.8045 0.000 0.000 0.996 0.004
#&gt; SRR1383400     1  0.0000     0.7918 1.000 0.000 0.000 0.000
#&gt; SRR1383397     4  0.3873     0.7485 0.000 0.228 0.000 0.772
#&gt; SRR1383401     3  0.2281     0.7655 0.000 0.096 0.904 0.000
#&gt; SRR1383398     4  0.4718     0.7064 0.116 0.092 0.000 0.792
#&gt; SRR1383402     2  0.0188     0.7300 0.000 0.996 0.000 0.004
#&gt; SRR1383404     1  0.2589     0.7228 0.884 0.116 0.000 0.000
#&gt; SRR1383403     1  0.4643     0.5715 0.656 0.000 0.000 0.344
#&gt; SRR1383405     4  0.4999     0.2933 0.000 0.492 0.000 0.508
#&gt; SRR1383406     4  0.4522     0.6591 0.000 0.320 0.000 0.680
#&gt; SRR1383407     2  0.4679     0.5058 0.000 0.648 0.352 0.000
#&gt; SRR1383408     2  0.2469     0.7314 0.000 0.892 0.108 0.000
#&gt; SRR1383409     2  0.1557     0.7386 0.000 0.944 0.056 0.000
#&gt; SRR1383410     2  0.0188     0.7300 0.000 0.996 0.000 0.004
</code></pre>

<script>
$('#tab-CV-NMF-get-classes-3-a').parent().next().next().hide();
$('#tab-CV-NMF-get-classes-3-a').click(function(){
  $('#tab-CV-NMF-get-classes-3-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-CV-NMF-get-classes-4'>
<p><a id='tab-CV-NMF-get-classes-4-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 5), get_membership(res, k = 5))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4    p5
#&gt; SRR1383358     3  0.0000      0.952 0.000 0.000 1.000 0.000 0.000
#&gt; SRR1383360     3  0.1444      0.924 0.040 0.000 0.948 0.012 0.000
#&gt; SRR1383359     3  0.0000      0.952 0.000 0.000 1.000 0.000 0.000
#&gt; SRR1383362     1  0.0000      0.833 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1383361     3  0.0290      0.950 0.000 0.000 0.992 0.008 0.000
#&gt; SRR1383363     3  0.0000      0.952 0.000 0.000 1.000 0.000 0.000
#&gt; SRR1383364     5  0.1502      0.930 0.000 0.004 0.056 0.000 0.940
#&gt; SRR1383365     3  0.0000      0.952 0.000 0.000 1.000 0.000 0.000
#&gt; SRR1383366     3  0.1341      0.920 0.000 0.000 0.944 0.056 0.000
#&gt; SRR1383367     3  0.0000      0.952 0.000 0.000 1.000 0.000 0.000
#&gt; SRR1383368     1  0.3895      0.446 0.680 0.000 0.320 0.000 0.000
#&gt; SRR1383369     5  0.3194      0.856 0.000 0.020 0.148 0.000 0.832
#&gt; SRR1383370     3  0.1043      0.933 0.000 0.000 0.960 0.040 0.000
#&gt; SRR1383371     5  0.1478      0.928 0.000 0.000 0.064 0.000 0.936
#&gt; SRR1383372     2  0.5109      0.113 0.000 0.504 0.460 0.000 0.036
#&gt; SRR1383373     3  0.3196      0.720 0.000 0.192 0.804 0.000 0.004
#&gt; SRR1383374     2  0.4171      0.331 0.000 0.604 0.396 0.000 0.000
#&gt; SRR1383375     4  0.6705     -0.136 0.364 0.000 0.000 0.392 0.244
#&gt; SRR1383376     2  0.2280      0.670 0.000 0.880 0.000 0.120 0.000
#&gt; SRR1383377     4  0.1121      0.620 0.000 0.000 0.000 0.956 0.044
#&gt; SRR1383378     2  0.1671      0.747 0.000 0.924 0.000 0.000 0.076
#&gt; SRR1383379     4  0.2020      0.638 0.000 0.100 0.000 0.900 0.000
#&gt; SRR1383380     4  0.1341      0.618 0.000 0.000 0.000 0.944 0.056
#&gt; SRR1383381     5  0.1205      0.930 0.000 0.000 0.040 0.004 0.956
#&gt; SRR1383382     1  0.0000      0.833 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1383383     2  0.4297      0.143 0.000 0.528 0.000 0.000 0.472
#&gt; SRR1383385     1  0.5352      0.185 0.536 0.000 0.000 0.408 0.056
#&gt; SRR1383384     2  0.0703      0.745 0.000 0.976 0.000 0.024 0.000
#&gt; SRR1383386     1  0.0000      0.833 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1383387     4  0.4256      0.295 0.000 0.436 0.000 0.564 0.000
#&gt; SRR1383389     2  0.4030      0.439 0.000 0.648 0.000 0.000 0.352
#&gt; SRR1383391     2  0.0404      0.755 0.000 0.988 0.000 0.000 0.012
#&gt; SRR1383388     4  0.4622      0.295 0.000 0.440 0.000 0.548 0.012
#&gt; SRR1383392     2  0.3102      0.706 0.000 0.860 0.084 0.056 0.000
#&gt; SRR1383390     2  0.1121      0.757 0.000 0.956 0.000 0.000 0.044
#&gt; SRR1383394     2  0.4045      0.220 0.000 0.644 0.000 0.356 0.000
#&gt; SRR1383393     4  0.6330      0.144 0.164 0.000 0.000 0.472 0.364
#&gt; SRR1383396     5  0.0912      0.902 0.000 0.016 0.000 0.012 0.972
#&gt; SRR1383395     4  0.0162      0.627 0.000 0.000 0.000 0.996 0.004
#&gt; SRR1383399     5  0.1205      0.930 0.000 0.000 0.040 0.004 0.956
#&gt; SRR1383400     1  0.0000      0.833 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1383397     4  0.2127      0.637 0.000 0.108 0.000 0.892 0.000
#&gt; SRR1383401     5  0.3151      0.813 0.000 0.144 0.020 0.000 0.836
#&gt; SRR1383398     4  0.1544      0.612 0.000 0.000 0.000 0.932 0.068
#&gt; SRR1383402     2  0.0703      0.745 0.000 0.976 0.000 0.024 0.000
#&gt; SRR1383404     1  0.1121      0.799 0.956 0.044 0.000 0.000 0.000
#&gt; SRR1383403     4  0.5594     -0.127 0.436 0.000 0.000 0.492 0.072
#&gt; SRR1383405     4  0.4171      0.371 0.000 0.396 0.000 0.604 0.000
#&gt; SRR1383406     4  0.3561      0.548 0.000 0.260 0.000 0.740 0.000
#&gt; SRR1383407     2  0.3932      0.481 0.000 0.672 0.000 0.000 0.328
#&gt; SRR1383408     2  0.0880      0.758 0.000 0.968 0.000 0.000 0.032
#&gt; SRR1383409     2  0.0963      0.758 0.000 0.964 0.000 0.000 0.036
#&gt; SRR1383410     2  0.1410      0.724 0.000 0.940 0.000 0.060 0.000
</code></pre>

<script>
$('#tab-CV-NMF-get-classes-4-a').parent().next().next().hide();
$('#tab-CV-NMF-get-classes-4-a').click(function(){
  $('#tab-CV-NMF-get-classes-4-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-CV-NMF-get-classes-5'>
<p><a id='tab-CV-NMF-get-classes-5-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 6), get_membership(res, k = 6))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4    p5    p6
#&gt; SRR1383358     3  0.0000      0.952 0.000 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1383360     3  0.1152      0.928 0.044 0.004 0.952 0.000 0.000 0.000
#&gt; SRR1383359     3  0.0260      0.950 0.008 0.000 0.992 0.000 0.000 0.000
#&gt; SRR1383362     6  0.0000      0.880 0.000 0.000 0.000 0.000 0.000 1.000
#&gt; SRR1383361     3  0.0000      0.952 0.000 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1383363     3  0.0291      0.951 0.000 0.004 0.992 0.000 0.004 0.000
#&gt; SRR1383364     5  0.0458      0.844 0.000 0.016 0.000 0.000 0.984 0.000
#&gt; SRR1383365     3  0.0748      0.942 0.016 0.000 0.976 0.004 0.004 0.000
#&gt; SRR1383366     3  0.0000      0.952 0.000 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1383367     3  0.0146      0.951 0.000 0.004 0.996 0.000 0.000 0.000
#&gt; SRR1383368     6  0.3468      0.610 0.000 0.004 0.284 0.000 0.000 0.712
#&gt; SRR1383369     5  0.1719      0.812 0.000 0.016 0.060 0.000 0.924 0.000
#&gt; SRR1383370     3  0.0972      0.937 0.028 0.008 0.964 0.000 0.000 0.000
#&gt; SRR1383371     5  0.0458      0.844 0.000 0.016 0.000 0.000 0.984 0.000
#&gt; SRR1383372     2  0.1411      0.862 0.000 0.936 0.060 0.000 0.004 0.000
#&gt; SRR1383373     3  0.3720      0.663 0.000 0.236 0.736 0.000 0.028 0.000
#&gt; SRR1383374     2  0.2191      0.818 0.000 0.876 0.120 0.000 0.004 0.000
#&gt; SRR1383375     1  0.3094      0.634 0.824 0.000 0.000 0.000 0.036 0.140
#&gt; SRR1383376     4  0.2100      0.708 0.000 0.112 0.000 0.884 0.004 0.000
#&gt; SRR1383377     4  0.3329      0.547 0.236 0.000 0.004 0.756 0.004 0.000
#&gt; SRR1383378     2  0.0779      0.896 0.008 0.976 0.000 0.008 0.008 0.000
#&gt; SRR1383379     4  0.0458      0.729 0.016 0.000 0.000 0.984 0.000 0.000
#&gt; SRR1383380     1  0.3482      0.513 0.684 0.000 0.000 0.316 0.000 0.000
#&gt; SRR1383381     5  0.1049      0.841 0.032 0.008 0.000 0.000 0.960 0.000
#&gt; SRR1383382     6  0.0000      0.880 0.000 0.000 0.000 0.000 0.000 1.000
#&gt; SRR1383383     5  0.5432      0.393 0.044 0.344 0.000 0.048 0.564 0.000
#&gt; SRR1383385     1  0.3364      0.609 0.780 0.000 0.000 0.024 0.000 0.196
#&gt; SRR1383384     2  0.3337      0.645 0.000 0.736 0.000 0.260 0.004 0.000
#&gt; SRR1383386     6  0.0837      0.872 0.020 0.004 0.000 0.004 0.000 0.972
#&gt; SRR1383387     4  0.1049      0.738 0.008 0.032 0.000 0.960 0.000 0.000
#&gt; SRR1383389     2  0.0508      0.891 0.004 0.984 0.000 0.000 0.012 0.000
#&gt; SRR1383391     2  0.0547      0.899 0.000 0.980 0.000 0.020 0.000 0.000
#&gt; SRR1383388     1  0.5134      0.275 0.524 0.088 0.000 0.388 0.000 0.000
#&gt; SRR1383392     4  0.6216      0.151 0.020 0.340 0.160 0.476 0.004 0.000
#&gt; SRR1383390     2  0.0458      0.900 0.000 0.984 0.000 0.016 0.000 0.000
#&gt; SRR1383394     4  0.1411      0.734 0.000 0.060 0.000 0.936 0.004 0.000
#&gt; SRR1383393     1  0.2202      0.673 0.908 0.000 0.000 0.012 0.052 0.028
#&gt; SRR1383396     1  0.4565      0.450 0.664 0.076 0.000 0.000 0.260 0.000
#&gt; SRR1383395     4  0.2491      0.646 0.164 0.000 0.000 0.836 0.000 0.000
#&gt; SRR1383399     5  0.1049      0.841 0.032 0.008 0.000 0.000 0.960 0.000
#&gt; SRR1383400     6  0.0000      0.880 0.000 0.000 0.000 0.000 0.000 1.000
#&gt; SRR1383397     4  0.0632      0.726 0.024 0.000 0.000 0.976 0.000 0.000
#&gt; SRR1383401     5  0.4214      0.737 0.052 0.124 0.000 0.048 0.776 0.000
#&gt; SRR1383398     1  0.3756      0.379 0.600 0.000 0.000 0.400 0.000 0.000
#&gt; SRR1383402     2  0.3584      0.556 0.000 0.688 0.000 0.308 0.004 0.000
#&gt; SRR1383404     6  0.3912      0.739 0.108 0.024 0.000 0.072 0.000 0.796
#&gt; SRR1383403     1  0.3134      0.652 0.820 0.000 0.000 0.036 0.000 0.144
#&gt; SRR1383405     4  0.0632      0.738 0.000 0.024 0.000 0.976 0.000 0.000
#&gt; SRR1383406     4  0.4251      0.235 0.348 0.028 0.000 0.624 0.000 0.000
#&gt; SRR1383407     2  0.0632      0.887 0.000 0.976 0.000 0.000 0.024 0.000
#&gt; SRR1383408     2  0.0458      0.900 0.000 0.984 0.000 0.016 0.000 0.000
#&gt; SRR1383409     2  0.0508      0.899 0.000 0.984 0.000 0.012 0.004 0.000
#&gt; SRR1383410     4  0.4165      0.151 0.008 0.420 0.000 0.568 0.004 0.000
</code></pre>

<script>
$('#tab-CV-NMF-get-classes-5-a').parent().next().next().hide();
$('#tab-CV-NMF-get-classes-5-a').click(function(){
  $('#tab-CV-NMF-get-classes-5-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>
</div>

Heatmaps for the consensus matrix. It visualizes the probability of two
samples to be in a same group.



<script>
$( function() {
	$( '#tabs-CV-NMF-consensus-heatmap' ).tabs();
} );
</script>
<div id='tabs-CV-NMF-consensus-heatmap'>
<ul>
<li><a href='#tab-CV-NMF-consensus-heatmap-1'>k = 2</a></li>
<li><a href='#tab-CV-NMF-consensus-heatmap-2'>k = 3</a></li>
<li><a href='#tab-CV-NMF-consensus-heatmap-3'>k = 4</a></li>
<li><a href='#tab-CV-NMF-consensus-heatmap-4'>k = 5</a></li>
<li><a href='#tab-CV-NMF-consensus-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-CV-NMF-consensus-heatmap-1'>
<pre><code class="r">consensus_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-CV-NMF-consensus-heatmap-1-1.png" alt="plot of chunk tab-CV-NMF-consensus-heatmap-1"/></p>

</div>
<div id='tab-CV-NMF-consensus-heatmap-2'>
<pre><code class="r">consensus_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-CV-NMF-consensus-heatmap-2-1.png" alt="plot of chunk tab-CV-NMF-consensus-heatmap-2"/></p>

</div>
<div id='tab-CV-NMF-consensus-heatmap-3'>
<pre><code class="r">consensus_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-CV-NMF-consensus-heatmap-3-1.png" alt="plot of chunk tab-CV-NMF-consensus-heatmap-3"/></p>

</div>
<div id='tab-CV-NMF-consensus-heatmap-4'>
<pre><code class="r">consensus_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-CV-NMF-consensus-heatmap-4-1.png" alt="plot of chunk tab-CV-NMF-consensus-heatmap-4"/></p>

</div>
<div id='tab-CV-NMF-consensus-heatmap-5'>
<pre><code class="r">consensus_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-CV-NMF-consensus-heatmap-5-1.png" alt="plot of chunk tab-CV-NMF-consensus-heatmap-5"/></p>

</div>
</div>

Heatmaps for the membership of samples in all partitions to see how consistent they are:




<script>
$( function() {
	$( '#tabs-CV-NMF-membership-heatmap' ).tabs();
} );
</script>
<div id='tabs-CV-NMF-membership-heatmap'>
<ul>
<li><a href='#tab-CV-NMF-membership-heatmap-1'>k = 2</a></li>
<li><a href='#tab-CV-NMF-membership-heatmap-2'>k = 3</a></li>
<li><a href='#tab-CV-NMF-membership-heatmap-3'>k = 4</a></li>
<li><a href='#tab-CV-NMF-membership-heatmap-4'>k = 5</a></li>
<li><a href='#tab-CV-NMF-membership-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-CV-NMF-membership-heatmap-1'>
<pre><code class="r">membership_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-CV-NMF-membership-heatmap-1-1.png" alt="plot of chunk tab-CV-NMF-membership-heatmap-1"/></p>

</div>
<div id='tab-CV-NMF-membership-heatmap-2'>
<pre><code class="r">membership_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-CV-NMF-membership-heatmap-2-1.png" alt="plot of chunk tab-CV-NMF-membership-heatmap-2"/></p>

</div>
<div id='tab-CV-NMF-membership-heatmap-3'>
<pre><code class="r">membership_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-CV-NMF-membership-heatmap-3-1.png" alt="plot of chunk tab-CV-NMF-membership-heatmap-3"/></p>

</div>
<div id='tab-CV-NMF-membership-heatmap-4'>
<pre><code class="r">membership_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-CV-NMF-membership-heatmap-4-1.png" alt="plot of chunk tab-CV-NMF-membership-heatmap-4"/></p>

</div>
<div id='tab-CV-NMF-membership-heatmap-5'>
<pre><code class="r">membership_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-CV-NMF-membership-heatmap-5-1.png" alt="plot of chunk tab-CV-NMF-membership-heatmap-5"/></p>

</div>
</div>

As soon as we have had the classes for columns, we can look for signatures
which are significantly different between classes which can be candidate marks
for certain classes. Following are the heatmaps for signatures.



Signature heatmaps where rows are scaled:



<script>
$( function() {
	$( '#tabs-CV-NMF-get-signatures' ).tabs();
} );
</script>
<div id='tabs-CV-NMF-get-signatures'>
<ul>
<li><a href='#tab-CV-NMF-get-signatures-1'>k = 2</a></li>
<li><a href='#tab-CV-NMF-get-signatures-2'>k = 3</a></li>
<li><a href='#tab-CV-NMF-get-signatures-3'>k = 4</a></li>
<li><a href='#tab-CV-NMF-get-signatures-4'>k = 5</a></li>
<li><a href='#tab-CV-NMF-get-signatures-5'>k = 6</a></li>
</ul>
<div id='tab-CV-NMF-get-signatures-1'>
<pre><code class="r">get_signatures(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-CV-NMF-get-signatures-1-1.png" alt="plot of chunk tab-CV-NMF-get-signatures-1"/></p>

</div>
<div id='tab-CV-NMF-get-signatures-2'>
<pre><code class="r">get_signatures(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-CV-NMF-get-signatures-2-1.png" alt="plot of chunk tab-CV-NMF-get-signatures-2"/></p>

</div>
<div id='tab-CV-NMF-get-signatures-3'>
<pre><code class="r">get_signatures(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-CV-NMF-get-signatures-3-1.png" alt="plot of chunk tab-CV-NMF-get-signatures-3"/></p>

</div>
<div id='tab-CV-NMF-get-signatures-4'>
<pre><code class="r">get_signatures(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-CV-NMF-get-signatures-4-1.png" alt="plot of chunk tab-CV-NMF-get-signatures-4"/></p>

</div>
<div id='tab-CV-NMF-get-signatures-5'>
<pre><code class="r">get_signatures(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-CV-NMF-get-signatures-5-1.png" alt="plot of chunk tab-CV-NMF-get-signatures-5"/></p>

</div>
</div>



Signature heatmaps where rows are not scaled:


<script>
$( function() {
	$( '#tabs-CV-NMF-get-signatures-no-scale' ).tabs();
} );
</script>
<div id='tabs-CV-NMF-get-signatures-no-scale'>
<ul>
<li><a href='#tab-CV-NMF-get-signatures-no-scale-1'>k = 2</a></li>
<li><a href='#tab-CV-NMF-get-signatures-no-scale-2'>k = 3</a></li>
<li><a href='#tab-CV-NMF-get-signatures-no-scale-3'>k = 4</a></li>
<li><a href='#tab-CV-NMF-get-signatures-no-scale-4'>k = 5</a></li>
<li><a href='#tab-CV-NMF-get-signatures-no-scale-5'>k = 6</a></li>
</ul>
<div id='tab-CV-NMF-get-signatures-no-scale-1'>
<pre><code class="r">get_signatures(res, k = 2, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-CV-NMF-get-signatures-no-scale-1-1.png" alt="plot of chunk tab-CV-NMF-get-signatures-no-scale-1"/></p>

</div>
<div id='tab-CV-NMF-get-signatures-no-scale-2'>
<pre><code class="r">get_signatures(res, k = 3, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-CV-NMF-get-signatures-no-scale-2-1.png" alt="plot of chunk tab-CV-NMF-get-signatures-no-scale-2"/></p>

</div>
<div id='tab-CV-NMF-get-signatures-no-scale-3'>
<pre><code class="r">get_signatures(res, k = 4, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-CV-NMF-get-signatures-no-scale-3-1.png" alt="plot of chunk tab-CV-NMF-get-signatures-no-scale-3"/></p>

</div>
<div id='tab-CV-NMF-get-signatures-no-scale-4'>
<pre><code class="r">get_signatures(res, k = 5, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-CV-NMF-get-signatures-no-scale-4-1.png" alt="plot of chunk tab-CV-NMF-get-signatures-no-scale-4"/></p>

</div>
<div id='tab-CV-NMF-get-signatures-no-scale-5'>
<pre><code class="r">get_signatures(res, k = 6, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-CV-NMF-get-signatures-no-scale-5-1.png" alt="plot of chunk tab-CV-NMF-get-signatures-no-scale-5"/></p>

</div>
</div>



Compare the overlap of signatures from different k:

```r
compare_signatures(res)
```

![plot of chunk CV-NMF-signature_compare](figure_cola/CV-NMF-signature_compare-1.png)

`get_signature()` returns a data frame invisibly. TO get the list of signatures, the function
call should be assigned to a variable explicitly. In following code, if `plot` argument is set
to `FALSE`, no heatmap is plotted while only the differential analysis is performed.

```r
# code only for demonstration
tb = get_signature(res, k = ..., plot = FALSE)
```

An example of the output of `tb` is:

```
#>   which_row         fdr    mean_1    mean_2 scaled_mean_1 scaled_mean_2 km
#> 1        38 0.042760348  8.373488  9.131774    -0.5533452     0.5164555  1
#> 2        40 0.018707592  7.106213  8.469186    -0.6173731     0.5762149  1
#> 3        55 0.019134737 10.221463 11.207825    -0.6159697     0.5749050  1
#> 4        59 0.006059896  5.921854  7.869574    -0.6899429     0.6439467  1
#> 5        60 0.018055526  8.928898 10.211722    -0.6204761     0.5791110  1
#> 6        98 0.009384629 15.714769 14.887706     0.6635654    -0.6193277  2
...
```

The columns in `tb` are:

1. `which_row`: row indices corresponding to the input matrix.
2. `fdr`: FDR for the differential test. 
3. `mean_x`: The mean value in group x.
4. `scaled_mean_x`: The mean value in group x after rows are scaled.
5. `km`: Row groups if k-means clustering is applied to rows.



UMAP plot which shows how samples are separated.


<script>
$( function() {
	$( '#tabs-CV-NMF-dimension-reduction' ).tabs();
} );
</script>
<div id='tabs-CV-NMF-dimension-reduction'>
<ul>
<li><a href='#tab-CV-NMF-dimension-reduction-1'>k = 2</a></li>
<li><a href='#tab-CV-NMF-dimension-reduction-2'>k = 3</a></li>
<li><a href='#tab-CV-NMF-dimension-reduction-3'>k = 4</a></li>
<li><a href='#tab-CV-NMF-dimension-reduction-4'>k = 5</a></li>
<li><a href='#tab-CV-NMF-dimension-reduction-5'>k = 6</a></li>
</ul>
<div id='tab-CV-NMF-dimension-reduction-1'>
<pre><code class="r">dimension_reduction(res, k = 2, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-CV-NMF-dimension-reduction-1-1.png" alt="plot of chunk tab-CV-NMF-dimension-reduction-1"/></p>

</div>
<div id='tab-CV-NMF-dimension-reduction-2'>
<pre><code class="r">dimension_reduction(res, k = 3, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-CV-NMF-dimension-reduction-2-1.png" alt="plot of chunk tab-CV-NMF-dimension-reduction-2"/></p>

</div>
<div id='tab-CV-NMF-dimension-reduction-3'>
<pre><code class="r">dimension_reduction(res, k = 4, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-CV-NMF-dimension-reduction-3-1.png" alt="plot of chunk tab-CV-NMF-dimension-reduction-3"/></p>

</div>
<div id='tab-CV-NMF-dimension-reduction-4'>
<pre><code class="r">dimension_reduction(res, k = 5, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-CV-NMF-dimension-reduction-4-1.png" alt="plot of chunk tab-CV-NMF-dimension-reduction-4"/></p>

</div>
<div id='tab-CV-NMF-dimension-reduction-5'>
<pre><code class="r">dimension_reduction(res, k = 6, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-CV-NMF-dimension-reduction-5-1.png" alt="plot of chunk tab-CV-NMF-dimension-reduction-5"/></p>

</div>
</div>


Following heatmap shows how subgroups are split when increasing `k`:

```r
collect_classes(res)
```

![plot of chunk CV-NMF-collect-classes](figure_cola/CV-NMF-collect-classes-1.png)


If matrix rows can be associated to genes, consider to use `functional_enrichment(res,
...)` to perform function enrichment for the signature genes. See [this vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/functional_enrichment.html) for more detailed explanations.


 

---------------------------------------------------




### MAD:hclust**






The object with results only for a single top-value method and a single partition method 
can be extracted as:

```r
res = res_list["MAD", "hclust"]
# you can also extract it by
# res = res_list["MAD:hclust"]
```

A summary of `res` and all the functions that can be applied to it:

```r
res
```

```
#> A 'ConsensusPartition' object with k = 2, 3, 4, 5, 6.
#>   On a matrix with 15680 rows and 53 columns.
#>   Top rows (1000, 2000, 3000, 4000, 5000) are extracted by 'MAD' method.
#>   Subgroups are detected by 'hclust' method.
#>   Performed in total 1250 partitions by row resampling.
#>   Best k for subgroups seems to be 2.
#> 
#> Following methods can be applied to this 'ConsensusPartition' object:
#>  [1] "cola_report"             "collect_classes"         "collect_plots"          
#>  [4] "collect_stats"           "colnames"                "compare_signatures"     
#>  [7] "consensus_heatmap"       "dimension_reduction"     "functional_enrichment"  
#> [10] "get_anno_col"            "get_anno"                "get_classes"            
#> [13] "get_consensus"           "get_matrix"              "get_membership"         
#> [16] "get_param"               "get_signatures"          "get_stats"              
#> [19] "is_best_k"               "is_stable_k"             "membership_heatmap"     
#> [22] "ncol"                    "nrow"                    "plot_ecdf"              
#> [25] "rownames"                "select_partition_number" "show"                   
#> [28] "suggest_best_k"          "test_to_known_factors"
```

`collect_plots()` function collects all the plots made from `res` for all `k` (number of partitions)
into one single page to provide an easy and fast comparison between different `k`.

```r
collect_plots(res)
```

![plot of chunk MAD-hclust-collect-plots](figure_cola/MAD-hclust-collect-plots-1.png)

The plots are:

- The first row: a plot of the ECDF (empirical cumulative distribution
  function) curves of the consensus matrix for each `k` and the heatmap of
  predicted classes for each `k`.
- The second row: heatmaps of the consensus matrix for each `k`.
- The third row: heatmaps of the membership matrix for each `k`.
- The fouth row: heatmaps of the signatures for each `k`.

All the plots in panels can be made by individual functions and they are
plotted later in this section.

`select_partition_number()` produces several plots showing different
statistics for choosing "optimized" `k`. There are following statistics:

- ECDF curves of the consensus matrix for each `k`;
- 1-PAC. [The PAC
  score](https://en.wikipedia.org/wiki/Consensus_clustering#Over-interpretation_potential_of_consensus_clustering)
  measures the proportion of the ambiguous subgrouping.
- Mean silhouette score.
- Concordance. The mean probability of fiting the consensus class ids in all
  partitions.
- Area increased. Denote $A_k$ as the area under the ECDF curve for current
  `k`, the area increased is defined as $A_k - A_{k-1}$.
- Rand index. The percent of pairs of samples that are both in a same cluster
  or both are not in a same cluster in the partition of k and k-1.
- Jaccard index. The ratio of pairs of samples are both in a same cluster in
  the partition of k and k-1 and the pairs of samples are both in a same
  cluster in the partition k or k-1.

The detailed explanations of these statistics can be found in [the _cola_
vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/cola.html#toc_13).

Generally speaking, lower PAC score, higher mean silhouette score or higher
concordance corresponds to better partition. Rand index and Jaccard index
measure how similar the current partition is compared to partition with `k-1`.
If they are too similar, we won't accept `k` is better than `k-1`.

```r
select_partition_number(res)
```

![plot of chunk MAD-hclust-select-partition-number](figure_cola/MAD-hclust-select-partition-number-1.png)

The numeric values for all these statistics can be obtained by `get_stats()`.

```r
get_stats(res)
```

```
#>   k 1-PAC mean_silhouette concordance area_increased  Rand Jaccard
#> 2 2 0.960           0.955       0.979         0.2623 0.766   0.766
#> 3 3 0.477           0.635       0.851         0.8924 0.826   0.773
#> 4 4 0.487           0.673       0.789         0.2840 0.710   0.526
#> 5 5 0.539           0.516       0.771         0.0778 0.982   0.947
#> 6 6 0.542           0.538       0.721         0.0579 0.940   0.820
```

`suggest_best_k()` suggests the best $k$ based on these statistics. The rules are as follows:

- All $k$ with Jaccard index larger than 0.95 are removed because increasing
  $k$ does not provide enough extra information. If all $k$ are removed, it is
  marked as no subgroup is detected.
- For all $k$ with 1-PAC score larger than 0.9, the maximal $k$ is taken as
  the best $k$, and other $k$ are marked as optional $k$.
- If it does not fit the second rule. The $k$ with the maximal vote of the
  highest 1-PAC score, highest mean silhouette, and highest concordance is
  taken as the best $k$.

```r
suggest_best_k(res)
```

```
#> [1] 2
```


Following shows the table of the partitions (You need to click the **show/hide
code output** link to see it). The membership matrix (columns with name `p*`)
is inferred by
[`clue::cl_consensus()`](https://www.rdocumentation.org/link/cl_consensus?package=clue)
function with the `SE` method. Basically the value in the membership matrix
represents the probability to belong to a certain group. The finall class
label for an item is determined with the group with highest probability it
belongs to.

In `get_classes()` function, the entropy is calculated from the membership
matrix and the silhouette score is calculated from the consensus matrix.



<script>
$( function() {
	$( '#tabs-MAD-hclust-get-classes' ).tabs();
} );
</script>
<div id='tabs-MAD-hclust-get-classes'>
<ul>
<li><a href='#tab-MAD-hclust-get-classes-1'>k = 2</a></li>
<li><a href='#tab-MAD-hclust-get-classes-2'>k = 3</a></li>
<li><a href='#tab-MAD-hclust-get-classes-3'>k = 4</a></li>
<li><a href='#tab-MAD-hclust-get-classes-4'>k = 5</a></li>
<li><a href='#tab-MAD-hclust-get-classes-5'>k = 6</a></li>
</ul>

<div id='tab-MAD-hclust-get-classes-1'>
<p><a id='tab-MAD-hclust-get-classes-1-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 2), get_membership(res, k = 2))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2
#&gt; SRR1383358     2  0.0000      0.975 0.000 1.000
#&gt; SRR1383360     2  0.6438      0.812 0.164 0.836
#&gt; SRR1383359     2  0.0000      0.975 0.000 1.000
#&gt; SRR1383362     1  0.0000      1.000 1.000 0.000
#&gt; SRR1383361     2  0.0000      0.975 0.000 1.000
#&gt; SRR1383363     2  0.0000      0.975 0.000 1.000
#&gt; SRR1383364     2  0.0376      0.973 0.004 0.996
#&gt; SRR1383365     2  0.0000      0.975 0.000 1.000
#&gt; SRR1383366     2  0.0000      0.975 0.000 1.000
#&gt; SRR1383367     2  0.0000      0.975 0.000 1.000
#&gt; SRR1383368     2  0.8555      0.646 0.280 0.720
#&gt; SRR1383369     2  0.0000      0.975 0.000 1.000
#&gt; SRR1383370     2  0.0000      0.975 0.000 1.000
#&gt; SRR1383371     2  0.0376      0.973 0.004 0.996
#&gt; SRR1383372     2  0.0000      0.975 0.000 1.000
#&gt; SRR1383373     2  0.0000      0.975 0.000 1.000
#&gt; SRR1383374     2  0.0000      0.975 0.000 1.000
#&gt; SRR1383375     1  0.0000      1.000 1.000 0.000
#&gt; SRR1383376     2  0.0000      0.975 0.000 1.000
#&gt; SRR1383377     2  0.0000      0.975 0.000 1.000
#&gt; SRR1383378     2  0.1843      0.954 0.028 0.972
#&gt; SRR1383379     2  0.0000      0.975 0.000 1.000
#&gt; SRR1383380     2  0.0938      0.968 0.012 0.988
#&gt; SRR1383381     2  0.0000      0.975 0.000 1.000
#&gt; SRR1383382     1  0.0000      1.000 1.000 0.000
#&gt; SRR1383383     2  0.0000      0.975 0.000 1.000
#&gt; SRR1383385     1  0.0000      1.000 1.000 0.000
#&gt; SRR1383384     2  0.0000      0.975 0.000 1.000
#&gt; SRR1383386     2  0.8555      0.646 0.280 0.720
#&gt; SRR1383387     2  0.0000      0.975 0.000 1.000
#&gt; SRR1383389     2  0.0376      0.973 0.004 0.996
#&gt; SRR1383391     2  0.0000      0.975 0.000 1.000
#&gt; SRR1383388     2  0.0938      0.968 0.012 0.988
#&gt; SRR1383392     2  0.0000      0.975 0.000 1.000
#&gt; SRR1383390     2  0.0000      0.975 0.000 1.000
#&gt; SRR1383394     2  0.0000      0.975 0.000 1.000
#&gt; SRR1383393     1  0.0000      1.000 1.000 0.000
#&gt; SRR1383396     2  0.1843      0.954 0.028 0.972
#&gt; SRR1383395     2  0.0000      0.975 0.000 1.000
#&gt; SRR1383399     2  0.0000      0.975 0.000 1.000
#&gt; SRR1383400     1  0.0000      1.000 1.000 0.000
#&gt; SRR1383397     2  0.0000      0.975 0.000 1.000
#&gt; SRR1383401     2  0.0000      0.975 0.000 1.000
#&gt; SRR1383398     2  0.0938      0.968 0.012 0.988
#&gt; SRR1383402     2  0.0000      0.975 0.000 1.000
#&gt; SRR1383404     2  0.8555      0.646 0.280 0.720
#&gt; SRR1383403     1  0.0000      1.000 1.000 0.000
#&gt; SRR1383405     2  0.0000      0.975 0.000 1.000
#&gt; SRR1383406     2  0.0938      0.968 0.012 0.988
#&gt; SRR1383407     2  0.0376      0.973 0.004 0.996
#&gt; SRR1383408     2  0.0000      0.975 0.000 1.000
#&gt; SRR1383409     2  0.0000      0.975 0.000 1.000
#&gt; SRR1383410     2  0.0000      0.975 0.000 1.000
</code></pre>

<script>
$('#tab-MAD-hclust-get-classes-1-a').parent().next().next().hide();
$('#tab-MAD-hclust-get-classes-1-a').click(function(){
  $('#tab-MAD-hclust-get-classes-1-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-MAD-hclust-get-classes-2'>
<p><a id='tab-MAD-hclust-get-classes-2-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 3), get_membership(res, k = 3))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3
#&gt; SRR1383358     2  0.6308     0.0668 0.000 0.508 0.492
#&gt; SRR1383360     2  0.5298     0.6466 0.164 0.804 0.032
#&gt; SRR1383359     3  0.3267     0.7710 0.000 0.116 0.884
#&gt; SRR1383362     1  0.0000     1.0000 1.000 0.000 0.000
#&gt; SRR1383361     2  0.6308     0.0668 0.000 0.508 0.492
#&gt; SRR1383363     2  0.6308     0.0668 0.000 0.508 0.492
#&gt; SRR1383364     3  0.0424     0.7157 0.000 0.008 0.992
#&gt; SRR1383365     2  0.6308     0.0668 0.000 0.508 0.492
#&gt; SRR1383366     2  0.6308     0.0668 0.000 0.508 0.492
#&gt; SRR1383367     2  0.6308     0.0668 0.000 0.508 0.492
#&gt; SRR1383368     2  0.5797     0.5142 0.280 0.712 0.008
#&gt; SRR1383369     3  0.4931     0.7194 0.000 0.232 0.768
#&gt; SRR1383370     2  0.6308     0.0668 0.000 0.508 0.492
#&gt; SRR1383371     3  0.0424     0.7157 0.000 0.008 0.992
#&gt; SRR1383372     2  0.6308     0.0668 0.000 0.508 0.492
#&gt; SRR1383373     2  0.6308     0.0668 0.000 0.508 0.492
#&gt; SRR1383374     2  0.6299     0.1121 0.000 0.524 0.476
#&gt; SRR1383375     1  0.0000     1.0000 1.000 0.000 0.000
#&gt; SRR1383376     2  0.0592     0.7632 0.000 0.988 0.012
#&gt; SRR1383377     2  0.4002     0.6704 0.000 0.840 0.160
#&gt; SRR1383378     2  0.1163     0.7577 0.028 0.972 0.000
#&gt; SRR1383379     2  0.0424     0.7601 0.000 0.992 0.008
#&gt; SRR1383380     2  0.1015     0.7558 0.012 0.980 0.008
#&gt; SRR1383381     3  0.5327     0.7115 0.000 0.272 0.728
#&gt; SRR1383382     1  0.0000     1.0000 1.000 0.000 0.000
#&gt; SRR1383383     2  0.0747     0.7618 0.000 0.984 0.016
#&gt; SRR1383385     1  0.0000     1.0000 1.000 0.000 0.000
#&gt; SRR1383384     2  0.0000     0.7617 0.000 1.000 0.000
#&gt; SRR1383386     2  0.5797     0.5142 0.280 0.712 0.008
#&gt; SRR1383387     2  0.0424     0.7601 0.000 0.992 0.008
#&gt; SRR1383389     2  0.1765     0.7553 0.004 0.956 0.040
#&gt; SRR1383391     2  0.0592     0.7632 0.000 0.988 0.012
#&gt; SRR1383388     2  0.1015     0.7558 0.012 0.980 0.008
#&gt; SRR1383392     2  0.4002     0.6704 0.000 0.840 0.160
#&gt; SRR1383390     2  0.0592     0.7632 0.000 0.988 0.012
#&gt; SRR1383394     2  0.0592     0.7632 0.000 0.988 0.012
#&gt; SRR1383393     1  0.0000     1.0000 1.000 0.000 0.000
#&gt; SRR1383396     2  0.1163     0.7577 0.028 0.972 0.000
#&gt; SRR1383395     2  0.4002     0.6704 0.000 0.840 0.160
#&gt; SRR1383399     3  0.5327     0.7115 0.000 0.272 0.728
#&gt; SRR1383400     1  0.0000     1.0000 1.000 0.000 0.000
#&gt; SRR1383397     2  0.0424     0.7601 0.000 0.992 0.008
#&gt; SRR1383401     2  0.0747     0.7618 0.000 0.984 0.016
#&gt; SRR1383398     2  0.1015     0.7558 0.012 0.980 0.008
#&gt; SRR1383402     2  0.0000     0.7617 0.000 1.000 0.000
#&gt; SRR1383404     2  0.5797     0.5142 0.280 0.712 0.008
#&gt; SRR1383403     1  0.0000     1.0000 1.000 0.000 0.000
#&gt; SRR1383405     2  0.0424     0.7601 0.000 0.992 0.008
#&gt; SRR1383406     2  0.1015     0.7558 0.012 0.980 0.008
#&gt; SRR1383407     2  0.1765     0.7553 0.004 0.956 0.040
#&gt; SRR1383408     2  0.0592     0.7632 0.000 0.988 0.012
#&gt; SRR1383409     2  0.0592     0.7632 0.000 0.988 0.012
#&gt; SRR1383410     2  0.4002     0.6704 0.000 0.840 0.160
</code></pre>

<script>
$('#tab-MAD-hclust-get-classes-2-a').parent().next().next().hide();
$('#tab-MAD-hclust-get-classes-2-a').click(function(){
  $('#tab-MAD-hclust-get-classes-2-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-MAD-hclust-get-classes-3'>
<p><a id='tab-MAD-hclust-get-classes-3-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 4), get_membership(res, k = 4))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4
#&gt; SRR1383358     3  0.2530     0.7113 0.000 0.112 0.888 0.000
#&gt; SRR1383360     2  0.9234     0.0309 0.160 0.428 0.280 0.132
#&gt; SRR1383359     3  0.5147    -0.4308 0.000 0.004 0.536 0.460
#&gt; SRR1383362     1  0.0592     0.9894 0.984 0.000 0.016 0.000
#&gt; SRR1383361     3  0.2530     0.7113 0.000 0.112 0.888 0.000
#&gt; SRR1383363     3  0.2530     0.7113 0.000 0.112 0.888 0.000
#&gt; SRR1383364     4  0.3074     0.7294 0.000 0.000 0.152 0.848
#&gt; SRR1383365     3  0.2530     0.7113 0.000 0.112 0.888 0.000
#&gt; SRR1383366     3  0.2530     0.7113 0.000 0.112 0.888 0.000
#&gt; SRR1383367     3  0.2530     0.7113 0.000 0.112 0.888 0.000
#&gt; SRR1383368     2  0.6987     0.4255 0.276 0.580 0.140 0.004
#&gt; SRR1383369     3  0.4950     0.0504 0.000 0.004 0.620 0.376
#&gt; SRR1383370     3  0.2530     0.7113 0.000 0.112 0.888 0.000
#&gt; SRR1383371     4  0.3074     0.7294 0.000 0.000 0.152 0.848
#&gt; SRR1383372     3  0.2530     0.7113 0.000 0.112 0.888 0.000
#&gt; SRR1383373     3  0.2530     0.7113 0.000 0.112 0.888 0.000
#&gt; SRR1383374     3  0.3024     0.6861 0.000 0.148 0.852 0.000
#&gt; SRR1383375     1  0.0000     0.9921 1.000 0.000 0.000 0.000
#&gt; SRR1383376     2  0.1474     0.8339 0.000 0.948 0.052 0.000
#&gt; SRR1383377     3  0.7119     0.2374 0.000 0.428 0.444 0.128
#&gt; SRR1383378     2  0.2773     0.8116 0.028 0.900 0.072 0.000
#&gt; SRR1383379     2  0.0000     0.8328 0.000 1.000 0.000 0.000
#&gt; SRR1383380     2  0.0469     0.8276 0.012 0.988 0.000 0.000
#&gt; SRR1383381     4  0.7028     0.6900 0.000 0.228 0.196 0.576
#&gt; SRR1383382     1  0.0592     0.9894 0.984 0.000 0.016 0.000
#&gt; SRR1383383     2  0.1637     0.8272 0.000 0.940 0.060 0.000
#&gt; SRR1383385     1  0.0000     0.9921 1.000 0.000 0.000 0.000
#&gt; SRR1383384     2  0.1118     0.8347 0.000 0.964 0.036 0.000
#&gt; SRR1383386     2  0.6987     0.4255 0.276 0.580 0.140 0.004
#&gt; SRR1383387     2  0.0000     0.8328 0.000 1.000 0.000 0.000
#&gt; SRR1383389     2  0.6966     0.1562 0.000 0.540 0.328 0.132
#&gt; SRR1383391     2  0.1474     0.8339 0.000 0.948 0.052 0.000
#&gt; SRR1383388     2  0.0469     0.8276 0.012 0.988 0.000 0.000
#&gt; SRR1383392     3  0.7119     0.2374 0.000 0.428 0.444 0.128
#&gt; SRR1383390     2  0.1474     0.8339 0.000 0.948 0.052 0.000
#&gt; SRR1383394     2  0.1474     0.8339 0.000 0.948 0.052 0.000
#&gt; SRR1383393     1  0.0000     0.9921 1.000 0.000 0.000 0.000
#&gt; SRR1383396     2  0.2773     0.8116 0.028 0.900 0.072 0.000
#&gt; SRR1383395     3  0.7119     0.2374 0.000 0.428 0.444 0.128
#&gt; SRR1383399     4  0.7028     0.6900 0.000 0.228 0.196 0.576
#&gt; SRR1383400     1  0.0592     0.9894 0.984 0.000 0.016 0.000
#&gt; SRR1383397     2  0.0000     0.8328 0.000 1.000 0.000 0.000
#&gt; SRR1383401     2  0.1637     0.8272 0.000 0.940 0.060 0.000
#&gt; SRR1383398     2  0.0469     0.8276 0.012 0.988 0.000 0.000
#&gt; SRR1383402     2  0.1118     0.8347 0.000 0.964 0.036 0.000
#&gt; SRR1383404     2  0.6987     0.4255 0.276 0.580 0.140 0.004
#&gt; SRR1383403     1  0.0000     0.9921 1.000 0.000 0.000 0.000
#&gt; SRR1383405     2  0.0000     0.8328 0.000 1.000 0.000 0.000
#&gt; SRR1383406     2  0.0469     0.8276 0.012 0.988 0.000 0.000
#&gt; SRR1383407     2  0.6966     0.1562 0.000 0.540 0.328 0.132
#&gt; SRR1383408     2  0.1474     0.8339 0.000 0.948 0.052 0.000
#&gt; SRR1383409     2  0.1474     0.8339 0.000 0.948 0.052 0.000
#&gt; SRR1383410     3  0.7119     0.2374 0.000 0.428 0.444 0.128
</code></pre>

<script>
$('#tab-MAD-hclust-get-classes-3-a').parent().next().next().hide();
$('#tab-MAD-hclust-get-classes-3-a').click(function(){
  $('#tab-MAD-hclust-get-classes-3-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-MAD-hclust-get-classes-4'>
<p><a id='tab-MAD-hclust-get-classes-4-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 5), get_membership(res, k = 5))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4    p5
#&gt; SRR1383358     3   0.167   0.680769 0.000 0.076 0.924 0.000 0.000
#&gt; SRR1383360     4   0.731   0.000000 0.052 0.204 0.256 0.488 0.000
#&gt; SRR1383359     3   0.572  -0.048688 0.000 0.000 0.520 0.392 0.088
#&gt; SRR1383362     1   0.314   0.881551 0.796 0.000 0.000 0.204 0.000
#&gt; SRR1383361     3   0.167   0.680769 0.000 0.076 0.924 0.000 0.000
#&gt; SRR1383363     3   0.167   0.680769 0.000 0.076 0.924 0.000 0.000
#&gt; SRR1383364     5   0.051   0.710649 0.000 0.000 0.016 0.000 0.984
#&gt; SRR1383365     3   0.167   0.680769 0.000 0.076 0.924 0.000 0.000
#&gt; SRR1383366     3   0.179   0.670326 0.000 0.084 0.916 0.000 0.000
#&gt; SRR1383367     3   0.167   0.680769 0.000 0.076 0.924 0.000 0.000
#&gt; SRR1383368     2   0.808  -0.471720 0.168 0.368 0.132 0.332 0.000
#&gt; SRR1383369     3   0.411   0.243100 0.000 0.000 0.624 0.000 0.376
#&gt; SRR1383370     3   0.167   0.680769 0.000 0.076 0.924 0.000 0.000
#&gt; SRR1383371     5   0.051   0.710649 0.000 0.000 0.016 0.000 0.984
#&gt; SRR1383372     3   0.167   0.680769 0.000 0.076 0.924 0.000 0.000
#&gt; SRR1383373     3   0.167   0.680769 0.000 0.076 0.924 0.000 0.000
#&gt; SRR1383374     3   0.223   0.644184 0.000 0.116 0.884 0.000 0.000
#&gt; SRR1383375     1   0.000   0.912540 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1383376     2   0.179   0.711284 0.000 0.916 0.084 0.000 0.000
#&gt; SRR1383377     3   0.655  -0.111292 0.000 0.348 0.444 0.208 0.000
#&gt; SRR1383378     2   0.528   0.539861 0.012 0.688 0.084 0.216 0.000
#&gt; SRR1383379     2   0.134   0.699885 0.000 0.944 0.000 0.056 0.000
#&gt; SRR1383380     2   0.174   0.692132 0.012 0.932 0.000 0.056 0.000
#&gt; SRR1383381     5   0.465   0.674234 0.000 0.228 0.060 0.000 0.712
#&gt; SRR1383382     1   0.314   0.881551 0.796 0.000 0.000 0.204 0.000
#&gt; SRR1383383     2   0.260   0.708323 0.000 0.884 0.092 0.024 0.000
#&gt; SRR1383385     1   0.000   0.912540 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1383384     2   0.154   0.715835 0.000 0.932 0.068 0.000 0.000
#&gt; SRR1383386     2   0.808  -0.471720 0.168 0.368 0.132 0.332 0.000
#&gt; SRR1383387     2   0.127   0.701563 0.000 0.948 0.000 0.052 0.000
#&gt; SRR1383389     2   0.673  -0.366751 0.000 0.408 0.328 0.264 0.000
#&gt; SRR1383391     2   0.239   0.714145 0.000 0.896 0.084 0.020 0.000
#&gt; SRR1383388     2   0.272   0.656623 0.012 0.864 0.000 0.124 0.000
#&gt; SRR1383392     3   0.630  -0.000971 0.000 0.384 0.460 0.156 0.000
#&gt; SRR1383390     2   0.248   0.713667 0.000 0.892 0.084 0.024 0.000
#&gt; SRR1383394     2   0.179   0.711284 0.000 0.916 0.084 0.000 0.000
#&gt; SRR1383393     1   0.000   0.912540 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1383396     2   0.528   0.539861 0.012 0.688 0.084 0.216 0.000
#&gt; SRR1383395     3   0.655  -0.111292 0.000 0.348 0.444 0.208 0.000
#&gt; SRR1383399     5   0.465   0.674234 0.000 0.228 0.060 0.000 0.712
#&gt; SRR1383400     1   0.314   0.881551 0.796 0.000 0.000 0.204 0.000
#&gt; SRR1383397     2   0.134   0.699885 0.000 0.944 0.000 0.056 0.000
#&gt; SRR1383401     2   0.260   0.708323 0.000 0.884 0.092 0.024 0.000
#&gt; SRR1383398     2   0.174   0.692132 0.012 0.932 0.000 0.056 0.000
#&gt; SRR1383402     2   0.154   0.715835 0.000 0.932 0.068 0.000 0.000
#&gt; SRR1383404     2   0.808  -0.471720 0.168 0.368 0.132 0.332 0.000
#&gt; SRR1383403     1   0.000   0.912540 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1383405     2   0.127   0.701563 0.000 0.948 0.000 0.052 0.000
#&gt; SRR1383406     2   0.272   0.656623 0.012 0.864 0.000 0.124 0.000
#&gt; SRR1383407     2   0.673  -0.366751 0.000 0.408 0.328 0.264 0.000
#&gt; SRR1383408     2   0.248   0.713667 0.000 0.892 0.084 0.024 0.000
#&gt; SRR1383409     2   0.239   0.714145 0.000 0.896 0.084 0.020 0.000
#&gt; SRR1383410     3   0.630  -0.000971 0.000 0.384 0.460 0.156 0.000
</code></pre>

<script>
$('#tab-MAD-hclust-get-classes-4-a').parent().next().next().hide();
$('#tab-MAD-hclust-get-classes-4-a').click(function(){
  $('#tab-MAD-hclust-get-classes-4-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-MAD-hclust-get-classes-5'>
<p><a id='tab-MAD-hclust-get-classes-5-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 6), get_membership(res, k = 6))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4    p5    p6
#&gt; SRR1383358     3  0.0937    0.73493 0.000 0.000 0.960 0.040 0.000 0.000
#&gt; SRR1383360     2  0.7614    0.00769 0.300 0.392 0.136 0.152 0.000 0.020
#&gt; SRR1383359     2  0.4165   -0.01770 0.000 0.536 0.452 0.000 0.012 0.000
#&gt; SRR1383362     6  0.0000    1.00000 0.000 0.000 0.000 0.000 0.000 1.000
#&gt; SRR1383361     3  0.0937    0.73493 0.000 0.000 0.960 0.040 0.000 0.000
#&gt; SRR1383363     3  0.0937    0.73493 0.000 0.000 0.960 0.040 0.000 0.000
#&gt; SRR1383364     5  0.0363    0.66366 0.000 0.000 0.012 0.000 0.988 0.000
#&gt; SRR1383365     3  0.0937    0.73493 0.000 0.000 0.960 0.040 0.000 0.000
#&gt; SRR1383366     3  0.1075    0.72498 0.000 0.000 0.952 0.048 0.000 0.000
#&gt; SRR1383367     3  0.0937    0.73493 0.000 0.000 0.960 0.040 0.000 0.000
#&gt; SRR1383368     4  0.7781   -0.25295 0.264 0.272 0.012 0.316 0.000 0.136
#&gt; SRR1383369     3  0.3695    0.20621 0.000 0.000 0.624 0.000 0.376 0.000
#&gt; SRR1383370     3  0.0937    0.73493 0.000 0.000 0.960 0.040 0.000 0.000
#&gt; SRR1383371     5  0.0363    0.66366 0.000 0.000 0.012 0.000 0.988 0.000
#&gt; SRR1383372     3  0.0937    0.73493 0.000 0.000 0.960 0.040 0.000 0.000
#&gt; SRR1383373     3  0.0937    0.73493 0.000 0.000 0.960 0.040 0.000 0.000
#&gt; SRR1383374     3  0.1807    0.70747 0.000 0.020 0.920 0.060 0.000 0.000
#&gt; SRR1383375     1  0.3351    0.28933 0.712 0.000 0.000 0.000 0.000 0.288
#&gt; SRR1383376     4  0.3270    0.72410 0.000 0.060 0.120 0.820 0.000 0.000
#&gt; SRR1383377     3  0.6183    0.31137 0.036 0.128 0.460 0.376 0.000 0.000
#&gt; SRR1383378     4  0.6126    0.50274 0.160 0.156 0.084 0.600 0.000 0.000
#&gt; SRR1383379     4  0.0622    0.72480 0.000 0.012 0.008 0.980 0.000 0.000
#&gt; SRR1383380     4  0.0547    0.71805 0.000 0.020 0.000 0.980 0.000 0.000
#&gt; SRR1383381     5  0.4254    0.66298 0.000 0.000 0.072 0.216 0.712 0.000
#&gt; SRR1383382     6  0.0000    1.00000 0.000 0.000 0.000 0.000 0.000 1.000
#&gt; SRR1383383     4  0.3787    0.72355 0.000 0.100 0.120 0.780 0.000 0.000
#&gt; SRR1383385     1  0.3351    0.28933 0.712 0.000 0.000 0.000 0.000 0.288
#&gt; SRR1383384     4  0.3045    0.72877 0.000 0.060 0.100 0.840 0.000 0.000
#&gt; SRR1383386     4  0.7781   -0.25295 0.264 0.272 0.012 0.316 0.000 0.136
#&gt; SRR1383387     4  0.0520    0.72608 0.000 0.008 0.008 0.984 0.000 0.000
#&gt; SRR1383389     1  0.7702   -0.18006 0.284 0.268 0.236 0.212 0.000 0.000
#&gt; SRR1383391     4  0.3693    0.72911 0.000 0.092 0.120 0.788 0.000 0.000
#&gt; SRR1383388     4  0.1863    0.68848 0.000 0.104 0.000 0.896 0.000 0.000
#&gt; SRR1383392     3  0.6344    0.36591 0.036 0.180 0.492 0.292 0.000 0.000
#&gt; SRR1383390     4  0.3832    0.72659 0.000 0.104 0.120 0.776 0.000 0.000
#&gt; SRR1383394     4  0.3270    0.72410 0.000 0.060 0.120 0.820 0.000 0.000
#&gt; SRR1383393     1  0.3351    0.28933 0.712 0.000 0.000 0.000 0.000 0.288
#&gt; SRR1383396     4  0.6126    0.50274 0.160 0.156 0.084 0.600 0.000 0.000
#&gt; SRR1383395     3  0.6183    0.31137 0.036 0.128 0.460 0.376 0.000 0.000
#&gt; SRR1383399     5  0.4254    0.66298 0.000 0.000 0.072 0.216 0.712 0.000
#&gt; SRR1383400     6  0.0000    1.00000 0.000 0.000 0.000 0.000 0.000 1.000
#&gt; SRR1383397     4  0.0622    0.72480 0.000 0.012 0.008 0.980 0.000 0.000
#&gt; SRR1383401     4  0.3787    0.72355 0.000 0.100 0.120 0.780 0.000 0.000
#&gt; SRR1383398     4  0.0547    0.71805 0.000 0.020 0.000 0.980 0.000 0.000
#&gt; SRR1383402     4  0.3045    0.72877 0.000 0.060 0.100 0.840 0.000 0.000
#&gt; SRR1383404     4  0.7781   -0.25295 0.264 0.272 0.012 0.316 0.000 0.136
#&gt; SRR1383403     1  0.3351    0.28933 0.712 0.000 0.000 0.000 0.000 0.288
#&gt; SRR1383405     4  0.0520    0.72608 0.000 0.008 0.008 0.984 0.000 0.000
#&gt; SRR1383406     4  0.1863    0.68848 0.000 0.104 0.000 0.896 0.000 0.000
#&gt; SRR1383407     1  0.7702   -0.18006 0.284 0.268 0.236 0.212 0.000 0.000
#&gt; SRR1383408     4  0.3832    0.72659 0.000 0.104 0.120 0.776 0.000 0.000
#&gt; SRR1383409     4  0.3693    0.72911 0.000 0.092 0.120 0.788 0.000 0.000
#&gt; SRR1383410     3  0.6344    0.36591 0.036 0.180 0.492 0.292 0.000 0.000
</code></pre>

<script>
$('#tab-MAD-hclust-get-classes-5-a').parent().next().next().hide();
$('#tab-MAD-hclust-get-classes-5-a').click(function(){
  $('#tab-MAD-hclust-get-classes-5-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>
</div>

Heatmaps for the consensus matrix. It visualizes the probability of two
samples to be in a same group.



<script>
$( function() {
	$( '#tabs-MAD-hclust-consensus-heatmap' ).tabs();
} );
</script>
<div id='tabs-MAD-hclust-consensus-heatmap'>
<ul>
<li><a href='#tab-MAD-hclust-consensus-heatmap-1'>k = 2</a></li>
<li><a href='#tab-MAD-hclust-consensus-heatmap-2'>k = 3</a></li>
<li><a href='#tab-MAD-hclust-consensus-heatmap-3'>k = 4</a></li>
<li><a href='#tab-MAD-hclust-consensus-heatmap-4'>k = 5</a></li>
<li><a href='#tab-MAD-hclust-consensus-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-MAD-hclust-consensus-heatmap-1'>
<pre><code class="r">consensus_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-MAD-hclust-consensus-heatmap-1-1.png" alt="plot of chunk tab-MAD-hclust-consensus-heatmap-1"/></p>

</div>
<div id='tab-MAD-hclust-consensus-heatmap-2'>
<pre><code class="r">consensus_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-MAD-hclust-consensus-heatmap-2-1.png" alt="plot of chunk tab-MAD-hclust-consensus-heatmap-2"/></p>

</div>
<div id='tab-MAD-hclust-consensus-heatmap-3'>
<pre><code class="r">consensus_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-MAD-hclust-consensus-heatmap-3-1.png" alt="plot of chunk tab-MAD-hclust-consensus-heatmap-3"/></p>

</div>
<div id='tab-MAD-hclust-consensus-heatmap-4'>
<pre><code class="r">consensus_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-MAD-hclust-consensus-heatmap-4-1.png" alt="plot of chunk tab-MAD-hclust-consensus-heatmap-4"/></p>

</div>
<div id='tab-MAD-hclust-consensus-heatmap-5'>
<pre><code class="r">consensus_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-MAD-hclust-consensus-heatmap-5-1.png" alt="plot of chunk tab-MAD-hclust-consensus-heatmap-5"/></p>

</div>
</div>

Heatmaps for the membership of samples in all partitions to see how consistent they are:




<script>
$( function() {
	$( '#tabs-MAD-hclust-membership-heatmap' ).tabs();
} );
</script>
<div id='tabs-MAD-hclust-membership-heatmap'>
<ul>
<li><a href='#tab-MAD-hclust-membership-heatmap-1'>k = 2</a></li>
<li><a href='#tab-MAD-hclust-membership-heatmap-2'>k = 3</a></li>
<li><a href='#tab-MAD-hclust-membership-heatmap-3'>k = 4</a></li>
<li><a href='#tab-MAD-hclust-membership-heatmap-4'>k = 5</a></li>
<li><a href='#tab-MAD-hclust-membership-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-MAD-hclust-membership-heatmap-1'>
<pre><code class="r">membership_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-MAD-hclust-membership-heatmap-1-1.png" alt="plot of chunk tab-MAD-hclust-membership-heatmap-1"/></p>

</div>
<div id='tab-MAD-hclust-membership-heatmap-2'>
<pre><code class="r">membership_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-MAD-hclust-membership-heatmap-2-1.png" alt="plot of chunk tab-MAD-hclust-membership-heatmap-2"/></p>

</div>
<div id='tab-MAD-hclust-membership-heatmap-3'>
<pre><code class="r">membership_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-MAD-hclust-membership-heatmap-3-1.png" alt="plot of chunk tab-MAD-hclust-membership-heatmap-3"/></p>

</div>
<div id='tab-MAD-hclust-membership-heatmap-4'>
<pre><code class="r">membership_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-MAD-hclust-membership-heatmap-4-1.png" alt="plot of chunk tab-MAD-hclust-membership-heatmap-4"/></p>

</div>
<div id='tab-MAD-hclust-membership-heatmap-5'>
<pre><code class="r">membership_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-MAD-hclust-membership-heatmap-5-1.png" alt="plot of chunk tab-MAD-hclust-membership-heatmap-5"/></p>

</div>
</div>

As soon as we have had the classes for columns, we can look for signatures
which are significantly different between classes which can be candidate marks
for certain classes. Following are the heatmaps for signatures.



Signature heatmaps where rows are scaled:



<script>
$( function() {
	$( '#tabs-MAD-hclust-get-signatures' ).tabs();
} );
</script>
<div id='tabs-MAD-hclust-get-signatures'>
<ul>
<li><a href='#tab-MAD-hclust-get-signatures-1'>k = 2</a></li>
<li><a href='#tab-MAD-hclust-get-signatures-2'>k = 3</a></li>
<li><a href='#tab-MAD-hclust-get-signatures-3'>k = 4</a></li>
<li><a href='#tab-MAD-hclust-get-signatures-4'>k = 5</a></li>
<li><a href='#tab-MAD-hclust-get-signatures-5'>k = 6</a></li>
</ul>
<div id='tab-MAD-hclust-get-signatures-1'>
<pre><code class="r">get_signatures(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-MAD-hclust-get-signatures-1-1.png" alt="plot of chunk tab-MAD-hclust-get-signatures-1"/></p>

</div>
<div id='tab-MAD-hclust-get-signatures-2'>
<pre><code class="r">get_signatures(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-MAD-hclust-get-signatures-2-1.png" alt="plot of chunk tab-MAD-hclust-get-signatures-2"/></p>

</div>
<div id='tab-MAD-hclust-get-signatures-3'>
<pre><code class="r">get_signatures(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-MAD-hclust-get-signatures-3-1.png" alt="plot of chunk tab-MAD-hclust-get-signatures-3"/></p>

</div>
<div id='tab-MAD-hclust-get-signatures-4'>
<pre><code class="r">get_signatures(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-MAD-hclust-get-signatures-4-1.png" alt="plot of chunk tab-MAD-hclust-get-signatures-4"/></p>

</div>
<div id='tab-MAD-hclust-get-signatures-5'>
<pre><code class="r">get_signatures(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-MAD-hclust-get-signatures-5-1.png" alt="plot of chunk tab-MAD-hclust-get-signatures-5"/></p>

</div>
</div>



Signature heatmaps where rows are not scaled:


<script>
$( function() {
	$( '#tabs-MAD-hclust-get-signatures-no-scale' ).tabs();
} );
</script>
<div id='tabs-MAD-hclust-get-signatures-no-scale'>
<ul>
<li><a href='#tab-MAD-hclust-get-signatures-no-scale-1'>k = 2</a></li>
<li><a href='#tab-MAD-hclust-get-signatures-no-scale-2'>k = 3</a></li>
<li><a href='#tab-MAD-hclust-get-signatures-no-scale-3'>k = 4</a></li>
<li><a href='#tab-MAD-hclust-get-signatures-no-scale-4'>k = 5</a></li>
<li><a href='#tab-MAD-hclust-get-signatures-no-scale-5'>k = 6</a></li>
</ul>
<div id='tab-MAD-hclust-get-signatures-no-scale-1'>
<pre><code class="r">get_signatures(res, k = 2, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-MAD-hclust-get-signatures-no-scale-1-1.png" alt="plot of chunk tab-MAD-hclust-get-signatures-no-scale-1"/></p>

</div>
<div id='tab-MAD-hclust-get-signatures-no-scale-2'>
<pre><code class="r">get_signatures(res, k = 3, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-MAD-hclust-get-signatures-no-scale-2-1.png" alt="plot of chunk tab-MAD-hclust-get-signatures-no-scale-2"/></p>

</div>
<div id='tab-MAD-hclust-get-signatures-no-scale-3'>
<pre><code class="r">get_signatures(res, k = 4, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-MAD-hclust-get-signatures-no-scale-3-1.png" alt="plot of chunk tab-MAD-hclust-get-signatures-no-scale-3"/></p>

</div>
<div id='tab-MAD-hclust-get-signatures-no-scale-4'>
<pre><code class="r">get_signatures(res, k = 5, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-MAD-hclust-get-signatures-no-scale-4-1.png" alt="plot of chunk tab-MAD-hclust-get-signatures-no-scale-4"/></p>

</div>
<div id='tab-MAD-hclust-get-signatures-no-scale-5'>
<pre><code class="r">get_signatures(res, k = 6, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-MAD-hclust-get-signatures-no-scale-5-1.png" alt="plot of chunk tab-MAD-hclust-get-signatures-no-scale-5"/></p>

</div>
</div>



Compare the overlap of signatures from different k:

```r
compare_signatures(res)
```

![plot of chunk MAD-hclust-signature_compare](figure_cola/MAD-hclust-signature_compare-1.png)

`get_signature()` returns a data frame invisibly. TO get the list of signatures, the function
call should be assigned to a variable explicitly. In following code, if `plot` argument is set
to `FALSE`, no heatmap is plotted while only the differential analysis is performed.

```r
# code only for demonstration
tb = get_signature(res, k = ..., plot = FALSE)
```

An example of the output of `tb` is:

```
#>   which_row         fdr    mean_1    mean_2 scaled_mean_1 scaled_mean_2 km
#> 1        38 0.042760348  8.373488  9.131774    -0.5533452     0.5164555  1
#> 2        40 0.018707592  7.106213  8.469186    -0.6173731     0.5762149  1
#> 3        55 0.019134737 10.221463 11.207825    -0.6159697     0.5749050  1
#> 4        59 0.006059896  5.921854  7.869574    -0.6899429     0.6439467  1
#> 5        60 0.018055526  8.928898 10.211722    -0.6204761     0.5791110  1
#> 6        98 0.009384629 15.714769 14.887706     0.6635654    -0.6193277  2
...
```

The columns in `tb` are:

1. `which_row`: row indices corresponding to the input matrix.
2. `fdr`: FDR for the differential test. 
3. `mean_x`: The mean value in group x.
4. `scaled_mean_x`: The mean value in group x after rows are scaled.
5. `km`: Row groups if k-means clustering is applied to rows.



UMAP plot which shows how samples are separated.


<script>
$( function() {
	$( '#tabs-MAD-hclust-dimension-reduction' ).tabs();
} );
</script>
<div id='tabs-MAD-hclust-dimension-reduction'>
<ul>
<li><a href='#tab-MAD-hclust-dimension-reduction-1'>k = 2</a></li>
<li><a href='#tab-MAD-hclust-dimension-reduction-2'>k = 3</a></li>
<li><a href='#tab-MAD-hclust-dimension-reduction-3'>k = 4</a></li>
<li><a href='#tab-MAD-hclust-dimension-reduction-4'>k = 5</a></li>
<li><a href='#tab-MAD-hclust-dimension-reduction-5'>k = 6</a></li>
</ul>
<div id='tab-MAD-hclust-dimension-reduction-1'>
<pre><code class="r">dimension_reduction(res, k = 2, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-MAD-hclust-dimension-reduction-1-1.png" alt="plot of chunk tab-MAD-hclust-dimension-reduction-1"/></p>

</div>
<div id='tab-MAD-hclust-dimension-reduction-2'>
<pre><code class="r">dimension_reduction(res, k = 3, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-MAD-hclust-dimension-reduction-2-1.png" alt="plot of chunk tab-MAD-hclust-dimension-reduction-2"/></p>

</div>
<div id='tab-MAD-hclust-dimension-reduction-3'>
<pre><code class="r">dimension_reduction(res, k = 4, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-MAD-hclust-dimension-reduction-3-1.png" alt="plot of chunk tab-MAD-hclust-dimension-reduction-3"/></p>

</div>
<div id='tab-MAD-hclust-dimension-reduction-4'>
<pre><code class="r">dimension_reduction(res, k = 5, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-MAD-hclust-dimension-reduction-4-1.png" alt="plot of chunk tab-MAD-hclust-dimension-reduction-4"/></p>

</div>
<div id='tab-MAD-hclust-dimension-reduction-5'>
<pre><code class="r">dimension_reduction(res, k = 6, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-MAD-hclust-dimension-reduction-5-1.png" alt="plot of chunk tab-MAD-hclust-dimension-reduction-5"/></p>

</div>
</div>


Following heatmap shows how subgroups are split when increasing `k`:

```r
collect_classes(res)
```

![plot of chunk MAD-hclust-collect-classes](figure_cola/MAD-hclust-collect-classes-1.png)


If matrix rows can be associated to genes, consider to use `functional_enrichment(res,
...)` to perform function enrichment for the signature genes. See [this vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/functional_enrichment.html) for more detailed explanations.


 

---------------------------------------------------




### MAD:kmeans






The object with results only for a single top-value method and a single partition method 
can be extracted as:

```r
res = res_list["MAD", "kmeans"]
# you can also extract it by
# res = res_list["MAD:kmeans"]
```

A summary of `res` and all the functions that can be applied to it:

```r
res
```

```
#> A 'ConsensusPartition' object with k = 2, 3, 4, 5, 6.
#>   On a matrix with 15680 rows and 53 columns.
#>   Top rows (1000, 2000, 3000, 4000, 5000) are extracted by 'MAD' method.
#>   Subgroups are detected by 'kmeans' method.
#>   Performed in total 1250 partitions by row resampling.
#>   Best k for subgroups seems to be 3.
#> 
#> Following methods can be applied to this 'ConsensusPartition' object:
#>  [1] "cola_report"             "collect_classes"         "collect_plots"          
#>  [4] "collect_stats"           "colnames"                "compare_signatures"     
#>  [7] "consensus_heatmap"       "dimension_reduction"     "functional_enrichment"  
#> [10] "get_anno_col"            "get_anno"                "get_classes"            
#> [13] "get_consensus"           "get_matrix"              "get_membership"         
#> [16] "get_param"               "get_signatures"          "get_stats"              
#> [19] "is_best_k"               "is_stable_k"             "membership_heatmap"     
#> [22] "ncol"                    "nrow"                    "plot_ecdf"              
#> [25] "rownames"                "select_partition_number" "show"                   
#> [28] "suggest_best_k"          "test_to_known_factors"
```

`collect_plots()` function collects all the plots made from `res` for all `k` (number of partitions)
into one single page to provide an easy and fast comparison between different `k`.

```r
collect_plots(res)
```

![plot of chunk MAD-kmeans-collect-plots](figure_cola/MAD-kmeans-collect-plots-1.png)

The plots are:

- The first row: a plot of the ECDF (empirical cumulative distribution
  function) curves of the consensus matrix for each `k` and the heatmap of
  predicted classes for each `k`.
- The second row: heatmaps of the consensus matrix for each `k`.
- The third row: heatmaps of the membership matrix for each `k`.
- The fouth row: heatmaps of the signatures for each `k`.

All the plots in panels can be made by individual functions and they are
plotted later in this section.

`select_partition_number()` produces several plots showing different
statistics for choosing "optimized" `k`. There are following statistics:

- ECDF curves of the consensus matrix for each `k`;
- 1-PAC. [The PAC
  score](https://en.wikipedia.org/wiki/Consensus_clustering#Over-interpretation_potential_of_consensus_clustering)
  measures the proportion of the ambiguous subgrouping.
- Mean silhouette score.
- Concordance. The mean probability of fiting the consensus class ids in all
  partitions.
- Area increased. Denote $A_k$ as the area under the ECDF curve for current
  `k`, the area increased is defined as $A_k - A_{k-1}$.
- Rand index. The percent of pairs of samples that are both in a same cluster
  or both are not in a same cluster in the partition of k and k-1.
- Jaccard index. The ratio of pairs of samples are both in a same cluster in
  the partition of k and k-1 and the pairs of samples are both in a same
  cluster in the partition k or k-1.

The detailed explanations of these statistics can be found in [the _cola_
vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/cola.html#toc_13).

Generally speaking, lower PAC score, higher mean silhouette score or higher
concordance corresponds to better partition. Rand index and Jaccard index
measure how similar the current partition is compared to partition with `k-1`.
If they are too similar, we won't accept `k` is better than `k-1`.

```r
select_partition_number(res)
```

![plot of chunk MAD-kmeans-select-partition-number](figure_cola/MAD-kmeans-select-partition-number-1.png)

The numeric values for all these statistics can be obtained by `get_stats()`.

```r
get_stats(res)
```

```
#>   k 1-PAC mean_silhouette concordance area_increased  Rand Jaccard
#> 2 2 0.420           0.837       0.888         0.4387 0.531   0.531
#> 3 3 0.563           0.853       0.899         0.3964 0.586   0.372
#> 4 4 0.607           0.576       0.762         0.1516 0.939   0.838
#> 5 5 0.662           0.678       0.793         0.0888 0.845   0.552
#> 6 6 0.704           0.716       0.798         0.0494 0.988   0.945
```

`suggest_best_k()` suggests the best $k$ based on these statistics. The rules are as follows:

- All $k$ with Jaccard index larger than 0.95 are removed because increasing
  $k$ does not provide enough extra information. If all $k$ are removed, it is
  marked as no subgroup is detected.
- For all $k$ with 1-PAC score larger than 0.9, the maximal $k$ is taken as
  the best $k$, and other $k$ are marked as optional $k$.
- If it does not fit the second rule. The $k$ with the maximal vote of the
  highest 1-PAC score, highest mean silhouette, and highest concordance is
  taken as the best $k$.

```r
suggest_best_k(res)
```

```
#> [1] 3
```


Following shows the table of the partitions (You need to click the **show/hide
code output** link to see it). The membership matrix (columns with name `p*`)
is inferred by
[`clue::cl_consensus()`](https://www.rdocumentation.org/link/cl_consensus?package=clue)
function with the `SE` method. Basically the value in the membership matrix
represents the probability to belong to a certain group. The finall class
label for an item is determined with the group with highest probability it
belongs to.

In `get_classes()` function, the entropy is calculated from the membership
matrix and the silhouette score is calculated from the consensus matrix.



<script>
$( function() {
	$( '#tabs-MAD-kmeans-get-classes' ).tabs();
} );
</script>
<div id='tabs-MAD-kmeans-get-classes'>
<ul>
<li><a href='#tab-MAD-kmeans-get-classes-1'>k = 2</a></li>
<li><a href='#tab-MAD-kmeans-get-classes-2'>k = 3</a></li>
<li><a href='#tab-MAD-kmeans-get-classes-3'>k = 4</a></li>
<li><a href='#tab-MAD-kmeans-get-classes-4'>k = 5</a></li>
<li><a href='#tab-MAD-kmeans-get-classes-5'>k = 6</a></li>
</ul>

<div id='tab-MAD-kmeans-get-classes-1'>
<p><a id='tab-MAD-kmeans-get-classes-1-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 2), get_membership(res, k = 2))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2
#&gt; SRR1383358     2   0.469      0.890 0.100 0.900
#&gt; SRR1383360     1   0.904      0.622 0.680 0.320
#&gt; SRR1383359     2   0.469      0.890 0.100 0.900
#&gt; SRR1383362     1   0.224      0.797 0.964 0.036
#&gt; SRR1383361     2   0.469      0.890 0.100 0.900
#&gt; SRR1383363     2   0.469      0.890 0.100 0.900
#&gt; SRR1383364     2   0.552      0.866 0.128 0.872
#&gt; SRR1383365     2   0.469      0.890 0.100 0.900
#&gt; SRR1383366     2   0.278      0.901 0.048 0.952
#&gt; SRR1383367     2   0.469      0.890 0.100 0.900
#&gt; SRR1383368     1   0.494      0.789 0.892 0.108
#&gt; SRR1383369     2   0.416      0.896 0.084 0.916
#&gt; SRR1383370     2   0.469      0.890 0.100 0.900
#&gt; SRR1383371     2   0.552      0.866 0.128 0.872
#&gt; SRR1383372     2   0.469      0.890 0.100 0.900
#&gt; SRR1383373     2   0.469      0.890 0.100 0.900
#&gt; SRR1383374     2   0.000      0.902 0.000 1.000
#&gt; SRR1383375     1   0.000      0.818 1.000 0.000
#&gt; SRR1383376     2   0.327      0.905 0.060 0.940
#&gt; SRR1383377     2   0.402      0.909 0.080 0.920
#&gt; SRR1383378     1   0.991      0.478 0.556 0.444
#&gt; SRR1383379     1   0.900      0.710 0.684 0.316
#&gt; SRR1383380     1   0.900      0.710 0.684 0.316
#&gt; SRR1383381     2   0.644      0.885 0.164 0.836
#&gt; SRR1383382     1   0.000      0.818 1.000 0.000
#&gt; SRR1383383     2   0.327      0.905 0.060 0.940
#&gt; SRR1383385     1   0.000      0.818 1.000 0.000
#&gt; SRR1383384     2   0.327      0.905 0.060 0.940
#&gt; SRR1383386     1   0.260      0.811 0.956 0.044
#&gt; SRR1383387     2   0.327      0.905 0.060 0.940
#&gt; SRR1383389     2   0.541      0.905 0.124 0.876
#&gt; SRR1383391     2   0.327      0.905 0.060 0.940
#&gt; SRR1383388     1   0.730      0.779 0.796 0.204
#&gt; SRR1383392     2   0.163      0.907 0.024 0.976
#&gt; SRR1383390     2   0.327      0.905 0.060 0.940
#&gt; SRR1383394     2   0.327      0.905 0.060 0.940
#&gt; SRR1383393     1   0.000      0.818 1.000 0.000
#&gt; SRR1383396     1   0.680      0.768 0.820 0.180
#&gt; SRR1383395     2   0.402      0.909 0.080 0.920
#&gt; SRR1383399     2   0.644      0.885 0.164 0.836
#&gt; SRR1383400     1   0.000      0.818 1.000 0.000
#&gt; SRR1383397     1   1.000      0.326 0.500 0.500
#&gt; SRR1383401     2   0.242      0.907 0.040 0.960
#&gt; SRR1383398     1   0.900      0.710 0.684 0.316
#&gt; SRR1383402     2   0.327      0.905 0.060 0.940
#&gt; SRR1383404     1   0.430      0.809 0.912 0.088
#&gt; SRR1383403     1   0.000      0.818 1.000 0.000
#&gt; SRR1383405     2   0.327      0.905 0.060 0.940
#&gt; SRR1383406     1   0.952      0.634 0.628 0.372
#&gt; SRR1383407     2   0.482      0.908 0.104 0.896
#&gt; SRR1383408     2   0.327      0.905 0.060 0.940
#&gt; SRR1383409     2   0.327      0.905 0.060 0.940
#&gt; SRR1383410     2   0.224      0.907 0.036 0.964
</code></pre>

<script>
$('#tab-MAD-kmeans-get-classes-1-a').parent().next().next().hide();
$('#tab-MAD-kmeans-get-classes-1-a').click(function(){
  $('#tab-MAD-kmeans-get-classes-1-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-MAD-kmeans-get-classes-2'>
<p><a id='tab-MAD-kmeans-get-classes-2-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 3), get_membership(res, k = 3))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3
#&gt; SRR1383358     3  0.2200      0.931 0.004 0.056 0.940
#&gt; SRR1383360     3  0.6336      0.732 0.180 0.064 0.756
#&gt; SRR1383359     3  0.2200      0.931 0.004 0.056 0.940
#&gt; SRR1383362     1  0.1015      0.879 0.980 0.008 0.012
#&gt; SRR1383361     3  0.2200      0.931 0.004 0.056 0.940
#&gt; SRR1383363     3  0.2200      0.931 0.004 0.056 0.940
#&gt; SRR1383364     3  0.1453      0.893 0.024 0.008 0.968
#&gt; SRR1383365     3  0.2200      0.931 0.004 0.056 0.940
#&gt; SRR1383366     3  0.3267      0.888 0.000 0.116 0.884
#&gt; SRR1383367     3  0.2200      0.931 0.004 0.056 0.940
#&gt; SRR1383368     3  0.5171      0.738 0.204 0.012 0.784
#&gt; SRR1383369     3  0.2031      0.912 0.016 0.032 0.952
#&gt; SRR1383370     3  0.2200      0.931 0.004 0.056 0.940
#&gt; SRR1383371     3  0.1453      0.893 0.024 0.008 0.968
#&gt; SRR1383372     3  0.1964      0.929 0.000 0.056 0.944
#&gt; SRR1383373     3  0.2200      0.931 0.004 0.056 0.940
#&gt; SRR1383374     3  0.2066      0.927 0.000 0.060 0.940
#&gt; SRR1383375     1  0.2297      0.890 0.944 0.036 0.020
#&gt; SRR1383376     2  0.1529      0.896 0.000 0.960 0.040
#&gt; SRR1383377     2  0.3752      0.836 0.000 0.856 0.144
#&gt; SRR1383378     2  0.3966      0.884 0.024 0.876 0.100
#&gt; SRR1383379     2  0.1170      0.872 0.016 0.976 0.008
#&gt; SRR1383380     2  0.3805      0.802 0.092 0.884 0.024
#&gt; SRR1383381     3  0.4802      0.775 0.020 0.156 0.824
#&gt; SRR1383382     1  0.0983      0.885 0.980 0.016 0.004
#&gt; SRR1383383     2  0.3349      0.891 0.004 0.888 0.108
#&gt; SRR1383385     1  0.2297      0.890 0.944 0.036 0.020
#&gt; SRR1383384     2  0.2261      0.899 0.000 0.932 0.068
#&gt; SRR1383386     1  0.5115      0.712 0.768 0.228 0.004
#&gt; SRR1383387     2  0.1031      0.890 0.000 0.976 0.024
#&gt; SRR1383389     2  0.4842      0.797 0.000 0.776 0.224
#&gt; SRR1383391     2  0.2959      0.895 0.000 0.900 0.100
#&gt; SRR1383388     2  0.3129      0.818 0.088 0.904 0.008
#&gt; SRR1383392     2  0.4291      0.832 0.000 0.820 0.180
#&gt; SRR1383390     2  0.3116      0.891 0.000 0.892 0.108
#&gt; SRR1383394     2  0.1529      0.896 0.000 0.960 0.040
#&gt; SRR1383393     1  0.2297      0.890 0.944 0.036 0.020
#&gt; SRR1383396     2  0.6031      0.802 0.116 0.788 0.096
#&gt; SRR1383395     2  0.3752      0.836 0.000 0.856 0.144
#&gt; SRR1383399     3  0.4802      0.775 0.020 0.156 0.824
#&gt; SRR1383400     1  0.0983      0.885 0.980 0.016 0.004
#&gt; SRR1383397     2  0.0661      0.879 0.004 0.988 0.008
#&gt; SRR1383401     2  0.3425      0.890 0.004 0.884 0.112
#&gt; SRR1383398     2  0.3805      0.802 0.092 0.884 0.024
#&gt; SRR1383402     2  0.2261      0.899 0.000 0.932 0.068
#&gt; SRR1383404     1  0.6509      0.144 0.524 0.472 0.004
#&gt; SRR1383403     1  0.2297      0.890 0.944 0.036 0.020
#&gt; SRR1383405     2  0.1031      0.890 0.000 0.976 0.024
#&gt; SRR1383406     2  0.0661      0.879 0.004 0.988 0.008
#&gt; SRR1383407     2  0.5859      0.598 0.000 0.656 0.344
#&gt; SRR1383408     2  0.3116      0.891 0.000 0.892 0.108
#&gt; SRR1383409     2  0.2959      0.895 0.000 0.900 0.100
#&gt; SRR1383410     2  0.2448      0.899 0.000 0.924 0.076
</code></pre>

<script>
$('#tab-MAD-kmeans-get-classes-2-a').parent().next().next().hide();
$('#tab-MAD-kmeans-get-classes-2-a').click(function(){
  $('#tab-MAD-kmeans-get-classes-2-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-MAD-kmeans-get-classes-3'>
<p><a id='tab-MAD-kmeans-get-classes-3-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 4), get_membership(res, k = 4))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4
#&gt; SRR1383358     3  0.1584     0.8665 0.000 0.036 0.952 0.012
#&gt; SRR1383360     3  0.4814     0.7346 0.088 0.012 0.804 0.096
#&gt; SRR1383359     3  0.1820     0.8635 0.000 0.036 0.944 0.020
#&gt; SRR1383362     1  0.0000     0.7681 1.000 0.000 0.000 0.000
#&gt; SRR1383361     3  0.1637     0.8724 0.000 0.060 0.940 0.000
#&gt; SRR1383363     3  0.1716     0.8721 0.000 0.064 0.936 0.000
#&gt; SRR1383364     3  0.4761     0.5365 0.000 0.004 0.664 0.332
#&gt; SRR1383365     3  0.1584     0.8665 0.000 0.036 0.952 0.012
#&gt; SRR1383366     3  0.2411     0.8501 0.000 0.040 0.920 0.040
#&gt; SRR1383367     3  0.1637     0.8724 0.000 0.060 0.940 0.000
#&gt; SRR1383368     3  0.4482     0.7433 0.148 0.016 0.808 0.028
#&gt; SRR1383369     3  0.4647     0.5951 0.000 0.008 0.704 0.288
#&gt; SRR1383370     3  0.1637     0.8724 0.000 0.060 0.940 0.000
#&gt; SRR1383371     3  0.4741     0.5424 0.000 0.004 0.668 0.328
#&gt; SRR1383372     3  0.1792     0.8701 0.000 0.068 0.932 0.000
#&gt; SRR1383373     3  0.1716     0.8721 0.000 0.064 0.936 0.000
#&gt; SRR1383374     3  0.1902     0.8697 0.000 0.064 0.932 0.004
#&gt; SRR1383375     1  0.3486     0.7893 0.812 0.000 0.000 0.188
#&gt; SRR1383376     2  0.1545     0.6588 0.000 0.952 0.008 0.040
#&gt; SRR1383377     2  0.7046     0.2971 0.000 0.524 0.136 0.340
#&gt; SRR1383378     2  0.3808     0.5919 0.000 0.812 0.012 0.176
#&gt; SRR1383379     2  0.5088     0.2570 0.000 0.572 0.004 0.424
#&gt; SRR1383380     4  0.6214    -0.1488 0.044 0.428 0.004 0.524
#&gt; SRR1383381     4  0.7393     0.1345 0.000 0.180 0.332 0.488
#&gt; SRR1383382     1  0.0000     0.7681 1.000 0.000 0.000 0.000
#&gt; SRR1383383     2  0.2861     0.6352 0.000 0.888 0.016 0.096
#&gt; SRR1383385     1  0.3610     0.7868 0.800 0.000 0.000 0.200
#&gt; SRR1383384     2  0.0779     0.6667 0.000 0.980 0.016 0.004
#&gt; SRR1383386     1  0.7264     0.3844 0.564 0.212 0.004 0.220
#&gt; SRR1383387     2  0.4621     0.4579 0.000 0.708 0.008 0.284
#&gt; SRR1383389     2  0.5624     0.4769 0.000 0.724 0.128 0.148
#&gt; SRR1383391     2  0.1059     0.6651 0.000 0.972 0.012 0.016
#&gt; SRR1383388     2  0.6146     0.1386 0.040 0.524 0.004 0.432
#&gt; SRR1383392     2  0.4344     0.5818 0.000 0.816 0.108 0.076
#&gt; SRR1383390     2  0.2450     0.6429 0.000 0.912 0.016 0.072
#&gt; SRR1383394     2  0.1545     0.6588 0.000 0.952 0.008 0.040
#&gt; SRR1383393     1  0.3486     0.7893 0.812 0.000 0.000 0.188
#&gt; SRR1383396     2  0.6548     0.3171 0.064 0.588 0.012 0.336
#&gt; SRR1383395     2  0.7046     0.2971 0.000 0.524 0.136 0.340
#&gt; SRR1383399     4  0.7393     0.1345 0.000 0.180 0.332 0.488
#&gt; SRR1383400     1  0.0000     0.7681 1.000 0.000 0.000 0.000
#&gt; SRR1383397     2  0.5088     0.2570 0.000 0.572 0.004 0.424
#&gt; SRR1383401     2  0.2861     0.6352 0.000 0.888 0.016 0.096
#&gt; SRR1383398     4  0.6214    -0.1488 0.044 0.428 0.004 0.524
#&gt; SRR1383402     2  0.0657     0.6666 0.000 0.984 0.012 0.004
#&gt; SRR1383404     1  0.7988     0.0419 0.408 0.284 0.004 0.304
#&gt; SRR1383403     1  0.3610     0.7868 0.800 0.000 0.000 0.200
#&gt; SRR1383405     2  0.4621     0.4579 0.000 0.708 0.008 0.284
#&gt; SRR1383406     2  0.5088     0.2570 0.000 0.572 0.004 0.424
#&gt; SRR1383407     2  0.6231     0.3844 0.000 0.668 0.184 0.148
#&gt; SRR1383408     2  0.2450     0.6429 0.000 0.912 0.016 0.072
#&gt; SRR1383409     2  0.1182     0.6641 0.000 0.968 0.016 0.016
#&gt; SRR1383410     2  0.2402     0.6581 0.000 0.912 0.012 0.076
</code></pre>

<script>
$('#tab-MAD-kmeans-get-classes-3-a').parent().next().next().hide();
$('#tab-MAD-kmeans-get-classes-3-a').click(function(){
  $('#tab-MAD-kmeans-get-classes-3-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-MAD-kmeans-get-classes-4'>
<p><a id='tab-MAD-kmeans-get-classes-4-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 5), get_membership(res, k = 5))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4    p5
#&gt; SRR1383358     3  0.1787      0.852 0.000 0.032 0.940 0.016 0.012
#&gt; SRR1383360     3  0.4649      0.654 0.076 0.000 0.788 0.076 0.060
#&gt; SRR1383359     3  0.2532      0.828 0.000 0.028 0.908 0.028 0.036
#&gt; SRR1383362     1  0.0000      0.778 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1383361     3  0.0703      0.867 0.000 0.024 0.976 0.000 0.000
#&gt; SRR1383363     3  0.0865      0.867 0.000 0.024 0.972 0.004 0.000
#&gt; SRR1383364     5  0.4249      0.509 0.000 0.000 0.432 0.000 0.568
#&gt; SRR1383365     3  0.2362      0.837 0.000 0.032 0.916 0.024 0.028
#&gt; SRR1383366     3  0.1914      0.847 0.000 0.032 0.932 0.032 0.004
#&gt; SRR1383367     3  0.1153      0.865 0.000 0.024 0.964 0.008 0.004
#&gt; SRR1383368     3  0.4709      0.650 0.108 0.004 0.784 0.040 0.064
#&gt; SRR1383369     3  0.4911     -0.453 0.000 0.008 0.504 0.012 0.476
#&gt; SRR1383370     3  0.1372      0.863 0.000 0.024 0.956 0.016 0.004
#&gt; SRR1383371     5  0.4249      0.509 0.000 0.000 0.432 0.000 0.568
#&gt; SRR1383372     3  0.0865      0.867 0.000 0.024 0.972 0.004 0.000
#&gt; SRR1383373     3  0.1026      0.866 0.000 0.024 0.968 0.004 0.004
#&gt; SRR1383374     3  0.0963      0.865 0.000 0.036 0.964 0.000 0.000
#&gt; SRR1383375     1  0.5801      0.830 0.620 0.000 0.008 0.116 0.256
#&gt; SRR1383376     2  0.3783      0.700 0.000 0.768 0.004 0.216 0.012
#&gt; SRR1383377     4  0.7303      0.418 0.000 0.316 0.068 0.476 0.140
#&gt; SRR1383378     2  0.5212      0.556 0.000 0.692 0.020 0.228 0.060
#&gt; SRR1383379     4  0.2338      0.711 0.000 0.112 0.000 0.884 0.004
#&gt; SRR1383380     4  0.4141      0.678 0.008 0.064 0.004 0.804 0.120
#&gt; SRR1383381     5  0.6249      0.650 0.000 0.272 0.144 0.012 0.572
#&gt; SRR1383382     1  0.0000      0.778 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1383383     2  0.1612      0.775 0.000 0.948 0.012 0.016 0.024
#&gt; SRR1383385     1  0.5801      0.830 0.620 0.000 0.008 0.116 0.256
#&gt; SRR1383384     2  0.2956      0.766 0.000 0.848 0.004 0.140 0.008
#&gt; SRR1383386     4  0.6808      0.266 0.316 0.056 0.004 0.536 0.088
#&gt; SRR1383387     4  0.4553      0.498 0.000 0.328 0.004 0.652 0.016
#&gt; SRR1383389     2  0.3561      0.704 0.000 0.844 0.060 0.012 0.084
#&gt; SRR1383391     2  0.2873      0.779 0.000 0.860 0.020 0.120 0.000
#&gt; SRR1383388     4  0.3536      0.692 0.008 0.100 0.000 0.840 0.052
#&gt; SRR1383392     2  0.4449      0.678 0.000 0.780 0.024 0.144 0.052
#&gt; SRR1383390     2  0.1891      0.780 0.000 0.936 0.016 0.032 0.016
#&gt; SRR1383394     2  0.3783      0.700 0.000 0.768 0.004 0.216 0.012
#&gt; SRR1383393     1  0.5801      0.830 0.620 0.000 0.008 0.116 0.256
#&gt; SRR1383396     2  0.6845      0.153 0.020 0.500 0.024 0.364 0.092
#&gt; SRR1383395     4  0.7303      0.418 0.000 0.316 0.068 0.476 0.140
#&gt; SRR1383399     5  0.6249      0.650 0.000 0.272 0.144 0.012 0.572
#&gt; SRR1383400     1  0.0000      0.778 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1383397     4  0.2445      0.710 0.000 0.108 0.004 0.884 0.004
#&gt; SRR1383401     2  0.1393      0.773 0.000 0.956 0.012 0.008 0.024
#&gt; SRR1383398     4  0.4141      0.678 0.008 0.064 0.004 0.804 0.120
#&gt; SRR1383402     2  0.2956      0.766 0.000 0.848 0.004 0.140 0.008
#&gt; SRR1383404     4  0.6690      0.363 0.272 0.060 0.004 0.576 0.088
#&gt; SRR1383403     1  0.5801      0.830 0.620 0.000 0.008 0.116 0.256
#&gt; SRR1383405     4  0.4553      0.498 0.000 0.328 0.004 0.652 0.016
#&gt; SRR1383406     4  0.2179      0.710 0.000 0.112 0.000 0.888 0.000
#&gt; SRR1383407     2  0.4408      0.653 0.000 0.784 0.100 0.012 0.104
#&gt; SRR1383408     2  0.1891      0.780 0.000 0.936 0.016 0.032 0.016
#&gt; SRR1383409     2  0.2873      0.779 0.000 0.860 0.020 0.120 0.000
#&gt; SRR1383410     2  0.4208      0.684 0.000 0.788 0.012 0.148 0.052
</code></pre>

<script>
$('#tab-MAD-kmeans-get-classes-4-a').parent().next().next().hide();
$('#tab-MAD-kmeans-get-classes-4-a').click(function(){
  $('#tab-MAD-kmeans-get-classes-4-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-MAD-kmeans-get-classes-5'>
<p><a id='tab-MAD-kmeans-get-classes-5-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 6), get_membership(res, k = 6))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4    p5 p6
#&gt; SRR1383358     3  0.2923      0.841 0.000 0.008 0.856 0.004 0.024 NA
#&gt; SRR1383360     3  0.3142      0.759 0.000 0.000 0.832 0.012 0.024 NA
#&gt; SRR1383359     3  0.5133      0.679 0.000 0.008 0.688 0.016 0.136 NA
#&gt; SRR1383362     1  0.3684      0.757 0.628 0.000 0.000 0.000 0.000 NA
#&gt; SRR1383361     3  0.0603      0.888 0.000 0.016 0.980 0.000 0.004 NA
#&gt; SRR1383363     3  0.0717      0.889 0.000 0.016 0.976 0.000 0.008 NA
#&gt; SRR1383364     5  0.1910      0.799 0.000 0.000 0.108 0.000 0.892 NA
#&gt; SRR1383365     3  0.4775      0.702 0.000 0.008 0.708 0.004 0.136 NA
#&gt; SRR1383366     3  0.2462      0.862 0.000 0.016 0.892 0.008 0.008 NA
#&gt; SRR1383367     3  0.0603      0.888 0.000 0.016 0.980 0.000 0.004 NA
#&gt; SRR1383368     3  0.3280      0.736 0.004 0.000 0.808 0.000 0.028 NA
#&gt; SRR1383369     5  0.4313      0.682 0.000 0.000 0.172 0.004 0.732 NA
#&gt; SRR1383370     3  0.0363      0.887 0.000 0.012 0.988 0.000 0.000 NA
#&gt; SRR1383371     5  0.1910      0.799 0.000 0.000 0.108 0.000 0.892 NA
#&gt; SRR1383372     3  0.0717      0.889 0.000 0.016 0.976 0.000 0.008 NA
#&gt; SRR1383373     3  0.0717      0.889 0.000 0.016 0.976 0.000 0.008 NA
#&gt; SRR1383374     3  0.1785      0.878 0.000 0.016 0.928 0.000 0.008 NA
#&gt; SRR1383375     1  0.1167      0.810 0.960 0.000 0.008 0.020 0.000 NA
#&gt; SRR1383376     2  0.3590      0.717 0.000 0.808 0.000 0.132 0.016 NA
#&gt; SRR1383377     4  0.7056      0.495 0.008 0.168 0.024 0.536 0.068 NA
#&gt; SRR1383378     2  0.6116      0.508 0.004 0.616 0.016 0.140 0.036 NA
#&gt; SRR1383379     4  0.2040      0.721 0.000 0.084 0.004 0.904 0.004 NA
#&gt; SRR1383380     4  0.4242      0.666 0.108 0.032 0.000 0.788 0.012 NA
#&gt; SRR1383381     5  0.5420      0.734 0.004 0.112 0.028 0.016 0.692 NA
#&gt; SRR1383382     1  0.3684      0.757 0.628 0.000 0.000 0.000 0.000 NA
#&gt; SRR1383383     2  0.2306      0.757 0.000 0.888 0.004 0.000 0.016 NA
#&gt; SRR1383385     1  0.1053      0.810 0.964 0.000 0.000 0.020 0.012 NA
#&gt; SRR1383384     2  0.2502      0.767 0.000 0.884 0.000 0.084 0.012 NA
#&gt; SRR1383386     4  0.7266      0.373 0.212 0.060 0.016 0.512 0.024 NA
#&gt; SRR1383387     4  0.4987      0.546 0.000 0.268 0.004 0.652 0.020 NA
#&gt; SRR1383389     2  0.5172      0.642 0.000 0.716 0.060 0.028 0.040 NA
#&gt; SRR1383391     2  0.1788      0.775 0.000 0.916 0.004 0.076 0.000 NA
#&gt; SRR1383388     4  0.4936      0.671 0.024 0.092 0.016 0.756 0.020 NA
#&gt; SRR1383392     2  0.5112      0.652 0.000 0.716 0.012 0.112 0.036 NA
#&gt; SRR1383390     2  0.1716      0.774 0.000 0.932 0.004 0.028 0.000 NA
#&gt; SRR1383394     2  0.3590      0.717 0.000 0.808 0.000 0.132 0.016 NA
#&gt; SRR1383393     1  0.1167      0.810 0.960 0.000 0.008 0.020 0.000 NA
#&gt; SRR1383396     2  0.7534      0.153 0.028 0.436 0.016 0.272 0.048 NA
#&gt; SRR1383395     4  0.7056      0.495 0.008 0.168 0.024 0.536 0.068 NA
#&gt; SRR1383399     5  0.5420      0.734 0.004 0.112 0.028 0.016 0.692 NA
#&gt; SRR1383400     1  0.3684      0.757 0.628 0.000 0.000 0.000 0.000 NA
#&gt; SRR1383397     4  0.2009      0.721 0.000 0.084 0.004 0.904 0.000 NA
#&gt; SRR1383401     2  0.2306      0.757 0.000 0.888 0.004 0.000 0.016 NA
#&gt; SRR1383398     4  0.4242      0.666 0.108 0.032 0.000 0.788 0.012 NA
#&gt; SRR1383402     2  0.2502      0.767 0.000 0.884 0.000 0.084 0.012 NA
#&gt; SRR1383404     4  0.7025      0.467 0.156 0.068 0.016 0.560 0.024 NA
#&gt; SRR1383403     1  0.1053      0.810 0.964 0.000 0.000 0.020 0.012 NA
#&gt; SRR1383405     4  0.4987      0.546 0.000 0.268 0.004 0.652 0.020 NA
#&gt; SRR1383406     4  0.2099      0.721 0.000 0.080 0.004 0.904 0.004 NA
#&gt; SRR1383407     2  0.5590      0.621 0.000 0.680 0.068 0.028 0.052 NA
#&gt; SRR1383408     2  0.1716      0.775 0.000 0.932 0.004 0.028 0.000 NA
#&gt; SRR1383409     2  0.1644      0.775 0.000 0.920 0.004 0.076 0.000 NA
#&gt; SRR1383410     2  0.4951      0.656 0.000 0.720 0.004 0.116 0.036 NA
</code></pre>

<script>
$('#tab-MAD-kmeans-get-classes-5-a').parent().next().next().hide();
$('#tab-MAD-kmeans-get-classes-5-a').click(function(){
  $('#tab-MAD-kmeans-get-classes-5-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>
</div>

Heatmaps for the consensus matrix. It visualizes the probability of two
samples to be in a same group.



<script>
$( function() {
	$( '#tabs-MAD-kmeans-consensus-heatmap' ).tabs();
} );
</script>
<div id='tabs-MAD-kmeans-consensus-heatmap'>
<ul>
<li><a href='#tab-MAD-kmeans-consensus-heatmap-1'>k = 2</a></li>
<li><a href='#tab-MAD-kmeans-consensus-heatmap-2'>k = 3</a></li>
<li><a href='#tab-MAD-kmeans-consensus-heatmap-3'>k = 4</a></li>
<li><a href='#tab-MAD-kmeans-consensus-heatmap-4'>k = 5</a></li>
<li><a href='#tab-MAD-kmeans-consensus-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-MAD-kmeans-consensus-heatmap-1'>
<pre><code class="r">consensus_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-MAD-kmeans-consensus-heatmap-1-1.png" alt="plot of chunk tab-MAD-kmeans-consensus-heatmap-1"/></p>

</div>
<div id='tab-MAD-kmeans-consensus-heatmap-2'>
<pre><code class="r">consensus_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-MAD-kmeans-consensus-heatmap-2-1.png" alt="plot of chunk tab-MAD-kmeans-consensus-heatmap-2"/></p>

</div>
<div id='tab-MAD-kmeans-consensus-heatmap-3'>
<pre><code class="r">consensus_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-MAD-kmeans-consensus-heatmap-3-1.png" alt="plot of chunk tab-MAD-kmeans-consensus-heatmap-3"/></p>

</div>
<div id='tab-MAD-kmeans-consensus-heatmap-4'>
<pre><code class="r">consensus_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-MAD-kmeans-consensus-heatmap-4-1.png" alt="plot of chunk tab-MAD-kmeans-consensus-heatmap-4"/></p>

</div>
<div id='tab-MAD-kmeans-consensus-heatmap-5'>
<pre><code class="r">consensus_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-MAD-kmeans-consensus-heatmap-5-1.png" alt="plot of chunk tab-MAD-kmeans-consensus-heatmap-5"/></p>

</div>
</div>

Heatmaps for the membership of samples in all partitions to see how consistent they are:




<script>
$( function() {
	$( '#tabs-MAD-kmeans-membership-heatmap' ).tabs();
} );
</script>
<div id='tabs-MAD-kmeans-membership-heatmap'>
<ul>
<li><a href='#tab-MAD-kmeans-membership-heatmap-1'>k = 2</a></li>
<li><a href='#tab-MAD-kmeans-membership-heatmap-2'>k = 3</a></li>
<li><a href='#tab-MAD-kmeans-membership-heatmap-3'>k = 4</a></li>
<li><a href='#tab-MAD-kmeans-membership-heatmap-4'>k = 5</a></li>
<li><a href='#tab-MAD-kmeans-membership-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-MAD-kmeans-membership-heatmap-1'>
<pre><code class="r">membership_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-MAD-kmeans-membership-heatmap-1-1.png" alt="plot of chunk tab-MAD-kmeans-membership-heatmap-1"/></p>

</div>
<div id='tab-MAD-kmeans-membership-heatmap-2'>
<pre><code class="r">membership_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-MAD-kmeans-membership-heatmap-2-1.png" alt="plot of chunk tab-MAD-kmeans-membership-heatmap-2"/></p>

</div>
<div id='tab-MAD-kmeans-membership-heatmap-3'>
<pre><code class="r">membership_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-MAD-kmeans-membership-heatmap-3-1.png" alt="plot of chunk tab-MAD-kmeans-membership-heatmap-3"/></p>

</div>
<div id='tab-MAD-kmeans-membership-heatmap-4'>
<pre><code class="r">membership_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-MAD-kmeans-membership-heatmap-4-1.png" alt="plot of chunk tab-MAD-kmeans-membership-heatmap-4"/></p>

</div>
<div id='tab-MAD-kmeans-membership-heatmap-5'>
<pre><code class="r">membership_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-MAD-kmeans-membership-heatmap-5-1.png" alt="plot of chunk tab-MAD-kmeans-membership-heatmap-5"/></p>

</div>
</div>

As soon as we have had the classes for columns, we can look for signatures
which are significantly different between classes which can be candidate marks
for certain classes. Following are the heatmaps for signatures.



Signature heatmaps where rows are scaled:



<script>
$( function() {
	$( '#tabs-MAD-kmeans-get-signatures' ).tabs();
} );
</script>
<div id='tabs-MAD-kmeans-get-signatures'>
<ul>
<li><a href='#tab-MAD-kmeans-get-signatures-1'>k = 2</a></li>
<li><a href='#tab-MAD-kmeans-get-signatures-2'>k = 3</a></li>
<li><a href='#tab-MAD-kmeans-get-signatures-3'>k = 4</a></li>
<li><a href='#tab-MAD-kmeans-get-signatures-4'>k = 5</a></li>
<li><a href='#tab-MAD-kmeans-get-signatures-5'>k = 6</a></li>
</ul>
<div id='tab-MAD-kmeans-get-signatures-1'>
<pre><code class="r">get_signatures(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-MAD-kmeans-get-signatures-1-1.png" alt="plot of chunk tab-MAD-kmeans-get-signatures-1"/></p>

</div>
<div id='tab-MAD-kmeans-get-signatures-2'>
<pre><code class="r">get_signatures(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-MAD-kmeans-get-signatures-2-1.png" alt="plot of chunk tab-MAD-kmeans-get-signatures-2"/></p>

</div>
<div id='tab-MAD-kmeans-get-signatures-3'>
<pre><code class="r">get_signatures(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-MAD-kmeans-get-signatures-3-1.png" alt="plot of chunk tab-MAD-kmeans-get-signatures-3"/></p>

</div>
<div id='tab-MAD-kmeans-get-signatures-4'>
<pre><code class="r">get_signatures(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-MAD-kmeans-get-signatures-4-1.png" alt="plot of chunk tab-MAD-kmeans-get-signatures-4"/></p>

</div>
<div id='tab-MAD-kmeans-get-signatures-5'>
<pre><code class="r">get_signatures(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-MAD-kmeans-get-signatures-5-1.png" alt="plot of chunk tab-MAD-kmeans-get-signatures-5"/></p>

</div>
</div>



Signature heatmaps where rows are not scaled:


<script>
$( function() {
	$( '#tabs-MAD-kmeans-get-signatures-no-scale' ).tabs();
} );
</script>
<div id='tabs-MAD-kmeans-get-signatures-no-scale'>
<ul>
<li><a href='#tab-MAD-kmeans-get-signatures-no-scale-1'>k = 2</a></li>
<li><a href='#tab-MAD-kmeans-get-signatures-no-scale-2'>k = 3</a></li>
<li><a href='#tab-MAD-kmeans-get-signatures-no-scale-3'>k = 4</a></li>
<li><a href='#tab-MAD-kmeans-get-signatures-no-scale-4'>k = 5</a></li>
<li><a href='#tab-MAD-kmeans-get-signatures-no-scale-5'>k = 6</a></li>
</ul>
<div id='tab-MAD-kmeans-get-signatures-no-scale-1'>
<pre><code class="r">get_signatures(res, k = 2, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-MAD-kmeans-get-signatures-no-scale-1-1.png" alt="plot of chunk tab-MAD-kmeans-get-signatures-no-scale-1"/></p>

</div>
<div id='tab-MAD-kmeans-get-signatures-no-scale-2'>
<pre><code class="r">get_signatures(res, k = 3, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-MAD-kmeans-get-signatures-no-scale-2-1.png" alt="plot of chunk tab-MAD-kmeans-get-signatures-no-scale-2"/></p>

</div>
<div id='tab-MAD-kmeans-get-signatures-no-scale-3'>
<pre><code class="r">get_signatures(res, k = 4, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-MAD-kmeans-get-signatures-no-scale-3-1.png" alt="plot of chunk tab-MAD-kmeans-get-signatures-no-scale-3"/></p>

</div>
<div id='tab-MAD-kmeans-get-signatures-no-scale-4'>
<pre><code class="r">get_signatures(res, k = 5, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-MAD-kmeans-get-signatures-no-scale-4-1.png" alt="plot of chunk tab-MAD-kmeans-get-signatures-no-scale-4"/></p>

</div>
<div id='tab-MAD-kmeans-get-signatures-no-scale-5'>
<pre><code class="r">get_signatures(res, k = 6, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-MAD-kmeans-get-signatures-no-scale-5-1.png" alt="plot of chunk tab-MAD-kmeans-get-signatures-no-scale-5"/></p>

</div>
</div>



Compare the overlap of signatures from different k:

```r
compare_signatures(res)
```

![plot of chunk MAD-kmeans-signature_compare](figure_cola/MAD-kmeans-signature_compare-1.png)

`get_signature()` returns a data frame invisibly. TO get the list of signatures, the function
call should be assigned to a variable explicitly. In following code, if `plot` argument is set
to `FALSE`, no heatmap is plotted while only the differential analysis is performed.

```r
# code only for demonstration
tb = get_signature(res, k = ..., plot = FALSE)
```

An example of the output of `tb` is:

```
#>   which_row         fdr    mean_1    mean_2 scaled_mean_1 scaled_mean_2 km
#> 1        38 0.042760348  8.373488  9.131774    -0.5533452     0.5164555  1
#> 2        40 0.018707592  7.106213  8.469186    -0.6173731     0.5762149  1
#> 3        55 0.019134737 10.221463 11.207825    -0.6159697     0.5749050  1
#> 4        59 0.006059896  5.921854  7.869574    -0.6899429     0.6439467  1
#> 5        60 0.018055526  8.928898 10.211722    -0.6204761     0.5791110  1
#> 6        98 0.009384629 15.714769 14.887706     0.6635654    -0.6193277  2
...
```

The columns in `tb` are:

1. `which_row`: row indices corresponding to the input matrix.
2. `fdr`: FDR for the differential test. 
3. `mean_x`: The mean value in group x.
4. `scaled_mean_x`: The mean value in group x after rows are scaled.
5. `km`: Row groups if k-means clustering is applied to rows.



UMAP plot which shows how samples are separated.


<script>
$( function() {
	$( '#tabs-MAD-kmeans-dimension-reduction' ).tabs();
} );
</script>
<div id='tabs-MAD-kmeans-dimension-reduction'>
<ul>
<li><a href='#tab-MAD-kmeans-dimension-reduction-1'>k = 2</a></li>
<li><a href='#tab-MAD-kmeans-dimension-reduction-2'>k = 3</a></li>
<li><a href='#tab-MAD-kmeans-dimension-reduction-3'>k = 4</a></li>
<li><a href='#tab-MAD-kmeans-dimension-reduction-4'>k = 5</a></li>
<li><a href='#tab-MAD-kmeans-dimension-reduction-5'>k = 6</a></li>
</ul>
<div id='tab-MAD-kmeans-dimension-reduction-1'>
<pre><code class="r">dimension_reduction(res, k = 2, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-MAD-kmeans-dimension-reduction-1-1.png" alt="plot of chunk tab-MAD-kmeans-dimension-reduction-1"/></p>

</div>
<div id='tab-MAD-kmeans-dimension-reduction-2'>
<pre><code class="r">dimension_reduction(res, k = 3, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-MAD-kmeans-dimension-reduction-2-1.png" alt="plot of chunk tab-MAD-kmeans-dimension-reduction-2"/></p>

</div>
<div id='tab-MAD-kmeans-dimension-reduction-3'>
<pre><code class="r">dimension_reduction(res, k = 4, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-MAD-kmeans-dimension-reduction-3-1.png" alt="plot of chunk tab-MAD-kmeans-dimension-reduction-3"/></p>

</div>
<div id='tab-MAD-kmeans-dimension-reduction-4'>
<pre><code class="r">dimension_reduction(res, k = 5, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-MAD-kmeans-dimension-reduction-4-1.png" alt="plot of chunk tab-MAD-kmeans-dimension-reduction-4"/></p>

</div>
<div id='tab-MAD-kmeans-dimension-reduction-5'>
<pre><code class="r">dimension_reduction(res, k = 6, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-MAD-kmeans-dimension-reduction-5-1.png" alt="plot of chunk tab-MAD-kmeans-dimension-reduction-5"/></p>

</div>
</div>


Following heatmap shows how subgroups are split when increasing `k`:

```r
collect_classes(res)
```

![plot of chunk MAD-kmeans-collect-classes](figure_cola/MAD-kmeans-collect-classes-1.png)


If matrix rows can be associated to genes, consider to use `functional_enrichment(res,
...)` to perform function enrichment for the signature genes. See [this vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/functional_enrichment.html) for more detailed explanations.


 

---------------------------------------------------




### MAD:skmeans**






The object with results only for a single top-value method and a single partition method 
can be extracted as:

```r
res = res_list["MAD", "skmeans"]
# you can also extract it by
# res = res_list["MAD:skmeans"]
```

A summary of `res` and all the functions that can be applied to it:

```r
res
```

```
#> A 'ConsensusPartition' object with k = 2, 3, 4, 5, 6.
#>   On a matrix with 15680 rows and 53 columns.
#>   Top rows (1000, 2000, 3000, 4000, 5000) are extracted by 'MAD' method.
#>   Subgroups are detected by 'skmeans' method.
#>   Performed in total 1250 partitions by row resampling.
#>   Best k for subgroups seems to be 2.
#> 
#> Following methods can be applied to this 'ConsensusPartition' object:
#>  [1] "cola_report"             "collect_classes"         "collect_plots"          
#>  [4] "collect_stats"           "colnames"                "compare_signatures"     
#>  [7] "consensus_heatmap"       "dimension_reduction"     "functional_enrichment"  
#> [10] "get_anno_col"            "get_anno"                "get_classes"            
#> [13] "get_consensus"           "get_matrix"              "get_membership"         
#> [16] "get_param"               "get_signatures"          "get_stats"              
#> [19] "is_best_k"               "is_stable_k"             "membership_heatmap"     
#> [22] "ncol"                    "nrow"                    "plot_ecdf"              
#> [25] "rownames"                "select_partition_number" "show"                   
#> [28] "suggest_best_k"          "test_to_known_factors"
```

`collect_plots()` function collects all the plots made from `res` for all `k` (number of partitions)
into one single page to provide an easy and fast comparison between different `k`.

```r
collect_plots(res)
```

![plot of chunk MAD-skmeans-collect-plots](figure_cola/MAD-skmeans-collect-plots-1.png)

The plots are:

- The first row: a plot of the ECDF (empirical cumulative distribution
  function) curves of the consensus matrix for each `k` and the heatmap of
  predicted classes for each `k`.
- The second row: heatmaps of the consensus matrix for each `k`.
- The third row: heatmaps of the membership matrix for each `k`.
- The fouth row: heatmaps of the signatures for each `k`.

All the plots in panels can be made by individual functions and they are
plotted later in this section.

`select_partition_number()` produces several plots showing different
statistics for choosing "optimized" `k`. There are following statistics:

- ECDF curves of the consensus matrix for each `k`;
- 1-PAC. [The PAC
  score](https://en.wikipedia.org/wiki/Consensus_clustering#Over-interpretation_potential_of_consensus_clustering)
  measures the proportion of the ambiguous subgrouping.
- Mean silhouette score.
- Concordance. The mean probability of fiting the consensus class ids in all
  partitions.
- Area increased. Denote $A_k$ as the area under the ECDF curve for current
  `k`, the area increased is defined as $A_k - A_{k-1}$.
- Rand index. The percent of pairs of samples that are both in a same cluster
  or both are not in a same cluster in the partition of k and k-1.
- Jaccard index. The ratio of pairs of samples are both in a same cluster in
  the partition of k and k-1 and the pairs of samples are both in a same
  cluster in the partition k or k-1.

The detailed explanations of these statistics can be found in [the _cola_
vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/cola.html#toc_13).

Generally speaking, lower PAC score, higher mean silhouette score or higher
concordance corresponds to better partition. Rand index and Jaccard index
measure how similar the current partition is compared to partition with `k-1`.
If they are too similar, we won't accept `k` is better than `k-1`.

```r
select_partition_number(res)
```

![plot of chunk MAD-skmeans-select-partition-number](figure_cola/MAD-skmeans-select-partition-number-1.png)

The numeric values for all these statistics can be obtained by `get_stats()`.

```r
get_stats(res)
```

```
#>   k 1-PAC mean_silhouette concordance area_increased  Rand Jaccard
#> 2 2 1.000           0.982       0.987         0.4718 0.531   0.531
#> 3 3 0.816           0.912       0.961         0.4364 0.743   0.537
#> 4 4 0.726           0.768       0.871         0.1149 0.839   0.556
#> 5 5 0.843           0.801       0.904         0.0603 0.907   0.651
#> 6 6 0.804           0.715       0.831         0.0389 0.966   0.836
```

`suggest_best_k()` suggests the best $k$ based on these statistics. The rules are as follows:

- All $k$ with Jaccard index larger than 0.95 are removed because increasing
  $k$ does not provide enough extra information. If all $k$ are removed, it is
  marked as no subgroup is detected.
- For all $k$ with 1-PAC score larger than 0.9, the maximal $k$ is taken as
  the best $k$, and other $k$ are marked as optional $k$.
- If it does not fit the second rule. The $k$ with the maximal vote of the
  highest 1-PAC score, highest mean silhouette, and highest concordance is
  taken as the best $k$.

```r
suggest_best_k(res)
```

```
#> [1] 2
```


Following shows the table of the partitions (You need to click the **show/hide
code output** link to see it). The membership matrix (columns with name `p*`)
is inferred by
[`clue::cl_consensus()`](https://www.rdocumentation.org/link/cl_consensus?package=clue)
function with the `SE` method. Basically the value in the membership matrix
represents the probability to belong to a certain group. The finall class
label for an item is determined with the group with highest probability it
belongs to.

In `get_classes()` function, the entropy is calculated from the membership
matrix and the silhouette score is calculated from the consensus matrix.



<script>
$( function() {
	$( '#tabs-MAD-skmeans-get-classes' ).tabs();
} );
</script>
<div id='tabs-MAD-skmeans-get-classes'>
<ul>
<li><a href='#tab-MAD-skmeans-get-classes-1'>k = 2</a></li>
<li><a href='#tab-MAD-skmeans-get-classes-2'>k = 3</a></li>
<li><a href='#tab-MAD-skmeans-get-classes-3'>k = 4</a></li>
<li><a href='#tab-MAD-skmeans-get-classes-4'>k = 5</a></li>
<li><a href='#tab-MAD-skmeans-get-classes-5'>k = 6</a></li>
</ul>

<div id='tab-MAD-skmeans-get-classes-1'>
<p><a id='tab-MAD-skmeans-get-classes-1-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 2), get_membership(res, k = 2))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2
#&gt; SRR1383358     2  0.0376      0.984 0.004 0.996
#&gt; SRR1383360     1  0.2423      0.959 0.960 0.040
#&gt; SRR1383359     2  0.0376      0.984 0.004 0.996
#&gt; SRR1383362     1  0.0000      0.994 1.000 0.000
#&gt; SRR1383361     2  0.0376      0.984 0.004 0.996
#&gt; SRR1383363     2  0.0376      0.984 0.004 0.996
#&gt; SRR1383364     2  0.0376      0.984 0.004 0.996
#&gt; SRR1383365     2  0.0376      0.984 0.004 0.996
#&gt; SRR1383366     2  0.0376      0.984 0.004 0.996
#&gt; SRR1383367     2  0.0376      0.984 0.004 0.996
#&gt; SRR1383368     1  0.2423      0.959 0.960 0.040
#&gt; SRR1383369     2  0.0376      0.984 0.004 0.996
#&gt; SRR1383370     2  0.0376      0.984 0.004 0.996
#&gt; SRR1383371     2  0.0376      0.984 0.004 0.996
#&gt; SRR1383372     2  0.0376      0.984 0.004 0.996
#&gt; SRR1383373     2  0.0376      0.984 0.004 0.996
#&gt; SRR1383374     2  0.0000      0.983 0.000 1.000
#&gt; SRR1383375     1  0.0000      0.994 1.000 0.000
#&gt; SRR1383376     2  0.2423      0.968 0.040 0.960
#&gt; SRR1383377     2  0.1633      0.972 0.024 0.976
#&gt; SRR1383378     1  0.0376      0.993 0.996 0.004
#&gt; SRR1383379     1  0.0376      0.993 0.996 0.004
#&gt; SRR1383380     1  0.0376      0.993 0.996 0.004
#&gt; SRR1383381     2  0.0376      0.984 0.004 0.996
#&gt; SRR1383382     1  0.0000      0.994 1.000 0.000
#&gt; SRR1383383     2  0.0000      0.983 0.000 1.000
#&gt; SRR1383385     1  0.0000      0.994 1.000 0.000
#&gt; SRR1383384     2  0.2423      0.968 0.040 0.960
#&gt; SRR1383386     1  0.0000      0.994 1.000 0.000
#&gt; SRR1383387     2  0.3431      0.950 0.064 0.936
#&gt; SRR1383389     2  0.0000      0.983 0.000 1.000
#&gt; SRR1383391     2  0.2423      0.968 0.040 0.960
#&gt; SRR1383388     1  0.0376      0.993 0.996 0.004
#&gt; SRR1383392     2  0.0000      0.983 0.000 1.000
#&gt; SRR1383390     2  0.2423      0.968 0.040 0.960
#&gt; SRR1383394     2  0.2423      0.968 0.040 0.960
#&gt; SRR1383393     1  0.0000      0.994 1.000 0.000
#&gt; SRR1383396     1  0.0000      0.994 1.000 0.000
#&gt; SRR1383395     2  0.1633      0.972 0.024 0.976
#&gt; SRR1383399     2  0.0376      0.984 0.004 0.996
#&gt; SRR1383400     1  0.0000      0.994 1.000 0.000
#&gt; SRR1383397     1  0.0376      0.993 0.996 0.004
#&gt; SRR1383401     2  0.0000      0.983 0.000 1.000
#&gt; SRR1383398     1  0.0376      0.993 0.996 0.004
#&gt; SRR1383402     2  0.2423      0.968 0.040 0.960
#&gt; SRR1383404     1  0.0000      0.994 1.000 0.000
#&gt; SRR1383403     1  0.0000      0.994 1.000 0.000
#&gt; SRR1383405     2  0.3431      0.950 0.064 0.936
#&gt; SRR1383406     1  0.0376      0.993 0.996 0.004
#&gt; SRR1383407     2  0.0000      0.983 0.000 1.000
#&gt; SRR1383408     2  0.2423      0.968 0.040 0.960
#&gt; SRR1383409     2  0.2423      0.968 0.040 0.960
#&gt; SRR1383410     2  0.0000      0.983 0.000 1.000
</code></pre>

<script>
$('#tab-MAD-skmeans-get-classes-1-a').parent().next().next().hide();
$('#tab-MAD-skmeans-get-classes-1-a').click(function(){
  $('#tab-MAD-skmeans-get-classes-1-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-MAD-skmeans-get-classes-2'>
<p><a id='tab-MAD-skmeans-get-classes-2-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 3), get_membership(res, k = 3))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3
#&gt; SRR1383358     3   0.000      0.924 0.000 0.000 1.000
#&gt; SRR1383360     3   0.603      0.407 0.376 0.000 0.624
#&gt; SRR1383359     3   0.000      0.924 0.000 0.000 1.000
#&gt; SRR1383362     1   0.000      0.964 1.000 0.000 0.000
#&gt; SRR1383361     3   0.000      0.924 0.000 0.000 1.000
#&gt; SRR1383363     3   0.000      0.924 0.000 0.000 1.000
#&gt; SRR1383364     3   0.000      0.924 0.000 0.000 1.000
#&gt; SRR1383365     3   0.000      0.924 0.000 0.000 1.000
#&gt; SRR1383366     3   0.000      0.924 0.000 0.000 1.000
#&gt; SRR1383367     3   0.000      0.924 0.000 0.000 1.000
#&gt; SRR1383368     3   0.623      0.262 0.436 0.000 0.564
#&gt; SRR1383369     3   0.000      0.924 0.000 0.000 1.000
#&gt; SRR1383370     3   0.000      0.924 0.000 0.000 1.000
#&gt; SRR1383371     3   0.000      0.924 0.000 0.000 1.000
#&gt; SRR1383372     3   0.000      0.924 0.000 0.000 1.000
#&gt; SRR1383373     3   0.000      0.924 0.000 0.000 1.000
#&gt; SRR1383374     3   0.000      0.924 0.000 0.000 1.000
#&gt; SRR1383375     1   0.000      0.964 1.000 0.000 0.000
#&gt; SRR1383376     2   0.000      0.978 0.000 1.000 0.000
#&gt; SRR1383377     2   0.216      0.932 0.000 0.936 0.064
#&gt; SRR1383378     1   0.455      0.747 0.800 0.200 0.000
#&gt; SRR1383379     1   0.312      0.893 0.892 0.108 0.000
#&gt; SRR1383380     1   0.000      0.964 1.000 0.000 0.000
#&gt; SRR1383381     3   0.460      0.715 0.000 0.204 0.796
#&gt; SRR1383382     1   0.000      0.964 1.000 0.000 0.000
#&gt; SRR1383383     2   0.000      0.978 0.000 1.000 0.000
#&gt; SRR1383385     1   0.000      0.964 1.000 0.000 0.000
#&gt; SRR1383384     2   0.000      0.978 0.000 1.000 0.000
#&gt; SRR1383386     1   0.000      0.964 1.000 0.000 0.000
#&gt; SRR1383387     2   0.000      0.978 0.000 1.000 0.000
#&gt; SRR1383389     2   0.304      0.890 0.000 0.896 0.104
#&gt; SRR1383391     2   0.000      0.978 0.000 1.000 0.000
#&gt; SRR1383388     1   0.000      0.964 1.000 0.000 0.000
#&gt; SRR1383392     2   0.000      0.978 0.000 1.000 0.000
#&gt; SRR1383390     2   0.000      0.978 0.000 1.000 0.000
#&gt; SRR1383394     2   0.000      0.978 0.000 1.000 0.000
#&gt; SRR1383393     1   0.000      0.964 1.000 0.000 0.000
#&gt; SRR1383396     1   0.000      0.964 1.000 0.000 0.000
#&gt; SRR1383395     2   0.216      0.932 0.000 0.936 0.064
#&gt; SRR1383399     3   0.460      0.715 0.000 0.204 0.796
#&gt; SRR1383400     1   0.000      0.964 1.000 0.000 0.000
#&gt; SRR1383397     1   0.312      0.893 0.892 0.108 0.000
#&gt; SRR1383401     2   0.000      0.978 0.000 1.000 0.000
#&gt; SRR1383398     1   0.000      0.964 1.000 0.000 0.000
#&gt; SRR1383402     2   0.000      0.978 0.000 1.000 0.000
#&gt; SRR1383404     1   0.000      0.964 1.000 0.000 0.000
#&gt; SRR1383403     1   0.000      0.964 1.000 0.000 0.000
#&gt; SRR1383405     2   0.000      0.978 0.000 1.000 0.000
#&gt; SRR1383406     1   0.312      0.893 0.892 0.108 0.000
#&gt; SRR1383407     2   0.319      0.881 0.000 0.888 0.112
#&gt; SRR1383408     2   0.000      0.978 0.000 1.000 0.000
#&gt; SRR1383409     2   0.000      0.978 0.000 1.000 0.000
#&gt; SRR1383410     2   0.000      0.978 0.000 1.000 0.000
</code></pre>

<script>
$('#tab-MAD-skmeans-get-classes-2-a').parent().next().next().hide();
$('#tab-MAD-skmeans-get-classes-2-a').click(function(){
  $('#tab-MAD-skmeans-get-classes-2-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-MAD-skmeans-get-classes-3'>
<p><a id='tab-MAD-skmeans-get-classes-3-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 4), get_membership(res, k = 4))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4
#&gt; SRR1383358     3  0.0188      0.892 0.000 0.000 0.996 0.004
#&gt; SRR1383360     1  0.4977      0.228 0.540 0.000 0.460 0.000
#&gt; SRR1383359     3  0.0336      0.891 0.000 0.000 0.992 0.008
#&gt; SRR1383362     1  0.0000      0.903 1.000 0.000 0.000 0.000
#&gt; SRR1383361     3  0.0000      0.893 0.000 0.000 1.000 0.000
#&gt; SRR1383363     3  0.0000      0.893 0.000 0.000 1.000 0.000
#&gt; SRR1383364     3  0.4040      0.728 0.000 0.000 0.752 0.248
#&gt; SRR1383365     3  0.0188      0.892 0.000 0.000 0.996 0.004
#&gt; SRR1383366     3  0.0000      0.893 0.000 0.000 1.000 0.000
#&gt; SRR1383367     3  0.0000      0.893 0.000 0.000 1.000 0.000
#&gt; SRR1383368     1  0.4431      0.566 0.696 0.000 0.304 0.000
#&gt; SRR1383369     3  0.1211      0.875 0.000 0.000 0.960 0.040
#&gt; SRR1383370     3  0.0000      0.893 0.000 0.000 1.000 0.000
#&gt; SRR1383371     3  0.4040      0.728 0.000 0.000 0.752 0.248
#&gt; SRR1383372     3  0.0000      0.893 0.000 0.000 1.000 0.000
#&gt; SRR1383373     3  0.0000      0.893 0.000 0.000 1.000 0.000
#&gt; SRR1383374     3  0.0000      0.893 0.000 0.000 1.000 0.000
#&gt; SRR1383375     1  0.0000      0.903 1.000 0.000 0.000 0.000
#&gt; SRR1383376     2  0.3172      0.764 0.000 0.840 0.000 0.160
#&gt; SRR1383377     4  0.0188      0.686 0.000 0.004 0.000 0.996
#&gt; SRR1383378     2  0.4843      0.335 0.396 0.604 0.000 0.000
#&gt; SRR1383379     4  0.5416      0.772 0.112 0.148 0.000 0.740
#&gt; SRR1383380     4  0.4356      0.671 0.292 0.000 0.000 0.708
#&gt; SRR1383381     3  0.7979      0.331 0.008 0.284 0.448 0.260
#&gt; SRR1383382     1  0.0000      0.903 1.000 0.000 0.000 0.000
#&gt; SRR1383383     2  0.0817      0.839 0.000 0.976 0.000 0.024
#&gt; SRR1383385     1  0.0000      0.903 1.000 0.000 0.000 0.000
#&gt; SRR1383384     2  0.0921      0.847 0.000 0.972 0.000 0.028
#&gt; SRR1383386     1  0.0000      0.903 1.000 0.000 0.000 0.000
#&gt; SRR1383387     4  0.4134      0.679 0.000 0.260 0.000 0.740
#&gt; SRR1383389     2  0.4283      0.646 0.000 0.740 0.004 0.256
#&gt; SRR1383391     2  0.0817      0.848 0.000 0.976 0.000 0.024
#&gt; SRR1383388     4  0.5167      0.289 0.488 0.004 0.000 0.508
#&gt; SRR1383392     2  0.3219      0.765 0.000 0.836 0.000 0.164
#&gt; SRR1383390     2  0.0188      0.845 0.000 0.996 0.000 0.004
#&gt; SRR1383394     2  0.3172      0.764 0.000 0.840 0.000 0.160
#&gt; SRR1383393     1  0.0000      0.903 1.000 0.000 0.000 0.000
#&gt; SRR1383396     1  0.0188      0.899 0.996 0.004 0.000 0.000
#&gt; SRR1383395     4  0.0188      0.686 0.000 0.004 0.000 0.996
#&gt; SRR1383399     3  0.7979      0.331 0.008 0.284 0.448 0.260
#&gt; SRR1383400     1  0.0000      0.903 1.000 0.000 0.000 0.000
#&gt; SRR1383397     4  0.5267      0.754 0.076 0.184 0.000 0.740
#&gt; SRR1383401     2  0.0817      0.839 0.000 0.976 0.000 0.024
#&gt; SRR1383398     4  0.4356      0.671 0.292 0.000 0.000 0.708
#&gt; SRR1383402     2  0.0921      0.847 0.000 0.972 0.000 0.028
#&gt; SRR1383404     1  0.0000      0.903 1.000 0.000 0.000 0.000
#&gt; SRR1383403     1  0.0000      0.903 1.000 0.000 0.000 0.000
#&gt; SRR1383405     4  0.4134      0.679 0.000 0.260 0.000 0.740
#&gt; SRR1383406     4  0.5423      0.773 0.116 0.144 0.000 0.740
#&gt; SRR1383407     2  0.4422      0.644 0.000 0.736 0.008 0.256
#&gt; SRR1383408     2  0.0188      0.845 0.000 0.996 0.000 0.004
#&gt; SRR1383409     2  0.0817      0.848 0.000 0.976 0.000 0.024
#&gt; SRR1383410     2  0.3219      0.765 0.000 0.836 0.000 0.164
</code></pre>

<script>
$('#tab-MAD-skmeans-get-classes-3-a').parent().next().next().hide();
$('#tab-MAD-skmeans-get-classes-3-a').click(function(){
  $('#tab-MAD-skmeans-get-classes-3-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-MAD-skmeans-get-classes-4'>
<p><a id='tab-MAD-skmeans-get-classes-4-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 5), get_membership(res, k = 5))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4    p5
#&gt; SRR1383358     3  0.0794      0.898 0.000 0.000 0.972 0.000 0.028
#&gt; SRR1383360     3  0.4375      0.389 0.364 0.000 0.628 0.004 0.004
#&gt; SRR1383359     3  0.1197      0.883 0.000 0.000 0.952 0.000 0.048
#&gt; SRR1383362     1  0.0000      0.891 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1383361     3  0.0000      0.911 0.000 0.000 1.000 0.000 0.000
#&gt; SRR1383363     3  0.0162      0.909 0.000 0.000 0.996 0.000 0.004
#&gt; SRR1383364     5  0.2732      0.642 0.000 0.000 0.160 0.000 0.840
#&gt; SRR1383365     3  0.0880      0.895 0.000 0.000 0.968 0.000 0.032
#&gt; SRR1383366     3  0.0000      0.911 0.000 0.000 1.000 0.000 0.000
#&gt; SRR1383367     3  0.0000      0.911 0.000 0.000 1.000 0.000 0.000
#&gt; SRR1383368     1  0.3662      0.616 0.744 0.000 0.252 0.000 0.004
#&gt; SRR1383369     3  0.4273      0.233 0.000 0.000 0.552 0.000 0.448
#&gt; SRR1383370     3  0.0000      0.911 0.000 0.000 1.000 0.000 0.000
#&gt; SRR1383371     5  0.2929      0.619 0.000 0.000 0.180 0.000 0.820
#&gt; SRR1383372     3  0.0000      0.911 0.000 0.000 1.000 0.000 0.000
#&gt; SRR1383373     3  0.0000      0.911 0.000 0.000 1.000 0.000 0.000
#&gt; SRR1383374     3  0.0000      0.911 0.000 0.000 1.000 0.000 0.000
#&gt; SRR1383375     1  0.0609      0.891 0.980 0.000 0.000 0.020 0.000
#&gt; SRR1383376     2  0.1282      0.933 0.000 0.952 0.000 0.044 0.004
#&gt; SRR1383377     4  0.3696      0.706 0.000 0.016 0.000 0.772 0.212
#&gt; SRR1383378     1  0.6176      0.261 0.540 0.288 0.000 0.000 0.172
#&gt; SRR1383379     4  0.1300      0.850 0.016 0.028 0.000 0.956 0.000
#&gt; SRR1383380     4  0.1357      0.841 0.048 0.000 0.000 0.948 0.004
#&gt; SRR1383381     5  0.0865      0.694 0.004 0.024 0.000 0.000 0.972
#&gt; SRR1383382     1  0.0000      0.891 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1383383     2  0.1908      0.895 0.000 0.908 0.000 0.000 0.092
#&gt; SRR1383385     1  0.1205      0.885 0.956 0.000 0.000 0.040 0.004
#&gt; SRR1383384     2  0.0404      0.948 0.000 0.988 0.000 0.012 0.000
#&gt; SRR1383386     1  0.0566      0.889 0.984 0.000 0.000 0.012 0.004
#&gt; SRR1383387     4  0.2690      0.781 0.000 0.156 0.000 0.844 0.000
#&gt; SRR1383389     5  0.4997      0.308 0.000 0.404 0.008 0.020 0.568
#&gt; SRR1383391     2  0.0579      0.948 0.000 0.984 0.000 0.008 0.008
#&gt; SRR1383388     4  0.3928      0.549 0.296 0.000 0.000 0.700 0.004
#&gt; SRR1383392     2  0.1668      0.930 0.000 0.940 0.000 0.032 0.028
#&gt; SRR1383390     2  0.1043      0.934 0.000 0.960 0.000 0.000 0.040
#&gt; SRR1383394     2  0.1282      0.933 0.000 0.952 0.000 0.044 0.004
#&gt; SRR1383393     1  0.0955      0.889 0.968 0.000 0.000 0.028 0.004
#&gt; SRR1383396     1  0.2848      0.766 0.840 0.004 0.000 0.000 0.156
#&gt; SRR1383395     4  0.3696      0.706 0.000 0.016 0.000 0.772 0.212
#&gt; SRR1383399     5  0.0865      0.694 0.004 0.024 0.000 0.000 0.972
#&gt; SRR1383400     1  0.0000      0.891 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1383397     4  0.1082      0.848 0.008 0.028 0.000 0.964 0.000
#&gt; SRR1383401     2  0.1908      0.895 0.000 0.908 0.000 0.000 0.092
#&gt; SRR1383398     4  0.1357      0.841 0.048 0.000 0.000 0.948 0.004
#&gt; SRR1383402     2  0.0404      0.948 0.000 0.988 0.000 0.012 0.000
#&gt; SRR1383404     1  0.1041      0.882 0.964 0.000 0.000 0.032 0.004
#&gt; SRR1383403     1  0.1282      0.883 0.952 0.000 0.000 0.044 0.004
#&gt; SRR1383405     4  0.2648      0.785 0.000 0.152 0.000 0.848 0.000
#&gt; SRR1383406     4  0.1117      0.849 0.020 0.016 0.000 0.964 0.000
#&gt; SRR1383407     5  0.5144      0.343 0.000 0.384 0.016 0.020 0.580
#&gt; SRR1383408     2  0.0794      0.940 0.000 0.972 0.000 0.000 0.028
#&gt; SRR1383409     2  0.0579      0.948 0.000 0.984 0.000 0.008 0.008
#&gt; SRR1383410     2  0.1579      0.931 0.000 0.944 0.000 0.032 0.024
</code></pre>

<script>
$('#tab-MAD-skmeans-get-classes-4-a').parent().next().next().hide();
$('#tab-MAD-skmeans-get-classes-4-a').click(function(){
  $('#tab-MAD-skmeans-get-classes-4-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-MAD-skmeans-get-classes-5'>
<p><a id='tab-MAD-skmeans-get-classes-5-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 6), get_membership(res, k = 6))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4    p5    p6
#&gt; SRR1383358     3  0.1713      0.896 0.000 0.000 0.928 0.000 0.044 0.028
#&gt; SRR1383360     3  0.4672      0.338 0.348 0.000 0.596 0.000 0.000 0.056
#&gt; SRR1383359     3  0.2784      0.817 0.000 0.000 0.848 0.000 0.124 0.028
#&gt; SRR1383362     1  0.0146      0.838 0.996 0.000 0.000 0.000 0.000 0.004
#&gt; SRR1383361     3  0.0458      0.918 0.000 0.000 0.984 0.000 0.000 0.016
#&gt; SRR1383363     3  0.0777      0.909 0.000 0.000 0.972 0.000 0.024 0.004
#&gt; SRR1383364     5  0.0865      0.815 0.000 0.000 0.036 0.000 0.964 0.000
#&gt; SRR1383365     3  0.1970      0.884 0.000 0.000 0.912 0.000 0.060 0.028
#&gt; SRR1383366     3  0.1010      0.915 0.000 0.000 0.960 0.000 0.004 0.036
#&gt; SRR1383367     3  0.0260      0.916 0.000 0.000 0.992 0.000 0.000 0.008
#&gt; SRR1383368     1  0.4101      0.492 0.664 0.000 0.308 0.000 0.000 0.028
#&gt; SRR1383369     5  0.3816      0.498 0.000 0.000 0.296 0.000 0.688 0.016
#&gt; SRR1383370     3  0.0260      0.916 0.000 0.000 0.992 0.000 0.000 0.008
#&gt; SRR1383371     5  0.1010      0.816 0.000 0.000 0.036 0.000 0.960 0.004
#&gt; SRR1383372     3  0.0000      0.918 0.000 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1383373     3  0.0000      0.918 0.000 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1383374     3  0.0713      0.916 0.000 0.000 0.972 0.000 0.000 0.028
#&gt; SRR1383375     1  0.2723      0.823 0.856 0.000 0.000 0.020 0.004 0.120
#&gt; SRR1383376     2  0.3344      0.670 0.000 0.804 0.000 0.044 0.000 0.152
#&gt; SRR1383377     4  0.5115      0.385 0.000 0.000 0.000 0.460 0.080 0.460
#&gt; SRR1383378     2  0.6896     -0.331 0.244 0.388 0.000 0.004 0.044 0.320
#&gt; SRR1383379     4  0.0551      0.747 0.004 0.008 0.000 0.984 0.000 0.004
#&gt; SRR1383380     4  0.3037      0.708 0.016 0.000 0.000 0.808 0.000 0.176
#&gt; SRR1383381     5  0.0790      0.790 0.000 0.000 0.000 0.000 0.968 0.032
#&gt; SRR1383382     1  0.0000      0.838 1.000 0.000 0.000 0.000 0.000 0.000
#&gt; SRR1383383     2  0.2726      0.648 0.000 0.856 0.000 0.000 0.032 0.112
#&gt; SRR1383385     1  0.3242      0.805 0.816 0.000 0.000 0.032 0.004 0.148
#&gt; SRR1383384     2  0.1219      0.725 0.000 0.948 0.000 0.004 0.000 0.048
#&gt; SRR1383386     1  0.1720      0.819 0.928 0.000 0.000 0.040 0.000 0.032
#&gt; SRR1383387     4  0.4030      0.657 0.000 0.080 0.000 0.748 0.000 0.172
#&gt; SRR1383389     6  0.5771      0.948 0.000 0.248 0.000 0.000 0.244 0.508
#&gt; SRR1383391     2  0.1257      0.720 0.000 0.952 0.000 0.028 0.000 0.020
#&gt; SRR1383388     4  0.3790      0.615 0.156 0.000 0.000 0.772 0.000 0.072
#&gt; SRR1383392     2  0.4076      0.393 0.000 0.592 0.000 0.012 0.000 0.396
#&gt; SRR1383390     2  0.1957      0.655 0.000 0.888 0.000 0.000 0.000 0.112
#&gt; SRR1383394     2  0.3344      0.670 0.000 0.804 0.000 0.044 0.000 0.152
#&gt; SRR1383393     1  0.2723      0.823 0.856 0.000 0.000 0.020 0.004 0.120
#&gt; SRR1383396     1  0.4683      0.476 0.628 0.000 0.000 0.004 0.056 0.312
#&gt; SRR1383395     4  0.5075      0.392 0.000 0.000 0.000 0.464 0.076 0.460
#&gt; SRR1383399     5  0.0790      0.790 0.000 0.000 0.000 0.000 0.968 0.032
#&gt; SRR1383400     1  0.0000      0.838 1.000 0.000 0.000 0.000 0.000 0.000
#&gt; SRR1383397     4  0.0520      0.747 0.000 0.008 0.000 0.984 0.000 0.008
#&gt; SRR1383401     2  0.3426      0.621 0.000 0.808 0.000 0.000 0.068 0.124
#&gt; SRR1383398     4  0.3037      0.708 0.016 0.000 0.000 0.808 0.000 0.176
#&gt; SRR1383402     2  0.1462      0.725 0.000 0.936 0.000 0.008 0.000 0.056
#&gt; SRR1383404     1  0.2164      0.806 0.900 0.000 0.000 0.068 0.000 0.032
#&gt; SRR1383403     1  0.3242      0.805 0.816 0.000 0.000 0.032 0.004 0.148
#&gt; SRR1383405     4  0.4030      0.657 0.000 0.080 0.000 0.748 0.000 0.172
#&gt; SRR1383406     4  0.0260      0.747 0.000 0.000 0.000 0.992 0.000 0.008
#&gt; SRR1383407     6  0.5742      0.946 0.000 0.220 0.000 0.000 0.268 0.512
#&gt; SRR1383408     2  0.1204      0.696 0.000 0.944 0.000 0.000 0.000 0.056
#&gt; SRR1383409     2  0.1168      0.721 0.000 0.956 0.000 0.028 0.000 0.016
#&gt; SRR1383410     2  0.4057      0.408 0.000 0.600 0.000 0.012 0.000 0.388
</code></pre>

<script>
$('#tab-MAD-skmeans-get-classes-5-a').parent().next().next().hide();
$('#tab-MAD-skmeans-get-classes-5-a').click(function(){
  $('#tab-MAD-skmeans-get-classes-5-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>
</div>

Heatmaps for the consensus matrix. It visualizes the probability of two
samples to be in a same group.



<script>
$( function() {
	$( '#tabs-MAD-skmeans-consensus-heatmap' ).tabs();
} );
</script>
<div id='tabs-MAD-skmeans-consensus-heatmap'>
<ul>
<li><a href='#tab-MAD-skmeans-consensus-heatmap-1'>k = 2</a></li>
<li><a href='#tab-MAD-skmeans-consensus-heatmap-2'>k = 3</a></li>
<li><a href='#tab-MAD-skmeans-consensus-heatmap-3'>k = 4</a></li>
<li><a href='#tab-MAD-skmeans-consensus-heatmap-4'>k = 5</a></li>
<li><a href='#tab-MAD-skmeans-consensus-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-MAD-skmeans-consensus-heatmap-1'>
<pre><code class="r">consensus_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-MAD-skmeans-consensus-heatmap-1-1.png" alt="plot of chunk tab-MAD-skmeans-consensus-heatmap-1"/></p>

</div>
<div id='tab-MAD-skmeans-consensus-heatmap-2'>
<pre><code class="r">consensus_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-MAD-skmeans-consensus-heatmap-2-1.png" alt="plot of chunk tab-MAD-skmeans-consensus-heatmap-2"/></p>

</div>
<div id='tab-MAD-skmeans-consensus-heatmap-3'>
<pre><code class="r">consensus_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-MAD-skmeans-consensus-heatmap-3-1.png" alt="plot of chunk tab-MAD-skmeans-consensus-heatmap-3"/></p>

</div>
<div id='tab-MAD-skmeans-consensus-heatmap-4'>
<pre><code class="r">consensus_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-MAD-skmeans-consensus-heatmap-4-1.png" alt="plot of chunk tab-MAD-skmeans-consensus-heatmap-4"/></p>

</div>
<div id='tab-MAD-skmeans-consensus-heatmap-5'>
<pre><code class="r">consensus_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-MAD-skmeans-consensus-heatmap-5-1.png" alt="plot of chunk tab-MAD-skmeans-consensus-heatmap-5"/></p>

</div>
</div>

Heatmaps for the membership of samples in all partitions to see how consistent they are:




<script>
$( function() {
	$( '#tabs-MAD-skmeans-membership-heatmap' ).tabs();
} );
</script>
<div id='tabs-MAD-skmeans-membership-heatmap'>
<ul>
<li><a href='#tab-MAD-skmeans-membership-heatmap-1'>k = 2</a></li>
<li><a href='#tab-MAD-skmeans-membership-heatmap-2'>k = 3</a></li>
<li><a href='#tab-MAD-skmeans-membership-heatmap-3'>k = 4</a></li>
<li><a href='#tab-MAD-skmeans-membership-heatmap-4'>k = 5</a></li>
<li><a href='#tab-MAD-skmeans-membership-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-MAD-skmeans-membership-heatmap-1'>
<pre><code class="r">membership_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-MAD-skmeans-membership-heatmap-1-1.png" alt="plot of chunk tab-MAD-skmeans-membership-heatmap-1"/></p>

</div>
<div id='tab-MAD-skmeans-membership-heatmap-2'>
<pre><code class="r">membership_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-MAD-skmeans-membership-heatmap-2-1.png" alt="plot of chunk tab-MAD-skmeans-membership-heatmap-2"/></p>

</div>
<div id='tab-MAD-skmeans-membership-heatmap-3'>
<pre><code class="r">membership_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-MAD-skmeans-membership-heatmap-3-1.png" alt="plot of chunk tab-MAD-skmeans-membership-heatmap-3"/></p>

</div>
<div id='tab-MAD-skmeans-membership-heatmap-4'>
<pre><code class="r">membership_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-MAD-skmeans-membership-heatmap-4-1.png" alt="plot of chunk tab-MAD-skmeans-membership-heatmap-4"/></p>

</div>
<div id='tab-MAD-skmeans-membership-heatmap-5'>
<pre><code class="r">membership_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-MAD-skmeans-membership-heatmap-5-1.png" alt="plot of chunk tab-MAD-skmeans-membership-heatmap-5"/></p>

</div>
</div>

As soon as we have had the classes for columns, we can look for signatures
which are significantly different between classes which can be candidate marks
for certain classes. Following are the heatmaps for signatures.



Signature heatmaps where rows are scaled:



<script>
$( function() {
	$( '#tabs-MAD-skmeans-get-signatures' ).tabs();
} );
</script>
<div id='tabs-MAD-skmeans-get-signatures'>
<ul>
<li><a href='#tab-MAD-skmeans-get-signatures-1'>k = 2</a></li>
<li><a href='#tab-MAD-skmeans-get-signatures-2'>k = 3</a></li>
<li><a href='#tab-MAD-skmeans-get-signatures-3'>k = 4</a></li>
<li><a href='#tab-MAD-skmeans-get-signatures-4'>k = 5</a></li>
<li><a href='#tab-MAD-skmeans-get-signatures-5'>k = 6</a></li>
</ul>
<div id='tab-MAD-skmeans-get-signatures-1'>
<pre><code class="r">get_signatures(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-MAD-skmeans-get-signatures-1-1.png" alt="plot of chunk tab-MAD-skmeans-get-signatures-1"/></p>

</div>
<div id='tab-MAD-skmeans-get-signatures-2'>
<pre><code class="r">get_signatures(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-MAD-skmeans-get-signatures-2-1.png" alt="plot of chunk tab-MAD-skmeans-get-signatures-2"/></p>

</div>
<div id='tab-MAD-skmeans-get-signatures-3'>
<pre><code class="r">get_signatures(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-MAD-skmeans-get-signatures-3-1.png" alt="plot of chunk tab-MAD-skmeans-get-signatures-3"/></p>

</div>
<div id='tab-MAD-skmeans-get-signatures-4'>
<pre><code class="r">get_signatures(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-MAD-skmeans-get-signatures-4-1.png" alt="plot of chunk tab-MAD-skmeans-get-signatures-4"/></p>

</div>
<div id='tab-MAD-skmeans-get-signatures-5'>
<pre><code class="r">get_signatures(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-MAD-skmeans-get-signatures-5-1.png" alt="plot of chunk tab-MAD-skmeans-get-signatures-5"/></p>

</div>
</div>



Signature heatmaps where rows are not scaled:


<script>
$( function() {
	$( '#tabs-MAD-skmeans-get-signatures-no-scale' ).tabs();
} );
</script>
<div id='tabs-MAD-skmeans-get-signatures-no-scale'>
<ul>
<li><a href='#tab-MAD-skmeans-get-signatures-no-scale-1'>k = 2</a></li>
<li><a href='#tab-MAD-skmeans-get-signatures-no-scale-2'>k = 3</a></li>
<li><a href='#tab-MAD-skmeans-get-signatures-no-scale-3'>k = 4</a></li>
<li><a href='#tab-MAD-skmeans-get-signatures-no-scale-4'>k = 5</a></li>
<li><a href='#tab-MAD-skmeans-get-signatures-no-scale-5'>k = 6</a></li>
</ul>
<div id='tab-MAD-skmeans-get-signatures-no-scale-1'>
<pre><code class="r">get_signatures(res, k = 2, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-MAD-skmeans-get-signatures-no-scale-1-1.png" alt="plot of chunk tab-MAD-skmeans-get-signatures-no-scale-1"/></p>

</div>
<div id='tab-MAD-skmeans-get-signatures-no-scale-2'>
<pre><code class="r">get_signatures(res, k = 3, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-MAD-skmeans-get-signatures-no-scale-2-1.png" alt="plot of chunk tab-MAD-skmeans-get-signatures-no-scale-2"/></p>

</div>
<div id='tab-MAD-skmeans-get-signatures-no-scale-3'>
<pre><code class="r">get_signatures(res, k = 4, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-MAD-skmeans-get-signatures-no-scale-3-1.png" alt="plot of chunk tab-MAD-skmeans-get-signatures-no-scale-3"/></p>

</div>
<div id='tab-MAD-skmeans-get-signatures-no-scale-4'>
<pre><code class="r">get_signatures(res, k = 5, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-MAD-skmeans-get-signatures-no-scale-4-1.png" alt="plot of chunk tab-MAD-skmeans-get-signatures-no-scale-4"/></p>

</div>
<div id='tab-MAD-skmeans-get-signatures-no-scale-5'>
<pre><code class="r">get_signatures(res, k = 6, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-MAD-skmeans-get-signatures-no-scale-5-1.png" alt="plot of chunk tab-MAD-skmeans-get-signatures-no-scale-5"/></p>

</div>
</div>



Compare the overlap of signatures from different k:

```r
compare_signatures(res)
```

![plot of chunk MAD-skmeans-signature_compare](figure_cola/MAD-skmeans-signature_compare-1.png)

`get_signature()` returns a data frame invisibly. TO get the list of signatures, the function
call should be assigned to a variable explicitly. In following code, if `plot` argument is set
to `FALSE`, no heatmap is plotted while only the differential analysis is performed.

```r
# code only for demonstration
tb = get_signature(res, k = ..., plot = FALSE)
```

An example of the output of `tb` is:

```
#>   which_row         fdr    mean_1    mean_2 scaled_mean_1 scaled_mean_2 km
#> 1        38 0.042760348  8.373488  9.131774    -0.5533452     0.5164555  1
#> 2        40 0.018707592  7.106213  8.469186    -0.6173731     0.5762149  1
#> 3        55 0.019134737 10.221463 11.207825    -0.6159697     0.5749050  1
#> 4        59 0.006059896  5.921854  7.869574    -0.6899429     0.6439467  1
#> 5        60 0.018055526  8.928898 10.211722    -0.6204761     0.5791110  1
#> 6        98 0.009384629 15.714769 14.887706     0.6635654    -0.6193277  2
...
```

The columns in `tb` are:

1. `which_row`: row indices corresponding to the input matrix.
2. `fdr`: FDR for the differential test. 
3. `mean_x`: The mean value in group x.
4. `scaled_mean_x`: The mean value in group x after rows are scaled.
5. `km`: Row groups if k-means clustering is applied to rows.



UMAP plot which shows how samples are separated.


<script>
$( function() {
	$( '#tabs-MAD-skmeans-dimension-reduction' ).tabs();
} );
</script>
<div id='tabs-MAD-skmeans-dimension-reduction'>
<ul>
<li><a href='#tab-MAD-skmeans-dimension-reduction-1'>k = 2</a></li>
<li><a href='#tab-MAD-skmeans-dimension-reduction-2'>k = 3</a></li>
<li><a href='#tab-MAD-skmeans-dimension-reduction-3'>k = 4</a></li>
<li><a href='#tab-MAD-skmeans-dimension-reduction-4'>k = 5</a></li>
<li><a href='#tab-MAD-skmeans-dimension-reduction-5'>k = 6</a></li>
</ul>
<div id='tab-MAD-skmeans-dimension-reduction-1'>
<pre><code class="r">dimension_reduction(res, k = 2, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-MAD-skmeans-dimension-reduction-1-1.png" alt="plot of chunk tab-MAD-skmeans-dimension-reduction-1"/></p>

</div>
<div id='tab-MAD-skmeans-dimension-reduction-2'>
<pre><code class="r">dimension_reduction(res, k = 3, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-MAD-skmeans-dimension-reduction-2-1.png" alt="plot of chunk tab-MAD-skmeans-dimension-reduction-2"/></p>

</div>
<div id='tab-MAD-skmeans-dimension-reduction-3'>
<pre><code class="r">dimension_reduction(res, k = 4, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-MAD-skmeans-dimension-reduction-3-1.png" alt="plot of chunk tab-MAD-skmeans-dimension-reduction-3"/></p>

</div>
<div id='tab-MAD-skmeans-dimension-reduction-4'>
<pre><code class="r">dimension_reduction(res, k = 5, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-MAD-skmeans-dimension-reduction-4-1.png" alt="plot of chunk tab-MAD-skmeans-dimension-reduction-4"/></p>

</div>
<div id='tab-MAD-skmeans-dimension-reduction-5'>
<pre><code class="r">dimension_reduction(res, k = 6, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-MAD-skmeans-dimension-reduction-5-1.png" alt="plot of chunk tab-MAD-skmeans-dimension-reduction-5"/></p>

</div>
</div>


Following heatmap shows how subgroups are split when increasing `k`:

```r
collect_classes(res)
```

![plot of chunk MAD-skmeans-collect-classes](figure_cola/MAD-skmeans-collect-classes-1.png)


If matrix rows can be associated to genes, consider to use `functional_enrichment(res,
...)` to perform function enrichment for the signature genes. See [this vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/functional_enrichment.html) for more detailed explanations.


 

---------------------------------------------------




### MAD:pam






The object with results only for a single top-value method and a single partition method 
can be extracted as:

```r
res = res_list["MAD", "pam"]
# you can also extract it by
# res = res_list["MAD:pam"]
```

A summary of `res` and all the functions that can be applied to it:

```r
res
```

```
#> A 'ConsensusPartition' object with k = 2, 3, 4, 5, 6.
#>   On a matrix with 15680 rows and 53 columns.
#>   Top rows (1000, 2000, 3000, 4000, 5000) are extracted by 'MAD' method.
#>   Subgroups are detected by 'pam' method.
#>   Performed in total 1250 partitions by row resampling.
#>   Best k for subgroups seems to be 3.
#> 
#> Following methods can be applied to this 'ConsensusPartition' object:
#>  [1] "cola_report"             "collect_classes"         "collect_plots"          
#>  [4] "collect_stats"           "colnames"                "compare_signatures"     
#>  [7] "consensus_heatmap"       "dimension_reduction"     "functional_enrichment"  
#> [10] "get_anno_col"            "get_anno"                "get_classes"            
#> [13] "get_consensus"           "get_matrix"              "get_membership"         
#> [16] "get_param"               "get_signatures"          "get_stats"              
#> [19] "is_best_k"               "is_stable_k"             "membership_heatmap"     
#> [22] "ncol"                    "nrow"                    "plot_ecdf"              
#> [25] "rownames"                "select_partition_number" "show"                   
#> [28] "suggest_best_k"          "test_to_known_factors"
```

`collect_plots()` function collects all the plots made from `res` for all `k` (number of partitions)
into one single page to provide an easy and fast comparison between different `k`.

```r
collect_plots(res)
```

![plot of chunk MAD-pam-collect-plots](figure_cola/MAD-pam-collect-plots-1.png)

The plots are:

- The first row: a plot of the ECDF (empirical cumulative distribution
  function) curves of the consensus matrix for each `k` and the heatmap of
  predicted classes for each `k`.
- The second row: heatmaps of the consensus matrix for each `k`.
- The third row: heatmaps of the membership matrix for each `k`.
- The fouth row: heatmaps of the signatures for each `k`.

All the plots in panels can be made by individual functions and they are
plotted later in this section.

`select_partition_number()` produces several plots showing different
statistics for choosing "optimized" `k`. There are following statistics:

- ECDF curves of the consensus matrix for each `k`;
- 1-PAC. [The PAC
  score](https://en.wikipedia.org/wiki/Consensus_clustering#Over-interpretation_potential_of_consensus_clustering)
  measures the proportion of the ambiguous subgrouping.
- Mean silhouette score.
- Concordance. The mean probability of fiting the consensus class ids in all
  partitions.
- Area increased. Denote $A_k$ as the area under the ECDF curve for current
  `k`, the area increased is defined as $A_k - A_{k-1}$.
- Rand index. The percent of pairs of samples that are both in a same cluster
  or both are not in a same cluster in the partition of k and k-1.
- Jaccard index. The ratio of pairs of samples are both in a same cluster in
  the partition of k and k-1 and the pairs of samples are both in a same
  cluster in the partition k or k-1.

The detailed explanations of these statistics can be found in [the _cola_
vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/cola.html#toc_13).

Generally speaking, lower PAC score, higher mean silhouette score or higher
concordance corresponds to better partition. Rand index and Jaccard index
measure how similar the current partition is compared to partition with `k-1`.
If they are too similar, we won't accept `k` is better than `k-1`.

```r
select_partition_number(res)
```

![plot of chunk MAD-pam-select-partition-number](figure_cola/MAD-pam-select-partition-number-1.png)

The numeric values for all these statistics can be obtained by `get_stats()`.

```r
get_stats(res)
```

```
#>   k 1-PAC mean_silhouette concordance area_increased  Rand Jaccard
#> 2 2 0.418           0.606       0.797         0.4530 0.505   0.505
#> 3 3 0.833           0.889       0.939         0.4695 0.704   0.478
#> 4 4 0.824           0.803       0.914         0.1142 0.866   0.631
#> 5 5 0.785           0.648       0.822         0.0357 0.950   0.818
#> 6 6 0.891           0.747       0.883         0.0337 0.954   0.811
```

`suggest_best_k()` suggests the best $k$ based on these statistics. The rules are as follows:

- All $k$ with Jaccard index larger than 0.95 are removed because increasing
  $k$ does not provide enough extra information. If all $k$ are removed, it is
  marked as no subgroup is detected.
- For all $k$ with 1-PAC score larger than 0.9, the maximal $k$ is taken as
  the best $k$, and other $k$ are marked as optional $k$.
- If it does not fit the second rule. The $k$ with the maximal vote of the
  highest 1-PAC score, highest mean silhouette, and highest concordance is
  taken as the best $k$.

```r
suggest_best_k(res)
```

```
#> [1] 3
```


Following shows the table of the partitions (You need to click the **show/hide
code output** link to see it). The membership matrix (columns with name `p*`)
is inferred by
[`clue::cl_consensus()`](https://www.rdocumentation.org/link/cl_consensus?package=clue)
function with the `SE` method. Basically the value in the membership matrix
represents the probability to belong to a certain group. The finall class
label for an item is determined with the group with highest probability it
belongs to.

In `get_classes()` function, the entropy is calculated from the membership
matrix and the silhouette score is calculated from the consensus matrix.



<script>
$( function() {
	$( '#tabs-MAD-pam-get-classes' ).tabs();
} );
</script>
<div id='tabs-MAD-pam-get-classes'>
<ul>
<li><a href='#tab-MAD-pam-get-classes-1'>k = 2</a></li>
<li><a href='#tab-MAD-pam-get-classes-2'>k = 3</a></li>
<li><a href='#tab-MAD-pam-get-classes-3'>k = 4</a></li>
<li><a href='#tab-MAD-pam-get-classes-4'>k = 5</a></li>
<li><a href='#tab-MAD-pam-get-classes-5'>k = 6</a></li>
</ul>

<div id='tab-MAD-pam-get-classes-1'>
<p><a id='tab-MAD-pam-get-classes-1-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 2), get_membership(res, k = 2))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2
#&gt; SRR1383358     2   0.000     0.8812 0.000 1.000
#&gt; SRR1383360     2   0.998     0.1217 0.472 0.528
#&gt; SRR1383359     2   0.000     0.8812 0.000 1.000
#&gt; SRR1383362     1   0.981    -0.0295 0.580 0.420
#&gt; SRR1383361     2   0.000     0.8812 0.000 1.000
#&gt; SRR1383363     2   0.000     0.8812 0.000 1.000
#&gt; SRR1383364     2   0.416     0.7913 0.084 0.916
#&gt; SRR1383365     2   0.000     0.8812 0.000 1.000
#&gt; SRR1383366     2   0.000     0.8812 0.000 1.000
#&gt; SRR1383367     2   0.000     0.8812 0.000 1.000
#&gt; SRR1383368     1   0.999    -0.1294 0.516 0.484
#&gt; SRR1383369     2   0.000     0.8812 0.000 1.000
#&gt; SRR1383370     2   0.000     0.8812 0.000 1.000
#&gt; SRR1383371     2   0.000     0.8812 0.000 1.000
#&gt; SRR1383372     2   0.000     0.8812 0.000 1.000
#&gt; SRR1383373     2   0.000     0.8812 0.000 1.000
#&gt; SRR1383374     2   0.000     0.8812 0.000 1.000
#&gt; SRR1383375     1   0.000     0.5660 1.000 0.000
#&gt; SRR1383376     1   0.997     0.5333 0.532 0.468
#&gt; SRR1383377     2   0.574     0.7089 0.136 0.864
#&gt; SRR1383378     1   0.767     0.5498 0.776 0.224
#&gt; SRR1383379     1   0.595     0.4470 0.856 0.144
#&gt; SRR1383380     1   0.997     0.5333 0.532 0.468
#&gt; SRR1383381     1   0.997     0.5333 0.532 0.468
#&gt; SRR1383382     1   0.000     0.5660 1.000 0.000
#&gt; SRR1383383     1   0.997     0.5333 0.532 0.468
#&gt; SRR1383385     1   0.000     0.5660 1.000 0.000
#&gt; SRR1383384     1   0.997     0.5333 0.532 0.468
#&gt; SRR1383386     1   0.000     0.5660 1.000 0.000
#&gt; SRR1383387     1   0.997     0.5333 0.532 0.468
#&gt; SRR1383389     1   0.997     0.5333 0.532 0.468
#&gt; SRR1383391     1   0.997     0.5333 0.532 0.468
#&gt; SRR1383388     1   0.000     0.5660 1.000 0.000
#&gt; SRR1383392     2   0.000     0.8812 0.000 1.000
#&gt; SRR1383390     1   0.997     0.5333 0.532 0.468
#&gt; SRR1383394     1   0.997     0.5333 0.532 0.468
#&gt; SRR1383393     1   0.000     0.5660 1.000 0.000
#&gt; SRR1383396     1   0.000     0.5660 1.000 0.000
#&gt; SRR1383395     2   0.295     0.8309 0.052 0.948
#&gt; SRR1383399     1   0.997     0.5333 0.532 0.468
#&gt; SRR1383400     1   0.000     0.5660 1.000 0.000
#&gt; SRR1383397     2   0.552     0.6991 0.128 0.872
#&gt; SRR1383401     1   0.998     0.5256 0.528 0.472
#&gt; SRR1383398     1   0.997     0.5333 0.532 0.468
#&gt; SRR1383402     1   0.997     0.5333 0.532 0.468
#&gt; SRR1383404     1   0.000     0.5660 1.000 0.000
#&gt; SRR1383403     1   0.000     0.5660 1.000 0.000
#&gt; SRR1383405     2   0.999    -0.4613 0.480 0.520
#&gt; SRR1383406     1   0.999     0.5000 0.516 0.484
#&gt; SRR1383407     2   0.625     0.6713 0.156 0.844
#&gt; SRR1383408     1   0.997     0.5333 0.532 0.468
#&gt; SRR1383409     1   0.997     0.5333 0.532 0.468
#&gt; SRR1383410     2   0.000     0.8812 0.000 1.000
</code></pre>

<script>
$('#tab-MAD-pam-get-classes-1-a').parent().next().next().hide();
$('#tab-MAD-pam-get-classes-1-a').click(function(){
  $('#tab-MAD-pam-get-classes-1-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-MAD-pam-get-classes-2'>
<p><a id='tab-MAD-pam-get-classes-2-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 3), get_membership(res, k = 3))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3
#&gt; SRR1383358     3  0.0000      0.929 0.000 0.000 1.000
#&gt; SRR1383360     3  0.3500      0.839 0.116 0.004 0.880
#&gt; SRR1383359     3  0.0000      0.929 0.000 0.000 1.000
#&gt; SRR1383362     1  0.0747      0.947 0.984 0.000 0.016
#&gt; SRR1383361     3  0.0000      0.929 0.000 0.000 1.000
#&gt; SRR1383363     3  0.0000      0.929 0.000 0.000 1.000
#&gt; SRR1383364     3  0.2772      0.882 0.004 0.080 0.916
#&gt; SRR1383365     3  0.0000      0.929 0.000 0.000 1.000
#&gt; SRR1383366     3  0.2356      0.890 0.000 0.072 0.928
#&gt; SRR1383367     3  0.0000      0.929 0.000 0.000 1.000
#&gt; SRR1383368     1  0.2537      0.882 0.920 0.000 0.080
#&gt; SRR1383369     3  0.2537      0.885 0.000 0.080 0.920
#&gt; SRR1383370     3  0.0237      0.928 0.000 0.004 0.996
#&gt; SRR1383371     3  0.0747      0.923 0.000 0.016 0.984
#&gt; SRR1383372     3  0.0237      0.928 0.000 0.004 0.996
#&gt; SRR1383373     3  0.0237      0.928 0.000 0.004 0.996
#&gt; SRR1383374     3  0.0000      0.929 0.000 0.000 1.000
#&gt; SRR1383375     1  0.0000      0.957 1.000 0.000 0.000
#&gt; SRR1383376     2  0.0237      0.920 0.004 0.996 0.000
#&gt; SRR1383377     3  0.5650      0.623 0.000 0.312 0.688
#&gt; SRR1383378     1  0.5864      0.535 0.704 0.288 0.008
#&gt; SRR1383379     1  0.2625      0.886 0.916 0.084 0.000
#&gt; SRR1383380     2  0.4750      0.780 0.216 0.784 0.000
#&gt; SRR1383381     2  0.3765      0.907 0.084 0.888 0.028
#&gt; SRR1383382     1  0.0000      0.957 1.000 0.000 0.000
#&gt; SRR1383383     2  0.3043      0.913 0.084 0.908 0.008
#&gt; SRR1383385     1  0.0000      0.957 1.000 0.000 0.000
#&gt; SRR1383384     2  0.1411      0.922 0.036 0.964 0.000
#&gt; SRR1383386     1  0.0000      0.957 1.000 0.000 0.000
#&gt; SRR1383387     2  0.0000      0.920 0.000 1.000 0.000
#&gt; SRR1383389     2  0.3637      0.909 0.084 0.892 0.024
#&gt; SRR1383391     2  0.2625      0.913 0.084 0.916 0.000
#&gt; SRR1383388     1  0.0237      0.956 0.996 0.004 0.000
#&gt; SRR1383392     2  0.0237      0.920 0.000 0.996 0.004
#&gt; SRR1383390     2  0.3043      0.913 0.084 0.908 0.008
#&gt; SRR1383394     2  0.0000      0.920 0.000 1.000 0.000
#&gt; SRR1383393     1  0.0237      0.956 0.996 0.004 0.000
#&gt; SRR1383396     1  0.0000      0.957 1.000 0.000 0.000
#&gt; SRR1383395     2  0.5098      0.611 0.000 0.752 0.248
#&gt; SRR1383399     2  0.3765      0.907 0.084 0.888 0.028
#&gt; SRR1383400     1  0.0000      0.957 1.000 0.000 0.000
#&gt; SRR1383397     2  0.4602      0.818 0.040 0.852 0.108
#&gt; SRR1383401     2  0.2772      0.915 0.080 0.916 0.004
#&gt; SRR1383398     2  0.3038      0.857 0.104 0.896 0.000
#&gt; SRR1383402     2  0.0000      0.920 0.000 1.000 0.000
#&gt; SRR1383404     1  0.0237      0.956 0.996 0.004 0.000
#&gt; SRR1383403     1  0.0237      0.956 0.996 0.004 0.000
#&gt; SRR1383405     2  0.0000      0.920 0.000 1.000 0.000
#&gt; SRR1383406     2  0.0747      0.915 0.000 0.984 0.016
#&gt; SRR1383407     3  0.7924      0.468 0.084 0.304 0.612
#&gt; SRR1383408     2  0.2625      0.913 0.084 0.916 0.000
#&gt; SRR1383409     2  0.2939      0.900 0.012 0.916 0.072
#&gt; SRR1383410     2  0.0237      0.920 0.000 0.996 0.004
</code></pre>

<script>
$('#tab-MAD-pam-get-classes-2-a').parent().next().next().hide();
$('#tab-MAD-pam-get-classes-2-a').click(function(){
  $('#tab-MAD-pam-get-classes-2-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-MAD-pam-get-classes-3'>
<p><a id='tab-MAD-pam-get-classes-3-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 4), get_membership(res, k = 4))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4
#&gt; SRR1383358     3  0.0000      0.926 0.000 0.000 1.000 0.000
#&gt; SRR1383360     3  0.3610      0.719 0.200 0.000 0.800 0.000
#&gt; SRR1383359     3  0.0000      0.926 0.000 0.000 1.000 0.000
#&gt; SRR1383362     1  0.0000      0.809 1.000 0.000 0.000 0.000
#&gt; SRR1383361     3  0.0000      0.926 0.000 0.000 1.000 0.000
#&gt; SRR1383363     3  0.0000      0.926 0.000 0.000 1.000 0.000
#&gt; SRR1383364     3  0.0336      0.922 0.000 0.000 0.992 0.008
#&gt; SRR1383365     3  0.0000      0.926 0.000 0.000 1.000 0.000
#&gt; SRR1383366     3  0.0188      0.924 0.000 0.000 0.996 0.004
#&gt; SRR1383367     3  0.0000      0.926 0.000 0.000 1.000 0.000
#&gt; SRR1383368     1  0.2868      0.726 0.864 0.000 0.136 0.000
#&gt; SRR1383369     3  0.0000      0.926 0.000 0.000 1.000 0.000
#&gt; SRR1383370     3  0.2647      0.819 0.000 0.000 0.880 0.120
#&gt; SRR1383371     3  0.0336      0.922 0.000 0.000 0.992 0.008
#&gt; SRR1383372     3  0.2589      0.822 0.000 0.116 0.884 0.000
#&gt; SRR1383373     3  0.0000      0.926 0.000 0.000 1.000 0.000
#&gt; SRR1383374     3  0.0000      0.926 0.000 0.000 1.000 0.000
#&gt; SRR1383375     1  0.0895      0.807 0.976 0.004 0.000 0.020
#&gt; SRR1383376     2  0.0336      0.943 0.000 0.992 0.000 0.008
#&gt; SRR1383377     4  0.4313      0.517 0.000 0.004 0.260 0.736
#&gt; SRR1383378     2  0.0188      0.944 0.000 0.996 0.004 0.000
#&gt; SRR1383379     1  0.5626      0.440 0.588 0.020 0.004 0.388
#&gt; SRR1383380     4  0.0469      0.774 0.000 0.012 0.000 0.988
#&gt; SRR1383381     2  0.0336      0.942 0.000 0.992 0.000 0.008
#&gt; SRR1383382     1  0.0000      0.809 1.000 0.000 0.000 0.000
#&gt; SRR1383383     2  0.0188      0.944 0.000 0.996 0.004 0.000
#&gt; SRR1383385     4  0.5016      0.427 0.396 0.004 0.000 0.600
#&gt; SRR1383384     2  0.0000      0.945 0.000 1.000 0.000 0.000
#&gt; SRR1383386     1  0.3325      0.792 0.864 0.024 0.000 0.112
#&gt; SRR1383387     2  0.4830      0.388 0.000 0.608 0.000 0.392
#&gt; SRR1383389     2  0.0188      0.944 0.000 0.996 0.004 0.000
#&gt; SRR1383391     2  0.0188      0.945 0.000 0.996 0.000 0.004
#&gt; SRR1383388     1  0.5039      0.444 0.592 0.004 0.000 0.404
#&gt; SRR1383392     2  0.0188      0.945 0.000 0.996 0.000 0.004
#&gt; SRR1383390     2  0.0188      0.944 0.000 0.996 0.004 0.000
#&gt; SRR1383394     2  0.0188      0.945 0.000 0.996 0.000 0.004
#&gt; SRR1383393     4  0.4741      0.489 0.328 0.004 0.000 0.668
#&gt; SRR1383396     1  0.3463      0.795 0.864 0.040 0.000 0.096
#&gt; SRR1383395     4  0.0336      0.775 0.000 0.008 0.000 0.992
#&gt; SRR1383399     2  0.0336      0.942 0.000 0.992 0.000 0.008
#&gt; SRR1383400     1  0.0000      0.809 1.000 0.000 0.000 0.000
#&gt; SRR1383397     4  0.0921      0.766 0.000 0.028 0.000 0.972
#&gt; SRR1383401     2  0.0188      0.945 0.000 0.996 0.000 0.004
#&gt; SRR1383398     4  0.0336      0.775 0.000 0.008 0.000 0.992
#&gt; SRR1383402     2  0.0188      0.945 0.000 0.996 0.000 0.004
#&gt; SRR1383404     1  0.3325      0.792 0.864 0.024 0.000 0.112
#&gt; SRR1383403     4  0.4483      0.551 0.284 0.004 0.000 0.712
#&gt; SRR1383405     2  0.4830      0.388 0.000 0.608 0.000 0.392
#&gt; SRR1383406     4  0.0707      0.771 0.000 0.020 0.000 0.980
#&gt; SRR1383407     3  0.4998      0.126 0.000 0.488 0.512 0.000
#&gt; SRR1383408     2  0.0000      0.945 0.000 1.000 0.000 0.000
#&gt; SRR1383409     2  0.0188      0.945 0.000 0.996 0.000 0.004
#&gt; SRR1383410     2  0.0188      0.945 0.000 0.996 0.000 0.004
</code></pre>

<script>
$('#tab-MAD-pam-get-classes-3-a').parent().next().next().hide();
$('#tab-MAD-pam-get-classes-3-a').click(function(){
  $('#tab-MAD-pam-get-classes-3-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-MAD-pam-get-classes-4'>
<p><a id='tab-MAD-pam-get-classes-4-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 5), get_membership(res, k = 5))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4    p5
#&gt; SRR1383358     3  0.0000     0.9123 0.000 0.000 1.000 0.000 0.000
#&gt; SRR1383360     3  0.2561     0.7825 0.000 0.000 0.856 0.000 0.144
#&gt; SRR1383359     3  0.0000     0.9123 0.000 0.000 1.000 0.000 0.000
#&gt; SRR1383362     1  0.6034     1.0000 0.572 0.000 0.000 0.172 0.256
#&gt; SRR1383361     3  0.0000     0.9123 0.000 0.000 1.000 0.000 0.000
#&gt; SRR1383363     3  0.0000     0.9123 0.000 0.000 1.000 0.000 0.000
#&gt; SRR1383364     3  0.4861     0.4908 0.428 0.000 0.548 0.024 0.000
#&gt; SRR1383365     3  0.0000     0.9123 0.000 0.000 1.000 0.000 0.000
#&gt; SRR1383366     3  0.0162     0.9106 0.000 0.000 0.996 0.004 0.000
#&gt; SRR1383367     3  0.0000     0.9123 0.000 0.000 1.000 0.000 0.000
#&gt; SRR1383368     4  0.6593     0.0241 0.000 0.000 0.284 0.464 0.252
#&gt; SRR1383369     3  0.0693     0.9035 0.012 0.008 0.980 0.000 0.000
#&gt; SRR1383370     3  0.1851     0.8475 0.000 0.000 0.912 0.088 0.000
#&gt; SRR1383371     3  0.4392     0.5653 0.380 0.000 0.612 0.008 0.000
#&gt; SRR1383372     3  0.1851     0.8409 0.000 0.088 0.912 0.000 0.000
#&gt; SRR1383373     3  0.0000     0.9123 0.000 0.000 1.000 0.000 0.000
#&gt; SRR1383374     3  0.0000     0.9123 0.000 0.000 1.000 0.000 0.000
#&gt; SRR1383375     4  0.4268     0.0791 0.000 0.000 0.000 0.556 0.444
#&gt; SRR1383376     2  0.0162     0.8279 0.000 0.996 0.000 0.004 0.000
#&gt; SRR1383377     4  0.7050    -0.4032 0.000 0.012 0.252 0.392 0.344
#&gt; SRR1383378     2  0.1965     0.7930 0.000 0.904 0.000 0.096 0.000
#&gt; SRR1383379     4  0.2392     0.2975 0.000 0.104 0.004 0.888 0.004
#&gt; SRR1383380     5  0.4249     0.6671 0.000 0.000 0.000 0.432 0.568
#&gt; SRR1383381     2  0.6034     0.3568 0.428 0.456 0.000 0.116 0.000
#&gt; SRR1383382     1  0.6034     1.0000 0.572 0.000 0.000 0.172 0.256
#&gt; SRR1383383     2  0.1908     0.7954 0.000 0.908 0.000 0.092 0.000
#&gt; SRR1383385     5  0.0162     0.4344 0.004 0.000 0.000 0.000 0.996
#&gt; SRR1383384     2  0.0162     0.8289 0.000 0.996 0.000 0.004 0.000
#&gt; SRR1383386     4  0.4167     0.3739 0.000 0.024 0.000 0.724 0.252
#&gt; SRR1383387     2  0.4375     0.2878 0.000 0.576 0.000 0.420 0.004
#&gt; SRR1383389     2  0.1908     0.7954 0.000 0.908 0.000 0.092 0.000
#&gt; SRR1383391     2  0.0162     0.8289 0.000 0.996 0.000 0.004 0.000
#&gt; SRR1383388     4  0.0880     0.3584 0.000 0.000 0.000 0.968 0.032
#&gt; SRR1383392     2  0.0000     0.8291 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1383390     2  0.1908     0.7954 0.000 0.908 0.000 0.092 0.000
#&gt; SRR1383394     2  0.0000     0.8291 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1383393     5  0.1121     0.3820 0.000 0.000 0.000 0.044 0.956
#&gt; SRR1383396     4  0.4701     0.3098 0.004 0.044 0.000 0.700 0.252
#&gt; SRR1383395     5  0.4738     0.6704 0.000 0.012 0.004 0.420 0.564
#&gt; SRR1383399     2  0.6034     0.3568 0.428 0.456 0.000 0.116 0.000
#&gt; SRR1383400     1  0.6034     1.0000 0.572 0.000 0.000 0.172 0.256
#&gt; SRR1383397     5  0.6030     0.5585 0.000 0.116 0.000 0.420 0.464
#&gt; SRR1383401     2  0.0000     0.8291 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1383398     5  0.4497     0.6710 0.000 0.008 0.000 0.424 0.568
#&gt; SRR1383402     2  0.0000     0.8291 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1383404     4  0.4193     0.3745 0.000 0.024 0.000 0.720 0.256
#&gt; SRR1383403     5  0.0162     0.4449 0.000 0.000 0.000 0.004 0.996
#&gt; SRR1383405     2  0.4375     0.2878 0.000 0.576 0.000 0.420 0.004
#&gt; SRR1383406     5  0.4848     0.6645 0.000 0.024 0.000 0.420 0.556
#&gt; SRR1383407     2  0.4644     0.0597 0.000 0.528 0.460 0.012 0.000
#&gt; SRR1383408     2  0.0290     0.8281 0.000 0.992 0.000 0.008 0.000
#&gt; SRR1383409     2  0.0162     0.8284 0.000 0.996 0.004 0.000 0.000
#&gt; SRR1383410     2  0.0000     0.8291 0.000 1.000 0.000 0.000 0.000
</code></pre>

<script>
$('#tab-MAD-pam-get-classes-4-a').parent().next().next().hide();
$('#tab-MAD-pam-get-classes-4-a').click(function(){
  $('#tab-MAD-pam-get-classes-4-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-MAD-pam-get-classes-5'>
<p><a id='tab-MAD-pam-get-classes-5-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 6), get_membership(res, k = 6))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4    p5 p6
#&gt; SRR1383358     3  0.0000      0.990 0.000 0.000 1.000 0.000 0.000  0
#&gt; SRR1383360     3  0.0914      0.965 0.016 0.000 0.968 0.016 0.000  0
#&gt; SRR1383359     3  0.0000      0.990 0.000 0.000 1.000 0.000 0.000  0
#&gt; SRR1383362     6  0.0000      1.000 0.000 0.000 0.000 0.000 0.000  1
#&gt; SRR1383361     3  0.0000      0.990 0.000 0.000 1.000 0.000 0.000  0
#&gt; SRR1383363     3  0.0000      0.990 0.000 0.000 1.000 0.000 0.000  0
#&gt; SRR1383364     5  0.0146      0.856 0.000 0.000 0.004 0.000 0.996  0
#&gt; SRR1383365     3  0.0000      0.990 0.000 0.000 1.000 0.000 0.000  0
#&gt; SRR1383366     3  0.0146      0.988 0.004 0.000 0.996 0.000 0.000  0
#&gt; SRR1383367     3  0.0000      0.990 0.000 0.000 1.000 0.000 0.000  0
#&gt; SRR1383368     4  0.4242      0.143 0.016 0.000 0.448 0.536 0.000  0
#&gt; SRR1383369     3  0.1088      0.953 0.000 0.024 0.960 0.000 0.016  0
#&gt; SRR1383370     3  0.0363      0.982 0.000 0.000 0.988 0.012 0.000  0
#&gt; SRR1383371     5  0.3151      0.583 0.000 0.000 0.252 0.000 0.748  0
#&gt; SRR1383372     3  0.0363      0.981 0.000 0.012 0.988 0.000 0.000  0
#&gt; SRR1383373     3  0.0000      0.990 0.000 0.000 1.000 0.000 0.000  0
#&gt; SRR1383374     3  0.0000      0.990 0.000 0.000 1.000 0.000 0.000  0
#&gt; SRR1383375     4  0.3765      0.329 0.404 0.000 0.000 0.596 0.000  0
#&gt; SRR1383376     2  0.0146      0.880 0.004 0.996 0.000 0.000 0.000  0
#&gt; SRR1383377     4  0.6516     -0.307 0.316 0.020 0.284 0.380 0.000  0
#&gt; SRR1383378     2  0.1806      0.840 0.000 0.908 0.000 0.088 0.004  0
#&gt; SRR1383379     4  0.1668      0.488 0.004 0.060 0.008 0.928 0.000  0
#&gt; SRR1383380     1  0.3782      0.673 0.588 0.000 0.000 0.412 0.000  0
#&gt; SRR1383381     5  0.0000      0.857 0.000 0.000 0.000 0.000 1.000  0
#&gt; SRR1383382     6  0.0000      1.000 0.000 0.000 0.000 0.000 0.000  1
#&gt; SRR1383383     2  0.1588      0.851 0.000 0.924 0.000 0.072 0.004  0
#&gt; SRR1383385     1  0.0146      0.550 0.996 0.000 0.000 0.004 0.000  0
#&gt; SRR1383384     2  0.0146      0.881 0.000 0.996 0.000 0.004 0.000  0
#&gt; SRR1383386     4  0.0603      0.548 0.016 0.000 0.000 0.980 0.004  0
#&gt; SRR1383387     2  0.3881      0.323 0.004 0.600 0.000 0.396 0.000  0
#&gt; SRR1383389     2  0.1588      0.851 0.000 0.924 0.000 0.072 0.004  0
#&gt; SRR1383391     2  0.0291      0.881 0.000 0.992 0.000 0.004 0.004  0
#&gt; SRR1383388     4  0.0000      0.538 0.000 0.000 0.000 1.000 0.000  0
#&gt; SRR1383392     2  0.0000      0.882 0.000 1.000 0.000 0.000 0.000  0
#&gt; SRR1383390     2  0.1588      0.851 0.000 0.924 0.000 0.072 0.004  0
#&gt; SRR1383394     2  0.0000      0.882 0.000 1.000 0.000 0.000 0.000  0
#&gt; SRR1383393     1  0.1075      0.512 0.952 0.000 0.000 0.048 0.000  0
#&gt; SRR1383396     4  0.5190      0.276 0.016 0.096 0.000 0.632 0.256  0
#&gt; SRR1383395     1  0.4228      0.682 0.588 0.020 0.000 0.392 0.000  0
#&gt; SRR1383399     5  0.0000      0.857 0.000 0.000 0.000 0.000 1.000  0
#&gt; SRR1383400     6  0.0000      1.000 0.000 0.000 0.000 0.000 0.000  1
#&gt; SRR1383397     1  0.5146      0.602 0.516 0.088 0.000 0.396 0.000  0
#&gt; SRR1383401     2  0.0000      0.882 0.000 1.000 0.000 0.000 0.000  0
#&gt; SRR1383398     1  0.4159      0.682 0.588 0.016 0.000 0.396 0.000  0
#&gt; SRR1383402     2  0.0000      0.882 0.000 1.000 0.000 0.000 0.000  0
#&gt; SRR1383404     4  0.0458      0.547 0.016 0.000 0.000 0.984 0.000  0
#&gt; SRR1383403     1  0.0146      0.550 0.996 0.000 0.000 0.004 0.000  0
#&gt; SRR1383405     2  0.3881      0.323 0.004 0.600 0.000 0.396 0.000  0
#&gt; SRR1383406     1  0.4403      0.677 0.580 0.012 0.012 0.396 0.000  0
#&gt; SRR1383407     2  0.4633      0.302 0.000 0.568 0.392 0.036 0.004  0
#&gt; SRR1383408     2  0.0291      0.881 0.000 0.992 0.000 0.004 0.004  0
#&gt; SRR1383409     2  0.0146      0.881 0.000 0.996 0.004 0.000 0.000  0
#&gt; SRR1383410     2  0.0000      0.882 0.000 1.000 0.000 0.000 0.000  0
</code></pre>

<script>
$('#tab-MAD-pam-get-classes-5-a').parent().next().next().hide();
$('#tab-MAD-pam-get-classes-5-a').click(function(){
  $('#tab-MAD-pam-get-classes-5-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>
</div>

Heatmaps for the consensus matrix. It visualizes the probability of two
samples to be in a same group.



<script>
$( function() {
	$( '#tabs-MAD-pam-consensus-heatmap' ).tabs();
} );
</script>
<div id='tabs-MAD-pam-consensus-heatmap'>
<ul>
<li><a href='#tab-MAD-pam-consensus-heatmap-1'>k = 2</a></li>
<li><a href='#tab-MAD-pam-consensus-heatmap-2'>k = 3</a></li>
<li><a href='#tab-MAD-pam-consensus-heatmap-3'>k = 4</a></li>
<li><a href='#tab-MAD-pam-consensus-heatmap-4'>k = 5</a></li>
<li><a href='#tab-MAD-pam-consensus-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-MAD-pam-consensus-heatmap-1'>
<pre><code class="r">consensus_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-MAD-pam-consensus-heatmap-1-1.png" alt="plot of chunk tab-MAD-pam-consensus-heatmap-1"/></p>

</div>
<div id='tab-MAD-pam-consensus-heatmap-2'>
<pre><code class="r">consensus_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-MAD-pam-consensus-heatmap-2-1.png" alt="plot of chunk tab-MAD-pam-consensus-heatmap-2"/></p>

</div>
<div id='tab-MAD-pam-consensus-heatmap-3'>
<pre><code class="r">consensus_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-MAD-pam-consensus-heatmap-3-1.png" alt="plot of chunk tab-MAD-pam-consensus-heatmap-3"/></p>

</div>
<div id='tab-MAD-pam-consensus-heatmap-4'>
<pre><code class="r">consensus_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-MAD-pam-consensus-heatmap-4-1.png" alt="plot of chunk tab-MAD-pam-consensus-heatmap-4"/></p>

</div>
<div id='tab-MAD-pam-consensus-heatmap-5'>
<pre><code class="r">consensus_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-MAD-pam-consensus-heatmap-5-1.png" alt="plot of chunk tab-MAD-pam-consensus-heatmap-5"/></p>

</div>
</div>

Heatmaps for the membership of samples in all partitions to see how consistent they are:




<script>
$( function() {
	$( '#tabs-MAD-pam-membership-heatmap' ).tabs();
} );
</script>
<div id='tabs-MAD-pam-membership-heatmap'>
<ul>
<li><a href='#tab-MAD-pam-membership-heatmap-1'>k = 2</a></li>
<li><a href='#tab-MAD-pam-membership-heatmap-2'>k = 3</a></li>
<li><a href='#tab-MAD-pam-membership-heatmap-3'>k = 4</a></li>
<li><a href='#tab-MAD-pam-membership-heatmap-4'>k = 5</a></li>
<li><a href='#tab-MAD-pam-membership-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-MAD-pam-membership-heatmap-1'>
<pre><code class="r">membership_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-MAD-pam-membership-heatmap-1-1.png" alt="plot of chunk tab-MAD-pam-membership-heatmap-1"/></p>

</div>
<div id='tab-MAD-pam-membership-heatmap-2'>
<pre><code class="r">membership_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-MAD-pam-membership-heatmap-2-1.png" alt="plot of chunk tab-MAD-pam-membership-heatmap-2"/></p>

</div>
<div id='tab-MAD-pam-membership-heatmap-3'>
<pre><code class="r">membership_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-MAD-pam-membership-heatmap-3-1.png" alt="plot of chunk tab-MAD-pam-membership-heatmap-3"/></p>

</div>
<div id='tab-MAD-pam-membership-heatmap-4'>
<pre><code class="r">membership_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-MAD-pam-membership-heatmap-4-1.png" alt="plot of chunk tab-MAD-pam-membership-heatmap-4"/></p>

</div>
<div id='tab-MAD-pam-membership-heatmap-5'>
<pre><code class="r">membership_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-MAD-pam-membership-heatmap-5-1.png" alt="plot of chunk tab-MAD-pam-membership-heatmap-5"/></p>

</div>
</div>

As soon as we have had the classes for columns, we can look for signatures
which are significantly different between classes which can be candidate marks
for certain classes. Following are the heatmaps for signatures.



Signature heatmaps where rows are scaled:



<script>
$( function() {
	$( '#tabs-MAD-pam-get-signatures' ).tabs();
} );
</script>
<div id='tabs-MAD-pam-get-signatures'>
<ul>
<li><a href='#tab-MAD-pam-get-signatures-1'>k = 2</a></li>
<li><a href='#tab-MAD-pam-get-signatures-2'>k = 3</a></li>
<li><a href='#tab-MAD-pam-get-signatures-3'>k = 4</a></li>
<li><a href='#tab-MAD-pam-get-signatures-4'>k = 5</a></li>
<li><a href='#tab-MAD-pam-get-signatures-5'>k = 6</a></li>
</ul>
<div id='tab-MAD-pam-get-signatures-1'>
<pre><code class="r">get_signatures(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-MAD-pam-get-signatures-1-1.png" alt="plot of chunk tab-MAD-pam-get-signatures-1"/></p>

</div>
<div id='tab-MAD-pam-get-signatures-2'>
<pre><code class="r">get_signatures(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-MAD-pam-get-signatures-2-1.png" alt="plot of chunk tab-MAD-pam-get-signatures-2"/></p>

</div>
<div id='tab-MAD-pam-get-signatures-3'>
<pre><code class="r">get_signatures(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-MAD-pam-get-signatures-3-1.png" alt="plot of chunk tab-MAD-pam-get-signatures-3"/></p>

</div>
<div id='tab-MAD-pam-get-signatures-4'>
<pre><code class="r">get_signatures(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-MAD-pam-get-signatures-4-1.png" alt="plot of chunk tab-MAD-pam-get-signatures-4"/></p>

</div>
<div id='tab-MAD-pam-get-signatures-5'>
<pre><code class="r">get_signatures(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-MAD-pam-get-signatures-5-1.png" alt="plot of chunk tab-MAD-pam-get-signatures-5"/></p>

</div>
</div>



Signature heatmaps where rows are not scaled:


<script>
$( function() {
	$( '#tabs-MAD-pam-get-signatures-no-scale' ).tabs();
} );
</script>
<div id='tabs-MAD-pam-get-signatures-no-scale'>
<ul>
<li><a href='#tab-MAD-pam-get-signatures-no-scale-1'>k = 2</a></li>
<li><a href='#tab-MAD-pam-get-signatures-no-scale-2'>k = 3</a></li>
<li><a href='#tab-MAD-pam-get-signatures-no-scale-3'>k = 4</a></li>
<li><a href='#tab-MAD-pam-get-signatures-no-scale-4'>k = 5</a></li>
<li><a href='#tab-MAD-pam-get-signatures-no-scale-5'>k = 6</a></li>
</ul>
<div id='tab-MAD-pam-get-signatures-no-scale-1'>
<pre><code class="r">get_signatures(res, k = 2, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-MAD-pam-get-signatures-no-scale-1-1.png" alt="plot of chunk tab-MAD-pam-get-signatures-no-scale-1"/></p>

</div>
<div id='tab-MAD-pam-get-signatures-no-scale-2'>
<pre><code class="r">get_signatures(res, k = 3, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-MAD-pam-get-signatures-no-scale-2-1.png" alt="plot of chunk tab-MAD-pam-get-signatures-no-scale-2"/></p>

</div>
<div id='tab-MAD-pam-get-signatures-no-scale-3'>
<pre><code class="r">get_signatures(res, k = 4, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-MAD-pam-get-signatures-no-scale-3-1.png" alt="plot of chunk tab-MAD-pam-get-signatures-no-scale-3"/></p>

</div>
<div id='tab-MAD-pam-get-signatures-no-scale-4'>
<pre><code class="r">get_signatures(res, k = 5, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-MAD-pam-get-signatures-no-scale-4-1.png" alt="plot of chunk tab-MAD-pam-get-signatures-no-scale-4"/></p>

</div>
<div id='tab-MAD-pam-get-signatures-no-scale-5'>
<pre><code class="r">get_signatures(res, k = 6, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-MAD-pam-get-signatures-no-scale-5-1.png" alt="plot of chunk tab-MAD-pam-get-signatures-no-scale-5"/></p>

</div>
</div>



Compare the overlap of signatures from different k:

```r
compare_signatures(res)
```

![plot of chunk MAD-pam-signature_compare](figure_cola/MAD-pam-signature_compare-1.png)

`get_signature()` returns a data frame invisibly. TO get the list of signatures, the function
call should be assigned to a variable explicitly. In following code, if `plot` argument is set
to `FALSE`, no heatmap is plotted while only the differential analysis is performed.

```r
# code only for demonstration
tb = get_signature(res, k = ..., plot = FALSE)
```

An example of the output of `tb` is:

```
#>   which_row         fdr    mean_1    mean_2 scaled_mean_1 scaled_mean_2 km
#> 1        38 0.042760348  8.373488  9.131774    -0.5533452     0.5164555  1
#> 2        40 0.018707592  7.106213  8.469186    -0.6173731     0.5762149  1
#> 3        55 0.019134737 10.221463 11.207825    -0.6159697     0.5749050  1
#> 4        59 0.006059896  5.921854  7.869574    -0.6899429     0.6439467  1
#> 5        60 0.018055526  8.928898 10.211722    -0.6204761     0.5791110  1
#> 6        98 0.009384629 15.714769 14.887706     0.6635654    -0.6193277  2
...
```

The columns in `tb` are:

1. `which_row`: row indices corresponding to the input matrix.
2. `fdr`: FDR for the differential test. 
3. `mean_x`: The mean value in group x.
4. `scaled_mean_x`: The mean value in group x after rows are scaled.
5. `km`: Row groups if k-means clustering is applied to rows.



UMAP plot which shows how samples are separated.


<script>
$( function() {
	$( '#tabs-MAD-pam-dimension-reduction' ).tabs();
} );
</script>
<div id='tabs-MAD-pam-dimension-reduction'>
<ul>
<li><a href='#tab-MAD-pam-dimension-reduction-1'>k = 2</a></li>
<li><a href='#tab-MAD-pam-dimension-reduction-2'>k = 3</a></li>
<li><a href='#tab-MAD-pam-dimension-reduction-3'>k = 4</a></li>
<li><a href='#tab-MAD-pam-dimension-reduction-4'>k = 5</a></li>
<li><a href='#tab-MAD-pam-dimension-reduction-5'>k = 6</a></li>
</ul>
<div id='tab-MAD-pam-dimension-reduction-1'>
<pre><code class="r">dimension_reduction(res, k = 2, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-MAD-pam-dimension-reduction-1-1.png" alt="plot of chunk tab-MAD-pam-dimension-reduction-1"/></p>

</div>
<div id='tab-MAD-pam-dimension-reduction-2'>
<pre><code class="r">dimension_reduction(res, k = 3, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-MAD-pam-dimension-reduction-2-1.png" alt="plot of chunk tab-MAD-pam-dimension-reduction-2"/></p>

</div>
<div id='tab-MAD-pam-dimension-reduction-3'>
<pre><code class="r">dimension_reduction(res, k = 4, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-MAD-pam-dimension-reduction-3-1.png" alt="plot of chunk tab-MAD-pam-dimension-reduction-3"/></p>

</div>
<div id='tab-MAD-pam-dimension-reduction-4'>
<pre><code class="r">dimension_reduction(res, k = 5, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-MAD-pam-dimension-reduction-4-1.png" alt="plot of chunk tab-MAD-pam-dimension-reduction-4"/></p>

</div>
<div id='tab-MAD-pam-dimension-reduction-5'>
<pre><code class="r">dimension_reduction(res, k = 6, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-MAD-pam-dimension-reduction-5-1.png" alt="plot of chunk tab-MAD-pam-dimension-reduction-5"/></p>

</div>
</div>


Following heatmap shows how subgroups are split when increasing `k`:

```r
collect_classes(res)
```

![plot of chunk MAD-pam-collect-classes](figure_cola/MAD-pam-collect-classes-1.png)


If matrix rows can be associated to genes, consider to use `functional_enrichment(res,
...)` to perform function enrichment for the signature genes. See [this vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/functional_enrichment.html) for more detailed explanations.


 

---------------------------------------------------




### MAD:mclust**






The object with results only for a single top-value method and a single partition method 
can be extracted as:

```r
res = res_list["MAD", "mclust"]
# you can also extract it by
# res = res_list["MAD:mclust"]
```

A summary of `res` and all the functions that can be applied to it:

```r
res
```

```
#> A 'ConsensusPartition' object with k = 2, 3, 4, 5, 6.
#>   On a matrix with 15680 rows and 53 columns.
#>   Top rows (1000, 2000, 3000, 4000, 5000) are extracted by 'MAD' method.
#>   Subgroups are detected by 'mclust' method.
#>   Performed in total 1250 partitions by row resampling.
#>   Best k for subgroups seems to be 2.
#> 
#> Following methods can be applied to this 'ConsensusPartition' object:
#>  [1] "cola_report"             "collect_classes"         "collect_plots"          
#>  [4] "collect_stats"           "colnames"                "compare_signatures"     
#>  [7] "consensus_heatmap"       "dimension_reduction"     "functional_enrichment"  
#> [10] "get_anno_col"            "get_anno"                "get_classes"            
#> [13] "get_consensus"           "get_matrix"              "get_membership"         
#> [16] "get_param"               "get_signatures"          "get_stats"              
#> [19] "is_best_k"               "is_stable_k"             "membership_heatmap"     
#> [22] "ncol"                    "nrow"                    "plot_ecdf"              
#> [25] "rownames"                "select_partition_number" "show"                   
#> [28] "suggest_best_k"          "test_to_known_factors"
```

`collect_plots()` function collects all the plots made from `res` for all `k` (number of partitions)
into one single page to provide an easy and fast comparison between different `k`.

```r
collect_plots(res)
```

![plot of chunk MAD-mclust-collect-plots](figure_cola/MAD-mclust-collect-plots-1.png)

The plots are:

- The first row: a plot of the ECDF (empirical cumulative distribution
  function) curves of the consensus matrix for each `k` and the heatmap of
  predicted classes for each `k`.
- The second row: heatmaps of the consensus matrix for each `k`.
- The third row: heatmaps of the membership matrix for each `k`.
- The fouth row: heatmaps of the signatures for each `k`.

All the plots in panels can be made by individual functions and they are
plotted later in this section.

`select_partition_number()` produces several plots showing different
statistics for choosing "optimized" `k`. There are following statistics:

- ECDF curves of the consensus matrix for each `k`;
- 1-PAC. [The PAC
  score](https://en.wikipedia.org/wiki/Consensus_clustering#Over-interpretation_potential_of_consensus_clustering)
  measures the proportion of the ambiguous subgrouping.
- Mean silhouette score.
- Concordance. The mean probability of fiting the consensus class ids in all
  partitions.
- Area increased. Denote $A_k$ as the area under the ECDF curve for current
  `k`, the area increased is defined as $A_k - A_{k-1}$.
- Rand index. The percent of pairs of samples that are both in a same cluster
  or both are not in a same cluster in the partition of k and k-1.
- Jaccard index. The ratio of pairs of samples are both in a same cluster in
  the partition of k and k-1 and the pairs of samples are both in a same
  cluster in the partition k or k-1.

The detailed explanations of these statistics can be found in [the _cola_
vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/cola.html#toc_13).

Generally speaking, lower PAC score, higher mean silhouette score or higher
concordance corresponds to better partition. Rand index and Jaccard index
measure how similar the current partition is compared to partition with `k-1`.
If they are too similar, we won't accept `k` is better than `k-1`.

```r
select_partition_number(res)
```

![plot of chunk MAD-mclust-select-partition-number](figure_cola/MAD-mclust-select-partition-number-1.png)

The numeric values for all these statistics can be obtained by `get_stats()`.

```r
get_stats(res)
```

```
#>   k 1-PAC mean_silhouette concordance area_increased  Rand Jaccard
#> 2 2 1.000           0.951       0.969         0.2644 0.766   0.766
#> 3 3 0.665           0.816       0.904         1.2270 0.634   0.523
#> 4 4 0.669           0.698       0.853         0.2223 0.816   0.568
#> 5 5 0.607           0.542       0.733         0.0714 0.925   0.723
#> 6 6 0.651           0.615       0.723         0.0390 0.903   0.591
```

`suggest_best_k()` suggests the best $k$ based on these statistics. The rules are as follows:

- All $k$ with Jaccard index larger than 0.95 are removed because increasing
  $k$ does not provide enough extra information. If all $k$ are removed, it is
  marked as no subgroup is detected.
- For all $k$ with 1-PAC score larger than 0.9, the maximal $k$ is taken as
  the best $k$, and other $k$ are marked as optional $k$.
- If it does not fit the second rule. The $k$ with the maximal vote of the
  highest 1-PAC score, highest mean silhouette, and highest concordance is
  taken as the best $k$.

```r
suggest_best_k(res)
```

```
#> [1] 2
```


Following shows the table of the partitions (You need to click the **show/hide
code output** link to see it). The membership matrix (columns with name `p*`)
is inferred by
[`clue::cl_consensus()`](https://www.rdocumentation.org/link/cl_consensus?package=clue)
function with the `SE` method. Basically the value in the membership matrix
represents the probability to belong to a certain group. The finall class
label for an item is determined with the group with highest probability it
belongs to.

In `get_classes()` function, the entropy is calculated from the membership
matrix and the silhouette score is calculated from the consensus matrix.



<script>
$( function() {
	$( '#tabs-MAD-mclust-get-classes' ).tabs();
} );
</script>
<div id='tabs-MAD-mclust-get-classes'>
<ul>
<li><a href='#tab-MAD-mclust-get-classes-1'>k = 2</a></li>
<li><a href='#tab-MAD-mclust-get-classes-2'>k = 3</a></li>
<li><a href='#tab-MAD-mclust-get-classes-3'>k = 4</a></li>
<li><a href='#tab-MAD-mclust-get-classes-4'>k = 5</a></li>
<li><a href='#tab-MAD-mclust-get-classes-5'>k = 6</a></li>
</ul>

<div id='tab-MAD-mclust-get-classes-1'>
<p><a id='tab-MAD-mclust-get-classes-1-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 2), get_membership(res, k = 2))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2
#&gt; SRR1383358     2  0.0376      0.963 0.004 0.996
#&gt; SRR1383360     2  0.4161      0.934 0.084 0.916
#&gt; SRR1383359     2  0.0376      0.963 0.004 0.996
#&gt; SRR1383362     1  0.0000      1.000 1.000 0.000
#&gt; SRR1383361     2  0.0000      0.963 0.000 1.000
#&gt; SRR1383363     2  0.0376      0.963 0.004 0.996
#&gt; SRR1383364     2  0.0376      0.963 0.004 0.996
#&gt; SRR1383365     2  0.0376      0.963 0.004 0.996
#&gt; SRR1383366     2  0.1414      0.958 0.020 0.980
#&gt; SRR1383367     2  0.0000      0.963 0.000 1.000
#&gt; SRR1383368     2  0.3584      0.941 0.068 0.932
#&gt; SRR1383369     2  0.0376      0.963 0.004 0.996
#&gt; SRR1383370     2  0.0376      0.963 0.004 0.996
#&gt; SRR1383371     2  0.0376      0.963 0.004 0.996
#&gt; SRR1383372     2  0.0000      0.963 0.000 1.000
#&gt; SRR1383373     2  0.0000      0.963 0.000 1.000
#&gt; SRR1383374     2  0.0376      0.963 0.004 0.996
#&gt; SRR1383375     1  0.0000      1.000 1.000 0.000
#&gt; SRR1383376     2  0.0000      0.963 0.000 1.000
#&gt; SRR1383377     2  0.4161      0.934 0.084 0.916
#&gt; SRR1383378     2  0.3431      0.943 0.064 0.936
#&gt; SRR1383379     2  0.4161      0.934 0.084 0.916
#&gt; SRR1383380     2  0.4161      0.934 0.084 0.916
#&gt; SRR1383381     2  0.0376      0.963 0.004 0.996
#&gt; SRR1383382     1  0.0000      1.000 1.000 0.000
#&gt; SRR1383383     2  0.0376      0.963 0.004 0.996
#&gt; SRR1383385     1  0.0000      1.000 1.000 0.000
#&gt; SRR1383384     2  0.0000      0.963 0.000 1.000
#&gt; SRR1383386     2  0.9580      0.476 0.380 0.620
#&gt; SRR1383387     2  0.4022      0.934 0.080 0.920
#&gt; SRR1383389     2  0.0000      0.963 0.000 1.000
#&gt; SRR1383391     2  0.0000      0.963 0.000 1.000
#&gt; SRR1383388     2  0.4161      0.934 0.084 0.916
#&gt; SRR1383392     2  0.0000      0.963 0.000 1.000
#&gt; SRR1383390     2  0.0000      0.963 0.000 1.000
#&gt; SRR1383394     2  0.0000      0.963 0.000 1.000
#&gt; SRR1383393     1  0.0000      1.000 1.000 0.000
#&gt; SRR1383396     2  0.4161      0.934 0.084 0.916
#&gt; SRR1383395     2  0.4161      0.934 0.084 0.916
#&gt; SRR1383399     2  0.0376      0.963 0.004 0.996
#&gt; SRR1383400     1  0.0000      1.000 1.000 0.000
#&gt; SRR1383397     2  0.4161      0.934 0.084 0.916
#&gt; SRR1383401     2  0.0376      0.963 0.004 0.996
#&gt; SRR1383398     2  0.4161      0.934 0.084 0.916
#&gt; SRR1383402     2  0.0000      0.963 0.000 1.000
#&gt; SRR1383404     2  0.4161      0.934 0.084 0.916
#&gt; SRR1383403     1  0.0000      1.000 1.000 0.000
#&gt; SRR1383405     2  0.4022      0.934 0.080 0.920
#&gt; SRR1383406     2  0.4161      0.934 0.084 0.916
#&gt; SRR1383407     2  0.0000      0.963 0.000 1.000
#&gt; SRR1383408     2  0.0000      0.963 0.000 1.000
#&gt; SRR1383409     2  0.0000      0.963 0.000 1.000
#&gt; SRR1383410     2  0.0000      0.963 0.000 1.000
</code></pre>

<script>
$('#tab-MAD-mclust-get-classes-1-a').parent().next().next().hide();
$('#tab-MAD-mclust-get-classes-1-a').click(function(){
  $('#tab-MAD-mclust-get-classes-1-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-MAD-mclust-get-classes-2'>
<p><a id='tab-MAD-mclust-get-classes-2-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 3), get_membership(res, k = 3))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3
#&gt; SRR1383358     3  0.0000    0.80196 0.000 0.000 1.000
#&gt; SRR1383360     3  0.6421    0.48013 0.004 0.424 0.572
#&gt; SRR1383359     3  0.0000    0.80196 0.000 0.000 1.000
#&gt; SRR1383362     1  0.0237    1.00000 0.996 0.000 0.004
#&gt; SRR1383361     3  0.3941    0.78859 0.000 0.156 0.844
#&gt; SRR1383363     3  0.2165    0.79648 0.000 0.064 0.936
#&gt; SRR1383364     3  0.0000    0.80196 0.000 0.000 1.000
#&gt; SRR1383365     3  0.0237    0.80246 0.000 0.004 0.996
#&gt; SRR1383366     3  0.6126    0.46320 0.000 0.400 0.600
#&gt; SRR1383367     3  0.5216    0.72333 0.000 0.260 0.740
#&gt; SRR1383368     3  0.7150    0.58548 0.036 0.348 0.616
#&gt; SRR1383369     3  0.0000    0.80196 0.000 0.000 1.000
#&gt; SRR1383370     3  0.6045    0.55911 0.000 0.380 0.620
#&gt; SRR1383371     3  0.0000    0.80196 0.000 0.000 1.000
#&gt; SRR1383372     3  0.4121    0.78496 0.000 0.168 0.832
#&gt; SRR1383373     3  0.2261    0.79661 0.000 0.068 0.932
#&gt; SRR1383374     3  0.5621    0.66784 0.000 0.308 0.692
#&gt; SRR1383375     1  0.0237    1.00000 0.996 0.000 0.004
#&gt; SRR1383376     2  0.0892    0.90450 0.000 0.980 0.020
#&gt; SRR1383377     2  0.6142    0.70846 0.040 0.748 0.212
#&gt; SRR1383378     2  0.1877    0.90048 0.032 0.956 0.012
#&gt; SRR1383379     2  0.2550    0.89179 0.040 0.936 0.024
#&gt; SRR1383380     2  0.3572    0.87053 0.040 0.900 0.060
#&gt; SRR1383381     3  0.0000    0.80196 0.000 0.000 1.000
#&gt; SRR1383382     1  0.0237    1.00000 0.996 0.000 0.004
#&gt; SRR1383383     2  0.1031    0.90430 0.000 0.976 0.024
#&gt; SRR1383385     1  0.0237    1.00000 0.996 0.000 0.004
#&gt; SRR1383384     2  0.0892    0.90450 0.000 0.980 0.020
#&gt; SRR1383386     2  0.6421    0.24444 0.424 0.572 0.004
#&gt; SRR1383387     2  0.0661    0.90224 0.004 0.988 0.008
#&gt; SRR1383389     2  0.3500    0.83653 0.004 0.880 0.116
#&gt; SRR1383391     2  0.0892    0.90450 0.000 0.980 0.020
#&gt; SRR1383388     2  0.1647    0.89777 0.036 0.960 0.004
#&gt; SRR1383392     2  0.2066    0.88254 0.000 0.940 0.060
#&gt; SRR1383390     2  0.0892    0.90450 0.000 0.980 0.020
#&gt; SRR1383394     2  0.0592    0.90393 0.000 0.988 0.012
#&gt; SRR1383393     1  0.0237    1.00000 0.996 0.000 0.004
#&gt; SRR1383396     2  0.1999    0.89951 0.036 0.952 0.012
#&gt; SRR1383395     2  0.5094    0.81686 0.040 0.824 0.136
#&gt; SRR1383399     3  0.0000    0.80196 0.000 0.000 1.000
#&gt; SRR1383400     1  0.0237    1.00000 0.996 0.000 0.004
#&gt; SRR1383397     2  0.3572    0.87053 0.040 0.900 0.060
#&gt; SRR1383401     2  0.2878    0.85729 0.000 0.904 0.096
#&gt; SRR1383398     2  0.3572    0.87053 0.040 0.900 0.060
#&gt; SRR1383402     2  0.0892    0.90450 0.000 0.980 0.020
#&gt; SRR1383404     2  0.1647    0.89777 0.036 0.960 0.004
#&gt; SRR1383403     1  0.0237    1.00000 0.996 0.000 0.004
#&gt; SRR1383405     2  0.2096    0.88394 0.004 0.944 0.052
#&gt; SRR1383406     2  0.2269    0.89466 0.040 0.944 0.016
#&gt; SRR1383407     2  0.6225    0.00235 0.000 0.568 0.432
#&gt; SRR1383408     2  0.0892    0.90450 0.000 0.980 0.020
#&gt; SRR1383409     2  0.0892    0.90450 0.000 0.980 0.020
#&gt; SRR1383410     2  0.0892    0.90450 0.000 0.980 0.020
</code></pre>

<script>
$('#tab-MAD-mclust-get-classes-2-a').parent().next().next().hide();
$('#tab-MAD-mclust-get-classes-2-a').click(function(){
  $('#tab-MAD-mclust-get-classes-2-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-MAD-mclust-get-classes-3'>
<p><a id='tab-MAD-mclust-get-classes-3-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 4), get_membership(res, k = 4))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4
#&gt; SRR1383358     3  0.0188     0.8236 0.000 0.004 0.996 0.000
#&gt; SRR1383360     3  0.8368     0.3482 0.068 0.128 0.488 0.316
#&gt; SRR1383359     3  0.0188     0.8236 0.000 0.004 0.996 0.000
#&gt; SRR1383362     1  0.0469     0.9646 0.988 0.000 0.000 0.012
#&gt; SRR1383361     3  0.3105     0.7991 0.000 0.140 0.856 0.004
#&gt; SRR1383363     3  0.2334     0.8199 0.000 0.088 0.908 0.004
#&gt; SRR1383364     3  0.0000     0.8217 0.000 0.000 1.000 0.000
#&gt; SRR1383365     3  0.0188     0.8236 0.000 0.004 0.996 0.000
#&gt; SRR1383366     3  0.5867     0.6728 0.000 0.216 0.688 0.096
#&gt; SRR1383367     3  0.3908     0.7541 0.000 0.212 0.784 0.004
#&gt; SRR1383368     3  0.8493     0.4963 0.084 0.196 0.532 0.188
#&gt; SRR1383369     3  0.0188     0.8236 0.000 0.004 0.996 0.000
#&gt; SRR1383370     3  0.4697     0.6651 0.000 0.296 0.696 0.008
#&gt; SRR1383371     3  0.0000     0.8217 0.000 0.000 1.000 0.000
#&gt; SRR1383372     3  0.4103     0.7154 0.000 0.256 0.744 0.000
#&gt; SRR1383373     3  0.2149     0.8201 0.000 0.088 0.912 0.000
#&gt; SRR1383374     2  0.4985    -0.1815 0.000 0.532 0.468 0.000
#&gt; SRR1383375     1  0.1474     0.9727 0.948 0.000 0.000 0.052
#&gt; SRR1383376     2  0.0188     0.8113 0.000 0.996 0.000 0.004
#&gt; SRR1383377     4  0.7883    -0.1256 0.000 0.352 0.284 0.364
#&gt; SRR1383378     4  0.5883     0.4465 0.040 0.388 0.000 0.572
#&gt; SRR1383379     4  0.1867     0.7673 0.000 0.072 0.000 0.928
#&gt; SRR1383380     4  0.0592     0.7372 0.000 0.016 0.000 0.984
#&gt; SRR1383381     3  0.0188     0.8221 0.000 0.000 0.996 0.004
#&gt; SRR1383382     1  0.0469     0.9646 0.988 0.000 0.000 0.012
#&gt; SRR1383383     2  0.0000     0.8119 0.000 1.000 0.000 0.000
#&gt; SRR1383385     1  0.1557     0.9725 0.944 0.000 0.000 0.056
#&gt; SRR1383384     2  0.0000     0.8119 0.000 1.000 0.000 0.000
#&gt; SRR1383386     4  0.6488     0.5801 0.244 0.128 0.000 0.628
#&gt; SRR1383387     2  0.4730     0.3298 0.000 0.636 0.000 0.364
#&gt; SRR1383389     2  0.5172     0.0447 0.000 0.588 0.404 0.008
#&gt; SRR1383391     2  0.0000     0.8119 0.000 1.000 0.000 0.000
#&gt; SRR1383388     4  0.3894     0.7540 0.068 0.088 0.000 0.844
#&gt; SRR1383392     2  0.0524     0.8100 0.000 0.988 0.004 0.008
#&gt; SRR1383390     2  0.0000     0.8119 0.000 1.000 0.000 0.000
#&gt; SRR1383394     2  0.0469     0.8094 0.000 0.988 0.000 0.012
#&gt; SRR1383393     1  0.1557     0.9725 0.944 0.000 0.000 0.056
#&gt; SRR1383396     4  0.6098     0.5574 0.068 0.316 0.000 0.616
#&gt; SRR1383395     2  0.7563     0.1217 0.000 0.440 0.196 0.364
#&gt; SRR1383399     3  0.0188     0.8221 0.000 0.000 0.996 0.004
#&gt; SRR1383400     1  0.0469     0.9646 0.988 0.000 0.000 0.012
#&gt; SRR1383397     4  0.1867     0.7673 0.000 0.072 0.000 0.928
#&gt; SRR1383401     2  0.1256     0.7913 0.000 0.964 0.028 0.008
#&gt; SRR1383398     4  0.0592     0.7372 0.000 0.016 0.000 0.984
#&gt; SRR1383402     2  0.0336     0.8100 0.000 0.992 0.000 0.008
#&gt; SRR1383404     4  0.4940     0.7301 0.096 0.128 0.000 0.776
#&gt; SRR1383403     1  0.1557     0.9725 0.944 0.000 0.000 0.056
#&gt; SRR1383405     2  0.4730     0.3298 0.000 0.636 0.000 0.364
#&gt; SRR1383406     4  0.1867     0.7673 0.000 0.072 0.000 0.928
#&gt; SRR1383407     3  0.5060     0.4664 0.000 0.412 0.584 0.004
#&gt; SRR1383408     2  0.0000     0.8119 0.000 1.000 0.000 0.000
#&gt; SRR1383409     2  0.0000     0.8119 0.000 1.000 0.000 0.000
#&gt; SRR1383410     2  0.0469     0.8094 0.000 0.988 0.000 0.012
</code></pre>

<script>
$('#tab-MAD-mclust-get-classes-3-a').parent().next().next().hide();
$('#tab-MAD-mclust-get-classes-3-a').click(function(){
  $('#tab-MAD-mclust-get-classes-3-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-MAD-mclust-get-classes-4'>
<p><a id='tab-MAD-mclust-get-classes-4-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 5), get_membership(res, k = 5))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4    p5
#&gt; SRR1383358     5  0.1608     0.6676 0.000 0.000 0.072 0.000 0.928
#&gt; SRR1383360     3  0.6857     0.4046 0.124 0.004 0.616 0.112 0.144
#&gt; SRR1383359     5  0.0000     0.7029 0.000 0.000 0.000 0.000 1.000
#&gt; SRR1383362     1  0.1197     0.9322 0.952 0.000 0.048 0.000 0.000
#&gt; SRR1383361     5  0.5227    -0.0154 0.000 0.044 0.448 0.000 0.508
#&gt; SRR1383363     5  0.4538     0.1324 0.000 0.008 0.452 0.000 0.540
#&gt; SRR1383364     5  0.0162     0.7018 0.000 0.000 0.004 0.000 0.996
#&gt; SRR1383365     5  0.0000     0.7029 0.000 0.000 0.000 0.000 1.000
#&gt; SRR1383366     3  0.8547     0.4720 0.012 0.132 0.368 0.260 0.228
#&gt; SRR1383367     3  0.5761     0.0843 0.000 0.088 0.492 0.000 0.420
#&gt; SRR1383368     3  0.6824     0.4060 0.116 0.008 0.628 0.124 0.124
#&gt; SRR1383369     5  0.0324     0.7003 0.000 0.004 0.004 0.000 0.992
#&gt; SRR1383370     3  0.7304     0.4695 0.000 0.244 0.404 0.028 0.324
#&gt; SRR1383371     5  0.0162     0.7018 0.000 0.000 0.004 0.000 0.996
#&gt; SRR1383372     3  0.7967     0.4952 0.000 0.204 0.376 0.096 0.324
#&gt; SRR1383373     5  0.1568     0.6701 0.000 0.020 0.036 0.000 0.944
#&gt; SRR1383374     2  0.7708    -0.3987 0.000 0.396 0.360 0.092 0.152
#&gt; SRR1383375     1  0.0880     0.9452 0.968 0.000 0.000 0.032 0.000
#&gt; SRR1383376     2  0.1341     0.7349 0.000 0.944 0.000 0.056 0.000
#&gt; SRR1383377     4  0.6897    -0.1277 0.000 0.140 0.332 0.492 0.036
#&gt; SRR1383378     4  0.6350     0.5152 0.024 0.092 0.380 0.504 0.000
#&gt; SRR1383379     4  0.0703     0.6613 0.000 0.024 0.000 0.976 0.000
#&gt; SRR1383380     4  0.0912     0.6507 0.016 0.000 0.012 0.972 0.000
#&gt; SRR1383381     5  0.4283     0.1713 0.000 0.000 0.456 0.000 0.544
#&gt; SRR1383382     1  0.2416     0.9128 0.888 0.000 0.100 0.012 0.000
#&gt; SRR1383383     2  0.1638     0.7225 0.000 0.932 0.064 0.000 0.004
#&gt; SRR1383385     1  0.1211     0.9456 0.960 0.000 0.016 0.024 0.000
#&gt; SRR1383384     2  0.0000     0.7194 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1383386     4  0.6566     0.5480 0.120 0.024 0.352 0.504 0.000
#&gt; SRR1383387     2  0.5009     0.3092 0.000 0.540 0.032 0.428 0.000
#&gt; SRR1383389     2  0.7255    -0.2044 0.000 0.416 0.400 0.108 0.076
#&gt; SRR1383391     2  0.2914     0.7313 0.000 0.872 0.076 0.052 0.000
#&gt; SRR1383388     4  0.5462     0.6197 0.064 0.024 0.244 0.668 0.000
#&gt; SRR1383392     2  0.5113     0.5427 0.000 0.708 0.160 0.128 0.004
#&gt; SRR1383390     2  0.1608     0.7208 0.000 0.928 0.072 0.000 0.000
#&gt; SRR1383394     2  0.1732     0.7305 0.000 0.920 0.000 0.080 0.000
#&gt; SRR1383393     1  0.1041     0.9447 0.964 0.000 0.004 0.032 0.000
#&gt; SRR1383396     4  0.6692     0.5600 0.072 0.028 0.364 0.516 0.020
#&gt; SRR1383395     4  0.6897    -0.1277 0.000 0.140 0.332 0.492 0.036
#&gt; SRR1383399     5  0.4278     0.1778 0.000 0.000 0.452 0.000 0.548
#&gt; SRR1383400     1  0.2416     0.9128 0.888 0.000 0.100 0.012 0.000
#&gt; SRR1383397     4  0.1364     0.6559 0.000 0.036 0.012 0.952 0.000
#&gt; SRR1383401     2  0.6223     0.4835 0.000 0.628 0.208 0.128 0.036
#&gt; SRR1383398     4  0.0912     0.6507 0.016 0.000 0.012 0.972 0.000
#&gt; SRR1383402     2  0.1478     0.7344 0.000 0.936 0.000 0.064 0.000
#&gt; SRR1383404     4  0.6093     0.5828 0.076 0.024 0.348 0.552 0.000
#&gt; SRR1383403     1  0.1211     0.9456 0.960 0.000 0.016 0.024 0.000
#&gt; SRR1383405     2  0.5009     0.3092 0.000 0.540 0.032 0.428 0.000
#&gt; SRR1383406     4  0.1485     0.6595 0.000 0.032 0.020 0.948 0.000
#&gt; SRR1383407     3  0.6549     0.3960 0.000 0.348 0.504 0.020 0.128
#&gt; SRR1383408     2  0.1410     0.7242 0.000 0.940 0.060 0.000 0.000
#&gt; SRR1383409     2  0.1341     0.7246 0.000 0.944 0.056 0.000 0.000
#&gt; SRR1383410     2  0.2694     0.7069 0.000 0.864 0.004 0.128 0.004
</code></pre>

<script>
$('#tab-MAD-mclust-get-classes-4-a').parent().next().next().hide();
$('#tab-MAD-mclust-get-classes-4-a').click(function(){
  $('#tab-MAD-mclust-get-classes-4-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-MAD-mclust-get-classes-5'>
<p><a id='tab-MAD-mclust-get-classes-5-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 6), get_membership(res, k = 6))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4    p5    p6
#&gt; SRR1383358     5  0.2178     0.7501 0.000 0.000 0.132 0.000 0.868 0.000
#&gt; SRR1383360     3  0.8001     0.1601 0.028 0.000 0.316 0.192 0.156 0.308
#&gt; SRR1383359     5  0.1167     0.8631 0.008 0.000 0.020 0.012 0.960 0.000
#&gt; SRR1383362     1  0.3717     0.8215 0.776 0.000 0.160 0.000 0.000 0.064
#&gt; SRR1383361     3  0.4139     0.5225 0.000 0.024 0.640 0.000 0.336 0.000
#&gt; SRR1383363     3  0.3714     0.4932 0.000 0.004 0.656 0.000 0.340 0.000
#&gt; SRR1383364     5  0.2365     0.8334 0.000 0.000 0.072 0.000 0.888 0.040
#&gt; SRR1383365     5  0.1082     0.8719 0.000 0.004 0.040 0.000 0.956 0.000
#&gt; SRR1383366     3  0.7883     0.4760 0.020 0.128 0.376 0.244 0.228 0.004
#&gt; SRR1383367     3  0.4408     0.5557 0.000 0.056 0.664 0.000 0.280 0.000
#&gt; SRR1383368     3  0.7823     0.2813 0.028 0.000 0.360 0.136 0.168 0.308
#&gt; SRR1383369     5  0.0937     0.8719 0.000 0.000 0.040 0.000 0.960 0.000
#&gt; SRR1383370     3  0.6582     0.5455 0.016 0.216 0.532 0.028 0.204 0.004
#&gt; SRR1383371     5  0.2221     0.8374 0.000 0.000 0.072 0.000 0.896 0.032
#&gt; SRR1383372     3  0.6565     0.5478 0.000 0.136 0.532 0.100 0.232 0.000
#&gt; SRR1383373     5  0.2668     0.7932 0.000 0.004 0.168 0.000 0.828 0.000
#&gt; SRR1383374     2  0.7615    -0.1430 0.000 0.324 0.264 0.232 0.180 0.000
#&gt; SRR1383375     1  0.0146     0.8529 0.996 0.000 0.000 0.000 0.000 0.004
#&gt; SRR1383376     2  0.1471     0.7662 0.000 0.932 0.000 0.064 0.000 0.004
#&gt; SRR1383377     4  0.5374     0.3125 0.000 0.052 0.276 0.624 0.044 0.004
#&gt; SRR1383378     6  0.4467     0.7678 0.004 0.040 0.072 0.120 0.000 0.764
#&gt; SRR1383379     4  0.3349     0.4951 0.000 0.008 0.000 0.748 0.000 0.244
#&gt; SRR1383380     4  0.3126     0.5215 0.000 0.000 0.000 0.752 0.000 0.248
#&gt; SRR1383381     3  0.3984     0.4167 0.000 0.000 0.596 0.000 0.396 0.008
#&gt; SRR1383382     1  0.5142     0.7700 0.648 0.000 0.240 0.020 0.000 0.092
#&gt; SRR1383383     2  0.2009     0.7643 0.000 0.908 0.068 0.000 0.000 0.024
#&gt; SRR1383385     1  0.1141     0.8464 0.948 0.000 0.000 0.000 0.000 0.052
#&gt; SRR1383384     2  0.0000     0.7591 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1383386     6  0.3324     0.8209 0.060 0.004 0.000 0.112 0.000 0.824
#&gt; SRR1383387     4  0.4039     0.2712 0.000 0.424 0.000 0.568 0.000 0.008
#&gt; SRR1383389     2  0.7360    -0.0168 0.000 0.404 0.360 0.112 0.080 0.044
#&gt; SRR1383391     2  0.3969     0.7451 0.000 0.800 0.084 0.076 0.000 0.040
#&gt; SRR1383388     6  0.3983     0.6270 0.004 0.008 0.000 0.348 0.000 0.640
#&gt; SRR1383392     2  0.5149     0.6207 0.000 0.652 0.072 0.244 0.032 0.000
#&gt; SRR1383390     2  0.2249     0.7586 0.000 0.900 0.064 0.004 0.000 0.032
#&gt; SRR1383394     2  0.1858     0.7596 0.000 0.904 0.000 0.092 0.000 0.004
#&gt; SRR1383393     1  0.0935     0.8331 0.964 0.000 0.000 0.032 0.000 0.004
#&gt; SRR1383396     6  0.3704     0.8211 0.024 0.020 0.016 0.088 0.016 0.836
#&gt; SRR1383395     4  0.5444     0.3258 0.000 0.060 0.268 0.624 0.044 0.004
#&gt; SRR1383399     3  0.3984     0.4167 0.000 0.000 0.596 0.000 0.396 0.008
#&gt; SRR1383400     1  0.5142     0.7700 0.648 0.000 0.240 0.020 0.000 0.092
#&gt; SRR1383397     4  0.3052     0.5274 0.000 0.004 0.000 0.780 0.000 0.216
#&gt; SRR1383401     2  0.5224     0.6421 0.000 0.616 0.136 0.244 0.004 0.000
#&gt; SRR1383398     4  0.3126     0.5215 0.000 0.000 0.000 0.752 0.000 0.248
#&gt; SRR1383402     2  0.1663     0.7614 0.000 0.912 0.000 0.088 0.000 0.000
#&gt; SRR1383404     6  0.3313     0.8201 0.024 0.008 0.000 0.160 0.000 0.808
#&gt; SRR1383403     1  0.1141     0.8464 0.948 0.000 0.000 0.000 0.000 0.052
#&gt; SRR1383405     4  0.3833     0.2299 0.000 0.444 0.000 0.556 0.000 0.000
#&gt; SRR1383406     4  0.3133     0.5291 0.000 0.008 0.000 0.780 0.000 0.212
#&gt; SRR1383407     3  0.5371     0.3491 0.000 0.300 0.612 0.012 0.044 0.032
#&gt; SRR1383408     2  0.1333     0.7669 0.000 0.944 0.048 0.000 0.000 0.008
#&gt; SRR1383409     2  0.1524     0.7676 0.000 0.932 0.060 0.000 0.000 0.008
#&gt; SRR1383410     2  0.3171     0.7146 0.000 0.784 0.012 0.204 0.000 0.000
</code></pre>

<script>
$('#tab-MAD-mclust-get-classes-5-a').parent().next().next().hide();
$('#tab-MAD-mclust-get-classes-5-a').click(function(){
  $('#tab-MAD-mclust-get-classes-5-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>
</div>

Heatmaps for the consensus matrix. It visualizes the probability of two
samples to be in a same group.



<script>
$( function() {
	$( '#tabs-MAD-mclust-consensus-heatmap' ).tabs();
} );
</script>
<div id='tabs-MAD-mclust-consensus-heatmap'>
<ul>
<li><a href='#tab-MAD-mclust-consensus-heatmap-1'>k = 2</a></li>
<li><a href='#tab-MAD-mclust-consensus-heatmap-2'>k = 3</a></li>
<li><a href='#tab-MAD-mclust-consensus-heatmap-3'>k = 4</a></li>
<li><a href='#tab-MAD-mclust-consensus-heatmap-4'>k = 5</a></li>
<li><a href='#tab-MAD-mclust-consensus-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-MAD-mclust-consensus-heatmap-1'>
<pre><code class="r">consensus_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-MAD-mclust-consensus-heatmap-1-1.png" alt="plot of chunk tab-MAD-mclust-consensus-heatmap-1"/></p>

</div>
<div id='tab-MAD-mclust-consensus-heatmap-2'>
<pre><code class="r">consensus_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-MAD-mclust-consensus-heatmap-2-1.png" alt="plot of chunk tab-MAD-mclust-consensus-heatmap-2"/></p>

</div>
<div id='tab-MAD-mclust-consensus-heatmap-3'>
<pre><code class="r">consensus_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-MAD-mclust-consensus-heatmap-3-1.png" alt="plot of chunk tab-MAD-mclust-consensus-heatmap-3"/></p>

</div>
<div id='tab-MAD-mclust-consensus-heatmap-4'>
<pre><code class="r">consensus_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-MAD-mclust-consensus-heatmap-4-1.png" alt="plot of chunk tab-MAD-mclust-consensus-heatmap-4"/></p>

</div>
<div id='tab-MAD-mclust-consensus-heatmap-5'>
<pre><code class="r">consensus_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-MAD-mclust-consensus-heatmap-5-1.png" alt="plot of chunk tab-MAD-mclust-consensus-heatmap-5"/></p>

</div>
</div>

Heatmaps for the membership of samples in all partitions to see how consistent they are:




<script>
$( function() {
	$( '#tabs-MAD-mclust-membership-heatmap' ).tabs();
} );
</script>
<div id='tabs-MAD-mclust-membership-heatmap'>
<ul>
<li><a href='#tab-MAD-mclust-membership-heatmap-1'>k = 2</a></li>
<li><a href='#tab-MAD-mclust-membership-heatmap-2'>k = 3</a></li>
<li><a href='#tab-MAD-mclust-membership-heatmap-3'>k = 4</a></li>
<li><a href='#tab-MAD-mclust-membership-heatmap-4'>k = 5</a></li>
<li><a href='#tab-MAD-mclust-membership-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-MAD-mclust-membership-heatmap-1'>
<pre><code class="r">membership_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-MAD-mclust-membership-heatmap-1-1.png" alt="plot of chunk tab-MAD-mclust-membership-heatmap-1"/></p>

</div>
<div id='tab-MAD-mclust-membership-heatmap-2'>
<pre><code class="r">membership_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-MAD-mclust-membership-heatmap-2-1.png" alt="plot of chunk tab-MAD-mclust-membership-heatmap-2"/></p>

</div>
<div id='tab-MAD-mclust-membership-heatmap-3'>
<pre><code class="r">membership_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-MAD-mclust-membership-heatmap-3-1.png" alt="plot of chunk tab-MAD-mclust-membership-heatmap-3"/></p>

</div>
<div id='tab-MAD-mclust-membership-heatmap-4'>
<pre><code class="r">membership_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-MAD-mclust-membership-heatmap-4-1.png" alt="plot of chunk tab-MAD-mclust-membership-heatmap-4"/></p>

</div>
<div id='tab-MAD-mclust-membership-heatmap-5'>
<pre><code class="r">membership_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-MAD-mclust-membership-heatmap-5-1.png" alt="plot of chunk tab-MAD-mclust-membership-heatmap-5"/></p>

</div>
</div>

As soon as we have had the classes for columns, we can look for signatures
which are significantly different between classes which can be candidate marks
for certain classes. Following are the heatmaps for signatures.



Signature heatmaps where rows are scaled:



<script>
$( function() {
	$( '#tabs-MAD-mclust-get-signatures' ).tabs();
} );
</script>
<div id='tabs-MAD-mclust-get-signatures'>
<ul>
<li><a href='#tab-MAD-mclust-get-signatures-1'>k = 2</a></li>
<li><a href='#tab-MAD-mclust-get-signatures-2'>k = 3</a></li>
<li><a href='#tab-MAD-mclust-get-signatures-3'>k = 4</a></li>
<li><a href='#tab-MAD-mclust-get-signatures-4'>k = 5</a></li>
<li><a href='#tab-MAD-mclust-get-signatures-5'>k = 6</a></li>
</ul>
<div id='tab-MAD-mclust-get-signatures-1'>
<pre><code class="r">get_signatures(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-MAD-mclust-get-signatures-1-1.png" alt="plot of chunk tab-MAD-mclust-get-signatures-1"/></p>

</div>
<div id='tab-MAD-mclust-get-signatures-2'>
<pre><code class="r">get_signatures(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-MAD-mclust-get-signatures-2-1.png" alt="plot of chunk tab-MAD-mclust-get-signatures-2"/></p>

</div>
<div id='tab-MAD-mclust-get-signatures-3'>
<pre><code class="r">get_signatures(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-MAD-mclust-get-signatures-3-1.png" alt="plot of chunk tab-MAD-mclust-get-signatures-3"/></p>

</div>
<div id='tab-MAD-mclust-get-signatures-4'>
<pre><code class="r">get_signatures(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-MAD-mclust-get-signatures-4-1.png" alt="plot of chunk tab-MAD-mclust-get-signatures-4"/></p>

</div>
<div id='tab-MAD-mclust-get-signatures-5'>
<pre><code class="r">get_signatures(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-MAD-mclust-get-signatures-5-1.png" alt="plot of chunk tab-MAD-mclust-get-signatures-5"/></p>

</div>
</div>



Signature heatmaps where rows are not scaled:


<script>
$( function() {
	$( '#tabs-MAD-mclust-get-signatures-no-scale' ).tabs();
} );
</script>
<div id='tabs-MAD-mclust-get-signatures-no-scale'>
<ul>
<li><a href='#tab-MAD-mclust-get-signatures-no-scale-1'>k = 2</a></li>
<li><a href='#tab-MAD-mclust-get-signatures-no-scale-2'>k = 3</a></li>
<li><a href='#tab-MAD-mclust-get-signatures-no-scale-3'>k = 4</a></li>
<li><a href='#tab-MAD-mclust-get-signatures-no-scale-4'>k = 5</a></li>
<li><a href='#tab-MAD-mclust-get-signatures-no-scale-5'>k = 6</a></li>
</ul>
<div id='tab-MAD-mclust-get-signatures-no-scale-1'>
<pre><code class="r">get_signatures(res, k = 2, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-MAD-mclust-get-signatures-no-scale-1-1.png" alt="plot of chunk tab-MAD-mclust-get-signatures-no-scale-1"/></p>

</div>
<div id='tab-MAD-mclust-get-signatures-no-scale-2'>
<pre><code class="r">get_signatures(res, k = 3, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-MAD-mclust-get-signatures-no-scale-2-1.png" alt="plot of chunk tab-MAD-mclust-get-signatures-no-scale-2"/></p>

</div>
<div id='tab-MAD-mclust-get-signatures-no-scale-3'>
<pre><code class="r">get_signatures(res, k = 4, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-MAD-mclust-get-signatures-no-scale-3-1.png" alt="plot of chunk tab-MAD-mclust-get-signatures-no-scale-3"/></p>

</div>
<div id='tab-MAD-mclust-get-signatures-no-scale-4'>
<pre><code class="r">get_signatures(res, k = 5, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-MAD-mclust-get-signatures-no-scale-4-1.png" alt="plot of chunk tab-MAD-mclust-get-signatures-no-scale-4"/></p>

</div>
<div id='tab-MAD-mclust-get-signatures-no-scale-5'>
<pre><code class="r">get_signatures(res, k = 6, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-MAD-mclust-get-signatures-no-scale-5-1.png" alt="plot of chunk tab-MAD-mclust-get-signatures-no-scale-5"/></p>

</div>
</div>



Compare the overlap of signatures from different k:

```r
compare_signatures(res)
```

![plot of chunk MAD-mclust-signature_compare](figure_cola/MAD-mclust-signature_compare-1.png)

`get_signature()` returns a data frame invisibly. TO get the list of signatures, the function
call should be assigned to a variable explicitly. In following code, if `plot` argument is set
to `FALSE`, no heatmap is plotted while only the differential analysis is performed.

```r
# code only for demonstration
tb = get_signature(res, k = ..., plot = FALSE)
```

An example of the output of `tb` is:

```
#>   which_row         fdr    mean_1    mean_2 scaled_mean_1 scaled_mean_2 km
#> 1        38 0.042760348  8.373488  9.131774    -0.5533452     0.5164555  1
#> 2        40 0.018707592  7.106213  8.469186    -0.6173731     0.5762149  1
#> 3        55 0.019134737 10.221463 11.207825    -0.6159697     0.5749050  1
#> 4        59 0.006059896  5.921854  7.869574    -0.6899429     0.6439467  1
#> 5        60 0.018055526  8.928898 10.211722    -0.6204761     0.5791110  1
#> 6        98 0.009384629 15.714769 14.887706     0.6635654    -0.6193277  2
...
```

The columns in `tb` are:

1. `which_row`: row indices corresponding to the input matrix.
2. `fdr`: FDR for the differential test. 
3. `mean_x`: The mean value in group x.
4. `scaled_mean_x`: The mean value in group x after rows are scaled.
5. `km`: Row groups if k-means clustering is applied to rows.



UMAP plot which shows how samples are separated.


<script>
$( function() {
	$( '#tabs-MAD-mclust-dimension-reduction' ).tabs();
} );
</script>
<div id='tabs-MAD-mclust-dimension-reduction'>
<ul>
<li><a href='#tab-MAD-mclust-dimension-reduction-1'>k = 2</a></li>
<li><a href='#tab-MAD-mclust-dimension-reduction-2'>k = 3</a></li>
<li><a href='#tab-MAD-mclust-dimension-reduction-3'>k = 4</a></li>
<li><a href='#tab-MAD-mclust-dimension-reduction-4'>k = 5</a></li>
<li><a href='#tab-MAD-mclust-dimension-reduction-5'>k = 6</a></li>
</ul>
<div id='tab-MAD-mclust-dimension-reduction-1'>
<pre><code class="r">dimension_reduction(res, k = 2, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-MAD-mclust-dimension-reduction-1-1.png" alt="plot of chunk tab-MAD-mclust-dimension-reduction-1"/></p>

</div>
<div id='tab-MAD-mclust-dimension-reduction-2'>
<pre><code class="r">dimension_reduction(res, k = 3, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-MAD-mclust-dimension-reduction-2-1.png" alt="plot of chunk tab-MAD-mclust-dimension-reduction-2"/></p>

</div>
<div id='tab-MAD-mclust-dimension-reduction-3'>
<pre><code class="r">dimension_reduction(res, k = 4, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-MAD-mclust-dimension-reduction-3-1.png" alt="plot of chunk tab-MAD-mclust-dimension-reduction-3"/></p>

</div>
<div id='tab-MAD-mclust-dimension-reduction-4'>
<pre><code class="r">dimension_reduction(res, k = 5, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-MAD-mclust-dimension-reduction-4-1.png" alt="plot of chunk tab-MAD-mclust-dimension-reduction-4"/></p>

</div>
<div id='tab-MAD-mclust-dimension-reduction-5'>
<pre><code class="r">dimension_reduction(res, k = 6, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-MAD-mclust-dimension-reduction-5-1.png" alt="plot of chunk tab-MAD-mclust-dimension-reduction-5"/></p>

</div>
</div>


Following heatmap shows how subgroups are split when increasing `k`:

```r
collect_classes(res)
```

![plot of chunk MAD-mclust-collect-classes](figure_cola/MAD-mclust-collect-classes-1.png)


If matrix rows can be associated to genes, consider to use `functional_enrichment(res,
...)` to perform function enrichment for the signature genes. See [this vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/functional_enrichment.html) for more detailed explanations.


 

---------------------------------------------------




### MAD:NMF**






The object with results only for a single top-value method and a single partition method 
can be extracted as:

```r
res = res_list["MAD", "NMF"]
# you can also extract it by
# res = res_list["MAD:NMF"]
```

A summary of `res` and all the functions that can be applied to it:

```r
res
```

```
#> A 'ConsensusPartition' object with k = 2, 3, 4, 5, 6.
#>   On a matrix with 15680 rows and 53 columns.
#>   Top rows (1000, 2000, 3000, 4000, 5000) are extracted by 'MAD' method.
#>   Subgroups are detected by 'NMF' method.
#>   Performed in total 1250 partitions by row resampling.
#>   Best k for subgroups seems to be 2.
#> 
#> Following methods can be applied to this 'ConsensusPartition' object:
#>  [1] "cola_report"             "collect_classes"         "collect_plots"          
#>  [4] "collect_stats"           "colnames"                "compare_signatures"     
#>  [7] "consensus_heatmap"       "dimension_reduction"     "functional_enrichment"  
#> [10] "get_anno_col"            "get_anno"                "get_classes"            
#> [13] "get_consensus"           "get_matrix"              "get_membership"         
#> [16] "get_param"               "get_signatures"          "get_stats"              
#> [19] "is_best_k"               "is_stable_k"             "membership_heatmap"     
#> [22] "ncol"                    "nrow"                    "plot_ecdf"              
#> [25] "rownames"                "select_partition_number" "show"                   
#> [28] "suggest_best_k"          "test_to_known_factors"
```

`collect_plots()` function collects all the plots made from `res` for all `k` (number of partitions)
into one single page to provide an easy and fast comparison between different `k`.

```r
collect_plots(res)
```

![plot of chunk MAD-NMF-collect-plots](figure_cola/MAD-NMF-collect-plots-1.png)

The plots are:

- The first row: a plot of the ECDF (empirical cumulative distribution
  function) curves of the consensus matrix for each `k` and the heatmap of
  predicted classes for each `k`.
- The second row: heatmaps of the consensus matrix for each `k`.
- The third row: heatmaps of the membership matrix for each `k`.
- The fouth row: heatmaps of the signatures for each `k`.

All the plots in panels can be made by individual functions and they are
plotted later in this section.

`select_partition_number()` produces several plots showing different
statistics for choosing "optimized" `k`. There are following statistics:

- ECDF curves of the consensus matrix for each `k`;
- 1-PAC. [The PAC
  score](https://en.wikipedia.org/wiki/Consensus_clustering#Over-interpretation_potential_of_consensus_clustering)
  measures the proportion of the ambiguous subgrouping.
- Mean silhouette score.
- Concordance. The mean probability of fiting the consensus class ids in all
  partitions.
- Area increased. Denote $A_k$ as the area under the ECDF curve for current
  `k`, the area increased is defined as $A_k - A_{k-1}$.
- Rand index. The percent of pairs of samples that are both in a same cluster
  or both are not in a same cluster in the partition of k and k-1.
- Jaccard index. The ratio of pairs of samples are both in a same cluster in
  the partition of k and k-1 and the pairs of samples are both in a same
  cluster in the partition k or k-1.

The detailed explanations of these statistics can be found in [the _cola_
vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/cola.html#toc_13).

Generally speaking, lower PAC score, higher mean silhouette score or higher
concordance corresponds to better partition. Rand index and Jaccard index
measure how similar the current partition is compared to partition with `k-1`.
If they are too similar, we won't accept `k` is better than `k-1`.

```r
select_partition_number(res)
```

![plot of chunk MAD-NMF-select-partition-number](figure_cola/MAD-NMF-select-partition-number-1.png)

The numeric values for all these statistics can be obtained by `get_stats()`.

```r
get_stats(res)
```

```
#>   k 1-PAC mean_silhouette concordance area_increased  Rand Jaccard
#> 2 2 1.000           0.956       0.982         0.4240 0.570   0.570
#> 3 3 0.732           0.837       0.929         0.5512 0.660   0.460
#> 4 4 0.633           0.721       0.843         0.1167 0.853   0.615
#> 5 5 0.858           0.864       0.930         0.0806 0.902   0.657
#> 6 6 0.709           0.592       0.791         0.0326 0.919   0.649
```

`suggest_best_k()` suggests the best $k$ based on these statistics. The rules are as follows:

- All $k$ with Jaccard index larger than 0.95 are removed because increasing
  $k$ does not provide enough extra information. If all $k$ are removed, it is
  marked as no subgroup is detected.
- For all $k$ with 1-PAC score larger than 0.9, the maximal $k$ is taken as
  the best $k$, and other $k$ are marked as optional $k$.
- If it does not fit the second rule. The $k$ with the maximal vote of the
  highest 1-PAC score, highest mean silhouette, and highest concordance is
  taken as the best $k$.

```r
suggest_best_k(res)
```

```
#> [1] 2
```


Following shows the table of the partitions (You need to click the **show/hide
code output** link to see it). The membership matrix (columns with name `p*`)
is inferred by
[`clue::cl_consensus()`](https://www.rdocumentation.org/link/cl_consensus?package=clue)
function with the `SE` method. Basically the value in the membership matrix
represents the probability to belong to a certain group. The finall class
label for an item is determined with the group with highest probability it
belongs to.

In `get_classes()` function, the entropy is calculated from the membership
matrix and the silhouette score is calculated from the consensus matrix.



<script>
$( function() {
	$( '#tabs-MAD-NMF-get-classes' ).tabs();
} );
</script>
<div id='tabs-MAD-NMF-get-classes'>
<ul>
<li><a href='#tab-MAD-NMF-get-classes-1'>k = 2</a></li>
<li><a href='#tab-MAD-NMF-get-classes-2'>k = 3</a></li>
<li><a href='#tab-MAD-NMF-get-classes-3'>k = 4</a></li>
<li><a href='#tab-MAD-NMF-get-classes-4'>k = 5</a></li>
<li><a href='#tab-MAD-NMF-get-classes-5'>k = 6</a></li>
</ul>

<div id='tab-MAD-NMF-get-classes-1'>
<p><a id='tab-MAD-NMF-get-classes-1-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 2), get_membership(res, k = 2))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2
#&gt; SRR1383358     2  0.0000      0.991 0.000 1.000
#&gt; SRR1383360     1  0.9710      0.343 0.600 0.400
#&gt; SRR1383359     2  0.0000      0.991 0.000 1.000
#&gt; SRR1383362     1  0.0000      0.955 1.000 0.000
#&gt; SRR1383361     2  0.0000      0.991 0.000 1.000
#&gt; SRR1383363     2  0.0000      0.991 0.000 1.000
#&gt; SRR1383364     2  0.2043      0.959 0.032 0.968
#&gt; SRR1383365     2  0.0000      0.991 0.000 1.000
#&gt; SRR1383366     2  0.0000      0.991 0.000 1.000
#&gt; SRR1383367     2  0.0000      0.991 0.000 1.000
#&gt; SRR1383368     1  0.0376      0.953 0.996 0.004
#&gt; SRR1383369     2  0.0000      0.991 0.000 1.000
#&gt; SRR1383370     2  0.0000      0.991 0.000 1.000
#&gt; SRR1383371     2  0.0000      0.991 0.000 1.000
#&gt; SRR1383372     2  0.0000      0.991 0.000 1.000
#&gt; SRR1383373     2  0.0000      0.991 0.000 1.000
#&gt; SRR1383374     2  0.0000      0.991 0.000 1.000
#&gt; SRR1383375     1  0.0000      0.955 1.000 0.000
#&gt; SRR1383376     2  0.0000      0.991 0.000 1.000
#&gt; SRR1383377     2  0.0000      0.991 0.000 1.000
#&gt; SRR1383378     1  0.7299      0.745 0.796 0.204
#&gt; SRR1383379     2  0.8386      0.611 0.268 0.732
#&gt; SRR1383380     1  0.0672      0.951 0.992 0.008
#&gt; SRR1383381     2  0.0000      0.991 0.000 1.000
#&gt; SRR1383382     1  0.0000      0.955 1.000 0.000
#&gt; SRR1383383     2  0.0000      0.991 0.000 1.000
#&gt; SRR1383385     1  0.0000      0.955 1.000 0.000
#&gt; SRR1383384     2  0.0000      0.991 0.000 1.000
#&gt; SRR1383386     1  0.0000      0.955 1.000 0.000
#&gt; SRR1383387     2  0.0000      0.991 0.000 1.000
#&gt; SRR1383389     2  0.0000      0.991 0.000 1.000
#&gt; SRR1383391     2  0.0000      0.991 0.000 1.000
#&gt; SRR1383388     1  0.0000      0.955 1.000 0.000
#&gt; SRR1383392     2  0.0000      0.991 0.000 1.000
#&gt; SRR1383390     2  0.0000      0.991 0.000 1.000
#&gt; SRR1383394     2  0.0000      0.991 0.000 1.000
#&gt; SRR1383393     1  0.0000      0.955 1.000 0.000
#&gt; SRR1383396     1  0.0000      0.955 1.000 0.000
#&gt; SRR1383395     2  0.0000      0.991 0.000 1.000
#&gt; SRR1383399     2  0.0000      0.991 0.000 1.000
#&gt; SRR1383400     1  0.0000      0.955 1.000 0.000
#&gt; SRR1383397     2  0.0000      0.991 0.000 1.000
#&gt; SRR1383401     2  0.0000      0.991 0.000 1.000
#&gt; SRR1383398     1  0.2603      0.923 0.956 0.044
#&gt; SRR1383402     2  0.0000      0.991 0.000 1.000
#&gt; SRR1383404     1  0.0000      0.955 1.000 0.000
#&gt; SRR1383403     1  0.0000      0.955 1.000 0.000
#&gt; SRR1383405     2  0.0000      0.991 0.000 1.000
#&gt; SRR1383406     2  0.0672      0.983 0.008 0.992
#&gt; SRR1383407     2  0.0000      0.991 0.000 1.000
#&gt; SRR1383408     2  0.0000      0.991 0.000 1.000
#&gt; SRR1383409     2  0.0000      0.991 0.000 1.000
#&gt; SRR1383410     2  0.0000      0.991 0.000 1.000
</code></pre>

<script>
$('#tab-MAD-NMF-get-classes-1-a').parent().next().next().hide();
$('#tab-MAD-NMF-get-classes-1-a').click(function(){
  $('#tab-MAD-NMF-get-classes-1-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-MAD-NMF-get-classes-2'>
<p><a id='tab-MAD-NMF-get-classes-2-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 3), get_membership(res, k = 3))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3
#&gt; SRR1383358     3  0.0000      0.942 0.000 0.000 1.000
#&gt; SRR1383360     1  0.6215      0.227 0.572 0.000 0.428
#&gt; SRR1383359     3  0.0000      0.942 0.000 0.000 1.000
#&gt; SRR1383362     1  0.0000      0.939 1.000 0.000 0.000
#&gt; SRR1383361     3  0.0000      0.942 0.000 0.000 1.000
#&gt; SRR1383363     3  0.0000      0.942 0.000 0.000 1.000
#&gt; SRR1383364     3  0.0000      0.942 0.000 0.000 1.000
#&gt; SRR1383365     3  0.0000      0.942 0.000 0.000 1.000
#&gt; SRR1383366     3  0.5785      0.508 0.000 0.332 0.668
#&gt; SRR1383367     3  0.0000      0.942 0.000 0.000 1.000
#&gt; SRR1383368     1  0.0237      0.937 0.996 0.000 0.004
#&gt; SRR1383369     3  0.0000      0.942 0.000 0.000 1.000
#&gt; SRR1383370     3  0.4235      0.776 0.000 0.176 0.824
#&gt; SRR1383371     3  0.0000      0.942 0.000 0.000 1.000
#&gt; SRR1383372     3  0.0237      0.939 0.000 0.004 0.996
#&gt; SRR1383373     3  0.0000      0.942 0.000 0.000 1.000
#&gt; SRR1383374     3  0.2356      0.884 0.000 0.072 0.928
#&gt; SRR1383375     1  0.0000      0.939 1.000 0.000 0.000
#&gt; SRR1383376     2  0.0000      0.889 0.000 1.000 0.000
#&gt; SRR1383377     2  0.4235      0.749 0.000 0.824 0.176
#&gt; SRR1383378     2  0.5327      0.618 0.272 0.728 0.000
#&gt; SRR1383379     2  0.0000      0.889 0.000 1.000 0.000
#&gt; SRR1383380     2  0.6274      0.206 0.456 0.544 0.000
#&gt; SRR1383381     3  0.0000      0.942 0.000 0.000 1.000
#&gt; SRR1383382     1  0.0000      0.939 1.000 0.000 0.000
#&gt; SRR1383383     2  0.4235      0.761 0.000 0.824 0.176
#&gt; SRR1383385     1  0.0000      0.939 1.000 0.000 0.000
#&gt; SRR1383384     2  0.0237      0.889 0.000 0.996 0.004
#&gt; SRR1383386     1  0.0000      0.939 1.000 0.000 0.000
#&gt; SRR1383387     2  0.0000      0.889 0.000 1.000 0.000
#&gt; SRR1383389     2  0.5882      0.495 0.000 0.652 0.348
#&gt; SRR1383391     2  0.0237      0.889 0.000 0.996 0.004
#&gt; SRR1383388     2  0.2625      0.841 0.084 0.916 0.000
#&gt; SRR1383392     2  0.0892      0.884 0.000 0.980 0.020
#&gt; SRR1383390     2  0.0592      0.887 0.000 0.988 0.012
#&gt; SRR1383394     2  0.0000      0.889 0.000 1.000 0.000
#&gt; SRR1383393     1  0.0000      0.939 1.000 0.000 0.000
#&gt; SRR1383396     1  0.0000      0.939 1.000 0.000 0.000
#&gt; SRR1383395     2  0.4452      0.729 0.000 0.808 0.192
#&gt; SRR1383399     3  0.0000      0.942 0.000 0.000 1.000
#&gt; SRR1383400     1  0.0000      0.939 1.000 0.000 0.000
#&gt; SRR1383397     2  0.0000      0.889 0.000 1.000 0.000
#&gt; SRR1383401     2  0.6045      0.428 0.000 0.620 0.380
#&gt; SRR1383398     2  0.4555      0.722 0.200 0.800 0.000
#&gt; SRR1383402     2  0.0000      0.889 0.000 1.000 0.000
#&gt; SRR1383404     1  0.4452      0.713 0.808 0.192 0.000
#&gt; SRR1383403     1  0.0000      0.939 1.000 0.000 0.000
#&gt; SRR1383405     2  0.0000      0.889 0.000 1.000 0.000
#&gt; SRR1383406     2  0.0000      0.889 0.000 1.000 0.000
#&gt; SRR1383407     3  0.4504      0.748 0.000 0.196 0.804
#&gt; SRR1383408     2  0.0424      0.888 0.000 0.992 0.008
#&gt; SRR1383409     2  0.0592      0.887 0.000 0.988 0.012
#&gt; SRR1383410     2  0.0237      0.889 0.000 0.996 0.004
</code></pre>

<script>
$('#tab-MAD-NMF-get-classes-2-a').parent().next().next().hide();
$('#tab-MAD-NMF-get-classes-2-a').click(function(){
  $('#tab-MAD-NMF-get-classes-2-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-MAD-NMF-get-classes-3'>
<p><a id='tab-MAD-NMF-get-classes-3-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 4), get_membership(res, k = 4))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4
#&gt; SRR1383358     3  0.0000      0.828 0.000 0.000 1.000 0.000
#&gt; SRR1383360     3  0.5349      0.353 0.364 0.008 0.620 0.008
#&gt; SRR1383359     3  0.0000      0.828 0.000 0.000 1.000 0.000
#&gt; SRR1383362     1  0.0469      0.728 0.988 0.000 0.000 0.012
#&gt; SRR1383361     3  0.0336      0.828 0.000 0.008 0.992 0.000
#&gt; SRR1383363     3  0.1022      0.827 0.000 0.000 0.968 0.032
#&gt; SRR1383364     3  0.3942      0.753 0.000 0.000 0.764 0.236
#&gt; SRR1383365     3  0.0188      0.829 0.000 0.004 0.996 0.000
#&gt; SRR1383366     3  0.4468      0.660 0.000 0.232 0.752 0.016
#&gt; SRR1383367     3  0.1022      0.824 0.000 0.032 0.968 0.000
#&gt; SRR1383368     1  0.1909      0.716 0.940 0.008 0.048 0.004
#&gt; SRR1383369     3  0.0188      0.829 0.000 0.000 0.996 0.004
#&gt; SRR1383370     3  0.3311      0.739 0.000 0.172 0.828 0.000
#&gt; SRR1383371     3  0.3356      0.785 0.000 0.000 0.824 0.176
#&gt; SRR1383372     3  0.4425      0.787 0.004 0.036 0.800 0.160
#&gt; SRR1383373     3  0.0188      0.829 0.000 0.004 0.996 0.000
#&gt; SRR1383374     3  0.3870      0.721 0.000 0.208 0.788 0.004
#&gt; SRR1383375     4  0.4431      0.727 0.304 0.000 0.000 0.696
#&gt; SRR1383376     2  0.0336      0.862 0.000 0.992 0.000 0.008
#&gt; SRR1383377     4  0.6049      0.587 0.000 0.264 0.084 0.652
#&gt; SRR1383378     1  0.6994      0.496 0.560 0.288 0.000 0.152
#&gt; SRR1383379     2  0.4406      0.542 0.000 0.700 0.000 0.300
#&gt; SRR1383380     4  0.5007      0.783 0.172 0.068 0.000 0.760
#&gt; SRR1383381     3  0.4252      0.743 0.000 0.004 0.744 0.252
#&gt; SRR1383382     1  0.0000      0.734 1.000 0.000 0.000 0.000
#&gt; SRR1383383     2  0.5292      0.620 0.000 0.728 0.064 0.208
#&gt; SRR1383385     4  0.4134      0.777 0.260 0.000 0.000 0.740
#&gt; SRR1383384     2  0.0000      0.862 0.000 1.000 0.000 0.000
#&gt; SRR1383386     1  0.0336      0.730 0.992 0.000 0.000 0.008
#&gt; SRR1383387     2  0.0817      0.857 0.000 0.976 0.000 0.024
#&gt; SRR1383389     1  0.8963      0.368 0.420 0.280 0.068 0.232
#&gt; SRR1383391     2  0.0672      0.857 0.008 0.984 0.000 0.008
#&gt; SRR1383388     2  0.2915      0.800 0.080 0.892 0.000 0.028
#&gt; SRR1383392     2  0.0524      0.862 0.000 0.988 0.004 0.008
#&gt; SRR1383390     2  0.2867      0.787 0.012 0.884 0.000 0.104
#&gt; SRR1383394     2  0.0469      0.861 0.000 0.988 0.000 0.012
#&gt; SRR1383393     4  0.4072      0.780 0.252 0.000 0.000 0.748
#&gt; SRR1383396     1  0.3105      0.687 0.856 0.000 0.004 0.140
#&gt; SRR1383395     4  0.6219      0.582 0.000 0.264 0.096 0.640
#&gt; SRR1383399     3  0.4220      0.745 0.000 0.004 0.748 0.248
#&gt; SRR1383400     1  0.0000      0.734 1.000 0.000 0.000 0.000
#&gt; SRR1383397     2  0.4804      0.324 0.000 0.616 0.000 0.384
#&gt; SRR1383401     2  0.7054      0.399 0.000 0.572 0.232 0.196
#&gt; SRR1383398     4  0.5171      0.764 0.128 0.112 0.000 0.760
#&gt; SRR1383402     2  0.0000      0.862 0.000 1.000 0.000 0.000
#&gt; SRR1383404     1  0.5271      0.444 0.656 0.320 0.000 0.024
#&gt; SRR1383403     4  0.4103      0.779 0.256 0.000 0.000 0.744
#&gt; SRR1383405     2  0.0921      0.855 0.000 0.972 0.000 0.028
#&gt; SRR1383406     2  0.4193      0.588 0.000 0.732 0.000 0.268
#&gt; SRR1383407     3  0.8345      0.368 0.024 0.320 0.424 0.232
#&gt; SRR1383408     2  0.1209      0.847 0.004 0.964 0.000 0.032
#&gt; SRR1383409     2  0.0188      0.861 0.000 0.996 0.000 0.004
#&gt; SRR1383410     2  0.0336      0.862 0.000 0.992 0.000 0.008
</code></pre>

<script>
$('#tab-MAD-NMF-get-classes-3-a').parent().next().next().hide();
$('#tab-MAD-NMF-get-classes-3-a').click(function(){
  $('#tab-MAD-NMF-get-classes-3-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-MAD-NMF-get-classes-4'>
<p><a id='tab-MAD-NMF-get-classes-4-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 5), get_membership(res, k = 5))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4    p5
#&gt; SRR1383358     3  0.0000      0.975 0.000 0.000 1.000 0.000 0.000
#&gt; SRR1383360     3  0.2377      0.855 0.128 0.000 0.872 0.000 0.000
#&gt; SRR1383359     3  0.0000      0.975 0.000 0.000 1.000 0.000 0.000
#&gt; SRR1383362     1  0.0290      0.886 0.992 0.000 0.000 0.008 0.000
#&gt; SRR1383361     3  0.0000      0.975 0.000 0.000 1.000 0.000 0.000
#&gt; SRR1383363     3  0.0000      0.975 0.000 0.000 1.000 0.000 0.000
#&gt; SRR1383364     5  0.1281      0.891 0.000 0.000 0.032 0.012 0.956
#&gt; SRR1383365     3  0.0000      0.975 0.000 0.000 1.000 0.000 0.000
#&gt; SRR1383366     3  0.0609      0.965 0.000 0.020 0.980 0.000 0.000
#&gt; SRR1383367     3  0.0000      0.975 0.000 0.000 1.000 0.000 0.000
#&gt; SRR1383368     1  0.0510      0.878 0.984 0.000 0.016 0.000 0.000
#&gt; SRR1383369     3  0.1270      0.940 0.000 0.000 0.948 0.000 0.052
#&gt; SRR1383370     3  0.0290      0.972 0.000 0.008 0.992 0.000 0.000
#&gt; SRR1383371     5  0.2193      0.850 0.000 0.000 0.092 0.008 0.900
#&gt; SRR1383372     3  0.1059      0.958 0.004 0.020 0.968 0.000 0.008
#&gt; SRR1383373     3  0.0000      0.975 0.000 0.000 1.000 0.000 0.000
#&gt; SRR1383374     3  0.1043      0.945 0.000 0.040 0.960 0.000 0.000
#&gt; SRR1383375     4  0.1764      0.882 0.064 0.000 0.000 0.928 0.008
#&gt; SRR1383376     2  0.0579      0.887 0.000 0.984 0.000 0.008 0.008
#&gt; SRR1383377     4  0.2732      0.806 0.000 0.160 0.000 0.840 0.000
#&gt; SRR1383378     1  0.3921      0.735 0.800 0.128 0.000 0.000 0.072
#&gt; SRR1383379     2  0.3210      0.730 0.000 0.788 0.000 0.212 0.000
#&gt; SRR1383380     4  0.0404      0.908 0.000 0.012 0.000 0.988 0.000
#&gt; SRR1383381     5  0.0451      0.903 0.000 0.000 0.004 0.008 0.988
#&gt; SRR1383382     1  0.0162      0.887 0.996 0.000 0.000 0.004 0.000
#&gt; SRR1383383     5  0.2074      0.873 0.000 0.104 0.000 0.000 0.896
#&gt; SRR1383385     4  0.1043      0.903 0.040 0.000 0.000 0.960 0.000
#&gt; SRR1383384     2  0.0609      0.884 0.000 0.980 0.000 0.000 0.020
#&gt; SRR1383386     1  0.0162      0.887 0.996 0.000 0.000 0.004 0.000
#&gt; SRR1383387     2  0.0963      0.880 0.000 0.964 0.000 0.036 0.000
#&gt; SRR1383389     5  0.2450      0.886 0.028 0.076 0.000 0.000 0.896
#&gt; SRR1383391     2  0.1205      0.875 0.004 0.956 0.000 0.000 0.040
#&gt; SRR1383388     2  0.1211      0.881 0.016 0.960 0.000 0.024 0.000
#&gt; SRR1383392     2  0.1082      0.878 0.000 0.964 0.028 0.008 0.000
#&gt; SRR1383390     2  0.2970      0.764 0.004 0.828 0.000 0.000 0.168
#&gt; SRR1383394     2  0.1018      0.888 0.000 0.968 0.000 0.016 0.016
#&gt; SRR1383393     4  0.1117      0.905 0.020 0.000 0.000 0.964 0.016
#&gt; SRR1383396     5  0.3381      0.776 0.176 0.016 0.000 0.000 0.808
#&gt; SRR1383395     4  0.2891      0.786 0.000 0.176 0.000 0.824 0.000
#&gt; SRR1383399     5  0.0451      0.903 0.000 0.000 0.004 0.008 0.988
#&gt; SRR1383400     1  0.0162      0.887 0.996 0.000 0.000 0.004 0.000
#&gt; SRR1383397     2  0.4262      0.241 0.000 0.560 0.000 0.440 0.000
#&gt; SRR1383401     5  0.0880      0.905 0.000 0.032 0.000 0.000 0.968
#&gt; SRR1383398     4  0.0404      0.908 0.000 0.012 0.000 0.988 0.000
#&gt; SRR1383402     2  0.0609      0.884 0.000 0.980 0.000 0.000 0.020
#&gt; SRR1383404     1  0.4218      0.485 0.660 0.332 0.000 0.008 0.000
#&gt; SRR1383403     4  0.0794      0.908 0.028 0.000 0.000 0.972 0.000
#&gt; SRR1383405     2  0.1043      0.879 0.000 0.960 0.000 0.040 0.000
#&gt; SRR1383406     2  0.3774      0.590 0.000 0.704 0.000 0.296 0.000
#&gt; SRR1383407     5  0.2919      0.866 0.004 0.104 0.024 0.000 0.868
#&gt; SRR1383408     2  0.2389      0.820 0.004 0.880 0.000 0.000 0.116
#&gt; SRR1383409     2  0.1121      0.876 0.000 0.956 0.000 0.000 0.044
#&gt; SRR1383410     2  0.0566      0.886 0.000 0.984 0.004 0.012 0.000
</code></pre>

<script>
$('#tab-MAD-NMF-get-classes-4-a').parent().next().next().hide();
$('#tab-MAD-NMF-get-classes-4-a').click(function(){
  $('#tab-MAD-NMF-get-classes-4-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-MAD-NMF-get-classes-5'>
<p><a id='tab-MAD-NMF-get-classes-5-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 6), get_membership(res, k = 6))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4    p5    p6
#&gt; SRR1383358     3  0.0717    0.84614 0.000 0.008 0.976 0.000 0.016 0.000
#&gt; SRR1383360     3  0.5144    0.62743 0.000 0.220 0.648 0.012 0.000 0.120
#&gt; SRR1383359     3  0.2019    0.82500 0.000 0.088 0.900 0.000 0.012 0.000
#&gt; SRR1383362     6  0.0146    0.87910 0.000 0.004 0.000 0.000 0.000 0.996
#&gt; SRR1383361     3  0.1610    0.85133 0.000 0.084 0.916 0.000 0.000 0.000
#&gt; SRR1383363     3  0.1951    0.85439 0.000 0.076 0.908 0.000 0.016 0.000
#&gt; SRR1383364     5  0.2152    0.68934 0.004 0.068 0.024 0.000 0.904 0.000
#&gt; SRR1383365     3  0.1812    0.83052 0.000 0.080 0.912 0.000 0.008 0.000
#&gt; SRR1383366     3  0.0767    0.85503 0.000 0.012 0.976 0.008 0.004 0.000
#&gt; SRR1383367     3  0.0622    0.85237 0.000 0.012 0.980 0.008 0.000 0.000
#&gt; SRR1383368     6  0.3885    0.51785 0.000 0.012 0.300 0.004 0.000 0.684
#&gt; SRR1383369     3  0.5703    0.25965 0.000 0.168 0.472 0.000 0.360 0.000
#&gt; SRR1383370     3  0.1297    0.85675 0.000 0.040 0.948 0.012 0.000 0.000
#&gt; SRR1383371     5  0.2547    0.67340 0.000 0.080 0.036 0.000 0.880 0.004
#&gt; SRR1383372     3  0.2841    0.81211 0.000 0.164 0.824 0.012 0.000 0.000
#&gt; SRR1383373     3  0.1753    0.85450 0.000 0.084 0.912 0.000 0.004 0.000
#&gt; SRR1383374     3  0.3920    0.72038 0.000 0.216 0.736 0.048 0.000 0.000
#&gt; SRR1383375     1  0.2859    0.82439 0.872 0.020 0.000 0.000 0.048 0.060
#&gt; SRR1383376     4  0.1957    0.66334 0.000 0.112 0.000 0.888 0.000 0.000
#&gt; SRR1383377     2  0.6672    0.08350 0.272 0.440 0.012 0.256 0.020 0.000
#&gt; SRR1383378     2  0.7044    0.14785 0.000 0.452 0.000 0.232 0.104 0.212
#&gt; SRR1383379     4  0.1643    0.65376 0.068 0.008 0.000 0.924 0.000 0.000
#&gt; SRR1383380     1  0.2538    0.81077 0.860 0.016 0.000 0.124 0.000 0.000
#&gt; SRR1383381     5  0.0603    0.71185 0.004 0.016 0.000 0.000 0.980 0.000
#&gt; SRR1383382     6  0.0458    0.88114 0.000 0.016 0.000 0.000 0.000 0.984
#&gt; SRR1383383     5  0.5054    0.33468 0.000 0.368 0.000 0.084 0.548 0.000
#&gt; SRR1383385     1  0.0777    0.87699 0.972 0.004 0.000 0.000 0.000 0.024
#&gt; SRR1383384     4  0.3515    0.47902 0.000 0.324 0.000 0.676 0.000 0.000
#&gt; SRR1383386     6  0.0858    0.86201 0.004 0.000 0.000 0.028 0.000 0.968
#&gt; SRR1383387     4  0.0508    0.66947 0.004 0.012 0.000 0.984 0.000 0.000
#&gt; SRR1383389     2  0.3962    0.01411 0.000 0.724 0.008 0.008 0.248 0.012
#&gt; SRR1383391     4  0.3189    0.58862 0.000 0.236 0.000 0.760 0.004 0.000
#&gt; SRR1383388     4  0.2685    0.64741 0.060 0.072 0.000 0.868 0.000 0.000
#&gt; SRR1383392     2  0.5144    0.20292 0.000 0.536 0.092 0.372 0.000 0.000
#&gt; SRR1383390     2  0.4948   -0.21253 0.000 0.468 0.000 0.468 0.064 0.000
#&gt; SRR1383394     4  0.1387    0.67863 0.000 0.068 0.000 0.932 0.000 0.000
#&gt; SRR1383393     1  0.1350    0.87274 0.952 0.020 0.000 0.000 0.008 0.020
#&gt; SRR1383396     5  0.6227    0.42887 0.088 0.320 0.000 0.000 0.516 0.076
#&gt; SRR1383395     2  0.6557    0.06178 0.284 0.404 0.008 0.292 0.012 0.000
#&gt; SRR1383399     5  0.0363    0.71261 0.000 0.012 0.000 0.000 0.988 0.000
#&gt; SRR1383400     6  0.0547    0.88015 0.000 0.020 0.000 0.000 0.000 0.980
#&gt; SRR1383397     4  0.2985    0.58448 0.100 0.056 0.000 0.844 0.000 0.000
#&gt; SRR1383401     5  0.4079    0.53768 0.000 0.288 0.000 0.032 0.680 0.000
#&gt; SRR1383398     1  0.3456    0.74128 0.788 0.040 0.000 0.172 0.000 0.000
#&gt; SRR1383402     4  0.3309    0.54124 0.000 0.280 0.000 0.720 0.000 0.000
#&gt; SRR1383404     4  0.5020    0.27588 0.032 0.020 0.004 0.568 0.000 0.376
#&gt; SRR1383403     1  0.0146    0.87696 0.996 0.000 0.000 0.000 0.000 0.004
#&gt; SRR1383405     4  0.2165    0.60725 0.008 0.108 0.000 0.884 0.000 0.000
#&gt; SRR1383406     4  0.3065    0.56933 0.152 0.028 0.000 0.820 0.000 0.000
#&gt; SRR1383407     2  0.3748    0.11231 0.000 0.756 0.012 0.020 0.212 0.000
#&gt; SRR1383408     4  0.4499    0.22080 0.000 0.428 0.000 0.540 0.032 0.000
#&gt; SRR1383409     4  0.2946    0.62967 0.000 0.176 0.000 0.812 0.012 0.000
#&gt; SRR1383410     2  0.4097    0.00295 0.000 0.504 0.008 0.488 0.000 0.000
</code></pre>

<script>
$('#tab-MAD-NMF-get-classes-5-a').parent().next().next().hide();
$('#tab-MAD-NMF-get-classes-5-a').click(function(){
  $('#tab-MAD-NMF-get-classes-5-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>
</div>

Heatmaps for the consensus matrix. It visualizes the probability of two
samples to be in a same group.



<script>
$( function() {
	$( '#tabs-MAD-NMF-consensus-heatmap' ).tabs();
} );
</script>
<div id='tabs-MAD-NMF-consensus-heatmap'>
<ul>
<li><a href='#tab-MAD-NMF-consensus-heatmap-1'>k = 2</a></li>
<li><a href='#tab-MAD-NMF-consensus-heatmap-2'>k = 3</a></li>
<li><a href='#tab-MAD-NMF-consensus-heatmap-3'>k = 4</a></li>
<li><a href='#tab-MAD-NMF-consensus-heatmap-4'>k = 5</a></li>
<li><a href='#tab-MAD-NMF-consensus-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-MAD-NMF-consensus-heatmap-1'>
<pre><code class="r">consensus_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-MAD-NMF-consensus-heatmap-1-1.png" alt="plot of chunk tab-MAD-NMF-consensus-heatmap-1"/></p>

</div>
<div id='tab-MAD-NMF-consensus-heatmap-2'>
<pre><code class="r">consensus_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-MAD-NMF-consensus-heatmap-2-1.png" alt="plot of chunk tab-MAD-NMF-consensus-heatmap-2"/></p>

</div>
<div id='tab-MAD-NMF-consensus-heatmap-3'>
<pre><code class="r">consensus_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-MAD-NMF-consensus-heatmap-3-1.png" alt="plot of chunk tab-MAD-NMF-consensus-heatmap-3"/></p>

</div>
<div id='tab-MAD-NMF-consensus-heatmap-4'>
<pre><code class="r">consensus_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-MAD-NMF-consensus-heatmap-4-1.png" alt="plot of chunk tab-MAD-NMF-consensus-heatmap-4"/></p>

</div>
<div id='tab-MAD-NMF-consensus-heatmap-5'>
<pre><code class="r">consensus_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-MAD-NMF-consensus-heatmap-5-1.png" alt="plot of chunk tab-MAD-NMF-consensus-heatmap-5"/></p>

</div>
</div>

Heatmaps for the membership of samples in all partitions to see how consistent they are:




<script>
$( function() {
	$( '#tabs-MAD-NMF-membership-heatmap' ).tabs();
} );
</script>
<div id='tabs-MAD-NMF-membership-heatmap'>
<ul>
<li><a href='#tab-MAD-NMF-membership-heatmap-1'>k = 2</a></li>
<li><a href='#tab-MAD-NMF-membership-heatmap-2'>k = 3</a></li>
<li><a href='#tab-MAD-NMF-membership-heatmap-3'>k = 4</a></li>
<li><a href='#tab-MAD-NMF-membership-heatmap-4'>k = 5</a></li>
<li><a href='#tab-MAD-NMF-membership-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-MAD-NMF-membership-heatmap-1'>
<pre><code class="r">membership_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-MAD-NMF-membership-heatmap-1-1.png" alt="plot of chunk tab-MAD-NMF-membership-heatmap-1"/></p>

</div>
<div id='tab-MAD-NMF-membership-heatmap-2'>
<pre><code class="r">membership_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-MAD-NMF-membership-heatmap-2-1.png" alt="plot of chunk tab-MAD-NMF-membership-heatmap-2"/></p>

</div>
<div id='tab-MAD-NMF-membership-heatmap-3'>
<pre><code class="r">membership_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-MAD-NMF-membership-heatmap-3-1.png" alt="plot of chunk tab-MAD-NMF-membership-heatmap-3"/></p>

</div>
<div id='tab-MAD-NMF-membership-heatmap-4'>
<pre><code class="r">membership_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-MAD-NMF-membership-heatmap-4-1.png" alt="plot of chunk tab-MAD-NMF-membership-heatmap-4"/></p>

</div>
<div id='tab-MAD-NMF-membership-heatmap-5'>
<pre><code class="r">membership_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-MAD-NMF-membership-heatmap-5-1.png" alt="plot of chunk tab-MAD-NMF-membership-heatmap-5"/></p>

</div>
</div>

As soon as we have had the classes for columns, we can look for signatures
which are significantly different between classes which can be candidate marks
for certain classes. Following are the heatmaps for signatures.



Signature heatmaps where rows are scaled:



<script>
$( function() {
	$( '#tabs-MAD-NMF-get-signatures' ).tabs();
} );
</script>
<div id='tabs-MAD-NMF-get-signatures'>
<ul>
<li><a href='#tab-MAD-NMF-get-signatures-1'>k = 2</a></li>
<li><a href='#tab-MAD-NMF-get-signatures-2'>k = 3</a></li>
<li><a href='#tab-MAD-NMF-get-signatures-3'>k = 4</a></li>
<li><a href='#tab-MAD-NMF-get-signatures-4'>k = 5</a></li>
<li><a href='#tab-MAD-NMF-get-signatures-5'>k = 6</a></li>
</ul>
<div id='tab-MAD-NMF-get-signatures-1'>
<pre><code class="r">get_signatures(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-MAD-NMF-get-signatures-1-1.png" alt="plot of chunk tab-MAD-NMF-get-signatures-1"/></p>

</div>
<div id='tab-MAD-NMF-get-signatures-2'>
<pre><code class="r">get_signatures(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-MAD-NMF-get-signatures-2-1.png" alt="plot of chunk tab-MAD-NMF-get-signatures-2"/></p>

</div>
<div id='tab-MAD-NMF-get-signatures-3'>
<pre><code class="r">get_signatures(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-MAD-NMF-get-signatures-3-1.png" alt="plot of chunk tab-MAD-NMF-get-signatures-3"/></p>

</div>
<div id='tab-MAD-NMF-get-signatures-4'>
<pre><code class="r">get_signatures(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-MAD-NMF-get-signatures-4-1.png" alt="plot of chunk tab-MAD-NMF-get-signatures-4"/></p>

</div>
<div id='tab-MAD-NMF-get-signatures-5'>
<pre><code class="r">get_signatures(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-MAD-NMF-get-signatures-5-1.png" alt="plot of chunk tab-MAD-NMF-get-signatures-5"/></p>

</div>
</div>



Signature heatmaps where rows are not scaled:


<script>
$( function() {
	$( '#tabs-MAD-NMF-get-signatures-no-scale' ).tabs();
} );
</script>
<div id='tabs-MAD-NMF-get-signatures-no-scale'>
<ul>
<li><a href='#tab-MAD-NMF-get-signatures-no-scale-1'>k = 2</a></li>
<li><a href='#tab-MAD-NMF-get-signatures-no-scale-2'>k = 3</a></li>
<li><a href='#tab-MAD-NMF-get-signatures-no-scale-3'>k = 4</a></li>
<li><a href='#tab-MAD-NMF-get-signatures-no-scale-4'>k = 5</a></li>
<li><a href='#tab-MAD-NMF-get-signatures-no-scale-5'>k = 6</a></li>
</ul>
<div id='tab-MAD-NMF-get-signatures-no-scale-1'>
<pre><code class="r">get_signatures(res, k = 2, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-MAD-NMF-get-signatures-no-scale-1-1.png" alt="plot of chunk tab-MAD-NMF-get-signatures-no-scale-1"/></p>

</div>
<div id='tab-MAD-NMF-get-signatures-no-scale-2'>
<pre><code class="r">get_signatures(res, k = 3, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-MAD-NMF-get-signatures-no-scale-2-1.png" alt="plot of chunk tab-MAD-NMF-get-signatures-no-scale-2"/></p>

</div>
<div id='tab-MAD-NMF-get-signatures-no-scale-3'>
<pre><code class="r">get_signatures(res, k = 4, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-MAD-NMF-get-signatures-no-scale-3-1.png" alt="plot of chunk tab-MAD-NMF-get-signatures-no-scale-3"/></p>

</div>
<div id='tab-MAD-NMF-get-signatures-no-scale-4'>
<pre><code class="r">get_signatures(res, k = 5, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-MAD-NMF-get-signatures-no-scale-4-1.png" alt="plot of chunk tab-MAD-NMF-get-signatures-no-scale-4"/></p>

</div>
<div id='tab-MAD-NMF-get-signatures-no-scale-5'>
<pre><code class="r">get_signatures(res, k = 6, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-MAD-NMF-get-signatures-no-scale-5-1.png" alt="plot of chunk tab-MAD-NMF-get-signatures-no-scale-5"/></p>

</div>
</div>



Compare the overlap of signatures from different k:

```r
compare_signatures(res)
```

![plot of chunk MAD-NMF-signature_compare](figure_cola/MAD-NMF-signature_compare-1.png)

`get_signature()` returns a data frame invisibly. TO get the list of signatures, the function
call should be assigned to a variable explicitly. In following code, if `plot` argument is set
to `FALSE`, no heatmap is plotted while only the differential analysis is performed.

```r
# code only for demonstration
tb = get_signature(res, k = ..., plot = FALSE)
```

An example of the output of `tb` is:

```
#>   which_row         fdr    mean_1    mean_2 scaled_mean_1 scaled_mean_2 km
#> 1        38 0.042760348  8.373488  9.131774    -0.5533452     0.5164555  1
#> 2        40 0.018707592  7.106213  8.469186    -0.6173731     0.5762149  1
#> 3        55 0.019134737 10.221463 11.207825    -0.6159697     0.5749050  1
#> 4        59 0.006059896  5.921854  7.869574    -0.6899429     0.6439467  1
#> 5        60 0.018055526  8.928898 10.211722    -0.6204761     0.5791110  1
#> 6        98 0.009384629 15.714769 14.887706     0.6635654    -0.6193277  2
...
```

The columns in `tb` are:

1. `which_row`: row indices corresponding to the input matrix.
2. `fdr`: FDR for the differential test. 
3. `mean_x`: The mean value in group x.
4. `scaled_mean_x`: The mean value in group x after rows are scaled.
5. `km`: Row groups if k-means clustering is applied to rows.



UMAP plot which shows how samples are separated.


<script>
$( function() {
	$( '#tabs-MAD-NMF-dimension-reduction' ).tabs();
} );
</script>
<div id='tabs-MAD-NMF-dimension-reduction'>
<ul>
<li><a href='#tab-MAD-NMF-dimension-reduction-1'>k = 2</a></li>
<li><a href='#tab-MAD-NMF-dimension-reduction-2'>k = 3</a></li>
<li><a href='#tab-MAD-NMF-dimension-reduction-3'>k = 4</a></li>
<li><a href='#tab-MAD-NMF-dimension-reduction-4'>k = 5</a></li>
<li><a href='#tab-MAD-NMF-dimension-reduction-5'>k = 6</a></li>
</ul>
<div id='tab-MAD-NMF-dimension-reduction-1'>
<pre><code class="r">dimension_reduction(res, k = 2, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-MAD-NMF-dimension-reduction-1-1.png" alt="plot of chunk tab-MAD-NMF-dimension-reduction-1"/></p>

</div>
<div id='tab-MAD-NMF-dimension-reduction-2'>
<pre><code class="r">dimension_reduction(res, k = 3, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-MAD-NMF-dimension-reduction-2-1.png" alt="plot of chunk tab-MAD-NMF-dimension-reduction-2"/></p>

</div>
<div id='tab-MAD-NMF-dimension-reduction-3'>
<pre><code class="r">dimension_reduction(res, k = 4, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-MAD-NMF-dimension-reduction-3-1.png" alt="plot of chunk tab-MAD-NMF-dimension-reduction-3"/></p>

</div>
<div id='tab-MAD-NMF-dimension-reduction-4'>
<pre><code class="r">dimension_reduction(res, k = 5, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-MAD-NMF-dimension-reduction-4-1.png" alt="plot of chunk tab-MAD-NMF-dimension-reduction-4"/></p>

</div>
<div id='tab-MAD-NMF-dimension-reduction-5'>
<pre><code class="r">dimension_reduction(res, k = 6, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-MAD-NMF-dimension-reduction-5-1.png" alt="plot of chunk tab-MAD-NMF-dimension-reduction-5"/></p>

</div>
</div>


Following heatmap shows how subgroups are split when increasing `k`:

```r
collect_classes(res)
```

![plot of chunk MAD-NMF-collect-classes](figure_cola/MAD-NMF-collect-classes-1.png)


If matrix rows can be associated to genes, consider to use `functional_enrichment(res,
...)` to perform function enrichment for the signature genes. See [this vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/functional_enrichment.html) for more detailed explanations.


 

---------------------------------------------------




### ATC:hclust






The object with results only for a single top-value method and a single partition method 
can be extracted as:

```r
res = res_list["ATC", "hclust"]
# you can also extract it by
# res = res_list["ATC:hclust"]
```

A summary of `res` and all the functions that can be applied to it:

```r
res
```

```
#> A 'ConsensusPartition' object with k = 2, 3, 4, 5, 6.
#>   On a matrix with 15680 rows and 53 columns.
#>   Top rows (1000, 2000, 3000, 4000, 5000) are extracted by 'ATC' method.
#>   Subgroups are detected by 'hclust' method.
#>   Performed in total 1250 partitions by row resampling.
#>   Best k for subgroups seems to be 3.
#> 
#> Following methods can be applied to this 'ConsensusPartition' object:
#>  [1] "cola_report"             "collect_classes"         "collect_plots"          
#>  [4] "collect_stats"           "colnames"                "compare_signatures"     
#>  [7] "consensus_heatmap"       "dimension_reduction"     "functional_enrichment"  
#> [10] "get_anno_col"            "get_anno"                "get_classes"            
#> [13] "get_consensus"           "get_matrix"              "get_membership"         
#> [16] "get_param"               "get_signatures"          "get_stats"              
#> [19] "is_best_k"               "is_stable_k"             "membership_heatmap"     
#> [22] "ncol"                    "nrow"                    "plot_ecdf"              
#> [25] "rownames"                "select_partition_number" "show"                   
#> [28] "suggest_best_k"          "test_to_known_factors"
```

`collect_plots()` function collects all the plots made from `res` for all `k` (number of partitions)
into one single page to provide an easy and fast comparison between different `k`.

```r
collect_plots(res)
```

![plot of chunk ATC-hclust-collect-plots](figure_cola/ATC-hclust-collect-plots-1.png)

The plots are:

- The first row: a plot of the ECDF (empirical cumulative distribution
  function) curves of the consensus matrix for each `k` and the heatmap of
  predicted classes for each `k`.
- The second row: heatmaps of the consensus matrix for each `k`.
- The third row: heatmaps of the membership matrix for each `k`.
- The fouth row: heatmaps of the signatures for each `k`.

All the plots in panels can be made by individual functions and they are
plotted later in this section.

`select_partition_number()` produces several plots showing different
statistics for choosing "optimized" `k`. There are following statistics:

- ECDF curves of the consensus matrix for each `k`;
- 1-PAC. [The PAC
  score](https://en.wikipedia.org/wiki/Consensus_clustering#Over-interpretation_potential_of_consensus_clustering)
  measures the proportion of the ambiguous subgrouping.
- Mean silhouette score.
- Concordance. The mean probability of fiting the consensus class ids in all
  partitions.
- Area increased. Denote $A_k$ as the area under the ECDF curve for current
  `k`, the area increased is defined as $A_k - A_{k-1}$.
- Rand index. The percent of pairs of samples that are both in a same cluster
  or both are not in a same cluster in the partition of k and k-1.
- Jaccard index. The ratio of pairs of samples are both in a same cluster in
  the partition of k and k-1 and the pairs of samples are both in a same
  cluster in the partition k or k-1.

The detailed explanations of these statistics can be found in [the _cola_
vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/cola.html#toc_13).

Generally speaking, lower PAC score, higher mean silhouette score or higher
concordance corresponds to better partition. Rand index and Jaccard index
measure how similar the current partition is compared to partition with `k-1`.
If they are too similar, we won't accept `k` is better than `k-1`.

```r
select_partition_number(res)
```

![plot of chunk ATC-hclust-select-partition-number](figure_cola/ATC-hclust-select-partition-number-1.png)

The numeric values for all these statistics can be obtained by `get_stats()`.

```r
get_stats(res)
```

```
#>   k 1-PAC mean_silhouette concordance area_increased  Rand Jaccard
#> 2 2 0.362           0.687       0.793         0.4379 0.570   0.570
#> 3 3 0.505           0.739       0.830         0.3977 0.734   0.542
#> 4 4 0.597           0.721       0.785         0.1327 1.000   1.000
#> 5 5 0.795           0.690       0.858         0.0920 0.935   0.800
#> 6 6 0.814           0.665       0.792         0.0489 0.933   0.752
```

`suggest_best_k()` suggests the best $k$ based on these statistics. The rules are as follows:

- All $k$ with Jaccard index larger than 0.95 are removed because increasing
  $k$ does not provide enough extra information. If all $k$ are removed, it is
  marked as no subgroup is detected.
- For all $k$ with 1-PAC score larger than 0.9, the maximal $k$ is taken as
  the best $k$, and other $k$ are marked as optional $k$.
- If it does not fit the second rule. The $k$ with the maximal vote of the
  highest 1-PAC score, highest mean silhouette, and highest concordance is
  taken as the best $k$.

```r
suggest_best_k(res)
```

```
#> [1] 3
```


Following shows the table of the partitions (You need to click the **show/hide
code output** link to see it). The membership matrix (columns with name `p*`)
is inferred by
[`clue::cl_consensus()`](https://www.rdocumentation.org/link/cl_consensus?package=clue)
function with the `SE` method. Basically the value in the membership matrix
represents the probability to belong to a certain group. The finall class
label for an item is determined with the group with highest probability it
belongs to.

In `get_classes()` function, the entropy is calculated from the membership
matrix and the silhouette score is calculated from the consensus matrix.



<script>
$( function() {
	$( '#tabs-ATC-hclust-get-classes' ).tabs();
} );
</script>
<div id='tabs-ATC-hclust-get-classes'>
<ul>
<li><a href='#tab-ATC-hclust-get-classes-1'>k = 2</a></li>
<li><a href='#tab-ATC-hclust-get-classes-2'>k = 3</a></li>
<li><a href='#tab-ATC-hclust-get-classes-3'>k = 4</a></li>
<li><a href='#tab-ATC-hclust-get-classes-4'>k = 5</a></li>
<li><a href='#tab-ATC-hclust-get-classes-5'>k = 6</a></li>
</ul>

<div id='tab-ATC-hclust-get-classes-1'>
<p><a id='tab-ATC-hclust-get-classes-1-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 2), get_membership(res, k = 2))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2
#&gt; SRR1383358     1  0.1843      0.576 0.972 0.028
#&gt; SRR1383360     1  0.8713      0.662 0.708 0.292
#&gt; SRR1383359     1  0.9850      0.642 0.572 0.428
#&gt; SRR1383362     1  0.9850      0.642 0.572 0.428
#&gt; SRR1383361     1  0.7745      0.666 0.772 0.228
#&gt; SRR1383363     1  0.7745      0.666 0.772 0.228
#&gt; SRR1383364     1  0.9850      0.642 0.572 0.428
#&gt; SRR1383365     1  0.9850      0.642 0.572 0.428
#&gt; SRR1383366     1  0.1843      0.576 0.972 0.028
#&gt; SRR1383367     1  0.1843      0.576 0.972 0.028
#&gt; SRR1383368     1  0.7950      0.666 0.760 0.240
#&gt; SRR1383369     1  0.2043      0.586 0.968 0.032
#&gt; SRR1383370     1  0.7745      0.666 0.772 0.228
#&gt; SRR1383371     1  0.9850      0.642 0.572 0.428
#&gt; SRR1383372     1  0.1843      0.576 0.972 0.028
#&gt; SRR1383373     1  0.7745      0.666 0.772 0.228
#&gt; SRR1383374     1  0.9998     -0.867 0.508 0.492
#&gt; SRR1383375     1  0.9775      0.646 0.588 0.412
#&gt; SRR1383376     2  0.9850      1.000 0.428 0.572
#&gt; SRR1383377     1  0.0672      0.591 0.992 0.008
#&gt; SRR1383378     1  0.4690      0.489 0.900 0.100
#&gt; SRR1383379     2  0.9850      1.000 0.428 0.572
#&gt; SRR1383380     1  0.4690      0.489 0.900 0.100
#&gt; SRR1383381     1  0.4298      0.509 0.912 0.088
#&gt; SRR1383382     1  0.9850      0.642 0.572 0.428
#&gt; SRR1383383     2  0.9850      1.000 0.428 0.572
#&gt; SRR1383385     1  0.9775      0.646 0.588 0.412
#&gt; SRR1383384     2  0.9850      1.000 0.428 0.572
#&gt; SRR1383386     1  0.4690      0.489 0.900 0.100
#&gt; SRR1383387     2  0.9850      1.000 0.428 0.572
#&gt; SRR1383389     1  0.3879      0.535 0.924 0.076
#&gt; SRR1383391     2  0.9850      1.000 0.428 0.572
#&gt; SRR1383388     1  0.4690      0.489 0.900 0.100
#&gt; SRR1383392     2  0.9850      1.000 0.428 0.572
#&gt; SRR1383390     2  0.9850      1.000 0.428 0.572
#&gt; SRR1383394     2  0.9850      1.000 0.428 0.572
#&gt; SRR1383393     1  0.9775      0.646 0.588 0.412
#&gt; SRR1383396     1  0.4939      0.537 0.892 0.108
#&gt; SRR1383395     1  0.0672      0.591 0.992 0.008
#&gt; SRR1383399     1  0.4298      0.509 0.912 0.088
#&gt; SRR1383400     1  0.9850      0.642 0.572 0.428
#&gt; SRR1383397     2  0.9850      1.000 0.428 0.572
#&gt; SRR1383401     2  0.9850      1.000 0.428 0.572
#&gt; SRR1383398     1  0.4690      0.489 0.900 0.100
#&gt; SRR1383402     2  0.9850      1.000 0.428 0.572
#&gt; SRR1383404     1  0.4690      0.489 0.900 0.100
#&gt; SRR1383403     1  0.9775      0.646 0.588 0.412
#&gt; SRR1383405     2  0.9850      1.000 0.428 0.572
#&gt; SRR1383406     1  0.4690      0.489 0.900 0.100
#&gt; SRR1383407     1  0.9850      0.642 0.572 0.428
#&gt; SRR1383408     2  0.9850      1.000 0.428 0.572
#&gt; SRR1383409     2  0.9850      1.000 0.428 0.572
#&gt; SRR1383410     2  0.9850      1.000 0.428 0.572
</code></pre>

<script>
$('#tab-ATC-hclust-get-classes-1-a').parent().next().next().hide();
$('#tab-ATC-hclust-get-classes-1-a').click(function(){
  $('#tab-ATC-hclust-get-classes-1-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-ATC-hclust-get-classes-2'>
<p><a id='tab-ATC-hclust-get-classes-2-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 3), get_membership(res, k = 3))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3
#&gt; SRR1383358     3   0.673      0.685 0.284 0.036 0.680
#&gt; SRR1383360     3   0.000      0.688 0.000 0.000 1.000
#&gt; SRR1383359     3   0.362      0.619 0.136 0.000 0.864
#&gt; SRR1383362     1   0.667      0.622 0.616 0.368 0.016
#&gt; SRR1383361     3   0.216      0.723 0.064 0.000 0.936
#&gt; SRR1383363     3   0.216      0.723 0.064 0.000 0.936
#&gt; SRR1383364     3   0.362      0.619 0.136 0.000 0.864
#&gt; SRR1383365     3   0.362      0.619 0.136 0.000 0.864
#&gt; SRR1383366     3   0.673      0.685 0.284 0.036 0.680
#&gt; SRR1383367     3   0.673      0.685 0.284 0.036 0.680
#&gt; SRR1383368     3   0.328      0.705 0.068 0.024 0.908
#&gt; SRR1383369     3   0.656      0.692 0.276 0.032 0.692
#&gt; SRR1383370     3   0.216      0.723 0.064 0.000 0.936
#&gt; SRR1383371     3   0.362      0.619 0.136 0.000 0.864
#&gt; SRR1383372     3   0.673      0.685 0.284 0.036 0.680
#&gt; SRR1383373     3   0.216      0.723 0.064 0.000 0.936
#&gt; SRR1383374     2   0.932      0.726 0.340 0.484 0.176
#&gt; SRR1383375     1   0.599      0.628 0.632 0.368 0.000
#&gt; SRR1383376     2   0.599      0.980 0.368 0.632 0.000
#&gt; SRR1383377     3   0.632      0.694 0.276 0.024 0.700
#&gt; SRR1383378     1   0.416      0.540 0.848 0.008 0.144
#&gt; SRR1383379     2   0.680      0.959 0.368 0.612 0.020
#&gt; SRR1383380     1   0.403      0.549 0.856 0.008 0.136
#&gt; SRR1383381     3   0.686      0.587 0.356 0.024 0.620
#&gt; SRR1383382     1   0.667      0.622 0.616 0.368 0.016
#&gt; SRR1383383     2   0.599      0.980 0.368 0.632 0.000
#&gt; SRR1383385     1   0.599      0.628 0.632 0.368 0.000
#&gt; SRR1383384     2   0.599      0.980 0.368 0.632 0.000
#&gt; SRR1383386     1   0.403      0.549 0.856 0.008 0.136
#&gt; SRR1383387     2   0.599      0.980 0.368 0.632 0.000
#&gt; SRR1383389     3   0.675      0.622 0.336 0.024 0.640
#&gt; SRR1383391     2   0.599      0.980 0.368 0.632 0.000
#&gt; SRR1383388     1   0.403      0.549 0.856 0.008 0.136
#&gt; SRR1383392     2   0.599      0.980 0.368 0.632 0.000
#&gt; SRR1383390     2   0.599      0.980 0.368 0.632 0.000
#&gt; SRR1383394     2   0.599      0.980 0.368 0.632 0.000
#&gt; SRR1383393     1   0.599      0.628 0.632 0.368 0.000
#&gt; SRR1383396     1   0.487      0.562 0.824 0.024 0.152
#&gt; SRR1383395     3   0.632      0.694 0.276 0.024 0.700
#&gt; SRR1383399     3   0.686      0.587 0.356 0.024 0.620
#&gt; SRR1383400     1   0.667      0.622 0.616 0.368 0.016
#&gt; SRR1383397     2   0.680      0.959 0.368 0.612 0.020
#&gt; SRR1383401     2   0.621      0.977 0.368 0.628 0.004
#&gt; SRR1383398     1   0.403      0.549 0.856 0.008 0.136
#&gt; SRR1383402     2   0.599      0.980 0.368 0.632 0.000
#&gt; SRR1383404     1   0.403      0.549 0.856 0.008 0.136
#&gt; SRR1383403     1   0.599      0.628 0.632 0.368 0.000
#&gt; SRR1383405     2   0.599      0.980 0.368 0.632 0.000
#&gt; SRR1383406     1   0.403      0.549 0.856 0.008 0.136
#&gt; SRR1383407     3   0.362      0.619 0.136 0.000 0.864
#&gt; SRR1383408     2   0.599      0.980 0.368 0.632 0.000
#&gt; SRR1383409     2   0.599      0.980 0.368 0.632 0.000
#&gt; SRR1383410     2   0.599      0.980 0.368 0.632 0.000
</code></pre>

<script>
$('#tab-ATC-hclust-get-classes-2-a').parent().next().next().hide();
$('#tab-ATC-hclust-get-classes-2-a').click(function(){
  $('#tab-ATC-hclust-get-classes-2-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-ATC-hclust-get-classes-3'>
<p><a id='tab-ATC-hclust-get-classes-3-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 4), get_membership(res, k = 4))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3 p4
#&gt; SRR1383358     3  0.6024      0.733 0.000 0.044 0.540 NA
#&gt; SRR1383360     3  0.2921      0.739 0.000 0.000 0.860 NA
#&gt; SRR1383359     3  0.2216      0.609 0.000 0.000 0.908 NA
#&gt; SRR1383362     1  0.4996      0.383 0.516 0.000 0.000 NA
#&gt; SRR1383361     3  0.3688      0.761 0.000 0.000 0.792 NA
#&gt; SRR1383363     3  0.3688      0.761 0.000 0.000 0.792 NA
#&gt; SRR1383364     3  0.2216      0.609 0.000 0.000 0.908 NA
#&gt; SRR1383365     3  0.0000      0.662 0.000 0.000 1.000 NA
#&gt; SRR1383366     3  0.6024      0.733 0.000 0.044 0.540 NA
#&gt; SRR1383367     3  0.6024      0.733 0.000 0.044 0.540 NA
#&gt; SRR1383368     3  0.4761      0.748 0.048 0.000 0.768 NA
#&gt; SRR1383369     3  0.5933      0.739 0.000 0.040 0.552 NA
#&gt; SRR1383370     3  0.3688      0.761 0.000 0.000 0.792 NA
#&gt; SRR1383371     3  0.0592      0.655 0.000 0.000 0.984 NA
#&gt; SRR1383372     3  0.6024      0.733 0.000 0.044 0.540 NA
#&gt; SRR1383373     3  0.3688      0.761 0.000 0.000 0.792 NA
#&gt; SRR1383374     2  0.6412      0.350 0.000 0.572 0.080 NA
#&gt; SRR1383375     1  0.0000      0.581 1.000 0.000 0.000 NA
#&gt; SRR1383376     2  0.0188      0.942 0.000 0.996 0.000 NA
#&gt; SRR1383377     3  0.5628      0.738 0.000 0.024 0.556 NA
#&gt; SRR1383378     1  0.7650      0.576 0.480 0.172 0.008 NA
#&gt; SRR1383379     2  0.1557      0.905 0.000 0.944 0.000 NA
#&gt; SRR1383380     1  0.7355      0.586 0.488 0.172 0.000 NA
#&gt; SRR1383381     3  0.7093      0.646 0.000 0.128 0.476 NA
#&gt; SRR1383382     1  0.4996      0.383 0.516 0.000 0.000 NA
#&gt; SRR1383383     2  0.1389      0.922 0.000 0.952 0.000 NA
#&gt; SRR1383385     1  0.0000      0.581 1.000 0.000 0.000 NA
#&gt; SRR1383384     2  0.0188      0.942 0.000 0.996 0.000 NA
#&gt; SRR1383386     1  0.7355      0.586 0.488 0.172 0.000 NA
#&gt; SRR1383387     2  0.0000      0.942 0.000 1.000 0.000 NA
#&gt; SRR1383389     3  0.6889      0.672 0.000 0.108 0.496 NA
#&gt; SRR1383391     2  0.0188      0.942 0.000 0.996 0.000 NA
#&gt; SRR1383388     1  0.7355      0.586 0.488 0.172 0.000 NA
#&gt; SRR1383392     2  0.1637      0.917 0.000 0.940 0.000 NA
#&gt; SRR1383390     2  0.0188      0.942 0.000 0.996 0.000 NA
#&gt; SRR1383394     2  0.0000      0.942 0.000 1.000 0.000 NA
#&gt; SRR1383393     1  0.0000      0.581 1.000 0.000 0.000 NA
#&gt; SRR1383396     1  0.7243      0.538 0.512 0.108 0.012 NA
#&gt; SRR1383395     3  0.5628      0.738 0.000 0.024 0.556 NA
#&gt; SRR1383399     3  0.7093      0.646 0.000 0.128 0.476 NA
#&gt; SRR1383400     1  0.4996      0.383 0.516 0.000 0.000 NA
#&gt; SRR1383397     2  0.1557      0.905 0.000 0.944 0.000 NA
#&gt; SRR1383401     2  0.1637      0.914 0.000 0.940 0.000 NA
#&gt; SRR1383398     1  0.7355      0.586 0.488 0.172 0.000 NA
#&gt; SRR1383402     2  0.0000      0.942 0.000 1.000 0.000 NA
#&gt; SRR1383404     1  0.7355      0.586 0.488 0.172 0.000 NA
#&gt; SRR1383403     1  0.0000      0.581 1.000 0.000 0.000 NA
#&gt; SRR1383405     2  0.0000      0.942 0.000 1.000 0.000 NA
#&gt; SRR1383406     1  0.7355      0.586 0.488 0.172 0.000 NA
#&gt; SRR1383407     3  0.0000      0.662 0.000 0.000 1.000 NA
#&gt; SRR1383408     2  0.0000      0.942 0.000 1.000 0.000 NA
#&gt; SRR1383409     2  0.0188      0.942 0.000 0.996 0.000 NA
#&gt; SRR1383410     2  0.1637      0.917 0.000 0.940 0.000 NA
</code></pre>

<script>
$('#tab-ATC-hclust-get-classes-3-a').parent().next().next().hide();
$('#tab-ATC-hclust-get-classes-3-a').click(function(){
  $('#tab-ATC-hclust-get-classes-3-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-ATC-hclust-get-classes-4'>
<p><a id='tab-ATC-hclust-get-classes-4-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 5), get_membership(res, k = 5))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4    p5
#&gt; SRR1383358     3  0.0912     0.6836 0.000 0.012 0.972 0.016 0.000
#&gt; SRR1383360     3  0.3774     0.5631 0.000 0.000 0.704 0.000 0.296
#&gt; SRR1383359     5  0.0000     0.6590 0.000 0.000 0.000 0.000 1.000
#&gt; SRR1383362     1  0.0000     1.0000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1383361     3  0.3336     0.6392 0.000 0.000 0.772 0.000 0.228
#&gt; SRR1383363     3  0.3336     0.6392 0.000 0.000 0.772 0.000 0.228
#&gt; SRR1383364     5  0.0000     0.6590 0.000 0.000 0.000 0.000 1.000
#&gt; SRR1383365     3  0.4262     0.2950 0.000 0.000 0.560 0.000 0.440
#&gt; SRR1383366     3  0.0912     0.6836 0.000 0.012 0.972 0.016 0.000
#&gt; SRR1383367     3  0.0912     0.6836 0.000 0.012 0.972 0.016 0.000
#&gt; SRR1383368     3  0.4707     0.6059 0.000 0.000 0.716 0.072 0.212
#&gt; SRR1383369     3  0.0579     0.6850 0.000 0.008 0.984 0.008 0.000
#&gt; SRR1383370     3  0.3336     0.6392 0.000 0.000 0.772 0.000 0.228
#&gt; SRR1383371     5  0.4201    -0.0654 0.000 0.000 0.408 0.000 0.592
#&gt; SRR1383372     3  0.0912     0.6836 0.000 0.012 0.972 0.016 0.000
#&gt; SRR1383373     3  0.3336     0.6392 0.000 0.000 0.772 0.000 0.228
#&gt; SRR1383374     2  0.4713     0.3373 0.000 0.544 0.440 0.016 0.000
#&gt; SRR1383375     4  0.4300     0.2318 0.476 0.000 0.000 0.524 0.000
#&gt; SRR1383376     2  0.0162     0.9355 0.000 0.996 0.004 0.000 0.000
#&gt; SRR1383377     3  0.0290     0.6882 0.000 0.000 0.992 0.008 0.000
#&gt; SRR1383378     4  0.1408     0.7604 0.000 0.044 0.008 0.948 0.000
#&gt; SRR1383379     2  0.1544     0.8947 0.000 0.932 0.000 0.068 0.000
#&gt; SRR1383380     4  0.1121     0.7667 0.000 0.044 0.000 0.956 0.000
#&gt; SRR1383381     3  0.4256     0.3623 0.000 0.000 0.564 0.436 0.000
#&gt; SRR1383382     1  0.0000     1.0000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1383383     2  0.2645     0.8754 0.000 0.888 0.044 0.068 0.000
#&gt; SRR1383385     4  0.4300     0.2318 0.476 0.000 0.000 0.524 0.000
#&gt; SRR1383384     2  0.0162     0.9355 0.000 0.996 0.004 0.000 0.000
#&gt; SRR1383386     4  0.1121     0.7667 0.000 0.044 0.000 0.956 0.000
#&gt; SRR1383387     2  0.0000     0.9349 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1383389     3  0.4321     0.4049 0.000 0.000 0.600 0.396 0.004
#&gt; SRR1383391     2  0.0162     0.9355 0.000 0.996 0.004 0.000 0.000
#&gt; SRR1383388     4  0.1121     0.7667 0.000 0.044 0.000 0.956 0.000
#&gt; SRR1383392     2  0.1557     0.9093 0.000 0.940 0.052 0.008 0.000
#&gt; SRR1383390     2  0.0162     0.9355 0.000 0.996 0.004 0.000 0.000
#&gt; SRR1383394     2  0.0000     0.9349 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1383393     4  0.4300     0.2318 0.476 0.000 0.000 0.524 0.000
#&gt; SRR1383396     4  0.1043     0.7215 0.000 0.000 0.040 0.960 0.000
#&gt; SRR1383395     3  0.0290     0.6882 0.000 0.000 0.992 0.008 0.000
#&gt; SRR1383399     3  0.4256     0.3623 0.000 0.000 0.564 0.436 0.000
#&gt; SRR1383400     1  0.0000     1.0000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1383397     2  0.1544     0.8947 0.000 0.932 0.000 0.068 0.000
#&gt; SRR1383401     2  0.2859     0.8674 0.000 0.876 0.056 0.068 0.000
#&gt; SRR1383398     4  0.1121     0.7667 0.000 0.044 0.000 0.956 0.000
#&gt; SRR1383402     2  0.0000     0.9349 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1383404     4  0.1121     0.7667 0.000 0.044 0.000 0.956 0.000
#&gt; SRR1383403     4  0.4300     0.2318 0.476 0.000 0.000 0.524 0.000
#&gt; SRR1383405     2  0.0000     0.9349 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1383406     4  0.1121     0.7667 0.000 0.044 0.000 0.956 0.000
#&gt; SRR1383407     3  0.4262     0.2950 0.000 0.000 0.560 0.000 0.440
#&gt; SRR1383408     2  0.0000     0.9349 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1383409     2  0.0162     0.9355 0.000 0.996 0.004 0.000 0.000
#&gt; SRR1383410     2  0.1557     0.9093 0.000 0.940 0.052 0.008 0.000
</code></pre>

<script>
$('#tab-ATC-hclust-get-classes-4-a').parent().next().next().hide();
$('#tab-ATC-hclust-get-classes-4-a').click(function(){
  $('#tab-ATC-hclust-get-classes-4-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-ATC-hclust-get-classes-5'>
<p><a id='tab-ATC-hclust-get-classes-5-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 6), get_membership(res, k = 6))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4    p5    p6
#&gt; SRR1383358     5  0.3727      0.579 0.000 0.000 0.388 0.000 0.612 0.000
#&gt; SRR1383360     3  0.2442      0.629 0.068 0.000 0.884 0.000 0.048 0.000
#&gt; SRR1383359     1  0.1007      1.000 0.956 0.000 0.044 0.000 0.000 0.000
#&gt; SRR1383362     6  0.0000      1.000 0.000 0.000 0.000 0.000 0.000 1.000
#&gt; SRR1383361     3  0.0000      0.638 0.000 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1383363     3  0.2178      0.547 0.000 0.000 0.868 0.000 0.132 0.000
#&gt; SRR1383364     1  0.1007      1.000 0.956 0.000 0.044 0.000 0.000 0.000
#&gt; SRR1383365     3  0.4871      0.531 0.212 0.000 0.656 0.000 0.132 0.000
#&gt; SRR1383366     5  0.3717      0.576 0.000 0.000 0.384 0.000 0.616 0.000
#&gt; SRR1383367     5  0.3727      0.579 0.000 0.000 0.388 0.000 0.612 0.000
#&gt; SRR1383368     3  0.3873      0.537 0.040 0.000 0.780 0.020 0.160 0.000
#&gt; SRR1383369     5  0.3765      0.554 0.000 0.000 0.404 0.000 0.596 0.000
#&gt; SRR1383370     3  0.0000      0.638 0.000 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1383371     3  0.3659      0.318 0.364 0.000 0.636 0.000 0.000 0.000
#&gt; SRR1383372     5  0.3727      0.579 0.000 0.000 0.388 0.000 0.612 0.000
#&gt; SRR1383373     3  0.0000      0.638 0.000 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1383374     2  0.5431      0.276 0.000 0.532 0.136 0.000 0.332 0.000
#&gt; SRR1383375     4  0.3964      0.298 0.044 0.000 0.000 0.724 0.000 0.232
#&gt; SRR1383376     2  0.0146      0.928 0.000 0.996 0.000 0.000 0.004 0.000
#&gt; SRR1383377     3  0.3867     -0.349 0.000 0.000 0.512 0.000 0.488 0.000
#&gt; SRR1383378     4  0.3592      0.742 0.000 0.000 0.000 0.656 0.344 0.000
#&gt; SRR1383379     2  0.1780      0.880 0.000 0.924 0.000 0.048 0.028 0.000
#&gt; SRR1383380     4  0.3563      0.747 0.000 0.000 0.000 0.664 0.336 0.000
#&gt; SRR1383381     5  0.5461      0.415 0.000 0.000 0.200 0.228 0.572 0.000
#&gt; SRR1383382     6  0.0000      1.000 0.000 0.000 0.000 0.000 0.000 1.000
#&gt; SRR1383383     2  0.2719      0.863 0.000 0.876 0.012 0.040 0.072 0.000
#&gt; SRR1383385     4  0.3964      0.298 0.044 0.000 0.000 0.724 0.000 0.232
#&gt; SRR1383384     2  0.0458      0.927 0.000 0.984 0.000 0.000 0.016 0.000
#&gt; SRR1383386     4  0.3563      0.747 0.000 0.000 0.000 0.664 0.336 0.000
#&gt; SRR1383387     2  0.0000      0.927 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1383389     5  0.5825      0.340 0.000 0.000 0.288 0.224 0.488 0.000
#&gt; SRR1383391     2  0.0146      0.928 0.000 0.996 0.000 0.000 0.004 0.000
#&gt; SRR1383388     4  0.3563      0.747 0.000 0.000 0.000 0.664 0.336 0.000
#&gt; SRR1383392     2  0.1444      0.898 0.000 0.928 0.000 0.000 0.072 0.000
#&gt; SRR1383390     2  0.0458      0.927 0.000 0.984 0.000 0.000 0.016 0.000
#&gt; SRR1383394     2  0.0000      0.927 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1383393     4  0.3964      0.298 0.044 0.000 0.000 0.724 0.000 0.232
#&gt; SRR1383396     4  0.4816      0.706 0.028 0.000 0.032 0.632 0.308 0.000
#&gt; SRR1383395     3  0.3867     -0.349 0.000 0.000 0.512 0.000 0.488 0.000
#&gt; SRR1383399     5  0.5461      0.415 0.000 0.000 0.200 0.228 0.572 0.000
#&gt; SRR1383400     6  0.0000      1.000 0.000 0.000 0.000 0.000 0.000 1.000
#&gt; SRR1383397     2  0.1780      0.880 0.000 0.924 0.000 0.048 0.028 0.000
#&gt; SRR1383401     2  0.2920      0.856 0.000 0.864 0.016 0.040 0.080 0.000
#&gt; SRR1383398     4  0.3563      0.747 0.000 0.000 0.000 0.664 0.336 0.000
#&gt; SRR1383402     2  0.0000      0.927 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1383404     4  0.3563      0.747 0.000 0.000 0.000 0.664 0.336 0.000
#&gt; SRR1383403     4  0.3964      0.298 0.044 0.000 0.000 0.724 0.000 0.232
#&gt; SRR1383405     2  0.0000      0.927 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1383406     4  0.3563      0.747 0.000 0.000 0.000 0.664 0.336 0.000
#&gt; SRR1383407     3  0.3766      0.505 0.212 0.000 0.748 0.000 0.040 0.000
#&gt; SRR1383408     2  0.0363      0.927 0.000 0.988 0.000 0.000 0.012 0.000
#&gt; SRR1383409     2  0.0146      0.928 0.000 0.996 0.000 0.000 0.004 0.000
#&gt; SRR1383410     2  0.1444      0.898 0.000 0.928 0.000 0.000 0.072 0.000
</code></pre>

<script>
$('#tab-ATC-hclust-get-classes-5-a').parent().next().next().hide();
$('#tab-ATC-hclust-get-classes-5-a').click(function(){
  $('#tab-ATC-hclust-get-classes-5-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>
</div>

Heatmaps for the consensus matrix. It visualizes the probability of two
samples to be in a same group.



<script>
$( function() {
	$( '#tabs-ATC-hclust-consensus-heatmap' ).tabs();
} );
</script>
<div id='tabs-ATC-hclust-consensus-heatmap'>
<ul>
<li><a href='#tab-ATC-hclust-consensus-heatmap-1'>k = 2</a></li>
<li><a href='#tab-ATC-hclust-consensus-heatmap-2'>k = 3</a></li>
<li><a href='#tab-ATC-hclust-consensus-heatmap-3'>k = 4</a></li>
<li><a href='#tab-ATC-hclust-consensus-heatmap-4'>k = 5</a></li>
<li><a href='#tab-ATC-hclust-consensus-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-ATC-hclust-consensus-heatmap-1'>
<pre><code class="r">consensus_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-ATC-hclust-consensus-heatmap-1-1.png" alt="plot of chunk tab-ATC-hclust-consensus-heatmap-1"/></p>

</div>
<div id='tab-ATC-hclust-consensus-heatmap-2'>
<pre><code class="r">consensus_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-ATC-hclust-consensus-heatmap-2-1.png" alt="plot of chunk tab-ATC-hclust-consensus-heatmap-2"/></p>

</div>
<div id='tab-ATC-hclust-consensus-heatmap-3'>
<pre><code class="r">consensus_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-ATC-hclust-consensus-heatmap-3-1.png" alt="plot of chunk tab-ATC-hclust-consensus-heatmap-3"/></p>

</div>
<div id='tab-ATC-hclust-consensus-heatmap-4'>
<pre><code class="r">consensus_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-ATC-hclust-consensus-heatmap-4-1.png" alt="plot of chunk tab-ATC-hclust-consensus-heatmap-4"/></p>

</div>
<div id='tab-ATC-hclust-consensus-heatmap-5'>
<pre><code class="r">consensus_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-ATC-hclust-consensus-heatmap-5-1.png" alt="plot of chunk tab-ATC-hclust-consensus-heatmap-5"/></p>

</div>
</div>

Heatmaps for the membership of samples in all partitions to see how consistent they are:




<script>
$( function() {
	$( '#tabs-ATC-hclust-membership-heatmap' ).tabs();
} );
</script>
<div id='tabs-ATC-hclust-membership-heatmap'>
<ul>
<li><a href='#tab-ATC-hclust-membership-heatmap-1'>k = 2</a></li>
<li><a href='#tab-ATC-hclust-membership-heatmap-2'>k = 3</a></li>
<li><a href='#tab-ATC-hclust-membership-heatmap-3'>k = 4</a></li>
<li><a href='#tab-ATC-hclust-membership-heatmap-4'>k = 5</a></li>
<li><a href='#tab-ATC-hclust-membership-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-ATC-hclust-membership-heatmap-1'>
<pre><code class="r">membership_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-ATC-hclust-membership-heatmap-1-1.png" alt="plot of chunk tab-ATC-hclust-membership-heatmap-1"/></p>

</div>
<div id='tab-ATC-hclust-membership-heatmap-2'>
<pre><code class="r">membership_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-ATC-hclust-membership-heatmap-2-1.png" alt="plot of chunk tab-ATC-hclust-membership-heatmap-2"/></p>

</div>
<div id='tab-ATC-hclust-membership-heatmap-3'>
<pre><code class="r">membership_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-ATC-hclust-membership-heatmap-3-1.png" alt="plot of chunk tab-ATC-hclust-membership-heatmap-3"/></p>

</div>
<div id='tab-ATC-hclust-membership-heatmap-4'>
<pre><code class="r">membership_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-ATC-hclust-membership-heatmap-4-1.png" alt="plot of chunk tab-ATC-hclust-membership-heatmap-4"/></p>

</div>
<div id='tab-ATC-hclust-membership-heatmap-5'>
<pre><code class="r">membership_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-ATC-hclust-membership-heatmap-5-1.png" alt="plot of chunk tab-ATC-hclust-membership-heatmap-5"/></p>

</div>
</div>

As soon as we have had the classes for columns, we can look for signatures
which are significantly different between classes which can be candidate marks
for certain classes. Following are the heatmaps for signatures.



Signature heatmaps where rows are scaled:



<script>
$( function() {
	$( '#tabs-ATC-hclust-get-signatures' ).tabs();
} );
</script>
<div id='tabs-ATC-hclust-get-signatures'>
<ul>
<li><a href='#tab-ATC-hclust-get-signatures-1'>k = 2</a></li>
<li><a href='#tab-ATC-hclust-get-signatures-2'>k = 3</a></li>
<li><a href='#tab-ATC-hclust-get-signatures-3'>k = 4</a></li>
<li><a href='#tab-ATC-hclust-get-signatures-4'>k = 5</a></li>
<li><a href='#tab-ATC-hclust-get-signatures-5'>k = 6</a></li>
</ul>
<div id='tab-ATC-hclust-get-signatures-1'>
<pre><code class="r">get_signatures(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-ATC-hclust-get-signatures-1-1.png" alt="plot of chunk tab-ATC-hclust-get-signatures-1"/></p>

</div>
<div id='tab-ATC-hclust-get-signatures-2'>
<pre><code class="r">get_signatures(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-ATC-hclust-get-signatures-2-1.png" alt="plot of chunk tab-ATC-hclust-get-signatures-2"/></p>

</div>
<div id='tab-ATC-hclust-get-signatures-3'>
<pre><code class="r">get_signatures(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-ATC-hclust-get-signatures-3-1.png" alt="plot of chunk tab-ATC-hclust-get-signatures-3"/></p>

</div>
<div id='tab-ATC-hclust-get-signatures-4'>
<pre><code class="r">get_signatures(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-ATC-hclust-get-signatures-4-1.png" alt="plot of chunk tab-ATC-hclust-get-signatures-4"/></p>

</div>
<div id='tab-ATC-hclust-get-signatures-5'>
<pre><code class="r">get_signatures(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-ATC-hclust-get-signatures-5-1.png" alt="plot of chunk tab-ATC-hclust-get-signatures-5"/></p>

</div>
</div>



Signature heatmaps where rows are not scaled:


<script>
$( function() {
	$( '#tabs-ATC-hclust-get-signatures-no-scale' ).tabs();
} );
</script>
<div id='tabs-ATC-hclust-get-signatures-no-scale'>
<ul>
<li><a href='#tab-ATC-hclust-get-signatures-no-scale-1'>k = 2</a></li>
<li><a href='#tab-ATC-hclust-get-signatures-no-scale-2'>k = 3</a></li>
<li><a href='#tab-ATC-hclust-get-signatures-no-scale-3'>k = 4</a></li>
<li><a href='#tab-ATC-hclust-get-signatures-no-scale-4'>k = 5</a></li>
<li><a href='#tab-ATC-hclust-get-signatures-no-scale-5'>k = 6</a></li>
</ul>
<div id='tab-ATC-hclust-get-signatures-no-scale-1'>
<pre><code class="r">get_signatures(res, k = 2, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-ATC-hclust-get-signatures-no-scale-1-1.png" alt="plot of chunk tab-ATC-hclust-get-signatures-no-scale-1"/></p>

</div>
<div id='tab-ATC-hclust-get-signatures-no-scale-2'>
<pre><code class="r">get_signatures(res, k = 3, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-ATC-hclust-get-signatures-no-scale-2-1.png" alt="plot of chunk tab-ATC-hclust-get-signatures-no-scale-2"/></p>

</div>
<div id='tab-ATC-hclust-get-signatures-no-scale-3'>
<pre><code class="r">get_signatures(res, k = 4, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-ATC-hclust-get-signatures-no-scale-3-1.png" alt="plot of chunk tab-ATC-hclust-get-signatures-no-scale-3"/></p>

</div>
<div id='tab-ATC-hclust-get-signatures-no-scale-4'>
<pre><code class="r">get_signatures(res, k = 5, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-ATC-hclust-get-signatures-no-scale-4-1.png" alt="plot of chunk tab-ATC-hclust-get-signatures-no-scale-4"/></p>

</div>
<div id='tab-ATC-hclust-get-signatures-no-scale-5'>
<pre><code class="r">get_signatures(res, k = 6, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-ATC-hclust-get-signatures-no-scale-5-1.png" alt="plot of chunk tab-ATC-hclust-get-signatures-no-scale-5"/></p>

</div>
</div>



Compare the overlap of signatures from different k:

```r
compare_signatures(res)
```

![plot of chunk ATC-hclust-signature_compare](figure_cola/ATC-hclust-signature_compare-1.png)

`get_signature()` returns a data frame invisibly. TO get the list of signatures, the function
call should be assigned to a variable explicitly. In following code, if `plot` argument is set
to `FALSE`, no heatmap is plotted while only the differential analysis is performed.

```r
# code only for demonstration
tb = get_signature(res, k = ..., plot = FALSE)
```

An example of the output of `tb` is:

```
#>   which_row         fdr    mean_1    mean_2 scaled_mean_1 scaled_mean_2 km
#> 1        38 0.042760348  8.373488  9.131774    -0.5533452     0.5164555  1
#> 2        40 0.018707592  7.106213  8.469186    -0.6173731     0.5762149  1
#> 3        55 0.019134737 10.221463 11.207825    -0.6159697     0.5749050  1
#> 4        59 0.006059896  5.921854  7.869574    -0.6899429     0.6439467  1
#> 5        60 0.018055526  8.928898 10.211722    -0.6204761     0.5791110  1
#> 6        98 0.009384629 15.714769 14.887706     0.6635654    -0.6193277  2
...
```

The columns in `tb` are:

1. `which_row`: row indices corresponding to the input matrix.
2. `fdr`: FDR for the differential test. 
3. `mean_x`: The mean value in group x.
4. `scaled_mean_x`: The mean value in group x after rows are scaled.
5. `km`: Row groups if k-means clustering is applied to rows.



UMAP plot which shows how samples are separated.


<script>
$( function() {
	$( '#tabs-ATC-hclust-dimension-reduction' ).tabs();
} );
</script>
<div id='tabs-ATC-hclust-dimension-reduction'>
<ul>
<li><a href='#tab-ATC-hclust-dimension-reduction-1'>k = 2</a></li>
<li><a href='#tab-ATC-hclust-dimension-reduction-2'>k = 3</a></li>
<li><a href='#tab-ATC-hclust-dimension-reduction-3'>k = 4</a></li>
<li><a href='#tab-ATC-hclust-dimension-reduction-4'>k = 5</a></li>
<li><a href='#tab-ATC-hclust-dimension-reduction-5'>k = 6</a></li>
</ul>
<div id='tab-ATC-hclust-dimension-reduction-1'>
<pre><code class="r">dimension_reduction(res, k = 2, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-ATC-hclust-dimension-reduction-1-1.png" alt="plot of chunk tab-ATC-hclust-dimension-reduction-1"/></p>

</div>
<div id='tab-ATC-hclust-dimension-reduction-2'>
<pre><code class="r">dimension_reduction(res, k = 3, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-ATC-hclust-dimension-reduction-2-1.png" alt="plot of chunk tab-ATC-hclust-dimension-reduction-2"/></p>

</div>
<div id='tab-ATC-hclust-dimension-reduction-3'>
<pre><code class="r">dimension_reduction(res, k = 4, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-ATC-hclust-dimension-reduction-3-1.png" alt="plot of chunk tab-ATC-hclust-dimension-reduction-3"/></p>

</div>
<div id='tab-ATC-hclust-dimension-reduction-4'>
<pre><code class="r">dimension_reduction(res, k = 5, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-ATC-hclust-dimension-reduction-4-1.png" alt="plot of chunk tab-ATC-hclust-dimension-reduction-4"/></p>

</div>
<div id='tab-ATC-hclust-dimension-reduction-5'>
<pre><code class="r">dimension_reduction(res, k = 6, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-ATC-hclust-dimension-reduction-5-1.png" alt="plot of chunk tab-ATC-hclust-dimension-reduction-5"/></p>

</div>
</div>


Following heatmap shows how subgroups are split when increasing `k`:

```r
collect_classes(res)
```

![plot of chunk ATC-hclust-collect-classes](figure_cola/ATC-hclust-collect-classes-1.png)


If matrix rows can be associated to genes, consider to use `functional_enrichment(res,
...)` to perform function enrichment for the signature genes. See [this vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/functional_enrichment.html) for more detailed explanations.


 

---------------------------------------------------




### ATC:kmeans






The object with results only for a single top-value method and a single partition method 
can be extracted as:

```r
res = res_list["ATC", "kmeans"]
# you can also extract it by
# res = res_list["ATC:kmeans"]
```

A summary of `res` and all the functions that can be applied to it:

```r
res
```

```
#> A 'ConsensusPartition' object with k = 2, 3, 4, 5, 6.
#>   On a matrix with 15680 rows and 53 columns.
#>   Top rows (1000, 2000, 3000, 4000, 5000) are extracted by 'ATC' method.
#>   Subgroups are detected by 'kmeans' method.
#>   Performed in total 1250 partitions by row resampling.
#>   Best k for subgroups seems to be 3.
#> 
#> Following methods can be applied to this 'ConsensusPartition' object:
#>  [1] "cola_report"             "collect_classes"         "collect_plots"          
#>  [4] "collect_stats"           "colnames"                "compare_signatures"     
#>  [7] "consensus_heatmap"       "dimension_reduction"     "functional_enrichment"  
#> [10] "get_anno_col"            "get_anno"                "get_classes"            
#> [13] "get_consensus"           "get_matrix"              "get_membership"         
#> [16] "get_param"               "get_signatures"          "get_stats"              
#> [19] "is_best_k"               "is_stable_k"             "membership_heatmap"     
#> [22] "ncol"                    "nrow"                    "plot_ecdf"              
#> [25] "rownames"                "select_partition_number" "show"                   
#> [28] "suggest_best_k"          "test_to_known_factors"
```

`collect_plots()` function collects all the plots made from `res` for all `k` (number of partitions)
into one single page to provide an easy and fast comparison between different `k`.

```r
collect_plots(res)
```

![plot of chunk ATC-kmeans-collect-plots](figure_cola/ATC-kmeans-collect-plots-1.png)

The plots are:

- The first row: a plot of the ECDF (empirical cumulative distribution
  function) curves of the consensus matrix for each `k` and the heatmap of
  predicted classes for each `k`.
- The second row: heatmaps of the consensus matrix for each `k`.
- The third row: heatmaps of the membership matrix for each `k`.
- The fouth row: heatmaps of the signatures for each `k`.

All the plots in panels can be made by individual functions and they are
plotted later in this section.

`select_partition_number()` produces several plots showing different
statistics for choosing "optimized" `k`. There are following statistics:

- ECDF curves of the consensus matrix for each `k`;
- 1-PAC. [The PAC
  score](https://en.wikipedia.org/wiki/Consensus_clustering#Over-interpretation_potential_of_consensus_clustering)
  measures the proportion of the ambiguous subgrouping.
- Mean silhouette score.
- Concordance. The mean probability of fiting the consensus class ids in all
  partitions.
- Area increased. Denote $A_k$ as the area under the ECDF curve for current
  `k`, the area increased is defined as $A_k - A_{k-1}$.
- Rand index. The percent of pairs of samples that are both in a same cluster
  or both are not in a same cluster in the partition of k and k-1.
- Jaccard index. The ratio of pairs of samples are both in a same cluster in
  the partition of k and k-1 and the pairs of samples are both in a same
  cluster in the partition k or k-1.

The detailed explanations of these statistics can be found in [the _cola_
vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/cola.html#toc_13).

Generally speaking, lower PAC score, higher mean silhouette score or higher
concordance corresponds to better partition. Rand index and Jaccard index
measure how similar the current partition is compared to partition with `k-1`.
If they are too similar, we won't accept `k` is better than `k-1`.

```r
select_partition_number(res)
```

![plot of chunk ATC-kmeans-select-partition-number](figure_cola/ATC-kmeans-select-partition-number-1.png)

The numeric values for all these statistics can be obtained by `get_stats()`.

```r
get_stats(res)
```

```
#>   k 1-PAC mean_silhouette concordance area_increased  Rand Jaccard
#> 2 2 0.813           0.833       0.925         0.4804 0.505   0.505
#> 3 3 0.900           0.903       0.962         0.2991 0.726   0.528
#> 4 4 0.734           0.716       0.794         0.1463 0.902   0.747
#> 5 5 0.847           0.920       0.923         0.0946 0.881   0.615
#> 6 6 0.843           0.840       0.874         0.0454 1.000   1.000
```

`suggest_best_k()` suggests the best $k$ based on these statistics. The rules are as follows:

- All $k$ with Jaccard index larger than 0.95 are removed because increasing
  $k$ does not provide enough extra information. If all $k$ are removed, it is
  marked as no subgroup is detected.
- For all $k$ with 1-PAC score larger than 0.9, the maximal $k$ is taken as
  the best $k$, and other $k$ are marked as optional $k$.
- If it does not fit the second rule. The $k$ with the maximal vote of the
  highest 1-PAC score, highest mean silhouette, and highest concordance is
  taken as the best $k$.

```r
suggest_best_k(res)
```

```
#> [1] 3
```


Following shows the table of the partitions (You need to click the **show/hide
code output** link to see it). The membership matrix (columns with name `p*`)
is inferred by
[`clue::cl_consensus()`](https://www.rdocumentation.org/link/cl_consensus?package=clue)
function with the `SE` method. Basically the value in the membership matrix
represents the probability to belong to a certain group. The finall class
label for an item is determined with the group with highest probability it
belongs to.

In `get_classes()` function, the entropy is calculated from the membership
matrix and the silhouette score is calculated from the consensus matrix.



<script>
$( function() {
	$( '#tabs-ATC-kmeans-get-classes' ).tabs();
} );
</script>
<div id='tabs-ATC-kmeans-get-classes'>
<ul>
<li><a href='#tab-ATC-kmeans-get-classes-1'>k = 2</a></li>
<li><a href='#tab-ATC-kmeans-get-classes-2'>k = 3</a></li>
<li><a href='#tab-ATC-kmeans-get-classes-3'>k = 4</a></li>
<li><a href='#tab-ATC-kmeans-get-classes-4'>k = 5</a></li>
<li><a href='#tab-ATC-kmeans-get-classes-5'>k = 6</a></li>
</ul>

<div id='tab-ATC-kmeans-get-classes-1'>
<p><a id='tab-ATC-kmeans-get-classes-1-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 2), get_membership(res, k = 2))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2
#&gt; SRR1383358     2   0.821    0.62285 0.256 0.744
#&gt; SRR1383360     1   0.388    0.89878 0.924 0.076
#&gt; SRR1383359     1   0.388    0.89878 0.924 0.076
#&gt; SRR1383362     1   0.000    0.88695 1.000 0.000
#&gt; SRR1383361     1   0.388    0.89878 0.924 0.076
#&gt; SRR1383363     1   0.388    0.89878 0.924 0.076
#&gt; SRR1383364     1   0.388    0.89878 0.924 0.076
#&gt; SRR1383365     1   0.388    0.89878 0.924 0.076
#&gt; SRR1383366     2   0.000    0.92892 0.000 1.000
#&gt; SRR1383367     2   0.821    0.62285 0.256 0.744
#&gt; SRR1383368     1   0.184    0.89276 0.972 0.028
#&gt; SRR1383369     2   0.795    0.65104 0.240 0.760
#&gt; SRR1383370     1   0.388    0.89878 0.924 0.076
#&gt; SRR1383371     1   0.388    0.89878 0.924 0.076
#&gt; SRR1383372     2   0.000    0.92892 0.000 1.000
#&gt; SRR1383373     1   0.388    0.89878 0.924 0.076
#&gt; SRR1383374     2   0.000    0.92892 0.000 1.000
#&gt; SRR1383375     1   0.000    0.88695 1.000 0.000
#&gt; SRR1383376     2   0.000    0.92892 0.000 1.000
#&gt; SRR1383377     1   0.963    0.42408 0.612 0.388
#&gt; SRR1383378     2   0.295    0.89789 0.052 0.948
#&gt; SRR1383379     2   0.000    0.92892 0.000 1.000
#&gt; SRR1383380     2   0.311    0.89489 0.056 0.944
#&gt; SRR1383381     1   1.000    0.10936 0.508 0.492
#&gt; SRR1383382     1   0.000    0.88695 1.000 0.000
#&gt; SRR1383383     2   0.000    0.92892 0.000 1.000
#&gt; SRR1383385     1   0.000    0.88695 1.000 0.000
#&gt; SRR1383384     2   0.000    0.92892 0.000 1.000
#&gt; SRR1383386     2   0.311    0.89489 0.056 0.944
#&gt; SRR1383387     2   0.000    0.92892 0.000 1.000
#&gt; SRR1383389     2   0.996    0.00319 0.464 0.536
#&gt; SRR1383391     2   0.000    0.92892 0.000 1.000
#&gt; SRR1383388     2   0.295    0.89789 0.052 0.948
#&gt; SRR1383392     2   0.000    0.92892 0.000 1.000
#&gt; SRR1383390     2   0.000    0.92892 0.000 1.000
#&gt; SRR1383394     2   0.000    0.92892 0.000 1.000
#&gt; SRR1383393     1   0.000    0.88695 1.000 0.000
#&gt; SRR1383396     1   0.141    0.89095 0.980 0.020
#&gt; SRR1383395     2   0.795    0.65104 0.240 0.760
#&gt; SRR1383399     1   1.000    0.10936 0.508 0.492
#&gt; SRR1383400     1   0.000    0.88695 1.000 0.000
#&gt; SRR1383397     2   0.000    0.92892 0.000 1.000
#&gt; SRR1383401     2   0.000    0.92892 0.000 1.000
#&gt; SRR1383398     2   0.311    0.89489 0.056 0.944
#&gt; SRR1383402     2   0.000    0.92892 0.000 1.000
#&gt; SRR1383404     2   0.295    0.89789 0.052 0.948
#&gt; SRR1383403     1   0.000    0.88695 1.000 0.000
#&gt; SRR1383405     2   0.000    0.92892 0.000 1.000
#&gt; SRR1383406     2   0.000    0.92892 0.000 1.000
#&gt; SRR1383407     1   0.388    0.89878 0.924 0.076
#&gt; SRR1383408     2   0.000    0.92892 0.000 1.000
#&gt; SRR1383409     2   0.000    0.92892 0.000 1.000
#&gt; SRR1383410     2   0.000    0.92892 0.000 1.000
</code></pre>

<script>
$('#tab-ATC-kmeans-get-classes-1-a').parent().next().next().hide();
$('#tab-ATC-kmeans-get-classes-1-a').click(function(){
  $('#tab-ATC-kmeans-get-classes-1-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-ATC-kmeans-get-classes-2'>
<p><a id='tab-ATC-kmeans-get-classes-2-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 3), get_membership(res, k = 3))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3
#&gt; SRR1383358     3   0.000      0.928 0.000 0.000 1.000
#&gt; SRR1383360     3   0.000      0.928 0.000 0.000 1.000
#&gt; SRR1383359     3   0.000      0.928 0.000 0.000 1.000
#&gt; SRR1383362     1   0.000      1.000 1.000 0.000 0.000
#&gt; SRR1383361     3   0.000      0.928 0.000 0.000 1.000
#&gt; SRR1383363     3   0.000      0.928 0.000 0.000 1.000
#&gt; SRR1383364     3   0.000      0.928 0.000 0.000 1.000
#&gt; SRR1383365     3   0.000      0.928 0.000 0.000 1.000
#&gt; SRR1383366     3   0.615      0.299 0.000 0.408 0.592
#&gt; SRR1383367     3   0.000      0.928 0.000 0.000 1.000
#&gt; SRR1383368     3   0.000      0.928 0.000 0.000 1.000
#&gt; SRR1383369     3   0.000      0.928 0.000 0.000 1.000
#&gt; SRR1383370     3   0.000      0.928 0.000 0.000 1.000
#&gt; SRR1383371     3   0.000      0.928 0.000 0.000 1.000
#&gt; SRR1383372     3   0.614      0.310 0.000 0.404 0.596
#&gt; SRR1383373     3   0.000      0.928 0.000 0.000 1.000
#&gt; SRR1383374     2   0.497      0.668 0.000 0.764 0.236
#&gt; SRR1383375     1   0.000      1.000 1.000 0.000 0.000
#&gt; SRR1383376     2   0.000      0.965 0.000 1.000 0.000
#&gt; SRR1383377     3   0.000      0.928 0.000 0.000 1.000
#&gt; SRR1383378     2   0.129      0.944 0.032 0.968 0.000
#&gt; SRR1383379     2   0.000      0.965 0.000 1.000 0.000
#&gt; SRR1383380     2   0.382      0.840 0.148 0.852 0.000
#&gt; SRR1383381     3   0.000      0.928 0.000 0.000 1.000
#&gt; SRR1383382     1   0.000      1.000 1.000 0.000 0.000
#&gt; SRR1383383     2   0.000      0.965 0.000 1.000 0.000
#&gt; SRR1383385     1   0.000      1.000 1.000 0.000 0.000
#&gt; SRR1383384     2   0.000      0.965 0.000 1.000 0.000
#&gt; SRR1383386     2   0.382      0.840 0.148 0.852 0.000
#&gt; SRR1383387     2   0.000      0.965 0.000 1.000 0.000
#&gt; SRR1383389     3   0.000      0.928 0.000 0.000 1.000
#&gt; SRR1383391     2   0.000      0.965 0.000 1.000 0.000
#&gt; SRR1383388     2   0.000      0.965 0.000 1.000 0.000
#&gt; SRR1383392     2   0.000      0.965 0.000 1.000 0.000
#&gt; SRR1383390     2   0.000      0.965 0.000 1.000 0.000
#&gt; SRR1383394     2   0.000      0.965 0.000 1.000 0.000
#&gt; SRR1383393     1   0.000      1.000 1.000 0.000 0.000
#&gt; SRR1383396     3   0.623      0.181 0.436 0.000 0.564
#&gt; SRR1383395     3   0.000      0.928 0.000 0.000 1.000
#&gt; SRR1383399     3   0.000      0.928 0.000 0.000 1.000
#&gt; SRR1383400     1   0.000      1.000 1.000 0.000 0.000
#&gt; SRR1383397     2   0.000      0.965 0.000 1.000 0.000
#&gt; SRR1383401     2   0.000      0.965 0.000 1.000 0.000
#&gt; SRR1383398     2   0.382      0.840 0.148 0.852 0.000
#&gt; SRR1383402     2   0.000      0.965 0.000 1.000 0.000
#&gt; SRR1383404     2   0.129      0.944 0.032 0.968 0.000
#&gt; SRR1383403     1   0.000      1.000 1.000 0.000 0.000
#&gt; SRR1383405     2   0.000      0.965 0.000 1.000 0.000
#&gt; SRR1383406     2   0.000      0.965 0.000 1.000 0.000
#&gt; SRR1383407     3   0.000      0.928 0.000 0.000 1.000
#&gt; SRR1383408     2   0.000      0.965 0.000 1.000 0.000
#&gt; SRR1383409     2   0.000      0.965 0.000 1.000 0.000
#&gt; SRR1383410     2   0.000      0.965 0.000 1.000 0.000
</code></pre>

<script>
$('#tab-ATC-kmeans-get-classes-2-a').parent().next().next().hide();
$('#tab-ATC-kmeans-get-classes-2-a').click(function(){
  $('#tab-ATC-kmeans-get-classes-2-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-ATC-kmeans-get-classes-3'>
<p><a id='tab-ATC-kmeans-get-classes-3-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 4), get_membership(res, k = 4))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4
#&gt; SRR1383358     3  0.1545      0.809 0.000 0.008 0.952 0.040
#&gt; SRR1383360     3  0.4830      0.693 0.000 0.000 0.608 0.392
#&gt; SRR1383359     3  0.5816      0.664 0.036 0.000 0.572 0.392
#&gt; SRR1383362     1  0.0188      0.917 0.996 0.000 0.000 0.004
#&gt; SRR1383361     3  0.2081      0.807 0.000 0.000 0.916 0.084
#&gt; SRR1383363     3  0.0336      0.817 0.000 0.000 0.992 0.008
#&gt; SRR1383364     3  0.5816      0.664 0.036 0.000 0.572 0.392
#&gt; SRR1383365     3  0.4804      0.696 0.000 0.000 0.616 0.384
#&gt; SRR1383366     3  0.4745      0.598 0.000 0.208 0.756 0.036
#&gt; SRR1383367     3  0.1807      0.804 0.000 0.008 0.940 0.052
#&gt; SRR1383368     3  0.2081      0.812 0.000 0.000 0.916 0.084
#&gt; SRR1383369     3  0.1356      0.811 0.000 0.008 0.960 0.032
#&gt; SRR1383370     3  0.1792      0.810 0.000 0.000 0.932 0.068
#&gt; SRR1383371     3  0.4830      0.693 0.000 0.000 0.608 0.392
#&gt; SRR1383372     3  0.3320      0.757 0.000 0.068 0.876 0.056
#&gt; SRR1383373     3  0.4804      0.696 0.000 0.000 0.616 0.384
#&gt; SRR1383374     2  0.5368      0.308 0.000 0.636 0.340 0.024
#&gt; SRR1383375     1  0.2814      0.925 0.868 0.000 0.000 0.132
#&gt; SRR1383376     2  0.0000      0.811 0.000 1.000 0.000 0.000
#&gt; SRR1383377     3  0.0469      0.817 0.000 0.000 0.988 0.012
#&gt; SRR1383378     4  0.6020      0.847 0.004 0.376 0.040 0.580
#&gt; SRR1383379     2  0.4907     -0.331 0.000 0.580 0.000 0.420
#&gt; SRR1383380     4  0.6020      0.847 0.004 0.376 0.040 0.580
#&gt; SRR1383381     3  0.1545      0.810 0.000 0.008 0.952 0.040
#&gt; SRR1383382     1  0.0188      0.917 0.996 0.000 0.000 0.004
#&gt; SRR1383383     2  0.0000      0.811 0.000 1.000 0.000 0.000
#&gt; SRR1383385     1  0.2760      0.926 0.872 0.000 0.000 0.128
#&gt; SRR1383384     2  0.0000      0.811 0.000 1.000 0.000 0.000
#&gt; SRR1383386     4  0.6020      0.847 0.004 0.376 0.040 0.580
#&gt; SRR1383387     2  0.0336      0.809 0.000 0.992 0.000 0.008
#&gt; SRR1383389     3  0.1452      0.810 0.000 0.008 0.956 0.036
#&gt; SRR1383391     2  0.0336      0.809 0.000 0.992 0.000 0.008
#&gt; SRR1383388     4  0.5080      0.751 0.004 0.420 0.000 0.576
#&gt; SRR1383392     2  0.2521      0.723 0.000 0.912 0.064 0.024
#&gt; SRR1383390     2  0.0000      0.811 0.000 1.000 0.000 0.000
#&gt; SRR1383394     2  0.0336      0.809 0.000 0.992 0.000 0.008
#&gt; SRR1383393     1  0.2345      0.930 0.900 0.000 0.000 0.100
#&gt; SRR1383396     4  0.6774      0.240 0.120 0.000 0.312 0.568
#&gt; SRR1383395     3  0.1545      0.810 0.000 0.008 0.952 0.040
#&gt; SRR1383399     3  0.1545      0.810 0.000 0.008 0.952 0.040
#&gt; SRR1383400     1  0.0000      0.919 1.000 0.000 0.000 0.000
#&gt; SRR1383397     2  0.4907     -0.331 0.000 0.580 0.000 0.420
#&gt; SRR1383401     2  0.2443      0.729 0.000 0.916 0.060 0.024
#&gt; SRR1383398     4  0.6020      0.847 0.004 0.376 0.040 0.580
#&gt; SRR1383402     2  0.0336      0.809 0.000 0.992 0.000 0.008
#&gt; SRR1383404     4  0.6020      0.847 0.004 0.376 0.040 0.580
#&gt; SRR1383403     1  0.2814      0.925 0.868 0.000 0.000 0.132
#&gt; SRR1383405     2  0.0336      0.809 0.000 0.992 0.000 0.008
#&gt; SRR1383406     2  0.4961     -0.430 0.000 0.552 0.000 0.448
#&gt; SRR1383407     3  0.4843      0.692 0.000 0.000 0.604 0.396
#&gt; SRR1383408     2  0.0000      0.811 0.000 1.000 0.000 0.000
#&gt; SRR1383409     2  0.0336      0.809 0.000 0.992 0.000 0.008
#&gt; SRR1383410     2  0.0817      0.792 0.000 0.976 0.000 0.024
</code></pre>

<script>
$('#tab-ATC-kmeans-get-classes-3-a').parent().next().next().hide();
$('#tab-ATC-kmeans-get-classes-3-a').click(function(){
  $('#tab-ATC-kmeans-get-classes-3-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-ATC-kmeans-get-classes-4'>
<p><a id='tab-ATC-kmeans-get-classes-4-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 5), get_membership(res, k = 5))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4    p5
#&gt; SRR1383358     3  0.0324      0.965 0.000 0.004 0.992 0.004 0.000
#&gt; SRR1383360     5  0.2929      0.965 0.000 0.000 0.152 0.008 0.840
#&gt; SRR1383359     5  0.2672      0.974 0.004 0.000 0.116 0.008 0.872
#&gt; SRR1383362     1  0.1478      0.894 0.936 0.000 0.000 0.000 0.064
#&gt; SRR1383361     3  0.0798      0.960 0.000 0.000 0.976 0.008 0.016
#&gt; SRR1383363     3  0.0579      0.963 0.000 0.000 0.984 0.008 0.008
#&gt; SRR1383364     5  0.2672      0.974 0.004 0.000 0.116 0.008 0.872
#&gt; SRR1383365     5  0.2660      0.979 0.000 0.000 0.128 0.008 0.864
#&gt; SRR1383366     3  0.2300      0.908 0.000 0.072 0.904 0.024 0.000
#&gt; SRR1383367     3  0.0451      0.964 0.000 0.004 0.988 0.008 0.000
#&gt; SRR1383368     3  0.0693      0.964 0.000 0.000 0.980 0.008 0.012
#&gt; SRR1383369     3  0.1399      0.949 0.000 0.028 0.952 0.020 0.000
#&gt; SRR1383370     3  0.0798      0.960 0.000 0.000 0.976 0.008 0.016
#&gt; SRR1383371     5  0.2329      0.979 0.000 0.000 0.124 0.000 0.876
#&gt; SRR1383372     3  0.1168      0.949 0.000 0.032 0.960 0.008 0.000
#&gt; SRR1383373     5  0.2929      0.965 0.000 0.000 0.152 0.008 0.840
#&gt; SRR1383374     2  0.4524      0.427 0.000 0.644 0.336 0.020 0.000
#&gt; SRR1383375     1  0.2230      0.919 0.884 0.000 0.000 0.116 0.000
#&gt; SRR1383376     2  0.0955      0.943 0.000 0.968 0.000 0.028 0.004
#&gt; SRR1383377     3  0.1538      0.957 0.000 0.008 0.948 0.036 0.008
#&gt; SRR1383378     4  0.1757      0.910 0.004 0.048 0.000 0.936 0.012
#&gt; SRR1383379     4  0.3319      0.845 0.000 0.160 0.000 0.820 0.020
#&gt; SRR1383380     4  0.1644      0.911 0.004 0.048 0.000 0.940 0.008
#&gt; SRR1383381     3  0.1211      0.956 0.000 0.000 0.960 0.016 0.024
#&gt; SRR1383382     1  0.1478      0.894 0.936 0.000 0.000 0.000 0.064
#&gt; SRR1383383     2  0.0794      0.943 0.000 0.972 0.000 0.028 0.000
#&gt; SRR1383385     1  0.2230      0.919 0.884 0.000 0.000 0.116 0.000
#&gt; SRR1383384     2  0.0794      0.943 0.000 0.972 0.000 0.028 0.000
#&gt; SRR1383386     4  0.1518      0.911 0.004 0.048 0.000 0.944 0.004
#&gt; SRR1383387     2  0.1668      0.937 0.000 0.940 0.000 0.032 0.028
#&gt; SRR1383389     3  0.0898      0.962 0.000 0.000 0.972 0.020 0.008
#&gt; SRR1383391     2  0.1168      0.942 0.000 0.960 0.000 0.032 0.008
#&gt; SRR1383388     4  0.1484      0.909 0.000 0.048 0.000 0.944 0.008
#&gt; SRR1383392     2  0.1012      0.907 0.000 0.968 0.012 0.020 0.000
#&gt; SRR1383390     2  0.0794      0.943 0.000 0.972 0.000 0.028 0.000
#&gt; SRR1383394     2  0.1836      0.934 0.000 0.932 0.000 0.032 0.036
#&gt; SRR1383393     1  0.2179      0.919 0.888 0.000 0.000 0.112 0.000
#&gt; SRR1383396     4  0.3489      0.721 0.016 0.000 0.148 0.824 0.012
#&gt; SRR1383395     3  0.1948      0.950 0.000 0.024 0.932 0.036 0.008
#&gt; SRR1383399     3  0.1211      0.956 0.000 0.000 0.960 0.016 0.024
#&gt; SRR1383400     1  0.1478      0.894 0.936 0.000 0.000 0.000 0.064
#&gt; SRR1383397     4  0.3319      0.845 0.000 0.160 0.000 0.820 0.020
#&gt; SRR1383401     2  0.0693      0.920 0.000 0.980 0.012 0.000 0.008
#&gt; SRR1383398     4  0.1644      0.911 0.004 0.048 0.000 0.940 0.008
#&gt; SRR1383402     2  0.1836      0.934 0.000 0.932 0.000 0.032 0.036
#&gt; SRR1383404     4  0.1518      0.911 0.004 0.048 0.000 0.944 0.004
#&gt; SRR1383403     1  0.2230      0.919 0.884 0.000 0.000 0.116 0.000
#&gt; SRR1383405     2  0.1668      0.937 0.000 0.940 0.000 0.032 0.028
#&gt; SRR1383406     4  0.2971      0.853 0.000 0.156 0.000 0.836 0.008
#&gt; SRR1383407     5  0.2536      0.978 0.000 0.000 0.128 0.004 0.868
#&gt; SRR1383408     2  0.0794      0.943 0.000 0.972 0.000 0.028 0.000
#&gt; SRR1383409     2  0.1168      0.942 0.000 0.960 0.000 0.032 0.008
#&gt; SRR1383410     2  0.0609      0.917 0.000 0.980 0.000 0.020 0.000
</code></pre>

<script>
$('#tab-ATC-kmeans-get-classes-4-a').parent().next().next().hide();
$('#tab-ATC-kmeans-get-classes-4-a').click(function(){
  $('#tab-ATC-kmeans-get-classes-4-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-ATC-kmeans-get-classes-5'>
<p><a id='tab-ATC-kmeans-get-classes-5-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 6), get_membership(res, k = 6))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4    p5 p6
#&gt; SRR1383358     3  0.1958     0.8380 0.000 0.000 0.896 0.000 0.004 NA
#&gt; SRR1383360     5  0.2888     0.8833 0.000 0.000 0.092 0.000 0.852 NA
#&gt; SRR1383359     5  0.1938     0.9136 0.000 0.000 0.020 0.008 0.920 NA
#&gt; SRR1383362     1  0.3050     0.8375 0.764 0.000 0.000 0.000 0.000 NA
#&gt; SRR1383361     3  0.2786     0.8067 0.000 0.000 0.860 0.000 0.084 NA
#&gt; SRR1383363     3  0.1983     0.8274 0.000 0.000 0.908 0.000 0.020 NA
#&gt; SRR1383364     5  0.1938     0.9136 0.000 0.000 0.020 0.008 0.920 NA
#&gt; SRR1383365     5  0.1616     0.9197 0.000 0.000 0.020 0.000 0.932 NA
#&gt; SRR1383366     3  0.3454     0.7949 0.000 0.012 0.760 0.000 0.004 NA
#&gt; SRR1383367     3  0.1588     0.8410 0.000 0.000 0.924 0.000 0.004 NA
#&gt; SRR1383368     3  0.3196     0.7921 0.000 0.000 0.816 0.008 0.020 NA
#&gt; SRR1383369     3  0.3276     0.7972 0.000 0.004 0.764 0.000 0.004 NA
#&gt; SRR1383370     3  0.2786     0.8067 0.000 0.000 0.860 0.000 0.084 NA
#&gt; SRR1383371     5  0.1148     0.9211 0.000 0.000 0.020 0.004 0.960 NA
#&gt; SRR1383372     3  0.2244     0.8377 0.000 0.004 0.888 0.004 0.004 NA
#&gt; SRR1383373     5  0.2948     0.8825 0.000 0.000 0.092 0.000 0.848 NA
#&gt; SRR1383374     2  0.6089    -0.0614 0.000 0.388 0.324 0.000 0.000 NA
#&gt; SRR1383375     1  0.1686     0.8782 0.924 0.000 0.000 0.064 0.012 NA
#&gt; SRR1383376     2  0.0777     0.9014 0.000 0.972 0.000 0.004 0.000 NA
#&gt; SRR1383377     3  0.3773     0.7847 0.000 0.000 0.752 0.000 0.044 NA
#&gt; SRR1383378     4  0.1320     0.8955 0.000 0.016 0.000 0.948 0.000 NA
#&gt; SRR1383379     4  0.3366     0.8459 0.000 0.080 0.000 0.824 0.004 NA
#&gt; SRR1383380     4  0.0964     0.8974 0.012 0.016 0.000 0.968 0.000 NA
#&gt; SRR1383381     3  0.3502     0.7724 0.000 0.000 0.780 0.020 0.008 NA
#&gt; SRR1383382     1  0.3050     0.8375 0.764 0.000 0.000 0.000 0.000 NA
#&gt; SRR1383383     2  0.1141     0.8938 0.000 0.948 0.000 0.000 0.000 NA
#&gt; SRR1383385     1  0.1327     0.8782 0.936 0.000 0.000 0.064 0.000 NA
#&gt; SRR1383384     2  0.0146     0.9003 0.000 0.996 0.000 0.004 0.000 NA
#&gt; SRR1383386     4  0.1320     0.8968 0.000 0.016 0.000 0.948 0.000 NA
#&gt; SRR1383387     2  0.1843     0.8881 0.000 0.912 0.000 0.004 0.004 NA
#&gt; SRR1383389     3  0.2357     0.8136 0.000 0.000 0.872 0.012 0.000 NA
#&gt; SRR1383391     2  0.1757     0.8935 0.000 0.916 0.000 0.008 0.000 NA
#&gt; SRR1383388     4  0.1485     0.8958 0.000 0.024 0.000 0.944 0.004 NA
#&gt; SRR1383392     2  0.1863     0.8578 0.000 0.896 0.000 0.000 0.000 NA
#&gt; SRR1383390     2  0.1152     0.8956 0.000 0.952 0.000 0.004 0.000 NA
#&gt; SRR1383394     2  0.1843     0.8886 0.000 0.912 0.000 0.004 0.004 NA
#&gt; SRR1383393     1  0.1686     0.8782 0.924 0.000 0.000 0.064 0.012 NA
#&gt; SRR1383396     4  0.4745     0.6366 0.000 0.000 0.144 0.700 0.008 NA
#&gt; SRR1383395     3  0.3860     0.7796 0.000 0.000 0.728 0.000 0.036 NA
#&gt; SRR1383399     3  0.3502     0.7724 0.000 0.000 0.780 0.020 0.008 NA
#&gt; SRR1383400     1  0.3050     0.8375 0.764 0.000 0.000 0.000 0.000 NA
#&gt; SRR1383397     4  0.3366     0.8459 0.000 0.080 0.000 0.824 0.004 NA
#&gt; SRR1383401     2  0.3352     0.7884 0.000 0.792 0.032 0.000 0.000 NA
#&gt; SRR1383398     4  0.0964     0.8974 0.012 0.016 0.000 0.968 0.000 NA
#&gt; SRR1383402     2  0.1843     0.8886 0.000 0.912 0.000 0.004 0.004 NA
#&gt; SRR1383404     4  0.1320     0.8968 0.000 0.016 0.000 0.948 0.000 NA
#&gt; SRR1383403     1  0.1327     0.8782 0.936 0.000 0.000 0.064 0.000 NA
#&gt; SRR1383405     2  0.1843     0.8881 0.000 0.912 0.000 0.004 0.004 NA
#&gt; SRR1383406     4  0.2696     0.8683 0.000 0.076 0.000 0.872 0.004 NA
#&gt; SRR1383407     5  0.1984     0.9096 0.000 0.000 0.056 0.000 0.912 NA
#&gt; SRR1383408     2  0.0146     0.9003 0.000 0.996 0.000 0.004 0.000 NA
#&gt; SRR1383409     2  0.1152     0.9003 0.000 0.952 0.000 0.004 0.000 NA
#&gt; SRR1383410     2  0.1267     0.8832 0.000 0.940 0.000 0.000 0.000 NA
</code></pre>

<script>
$('#tab-ATC-kmeans-get-classes-5-a').parent().next().next().hide();
$('#tab-ATC-kmeans-get-classes-5-a').click(function(){
  $('#tab-ATC-kmeans-get-classes-5-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>
</div>

Heatmaps for the consensus matrix. It visualizes the probability of two
samples to be in a same group.



<script>
$( function() {
	$( '#tabs-ATC-kmeans-consensus-heatmap' ).tabs();
} );
</script>
<div id='tabs-ATC-kmeans-consensus-heatmap'>
<ul>
<li><a href='#tab-ATC-kmeans-consensus-heatmap-1'>k = 2</a></li>
<li><a href='#tab-ATC-kmeans-consensus-heatmap-2'>k = 3</a></li>
<li><a href='#tab-ATC-kmeans-consensus-heatmap-3'>k = 4</a></li>
<li><a href='#tab-ATC-kmeans-consensus-heatmap-4'>k = 5</a></li>
<li><a href='#tab-ATC-kmeans-consensus-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-ATC-kmeans-consensus-heatmap-1'>
<pre><code class="r">consensus_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-ATC-kmeans-consensus-heatmap-1-1.png" alt="plot of chunk tab-ATC-kmeans-consensus-heatmap-1"/></p>

</div>
<div id='tab-ATC-kmeans-consensus-heatmap-2'>
<pre><code class="r">consensus_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-ATC-kmeans-consensus-heatmap-2-1.png" alt="plot of chunk tab-ATC-kmeans-consensus-heatmap-2"/></p>

</div>
<div id='tab-ATC-kmeans-consensus-heatmap-3'>
<pre><code class="r">consensus_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-ATC-kmeans-consensus-heatmap-3-1.png" alt="plot of chunk tab-ATC-kmeans-consensus-heatmap-3"/></p>

</div>
<div id='tab-ATC-kmeans-consensus-heatmap-4'>
<pre><code class="r">consensus_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-ATC-kmeans-consensus-heatmap-4-1.png" alt="plot of chunk tab-ATC-kmeans-consensus-heatmap-4"/></p>

</div>
<div id='tab-ATC-kmeans-consensus-heatmap-5'>
<pre><code class="r">consensus_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-ATC-kmeans-consensus-heatmap-5-1.png" alt="plot of chunk tab-ATC-kmeans-consensus-heatmap-5"/></p>

</div>
</div>

Heatmaps for the membership of samples in all partitions to see how consistent they are:




<script>
$( function() {
	$( '#tabs-ATC-kmeans-membership-heatmap' ).tabs();
} );
</script>
<div id='tabs-ATC-kmeans-membership-heatmap'>
<ul>
<li><a href='#tab-ATC-kmeans-membership-heatmap-1'>k = 2</a></li>
<li><a href='#tab-ATC-kmeans-membership-heatmap-2'>k = 3</a></li>
<li><a href='#tab-ATC-kmeans-membership-heatmap-3'>k = 4</a></li>
<li><a href='#tab-ATC-kmeans-membership-heatmap-4'>k = 5</a></li>
<li><a href='#tab-ATC-kmeans-membership-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-ATC-kmeans-membership-heatmap-1'>
<pre><code class="r">membership_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-ATC-kmeans-membership-heatmap-1-1.png" alt="plot of chunk tab-ATC-kmeans-membership-heatmap-1"/></p>

</div>
<div id='tab-ATC-kmeans-membership-heatmap-2'>
<pre><code class="r">membership_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-ATC-kmeans-membership-heatmap-2-1.png" alt="plot of chunk tab-ATC-kmeans-membership-heatmap-2"/></p>

</div>
<div id='tab-ATC-kmeans-membership-heatmap-3'>
<pre><code class="r">membership_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-ATC-kmeans-membership-heatmap-3-1.png" alt="plot of chunk tab-ATC-kmeans-membership-heatmap-3"/></p>

</div>
<div id='tab-ATC-kmeans-membership-heatmap-4'>
<pre><code class="r">membership_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-ATC-kmeans-membership-heatmap-4-1.png" alt="plot of chunk tab-ATC-kmeans-membership-heatmap-4"/></p>

</div>
<div id='tab-ATC-kmeans-membership-heatmap-5'>
<pre><code class="r">membership_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-ATC-kmeans-membership-heatmap-5-1.png" alt="plot of chunk tab-ATC-kmeans-membership-heatmap-5"/></p>

</div>
</div>

As soon as we have had the classes for columns, we can look for signatures
which are significantly different between classes which can be candidate marks
for certain classes. Following are the heatmaps for signatures.



Signature heatmaps where rows are scaled:



<script>
$( function() {
	$( '#tabs-ATC-kmeans-get-signatures' ).tabs();
} );
</script>
<div id='tabs-ATC-kmeans-get-signatures'>
<ul>
<li><a href='#tab-ATC-kmeans-get-signatures-1'>k = 2</a></li>
<li><a href='#tab-ATC-kmeans-get-signatures-2'>k = 3</a></li>
<li><a href='#tab-ATC-kmeans-get-signatures-3'>k = 4</a></li>
<li><a href='#tab-ATC-kmeans-get-signatures-4'>k = 5</a></li>
<li><a href='#tab-ATC-kmeans-get-signatures-5'>k = 6</a></li>
</ul>
<div id='tab-ATC-kmeans-get-signatures-1'>
<pre><code class="r">get_signatures(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-ATC-kmeans-get-signatures-1-1.png" alt="plot of chunk tab-ATC-kmeans-get-signatures-1"/></p>

</div>
<div id='tab-ATC-kmeans-get-signatures-2'>
<pre><code class="r">get_signatures(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-ATC-kmeans-get-signatures-2-1.png" alt="plot of chunk tab-ATC-kmeans-get-signatures-2"/></p>

</div>
<div id='tab-ATC-kmeans-get-signatures-3'>
<pre><code class="r">get_signatures(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-ATC-kmeans-get-signatures-3-1.png" alt="plot of chunk tab-ATC-kmeans-get-signatures-3"/></p>

</div>
<div id='tab-ATC-kmeans-get-signatures-4'>
<pre><code class="r">get_signatures(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-ATC-kmeans-get-signatures-4-1.png" alt="plot of chunk tab-ATC-kmeans-get-signatures-4"/></p>

</div>
<div id='tab-ATC-kmeans-get-signatures-5'>
<pre><code class="r">get_signatures(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-ATC-kmeans-get-signatures-5-1.png" alt="plot of chunk tab-ATC-kmeans-get-signatures-5"/></p>

</div>
</div>



Signature heatmaps where rows are not scaled:


<script>
$( function() {
	$( '#tabs-ATC-kmeans-get-signatures-no-scale' ).tabs();
} );
</script>
<div id='tabs-ATC-kmeans-get-signatures-no-scale'>
<ul>
<li><a href='#tab-ATC-kmeans-get-signatures-no-scale-1'>k = 2</a></li>
<li><a href='#tab-ATC-kmeans-get-signatures-no-scale-2'>k = 3</a></li>
<li><a href='#tab-ATC-kmeans-get-signatures-no-scale-3'>k = 4</a></li>
<li><a href='#tab-ATC-kmeans-get-signatures-no-scale-4'>k = 5</a></li>
<li><a href='#tab-ATC-kmeans-get-signatures-no-scale-5'>k = 6</a></li>
</ul>
<div id='tab-ATC-kmeans-get-signatures-no-scale-1'>
<pre><code class="r">get_signatures(res, k = 2, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-ATC-kmeans-get-signatures-no-scale-1-1.png" alt="plot of chunk tab-ATC-kmeans-get-signatures-no-scale-1"/></p>

</div>
<div id='tab-ATC-kmeans-get-signatures-no-scale-2'>
<pre><code class="r">get_signatures(res, k = 3, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-ATC-kmeans-get-signatures-no-scale-2-1.png" alt="plot of chunk tab-ATC-kmeans-get-signatures-no-scale-2"/></p>

</div>
<div id='tab-ATC-kmeans-get-signatures-no-scale-3'>
<pre><code class="r">get_signatures(res, k = 4, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-ATC-kmeans-get-signatures-no-scale-3-1.png" alt="plot of chunk tab-ATC-kmeans-get-signatures-no-scale-3"/></p>

</div>
<div id='tab-ATC-kmeans-get-signatures-no-scale-4'>
<pre><code class="r">get_signatures(res, k = 5, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-ATC-kmeans-get-signatures-no-scale-4-1.png" alt="plot of chunk tab-ATC-kmeans-get-signatures-no-scale-4"/></p>

</div>
<div id='tab-ATC-kmeans-get-signatures-no-scale-5'>
<pre><code class="r">get_signatures(res, k = 6, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-ATC-kmeans-get-signatures-no-scale-5-1.png" alt="plot of chunk tab-ATC-kmeans-get-signatures-no-scale-5"/></p>

</div>
</div>



Compare the overlap of signatures from different k:

```r
compare_signatures(res)
```

![plot of chunk ATC-kmeans-signature_compare](figure_cola/ATC-kmeans-signature_compare-1.png)

`get_signature()` returns a data frame invisibly. TO get the list of signatures, the function
call should be assigned to a variable explicitly. In following code, if `plot` argument is set
to `FALSE`, no heatmap is plotted while only the differential analysis is performed.

```r
# code only for demonstration
tb = get_signature(res, k = ..., plot = FALSE)
```

An example of the output of `tb` is:

```
#>   which_row         fdr    mean_1    mean_2 scaled_mean_1 scaled_mean_2 km
#> 1        38 0.042760348  8.373488  9.131774    -0.5533452     0.5164555  1
#> 2        40 0.018707592  7.106213  8.469186    -0.6173731     0.5762149  1
#> 3        55 0.019134737 10.221463 11.207825    -0.6159697     0.5749050  1
#> 4        59 0.006059896  5.921854  7.869574    -0.6899429     0.6439467  1
#> 5        60 0.018055526  8.928898 10.211722    -0.6204761     0.5791110  1
#> 6        98 0.009384629 15.714769 14.887706     0.6635654    -0.6193277  2
...
```

The columns in `tb` are:

1. `which_row`: row indices corresponding to the input matrix.
2. `fdr`: FDR for the differential test. 
3. `mean_x`: The mean value in group x.
4. `scaled_mean_x`: The mean value in group x after rows are scaled.
5. `km`: Row groups if k-means clustering is applied to rows.



UMAP plot which shows how samples are separated.


<script>
$( function() {
	$( '#tabs-ATC-kmeans-dimension-reduction' ).tabs();
} );
</script>
<div id='tabs-ATC-kmeans-dimension-reduction'>
<ul>
<li><a href='#tab-ATC-kmeans-dimension-reduction-1'>k = 2</a></li>
<li><a href='#tab-ATC-kmeans-dimension-reduction-2'>k = 3</a></li>
<li><a href='#tab-ATC-kmeans-dimension-reduction-3'>k = 4</a></li>
<li><a href='#tab-ATC-kmeans-dimension-reduction-4'>k = 5</a></li>
<li><a href='#tab-ATC-kmeans-dimension-reduction-5'>k = 6</a></li>
</ul>
<div id='tab-ATC-kmeans-dimension-reduction-1'>
<pre><code class="r">dimension_reduction(res, k = 2, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-ATC-kmeans-dimension-reduction-1-1.png" alt="plot of chunk tab-ATC-kmeans-dimension-reduction-1"/></p>

</div>
<div id='tab-ATC-kmeans-dimension-reduction-2'>
<pre><code class="r">dimension_reduction(res, k = 3, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-ATC-kmeans-dimension-reduction-2-1.png" alt="plot of chunk tab-ATC-kmeans-dimension-reduction-2"/></p>

</div>
<div id='tab-ATC-kmeans-dimension-reduction-3'>
<pre><code class="r">dimension_reduction(res, k = 4, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-ATC-kmeans-dimension-reduction-3-1.png" alt="plot of chunk tab-ATC-kmeans-dimension-reduction-3"/></p>

</div>
<div id='tab-ATC-kmeans-dimension-reduction-4'>
<pre><code class="r">dimension_reduction(res, k = 5, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-ATC-kmeans-dimension-reduction-4-1.png" alt="plot of chunk tab-ATC-kmeans-dimension-reduction-4"/></p>

</div>
<div id='tab-ATC-kmeans-dimension-reduction-5'>
<pre><code class="r">dimension_reduction(res, k = 6, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-ATC-kmeans-dimension-reduction-5-1.png" alt="plot of chunk tab-ATC-kmeans-dimension-reduction-5"/></p>

</div>
</div>


Following heatmap shows how subgroups are split when increasing `k`:

```r
collect_classes(res)
```

![plot of chunk ATC-kmeans-collect-classes](figure_cola/ATC-kmeans-collect-classes-1.png)


If matrix rows can be associated to genes, consider to use `functional_enrichment(res,
...)` to perform function enrichment for the signature genes. See [this vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/functional_enrichment.html) for more detailed explanations.


 

---------------------------------------------------




### ATC:skmeans**






The object with results only for a single top-value method and a single partition method 
can be extracted as:

```r
res = res_list["ATC", "skmeans"]
# you can also extract it by
# res = res_list["ATC:skmeans"]
```

A summary of `res` and all the functions that can be applied to it:

```r
res
```

```
#> A 'ConsensusPartition' object with k = 2, 3, 4, 5, 6.
#>   On a matrix with 15680 rows and 53 columns.
#>   Top rows (1000, 2000, 3000, 4000, 5000) are extracted by 'ATC' method.
#>   Subgroups are detected by 'skmeans' method.
#>   Performed in total 1250 partitions by row resampling.
#>   Best k for subgroups seems to be 6.
#> 
#> Following methods can be applied to this 'ConsensusPartition' object:
#>  [1] "cola_report"             "collect_classes"         "collect_plots"          
#>  [4] "collect_stats"           "colnames"                "compare_signatures"     
#>  [7] "consensus_heatmap"       "dimension_reduction"     "functional_enrichment"  
#> [10] "get_anno_col"            "get_anno"                "get_classes"            
#> [13] "get_consensus"           "get_matrix"              "get_membership"         
#> [16] "get_param"               "get_signatures"          "get_stats"              
#> [19] "is_best_k"               "is_stable_k"             "membership_heatmap"     
#> [22] "ncol"                    "nrow"                    "plot_ecdf"              
#> [25] "rownames"                "select_partition_number" "show"                   
#> [28] "suggest_best_k"          "test_to_known_factors"
```

`collect_plots()` function collects all the plots made from `res` for all `k` (number of partitions)
into one single page to provide an easy and fast comparison between different `k`.

```r
collect_plots(res)
```

![plot of chunk ATC-skmeans-collect-plots](figure_cola/ATC-skmeans-collect-plots-1.png)

The plots are:

- The first row: a plot of the ECDF (empirical cumulative distribution
  function) curves of the consensus matrix for each `k` and the heatmap of
  predicted classes for each `k`.
- The second row: heatmaps of the consensus matrix for each `k`.
- The third row: heatmaps of the membership matrix for each `k`.
- The fouth row: heatmaps of the signatures for each `k`.

All the plots in panels can be made by individual functions and they are
plotted later in this section.

`select_partition_number()` produces several plots showing different
statistics for choosing "optimized" `k`. There are following statistics:

- ECDF curves of the consensus matrix for each `k`;
- 1-PAC. [The PAC
  score](https://en.wikipedia.org/wiki/Consensus_clustering#Over-interpretation_potential_of_consensus_clustering)
  measures the proportion of the ambiguous subgrouping.
- Mean silhouette score.
- Concordance. The mean probability of fiting the consensus class ids in all
  partitions.
- Area increased. Denote $A_k$ as the area under the ECDF curve for current
  `k`, the area increased is defined as $A_k - A_{k-1}$.
- Rand index. The percent of pairs of samples that are both in a same cluster
  or both are not in a same cluster in the partition of k and k-1.
- Jaccard index. The ratio of pairs of samples are both in a same cluster in
  the partition of k and k-1 and the pairs of samples are both in a same
  cluster in the partition k or k-1.

The detailed explanations of these statistics can be found in [the _cola_
vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/cola.html#toc_13).

Generally speaking, lower PAC score, higher mean silhouette score or higher
concordance corresponds to better partition. Rand index and Jaccard index
measure how similar the current partition is compared to partition with `k-1`.
If they are too similar, we won't accept `k` is better than `k-1`.

```r
select_partition_number(res)
```

![plot of chunk ATC-skmeans-select-partition-number](figure_cola/ATC-skmeans-select-partition-number-1.png)

The numeric values for all these statistics can be obtained by `get_stats()`.

```r
get_stats(res)
```

```
#>   k 1-PAC mean_silhouette concordance area_increased  Rand Jaccard
#> 2 2 1.000           0.980       0.991         0.5096 0.491   0.491
#> 3 3 0.975           0.939       0.976         0.3176 0.768   0.558
#> 4 4 0.865           0.938       0.950         0.1006 0.896   0.701
#> 5 5 0.934           0.919       0.940         0.0765 0.930   0.741
#> 6 6 0.976           0.927       0.960         0.0318 0.974   0.873
```

`suggest_best_k()` suggests the best $k$ based on these statistics. The rules are as follows:

- All $k$ with Jaccard index larger than 0.95 are removed because increasing
  $k$ does not provide enough extra information. If all $k$ are removed, it is
  marked as no subgroup is detected.
- For all $k$ with 1-PAC score larger than 0.9, the maximal $k$ is taken as
  the best $k$, and other $k$ are marked as optional $k$.
- If it does not fit the second rule. The $k$ with the maximal vote of the
  highest 1-PAC score, highest mean silhouette, and highest concordance is
  taken as the best $k$.

```r
suggest_best_k(res)
```

```
#> [1] 6
#> attr(,"optional")
#> [1] 2 3 5
```

There is also optional best $k$ = 2 3 5 that is worth to check.

Following shows the table of the partitions (You need to click the **show/hide
code output** link to see it). The membership matrix (columns with name `p*`)
is inferred by
[`clue::cl_consensus()`](https://www.rdocumentation.org/link/cl_consensus?package=clue)
function with the `SE` method. Basically the value in the membership matrix
represents the probability to belong to a certain group. The finall class
label for an item is determined with the group with highest probability it
belongs to.

In `get_classes()` function, the entropy is calculated from the membership
matrix and the silhouette score is calculated from the consensus matrix.



<script>
$( function() {
	$( '#tabs-ATC-skmeans-get-classes' ).tabs();
} );
</script>
<div id='tabs-ATC-skmeans-get-classes'>
<ul>
<li><a href='#tab-ATC-skmeans-get-classes-1'>k = 2</a></li>
<li><a href='#tab-ATC-skmeans-get-classes-2'>k = 3</a></li>
<li><a href='#tab-ATC-skmeans-get-classes-3'>k = 4</a></li>
<li><a href='#tab-ATC-skmeans-get-classes-4'>k = 5</a></li>
<li><a href='#tab-ATC-skmeans-get-classes-5'>k = 6</a></li>
</ul>

<div id='tab-ATC-skmeans-get-classes-1'>
<p><a id='tab-ATC-skmeans-get-classes-1-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 2), get_membership(res, k = 2))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2
#&gt; SRR1383358     1   0.000      0.981 1.000 0.000
#&gt; SRR1383360     1   0.000      0.981 1.000 0.000
#&gt; SRR1383359     1   0.000      0.981 1.000 0.000
#&gt; SRR1383362     1   0.000      0.981 1.000 0.000
#&gt; SRR1383361     1   0.000      0.981 1.000 0.000
#&gt; SRR1383363     1   0.000      0.981 1.000 0.000
#&gt; SRR1383364     1   0.000      0.981 1.000 0.000
#&gt; SRR1383365     1   0.000      0.981 1.000 0.000
#&gt; SRR1383366     2   0.000      1.000 0.000 1.000
#&gt; SRR1383367     1   0.000      0.981 1.000 0.000
#&gt; SRR1383368     1   0.000      0.981 1.000 0.000
#&gt; SRR1383369     1   0.753      0.732 0.784 0.216
#&gt; SRR1383370     1   0.000      0.981 1.000 0.000
#&gt; SRR1383371     1   0.000      0.981 1.000 0.000
#&gt; SRR1383372     2   0.000      1.000 0.000 1.000
#&gt; SRR1383373     1   0.000      0.981 1.000 0.000
#&gt; SRR1383374     2   0.000      1.000 0.000 1.000
#&gt; SRR1383375     1   0.000      0.981 1.000 0.000
#&gt; SRR1383376     2   0.000      1.000 0.000 1.000
#&gt; SRR1383377     1   0.000      0.981 1.000 0.000
#&gt; SRR1383378     2   0.000      1.000 0.000 1.000
#&gt; SRR1383379     2   0.000      1.000 0.000 1.000
#&gt; SRR1383380     2   0.000      1.000 0.000 1.000
#&gt; SRR1383381     1   0.000      0.981 1.000 0.000
#&gt; SRR1383382     1   0.000      0.981 1.000 0.000
#&gt; SRR1383383     2   0.000      1.000 0.000 1.000
#&gt; SRR1383385     1   0.000      0.981 1.000 0.000
#&gt; SRR1383384     2   0.000      1.000 0.000 1.000
#&gt; SRR1383386     2   0.000      1.000 0.000 1.000
#&gt; SRR1383387     2   0.000      1.000 0.000 1.000
#&gt; SRR1383389     1   0.000      0.981 1.000 0.000
#&gt; SRR1383391     2   0.000      1.000 0.000 1.000
#&gt; SRR1383388     2   0.000      1.000 0.000 1.000
#&gt; SRR1383392     2   0.000      1.000 0.000 1.000
#&gt; SRR1383390     2   0.000      1.000 0.000 1.000
#&gt; SRR1383394     2   0.000      1.000 0.000 1.000
#&gt; SRR1383393     1   0.000      0.981 1.000 0.000
#&gt; SRR1383396     1   0.000      0.981 1.000 0.000
#&gt; SRR1383395     1   0.827      0.662 0.740 0.260
#&gt; SRR1383399     1   0.000      0.981 1.000 0.000
#&gt; SRR1383400     1   0.000      0.981 1.000 0.000
#&gt; SRR1383397     2   0.000      1.000 0.000 1.000
#&gt; SRR1383401     2   0.000      1.000 0.000 1.000
#&gt; SRR1383398     2   0.000      1.000 0.000 1.000
#&gt; SRR1383402     2   0.000      1.000 0.000 1.000
#&gt; SRR1383404     2   0.000      1.000 0.000 1.000
#&gt; SRR1383403     1   0.000      0.981 1.000 0.000
#&gt; SRR1383405     2   0.000      1.000 0.000 1.000
#&gt; SRR1383406     2   0.000      1.000 0.000 1.000
#&gt; SRR1383407     1   0.000      0.981 1.000 0.000
#&gt; SRR1383408     2   0.000      1.000 0.000 1.000
#&gt; SRR1383409     2   0.000      1.000 0.000 1.000
#&gt; SRR1383410     2   0.000      1.000 0.000 1.000
</code></pre>

<script>
$('#tab-ATC-skmeans-get-classes-1-a').parent().next().next().hide();
$('#tab-ATC-skmeans-get-classes-1-a').click(function(){
  $('#tab-ATC-skmeans-get-classes-1-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-ATC-skmeans-get-classes-2'>
<p><a id='tab-ATC-skmeans-get-classes-2-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 3), get_membership(res, k = 3))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3
#&gt; SRR1383358     3   0.000      0.988 0.000 0.000 1.000
#&gt; SRR1383360     3   0.000      0.988 0.000 0.000 1.000
#&gt; SRR1383359     3   0.000      0.988 0.000 0.000 1.000
#&gt; SRR1383362     1   0.000      0.982 1.000 0.000 0.000
#&gt; SRR1383361     3   0.000      0.988 0.000 0.000 1.000
#&gt; SRR1383363     3   0.000      0.988 0.000 0.000 1.000
#&gt; SRR1383364     3   0.000      0.988 0.000 0.000 1.000
#&gt; SRR1383365     3   0.000      0.988 0.000 0.000 1.000
#&gt; SRR1383366     2   0.614      0.350 0.000 0.596 0.404
#&gt; SRR1383367     3   0.000      0.988 0.000 0.000 1.000
#&gt; SRR1383368     3   0.484      0.717 0.224 0.000 0.776
#&gt; SRR1383369     3   0.000      0.988 0.000 0.000 1.000
#&gt; SRR1383370     3   0.000      0.988 0.000 0.000 1.000
#&gt; SRR1383371     3   0.000      0.988 0.000 0.000 1.000
#&gt; SRR1383372     2   0.615      0.339 0.000 0.592 0.408
#&gt; SRR1383373     3   0.000      0.988 0.000 0.000 1.000
#&gt; SRR1383374     2   0.000      0.952 0.000 1.000 0.000
#&gt; SRR1383375     1   0.000      0.982 1.000 0.000 0.000
#&gt; SRR1383376     2   0.000      0.952 0.000 1.000 0.000
#&gt; SRR1383377     3   0.000      0.988 0.000 0.000 1.000
#&gt; SRR1383378     1   0.000      0.982 1.000 0.000 0.000
#&gt; SRR1383379     2   0.000      0.952 0.000 1.000 0.000
#&gt; SRR1383380     1   0.000      0.982 1.000 0.000 0.000
#&gt; SRR1383381     3   0.000      0.988 0.000 0.000 1.000
#&gt; SRR1383382     1   0.000      0.982 1.000 0.000 0.000
#&gt; SRR1383383     2   0.000      0.952 0.000 1.000 0.000
#&gt; SRR1383385     1   0.000      0.982 1.000 0.000 0.000
#&gt; SRR1383384     2   0.000      0.952 0.000 1.000 0.000
#&gt; SRR1383386     1   0.000      0.982 1.000 0.000 0.000
#&gt; SRR1383387     2   0.000      0.952 0.000 1.000 0.000
#&gt; SRR1383389     3   0.000      0.988 0.000 0.000 1.000
#&gt; SRR1383391     2   0.000      0.952 0.000 1.000 0.000
#&gt; SRR1383388     1   0.480      0.704 0.780 0.220 0.000
#&gt; SRR1383392     2   0.000      0.952 0.000 1.000 0.000
#&gt; SRR1383390     2   0.000      0.952 0.000 1.000 0.000
#&gt; SRR1383394     2   0.000      0.952 0.000 1.000 0.000
#&gt; SRR1383393     1   0.000      0.982 1.000 0.000 0.000
#&gt; SRR1383396     1   0.000      0.982 1.000 0.000 0.000
#&gt; SRR1383395     3   0.000      0.988 0.000 0.000 1.000
#&gt; SRR1383399     3   0.000      0.988 0.000 0.000 1.000
#&gt; SRR1383400     1   0.000      0.982 1.000 0.000 0.000
#&gt; SRR1383397     2   0.000      0.952 0.000 1.000 0.000
#&gt; SRR1383401     2   0.000      0.952 0.000 1.000 0.000
#&gt; SRR1383398     1   0.000      0.982 1.000 0.000 0.000
#&gt; SRR1383402     2   0.000      0.952 0.000 1.000 0.000
#&gt; SRR1383404     1   0.000      0.982 1.000 0.000 0.000
#&gt; SRR1383403     1   0.000      0.982 1.000 0.000 0.000
#&gt; SRR1383405     2   0.000      0.952 0.000 1.000 0.000
#&gt; SRR1383406     2   0.000      0.952 0.000 1.000 0.000
#&gt; SRR1383407     3   0.000      0.988 0.000 0.000 1.000
#&gt; SRR1383408     2   0.000      0.952 0.000 1.000 0.000
#&gt; SRR1383409     2   0.000      0.952 0.000 1.000 0.000
#&gt; SRR1383410     2   0.000      0.952 0.000 1.000 0.000
</code></pre>

<script>
$('#tab-ATC-skmeans-get-classes-2-a').parent().next().next().hide();
$('#tab-ATC-skmeans-get-classes-2-a').click(function(){
  $('#tab-ATC-skmeans-get-classes-2-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-ATC-skmeans-get-classes-3'>
<p><a id='tab-ATC-skmeans-get-classes-3-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 4), get_membership(res, k = 4))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4
#&gt; SRR1383358     3  0.2760      0.901 0.000 0.000 0.872 0.128
#&gt; SRR1383360     3  0.0188      0.967 0.000 0.000 0.996 0.004
#&gt; SRR1383359     3  0.0469      0.966 0.000 0.000 0.988 0.012
#&gt; SRR1383362     1  0.0000      0.979 1.000 0.000 0.000 0.000
#&gt; SRR1383361     3  0.0469      0.966 0.000 0.000 0.988 0.012
#&gt; SRR1383363     3  0.0592      0.966 0.000 0.000 0.984 0.016
#&gt; SRR1383364     3  0.0469      0.966 0.000 0.000 0.988 0.012
#&gt; SRR1383365     3  0.0469      0.966 0.000 0.000 0.988 0.012
#&gt; SRR1383366     2  0.5280      0.743 0.000 0.752 0.120 0.128
#&gt; SRR1383367     3  0.2760      0.901 0.000 0.000 0.872 0.128
#&gt; SRR1383368     1  0.3048      0.831 0.876 0.000 0.108 0.016
#&gt; SRR1383369     3  0.2760      0.901 0.000 0.000 0.872 0.128
#&gt; SRR1383370     3  0.0469      0.966 0.000 0.000 0.988 0.012
#&gt; SRR1383371     3  0.0469      0.966 0.000 0.000 0.988 0.012
#&gt; SRR1383372     2  0.4100      0.827 0.000 0.824 0.048 0.128
#&gt; SRR1383373     3  0.0469      0.966 0.000 0.000 0.988 0.012
#&gt; SRR1383374     2  0.3217      0.858 0.000 0.860 0.012 0.128
#&gt; SRR1383375     1  0.0000      0.979 1.000 0.000 0.000 0.000
#&gt; SRR1383376     2  0.0000      0.962 0.000 1.000 0.000 0.000
#&gt; SRR1383377     3  0.0592      0.964 0.000 0.000 0.984 0.016
#&gt; SRR1383378     4  0.2921      0.908 0.140 0.000 0.000 0.860
#&gt; SRR1383379     4  0.2921      0.866 0.000 0.140 0.000 0.860
#&gt; SRR1383380     4  0.2921      0.908 0.140 0.000 0.000 0.860
#&gt; SRR1383381     3  0.0804      0.962 0.008 0.000 0.980 0.012
#&gt; SRR1383382     1  0.0000      0.979 1.000 0.000 0.000 0.000
#&gt; SRR1383383     2  0.0000      0.962 0.000 1.000 0.000 0.000
#&gt; SRR1383385     1  0.0000      0.979 1.000 0.000 0.000 0.000
#&gt; SRR1383384     2  0.0000      0.962 0.000 1.000 0.000 0.000
#&gt; SRR1383386     4  0.2921      0.908 0.140 0.000 0.000 0.860
#&gt; SRR1383387     2  0.0000      0.962 0.000 1.000 0.000 0.000
#&gt; SRR1383389     3  0.0469      0.966 0.000 0.000 0.988 0.012
#&gt; SRR1383391     2  0.0000      0.962 0.000 1.000 0.000 0.000
#&gt; SRR1383388     4  0.3621      0.897 0.068 0.072 0.000 0.860
#&gt; SRR1383392     2  0.1022      0.941 0.000 0.968 0.000 0.032
#&gt; SRR1383390     2  0.0000      0.962 0.000 1.000 0.000 0.000
#&gt; SRR1383394     2  0.0000      0.962 0.000 1.000 0.000 0.000
#&gt; SRR1383393     1  0.0000      0.979 1.000 0.000 0.000 0.000
#&gt; SRR1383396     1  0.0000      0.979 1.000 0.000 0.000 0.000
#&gt; SRR1383395     3  0.2149      0.926 0.000 0.000 0.912 0.088
#&gt; SRR1383399     3  0.0804      0.962 0.008 0.000 0.980 0.012
#&gt; SRR1383400     1  0.0000      0.979 1.000 0.000 0.000 0.000
#&gt; SRR1383397     4  0.2921      0.866 0.000 0.140 0.000 0.860
#&gt; SRR1383401     2  0.0000      0.962 0.000 1.000 0.000 0.000
#&gt; SRR1383398     4  0.2921      0.908 0.140 0.000 0.000 0.860
#&gt; SRR1383402     2  0.0000      0.962 0.000 1.000 0.000 0.000
#&gt; SRR1383404     4  0.2921      0.908 0.140 0.000 0.000 0.860
#&gt; SRR1383403     1  0.0000      0.979 1.000 0.000 0.000 0.000
#&gt; SRR1383405     2  0.0000      0.962 0.000 1.000 0.000 0.000
#&gt; SRR1383406     4  0.2921      0.866 0.000 0.140 0.000 0.860
#&gt; SRR1383407     3  0.0469      0.966 0.000 0.000 0.988 0.012
#&gt; SRR1383408     2  0.0000      0.962 0.000 1.000 0.000 0.000
#&gt; SRR1383409     2  0.0000      0.962 0.000 1.000 0.000 0.000
#&gt; SRR1383410     2  0.0000      0.962 0.000 1.000 0.000 0.000
</code></pre>

<script>
$('#tab-ATC-skmeans-get-classes-3-a').parent().next().next().hide();
$('#tab-ATC-skmeans-get-classes-3-a').click(function(){
  $('#tab-ATC-skmeans-get-classes-3-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-ATC-skmeans-get-classes-4'>
<p><a id='tab-ATC-skmeans-get-classes-4-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 5), get_membership(res, k = 5))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4    p5
#&gt; SRR1383358     3  0.1544      0.917 0.000 0.000 0.932 0.000 0.068
#&gt; SRR1383360     5  0.1608      0.878 0.000 0.000 0.072 0.000 0.928
#&gt; SRR1383359     5  0.0794      0.880 0.000 0.000 0.028 0.000 0.972
#&gt; SRR1383362     1  0.0000      0.986 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1383361     5  0.2127      0.870 0.000 0.000 0.108 0.000 0.892
#&gt; SRR1383363     5  0.2648      0.848 0.000 0.000 0.152 0.000 0.848
#&gt; SRR1383364     5  0.1357      0.871 0.000 0.000 0.048 0.004 0.948
#&gt; SRR1383365     5  0.2179      0.868 0.000 0.000 0.112 0.000 0.888
#&gt; SRR1383366     3  0.2376      0.917 0.000 0.044 0.904 0.000 0.052
#&gt; SRR1383367     3  0.1608      0.916 0.000 0.000 0.928 0.000 0.072
#&gt; SRR1383368     1  0.2236      0.884 0.908 0.000 0.024 0.000 0.068
#&gt; SRR1383369     3  0.1732      0.912 0.000 0.000 0.920 0.000 0.080
#&gt; SRR1383370     5  0.2230      0.866 0.000 0.000 0.116 0.000 0.884
#&gt; SRR1383371     5  0.0609      0.879 0.000 0.000 0.020 0.000 0.980
#&gt; SRR1383372     3  0.1877      0.904 0.000 0.064 0.924 0.000 0.012
#&gt; SRR1383373     5  0.2127      0.870 0.000 0.000 0.108 0.000 0.892
#&gt; SRR1383374     3  0.2852      0.804 0.000 0.172 0.828 0.000 0.000
#&gt; SRR1383375     1  0.0000      0.986 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1383376     2  0.0000      0.994 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1383377     5  0.1430      0.878 0.000 0.000 0.052 0.004 0.944
#&gt; SRR1383378     4  0.1410      0.958 0.060 0.000 0.000 0.940 0.000
#&gt; SRR1383379     4  0.1608      0.929 0.000 0.072 0.000 0.928 0.000
#&gt; SRR1383380     4  0.1410      0.958 0.060 0.000 0.000 0.940 0.000
#&gt; SRR1383381     5  0.3937      0.781 0.004 0.000 0.132 0.060 0.804
#&gt; SRR1383382     1  0.0000      0.986 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1383383     2  0.0162      0.991 0.000 0.996 0.000 0.004 0.000
#&gt; SRR1383385     1  0.0000      0.986 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1383384     2  0.0000      0.994 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1383386     4  0.1410      0.958 0.060 0.000 0.000 0.940 0.000
#&gt; SRR1383387     2  0.0000      0.994 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1383389     5  0.3051      0.811 0.000 0.000 0.076 0.060 0.864
#&gt; SRR1383391     2  0.0000      0.994 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1383388     4  0.1661      0.950 0.024 0.036 0.000 0.940 0.000
#&gt; SRR1383392     2  0.0963      0.959 0.000 0.964 0.036 0.000 0.000
#&gt; SRR1383390     2  0.0000      0.994 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1383394     2  0.0000      0.994 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1383393     1  0.0000      0.986 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1383396     1  0.0000      0.986 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1383395     5  0.4350      0.250 0.000 0.000 0.408 0.004 0.588
#&gt; SRR1383399     5  0.3937      0.781 0.004 0.000 0.132 0.060 0.804
#&gt; SRR1383400     1  0.0000      0.986 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1383397     4  0.1792      0.918 0.000 0.084 0.000 0.916 0.000
#&gt; SRR1383401     2  0.0880      0.967 0.000 0.968 0.000 0.032 0.000
#&gt; SRR1383398     4  0.1410      0.958 0.060 0.000 0.000 0.940 0.000
#&gt; SRR1383402     2  0.0000      0.994 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1383404     4  0.1410      0.958 0.060 0.000 0.000 0.940 0.000
#&gt; SRR1383403     1  0.0000      0.986 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1383405     2  0.0000      0.994 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1383406     4  0.1410      0.937 0.000 0.060 0.000 0.940 0.000
#&gt; SRR1383407     5  0.0000      0.874 0.000 0.000 0.000 0.000 1.000
#&gt; SRR1383408     2  0.0000      0.994 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1383409     2  0.0000      0.994 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1383410     2  0.0000      0.994 0.000 1.000 0.000 0.000 0.000
</code></pre>

<script>
$('#tab-ATC-skmeans-get-classes-4-a').parent().next().next().hide();
$('#tab-ATC-skmeans-get-classes-4-a').click(function(){
  $('#tab-ATC-skmeans-get-classes-4-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-ATC-skmeans-get-classes-5'>
<p><a id='tab-ATC-skmeans-get-classes-5-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 6), get_membership(res, k = 6))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4    p5    p6
#&gt; SRR1383358     6  0.0551      0.970 0.000 0.000 0.004 0.004 0.008 0.984
#&gt; SRR1383360     3  0.0000      0.905 0.000 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1383359     3  0.0622      0.907 0.000 0.000 0.980 0.000 0.012 0.008
#&gt; SRR1383362     1  0.0000      0.970 1.000 0.000 0.000 0.000 0.000 0.000
#&gt; SRR1383361     3  0.0547      0.908 0.000 0.000 0.980 0.000 0.000 0.020
#&gt; SRR1383363     3  0.2069      0.860 0.000 0.000 0.908 0.004 0.020 0.068
#&gt; SRR1383364     3  0.1863      0.838 0.000 0.000 0.896 0.000 0.104 0.000
#&gt; SRR1383365     3  0.0632      0.907 0.000 0.000 0.976 0.000 0.000 0.024
#&gt; SRR1383366     6  0.0603      0.970 0.000 0.004 0.016 0.000 0.000 0.980
#&gt; SRR1383367     6  0.0951      0.964 0.000 0.000 0.020 0.004 0.008 0.968
#&gt; SRR1383368     1  0.2926      0.789 0.844 0.000 0.132 0.004 0.008 0.012
#&gt; SRR1383369     6  0.0603      0.968 0.000 0.000 0.016 0.000 0.004 0.980
#&gt; SRR1383370     3  0.0547      0.908 0.000 0.000 0.980 0.000 0.000 0.020
#&gt; SRR1383371     3  0.0260      0.906 0.000 0.000 0.992 0.000 0.008 0.000
#&gt; SRR1383372     6  0.0810      0.971 0.000 0.008 0.004 0.004 0.008 0.976
#&gt; SRR1383373     3  0.0547      0.908 0.000 0.000 0.980 0.000 0.000 0.020
#&gt; SRR1383374     6  0.0865      0.943 0.000 0.036 0.000 0.000 0.000 0.964
#&gt; SRR1383375     1  0.0458      0.968 0.984 0.000 0.000 0.000 0.016 0.000
#&gt; SRR1383376     2  0.0000      0.994 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1383377     3  0.3178      0.753 0.000 0.000 0.832 0.012 0.128 0.028
#&gt; SRR1383378     4  0.0914      0.959 0.016 0.000 0.000 0.968 0.016 0.000
#&gt; SRR1383379     4  0.1349      0.928 0.000 0.056 0.000 0.940 0.004 0.000
#&gt; SRR1383380     4  0.1168      0.953 0.016 0.000 0.000 0.956 0.028 0.000
#&gt; SRR1383381     5  0.1471      0.861 0.000 0.000 0.064 0.000 0.932 0.004
#&gt; SRR1383382     1  0.0000      0.970 1.000 0.000 0.000 0.000 0.000 0.000
#&gt; SRR1383383     2  0.0000      0.994 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1383385     1  0.0458      0.968 0.984 0.000 0.000 0.000 0.016 0.000
#&gt; SRR1383384     2  0.0000      0.994 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1383386     4  0.0914      0.959 0.016 0.000 0.000 0.968 0.016 0.000
#&gt; SRR1383387     2  0.0000      0.994 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1383389     5  0.3848      0.674 0.000 0.000 0.292 0.004 0.692 0.012
#&gt; SRR1383391     2  0.0000      0.994 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1383388     4  0.0458      0.958 0.000 0.016 0.000 0.984 0.000 0.000
#&gt; SRR1383392     2  0.0632      0.974 0.000 0.976 0.000 0.000 0.000 0.024
#&gt; SRR1383390     2  0.0000      0.994 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1383394     2  0.0000      0.994 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1383393     1  0.0260      0.969 0.992 0.000 0.000 0.000 0.008 0.000
#&gt; SRR1383396     1  0.0000      0.970 1.000 0.000 0.000 0.000 0.000 0.000
#&gt; SRR1383395     3  0.5501      0.333 0.000 0.000 0.584 0.012 0.128 0.276
#&gt; SRR1383399     5  0.1471      0.861 0.000 0.000 0.064 0.000 0.932 0.004
#&gt; SRR1383400     1  0.0000      0.970 1.000 0.000 0.000 0.000 0.000 0.000
#&gt; SRR1383397     4  0.1753      0.895 0.000 0.084 0.000 0.912 0.004 0.000
#&gt; SRR1383401     2  0.1082      0.957 0.000 0.956 0.000 0.000 0.040 0.004
#&gt; SRR1383398     4  0.1168      0.953 0.016 0.000 0.000 0.956 0.028 0.000
#&gt; SRR1383402     2  0.0000      0.994 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1383404     4  0.0914      0.959 0.016 0.000 0.000 0.968 0.016 0.000
#&gt; SRR1383403     1  0.0458      0.968 0.984 0.000 0.000 0.000 0.016 0.000
#&gt; SRR1383405     2  0.0000      0.994 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1383406     4  0.0458      0.958 0.000 0.016 0.000 0.984 0.000 0.000
#&gt; SRR1383407     3  0.0146      0.903 0.000 0.000 0.996 0.000 0.000 0.004
#&gt; SRR1383408     2  0.0000      0.994 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1383409     2  0.0000      0.994 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1383410     2  0.0146      0.991 0.000 0.996 0.000 0.000 0.000 0.004
</code></pre>

<script>
$('#tab-ATC-skmeans-get-classes-5-a').parent().next().next().hide();
$('#tab-ATC-skmeans-get-classes-5-a').click(function(){
  $('#tab-ATC-skmeans-get-classes-5-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>
</div>

Heatmaps for the consensus matrix. It visualizes the probability of two
samples to be in a same group.



<script>
$( function() {
	$( '#tabs-ATC-skmeans-consensus-heatmap' ).tabs();
} );
</script>
<div id='tabs-ATC-skmeans-consensus-heatmap'>
<ul>
<li><a href='#tab-ATC-skmeans-consensus-heatmap-1'>k = 2</a></li>
<li><a href='#tab-ATC-skmeans-consensus-heatmap-2'>k = 3</a></li>
<li><a href='#tab-ATC-skmeans-consensus-heatmap-3'>k = 4</a></li>
<li><a href='#tab-ATC-skmeans-consensus-heatmap-4'>k = 5</a></li>
<li><a href='#tab-ATC-skmeans-consensus-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-ATC-skmeans-consensus-heatmap-1'>
<pre><code class="r">consensus_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-ATC-skmeans-consensus-heatmap-1-1.png" alt="plot of chunk tab-ATC-skmeans-consensus-heatmap-1"/></p>

</div>
<div id='tab-ATC-skmeans-consensus-heatmap-2'>
<pre><code class="r">consensus_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-ATC-skmeans-consensus-heatmap-2-1.png" alt="plot of chunk tab-ATC-skmeans-consensus-heatmap-2"/></p>

</div>
<div id='tab-ATC-skmeans-consensus-heatmap-3'>
<pre><code class="r">consensus_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-ATC-skmeans-consensus-heatmap-3-1.png" alt="plot of chunk tab-ATC-skmeans-consensus-heatmap-3"/></p>

</div>
<div id='tab-ATC-skmeans-consensus-heatmap-4'>
<pre><code class="r">consensus_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-ATC-skmeans-consensus-heatmap-4-1.png" alt="plot of chunk tab-ATC-skmeans-consensus-heatmap-4"/></p>

</div>
<div id='tab-ATC-skmeans-consensus-heatmap-5'>
<pre><code class="r">consensus_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-ATC-skmeans-consensus-heatmap-5-1.png" alt="plot of chunk tab-ATC-skmeans-consensus-heatmap-5"/></p>

</div>
</div>

Heatmaps for the membership of samples in all partitions to see how consistent they are:




<script>
$( function() {
	$( '#tabs-ATC-skmeans-membership-heatmap' ).tabs();
} );
</script>
<div id='tabs-ATC-skmeans-membership-heatmap'>
<ul>
<li><a href='#tab-ATC-skmeans-membership-heatmap-1'>k = 2</a></li>
<li><a href='#tab-ATC-skmeans-membership-heatmap-2'>k = 3</a></li>
<li><a href='#tab-ATC-skmeans-membership-heatmap-3'>k = 4</a></li>
<li><a href='#tab-ATC-skmeans-membership-heatmap-4'>k = 5</a></li>
<li><a href='#tab-ATC-skmeans-membership-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-ATC-skmeans-membership-heatmap-1'>
<pre><code class="r">membership_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-ATC-skmeans-membership-heatmap-1-1.png" alt="plot of chunk tab-ATC-skmeans-membership-heatmap-1"/></p>

</div>
<div id='tab-ATC-skmeans-membership-heatmap-2'>
<pre><code class="r">membership_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-ATC-skmeans-membership-heatmap-2-1.png" alt="plot of chunk tab-ATC-skmeans-membership-heatmap-2"/></p>

</div>
<div id='tab-ATC-skmeans-membership-heatmap-3'>
<pre><code class="r">membership_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-ATC-skmeans-membership-heatmap-3-1.png" alt="plot of chunk tab-ATC-skmeans-membership-heatmap-3"/></p>

</div>
<div id='tab-ATC-skmeans-membership-heatmap-4'>
<pre><code class="r">membership_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-ATC-skmeans-membership-heatmap-4-1.png" alt="plot of chunk tab-ATC-skmeans-membership-heatmap-4"/></p>

</div>
<div id='tab-ATC-skmeans-membership-heatmap-5'>
<pre><code class="r">membership_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-ATC-skmeans-membership-heatmap-5-1.png" alt="plot of chunk tab-ATC-skmeans-membership-heatmap-5"/></p>

</div>
</div>

As soon as we have had the classes for columns, we can look for signatures
which are significantly different between classes which can be candidate marks
for certain classes. Following are the heatmaps for signatures.



Signature heatmaps where rows are scaled:



<script>
$( function() {
	$( '#tabs-ATC-skmeans-get-signatures' ).tabs();
} );
</script>
<div id='tabs-ATC-skmeans-get-signatures'>
<ul>
<li><a href='#tab-ATC-skmeans-get-signatures-1'>k = 2</a></li>
<li><a href='#tab-ATC-skmeans-get-signatures-2'>k = 3</a></li>
<li><a href='#tab-ATC-skmeans-get-signatures-3'>k = 4</a></li>
<li><a href='#tab-ATC-skmeans-get-signatures-4'>k = 5</a></li>
<li><a href='#tab-ATC-skmeans-get-signatures-5'>k = 6</a></li>
</ul>
<div id='tab-ATC-skmeans-get-signatures-1'>
<pre><code class="r">get_signatures(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-ATC-skmeans-get-signatures-1-1.png" alt="plot of chunk tab-ATC-skmeans-get-signatures-1"/></p>

</div>
<div id='tab-ATC-skmeans-get-signatures-2'>
<pre><code class="r">get_signatures(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-ATC-skmeans-get-signatures-2-1.png" alt="plot of chunk tab-ATC-skmeans-get-signatures-2"/></p>

</div>
<div id='tab-ATC-skmeans-get-signatures-3'>
<pre><code class="r">get_signatures(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-ATC-skmeans-get-signatures-3-1.png" alt="plot of chunk tab-ATC-skmeans-get-signatures-3"/></p>

</div>
<div id='tab-ATC-skmeans-get-signatures-4'>
<pre><code class="r">get_signatures(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-ATC-skmeans-get-signatures-4-1.png" alt="plot of chunk tab-ATC-skmeans-get-signatures-4"/></p>

</div>
<div id='tab-ATC-skmeans-get-signatures-5'>
<pre><code class="r">get_signatures(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-ATC-skmeans-get-signatures-5-1.png" alt="plot of chunk tab-ATC-skmeans-get-signatures-5"/></p>

</div>
</div>



Signature heatmaps where rows are not scaled:


<script>
$( function() {
	$( '#tabs-ATC-skmeans-get-signatures-no-scale' ).tabs();
} );
</script>
<div id='tabs-ATC-skmeans-get-signatures-no-scale'>
<ul>
<li><a href='#tab-ATC-skmeans-get-signatures-no-scale-1'>k = 2</a></li>
<li><a href='#tab-ATC-skmeans-get-signatures-no-scale-2'>k = 3</a></li>
<li><a href='#tab-ATC-skmeans-get-signatures-no-scale-3'>k = 4</a></li>
<li><a href='#tab-ATC-skmeans-get-signatures-no-scale-4'>k = 5</a></li>
<li><a href='#tab-ATC-skmeans-get-signatures-no-scale-5'>k = 6</a></li>
</ul>
<div id='tab-ATC-skmeans-get-signatures-no-scale-1'>
<pre><code class="r">get_signatures(res, k = 2, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-ATC-skmeans-get-signatures-no-scale-1-1.png" alt="plot of chunk tab-ATC-skmeans-get-signatures-no-scale-1"/></p>

</div>
<div id='tab-ATC-skmeans-get-signatures-no-scale-2'>
<pre><code class="r">get_signatures(res, k = 3, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-ATC-skmeans-get-signatures-no-scale-2-1.png" alt="plot of chunk tab-ATC-skmeans-get-signatures-no-scale-2"/></p>

</div>
<div id='tab-ATC-skmeans-get-signatures-no-scale-3'>
<pre><code class="r">get_signatures(res, k = 4, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-ATC-skmeans-get-signatures-no-scale-3-1.png" alt="plot of chunk tab-ATC-skmeans-get-signatures-no-scale-3"/></p>

</div>
<div id='tab-ATC-skmeans-get-signatures-no-scale-4'>
<pre><code class="r">get_signatures(res, k = 5, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-ATC-skmeans-get-signatures-no-scale-4-1.png" alt="plot of chunk tab-ATC-skmeans-get-signatures-no-scale-4"/></p>

</div>
<div id='tab-ATC-skmeans-get-signatures-no-scale-5'>
<pre><code class="r">get_signatures(res, k = 6, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-ATC-skmeans-get-signatures-no-scale-5-1.png" alt="plot of chunk tab-ATC-skmeans-get-signatures-no-scale-5"/></p>

</div>
</div>



Compare the overlap of signatures from different k:

```r
compare_signatures(res)
```

![plot of chunk ATC-skmeans-signature_compare](figure_cola/ATC-skmeans-signature_compare-1.png)

`get_signature()` returns a data frame invisibly. TO get the list of signatures, the function
call should be assigned to a variable explicitly. In following code, if `plot` argument is set
to `FALSE`, no heatmap is plotted while only the differential analysis is performed.

```r
# code only for demonstration
tb = get_signature(res, k = ..., plot = FALSE)
```

An example of the output of `tb` is:

```
#>   which_row         fdr    mean_1    mean_2 scaled_mean_1 scaled_mean_2 km
#> 1        38 0.042760348  8.373488  9.131774    -0.5533452     0.5164555  1
#> 2        40 0.018707592  7.106213  8.469186    -0.6173731     0.5762149  1
#> 3        55 0.019134737 10.221463 11.207825    -0.6159697     0.5749050  1
#> 4        59 0.006059896  5.921854  7.869574    -0.6899429     0.6439467  1
#> 5        60 0.018055526  8.928898 10.211722    -0.6204761     0.5791110  1
#> 6        98 0.009384629 15.714769 14.887706     0.6635654    -0.6193277  2
...
```

The columns in `tb` are:

1. `which_row`: row indices corresponding to the input matrix.
2. `fdr`: FDR for the differential test. 
3. `mean_x`: The mean value in group x.
4. `scaled_mean_x`: The mean value in group x after rows are scaled.
5. `km`: Row groups if k-means clustering is applied to rows.



UMAP plot which shows how samples are separated.


<script>
$( function() {
	$( '#tabs-ATC-skmeans-dimension-reduction' ).tabs();
} );
</script>
<div id='tabs-ATC-skmeans-dimension-reduction'>
<ul>
<li><a href='#tab-ATC-skmeans-dimension-reduction-1'>k = 2</a></li>
<li><a href='#tab-ATC-skmeans-dimension-reduction-2'>k = 3</a></li>
<li><a href='#tab-ATC-skmeans-dimension-reduction-3'>k = 4</a></li>
<li><a href='#tab-ATC-skmeans-dimension-reduction-4'>k = 5</a></li>
<li><a href='#tab-ATC-skmeans-dimension-reduction-5'>k = 6</a></li>
</ul>
<div id='tab-ATC-skmeans-dimension-reduction-1'>
<pre><code class="r">dimension_reduction(res, k = 2, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-ATC-skmeans-dimension-reduction-1-1.png" alt="plot of chunk tab-ATC-skmeans-dimension-reduction-1"/></p>

</div>
<div id='tab-ATC-skmeans-dimension-reduction-2'>
<pre><code class="r">dimension_reduction(res, k = 3, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-ATC-skmeans-dimension-reduction-2-1.png" alt="plot of chunk tab-ATC-skmeans-dimension-reduction-2"/></p>

</div>
<div id='tab-ATC-skmeans-dimension-reduction-3'>
<pre><code class="r">dimension_reduction(res, k = 4, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-ATC-skmeans-dimension-reduction-3-1.png" alt="plot of chunk tab-ATC-skmeans-dimension-reduction-3"/></p>

</div>
<div id='tab-ATC-skmeans-dimension-reduction-4'>
<pre><code class="r">dimension_reduction(res, k = 5, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-ATC-skmeans-dimension-reduction-4-1.png" alt="plot of chunk tab-ATC-skmeans-dimension-reduction-4"/></p>

</div>
<div id='tab-ATC-skmeans-dimension-reduction-5'>
<pre><code class="r">dimension_reduction(res, k = 6, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-ATC-skmeans-dimension-reduction-5-1.png" alt="plot of chunk tab-ATC-skmeans-dimension-reduction-5"/></p>

</div>
</div>


Following heatmap shows how subgroups are split when increasing `k`:

```r
collect_classes(res)
```

![plot of chunk ATC-skmeans-collect-classes](figure_cola/ATC-skmeans-collect-classes-1.png)


If matrix rows can be associated to genes, consider to use `functional_enrichment(res,
...)` to perform function enrichment for the signature genes. See [this vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/functional_enrichment.html) for more detailed explanations.


 

---------------------------------------------------




### ATC:pam**






The object with results only for a single top-value method and a single partition method 
can be extracted as:

```r
res = res_list["ATC", "pam"]
# you can also extract it by
# res = res_list["ATC:pam"]
```

A summary of `res` and all the functions that can be applied to it:

```r
res
```

```
#> A 'ConsensusPartition' object with k = 2, 3, 4, 5, 6.
#>   On a matrix with 15680 rows and 53 columns.
#>   Top rows (1000, 2000, 3000, 4000, 5000) are extracted by 'ATC' method.
#>   Subgroups are detected by 'pam' method.
#>   Performed in total 1250 partitions by row resampling.
#>   Best k for subgroups seems to be 3.
#> 
#> Following methods can be applied to this 'ConsensusPartition' object:
#>  [1] "cola_report"             "collect_classes"         "collect_plots"          
#>  [4] "collect_stats"           "colnames"                "compare_signatures"     
#>  [7] "consensus_heatmap"       "dimension_reduction"     "functional_enrichment"  
#> [10] "get_anno_col"            "get_anno"                "get_classes"            
#> [13] "get_consensus"           "get_matrix"              "get_membership"         
#> [16] "get_param"               "get_signatures"          "get_stats"              
#> [19] "is_best_k"               "is_stable_k"             "membership_heatmap"     
#> [22] "ncol"                    "nrow"                    "plot_ecdf"              
#> [25] "rownames"                "select_partition_number" "show"                   
#> [28] "suggest_best_k"          "test_to_known_factors"
```

`collect_plots()` function collects all the plots made from `res` for all `k` (number of partitions)
into one single page to provide an easy and fast comparison between different `k`.

```r
collect_plots(res)
```

![plot of chunk ATC-pam-collect-plots](figure_cola/ATC-pam-collect-plots-1.png)

The plots are:

- The first row: a plot of the ECDF (empirical cumulative distribution
  function) curves of the consensus matrix for each `k` and the heatmap of
  predicted classes for each `k`.
- The second row: heatmaps of the consensus matrix for each `k`.
- The third row: heatmaps of the membership matrix for each `k`.
- The fouth row: heatmaps of the signatures for each `k`.

All the plots in panels can be made by individual functions and they are
plotted later in this section.

`select_partition_number()` produces several plots showing different
statistics for choosing "optimized" `k`. There are following statistics:

- ECDF curves of the consensus matrix for each `k`;
- 1-PAC. [The PAC
  score](https://en.wikipedia.org/wiki/Consensus_clustering#Over-interpretation_potential_of_consensus_clustering)
  measures the proportion of the ambiguous subgrouping.
- Mean silhouette score.
- Concordance. The mean probability of fiting the consensus class ids in all
  partitions.
- Area increased. Denote $A_k$ as the area under the ECDF curve for current
  `k`, the area increased is defined as $A_k - A_{k-1}$.
- Rand index. The percent of pairs of samples that are both in a same cluster
  or both are not in a same cluster in the partition of k and k-1.
- Jaccard index. The ratio of pairs of samples are both in a same cluster in
  the partition of k and k-1 and the pairs of samples are both in a same
  cluster in the partition k or k-1.

The detailed explanations of these statistics can be found in [the _cola_
vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/cola.html#toc_13).

Generally speaking, lower PAC score, higher mean silhouette score or higher
concordance corresponds to better partition. Rand index and Jaccard index
measure how similar the current partition is compared to partition with `k-1`.
If they are too similar, we won't accept `k` is better than `k-1`.

```r
select_partition_number(res)
```

![plot of chunk ATC-pam-select-partition-number](figure_cola/ATC-pam-select-partition-number-1.png)

The numeric values for all these statistics can be obtained by `get_stats()`.

```r
get_stats(res)
```

```
#>   k 1-PAC mean_silhouette concordance area_increased  Rand Jaccard
#> 2 2 0.958           0.936       0.974         0.5081 0.491   0.491
#> 3 3 1.000           0.976       0.991         0.2145 0.878   0.755
#> 4 4 0.859           0.872       0.936         0.1672 0.852   0.630
#> 5 5 0.953           0.932       0.971         0.0310 0.991   0.968
#> 6 6 0.839           0.866       0.927         0.0768 0.909   0.671
```

`suggest_best_k()` suggests the best $k$ based on these statistics. The rules are as follows:

- All $k$ with Jaccard index larger than 0.95 are removed because increasing
  $k$ does not provide enough extra information. If all $k$ are removed, it is
  marked as no subgroup is detected.
- For all $k$ with 1-PAC score larger than 0.9, the maximal $k$ is taken as
  the best $k$, and other $k$ are marked as optional $k$.
- If it does not fit the second rule. The $k$ with the maximal vote of the
  highest 1-PAC score, highest mean silhouette, and highest concordance is
  taken as the best $k$.

```r
suggest_best_k(res)
```

```
#> [1] 3
#> attr(,"optional")
#> [1] 2
```

There is also optional best $k$ = 2 that is worth to check.

Following shows the table of the partitions (You need to click the **show/hide
code output** link to see it). The membership matrix (columns with name `p*`)
is inferred by
[`clue::cl_consensus()`](https://www.rdocumentation.org/link/cl_consensus?package=clue)
function with the `SE` method. Basically the value in the membership matrix
represents the probability to belong to a certain group. The finall class
label for an item is determined with the group with highest probability it
belongs to.

In `get_classes()` function, the entropy is calculated from the membership
matrix and the silhouette score is calculated from the consensus matrix.



<script>
$( function() {
	$( '#tabs-ATC-pam-get-classes' ).tabs();
} );
</script>
<div id='tabs-ATC-pam-get-classes'>
<ul>
<li><a href='#tab-ATC-pam-get-classes-1'>k = 2</a></li>
<li><a href='#tab-ATC-pam-get-classes-2'>k = 3</a></li>
<li><a href='#tab-ATC-pam-get-classes-3'>k = 4</a></li>
<li><a href='#tab-ATC-pam-get-classes-4'>k = 5</a></li>
<li><a href='#tab-ATC-pam-get-classes-5'>k = 6</a></li>
</ul>

<div id='tab-ATC-pam-get-classes-1'>
<p><a id='tab-ATC-pam-get-classes-1-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 2), get_membership(res, k = 2))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2
#&gt; SRR1383358     1   0.000      0.984 1.000 0.000
#&gt; SRR1383360     1   0.000      0.984 1.000 0.000
#&gt; SRR1383359     1   0.000      0.984 1.000 0.000
#&gt; SRR1383362     1   0.000      0.984 1.000 0.000
#&gt; SRR1383361     1   0.000      0.984 1.000 0.000
#&gt; SRR1383363     1   0.000      0.984 1.000 0.000
#&gt; SRR1383364     1   0.000      0.984 1.000 0.000
#&gt; SRR1383365     1   0.000      0.984 1.000 0.000
#&gt; SRR1383366     1   0.000      0.984 1.000 0.000
#&gt; SRR1383367     1   0.000      0.984 1.000 0.000
#&gt; SRR1383368     1   0.000      0.984 1.000 0.000
#&gt; SRR1383369     1   0.000      0.984 1.000 0.000
#&gt; SRR1383370     1   0.000      0.984 1.000 0.000
#&gt; SRR1383371     1   0.000      0.984 1.000 0.000
#&gt; SRR1383372     1   0.000      0.984 1.000 0.000
#&gt; SRR1383373     1   0.000      0.984 1.000 0.000
#&gt; SRR1383374     2   0.767      0.711 0.224 0.776
#&gt; SRR1383375     2   0.991      0.200 0.444 0.556
#&gt; SRR1383376     2   0.000      0.958 0.000 1.000
#&gt; SRR1383377     1   0.000      0.984 1.000 0.000
#&gt; SRR1383378     2   0.000      0.958 0.000 1.000
#&gt; SRR1383379     2   0.000      0.958 0.000 1.000
#&gt; SRR1383380     2   0.000      0.958 0.000 1.000
#&gt; SRR1383381     1   0.595      0.830 0.856 0.144
#&gt; SRR1383382     1   0.000      0.984 1.000 0.000
#&gt; SRR1383383     2   0.000      0.958 0.000 1.000
#&gt; SRR1383385     1   0.224      0.959 0.964 0.036
#&gt; SRR1383384     2   0.000      0.958 0.000 1.000
#&gt; SRR1383386     2   0.000      0.958 0.000 1.000
#&gt; SRR1383387     2   0.000      0.958 0.000 1.000
#&gt; SRR1383389     1   0.000      0.984 1.000 0.000
#&gt; SRR1383391     2   0.000      0.958 0.000 1.000
#&gt; SRR1383388     2   0.000      0.958 0.000 1.000
#&gt; SRR1383392     2   0.000      0.958 0.000 1.000
#&gt; SRR1383390     2   0.000      0.958 0.000 1.000
#&gt; SRR1383394     2   0.000      0.958 0.000 1.000
#&gt; SRR1383393     1   0.224      0.959 0.964 0.036
#&gt; SRR1383396     1   0.224      0.959 0.964 0.036
#&gt; SRR1383395     1   0.000      0.984 1.000 0.000
#&gt; SRR1383399     1   0.456      0.892 0.904 0.096
#&gt; SRR1383400     1   0.224      0.959 0.964 0.036
#&gt; SRR1383397     2   0.000      0.958 0.000 1.000
#&gt; SRR1383401     2   0.000      0.958 0.000 1.000
#&gt; SRR1383398     2   0.000      0.958 0.000 1.000
#&gt; SRR1383402     2   0.000      0.958 0.000 1.000
#&gt; SRR1383404     2   0.000      0.958 0.000 1.000
#&gt; SRR1383403     2   0.932      0.463 0.348 0.652
#&gt; SRR1383405     2   0.000      0.958 0.000 1.000
#&gt; SRR1383406     2   0.000      0.958 0.000 1.000
#&gt; SRR1383407     1   0.000      0.984 1.000 0.000
#&gt; SRR1383408     2   0.000      0.958 0.000 1.000
#&gt; SRR1383409     2   0.000      0.958 0.000 1.000
#&gt; SRR1383410     2   0.000      0.958 0.000 1.000
</code></pre>

<script>
$('#tab-ATC-pam-get-classes-1-a').parent().next().next().hide();
$('#tab-ATC-pam-get-classes-1-a').click(function(){
  $('#tab-ATC-pam-get-classes-1-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-ATC-pam-get-classes-2'>
<p><a id='tab-ATC-pam-get-classes-2-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 3), get_membership(res, k = 3))
</code></pre>

<pre><code>#&gt;            class entropy silhouette p1    p2    p3
#&gt; SRR1383358     3   0.000      0.983  0 0.000 1.000
#&gt; SRR1383360     3   0.000      0.983  0 0.000 1.000
#&gt; SRR1383359     3   0.000      0.983  0 0.000 1.000
#&gt; SRR1383362     1   0.000      1.000  1 0.000 0.000
#&gt; SRR1383361     3   0.000      0.983  0 0.000 1.000
#&gt; SRR1383363     3   0.000      0.983  0 0.000 1.000
#&gt; SRR1383364     3   0.000      0.983  0 0.000 1.000
#&gt; SRR1383365     3   0.000      0.983  0 0.000 1.000
#&gt; SRR1383366     3   0.000      0.983  0 0.000 1.000
#&gt; SRR1383367     3   0.000      0.983  0 0.000 1.000
#&gt; SRR1383368     3   0.000      0.983  0 0.000 1.000
#&gt; SRR1383369     3   0.000      0.983  0 0.000 1.000
#&gt; SRR1383370     3   0.000      0.983  0 0.000 1.000
#&gt; SRR1383371     3   0.000      0.983  0 0.000 1.000
#&gt; SRR1383372     3   0.000      0.983  0 0.000 1.000
#&gt; SRR1383373     3   0.000      0.983  0 0.000 1.000
#&gt; SRR1383374     2   0.480      0.695  0 0.780 0.220
#&gt; SRR1383375     1   0.000      1.000  1 0.000 0.000
#&gt; SRR1383376     2   0.000      0.989  0 1.000 0.000
#&gt; SRR1383377     3   0.000      0.983  0 0.000 1.000
#&gt; SRR1383378     2   0.000      0.989  0 1.000 0.000
#&gt; SRR1383379     2   0.000      0.989  0 1.000 0.000
#&gt; SRR1383380     2   0.000      0.989  0 1.000 0.000
#&gt; SRR1383381     3   0.412      0.774  0 0.168 0.832
#&gt; SRR1383382     1   0.000      1.000  1 0.000 0.000
#&gt; SRR1383383     2   0.000      0.989  0 1.000 0.000
#&gt; SRR1383385     1   0.000      1.000  1 0.000 0.000
#&gt; SRR1383384     2   0.000      0.989  0 1.000 0.000
#&gt; SRR1383386     2   0.000      0.989  0 1.000 0.000
#&gt; SRR1383387     2   0.000      0.989  0 1.000 0.000
#&gt; SRR1383389     3   0.000      0.983  0 0.000 1.000
#&gt; SRR1383391     2   0.000      0.989  0 1.000 0.000
#&gt; SRR1383388     2   0.000      0.989  0 1.000 0.000
#&gt; SRR1383392     2   0.000      0.989  0 1.000 0.000
#&gt; SRR1383390     2   0.000      0.989  0 1.000 0.000
#&gt; SRR1383394     2   0.000      0.989  0 1.000 0.000
#&gt; SRR1383393     1   0.000      1.000  1 0.000 0.000
#&gt; SRR1383396     3   0.000      0.983  0 0.000 1.000
#&gt; SRR1383395     3   0.000      0.983  0 0.000 1.000
#&gt; SRR1383399     3   0.312      0.857  0 0.108 0.892
#&gt; SRR1383400     1   0.000      1.000  1 0.000 0.000
#&gt; SRR1383397     2   0.000      0.989  0 1.000 0.000
#&gt; SRR1383401     2   0.000      0.989  0 1.000 0.000
#&gt; SRR1383398     2   0.000      0.989  0 1.000 0.000
#&gt; SRR1383402     2   0.000      0.989  0 1.000 0.000
#&gt; SRR1383404     2   0.000      0.989  0 1.000 0.000
#&gt; SRR1383403     1   0.000      1.000  1 0.000 0.000
#&gt; SRR1383405     2   0.000      0.989  0 1.000 0.000
#&gt; SRR1383406     2   0.000      0.989  0 1.000 0.000
#&gt; SRR1383407     3   0.000      0.983  0 0.000 1.000
#&gt; SRR1383408     2   0.000      0.989  0 1.000 0.000
#&gt; SRR1383409     2   0.000      0.989  0 1.000 0.000
#&gt; SRR1383410     2   0.000      0.989  0 1.000 0.000
</code></pre>

<script>
$('#tab-ATC-pam-get-classes-2-a').parent().next().next().hide();
$('#tab-ATC-pam-get-classes-2-a').click(function(){
  $('#tab-ATC-pam-get-classes-2-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-ATC-pam-get-classes-3'>
<p><a id='tab-ATC-pam-get-classes-3-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 4), get_membership(res, k = 4))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4
#&gt; SRR1383358     3   0.000      0.971 0.000 0.000 1.000 0.000
#&gt; SRR1383360     3   0.000      0.971 0.000 0.000 1.000 0.000
#&gt; SRR1383359     3   0.000      0.971 0.000 0.000 1.000 0.000
#&gt; SRR1383362     1   0.000      0.763 1.000 0.000 0.000 0.000
#&gt; SRR1383361     3   0.000      0.971 0.000 0.000 1.000 0.000
#&gt; SRR1383363     3   0.000      0.971 0.000 0.000 1.000 0.000
#&gt; SRR1383364     3   0.000      0.971 0.000 0.000 1.000 0.000
#&gt; SRR1383365     3   0.000      0.971 0.000 0.000 1.000 0.000
#&gt; SRR1383366     3   0.361      0.720 0.000 0.200 0.800 0.000
#&gt; SRR1383367     3   0.000      0.971 0.000 0.000 1.000 0.000
#&gt; SRR1383368     3   0.000      0.971 0.000 0.000 1.000 0.000
#&gt; SRR1383369     3   0.000      0.971 0.000 0.000 1.000 0.000
#&gt; SRR1383370     3   0.000      0.971 0.000 0.000 1.000 0.000
#&gt; SRR1383371     3   0.000      0.971 0.000 0.000 1.000 0.000
#&gt; SRR1383372     3   0.387      0.677 0.000 0.000 0.772 0.228
#&gt; SRR1383373     3   0.000      0.971 0.000 0.000 1.000 0.000
#&gt; SRR1383374     2   0.419      0.609 0.000 0.732 0.268 0.000
#&gt; SRR1383375     1   0.484      0.683 0.604 0.000 0.000 0.396
#&gt; SRR1383376     2   0.000      0.962 0.000 1.000 0.000 0.000
#&gt; SRR1383377     3   0.000      0.971 0.000 0.000 1.000 0.000
#&gt; SRR1383378     4   0.000      0.811 0.000 0.000 0.000 1.000
#&gt; SRR1383379     2   0.139      0.923 0.000 0.952 0.000 0.048
#&gt; SRR1383380     4   0.000      0.811 0.000 0.000 0.000 1.000
#&gt; SRR1383381     4   0.519      0.690 0.000 0.148 0.096 0.756
#&gt; SRR1383382     1   0.000      0.763 1.000 0.000 0.000 0.000
#&gt; SRR1383383     2   0.000      0.962 0.000 1.000 0.000 0.000
#&gt; SRR1383385     1   0.404      0.765 0.752 0.000 0.000 0.248
#&gt; SRR1383384     2   0.000      0.962 0.000 1.000 0.000 0.000
#&gt; SRR1383386     4   0.000      0.811 0.000 0.000 0.000 1.000
#&gt; SRR1383387     2   0.000      0.962 0.000 1.000 0.000 0.000
#&gt; SRR1383389     4   0.433      0.558 0.000 0.000 0.288 0.712
#&gt; SRR1383391     2   0.000      0.962 0.000 1.000 0.000 0.000
#&gt; SRR1383388     4   0.000      0.811 0.000 0.000 0.000 1.000
#&gt; SRR1383392     2   0.000      0.962 0.000 1.000 0.000 0.000
#&gt; SRR1383390     2   0.312      0.793 0.000 0.844 0.000 0.156
#&gt; SRR1383394     2   0.000      0.962 0.000 1.000 0.000 0.000
#&gt; SRR1383393     1   0.464      0.731 0.656 0.000 0.000 0.344
#&gt; SRR1383396     4   0.000      0.811 0.000 0.000 0.000 1.000
#&gt; SRR1383395     3   0.000      0.971 0.000 0.000 1.000 0.000
#&gt; SRR1383399     4   0.516      0.686 0.000 0.088 0.156 0.756
#&gt; SRR1383400     1   0.000      0.763 1.000 0.000 0.000 0.000
#&gt; SRR1383397     2   0.000      0.962 0.000 1.000 0.000 0.000
#&gt; SRR1383401     2   0.000      0.962 0.000 1.000 0.000 0.000
#&gt; SRR1383398     4   0.000      0.811 0.000 0.000 0.000 1.000
#&gt; SRR1383402     2   0.000      0.962 0.000 1.000 0.000 0.000
#&gt; SRR1383404     4   0.401      0.615 0.000 0.244 0.000 0.756
#&gt; SRR1383403     1   0.483      0.689 0.608 0.000 0.000 0.392
#&gt; SRR1383405     2   0.000      0.962 0.000 1.000 0.000 0.000
#&gt; SRR1383406     2   0.179      0.904 0.000 0.932 0.000 0.068
#&gt; SRR1383407     3   0.000      0.971 0.000 0.000 1.000 0.000
#&gt; SRR1383408     2   0.000      0.962 0.000 1.000 0.000 0.000
#&gt; SRR1383409     2   0.000      0.962 0.000 1.000 0.000 0.000
#&gt; SRR1383410     2   0.000      0.962 0.000 1.000 0.000 0.000
</code></pre>

<script>
$('#tab-ATC-pam-get-classes-3-a').parent().next().next().hide();
$('#tab-ATC-pam-get-classes-3-a').click(function(){
  $('#tab-ATC-pam-get-classes-3-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-ATC-pam-get-classes-4'>
<p><a id='tab-ATC-pam-get-classes-4-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 5), get_membership(res, k = 5))
</code></pre>

<pre><code>#&gt;            class entropy silhouette   p1    p2    p3    p4    p5
#&gt; SRR1383358     3  0.0609      0.958 0.00 0.000 0.980 0.000 0.020
#&gt; SRR1383360     3  0.0000      0.966 0.00 0.000 1.000 0.000 0.000
#&gt; SRR1383359     3  0.0000      0.966 0.00 0.000 1.000 0.000 0.000
#&gt; SRR1383362     5  0.0609      1.000 0.02 0.000 0.000 0.000 0.980
#&gt; SRR1383361     3  0.0000      0.966 0.00 0.000 1.000 0.000 0.000
#&gt; SRR1383363     3  0.0000      0.966 0.00 0.000 1.000 0.000 0.000
#&gt; SRR1383364     3  0.0000      0.966 0.00 0.000 1.000 0.000 0.000
#&gt; SRR1383365     3  0.0000      0.966 0.00 0.000 1.000 0.000 0.000
#&gt; SRR1383366     3  0.3586      0.713 0.00 0.188 0.792 0.000 0.020
#&gt; SRR1383367     3  0.0609      0.958 0.00 0.000 0.980 0.000 0.020
#&gt; SRR1383368     3  0.0000      0.966 0.00 0.000 1.000 0.000 0.000
#&gt; SRR1383369     3  0.0510      0.959 0.00 0.000 0.984 0.000 0.016
#&gt; SRR1383370     3  0.0000      0.966 0.00 0.000 1.000 0.000 0.000
#&gt; SRR1383371     3  0.0000      0.966 0.00 0.000 1.000 0.000 0.000
#&gt; SRR1383372     3  0.3757      0.712 0.00 0.000 0.772 0.208 0.020
#&gt; SRR1383373     3  0.0000      0.966 0.00 0.000 1.000 0.000 0.000
#&gt; SRR1383374     2  0.4161      0.544 0.00 0.704 0.280 0.000 0.016
#&gt; SRR1383375     1  0.0000      1.000 1.00 0.000 0.000 0.000 0.000
#&gt; SRR1383376     2  0.0000      0.938 0.00 1.000 0.000 0.000 0.000
#&gt; SRR1383377     3  0.0162      0.964 0.00 0.000 0.996 0.000 0.004
#&gt; SRR1383378     4  0.0000      0.986 0.00 0.000 0.000 1.000 0.000
#&gt; SRR1383379     2  0.2852      0.766 0.00 0.828 0.000 0.172 0.000
#&gt; SRR1383380     4  0.0000      0.986 0.00 0.000 0.000 1.000 0.000
#&gt; SRR1383381     4  0.0162      0.984 0.00 0.000 0.000 0.996 0.004
#&gt; SRR1383382     5  0.0609      1.000 0.02 0.000 0.000 0.000 0.980
#&gt; SRR1383383     2  0.0000      0.938 0.00 1.000 0.000 0.000 0.000
#&gt; SRR1383385     1  0.0000      1.000 1.00 0.000 0.000 0.000 0.000
#&gt; SRR1383384     2  0.0000      0.938 0.00 1.000 0.000 0.000 0.000
#&gt; SRR1383386     4  0.0000      0.986 0.00 0.000 0.000 1.000 0.000
#&gt; SRR1383387     2  0.0000      0.938 0.00 1.000 0.000 0.000 0.000
#&gt; SRR1383389     4  0.1831      0.881 0.00 0.000 0.076 0.920 0.004
#&gt; SRR1383391     2  0.0000      0.938 0.00 1.000 0.000 0.000 0.000
#&gt; SRR1383388     4  0.0000      0.986 0.00 0.000 0.000 1.000 0.000
#&gt; SRR1383392     2  0.0000      0.938 0.00 1.000 0.000 0.000 0.000
#&gt; SRR1383390     2  0.4126      0.423 0.00 0.620 0.000 0.380 0.000
#&gt; SRR1383394     2  0.0000      0.938 0.00 1.000 0.000 0.000 0.000
#&gt; SRR1383393     1  0.0000      1.000 1.00 0.000 0.000 0.000 0.000
#&gt; SRR1383396     4  0.0162      0.984 0.00 0.000 0.000 0.996 0.004
#&gt; SRR1383395     3  0.0609      0.958 0.00 0.000 0.980 0.000 0.020
#&gt; SRR1383399     4  0.0162      0.984 0.00 0.000 0.000 0.996 0.004
#&gt; SRR1383400     5  0.0609      1.000 0.02 0.000 0.000 0.000 0.980
#&gt; SRR1383397     2  0.0162      0.936 0.00 0.996 0.000 0.004 0.000
#&gt; SRR1383401     2  0.0000      0.938 0.00 1.000 0.000 0.000 0.000
#&gt; SRR1383398     4  0.0000      0.986 0.00 0.000 0.000 1.000 0.000
#&gt; SRR1383402     2  0.0000      0.938 0.00 1.000 0.000 0.000 0.000
#&gt; SRR1383404     4  0.0000      0.986 0.00 0.000 0.000 1.000 0.000
#&gt; SRR1383403     1  0.0000      1.000 1.00 0.000 0.000 0.000 0.000
#&gt; SRR1383405     2  0.0000      0.938 0.00 1.000 0.000 0.000 0.000
#&gt; SRR1383406     2  0.0609      0.923 0.00 0.980 0.000 0.020 0.000
#&gt; SRR1383407     3  0.0000      0.966 0.00 0.000 1.000 0.000 0.000
#&gt; SRR1383408     2  0.0000      0.938 0.00 1.000 0.000 0.000 0.000
#&gt; SRR1383409     2  0.0000      0.938 0.00 1.000 0.000 0.000 0.000
#&gt; SRR1383410     2  0.0000      0.938 0.00 1.000 0.000 0.000 0.000
</code></pre>

<script>
$('#tab-ATC-pam-get-classes-4-a').parent().next().next().hide();
$('#tab-ATC-pam-get-classes-4-a').click(function(){
  $('#tab-ATC-pam-get-classes-4-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-ATC-pam-get-classes-5'>
<p><a id='tab-ATC-pam-get-classes-5-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 6), get_membership(res, k = 6))
</code></pre>

<pre><code>#&gt;            class entropy silhouette p1    p2    p3    p4    p5 p6
#&gt; SRR1383358     3  0.2048     0.8182  0 0.000 0.880 0.000 0.120  0
#&gt; SRR1383360     5  0.0000     0.9031  0 0.000 0.000 0.000 1.000  0
#&gt; SRR1383359     5  0.0000     0.9031  0 0.000 0.000 0.000 1.000  0
#&gt; SRR1383362     6  0.0000     1.0000  0 0.000 0.000 0.000 0.000  1
#&gt; SRR1383361     5  0.0000     0.9031  0 0.000 0.000 0.000 1.000  0
#&gt; SRR1383363     3  0.3531     0.6673  0 0.000 0.672 0.000 0.328  0
#&gt; SRR1383364     5  0.2048     0.7816  0 0.000 0.120 0.000 0.880  0
#&gt; SRR1383365     5  0.0000     0.9031  0 0.000 0.000 0.000 1.000  0
#&gt; SRR1383366     3  0.2048     0.8182  0 0.000 0.880 0.000 0.120  0
#&gt; SRR1383367     3  0.2048     0.8182  0 0.000 0.880 0.000 0.120  0
#&gt; SRR1383368     3  0.3531     0.6673  0 0.000 0.672 0.000 0.328  0
#&gt; SRR1383369     5  0.2823     0.6806  0 0.000 0.204 0.000 0.796  0
#&gt; SRR1383370     5  0.1204     0.8539  0 0.000 0.056 0.000 0.944  0
#&gt; SRR1383371     5  0.0000     0.9031  0 0.000 0.000 0.000 1.000  0
#&gt; SRR1383372     3  0.2048     0.8182  0 0.000 0.880 0.000 0.120  0
#&gt; SRR1383373     5  0.0000     0.9031  0 0.000 0.000 0.000 1.000  0
#&gt; SRR1383374     3  0.3107     0.7824  0 0.052 0.832 0.000 0.116  0
#&gt; SRR1383375     1  0.0000     1.0000  1 0.000 0.000 0.000 0.000  0
#&gt; SRR1383376     2  0.0000     0.9470  0 1.000 0.000 0.000 0.000  0
#&gt; SRR1383377     5  0.0146     0.9008  0 0.000 0.004 0.000 0.996  0
#&gt; SRR1383378     4  0.0000     0.9607  0 0.000 0.000 1.000 0.000  0
#&gt; SRR1383379     2  0.2941     0.7644  0 0.780 0.000 0.220 0.000  0
#&gt; SRR1383380     4  0.0000     0.9607  0 0.000 0.000 1.000 0.000  0
#&gt; SRR1383381     4  0.2135     0.8742  0 0.000 0.128 0.872 0.000  0
#&gt; SRR1383382     6  0.0000     1.0000  0 0.000 0.000 0.000 0.000  1
#&gt; SRR1383383     2  0.0000     0.9470  0 1.000 0.000 0.000 0.000  0
#&gt; SRR1383385     1  0.0000     1.0000  1 0.000 0.000 0.000 0.000  0
#&gt; SRR1383384     2  0.0000     0.9470  0 1.000 0.000 0.000 0.000  0
#&gt; SRR1383386     4  0.0000     0.9607  0 0.000 0.000 1.000 0.000  0
#&gt; SRR1383387     2  0.0000     0.9470  0 1.000 0.000 0.000 0.000  0
#&gt; SRR1383389     3  0.5277     0.4629  0 0.000 0.528 0.364 0.108  0
#&gt; SRR1383391     2  0.0000     0.9470  0 1.000 0.000 0.000 0.000  0
#&gt; SRR1383388     4  0.0000     0.9607  0 0.000 0.000 1.000 0.000  0
#&gt; SRR1383392     2  0.0000     0.9470  0 1.000 0.000 0.000 0.000  0
#&gt; SRR1383390     2  0.3198     0.6585  0 0.740 0.000 0.260 0.000  0
#&gt; SRR1383394     2  0.0000     0.9470  0 1.000 0.000 0.000 0.000  0
#&gt; SRR1383393     1  0.0000     1.0000  1 0.000 0.000 0.000 0.000  0
#&gt; SRR1383396     4  0.2092     0.8776  0 0.000 0.124 0.876 0.000  0
#&gt; SRR1383395     5  0.3862    -0.0162  0 0.000 0.476 0.000 0.524  0
#&gt; SRR1383399     3  0.2823     0.5872  0 0.000 0.796 0.204 0.000  0
#&gt; SRR1383400     6  0.0000     1.0000  0 0.000 0.000 0.000 0.000  1
#&gt; SRR1383397     2  0.2135     0.8555  0 0.872 0.000 0.128 0.000  0
#&gt; SRR1383401     2  0.0000     0.9470  0 1.000 0.000 0.000 0.000  0
#&gt; SRR1383398     4  0.0000     0.9607  0 0.000 0.000 1.000 0.000  0
#&gt; SRR1383402     2  0.0000     0.9470  0 1.000 0.000 0.000 0.000  0
#&gt; SRR1383404     4  0.0000     0.9607  0 0.000 0.000 1.000 0.000  0
#&gt; SRR1383403     1  0.0000     1.0000  1 0.000 0.000 0.000 0.000  0
#&gt; SRR1383405     2  0.0632     0.9333  0 0.976 0.000 0.024 0.000  0
#&gt; SRR1383406     2  0.2300     0.8421  0 0.856 0.000 0.144 0.000  0
#&gt; SRR1383407     5  0.0000     0.9031  0 0.000 0.000 0.000 1.000  0
#&gt; SRR1383408     2  0.0000     0.9470  0 1.000 0.000 0.000 0.000  0
#&gt; SRR1383409     2  0.0000     0.9470  0 1.000 0.000 0.000 0.000  0
#&gt; SRR1383410     2  0.0000     0.9470  0 1.000 0.000 0.000 0.000  0
</code></pre>

<script>
$('#tab-ATC-pam-get-classes-5-a').parent().next().next().hide();
$('#tab-ATC-pam-get-classes-5-a').click(function(){
  $('#tab-ATC-pam-get-classes-5-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>
</div>

Heatmaps for the consensus matrix. It visualizes the probability of two
samples to be in a same group.



<script>
$( function() {
	$( '#tabs-ATC-pam-consensus-heatmap' ).tabs();
} );
</script>
<div id='tabs-ATC-pam-consensus-heatmap'>
<ul>
<li><a href='#tab-ATC-pam-consensus-heatmap-1'>k = 2</a></li>
<li><a href='#tab-ATC-pam-consensus-heatmap-2'>k = 3</a></li>
<li><a href='#tab-ATC-pam-consensus-heatmap-3'>k = 4</a></li>
<li><a href='#tab-ATC-pam-consensus-heatmap-4'>k = 5</a></li>
<li><a href='#tab-ATC-pam-consensus-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-ATC-pam-consensus-heatmap-1'>
<pre><code class="r">consensus_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-ATC-pam-consensus-heatmap-1-1.png" alt="plot of chunk tab-ATC-pam-consensus-heatmap-1"/></p>

</div>
<div id='tab-ATC-pam-consensus-heatmap-2'>
<pre><code class="r">consensus_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-ATC-pam-consensus-heatmap-2-1.png" alt="plot of chunk tab-ATC-pam-consensus-heatmap-2"/></p>

</div>
<div id='tab-ATC-pam-consensus-heatmap-3'>
<pre><code class="r">consensus_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-ATC-pam-consensus-heatmap-3-1.png" alt="plot of chunk tab-ATC-pam-consensus-heatmap-3"/></p>

</div>
<div id='tab-ATC-pam-consensus-heatmap-4'>
<pre><code class="r">consensus_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-ATC-pam-consensus-heatmap-4-1.png" alt="plot of chunk tab-ATC-pam-consensus-heatmap-4"/></p>

</div>
<div id='tab-ATC-pam-consensus-heatmap-5'>
<pre><code class="r">consensus_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-ATC-pam-consensus-heatmap-5-1.png" alt="plot of chunk tab-ATC-pam-consensus-heatmap-5"/></p>

</div>
</div>

Heatmaps for the membership of samples in all partitions to see how consistent they are:




<script>
$( function() {
	$( '#tabs-ATC-pam-membership-heatmap' ).tabs();
} );
</script>
<div id='tabs-ATC-pam-membership-heatmap'>
<ul>
<li><a href='#tab-ATC-pam-membership-heatmap-1'>k = 2</a></li>
<li><a href='#tab-ATC-pam-membership-heatmap-2'>k = 3</a></li>
<li><a href='#tab-ATC-pam-membership-heatmap-3'>k = 4</a></li>
<li><a href='#tab-ATC-pam-membership-heatmap-4'>k = 5</a></li>
<li><a href='#tab-ATC-pam-membership-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-ATC-pam-membership-heatmap-1'>
<pre><code class="r">membership_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-ATC-pam-membership-heatmap-1-1.png" alt="plot of chunk tab-ATC-pam-membership-heatmap-1"/></p>

</div>
<div id='tab-ATC-pam-membership-heatmap-2'>
<pre><code class="r">membership_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-ATC-pam-membership-heatmap-2-1.png" alt="plot of chunk tab-ATC-pam-membership-heatmap-2"/></p>

</div>
<div id='tab-ATC-pam-membership-heatmap-3'>
<pre><code class="r">membership_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-ATC-pam-membership-heatmap-3-1.png" alt="plot of chunk tab-ATC-pam-membership-heatmap-3"/></p>

</div>
<div id='tab-ATC-pam-membership-heatmap-4'>
<pre><code class="r">membership_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-ATC-pam-membership-heatmap-4-1.png" alt="plot of chunk tab-ATC-pam-membership-heatmap-4"/></p>

</div>
<div id='tab-ATC-pam-membership-heatmap-5'>
<pre><code class="r">membership_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-ATC-pam-membership-heatmap-5-1.png" alt="plot of chunk tab-ATC-pam-membership-heatmap-5"/></p>

</div>
</div>

As soon as we have had the classes for columns, we can look for signatures
which are significantly different between classes which can be candidate marks
for certain classes. Following are the heatmaps for signatures.



Signature heatmaps where rows are scaled:



<script>
$( function() {
	$( '#tabs-ATC-pam-get-signatures' ).tabs();
} );
</script>
<div id='tabs-ATC-pam-get-signatures'>
<ul>
<li><a href='#tab-ATC-pam-get-signatures-1'>k = 2</a></li>
<li><a href='#tab-ATC-pam-get-signatures-2'>k = 3</a></li>
<li><a href='#tab-ATC-pam-get-signatures-3'>k = 4</a></li>
<li><a href='#tab-ATC-pam-get-signatures-4'>k = 5</a></li>
<li><a href='#tab-ATC-pam-get-signatures-5'>k = 6</a></li>
</ul>
<div id='tab-ATC-pam-get-signatures-1'>
<pre><code class="r">get_signatures(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-ATC-pam-get-signatures-1-1.png" alt="plot of chunk tab-ATC-pam-get-signatures-1"/></p>

</div>
<div id='tab-ATC-pam-get-signatures-2'>
<pre><code class="r">get_signatures(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-ATC-pam-get-signatures-2-1.png" alt="plot of chunk tab-ATC-pam-get-signatures-2"/></p>

</div>
<div id='tab-ATC-pam-get-signatures-3'>
<pre><code class="r">get_signatures(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-ATC-pam-get-signatures-3-1.png" alt="plot of chunk tab-ATC-pam-get-signatures-3"/></p>

</div>
<div id='tab-ATC-pam-get-signatures-4'>
<pre><code class="r">get_signatures(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-ATC-pam-get-signatures-4-1.png" alt="plot of chunk tab-ATC-pam-get-signatures-4"/></p>

</div>
<div id='tab-ATC-pam-get-signatures-5'>
<pre><code class="r">get_signatures(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-ATC-pam-get-signatures-5-1.png" alt="plot of chunk tab-ATC-pam-get-signatures-5"/></p>

</div>
</div>



Signature heatmaps where rows are not scaled:


<script>
$( function() {
	$( '#tabs-ATC-pam-get-signatures-no-scale' ).tabs();
} );
</script>
<div id='tabs-ATC-pam-get-signatures-no-scale'>
<ul>
<li><a href='#tab-ATC-pam-get-signatures-no-scale-1'>k = 2</a></li>
<li><a href='#tab-ATC-pam-get-signatures-no-scale-2'>k = 3</a></li>
<li><a href='#tab-ATC-pam-get-signatures-no-scale-3'>k = 4</a></li>
<li><a href='#tab-ATC-pam-get-signatures-no-scale-4'>k = 5</a></li>
<li><a href='#tab-ATC-pam-get-signatures-no-scale-5'>k = 6</a></li>
</ul>
<div id='tab-ATC-pam-get-signatures-no-scale-1'>
<pre><code class="r">get_signatures(res, k = 2, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-ATC-pam-get-signatures-no-scale-1-1.png" alt="plot of chunk tab-ATC-pam-get-signatures-no-scale-1"/></p>

</div>
<div id='tab-ATC-pam-get-signatures-no-scale-2'>
<pre><code class="r">get_signatures(res, k = 3, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-ATC-pam-get-signatures-no-scale-2-1.png" alt="plot of chunk tab-ATC-pam-get-signatures-no-scale-2"/></p>

</div>
<div id='tab-ATC-pam-get-signatures-no-scale-3'>
<pre><code class="r">get_signatures(res, k = 4, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-ATC-pam-get-signatures-no-scale-3-1.png" alt="plot of chunk tab-ATC-pam-get-signatures-no-scale-3"/></p>

</div>
<div id='tab-ATC-pam-get-signatures-no-scale-4'>
<pre><code class="r">get_signatures(res, k = 5, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-ATC-pam-get-signatures-no-scale-4-1.png" alt="plot of chunk tab-ATC-pam-get-signatures-no-scale-4"/></p>

</div>
<div id='tab-ATC-pam-get-signatures-no-scale-5'>
<pre><code class="r">get_signatures(res, k = 6, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-ATC-pam-get-signatures-no-scale-5-1.png" alt="plot of chunk tab-ATC-pam-get-signatures-no-scale-5"/></p>

</div>
</div>



Compare the overlap of signatures from different k:

```r
compare_signatures(res)
```

![plot of chunk ATC-pam-signature_compare](figure_cola/ATC-pam-signature_compare-1.png)

`get_signature()` returns a data frame invisibly. TO get the list of signatures, the function
call should be assigned to a variable explicitly. In following code, if `plot` argument is set
to `FALSE`, no heatmap is plotted while only the differential analysis is performed.

```r
# code only for demonstration
tb = get_signature(res, k = ..., plot = FALSE)
```

An example of the output of `tb` is:

```
#>   which_row         fdr    mean_1    mean_2 scaled_mean_1 scaled_mean_2 km
#> 1        38 0.042760348  8.373488  9.131774    -0.5533452     0.5164555  1
#> 2        40 0.018707592  7.106213  8.469186    -0.6173731     0.5762149  1
#> 3        55 0.019134737 10.221463 11.207825    -0.6159697     0.5749050  1
#> 4        59 0.006059896  5.921854  7.869574    -0.6899429     0.6439467  1
#> 5        60 0.018055526  8.928898 10.211722    -0.6204761     0.5791110  1
#> 6        98 0.009384629 15.714769 14.887706     0.6635654    -0.6193277  2
...
```

The columns in `tb` are:

1. `which_row`: row indices corresponding to the input matrix.
2. `fdr`: FDR for the differential test. 
3. `mean_x`: The mean value in group x.
4. `scaled_mean_x`: The mean value in group x after rows are scaled.
5. `km`: Row groups if k-means clustering is applied to rows.



UMAP plot which shows how samples are separated.


<script>
$( function() {
	$( '#tabs-ATC-pam-dimension-reduction' ).tabs();
} );
</script>
<div id='tabs-ATC-pam-dimension-reduction'>
<ul>
<li><a href='#tab-ATC-pam-dimension-reduction-1'>k = 2</a></li>
<li><a href='#tab-ATC-pam-dimension-reduction-2'>k = 3</a></li>
<li><a href='#tab-ATC-pam-dimension-reduction-3'>k = 4</a></li>
<li><a href='#tab-ATC-pam-dimension-reduction-4'>k = 5</a></li>
<li><a href='#tab-ATC-pam-dimension-reduction-5'>k = 6</a></li>
</ul>
<div id='tab-ATC-pam-dimension-reduction-1'>
<pre><code class="r">dimension_reduction(res, k = 2, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-ATC-pam-dimension-reduction-1-1.png" alt="plot of chunk tab-ATC-pam-dimension-reduction-1"/></p>

</div>
<div id='tab-ATC-pam-dimension-reduction-2'>
<pre><code class="r">dimension_reduction(res, k = 3, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-ATC-pam-dimension-reduction-2-1.png" alt="plot of chunk tab-ATC-pam-dimension-reduction-2"/></p>

</div>
<div id='tab-ATC-pam-dimension-reduction-3'>
<pre><code class="r">dimension_reduction(res, k = 4, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-ATC-pam-dimension-reduction-3-1.png" alt="plot of chunk tab-ATC-pam-dimension-reduction-3"/></p>

</div>
<div id='tab-ATC-pam-dimension-reduction-4'>
<pre><code class="r">dimension_reduction(res, k = 5, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-ATC-pam-dimension-reduction-4-1.png" alt="plot of chunk tab-ATC-pam-dimension-reduction-4"/></p>

</div>
<div id='tab-ATC-pam-dimension-reduction-5'>
<pre><code class="r">dimension_reduction(res, k = 6, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-ATC-pam-dimension-reduction-5-1.png" alt="plot of chunk tab-ATC-pam-dimension-reduction-5"/></p>

</div>
</div>


Following heatmap shows how subgroups are split when increasing `k`:

```r
collect_classes(res)
```

![plot of chunk ATC-pam-collect-classes](figure_cola/ATC-pam-collect-classes-1.png)


If matrix rows can be associated to genes, consider to use `functional_enrichment(res,
...)` to perform function enrichment for the signature genes. See [this vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/functional_enrichment.html) for more detailed explanations.


 

---------------------------------------------------




### ATC:mclust






The object with results only for a single top-value method and a single partition method 
can be extracted as:

```r
res = res_list["ATC", "mclust"]
# you can also extract it by
# res = res_list["ATC:mclust"]
```

A summary of `res` and all the functions that can be applied to it:

```r
res
```

```
#> A 'ConsensusPartition' object with k = 2, 3, 4, 5, 6.
#>   On a matrix with 15680 rows and 53 columns.
#>   Top rows (1000, 2000, 3000, 4000, 5000) are extracted by 'ATC' method.
#>   Subgroups are detected by 'mclust' method.
#>   Performed in total 1250 partitions by row resampling.
#>   Best k for subgroups seems to be 3.
#> 
#> Following methods can be applied to this 'ConsensusPartition' object:
#>  [1] "cola_report"             "collect_classes"         "collect_plots"          
#>  [4] "collect_stats"           "colnames"                "compare_signatures"     
#>  [7] "consensus_heatmap"       "dimension_reduction"     "functional_enrichment"  
#> [10] "get_anno_col"            "get_anno"                "get_classes"            
#> [13] "get_consensus"           "get_matrix"              "get_membership"         
#> [16] "get_param"               "get_signatures"          "get_stats"              
#> [19] "is_best_k"               "is_stable_k"             "membership_heatmap"     
#> [22] "ncol"                    "nrow"                    "plot_ecdf"              
#> [25] "rownames"                "select_partition_number" "show"                   
#> [28] "suggest_best_k"          "test_to_known_factors"
```

`collect_plots()` function collects all the plots made from `res` for all `k` (number of partitions)
into one single page to provide an easy and fast comparison between different `k`.

```r
collect_plots(res)
```

![plot of chunk ATC-mclust-collect-plots](figure_cola/ATC-mclust-collect-plots-1.png)

The plots are:

- The first row: a plot of the ECDF (empirical cumulative distribution
  function) curves of the consensus matrix for each `k` and the heatmap of
  predicted classes for each `k`.
- The second row: heatmaps of the consensus matrix for each `k`.
- The third row: heatmaps of the membership matrix for each `k`.
- The fouth row: heatmaps of the signatures for each `k`.

All the plots in panels can be made by individual functions and they are
plotted later in this section.

`select_partition_number()` produces several plots showing different
statistics for choosing "optimized" `k`. There are following statistics:

- ECDF curves of the consensus matrix for each `k`;
- 1-PAC. [The PAC
  score](https://en.wikipedia.org/wiki/Consensus_clustering#Over-interpretation_potential_of_consensus_clustering)
  measures the proportion of the ambiguous subgrouping.
- Mean silhouette score.
- Concordance. The mean probability of fiting the consensus class ids in all
  partitions.
- Area increased. Denote $A_k$ as the area under the ECDF curve for current
  `k`, the area increased is defined as $A_k - A_{k-1}$.
- Rand index. The percent of pairs of samples that are both in a same cluster
  or both are not in a same cluster in the partition of k and k-1.
- Jaccard index. The ratio of pairs of samples are both in a same cluster in
  the partition of k and k-1 and the pairs of samples are both in a same
  cluster in the partition k or k-1.

The detailed explanations of these statistics can be found in [the _cola_
vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/cola.html#toc_13).

Generally speaking, lower PAC score, higher mean silhouette score or higher
concordance corresponds to better partition. Rand index and Jaccard index
measure how similar the current partition is compared to partition with `k-1`.
If they are too similar, we won't accept `k` is better than `k-1`.

```r
select_partition_number(res)
```

![plot of chunk ATC-mclust-select-partition-number](figure_cola/ATC-mclust-select-partition-number-1.png)

The numeric values for all these statistics can be obtained by `get_stats()`.

```r
get_stats(res)
```

```
#>   k 1-PAC mean_silhouette concordance area_increased  Rand Jaccard
#> 2 2 0.403           0.849       0.845         0.4305 0.543   0.543
#> 3 3 0.418           0.723       0.841         0.4496 0.669   0.453
#> 4 4 0.514           0.375       0.648         0.1433 0.774   0.479
#> 5 5 0.586           0.498       0.607         0.0864 0.765   0.388
#> 6 6 0.765           0.760       0.843         0.0620 0.900   0.587
```

`suggest_best_k()` suggests the best $k$ based on these statistics. The rules are as follows:

- All $k$ with Jaccard index larger than 0.95 are removed because increasing
  $k$ does not provide enough extra information. If all $k$ are removed, it is
  marked as no subgroup is detected.
- For all $k$ with 1-PAC score larger than 0.9, the maximal $k$ is taken as
  the best $k$, and other $k$ are marked as optional $k$.
- If it does not fit the second rule. The $k$ with the maximal vote of the
  highest 1-PAC score, highest mean silhouette, and highest concordance is
  taken as the best $k$.

```r
suggest_best_k(res)
```

```
#> [1] 3
```


Following shows the table of the partitions (You need to click the **show/hide
code output** link to see it). The membership matrix (columns with name `p*`)
is inferred by
[`clue::cl_consensus()`](https://www.rdocumentation.org/link/cl_consensus?package=clue)
function with the `SE` method. Basically the value in the membership matrix
represents the probability to belong to a certain group. The finall class
label for an item is determined with the group with highest probability it
belongs to.

In `get_classes()` function, the entropy is calculated from the membership
matrix and the silhouette score is calculated from the consensus matrix.



<script>
$( function() {
	$( '#tabs-ATC-mclust-get-classes' ).tabs();
} );
</script>
<div id='tabs-ATC-mclust-get-classes'>
<ul>
<li><a href='#tab-ATC-mclust-get-classes-1'>k = 2</a></li>
<li><a href='#tab-ATC-mclust-get-classes-2'>k = 3</a></li>
<li><a href='#tab-ATC-mclust-get-classes-3'>k = 4</a></li>
<li><a href='#tab-ATC-mclust-get-classes-4'>k = 5</a></li>
<li><a href='#tab-ATC-mclust-get-classes-5'>k = 6</a></li>
</ul>

<div id='tab-ATC-mclust-get-classes-1'>
<p><a id='tab-ATC-mclust-get-classes-1-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 2), get_membership(res, k = 2))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2
#&gt; SRR1383358     2  0.8661      0.853 0.288 0.712
#&gt; SRR1383360     2  0.8713      0.851 0.292 0.708
#&gt; SRR1383359     2  0.8661      0.853 0.288 0.712
#&gt; SRR1383362     1  0.1843      0.930 0.972 0.028
#&gt; SRR1383361     2  0.8661      0.853 0.288 0.712
#&gt; SRR1383363     2  0.8661      0.853 0.288 0.712
#&gt; SRR1383364     2  0.8661      0.853 0.288 0.712
#&gt; SRR1383365     2  0.8661      0.853 0.288 0.712
#&gt; SRR1383366     2  0.8661      0.853 0.288 0.712
#&gt; SRR1383367     2  0.8661      0.853 0.288 0.712
#&gt; SRR1383368     1  0.5946      0.776 0.856 0.144
#&gt; SRR1383369     2  0.8661      0.853 0.288 0.712
#&gt; SRR1383370     2  0.8661      0.853 0.288 0.712
#&gt; SRR1383371     2  0.8661      0.853 0.288 0.712
#&gt; SRR1383372     2  0.8608      0.854 0.284 0.716
#&gt; SRR1383373     2  0.8661      0.853 0.288 0.712
#&gt; SRR1383374     2  0.7815      0.845 0.232 0.768
#&gt; SRR1383375     1  0.0000      0.951 1.000 0.000
#&gt; SRR1383376     2  0.1843      0.735 0.028 0.972
#&gt; SRR1383377     2  0.8763      0.852 0.296 0.704
#&gt; SRR1383378     1  0.0376      0.951 0.996 0.004
#&gt; SRR1383379     1  0.5178      0.844 0.884 0.116
#&gt; SRR1383380     1  0.0376      0.951 0.996 0.004
#&gt; SRR1383381     2  0.9044      0.842 0.320 0.680
#&gt; SRR1383382     1  0.1843      0.930 0.972 0.028
#&gt; SRR1383383     2  0.2603      0.743 0.044 0.956
#&gt; SRR1383385     1  0.0000      0.951 1.000 0.000
#&gt; SRR1383384     2  0.1843      0.735 0.028 0.972
#&gt; SRR1383386     1  0.0376      0.951 0.996 0.004
#&gt; SRR1383387     2  0.4690      0.761 0.100 0.900
#&gt; SRR1383389     2  0.9000      0.844 0.316 0.684
#&gt; SRR1383391     2  0.7219      0.658 0.200 0.800
#&gt; SRR1383388     1  0.1633      0.938 0.976 0.024
#&gt; SRR1383392     2  0.7528      0.831 0.216 0.784
#&gt; SRR1383390     2  0.4431      0.773 0.092 0.908
#&gt; SRR1383394     2  0.4815      0.759 0.104 0.896
#&gt; SRR1383393     1  0.0000      0.951 1.000 0.000
#&gt; SRR1383396     1  0.0376      0.951 0.996 0.004
#&gt; SRR1383395     2  0.8909      0.848 0.308 0.692
#&gt; SRR1383399     2  0.9044      0.842 0.320 0.680
#&gt; SRR1383400     1  0.1414      0.937 0.980 0.020
#&gt; SRR1383397     1  0.7602      0.708 0.780 0.220
#&gt; SRR1383401     2  0.8267      0.836 0.260 0.740
#&gt; SRR1383398     1  0.0376      0.951 0.996 0.004
#&gt; SRR1383402     2  0.4690      0.765 0.100 0.900
#&gt; SRR1383404     1  0.0376      0.951 0.996 0.004
#&gt; SRR1383403     1  0.0000      0.951 1.000 0.000
#&gt; SRR1383405     2  0.2236      0.737 0.036 0.964
#&gt; SRR1383406     1  0.2236      0.929 0.964 0.036
#&gt; SRR1383407     2  0.8661      0.853 0.288 0.712
#&gt; SRR1383408     2  0.1843      0.735 0.028 0.972
#&gt; SRR1383409     2  0.4298      0.766 0.088 0.912
#&gt; SRR1383410     2  0.4022      0.769 0.080 0.920
</code></pre>

<script>
$('#tab-ATC-mclust-get-classes-1-a').parent().next().next().hide();
$('#tab-ATC-mclust-get-classes-1-a').click(function(){
  $('#tab-ATC-mclust-get-classes-1-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-ATC-mclust-get-classes-2'>
<p><a id='tab-ATC-mclust-get-classes-2-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 3), get_membership(res, k = 3))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3
#&gt; SRR1383358     3  0.4178      0.732 0.000 0.172 0.828
#&gt; SRR1383360     3  0.3995      0.817 0.116 0.016 0.868
#&gt; SRR1383359     3  0.3551      0.819 0.132 0.000 0.868
#&gt; SRR1383362     1  0.0237      0.737 0.996 0.004 0.000
#&gt; SRR1383361     3  0.0000      0.812 0.000 0.000 1.000
#&gt; SRR1383363     3  0.4002      0.745 0.000 0.160 0.840
#&gt; SRR1383364     3  0.7880      0.688 0.164 0.168 0.668
#&gt; SRR1383365     3  0.3482      0.821 0.128 0.000 0.872
#&gt; SRR1383366     3  0.3918      0.754 0.004 0.140 0.856
#&gt; SRR1383367     3  0.5397      0.588 0.000 0.280 0.720
#&gt; SRR1383368     2  0.8920      0.254 0.144 0.532 0.324
#&gt; SRR1383369     3  0.0983      0.819 0.016 0.004 0.980
#&gt; SRR1383370     3  0.0000      0.812 0.000 0.000 1.000
#&gt; SRR1383371     3  0.3551      0.819 0.132 0.000 0.868
#&gt; SRR1383372     2  0.5365      0.724 0.004 0.744 0.252
#&gt; SRR1383373     3  0.0000      0.812 0.000 0.000 1.000
#&gt; SRR1383374     3  0.3851      0.762 0.004 0.136 0.860
#&gt; SRR1383375     1  0.0592      0.737 0.988 0.012 0.000
#&gt; SRR1383376     2  0.2066      0.852 0.000 0.940 0.060
#&gt; SRR1383377     3  0.3715      0.822 0.128 0.004 0.868
#&gt; SRR1383378     2  0.5706      0.312 0.320 0.680 0.000
#&gt; SRR1383379     2  0.1529      0.797 0.040 0.960 0.000
#&gt; SRR1383380     1  0.6180      0.549 0.584 0.416 0.000
#&gt; SRR1383381     2  0.6902      0.712 0.168 0.732 0.100
#&gt; SRR1383382     1  0.0237      0.737 0.996 0.004 0.000
#&gt; SRR1383383     2  0.2200      0.853 0.004 0.940 0.056
#&gt; SRR1383385     1  0.0000      0.736 1.000 0.000 0.000
#&gt; SRR1383384     2  0.1964      0.853 0.000 0.944 0.056
#&gt; SRR1383386     1  0.6154      0.559 0.592 0.408 0.000
#&gt; SRR1383387     2  0.1964      0.853 0.000 0.944 0.056
#&gt; SRR1383389     2  0.7265      0.697 0.128 0.712 0.160
#&gt; SRR1383391     2  0.2703      0.850 0.016 0.928 0.056
#&gt; SRR1383388     1  0.6204      0.539 0.576 0.424 0.000
#&gt; SRR1383392     3  0.7508      0.204 0.040 0.416 0.544
#&gt; SRR1383390     2  0.2550      0.853 0.012 0.932 0.056
#&gt; SRR1383394     2  0.1964      0.853 0.000 0.944 0.056
#&gt; SRR1383393     1  0.0000      0.736 1.000 0.000 0.000
#&gt; SRR1383396     1  0.6274      0.416 0.544 0.456 0.000
#&gt; SRR1383395     3  0.3965      0.819 0.132 0.008 0.860
#&gt; SRR1383399     2  0.7180      0.697 0.168 0.716 0.116
#&gt; SRR1383400     1  0.0237      0.737 0.996 0.004 0.000
#&gt; SRR1383397     2  0.1832      0.807 0.036 0.956 0.008
#&gt; SRR1383401     2  0.5603      0.761 0.136 0.804 0.060
#&gt; SRR1383398     1  0.6180      0.549 0.584 0.416 0.000
#&gt; SRR1383402     2  0.2384      0.853 0.008 0.936 0.056
#&gt; SRR1383404     1  0.6215      0.531 0.572 0.428 0.000
#&gt; SRR1383403     1  0.0000      0.736 1.000 0.000 0.000
#&gt; SRR1383405     2  0.2200      0.852 0.004 0.940 0.056
#&gt; SRR1383406     2  0.3116      0.757 0.108 0.892 0.000
#&gt; SRR1383407     3  0.3551      0.819 0.132 0.000 0.868
#&gt; SRR1383408     2  0.1964      0.853 0.000 0.944 0.056
#&gt; SRR1383409     2  0.2200      0.853 0.004 0.940 0.056
#&gt; SRR1383410     2  0.5244      0.677 0.004 0.756 0.240
</code></pre>

<script>
$('#tab-ATC-mclust-get-classes-2-a').parent().next().next().hide();
$('#tab-ATC-mclust-get-classes-2-a').click(function(){
  $('#tab-ATC-mclust-get-classes-2-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-ATC-mclust-get-classes-3'>
<p><a id='tab-ATC-mclust-get-classes-3-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 4), get_membership(res, k = 4))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4
#&gt; SRR1383358     3  0.5459     0.0731 0.000 0.016 0.552 0.432
#&gt; SRR1383360     3  0.5167    -0.4092 0.000 0.004 0.508 0.488
#&gt; SRR1383359     4  0.0000     0.6268 0.000 0.000 0.000 1.000
#&gt; SRR1383362     1  0.0592     0.9480 0.984 0.000 0.016 0.000
#&gt; SRR1383361     4  0.4304     0.5359 0.000 0.000 0.284 0.716
#&gt; SRR1383363     3  0.5277     0.0179 0.000 0.008 0.532 0.460
#&gt; SRR1383364     4  0.4304     0.1370 0.000 0.000 0.284 0.716
#&gt; SRR1383365     4  0.1474     0.6340 0.000 0.000 0.052 0.948
#&gt; SRR1383366     3  0.5452    -0.1945 0.000 0.024 0.616 0.360
#&gt; SRR1383367     3  0.7013     0.2802 0.000 0.292 0.556 0.152
#&gt; SRR1383368     2  0.8057    -0.2691 0.032 0.464 0.356 0.148
#&gt; SRR1383369     4  0.4799     0.4865 0.004 0.008 0.284 0.704
#&gt; SRR1383370     4  0.4941     0.4034 0.000 0.000 0.436 0.564
#&gt; SRR1383371     4  0.0000     0.6268 0.000 0.000 0.000 1.000
#&gt; SRR1383372     3  0.6627     0.1539 0.000 0.348 0.556 0.096
#&gt; SRR1383373     4  0.3688     0.5655 0.000 0.000 0.208 0.792
#&gt; SRR1383374     3  0.5403    -0.1540 0.000 0.024 0.628 0.348
#&gt; SRR1383375     1  0.0707     0.9409 0.980 0.020 0.000 0.000
#&gt; SRR1383376     2  0.4761     0.5155 0.000 0.628 0.372 0.000
#&gt; SRR1383377     4  0.5452     0.3892 0.012 0.004 0.400 0.584
#&gt; SRR1383378     2  0.3266     0.3962 0.168 0.832 0.000 0.000
#&gt; SRR1383379     2  0.4382     0.1713 0.296 0.704 0.000 0.000
#&gt; SRR1383380     2  0.4976     0.0693 0.340 0.652 0.004 0.004
#&gt; SRR1383381     3  0.7846     0.1411 0.000 0.296 0.404 0.300
#&gt; SRR1383382     1  0.0592     0.9480 0.984 0.000 0.016 0.000
#&gt; SRR1383383     2  0.4730     0.5229 0.000 0.636 0.364 0.000
#&gt; SRR1383385     1  0.0895     0.9433 0.976 0.020 0.004 0.000
#&gt; SRR1383384     2  0.4761     0.5155 0.000 0.628 0.372 0.000
#&gt; SRR1383386     2  0.4933    -0.0986 0.432 0.568 0.000 0.000
#&gt; SRR1383387     2  0.4543     0.5360 0.000 0.676 0.324 0.000
#&gt; SRR1383389     2  0.7019     0.2405 0.004 0.512 0.376 0.108
#&gt; SRR1383391     2  0.5311     0.5340 0.024 0.648 0.328 0.000
#&gt; SRR1383388     2  0.4624     0.0853 0.340 0.660 0.000 0.000
#&gt; SRR1383392     3  0.6259    -0.0622 0.000 0.084 0.616 0.300
#&gt; SRR1383390     2  0.4730     0.5229 0.000 0.636 0.364 0.000
#&gt; SRR1383394     2  0.4543     0.5360 0.000 0.676 0.324 0.000
#&gt; SRR1383393     1  0.3933     0.7688 0.796 0.196 0.004 0.004
#&gt; SRR1383396     2  0.5511     0.1287 0.332 0.636 0.000 0.032
#&gt; SRR1383395     4  0.5500     0.3798 0.012 0.004 0.420 0.564
#&gt; SRR1383399     3  0.7846     0.1411 0.000 0.296 0.404 0.300
#&gt; SRR1383400     1  0.0592     0.9480 0.984 0.000 0.016 0.000
#&gt; SRR1383397     2  0.2796     0.4976 0.016 0.892 0.092 0.000
#&gt; SRR1383401     2  0.7810     0.1478 0.004 0.396 0.392 0.208
#&gt; SRR1383398     2  0.4976     0.0693 0.340 0.652 0.004 0.004
#&gt; SRR1383402     2  0.5110     0.5364 0.016 0.656 0.328 0.000
#&gt; SRR1383404     2  0.4855    -0.0205 0.400 0.600 0.000 0.000
#&gt; SRR1383403     1  0.0895     0.9433 0.976 0.020 0.004 0.000
#&gt; SRR1383405     2  0.4661     0.5257 0.000 0.652 0.348 0.000
#&gt; SRR1383406     2  0.1635     0.4750 0.044 0.948 0.008 0.000
#&gt; SRR1383407     4  0.0188     0.6286 0.000 0.000 0.004 0.996
#&gt; SRR1383408     2  0.4730     0.5229 0.000 0.636 0.364 0.000
#&gt; SRR1383409     2  0.5368     0.5295 0.024 0.636 0.340 0.000
#&gt; SRR1383410     2  0.6523     0.3604 0.000 0.628 0.236 0.136
</code></pre>

<script>
$('#tab-ATC-mclust-get-classes-3-a').parent().next().next().hide();
$('#tab-ATC-mclust-get-classes-3-a').click(function(){
  $('#tab-ATC-mclust-get-classes-3-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-ATC-mclust-get-classes-4'>
<p><a id='tab-ATC-mclust-get-classes-4-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 5), get_membership(res, k = 5))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4    p5
#&gt; SRR1383358     2  0.5760    -0.1720 0.000 0.472 0.456 0.008 0.064
#&gt; SRR1383360     3  0.3395     0.0861 0.000 0.000 0.764 0.000 0.236
#&gt; SRR1383359     5  0.3242     0.5964 0.000 0.000 0.216 0.000 0.784
#&gt; SRR1383362     1  0.0162     0.9567 0.996 0.000 0.000 0.004 0.000
#&gt; SRR1383361     3  0.2929     0.4144 0.000 0.000 0.820 0.000 0.180
#&gt; SRR1383363     3  0.5900     0.0778 0.000 0.448 0.468 0.008 0.076
#&gt; SRR1383364     5  0.5151     0.1465 0.000 0.436 0.020 0.012 0.532
#&gt; SRR1383365     5  0.1704     0.5078 0.000 0.004 0.068 0.000 0.928
#&gt; SRR1383366     3  0.3517     0.4652 0.000 0.072 0.840 0.004 0.084
#&gt; SRR1383367     2  0.5268    -0.1057 0.000 0.488 0.476 0.016 0.020
#&gt; SRR1383368     3  0.6530     0.1895 0.000 0.196 0.424 0.380 0.000
#&gt; SRR1383369     5  0.5377    -0.2314 0.000 0.044 0.456 0.004 0.496
#&gt; SRR1383370     3  0.2690     0.4351 0.000 0.000 0.844 0.000 0.156
#&gt; SRR1383371     5  0.3210     0.5954 0.000 0.000 0.212 0.000 0.788
#&gt; SRR1383372     2  0.5173    -0.0285 0.000 0.500 0.460 0.040 0.000
#&gt; SRR1383373     5  0.4497     0.3353 0.000 0.008 0.424 0.000 0.568
#&gt; SRR1383374     3  0.6323     0.3014 0.000 0.184 0.544 0.004 0.268
#&gt; SRR1383375     1  0.1502     0.9606 0.940 0.000 0.004 0.056 0.000
#&gt; SRR1383376     2  0.3395     0.6281 0.000 0.764 0.000 0.236 0.000
#&gt; SRR1383377     3  0.4282     0.3811 0.000 0.064 0.800 0.024 0.112
#&gt; SRR1383378     4  0.4640     0.7976 0.148 0.088 0.008 0.756 0.000
#&gt; SRR1383379     4  0.2193     0.6774 0.008 0.092 0.000 0.900 0.000
#&gt; SRR1383380     4  0.4230     0.7805 0.188 0.036 0.004 0.768 0.004
#&gt; SRR1383381     2  0.7050     0.0619 0.000 0.540 0.236 0.056 0.168
#&gt; SRR1383382     1  0.0162     0.9567 0.996 0.000 0.000 0.004 0.000
#&gt; SRR1383383     2  0.2773     0.5925 0.000 0.836 0.000 0.164 0.000
#&gt; SRR1383385     1  0.1430     0.9624 0.944 0.000 0.004 0.052 0.000
#&gt; SRR1383384     2  0.3366     0.6280 0.000 0.768 0.000 0.232 0.000
#&gt; SRR1383386     4  0.4245     0.7252 0.236 0.020 0.008 0.736 0.000
#&gt; SRR1383387     2  0.3534     0.6219 0.000 0.744 0.000 0.256 0.000
#&gt; SRR1383389     2  0.4989     0.2673 0.000 0.648 0.296 0.056 0.000
#&gt; SRR1383391     2  0.3684     0.6056 0.000 0.720 0.000 0.280 0.000
#&gt; SRR1383388     4  0.4479     0.7987 0.184 0.072 0.000 0.744 0.000
#&gt; SRR1383392     2  0.6969    -0.1536 0.000 0.392 0.344 0.008 0.256
#&gt; SRR1383390     2  0.3366     0.6067 0.000 0.768 0.000 0.232 0.000
#&gt; SRR1383394     2  0.3508     0.6233 0.000 0.748 0.000 0.252 0.000
#&gt; SRR1383393     1  0.2228     0.9301 0.900 0.004 0.004 0.092 0.000
#&gt; SRR1383396     4  0.4605     0.7917 0.176 0.048 0.020 0.756 0.000
#&gt; SRR1383395     3  0.4320     0.4009 0.000 0.076 0.804 0.032 0.088
#&gt; SRR1383399     2  0.7070     0.0539 0.000 0.536 0.240 0.056 0.168
#&gt; SRR1383400     1  0.0162     0.9567 0.996 0.000 0.000 0.004 0.000
#&gt; SRR1383397     4  0.4088     0.1866 0.000 0.368 0.000 0.632 0.000
#&gt; SRR1383401     2  0.4422     0.4341 0.000 0.792 0.024 0.080 0.104
#&gt; SRR1383398     4  0.4230     0.7805 0.188 0.036 0.004 0.768 0.004
#&gt; SRR1383402     2  0.3424     0.6261 0.000 0.760 0.000 0.240 0.000
#&gt; SRR1383404     4  0.4444     0.7935 0.184 0.052 0.008 0.756 0.000
#&gt; SRR1383403     1  0.1430     0.9624 0.944 0.000 0.004 0.052 0.000
#&gt; SRR1383405     2  0.3366     0.6280 0.000 0.768 0.000 0.232 0.000
#&gt; SRR1383406     4  0.2424     0.6524 0.000 0.132 0.000 0.868 0.000
#&gt; SRR1383407     5  0.3274     0.5945 0.000 0.000 0.220 0.000 0.780
#&gt; SRR1383408     2  0.3684     0.6056 0.000 0.720 0.000 0.280 0.000
#&gt; SRR1383409     2  0.3684     0.6056 0.000 0.720 0.000 0.280 0.000
#&gt; SRR1383410     2  0.7540     0.2999 0.000 0.508 0.132 0.128 0.232
</code></pre>

<script>
$('#tab-ATC-mclust-get-classes-4-a').parent().next().next().hide();
$('#tab-ATC-mclust-get-classes-4-a').click(function(){
  $('#tab-ATC-mclust-get-classes-4-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-ATC-mclust-get-classes-5'>
<p><a id='tab-ATC-mclust-get-classes-5-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 6), get_membership(res, k = 6))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4    p5    p6
#&gt; SRR1383358     3  0.5245     0.6909 0.000 0.072 0.576 0.000 0.016 0.336
#&gt; SRR1383360     6  0.2491     0.5861 0.000 0.000 0.000 0.000 0.164 0.836
#&gt; SRR1383359     5  0.2562     0.7427 0.000 0.000 0.000 0.000 0.828 0.172
#&gt; SRR1383362     1  0.1010     0.9026 0.960 0.000 0.036 0.004 0.000 0.000
#&gt; SRR1383361     6  0.2060     0.7077 0.000 0.000 0.016 0.000 0.084 0.900
#&gt; SRR1383363     3  0.5343     0.6765 0.000 0.060 0.568 0.000 0.028 0.344
#&gt; SRR1383364     5  0.3890     0.3179 0.004 0.000 0.400 0.000 0.596 0.000
#&gt; SRR1383365     5  0.2597     0.7413 0.000 0.000 0.000 0.000 0.824 0.176
#&gt; SRR1383366     6  0.1458     0.7380 0.000 0.016 0.020 0.000 0.016 0.948
#&gt; SRR1383367     3  0.5115     0.6936 0.000 0.084 0.572 0.000 0.004 0.340
#&gt; SRR1383368     3  0.7202     0.4876 0.004 0.052 0.392 0.212 0.012 0.328
#&gt; SRR1383369     5  0.4399     0.0756 0.000 0.004 0.028 0.000 0.616 0.352
#&gt; SRR1383370     6  0.1563     0.7287 0.000 0.000 0.012 0.000 0.056 0.932
#&gt; SRR1383371     5  0.2562     0.7427 0.000 0.000 0.000 0.000 0.828 0.172
#&gt; SRR1383372     3  0.5398     0.6919 0.004 0.100 0.556 0.000 0.004 0.336
#&gt; SRR1383373     5  0.3747     0.4779 0.000 0.000 0.000 0.000 0.604 0.396
#&gt; SRR1383374     6  0.4600     0.6017 0.000 0.060 0.032 0.000 0.184 0.724
#&gt; SRR1383375     1  0.2504     0.8864 0.856 0.000 0.004 0.136 0.000 0.004
#&gt; SRR1383376     2  0.0146     0.9599 0.000 0.996 0.004 0.000 0.000 0.000
#&gt; SRR1383377     6  0.2364     0.7103 0.004 0.000 0.072 0.000 0.032 0.892
#&gt; SRR1383378     4  0.0858     0.8959 0.000 0.028 0.004 0.968 0.000 0.000
#&gt; SRR1383379     4  0.2442     0.8246 0.000 0.144 0.004 0.852 0.000 0.000
#&gt; SRR1383380     4  0.0798     0.8899 0.004 0.004 0.012 0.976 0.000 0.004
#&gt; SRR1383381     3  0.1265     0.5723 0.000 0.000 0.948 0.000 0.008 0.044
#&gt; SRR1383382     1  0.1124     0.9033 0.956 0.000 0.036 0.008 0.000 0.000
#&gt; SRR1383383     2  0.0717     0.9542 0.000 0.976 0.016 0.008 0.000 0.000
#&gt; SRR1383385     1  0.1674     0.9123 0.924 0.000 0.004 0.068 0.000 0.004
#&gt; SRR1383384     2  0.0146     0.9599 0.000 0.996 0.004 0.000 0.000 0.000
#&gt; SRR1383386     4  0.0603     0.8957 0.000 0.016 0.004 0.980 0.000 0.000
#&gt; SRR1383387     2  0.0363     0.9573 0.000 0.988 0.000 0.012 0.000 0.000
#&gt; SRR1383389     3  0.5559     0.6739 0.004 0.148 0.596 0.000 0.008 0.244
#&gt; SRR1383391     2  0.0260     0.9607 0.000 0.992 0.000 0.008 0.000 0.000
#&gt; SRR1383388     4  0.0622     0.8950 0.000 0.012 0.008 0.980 0.000 0.000
#&gt; SRR1383392     6  0.5839     0.3998 0.000 0.284 0.008 0.000 0.184 0.524
#&gt; SRR1383390     2  0.0717     0.9542 0.000 0.976 0.016 0.008 0.000 0.000
#&gt; SRR1383394     2  0.0363     0.9573 0.000 0.988 0.000 0.012 0.000 0.000
#&gt; SRR1383393     1  0.3293     0.8192 0.788 0.000 0.008 0.196 0.004 0.004
#&gt; SRR1383396     4  0.3050     0.8069 0.096 0.016 0.028 0.856 0.004 0.000
#&gt; SRR1383395     6  0.2438     0.7129 0.004 0.008 0.076 0.000 0.020 0.892
#&gt; SRR1383399     3  0.1265     0.5723 0.000 0.000 0.948 0.000 0.008 0.044
#&gt; SRR1383400     1  0.1124     0.9033 0.956 0.000 0.036 0.008 0.000 0.000
#&gt; SRR1383397     4  0.3584     0.6115 0.004 0.308 0.000 0.688 0.000 0.000
#&gt; SRR1383401     3  0.4224     0.2977 0.000 0.384 0.600 0.004 0.008 0.004
#&gt; SRR1383398     4  0.0798     0.8899 0.004 0.004 0.012 0.976 0.000 0.004
#&gt; SRR1383402     2  0.1075     0.9274 0.000 0.952 0.000 0.048 0.000 0.000
#&gt; SRR1383404     4  0.0603     0.8957 0.000 0.016 0.004 0.980 0.000 0.000
#&gt; SRR1383403     1  0.1843     0.9107 0.912 0.000 0.004 0.080 0.000 0.004
#&gt; SRR1383405     2  0.0260     0.9605 0.000 0.992 0.000 0.008 0.000 0.000
#&gt; SRR1383406     4  0.2544     0.8283 0.004 0.140 0.000 0.852 0.000 0.004
#&gt; SRR1383407     5  0.2562     0.7427 0.000 0.000 0.000 0.000 0.828 0.172
#&gt; SRR1383408     2  0.0405     0.9603 0.000 0.988 0.004 0.008 0.000 0.000
#&gt; SRR1383409     2  0.0260     0.9607 0.000 0.992 0.000 0.008 0.000 0.000
#&gt; SRR1383410     2  0.4056     0.6918 0.000 0.748 0.000 0.004 0.184 0.064
</code></pre>

<script>
$('#tab-ATC-mclust-get-classes-5-a').parent().next().next().hide();
$('#tab-ATC-mclust-get-classes-5-a').click(function(){
  $('#tab-ATC-mclust-get-classes-5-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>
</div>

Heatmaps for the consensus matrix. It visualizes the probability of two
samples to be in a same group.



<script>
$( function() {
	$( '#tabs-ATC-mclust-consensus-heatmap' ).tabs();
} );
</script>
<div id='tabs-ATC-mclust-consensus-heatmap'>
<ul>
<li><a href='#tab-ATC-mclust-consensus-heatmap-1'>k = 2</a></li>
<li><a href='#tab-ATC-mclust-consensus-heatmap-2'>k = 3</a></li>
<li><a href='#tab-ATC-mclust-consensus-heatmap-3'>k = 4</a></li>
<li><a href='#tab-ATC-mclust-consensus-heatmap-4'>k = 5</a></li>
<li><a href='#tab-ATC-mclust-consensus-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-ATC-mclust-consensus-heatmap-1'>
<pre><code class="r">consensus_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-ATC-mclust-consensus-heatmap-1-1.png" alt="plot of chunk tab-ATC-mclust-consensus-heatmap-1"/></p>

</div>
<div id='tab-ATC-mclust-consensus-heatmap-2'>
<pre><code class="r">consensus_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-ATC-mclust-consensus-heatmap-2-1.png" alt="plot of chunk tab-ATC-mclust-consensus-heatmap-2"/></p>

</div>
<div id='tab-ATC-mclust-consensus-heatmap-3'>
<pre><code class="r">consensus_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-ATC-mclust-consensus-heatmap-3-1.png" alt="plot of chunk tab-ATC-mclust-consensus-heatmap-3"/></p>

</div>
<div id='tab-ATC-mclust-consensus-heatmap-4'>
<pre><code class="r">consensus_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-ATC-mclust-consensus-heatmap-4-1.png" alt="plot of chunk tab-ATC-mclust-consensus-heatmap-4"/></p>

</div>
<div id='tab-ATC-mclust-consensus-heatmap-5'>
<pre><code class="r">consensus_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-ATC-mclust-consensus-heatmap-5-1.png" alt="plot of chunk tab-ATC-mclust-consensus-heatmap-5"/></p>

</div>
</div>

Heatmaps for the membership of samples in all partitions to see how consistent they are:




<script>
$( function() {
	$( '#tabs-ATC-mclust-membership-heatmap' ).tabs();
} );
</script>
<div id='tabs-ATC-mclust-membership-heatmap'>
<ul>
<li><a href='#tab-ATC-mclust-membership-heatmap-1'>k = 2</a></li>
<li><a href='#tab-ATC-mclust-membership-heatmap-2'>k = 3</a></li>
<li><a href='#tab-ATC-mclust-membership-heatmap-3'>k = 4</a></li>
<li><a href='#tab-ATC-mclust-membership-heatmap-4'>k = 5</a></li>
<li><a href='#tab-ATC-mclust-membership-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-ATC-mclust-membership-heatmap-1'>
<pre><code class="r">membership_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-ATC-mclust-membership-heatmap-1-1.png" alt="plot of chunk tab-ATC-mclust-membership-heatmap-1"/></p>

</div>
<div id='tab-ATC-mclust-membership-heatmap-2'>
<pre><code class="r">membership_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-ATC-mclust-membership-heatmap-2-1.png" alt="plot of chunk tab-ATC-mclust-membership-heatmap-2"/></p>

</div>
<div id='tab-ATC-mclust-membership-heatmap-3'>
<pre><code class="r">membership_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-ATC-mclust-membership-heatmap-3-1.png" alt="plot of chunk tab-ATC-mclust-membership-heatmap-3"/></p>

</div>
<div id='tab-ATC-mclust-membership-heatmap-4'>
<pre><code class="r">membership_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-ATC-mclust-membership-heatmap-4-1.png" alt="plot of chunk tab-ATC-mclust-membership-heatmap-4"/></p>

</div>
<div id='tab-ATC-mclust-membership-heatmap-5'>
<pre><code class="r">membership_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-ATC-mclust-membership-heatmap-5-1.png" alt="plot of chunk tab-ATC-mclust-membership-heatmap-5"/></p>

</div>
</div>

As soon as we have had the classes for columns, we can look for signatures
which are significantly different between classes which can be candidate marks
for certain classes. Following are the heatmaps for signatures.



Signature heatmaps where rows are scaled:



<script>
$( function() {
	$( '#tabs-ATC-mclust-get-signatures' ).tabs();
} );
</script>
<div id='tabs-ATC-mclust-get-signatures'>
<ul>
<li><a href='#tab-ATC-mclust-get-signatures-1'>k = 2</a></li>
<li><a href='#tab-ATC-mclust-get-signatures-2'>k = 3</a></li>
<li><a href='#tab-ATC-mclust-get-signatures-3'>k = 4</a></li>
<li><a href='#tab-ATC-mclust-get-signatures-4'>k = 5</a></li>
<li><a href='#tab-ATC-mclust-get-signatures-5'>k = 6</a></li>
</ul>
<div id='tab-ATC-mclust-get-signatures-1'>
<pre><code class="r">get_signatures(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-ATC-mclust-get-signatures-1-1.png" alt="plot of chunk tab-ATC-mclust-get-signatures-1"/></p>

</div>
<div id='tab-ATC-mclust-get-signatures-2'>
<pre><code class="r">get_signatures(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-ATC-mclust-get-signatures-2-1.png" alt="plot of chunk tab-ATC-mclust-get-signatures-2"/></p>

</div>
<div id='tab-ATC-mclust-get-signatures-3'>
<pre><code class="r">get_signatures(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-ATC-mclust-get-signatures-3-1.png" alt="plot of chunk tab-ATC-mclust-get-signatures-3"/></p>

</div>
<div id='tab-ATC-mclust-get-signatures-4'>
<pre><code class="r">get_signatures(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-ATC-mclust-get-signatures-4-1.png" alt="plot of chunk tab-ATC-mclust-get-signatures-4"/></p>

</div>
<div id='tab-ATC-mclust-get-signatures-5'>
<pre><code class="r">get_signatures(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-ATC-mclust-get-signatures-5-1.png" alt="plot of chunk tab-ATC-mclust-get-signatures-5"/></p>

</div>
</div>



Signature heatmaps where rows are not scaled:


<script>
$( function() {
	$( '#tabs-ATC-mclust-get-signatures-no-scale' ).tabs();
} );
</script>
<div id='tabs-ATC-mclust-get-signatures-no-scale'>
<ul>
<li><a href='#tab-ATC-mclust-get-signatures-no-scale-1'>k = 2</a></li>
<li><a href='#tab-ATC-mclust-get-signatures-no-scale-2'>k = 3</a></li>
<li><a href='#tab-ATC-mclust-get-signatures-no-scale-3'>k = 4</a></li>
<li><a href='#tab-ATC-mclust-get-signatures-no-scale-4'>k = 5</a></li>
<li><a href='#tab-ATC-mclust-get-signatures-no-scale-5'>k = 6</a></li>
</ul>
<div id='tab-ATC-mclust-get-signatures-no-scale-1'>
<pre><code class="r">get_signatures(res, k = 2, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-ATC-mclust-get-signatures-no-scale-1-1.png" alt="plot of chunk tab-ATC-mclust-get-signatures-no-scale-1"/></p>

</div>
<div id='tab-ATC-mclust-get-signatures-no-scale-2'>
<pre><code class="r">get_signatures(res, k = 3, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-ATC-mclust-get-signatures-no-scale-2-1.png" alt="plot of chunk tab-ATC-mclust-get-signatures-no-scale-2"/></p>

</div>
<div id='tab-ATC-mclust-get-signatures-no-scale-3'>
<pre><code class="r">get_signatures(res, k = 4, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-ATC-mclust-get-signatures-no-scale-3-1.png" alt="plot of chunk tab-ATC-mclust-get-signatures-no-scale-3"/></p>

</div>
<div id='tab-ATC-mclust-get-signatures-no-scale-4'>
<pre><code class="r">get_signatures(res, k = 5, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-ATC-mclust-get-signatures-no-scale-4-1.png" alt="plot of chunk tab-ATC-mclust-get-signatures-no-scale-4"/></p>

</div>
<div id='tab-ATC-mclust-get-signatures-no-scale-5'>
<pre><code class="r">get_signatures(res, k = 6, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-ATC-mclust-get-signatures-no-scale-5-1.png" alt="plot of chunk tab-ATC-mclust-get-signatures-no-scale-5"/></p>

</div>
</div>



Compare the overlap of signatures from different k:

```r
compare_signatures(res)
```

![plot of chunk ATC-mclust-signature_compare](figure_cola/ATC-mclust-signature_compare-1.png)

`get_signature()` returns a data frame invisibly. TO get the list of signatures, the function
call should be assigned to a variable explicitly. In following code, if `plot` argument is set
to `FALSE`, no heatmap is plotted while only the differential analysis is performed.

```r
# code only for demonstration
tb = get_signature(res, k = ..., plot = FALSE)
```

An example of the output of `tb` is:

```
#>   which_row         fdr    mean_1    mean_2 scaled_mean_1 scaled_mean_2 km
#> 1        38 0.042760348  8.373488  9.131774    -0.5533452     0.5164555  1
#> 2        40 0.018707592  7.106213  8.469186    -0.6173731     0.5762149  1
#> 3        55 0.019134737 10.221463 11.207825    -0.6159697     0.5749050  1
#> 4        59 0.006059896  5.921854  7.869574    -0.6899429     0.6439467  1
#> 5        60 0.018055526  8.928898 10.211722    -0.6204761     0.5791110  1
#> 6        98 0.009384629 15.714769 14.887706     0.6635654    -0.6193277  2
...
```

The columns in `tb` are:

1. `which_row`: row indices corresponding to the input matrix.
2. `fdr`: FDR for the differential test. 
3. `mean_x`: The mean value in group x.
4. `scaled_mean_x`: The mean value in group x after rows are scaled.
5. `km`: Row groups if k-means clustering is applied to rows.



UMAP plot which shows how samples are separated.


<script>
$( function() {
	$( '#tabs-ATC-mclust-dimension-reduction' ).tabs();
} );
</script>
<div id='tabs-ATC-mclust-dimension-reduction'>
<ul>
<li><a href='#tab-ATC-mclust-dimension-reduction-1'>k = 2</a></li>
<li><a href='#tab-ATC-mclust-dimension-reduction-2'>k = 3</a></li>
<li><a href='#tab-ATC-mclust-dimension-reduction-3'>k = 4</a></li>
<li><a href='#tab-ATC-mclust-dimension-reduction-4'>k = 5</a></li>
<li><a href='#tab-ATC-mclust-dimension-reduction-5'>k = 6</a></li>
</ul>
<div id='tab-ATC-mclust-dimension-reduction-1'>
<pre><code class="r">dimension_reduction(res, k = 2, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-ATC-mclust-dimension-reduction-1-1.png" alt="plot of chunk tab-ATC-mclust-dimension-reduction-1"/></p>

</div>
<div id='tab-ATC-mclust-dimension-reduction-2'>
<pre><code class="r">dimension_reduction(res, k = 3, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-ATC-mclust-dimension-reduction-2-1.png" alt="plot of chunk tab-ATC-mclust-dimension-reduction-2"/></p>

</div>
<div id='tab-ATC-mclust-dimension-reduction-3'>
<pre><code class="r">dimension_reduction(res, k = 4, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-ATC-mclust-dimension-reduction-3-1.png" alt="plot of chunk tab-ATC-mclust-dimension-reduction-3"/></p>

</div>
<div id='tab-ATC-mclust-dimension-reduction-4'>
<pre><code class="r">dimension_reduction(res, k = 5, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-ATC-mclust-dimension-reduction-4-1.png" alt="plot of chunk tab-ATC-mclust-dimension-reduction-4"/></p>

</div>
<div id='tab-ATC-mclust-dimension-reduction-5'>
<pre><code class="r">dimension_reduction(res, k = 6, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-ATC-mclust-dimension-reduction-5-1.png" alt="plot of chunk tab-ATC-mclust-dimension-reduction-5"/></p>

</div>
</div>


Following heatmap shows how subgroups are split when increasing `k`:

```r
collect_classes(res)
```

![plot of chunk ATC-mclust-collect-classes](figure_cola/ATC-mclust-collect-classes-1.png)


If matrix rows can be associated to genes, consider to use `functional_enrichment(res,
...)` to perform function enrichment for the signature genes. See [this vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/functional_enrichment.html) for more detailed explanations.


 

---------------------------------------------------




### ATC:NMF**






The object with results only for a single top-value method and a single partition method 
can be extracted as:

```r
res = res_list["ATC", "NMF"]
# you can also extract it by
# res = res_list["ATC:NMF"]
```

A summary of `res` and all the functions that can be applied to it:

```r
res
```

```
#> A 'ConsensusPartition' object with k = 2, 3, 4, 5, 6.
#>   On a matrix with 15680 rows and 53 columns.
#>   Top rows (1000, 2000, 3000, 4000, 5000) are extracted by 'ATC' method.
#>   Subgroups are detected by 'NMF' method.
#>   Performed in total 1250 partitions by row resampling.
#>   Best k for subgroups seems to be 3.
#> 
#> Following methods can be applied to this 'ConsensusPartition' object:
#>  [1] "cola_report"             "collect_classes"         "collect_plots"          
#>  [4] "collect_stats"           "colnames"                "compare_signatures"     
#>  [7] "consensus_heatmap"       "dimension_reduction"     "functional_enrichment"  
#> [10] "get_anno_col"            "get_anno"                "get_classes"            
#> [13] "get_consensus"           "get_matrix"              "get_membership"         
#> [16] "get_param"               "get_signatures"          "get_stats"              
#> [19] "is_best_k"               "is_stable_k"             "membership_heatmap"     
#> [22] "ncol"                    "nrow"                    "plot_ecdf"              
#> [25] "rownames"                "select_partition_number" "show"                   
#> [28] "suggest_best_k"          "test_to_known_factors"
```

`collect_plots()` function collects all the plots made from `res` for all `k` (number of partitions)
into one single page to provide an easy and fast comparison between different `k`.

```r
collect_plots(res)
```

![plot of chunk ATC-NMF-collect-plots](figure_cola/ATC-NMF-collect-plots-1.png)

The plots are:

- The first row: a plot of the ECDF (empirical cumulative distribution
  function) curves of the consensus matrix for each `k` and the heatmap of
  predicted classes for each `k`.
- The second row: heatmaps of the consensus matrix for each `k`.
- The third row: heatmaps of the membership matrix for each `k`.
- The fouth row: heatmaps of the signatures for each `k`.

All the plots in panels can be made by individual functions and they are
plotted later in this section.

`select_partition_number()` produces several plots showing different
statistics for choosing "optimized" `k`. There are following statistics:

- ECDF curves of the consensus matrix for each `k`;
- 1-PAC. [The PAC
  score](https://en.wikipedia.org/wiki/Consensus_clustering#Over-interpretation_potential_of_consensus_clustering)
  measures the proportion of the ambiguous subgrouping.
- Mean silhouette score.
- Concordance. The mean probability of fiting the consensus class ids in all
  partitions.
- Area increased. Denote $A_k$ as the area under the ECDF curve for current
  `k`, the area increased is defined as $A_k - A_{k-1}$.
- Rand index. The percent of pairs of samples that are both in a same cluster
  or both are not in a same cluster in the partition of k and k-1.
- Jaccard index. The ratio of pairs of samples are both in a same cluster in
  the partition of k and k-1 and the pairs of samples are both in a same
  cluster in the partition k or k-1.

The detailed explanations of these statistics can be found in [the _cola_
vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/cola.html#toc_13).

Generally speaking, lower PAC score, higher mean silhouette score or higher
concordance corresponds to better partition. Rand index and Jaccard index
measure how similar the current partition is compared to partition with `k-1`.
If they are too similar, we won't accept `k` is better than `k-1`.

```r
select_partition_number(res)
```

![plot of chunk ATC-NMF-select-partition-number](figure_cola/ATC-NMF-select-partition-number-1.png)

The numeric values for all these statistics can be obtained by `get_stats()`.

```r
get_stats(res)
```

```
#>   k 1-PAC mean_silhouette concordance area_increased  Rand Jaccard
#> 2 2 0.882           0.906       0.965         0.3276 0.688   0.688
#> 3 3 0.963           0.946       0.978         0.7909 0.627   0.492
#> 4 4 0.503           0.619       0.811         0.1690 0.713   0.427
#> 5 5 0.539           0.547       0.762         0.0961 0.797   0.464
#> 6 6 0.564           0.515       0.728         0.0394 0.893   0.639
```

`suggest_best_k()` suggests the best $k$ based on these statistics. The rules are as follows:

- All $k$ with Jaccard index larger than 0.95 are removed because increasing
  $k$ does not provide enough extra information. If all $k$ are removed, it is
  marked as no subgroup is detected.
- For all $k$ with 1-PAC score larger than 0.9, the maximal $k$ is taken as
  the best $k$, and other $k$ are marked as optional $k$.
- If it does not fit the second rule. The $k$ with the maximal vote of the
  highest 1-PAC score, highest mean silhouette, and highest concordance is
  taken as the best $k$.

```r
suggest_best_k(res)
```

```
#> [1] 3
```


Following shows the table of the partitions (You need to click the **show/hide
code output** link to see it). The membership matrix (columns with name `p*`)
is inferred by
[`clue::cl_consensus()`](https://www.rdocumentation.org/link/cl_consensus?package=clue)
function with the `SE` method. Basically the value in the membership matrix
represents the probability to belong to a certain group. The finall class
label for an item is determined with the group with highest probability it
belongs to.

In `get_classes()` function, the entropy is calculated from the membership
matrix and the silhouette score is calculated from the consensus matrix.



<script>
$( function() {
	$( '#tabs-ATC-NMF-get-classes' ).tabs();
} );
</script>
<div id='tabs-ATC-NMF-get-classes'>
<ul>
<li><a href='#tab-ATC-NMF-get-classes-1'>k = 2</a></li>
<li><a href='#tab-ATC-NMF-get-classes-2'>k = 3</a></li>
<li><a href='#tab-ATC-NMF-get-classes-3'>k = 4</a></li>
<li><a href='#tab-ATC-NMF-get-classes-4'>k = 5</a></li>
<li><a href='#tab-ATC-NMF-get-classes-5'>k = 6</a></li>
</ul>

<div id='tab-ATC-NMF-get-classes-1'>
<p><a id='tab-ATC-NMF-get-classes-1-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 2), get_membership(res, k = 2))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2
#&gt; SRR1383358     2  0.0000     0.9656 0.000 1.000
#&gt; SRR1383360     2  0.0000     0.9656 0.000 1.000
#&gt; SRR1383359     2  0.0000     0.9656 0.000 1.000
#&gt; SRR1383362     1  0.0000     0.9346 1.000 0.000
#&gt; SRR1383361     2  0.0000     0.9656 0.000 1.000
#&gt; SRR1383363     2  0.0000     0.9656 0.000 1.000
#&gt; SRR1383364     2  0.0672     0.9589 0.008 0.992
#&gt; SRR1383365     2  0.0000     0.9656 0.000 1.000
#&gt; SRR1383366     2  0.0000     0.9656 0.000 1.000
#&gt; SRR1383367     2  0.0000     0.9656 0.000 1.000
#&gt; SRR1383368     2  0.2948     0.9175 0.052 0.948
#&gt; SRR1383369     2  0.0000     0.9656 0.000 1.000
#&gt; SRR1383370     2  0.0000     0.9656 0.000 1.000
#&gt; SRR1383371     2  0.0000     0.9656 0.000 1.000
#&gt; SRR1383372     2  0.0000     0.9656 0.000 1.000
#&gt; SRR1383373     2  0.0000     0.9656 0.000 1.000
#&gt; SRR1383374     2  0.0000     0.9656 0.000 1.000
#&gt; SRR1383375     1  0.0000     0.9346 1.000 0.000
#&gt; SRR1383376     2  0.0000     0.9656 0.000 1.000
#&gt; SRR1383377     2  0.0000     0.9656 0.000 1.000
#&gt; SRR1383378     2  0.5629     0.8237 0.132 0.868
#&gt; SRR1383379     2  0.0000     0.9656 0.000 1.000
#&gt; SRR1383380     1  0.9732     0.2946 0.596 0.404
#&gt; SRR1383381     2  0.0000     0.9656 0.000 1.000
#&gt; SRR1383382     1  0.0000     0.9346 1.000 0.000
#&gt; SRR1383383     2  0.0000     0.9656 0.000 1.000
#&gt; SRR1383385     1  0.0000     0.9346 1.000 0.000
#&gt; SRR1383384     2  0.0000     0.9656 0.000 1.000
#&gt; SRR1383386     1  0.0376     0.9324 0.996 0.004
#&gt; SRR1383387     2  0.0000     0.9656 0.000 1.000
#&gt; SRR1383389     2  0.0000     0.9656 0.000 1.000
#&gt; SRR1383391     2  0.0000     0.9656 0.000 1.000
#&gt; SRR1383388     2  0.9393     0.4231 0.356 0.644
#&gt; SRR1383392     2  0.0000     0.9656 0.000 1.000
#&gt; SRR1383390     2  0.0000     0.9656 0.000 1.000
#&gt; SRR1383394     2  0.0000     0.9656 0.000 1.000
#&gt; SRR1383393     1  0.0000     0.9346 1.000 0.000
#&gt; SRR1383396     1  0.5842     0.8070 0.860 0.140
#&gt; SRR1383395     2  0.0000     0.9656 0.000 1.000
#&gt; SRR1383399     2  0.0000     0.9656 0.000 1.000
#&gt; SRR1383400     1  0.0000     0.9346 1.000 0.000
#&gt; SRR1383397     2  0.0000     0.9656 0.000 1.000
#&gt; SRR1383401     2  0.0000     0.9656 0.000 1.000
#&gt; SRR1383398     2  0.9970     0.0745 0.468 0.532
#&gt; SRR1383402     2  0.0000     0.9656 0.000 1.000
#&gt; SRR1383404     2  0.8955     0.5253 0.312 0.688
#&gt; SRR1383403     1  0.0000     0.9346 1.000 0.000
#&gt; SRR1383405     2  0.0000     0.9656 0.000 1.000
#&gt; SRR1383406     2  0.0000     0.9656 0.000 1.000
#&gt; SRR1383407     2  0.0000     0.9656 0.000 1.000
#&gt; SRR1383408     2  0.0000     0.9656 0.000 1.000
#&gt; SRR1383409     2  0.0000     0.9656 0.000 1.000
#&gt; SRR1383410     2  0.0000     0.9656 0.000 1.000
</code></pre>

<script>
$('#tab-ATC-NMF-get-classes-1-a').parent().next().next().hide();
$('#tab-ATC-NMF-get-classes-1-a').click(function(){
  $('#tab-ATC-NMF-get-classes-1-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-ATC-NMF-get-classes-2'>
<p><a id='tab-ATC-NMF-get-classes-2-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 3), get_membership(res, k = 3))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3
#&gt; SRR1383358     3  0.5216      0.607 0.000 0.260 0.740
#&gt; SRR1383360     3  0.0000      0.957 0.000 0.000 1.000
#&gt; SRR1383359     3  0.0000      0.957 0.000 0.000 1.000
#&gt; SRR1383362     1  0.0000      0.946 1.000 0.000 0.000
#&gt; SRR1383361     3  0.0000      0.957 0.000 0.000 1.000
#&gt; SRR1383363     3  0.0000      0.957 0.000 0.000 1.000
#&gt; SRR1383364     3  0.0000      0.957 0.000 0.000 1.000
#&gt; SRR1383365     3  0.0000      0.957 0.000 0.000 1.000
#&gt; SRR1383366     2  0.2878      0.891 0.000 0.904 0.096
#&gt; SRR1383367     2  0.1529      0.951 0.000 0.960 0.040
#&gt; SRR1383368     1  0.2998      0.878 0.916 0.068 0.016
#&gt; SRR1383369     3  0.0000      0.957 0.000 0.000 1.000
#&gt; SRR1383370     3  0.0000      0.957 0.000 0.000 1.000
#&gt; SRR1383371     3  0.0000      0.957 0.000 0.000 1.000
#&gt; SRR1383372     2  0.0000      0.984 0.000 1.000 0.000
#&gt; SRR1383373     3  0.0000      0.957 0.000 0.000 1.000
#&gt; SRR1383374     2  0.0237      0.981 0.000 0.996 0.004
#&gt; SRR1383375     1  0.0000      0.946 1.000 0.000 0.000
#&gt; SRR1383376     2  0.0000      0.984 0.000 1.000 0.000
#&gt; SRR1383377     3  0.0000      0.957 0.000 0.000 1.000
#&gt; SRR1383378     2  0.0000      0.984 0.000 1.000 0.000
#&gt; SRR1383379     2  0.0000      0.984 0.000 1.000 0.000
#&gt; SRR1383380     2  0.0592      0.975 0.012 0.988 0.000
#&gt; SRR1383381     2  0.0747      0.972 0.000 0.984 0.016
#&gt; SRR1383382     1  0.0000      0.946 1.000 0.000 0.000
#&gt; SRR1383383     2  0.0000      0.984 0.000 1.000 0.000
#&gt; SRR1383385     1  0.0000      0.946 1.000 0.000 0.000
#&gt; SRR1383384     2  0.0000      0.984 0.000 1.000 0.000
#&gt; SRR1383386     2  0.1964      0.935 0.056 0.944 0.000
#&gt; SRR1383387     2  0.0000      0.984 0.000 1.000 0.000
#&gt; SRR1383389     2  0.0424      0.979 0.000 0.992 0.008
#&gt; SRR1383391     2  0.0000      0.984 0.000 1.000 0.000
#&gt; SRR1383388     2  0.0000      0.984 0.000 1.000 0.000
#&gt; SRR1383392     2  0.0000      0.984 0.000 1.000 0.000
#&gt; SRR1383390     2  0.0000      0.984 0.000 1.000 0.000
#&gt; SRR1383394     2  0.0000      0.984 0.000 1.000 0.000
#&gt; SRR1383393     1  0.0000      0.946 1.000 0.000 0.000
#&gt; SRR1383396     1  0.5098      0.662 0.752 0.248 0.000
#&gt; SRR1383395     3  0.3619      0.794 0.000 0.136 0.864
#&gt; SRR1383399     2  0.4555      0.752 0.000 0.800 0.200
#&gt; SRR1383400     1  0.0000      0.946 1.000 0.000 0.000
#&gt; SRR1383397     2  0.0000      0.984 0.000 1.000 0.000
#&gt; SRR1383401     2  0.0000      0.984 0.000 1.000 0.000
#&gt; SRR1383398     2  0.0000      0.984 0.000 1.000 0.000
#&gt; SRR1383402     2  0.0000      0.984 0.000 1.000 0.000
#&gt; SRR1383404     2  0.0000      0.984 0.000 1.000 0.000
#&gt; SRR1383403     1  0.0000      0.946 1.000 0.000 0.000
#&gt; SRR1383405     2  0.0000      0.984 0.000 1.000 0.000
#&gt; SRR1383406     2  0.0000      0.984 0.000 1.000 0.000
#&gt; SRR1383407     3  0.0000      0.957 0.000 0.000 1.000
#&gt; SRR1383408     2  0.0000      0.984 0.000 1.000 0.000
#&gt; SRR1383409     2  0.0000      0.984 0.000 1.000 0.000
#&gt; SRR1383410     2  0.0000      0.984 0.000 1.000 0.000
</code></pre>

<script>
$('#tab-ATC-NMF-get-classes-2-a').parent().next().next().hide();
$('#tab-ATC-NMF-get-classes-2-a').click(function(){
  $('#tab-ATC-NMF-get-classes-2-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-ATC-NMF-get-classes-3'>
<p><a id='tab-ATC-NMF-get-classes-3-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 4), get_membership(res, k = 4))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4
#&gt; SRR1383358     3  0.5628     0.2382 0.000 0.420 0.556 0.024
#&gt; SRR1383360     3  0.5520     0.6195 0.000 0.244 0.696 0.060
#&gt; SRR1383359     3  0.0592     0.7369 0.000 0.000 0.984 0.016
#&gt; SRR1383362     1  0.0000     0.7794 1.000 0.000 0.000 0.000
#&gt; SRR1383361     2  0.5793     0.1948 0.000 0.580 0.384 0.036
#&gt; SRR1383363     2  0.4839     0.5748 0.000 0.756 0.200 0.044
#&gt; SRR1383364     3  0.1022     0.7308 0.000 0.000 0.968 0.032
#&gt; SRR1383365     3  0.0592     0.7369 0.000 0.000 0.984 0.016
#&gt; SRR1383366     2  0.3706     0.6923 0.000 0.848 0.112 0.040
#&gt; SRR1383367     2  0.0672     0.7912 0.000 0.984 0.008 0.008
#&gt; SRR1383368     1  0.5839     0.3691 0.636 0.324 0.020 0.020
#&gt; SRR1383369     2  0.5658     0.3422 0.000 0.632 0.328 0.040
#&gt; SRR1383370     2  0.5935    -0.0903 0.000 0.496 0.468 0.036
#&gt; SRR1383371     3  0.0336     0.7394 0.000 0.000 0.992 0.008
#&gt; SRR1383372     2  0.0707     0.7949 0.000 0.980 0.000 0.020
#&gt; SRR1383373     3  0.2965     0.7278 0.000 0.072 0.892 0.036
#&gt; SRR1383374     2  0.1798     0.7739 0.000 0.944 0.016 0.040
#&gt; SRR1383375     4  0.4222     0.3860 0.272 0.000 0.000 0.728
#&gt; SRR1383376     2  0.1211     0.7974 0.000 0.960 0.000 0.040
#&gt; SRR1383377     2  0.6764     0.2942 0.000 0.596 0.260 0.144
#&gt; SRR1383378     2  0.4585     0.3716 0.000 0.668 0.000 0.332
#&gt; SRR1383379     4  0.4830     0.5103 0.000 0.392 0.000 0.608
#&gt; SRR1383380     4  0.2271     0.6719 0.008 0.076 0.000 0.916
#&gt; SRR1383381     4  0.6934     0.4720 0.000 0.164 0.256 0.580
#&gt; SRR1383382     1  0.0000     0.7794 1.000 0.000 0.000 0.000
#&gt; SRR1383383     2  0.1637     0.7943 0.000 0.940 0.000 0.060
#&gt; SRR1383385     1  0.3610     0.6956 0.800 0.000 0.000 0.200
#&gt; SRR1383384     2  0.1211     0.7974 0.000 0.960 0.000 0.040
#&gt; SRR1383386     4  0.7442     0.4207 0.340 0.184 0.000 0.476
#&gt; SRR1383387     2  0.1867     0.7887 0.000 0.928 0.000 0.072
#&gt; SRR1383389     2  0.2335     0.7737 0.000 0.920 0.020 0.060
#&gt; SRR1383391     2  0.2760     0.7452 0.000 0.872 0.000 0.128
#&gt; SRR1383388     4  0.3764     0.6875 0.000 0.216 0.000 0.784
#&gt; SRR1383392     2  0.1798     0.7749 0.000 0.944 0.016 0.040
#&gt; SRR1383390     2  0.1474     0.7966 0.000 0.948 0.000 0.052
#&gt; SRR1383394     2  0.2589     0.7562 0.000 0.884 0.000 0.116
#&gt; SRR1383393     1  0.4500     0.5678 0.684 0.000 0.000 0.316
#&gt; SRR1383396     1  0.3591     0.6783 0.824 0.008 0.000 0.168
#&gt; SRR1383395     3  0.7332     0.3813 0.000 0.356 0.480 0.164
#&gt; SRR1383399     3  0.6407     0.4141 0.000 0.204 0.648 0.148
#&gt; SRR1383400     1  0.0000     0.7794 1.000 0.000 0.000 0.000
#&gt; SRR1383397     4  0.3837     0.6867 0.000 0.224 0.000 0.776
#&gt; SRR1383401     2  0.3123     0.7293 0.000 0.844 0.000 0.156
#&gt; SRR1383398     4  0.2197     0.6747 0.004 0.080 0.000 0.916
#&gt; SRR1383402     2  0.4072     0.5648 0.000 0.748 0.000 0.252
#&gt; SRR1383404     4  0.4866     0.4767 0.000 0.404 0.000 0.596
#&gt; SRR1383403     4  0.4356     0.2593 0.292 0.000 0.000 0.708
#&gt; SRR1383405     2  0.1716     0.7941 0.000 0.936 0.000 0.064
#&gt; SRR1383406     4  0.2281     0.6816 0.000 0.096 0.000 0.904
#&gt; SRR1383407     3  0.2319     0.7304 0.000 0.040 0.924 0.036
#&gt; SRR1383408     2  0.1474     0.7966 0.000 0.948 0.000 0.052
#&gt; SRR1383409     2  0.3024     0.7243 0.000 0.852 0.000 0.148
#&gt; SRR1383410     2  0.1302     0.7974 0.000 0.956 0.000 0.044
</code></pre>

<script>
$('#tab-ATC-NMF-get-classes-3-a').parent().next().next().hide();
$('#tab-ATC-NMF-get-classes-3-a').click(function(){
  $('#tab-ATC-NMF-get-classes-3-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-ATC-NMF-get-classes-4'>
<p><a id='tab-ATC-NMF-get-classes-4-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 5), get_membership(res, k = 5))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4    p5
#&gt; SRR1383358     5  0.5702     0.2432 0.000 0.320 0.104 0.000 0.576
#&gt; SRR1383360     3  0.3244     0.5343 0.008 0.048 0.860 0.000 0.084
#&gt; SRR1383359     5  0.3487     0.5953 0.000 0.000 0.212 0.008 0.780
#&gt; SRR1383362     1  0.0162     0.8128 0.996 0.000 0.004 0.000 0.000
#&gt; SRR1383361     3  0.4496     0.6232 0.000 0.216 0.728 0.000 0.056
#&gt; SRR1383363     3  0.6326     0.4144 0.000 0.380 0.460 0.000 0.160
#&gt; SRR1383364     5  0.1121     0.6212 0.000 0.000 0.044 0.000 0.956
#&gt; SRR1383365     5  0.3519     0.5943 0.000 0.000 0.216 0.008 0.776
#&gt; SRR1383366     3  0.4302     0.1444 0.000 0.480 0.520 0.000 0.000
#&gt; SRR1383367     2  0.3333     0.6126 0.000 0.788 0.208 0.000 0.004
#&gt; SRR1383368     1  0.4219     0.6196 0.772 0.156 0.072 0.000 0.000
#&gt; SRR1383369     3  0.6748     0.4424 0.000 0.320 0.404 0.000 0.276
#&gt; SRR1383370     3  0.4618     0.6237 0.000 0.208 0.724 0.000 0.068
#&gt; SRR1383371     5  0.3966     0.3659 0.000 0.000 0.336 0.000 0.664
#&gt; SRR1383372     2  0.3300     0.6168 0.000 0.792 0.204 0.000 0.004
#&gt; SRR1383373     3  0.4746     0.1560 0.000 0.024 0.600 0.000 0.376
#&gt; SRR1383374     2  0.4434    -0.0479 0.000 0.536 0.460 0.000 0.004
#&gt; SRR1383375     4  0.1704     0.7537 0.068 0.000 0.000 0.928 0.004
#&gt; SRR1383376     2  0.2424     0.6837 0.000 0.868 0.132 0.000 0.000
#&gt; SRR1383377     3  0.3778     0.5862 0.000 0.124 0.824 0.024 0.028
#&gt; SRR1383378     2  0.4792     0.6287 0.004 0.752 0.020 0.172 0.052
#&gt; SRR1383379     2  0.4481     0.3199 0.000 0.576 0.008 0.416 0.000
#&gt; SRR1383380     4  0.0566     0.7699 0.000 0.012 0.004 0.984 0.000
#&gt; SRR1383381     5  0.5510     0.5078 0.000 0.196 0.056 0.052 0.696
#&gt; SRR1383382     1  0.0000     0.8144 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1383383     2  0.2502     0.7101 0.000 0.904 0.024 0.012 0.060
#&gt; SRR1383385     4  0.4480     0.3417 0.400 0.000 0.004 0.592 0.004
#&gt; SRR1383384     2  0.1410     0.7127 0.000 0.940 0.060 0.000 0.000
#&gt; SRR1383386     2  0.6283     0.3320 0.280 0.556 0.008 0.156 0.000
#&gt; SRR1383387     2  0.2777     0.6987 0.000 0.864 0.120 0.016 0.000
#&gt; SRR1383389     2  0.5812    -0.0202 0.000 0.476 0.432 0.000 0.092
#&gt; SRR1383391     2  0.2243     0.7219 0.000 0.916 0.016 0.056 0.012
#&gt; SRR1383388     4  0.4490     0.1816 0.000 0.404 0.004 0.588 0.004
#&gt; SRR1383392     2  0.4235     0.1131 0.000 0.576 0.424 0.000 0.000
#&gt; SRR1383390     2  0.2300     0.7115 0.000 0.908 0.052 0.000 0.040
#&gt; SRR1383394     2  0.1965     0.7222 0.000 0.924 0.052 0.024 0.000
#&gt; SRR1383393     4  0.4491     0.4496 0.336 0.000 0.012 0.648 0.004
#&gt; SRR1383396     1  0.7840     0.4906 0.556 0.056 0.120 0.184 0.084
#&gt; SRR1383395     3  0.5021     0.4543 0.000 0.084 0.728 0.172 0.016
#&gt; SRR1383399     5  0.5028     0.5197 0.000 0.212 0.068 0.012 0.708
#&gt; SRR1383400     1  0.0000     0.8144 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1383397     4  0.1965     0.7146 0.000 0.096 0.000 0.904 0.000
#&gt; SRR1383401     2  0.4402     0.6452 0.000 0.780 0.020 0.052 0.148
#&gt; SRR1383398     4  0.0566     0.7699 0.000 0.012 0.004 0.984 0.000
#&gt; SRR1383402     2  0.2899     0.7023 0.000 0.872 0.008 0.100 0.020
#&gt; SRR1383404     2  0.4060     0.6134 0.004 0.760 0.012 0.216 0.008
#&gt; SRR1383403     4  0.1697     0.7541 0.060 0.000 0.008 0.932 0.000
#&gt; SRR1383405     2  0.3795     0.6674 0.000 0.788 0.184 0.024 0.004
#&gt; SRR1383406     4  0.0703     0.7663 0.000 0.024 0.000 0.976 0.000
#&gt; SRR1383407     3  0.3715     0.3007 0.000 0.004 0.736 0.000 0.260
#&gt; SRR1383408     2  0.1173     0.7218 0.000 0.964 0.020 0.004 0.012
#&gt; SRR1383409     2  0.2238     0.7171 0.000 0.912 0.004 0.064 0.020
#&gt; SRR1383410     2  0.3003     0.6393 0.000 0.812 0.188 0.000 0.000
</code></pre>

<script>
$('#tab-ATC-NMF-get-classes-4-a').parent().next().next().hide();
$('#tab-ATC-NMF-get-classes-4-a').click(function(){
  $('#tab-ATC-NMF-get-classes-4-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-ATC-NMF-get-classes-5'>
<p><a id='tab-ATC-NMF-get-classes-5-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 6), get_membership(res, k = 6))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4    p5    p6
#&gt; SRR1383358     4  0.6359     0.1547 0.000 0.232 0.240 0.496 0.032 0.000
#&gt; SRR1383360     3  0.3254     0.4326 0.008 0.016 0.856 0.088 0.020 0.012
#&gt; SRR1383359     4  0.0363     0.5479 0.000 0.000 0.012 0.988 0.000 0.000
#&gt; SRR1383362     6  0.0146     0.7775 0.000 0.000 0.000 0.000 0.004 0.996
#&gt; SRR1383361     3  0.3233     0.4793 0.000 0.104 0.832 0.060 0.004 0.000
#&gt; SRR1383363     3  0.5591     0.4375 0.000 0.220 0.632 0.052 0.096 0.000
#&gt; SRR1383364     4  0.3672     0.3071 0.000 0.000 0.008 0.688 0.304 0.000
#&gt; SRR1383365     4  0.1910     0.5789 0.000 0.000 0.108 0.892 0.000 0.000
#&gt; SRR1383366     3  0.4850     0.1369 0.000 0.448 0.496 0.000 0.056 0.000
#&gt; SRR1383367     2  0.5103     0.2709 0.000 0.576 0.336 0.004 0.084 0.000
#&gt; SRR1383368     6  0.6059     0.2785 0.000 0.124 0.248 0.000 0.056 0.572
#&gt; SRR1383369     3  0.5345     0.4434 0.000 0.232 0.648 0.060 0.060 0.000
#&gt; SRR1383370     3  0.3746     0.4393 0.000 0.080 0.780 0.140 0.000 0.000
#&gt; SRR1383371     3  0.6020    -0.1950 0.000 0.000 0.408 0.248 0.344 0.000
#&gt; SRR1383372     2  0.5023     0.3211 0.000 0.600 0.312 0.004 0.084 0.000
#&gt; SRR1383373     3  0.3563     0.2320 0.000 0.000 0.664 0.336 0.000 0.000
#&gt; SRR1383374     3  0.5013     0.1914 0.000 0.428 0.508 0.004 0.060 0.000
#&gt; SRR1383375     1  0.2507     0.7987 0.888 0.004 0.000 0.004 0.032 0.072
#&gt; SRR1383376     2  0.3142     0.6888 0.008 0.840 0.108 0.000 0.044 0.000
#&gt; SRR1383377     3  0.4150     0.3244 0.016 0.028 0.720 0.000 0.236 0.000
#&gt; SRR1383378     2  0.4732     0.4795 0.084 0.664 0.004 0.000 0.248 0.000
#&gt; SRR1383379     2  0.4692     0.5841 0.268 0.668 0.040 0.000 0.024 0.000
#&gt; SRR1383380     1  0.0146     0.8127 0.996 0.004 0.000 0.000 0.000 0.000
#&gt; SRR1383381     5  0.5093     0.6879 0.020 0.124 0.012 0.140 0.704 0.000
#&gt; SRR1383382     6  0.0000     0.7779 0.000 0.000 0.000 0.000 0.000 1.000
#&gt; SRR1383383     2  0.3519     0.5769 0.004 0.744 0.004 0.004 0.244 0.000
#&gt; SRR1383385     1  0.3076     0.6847 0.760 0.000 0.000 0.000 0.000 0.240
#&gt; SRR1383384     2  0.2398     0.7089 0.004 0.888 0.088 0.004 0.016 0.000
#&gt; SRR1383386     2  0.5478     0.4048 0.040 0.600 0.008 0.000 0.048 0.304
#&gt; SRR1383387     2  0.2956     0.7065 0.016 0.856 0.100 0.000 0.028 0.000
#&gt; SRR1383389     3  0.5675    -0.0452 0.000 0.168 0.488 0.000 0.344 0.000
#&gt; SRR1383391     2  0.2274     0.7214 0.008 0.892 0.012 0.000 0.088 0.000
#&gt; SRR1383388     2  0.4888     0.3468 0.380 0.560 0.000 0.004 0.056 0.000
#&gt; SRR1383392     3  0.4899     0.2521 0.000 0.404 0.532 0.000 0.064 0.000
#&gt; SRR1383390     2  0.2416     0.6728 0.000 0.844 0.000 0.000 0.156 0.000
#&gt; SRR1383394     2  0.2556     0.7188 0.028 0.884 0.076 0.000 0.012 0.000
#&gt; SRR1383393     1  0.3265     0.6722 0.748 0.000 0.000 0.000 0.004 0.248
#&gt; SRR1383396     5  0.7646     0.4342 0.116 0.092 0.124 0.000 0.504 0.164
#&gt; SRR1383395     3  0.4934     0.3438 0.116 0.012 0.728 0.028 0.116 0.000
#&gt; SRR1383399     5  0.4817     0.6830 0.008 0.104 0.016 0.152 0.720 0.000
#&gt; SRR1383400     6  0.0146     0.7770 0.000 0.000 0.000 0.000 0.004 0.996
#&gt; SRR1383397     1  0.3970     0.4366 0.692 0.280 0.000 0.000 0.028 0.000
#&gt; SRR1383401     2  0.4072     0.4863 0.008 0.688 0.004 0.012 0.288 0.000
#&gt; SRR1383398     1  0.0146     0.8127 0.996 0.004 0.000 0.000 0.000 0.000
#&gt; SRR1383402     2  0.2067     0.7247 0.028 0.916 0.004 0.004 0.048 0.000
#&gt; SRR1383404     2  0.3975     0.6589 0.136 0.788 0.012 0.000 0.056 0.008
#&gt; SRR1383403     1  0.1152     0.8129 0.952 0.000 0.000 0.000 0.004 0.044
#&gt; SRR1383405     2  0.4249     0.6812 0.048 0.776 0.116 0.000 0.060 0.000
#&gt; SRR1383406     1  0.1769     0.7774 0.924 0.060 0.004 0.000 0.012 0.000
#&gt; SRR1383407     3  0.4991     0.2265 0.000 0.008 0.648 0.100 0.244 0.000
#&gt; SRR1383408     2  0.1644     0.7306 0.000 0.932 0.028 0.000 0.040 0.000
#&gt; SRR1383409     2  0.1738     0.7225 0.016 0.928 0.000 0.004 0.052 0.000
#&gt; SRR1383410     2  0.4067     0.5985 0.004 0.752 0.172 0.000 0.072 0.000
</code></pre>

<script>
$('#tab-ATC-NMF-get-classes-5-a').parent().next().next().hide();
$('#tab-ATC-NMF-get-classes-5-a').click(function(){
  $('#tab-ATC-NMF-get-classes-5-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>
</div>

Heatmaps for the consensus matrix. It visualizes the probability of two
samples to be in a same group.



<script>
$( function() {
	$( '#tabs-ATC-NMF-consensus-heatmap' ).tabs();
} );
</script>
<div id='tabs-ATC-NMF-consensus-heatmap'>
<ul>
<li><a href='#tab-ATC-NMF-consensus-heatmap-1'>k = 2</a></li>
<li><a href='#tab-ATC-NMF-consensus-heatmap-2'>k = 3</a></li>
<li><a href='#tab-ATC-NMF-consensus-heatmap-3'>k = 4</a></li>
<li><a href='#tab-ATC-NMF-consensus-heatmap-4'>k = 5</a></li>
<li><a href='#tab-ATC-NMF-consensus-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-ATC-NMF-consensus-heatmap-1'>
<pre><code class="r">consensus_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-ATC-NMF-consensus-heatmap-1-1.png" alt="plot of chunk tab-ATC-NMF-consensus-heatmap-1"/></p>

</div>
<div id='tab-ATC-NMF-consensus-heatmap-2'>
<pre><code class="r">consensus_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-ATC-NMF-consensus-heatmap-2-1.png" alt="plot of chunk tab-ATC-NMF-consensus-heatmap-2"/></p>

</div>
<div id='tab-ATC-NMF-consensus-heatmap-3'>
<pre><code class="r">consensus_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-ATC-NMF-consensus-heatmap-3-1.png" alt="plot of chunk tab-ATC-NMF-consensus-heatmap-3"/></p>

</div>
<div id='tab-ATC-NMF-consensus-heatmap-4'>
<pre><code class="r">consensus_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-ATC-NMF-consensus-heatmap-4-1.png" alt="plot of chunk tab-ATC-NMF-consensus-heatmap-4"/></p>

</div>
<div id='tab-ATC-NMF-consensus-heatmap-5'>
<pre><code class="r">consensus_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-ATC-NMF-consensus-heatmap-5-1.png" alt="plot of chunk tab-ATC-NMF-consensus-heatmap-5"/></p>

</div>
</div>

Heatmaps for the membership of samples in all partitions to see how consistent they are:




<script>
$( function() {
	$( '#tabs-ATC-NMF-membership-heatmap' ).tabs();
} );
</script>
<div id='tabs-ATC-NMF-membership-heatmap'>
<ul>
<li><a href='#tab-ATC-NMF-membership-heatmap-1'>k = 2</a></li>
<li><a href='#tab-ATC-NMF-membership-heatmap-2'>k = 3</a></li>
<li><a href='#tab-ATC-NMF-membership-heatmap-3'>k = 4</a></li>
<li><a href='#tab-ATC-NMF-membership-heatmap-4'>k = 5</a></li>
<li><a href='#tab-ATC-NMF-membership-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-ATC-NMF-membership-heatmap-1'>
<pre><code class="r">membership_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-ATC-NMF-membership-heatmap-1-1.png" alt="plot of chunk tab-ATC-NMF-membership-heatmap-1"/></p>

</div>
<div id='tab-ATC-NMF-membership-heatmap-2'>
<pre><code class="r">membership_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-ATC-NMF-membership-heatmap-2-1.png" alt="plot of chunk tab-ATC-NMF-membership-heatmap-2"/></p>

</div>
<div id='tab-ATC-NMF-membership-heatmap-3'>
<pre><code class="r">membership_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-ATC-NMF-membership-heatmap-3-1.png" alt="plot of chunk tab-ATC-NMF-membership-heatmap-3"/></p>

</div>
<div id='tab-ATC-NMF-membership-heatmap-4'>
<pre><code class="r">membership_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-ATC-NMF-membership-heatmap-4-1.png" alt="plot of chunk tab-ATC-NMF-membership-heatmap-4"/></p>

</div>
<div id='tab-ATC-NMF-membership-heatmap-5'>
<pre><code class="r">membership_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-ATC-NMF-membership-heatmap-5-1.png" alt="plot of chunk tab-ATC-NMF-membership-heatmap-5"/></p>

</div>
</div>

As soon as we have had the classes for columns, we can look for signatures
which are significantly different between classes which can be candidate marks
for certain classes. Following are the heatmaps for signatures.



Signature heatmaps where rows are scaled:



<script>
$( function() {
	$( '#tabs-ATC-NMF-get-signatures' ).tabs();
} );
</script>
<div id='tabs-ATC-NMF-get-signatures'>
<ul>
<li><a href='#tab-ATC-NMF-get-signatures-1'>k = 2</a></li>
<li><a href='#tab-ATC-NMF-get-signatures-2'>k = 3</a></li>
<li><a href='#tab-ATC-NMF-get-signatures-3'>k = 4</a></li>
<li><a href='#tab-ATC-NMF-get-signatures-4'>k = 5</a></li>
<li><a href='#tab-ATC-NMF-get-signatures-5'>k = 6</a></li>
</ul>
<div id='tab-ATC-NMF-get-signatures-1'>
<pre><code class="r">get_signatures(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-ATC-NMF-get-signatures-1-1.png" alt="plot of chunk tab-ATC-NMF-get-signatures-1"/></p>

</div>
<div id='tab-ATC-NMF-get-signatures-2'>
<pre><code class="r">get_signatures(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-ATC-NMF-get-signatures-2-1.png" alt="plot of chunk tab-ATC-NMF-get-signatures-2"/></p>

</div>
<div id='tab-ATC-NMF-get-signatures-3'>
<pre><code class="r">get_signatures(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-ATC-NMF-get-signatures-3-1.png" alt="plot of chunk tab-ATC-NMF-get-signatures-3"/></p>

</div>
<div id='tab-ATC-NMF-get-signatures-4'>
<pre><code class="r">get_signatures(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-ATC-NMF-get-signatures-4-1.png" alt="plot of chunk tab-ATC-NMF-get-signatures-4"/></p>

</div>
<div id='tab-ATC-NMF-get-signatures-5'>
<pre><code class="r">get_signatures(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-ATC-NMF-get-signatures-5-1.png" alt="plot of chunk tab-ATC-NMF-get-signatures-5"/></p>

</div>
</div>



Signature heatmaps where rows are not scaled:


<script>
$( function() {
	$( '#tabs-ATC-NMF-get-signatures-no-scale' ).tabs();
} );
</script>
<div id='tabs-ATC-NMF-get-signatures-no-scale'>
<ul>
<li><a href='#tab-ATC-NMF-get-signatures-no-scale-1'>k = 2</a></li>
<li><a href='#tab-ATC-NMF-get-signatures-no-scale-2'>k = 3</a></li>
<li><a href='#tab-ATC-NMF-get-signatures-no-scale-3'>k = 4</a></li>
<li><a href='#tab-ATC-NMF-get-signatures-no-scale-4'>k = 5</a></li>
<li><a href='#tab-ATC-NMF-get-signatures-no-scale-5'>k = 6</a></li>
</ul>
<div id='tab-ATC-NMF-get-signatures-no-scale-1'>
<pre><code class="r">get_signatures(res, k = 2, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-ATC-NMF-get-signatures-no-scale-1-1.png" alt="plot of chunk tab-ATC-NMF-get-signatures-no-scale-1"/></p>

</div>
<div id='tab-ATC-NMF-get-signatures-no-scale-2'>
<pre><code class="r">get_signatures(res, k = 3, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-ATC-NMF-get-signatures-no-scale-2-1.png" alt="plot of chunk tab-ATC-NMF-get-signatures-no-scale-2"/></p>

</div>
<div id='tab-ATC-NMF-get-signatures-no-scale-3'>
<pre><code class="r">get_signatures(res, k = 4, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-ATC-NMF-get-signatures-no-scale-3-1.png" alt="plot of chunk tab-ATC-NMF-get-signatures-no-scale-3"/></p>

</div>
<div id='tab-ATC-NMF-get-signatures-no-scale-4'>
<pre><code class="r">get_signatures(res, k = 5, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-ATC-NMF-get-signatures-no-scale-4-1.png" alt="plot of chunk tab-ATC-NMF-get-signatures-no-scale-4"/></p>

</div>
<div id='tab-ATC-NMF-get-signatures-no-scale-5'>
<pre><code class="r">get_signatures(res, k = 6, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-ATC-NMF-get-signatures-no-scale-5-1.png" alt="plot of chunk tab-ATC-NMF-get-signatures-no-scale-5"/></p>

</div>
</div>



Compare the overlap of signatures from different k:

```r
compare_signatures(res)
```

![plot of chunk ATC-NMF-signature_compare](figure_cola/ATC-NMF-signature_compare-1.png)

`get_signature()` returns a data frame invisibly. TO get the list of signatures, the function
call should be assigned to a variable explicitly. In following code, if `plot` argument is set
to `FALSE`, no heatmap is plotted while only the differential analysis is performed.

```r
# code only for demonstration
tb = get_signature(res, k = ..., plot = FALSE)
```

An example of the output of `tb` is:

```
#>   which_row         fdr    mean_1    mean_2 scaled_mean_1 scaled_mean_2 km
#> 1        38 0.042760348  8.373488  9.131774    -0.5533452     0.5164555  1
#> 2        40 0.018707592  7.106213  8.469186    -0.6173731     0.5762149  1
#> 3        55 0.019134737 10.221463 11.207825    -0.6159697     0.5749050  1
#> 4        59 0.006059896  5.921854  7.869574    -0.6899429     0.6439467  1
#> 5        60 0.018055526  8.928898 10.211722    -0.6204761     0.5791110  1
#> 6        98 0.009384629 15.714769 14.887706     0.6635654    -0.6193277  2
...
```

The columns in `tb` are:

1. `which_row`: row indices corresponding to the input matrix.
2. `fdr`: FDR for the differential test. 
3. `mean_x`: The mean value in group x.
4. `scaled_mean_x`: The mean value in group x after rows are scaled.
5. `km`: Row groups if k-means clustering is applied to rows.



UMAP plot which shows how samples are separated.


<script>
$( function() {
	$( '#tabs-ATC-NMF-dimension-reduction' ).tabs();
} );
</script>
<div id='tabs-ATC-NMF-dimension-reduction'>
<ul>
<li><a href='#tab-ATC-NMF-dimension-reduction-1'>k = 2</a></li>
<li><a href='#tab-ATC-NMF-dimension-reduction-2'>k = 3</a></li>
<li><a href='#tab-ATC-NMF-dimension-reduction-3'>k = 4</a></li>
<li><a href='#tab-ATC-NMF-dimension-reduction-4'>k = 5</a></li>
<li><a href='#tab-ATC-NMF-dimension-reduction-5'>k = 6</a></li>
</ul>
<div id='tab-ATC-NMF-dimension-reduction-1'>
<pre><code class="r">dimension_reduction(res, k = 2, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-ATC-NMF-dimension-reduction-1-1.png" alt="plot of chunk tab-ATC-NMF-dimension-reduction-1"/></p>

</div>
<div id='tab-ATC-NMF-dimension-reduction-2'>
<pre><code class="r">dimension_reduction(res, k = 3, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-ATC-NMF-dimension-reduction-2-1.png" alt="plot of chunk tab-ATC-NMF-dimension-reduction-2"/></p>

</div>
<div id='tab-ATC-NMF-dimension-reduction-3'>
<pre><code class="r">dimension_reduction(res, k = 4, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-ATC-NMF-dimension-reduction-3-1.png" alt="plot of chunk tab-ATC-NMF-dimension-reduction-3"/></p>

</div>
<div id='tab-ATC-NMF-dimension-reduction-4'>
<pre><code class="r">dimension_reduction(res, k = 5, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-ATC-NMF-dimension-reduction-4-1.png" alt="plot of chunk tab-ATC-NMF-dimension-reduction-4"/></p>

</div>
<div id='tab-ATC-NMF-dimension-reduction-5'>
<pre><code class="r">dimension_reduction(res, k = 6, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-ATC-NMF-dimension-reduction-5-1.png" alt="plot of chunk tab-ATC-NMF-dimension-reduction-5"/></p>

</div>
</div>


Following heatmap shows how subgroups are split when increasing `k`:

```r
collect_classes(res)
```

![plot of chunk ATC-NMF-collect-classes](figure_cola/ATC-NMF-collect-classes-1.png)


If matrix rows can be associated to genes, consider to use `functional_enrichment(res,
...)` to perform function enrichment for the signature genes. See [this vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/functional_enrichment.html) for more detailed explanations.


 

## Session info


```r
sessionInfo()
```

```
#> R version 3.6.0 (2019-04-26)
#> Platform: x86_64-pc-linux-gnu (64-bit)
#> Running under: CentOS Linux 7 (Core)
#> 
#> Matrix products: default
#> BLAS:   /usr/lib64/libblas.so.3.4.2
#> LAPACK: /usr/lib64/liblapack.so.3.4.2
#> 
#> locale:
#>  [1] LC_CTYPE=en_GB.UTF-8       LC_NUMERIC=C               LC_TIME=en_GB.UTF-8       
#>  [4] LC_COLLATE=en_GB.UTF-8     LC_MONETARY=en_GB.UTF-8    LC_MESSAGES=en_GB.UTF-8   
#>  [7] LC_PAPER=en_GB.UTF-8       LC_NAME=C                  LC_ADDRESS=C              
#> [10] LC_TELEPHONE=C             LC_MEASUREMENT=en_GB.UTF-8 LC_IDENTIFICATION=C       
#> 
#> attached base packages:
#> [1] grid      stats     graphics  grDevices utils     datasets  methods   base     
#> 
#> other attached packages:
#> [1] genefilter_1.66.0    ComplexHeatmap_2.3.1 markdown_1.1         knitr_1.26          
#> [5] GetoptLong_0.1.7     cola_1.3.2          
#> 
#> loaded via a namespace (and not attached):
#>  [1] circlize_0.4.8       shape_1.4.4          xfun_0.11            slam_0.1-46         
#>  [5] lattice_0.20-38      splines_3.6.0        colorspace_1.4-1     vctrs_0.2.0         
#>  [9] stats4_3.6.0         blob_1.2.0           XML_3.98-1.20        survival_2.44-1.1   
#> [13] rlang_0.4.2          pillar_1.4.2         DBI_1.0.0            BiocGenerics_0.30.0 
#> [17] bit64_0.9-7          RColorBrewer_1.1-2   matrixStats_0.55.0   stringr_1.4.0       
#> [21] GlobalOptions_0.1.1  evaluate_0.14        memoise_1.1.0        Biobase_2.44.0      
#> [25] IRanges_2.18.3       parallel_3.6.0       AnnotationDbi_1.46.1 highr_0.8           
#> [29] Rcpp_1.0.3           xtable_1.8-4         backports_1.1.5      S4Vectors_0.22.1    
#> [33] annotate_1.62.0      skmeans_0.2-11       bit_1.1-14           microbenchmark_1.4-7
#> [37] brew_1.0-6           impute_1.58.0        rjson_0.2.20         png_0.1-7           
#> [41] digest_0.6.23        stringi_1.4.3        polyclip_1.10-0      clue_0.3-57         
#> [45] tools_3.6.0          bitops_1.0-6         magrittr_1.5         eulerr_6.0.0        
#> [49] RCurl_1.95-4.12      RSQLite_2.1.4        tibble_2.1.3         cluster_2.1.0       
#> [53] crayon_1.3.4         pkgconfig_2.0.3      zeallot_0.1.0        Matrix_1.2-17       
#> [57] xml2_1.2.2           httr_1.4.1           R6_2.4.1             mclust_5.4.5        
#> [61] compiler_3.6.0
```


