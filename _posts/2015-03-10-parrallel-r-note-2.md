---
layout: post
description: ""
category: 
tags: []
---
{% include JB/setup %}


<html xmlns="http://www.w3.org/1999/xhtml">

<head>

<meta charset="utf-8">
<meta http-equiv="Content-Type" content="text/html; charset=utf-8" />
<meta name="generator" content="pandoc" />


<meta name="date" content="2015-03-10" />





<style type="text/css">code{white-space: pre;}</style>
<style type="text/css">
table.sourceCode, tr.sourceCode, td.lineNumbers, td.sourceCode {
  margin: 0; padding: 0; vertical-align: baseline; border: none; }
table.sourceCode { width: 100%; line-height: 100%; }
td.lineNumbers { text-align: right; padding-right: 4px; padding-left: 4px; color: #aaaaaa; border-right: 1px solid #aaaaaa; }
td.sourceCode { padding-left: 5px; }
code > span.kw { color: #007020; font-weight: bold; }
code > span.dt { color: #902000; }
code > span.dv { color: #40a070; }
code > span.bn { color: #40a070; }
code > span.fl { color: #40a070; }
code > span.ch { color: #4070a0; }
code > span.st { color: #4070a0; }
code > span.co { color: #60a0b0; font-style: italic; }
code > span.ot { color: #007020; }
code > span.al { color: #ff0000; font-weight: bold; }
code > span.fu { color: #06287e; }
code > span.er { color: #ff0000; font-weight: bold; }
</style>
<style type="text/css">
  pre:not([class]) {
    background-color: white;
  }
</style>


<link href="data:text/css,body%20%7B%0A%20%20background%2Dcolor%3A%20%23fff%3B%0A%20%20margin%3A%201em%20auto%3B%0A%20%20max%2Dwidth%3A%20700px%3B%0A%20%20overflow%3A%20visible%3B%0A%20%20padding%2Dleft%3A%202em%3B%0A%20%20padding%2Dright%3A%202em%3B%0A%20%20font%2Dfamily%3A%20%22Open%20Sans%22%2C%20%22Helvetica%20Neue%22%2C%20Helvetica%2C%20Arial%2C%20sans%2Dserif%3B%0A%20%20font%2Dsize%3A%2014px%3B%0A%20%20line%2Dheight%3A%201%2E35%3B%0A%7D%0A%0A%23header%20%7B%0A%20%20text%2Dalign%3A%20center%3B%0A%7D%0A%0A%23TOC%20%7B%0A%20%20clear%3A%20both%3B%0A%20%20margin%3A%200%200%2010px%2010px%3B%0A%20%20padding%3A%204px%3B%0A%20%20width%3A%20400px%3B%0A%20%20border%3A%201px%20solid%20%23CCCCCC%3B%0A%20%20border%2Dradius%3A%205px%3B%0A%0A%20%20background%2Dcolor%3A%20%23f6f6f6%3B%0A%20%20font%2Dsize%3A%2013px%3B%0A%20%20line%2Dheight%3A%201%2E3%3B%0A%7D%0A%20%20%23TOC%20%2Etoctitle%20%7B%0A%20%20%20%20font%2Dweight%3A%20bold%3B%0A%20%20%20%20font%2Dsize%3A%2015px%3B%0A%20%20%20%20margin%2Dleft%3A%205px%3B%0A%20%20%7D%0A%0A%20%20%23TOC%20ul%20%7B%0A%20%20%20%20padding%2Dleft%3A%2040px%3B%0A%20%20%20%20margin%2Dleft%3A%20%2D1%2E5em%3B%0A%20%20%20%20margin%2Dtop%3A%205px%3B%0A%20%20%20%20margin%2Dbottom%3A%205px%3B%0A%20%20%7D%0A%20%20%23TOC%20ul%20ul%20%7B%0A%20%20%20%20margin%2Dleft%3A%20%2D2em%3B%0A%20%20%7D%0A%20%20%23TOC%20li%20%7B%0A%20%20%20%20line%2Dheight%3A%2016px%3B%0A%20%20%7D%0A%0Atable%20%7B%0A%20%20margin%3A%201em%20auto%3B%0A%20%20border%2Dwidth%3A%201px%3B%0A%20%20border%2Dcolor%3A%20%23DDDDDD%3B%0A%20%20border%2Dstyle%3A%20outset%3B%0A%20%20border%2Dcollapse%3A%20collapse%3B%0A%7D%0Atable%20th%20%7B%0A%20%20border%2Dwidth%3A%202px%3B%0A%20%20padding%3A%205px%3B%0A%20%20border%2Dstyle%3A%20inset%3B%0A%7D%0Atable%20td%20%7B%0A%20%20border%2Dwidth%3A%201px%3B%0A%20%20border%2Dstyle%3A%20inset%3B%0A%20%20line%2Dheight%3A%2018px%3B%0A%20%20padding%3A%205px%205px%3B%0A%7D%0Atable%2C%20table%20th%2C%20table%20td%20%7B%0A%20%20border%2Dleft%2Dstyle%3A%20none%3B%0A%20%20border%2Dright%2Dstyle%3A%20none%3B%0A%7D%0Atable%20thead%2C%20table%20tr%2Eeven%20%7B%0A%20%20background%2Dcolor%3A%20%23f7f7f7%3B%0A%7D%0A%0Ap%20%7B%0A%20%20margin%3A%200%2E5em%200%3B%0A%7D%0A%0Ablockquote%20%7B%0A%20%20background%2Dcolor%3A%20%23f6f6f6%3B%0A%20%20padding%3A%200%2E25em%200%2E75em%3B%0A%7D%0A%0Ahr%20%7B%0A%20%20border%2Dstyle%3A%20solid%3B%0A%20%20border%3A%20none%3B%0A%20%20border%2Dtop%3A%201px%20solid%20%23777%3B%0A%20%20margin%3A%2028px%200%3B%0A%7D%0A%0Adl%20%7B%0A%20%20margin%2Dleft%3A%200%3B%0A%7D%0A%20%20dl%20dd%20%7B%0A%20%20%20%20margin%2Dbottom%3A%2013px%3B%0A%20%20%20%20margin%2Dleft%3A%2013px%3B%0A%20%20%7D%0A%20%20dl%20dt%20%7B%0A%20%20%20%20font%2Dweight%3A%20bold%3B%0A%20%20%7D%0A%0Aul%20%7B%0A%20%20margin%2Dtop%3A%200%3B%0A%7D%0A%20%20ul%20li%20%7B%0A%20%20%20%20list%2Dstyle%3A%20circle%20outside%3B%0A%20%20%7D%0A%20%20ul%20ul%20%7B%0A%20%20%20%20margin%2Dbottom%3A%200%3B%0A%20%20%7D%0A%0Apre%2C%20code%20%7B%0A%20%20background%2Dcolor%3A%20%23f7f7f7%3B%0A%20%20border%2Dradius%3A%203px%3B%0A%20%20color%3A%20%23333%3B%0A%7D%0Apre%20%7B%0A%20%20white%2Dspace%3A%20pre%2Dwrap%3B%20%20%20%20%2F%2A%20Wrap%20long%20lines%20%2A%2F%0A%20%20border%2Dradius%3A%203px%3B%0A%20%20margin%3A%205px%200px%2010px%200px%3B%0A%20%20padding%3A%2010px%3B%0A%7D%0Apre%3Anot%28%5Bclass%5D%29%20%7B%0A%20%20background%2Dcolor%3A%20%23f7f7f7%3B%0A%7D%0A%0Acode%20%7B%0A%20%20font%2Dfamily%3A%20Consolas%2C%20Monaco%2C%20%27Courier%20New%27%2C%20monospace%3B%0A%20%20font%2Dsize%3A%2085%25%3B%0A%7D%0Ap%20%3E%20code%2C%20li%20%3E%20code%20%7B%0A%20%20padding%3A%202px%200px%3B%0A%7D%0A%0Adiv%2Efigure%20%7B%0A%20%20text%2Dalign%3A%20center%3B%0A%7D%0Aimg%20%7B%0A%20%20background%2Dcolor%3A%20%23FFFFFF%3B%0A%20%20padding%3A%202px%3B%0A%20%20border%3A%201px%20solid%20%23DDDDDD%3B%0A%20%20border%2Dradius%3A%203px%3B%0A%20%20border%3A%201px%20solid%20%23CCCCCC%3B%0A%20%20margin%3A%200%205px%3B%0A%7D%0A%0Ah1%20%7B%0A%20%20margin%2Dtop%3A%200%3B%0A%20%20font%2Dsize%3A%2035px%3B%0A%20%20line%2Dheight%3A%2040px%3B%0A%7D%0A%0Ah2%20%7B%0A%20%20border%2Dbottom%3A%204px%20solid%20%23f7f7f7%3B%0A%20%20padding%2Dtop%3A%2010px%3B%0A%20%20padding%2Dbottom%3A%202px%3B%0A%20%20font%2Dsize%3A%20145%25%3B%0A%7D%0A%0Ah3%20%7B%0A%20%20border%2Dbottom%3A%202px%20solid%20%23f7f7f7%3B%0A%20%20padding%2Dtop%3A%2010px%3B%0A%20%20font%2Dsize%3A%20120%25%3B%0A%7D%0A%0Ah4%20%7B%0A%20%20border%2Dbottom%3A%201px%20solid%20%23f7f7f7%3B%0A%20%20margin%2Dleft%3A%208px%3B%0A%20%20font%2Dsize%3A%20105%25%3B%0A%7D%0A%0Ah5%2C%20h6%20%7B%0A%20%20border%2Dbottom%3A%201px%20solid%20%23ccc%3B%0A%20%20font%2Dsize%3A%20105%25%3B%0A%7D%0A%0Aa%20%7B%0A%20%20color%3A%20%230033dd%3B%0A%20%20text%2Ddecoration%3A%20none%3B%0A%7D%0A%20%20a%3Ahover%20%7B%0A%20%20%20%20color%3A%20%236666ff%3B%20%7D%0A%20%20a%3Avisited%20%7B%0A%20%20%20%20color%3A%20%23800080%3B%20%7D%0A%20%20a%3Avisited%3Ahover%20%7B%0A%20%20%20%20color%3A%20%23BB00BB%3B%20%7D%0A%20%20a%5Bhref%5E%3D%22http%3A%22%5D%20%7B%0A%20%20%20%20text%2Ddecoration%3A%20underline%3B%20%7D%0A%20%20a%5Bhref%5E%3D%22https%3A%22%5D%20%7B%0A%20%20%20%20text%2Ddecoration%3A%20underline%3B%20%7D%0A%0A%2F%2A%20Class%20described%20in%20https%3A%2F%2Fbenjeffrey%2Ecom%2Fposts%2Fpandoc%2Dsyntax%2Dhighlighting%2Dcss%0A%20%20%20Colours%20from%20https%3A%2F%2Fgist%2Egithub%2Ecom%2Frobsimmons%2F1172277%20%2A%2F%0A%0Acode%20%3E%20span%2Ekw%20%7B%20color%3A%20%23555%3B%20font%2Dweight%3A%20bold%3B%20%7D%20%2F%2A%20Keyword%20%2A%2F%0Acode%20%3E%20span%2Edt%20%7B%20color%3A%20%23902000%3B%20%7D%20%2F%2A%20DataType%20%2A%2F%0Acode%20%3E%20span%2Edv%20%7B%20color%3A%20%2340a070%3B%20%7D%20%2F%2A%20DecVal%20%28decimal%20values%29%20%2A%2F%0Acode%20%3E%20span%2Ebn%20%7B%20color%3A%20%23d14%3B%20%7D%20%2F%2A%20BaseN%20%2A%2F%0Acode%20%3E%20span%2Efl%20%7B%20color%3A%20%23d14%3B%20%7D%20%2F%2A%20Float%20%2A%2F%0Acode%20%3E%20span%2Ech%20%7B%20color%3A%20%23d14%3B%20%7D%20%2F%2A%20Char%20%2A%2F%0Acode%20%3E%20span%2Est%20%7B%20color%3A%20%23d14%3B%20%7D%20%2F%2A%20String%20%2A%2F%0Acode%20%3E%20span%2Eco%20%7B%20color%3A%20%23888888%3B%20font%2Dstyle%3A%20italic%3B%20%7D%20%2F%2A%20Comment%20%2A%2F%0Acode%20%3E%20span%2Eot%20%7B%20color%3A%20%23007020%3B%20%7D%20%2F%2A%20OtherToken%20%2A%2F%0Acode%20%3E%20span%2Eal%20%7B%20color%3A%20%23ff0000%3B%20font%2Dweight%3A%20bold%3B%20%7D%20%2F%2A%20AlertToken%20%2A%2F%0Acode%20%3E%20span%2Efu%20%7B%20color%3A%20%23900%3B%20font%2Dweight%3A%20bold%3B%20%7D%20%2F%2A%20Function%20calls%20%2A%2F%20%0Acode%20%3E%20span%2Eer%20%7B%20color%3A%20%23a61717%3B%20background%2Dcolor%3A%20%23e3d2d2%3B%20%7D%20%2F%2A%20ErrorTok%20%2A%2F%0A%0A" rel="stylesheet" type="text/css" />

</head>

<body>



<div id="header">

<h4 class="date"><em>2015-03-10</em></h4>
</div>


<div id="motivation" class="section level2">
<h2>Motivation</h2>
<p>I want to use a Linux cluster to run an R script faster. I am sick of waiting many hours or days for the Monte Carlo simulation to finish.</p>
<p><code>Monte Carlo simulation</code>: a computerized mathematical technique that allows people to account for risk in quantitative analysis and decision making. This technique furnishes the decision-maker with a range of possible outcomes and the probabilities they will occur for any choice of action. It shows the extreme possibilities—the outcomes of going for broke and for the most conservative decision—along with all possible consequences for middle-of-the-road decisions.</p>
</div>
<div id="solution" class="section level2">
<h2>Solution</h2>
<p>Use <code>snow</code> to run my R code on the company or university’s Linux cluster. <code>snow</code> fits well with tradtional cluster environment, and is able to take advantage of high-speed communication networks using MPI (if you don’t understand this term, refer to <a href="http://mayweiwang.com/2015/03/">Parallel R note 1</a>).</p>
</div>
<div id="how-it-works" class="section level2">
<h2>How it works</h2>
<p><code>snow</code> provides parallel execution functions. These functions are variations of the standard <code>lapply()</code> function. <code>snow</code> uses a <code>master/worker</code> architecture.</p>
<ul>
<li>architecture: master/worker</li>
<li>master: sends tasks to the workers</li>
<li>worker: execute the tasks and return the results to the master</li>
<li>communication mechanism : between master and worker</li>
</ul>
</div>
<div id="important-feature-communication-mechanism" class="section level2">
<h2>Important feature : communication mechanism</h2>
<p>Different transport mechanisms include <code>socket connection</code>, <code>MPI</code>, <code>PVM</code>, or <code>NetWorkSpaces</code>. This allows <code>snow</code> to be portable, but still take advantage of high-performance communication mechanisms if available.</p>
<ul>
<li><code>socket</code>: most portable, no additional packages required</li>
<li><code>MPI</code> : supported via the <code>Rmpi</code> package, popular on Linux clusters</li>
<li><code>PVM</code> : supported via the <code>rpvm</code> package, popular on multicore, e.g., Windows PC</li>
<li><code>NWS</code> : supported via the <code>nws</code> package</li>
</ul>
</div>
<div id="suitable-applications" class="section level2">
<h2>Suitable applications</h2>
<p>Monte Carlo simulations, bootstrapping, cross validation, ensemble machine learning algorithms, and K-means clustering.</p>
<p><strong>Tip 1</strong>: using the <code>rsprng</code> and <code>rlecuyer</code> packages for parallel random number generation. This is <strong>important</strong> for simulations, bootstrapping, and machine learning.</p>
<p><strong>Tip 2</strong>: <code>snow</code> is not designed for dealing with large data, such as distributing data files to the workers. The input arguments must fit into memory and all of the task results are kept in memory on the master until they are returned to the caller in a list.</p>
<p><strong>Tip 3</strong> <code>snow</code> can be used with high-performance dfs (distributed file system) in order to operate on large data files, but the user has to arrange this.</p>
</div>
<div id="setting-up" class="section level2">
<h2>Setting up</h2>
<p><code>snow</code> is available on <code>CRAN</code>(Comprehensive R Archive Network). It is pure R code and installed like any other <code>CRAN</code> package.</p>
<pre class="sourceCode r"><code class="sourceCode r"><span class="kw">library</span>(<span class="st">&quot;snow&quot;</span>)</code></pre>
<p>To use <code>snow</code> with <code>MPI</code>, I will also need to install the <code>Rmpi</code> package. However, this is usually quite problematic, because it has an external dependency on MPI. The <code>socket</code> transport can be used without installing any packages. For the reason that I am new to <code>snow</code>, I would just play with this communication mechinsim first.</p>
<p>I will first of all check if i have successfully installed the <code>snow</code> package by</p>
<pre class="sourceCode r"><code class="sourceCode r"><span class="kw">library</span>()</code></pre>
<p>And I do find <code>snow</code> in the file <code>R packages available</code>.</p>
<div id="creating-clusters" class="section level3">
<h3>Creating clusters</h3>
<p>The first thing to do is to create a <em>cluster object</em>. It is used to interact with the cluster workers, and is passed as the first argument to many of the <code>snow</code> functions.</p>
<p><strong>Tip</strong>: I can create different types of cluster objects, depending on the <strong>transport mechanism</strong>.</p>
<pre class="sourceCode r"><code class="sourceCode r"><span class="kw">library</span>(<span class="st">&quot;snow&quot;</span>)
cl &lt;-<span class="st"> </span><span class="kw">makeCluster</span>(<span class="dv">4</span>,<span class="dt">type=</span><span class="st">&quot;SOCK&quot;</span>)</code></pre>
<p><code>4</code> is the cluster specification, and the <code>SOCK</code> is the cluster type.</p>
<p>The <code>socket</code> transport lauches each of these workers via the <code>ssh</code> command unless the <code>name</code> is <code>localhost</code>, in which case <code>makeCluster()</code> starts the worker itself. <strong>Tip</strong>: For remote execution, I should configure <code>ssh</code> to use password-less login. This can be done using public-key authentication and SSH agents.</p>
</div>
</div>
<div id="demo-parallel-k-means" class="section level2">
<h2>Demo: Parallel K-Means</h2>
<p><code>K-Means</code> is a unsupervised clustering algorithm that classifies the rows of observations (a dataset) into k clusters<a href="#fn1" class="footnoteRef" id="fnref1"><sup>1</sup></a>. It starts with a guess of the location for each of the cluster centers, and gradually improves the center locations until it finishes the clustering. This algorithm is included in the <code>stats</code> package as <code>kmenas()</code> function.<br />To load the package <code>MASS</code>,</p>
<pre class="sourceCode r"><code class="sourceCode r"><span class="kw">library</span>(MASS)</code></pre>
<p>Before I use it for parallel, I try using the <code>lapply()</code> function to make sure it works. Once this is done, it should be fairly easy to convert to one of the <code>snow</code> parallel execution functions.</p>
<p>I use a vector of four 25s to specify the <code>nstart</code> argument in order to get equivalent results to using a 100 in a single call to kmeans(). The length of the vector <code>x</code> should be equal to the number of workers in the cluster when running in parallel.</p>
<pre class="sourceCode r"><code class="sourceCode r">x &lt;-<span class="st"> </span><span class="kw">rep</span>(<span class="dv">25</span>,<span class="dv">4</span>)
x</code></pre>
<pre><code>## [1] 25 25 25 25</code></pre>
<pre class="sourceCode r"><code class="sourceCode r">results &lt;-<span class="kw">lapply</span>(x,function(nstart) <span class="kw">kmeans</span>(Boston,<span class="dv">4</span>,<span class="dt">nstart=</span>nstart))
i &lt;-<span class="st"> </span><span class="kw">sapply</span>(results, function(result) result$<span class="st"> </span>tot.withinss)
result &lt;-results[[<span class="kw">which.min</span>(i)]]
<span class="kw">print</span>(result)</code></pre>
<pre><code>## K-means clustering with 4 clusters of sizes 102, 268, 38, 98
## 
## Cluster means:
##         crim       zn     indus       chas       nox       rm      age
## 1 10.9105113  0.00000 18.572549 0.07843137 0.6712255 5.982265 89.91373
## 2  0.2410479 17.81716  6.668582 0.07462687 0.4833981 6.465448 55.70522
## 3 15.2190382  0.00000 17.926842 0.02631579 0.6737105 6.065500 89.90526
## 4  0.7412906  9.94898 12.983776 0.06122449 0.5822347 6.189847 73.28878
##        dis       rad      tax  ptratio     black     lstat     medv
## 1 2.077164 23.019608 668.2059 20.19510 371.80304 17.874020 17.42941
## 2 4.873560  4.313433 276.5485 17.87313 387.81407  9.538022 25.86530
## 3 1.994429 22.500000 644.7368 19.92895  57.78632 20.448684 13.12632
## 4 3.331821  4.826531 406.0816 17.66633 371.66429 12.714898 22.37857
## 
## Clustering vector:
##   1   2   3   4   5   6   7   8   9  10  11  12  13  14  15  16  17  18 
##   2   2   2   2   2   2   2   2   2   2   2   2   2   2   2   2   2   2 
##  19  20  21  22  23  24  25  26  27  28  29  30  31  32  33  34  35  36 
##   2   2   2   2   2   2   2   2   2   2   2   2   2   2   2   2   2   2 
##  37  38  39  40  41  42  43  44  45  46  47  48  49  50  51  52  53  54 
##   2   2   2   2   2   2   2   2   2   2   2   2   2   2   2   2   2   2 
##  55  56  57  58  59  60  61  62  63  64  65  66  67  68  69  70  71  72 
##   4   2   2   2   2   2   2   2   2   2   2   2   2   2   2   2   2   2 
##  73  74  75  76  77  78  79  80  81  82  83  84  85  86  87  88  89  90 
##   2   2   4   4   4   4   4   4   2   2   2   2   2   2   2   2   2   2 
##  91  92  93  94  95  96  97  98  99 100 101 102 103 104 105 106 107 108 
##   2   2   2   2   2   2   2   2   2   2   4   4   3   4   4   4   4   4 
## 109 110 111 112 113 114 115 116 117 118 119 120 121 122 123 124 125 126 
##   4   4   4   4   4   4   4   4   4   4   4   4   2   2   2   2   2   2 
## 127 128 129 130 131 132 133 134 135 136 137 138 139 140 141 142 143 144 
##   2   4   4   4   4   4   4   4   4   4   4   4   4   4   4   4   4   4 
## 145 146 147 148 149 150 151 152 153 154 155 156 157 158 159 160 161 162 
##   4   4   4   4   4   4   4   4   4   4   4   3   3   4   4   4   4   4 
## 163 164 165 166 167 168 169 170 171 172 173 174 175 176 177 178 179 180 
##   4   4   4   4   4   4   4   4   4   4   2   2   2   2   2   2   2   2 
## 181 182 183 184 185 186 187 188 189 190 191 192 193 194 195 196 197 198 
##   2   2   2   2   2   2   2   4   4   4   4   4   4   2   2   2   2   2 
## 199 200 201 202 203 204 205 206 207 208 209 210 211 212 213 214 215 216 
##   2   4   4   2   2   2   2   2   2   2   2   2   2   2   2   2   2   2 
## 217 218 219 220 221 222 223 224 225 226 227 228 229 230 231 232 233 234 
##   2   2   2   2   2   2   2   2   2   2   2   2   2   2   2   2   2   2 
## 235 236 237 238 239 240 241 242 243 244 245 246 247 248 249 250 251 252 
##   2   2   2   2   2   2   2   2   2   2   2   2   2   2   2   2   2   2 
## 253 254 255 256 257 258 259 260 261 262 263 264 265 266 267 268 269 270 
##   2   2   2   2   2   2   2   2   2   2   2   2   2   2   2   2   2   2 
## 271 272 273 274 275 276 277 278 279 280 281 282 283 284 285 286 287 288 
##   2   2   2   2   2   2   2   2   2   2   2   2   2   2   2   2   2   2 
## 289 290 291 292 293 294 295 296 297 298 299 300 301 302 303 304 305 306 
##   2   2   2   2   2   2   2   2   2   2   4   4   4   2   2   2   2   2 
## 307 308 309 310 311 312 313 314 315 316 317 318 319 320 321 322 323 324 
##   2   2   2   2   2   2   2   2   2   2   2   2   2   2   2   2   2   2 
## 325 326 327 328 329 330 331 332 333 334 335 336 337 338 339 340 341 342 
##   2   2   2   2   4   4   4   2   2   2   2   2   2   2   2   2   2   2 
## 343 344 345 346 347 348 349 350 351 352 353 354 355 356 357 358 359 360 
##   4   4   4   4   4   2   2   2   2   4   4   2   2   2   1   1   1   1 
## 361 362 363 364 365 366 367 368 369 370 371 372 373 374 375 376 377 378 
##   1   1   1   1   1   1   1   3   1   1   1   1   1   1   1   1   1   1 
## 379 380 381 382 383 384 385 386 387 388 389 390 391 392 393 394 395 396 
##   1   1   1   1   1   1   1   1   1   1   1   1   1   1   1   1   1   1 
## 397 398 399 400 401 402 403 404 405 406 407 408 409 410 411 412 413 414 
##   1   1   1   1   1   1   1   1   1   1   1   1   1   3   3   3   3   3 
## 415 416 417 418 419 420 421 422 423 424 425 426 427 428 429 430 431 432 
##   3   3   3   3   3   3   1   1   1   3   3   3   3   3   3   3   3   3 
## 433 434 435 436 437 438 439 440 441 442 443 444 445 446 447 448 449 450 
##   3   3   3   3   3   3   3   1   1   1   1   1   1   3   1   1   1   1 
## 451 452 453 454 455 456 457 458 459 460 461 462 463 464 465 466 467 468 
##   3   1   1   1   3   3   3   3   1   1   1   1   1   1   1   1   3   1 
## 469 470 471 472 473 474 475 476 477 478 479 480 481 482 483 484 485 486 
##   1   1   1   1   1   1   1   1   1   1   1   1   1   1   1   1   1   1 
## 487 488 489 490 491 492 493 494 495 496 497 498 499 500 501 502 503 504 
##   1   1   1   1   1   1   1   4   4   4   4   4   4   4   4   2   2   2 
## 505 506 
##   2   2 
## 
## Within cluster sum of squares by cluster:
## [1] 181891.7 924118.8 313208.7 395218.3
##  (between_SS / total_SS =  90.6 %)
## 
## Available components:
## 
## [1] &quot;cluster&quot;      &quot;centers&quot;      &quot;totss&quot;        &quot;withinss&quot;    
## [5] &quot;tot.withinss&quot; &quot;betweenss&quot;    &quot;size&quot;         &quot;iter&quot;        
## [9] &quot;ifault&quot;</code></pre>
<p>Now I will parallel this algorithm. let’s look at which functions in <code>snow</code> can be used.</p>
<ul>
<li>clusterApply()</li>
<li>clusterApplyLB()</li>
<li>parLapply()</li>
</ul>
<p>I will use <code>clusterApply()</code> for this demo. The first argument of this function <strong>must</strong> be a <code>snow</code> cluster object. I also need to load <code>MASS</code> on the <strong>workers</strong>, rather than on the master, since it is the workers that use the <code>boston</code> dataset.</p>
<pre class="sourceCode r"><code class="sourceCode r"><span class="kw">library</span>(snow)
cl &lt;-<span class="st"> </span><span class="kw">makeCluster</span>(<span class="dv">4</span>,<span class="dt">type=</span><span class="st">&quot;SOCK&quot;</span>) 
ignore &lt;-<span class="st"> </span><span class="kw">clusterEvalQ</span>(cl,{<span class="kw">library</span>(MASS);<span class="ot">NULL</span>})
results &lt;-<span class="kw">clusterApply</span>(cl,<span class="kw">rep</span>(<span class="dv">25</span>,<span class="dv">4</span>),function(nstart) <span class="kw">kmeans</span>(Boston,<span class="dv">4</span>,<span class="dt">nstart=</span>nstart))
i &lt;-<span class="st"> </span><span class="kw">sapply</span>(results, function(result) result$tot.withinss)
result &lt;-results[[<span class="kw">which.min</span>(i)]]
<span class="kw">print</span>(result)</code></pre>
<pre><code>## K-means clustering with 4 clusters of sizes 98, 268, 102, 38
## 
## Cluster means:
##         crim       zn     indus       chas       nox       rm      age
## 1  0.7412906  9.94898 12.983776 0.06122449 0.5822347 6.189847 73.28878
## 2  0.2410479 17.81716  6.668582 0.07462687 0.4833981 6.465448 55.70522
## 3 10.9105113  0.00000 18.572549 0.07843137 0.6712255 5.982265 89.91373
## 4 15.2190382  0.00000 17.926842 0.02631579 0.6737105 6.065500 89.90526
##        dis       rad      tax  ptratio     black     lstat     medv
## 1 3.331821  4.826531 406.0816 17.66633 371.66429 12.714898 22.37857
## 2 4.873560  4.313433 276.5485 17.87313 387.81407  9.538022 25.86530
## 3 2.077164 23.019608 668.2059 20.19510 371.80304 17.874020 17.42941
## 4 1.994429 22.500000 644.7368 19.92895  57.78632 20.448684 13.12632
## 
## Clustering vector:
##   1   2   3   4   5   6   7   8   9  10  11  12  13  14  15  16  17  18 
##   2   2   2   2   2   2   2   2   2   2   2   2   2   2   2   2   2   2 
##  19  20  21  22  23  24  25  26  27  28  29  30  31  32  33  34  35  36 
##   2   2   2   2   2   2   2   2   2   2   2   2   2   2   2   2   2   2 
##  37  38  39  40  41  42  43  44  45  46  47  48  49  50  51  52  53  54 
##   2   2   2   2   2   2   2   2   2   2   2   2   2   2   2   2   2   2 
##  55  56  57  58  59  60  61  62  63  64  65  66  67  68  69  70  71  72 
##   1   2   2   2   2   2   2   2   2   2   2   2   2   2   2   2   2   2 
##  73  74  75  76  77  78  79  80  81  82  83  84  85  86  87  88  89  90 
##   2   2   1   1   1   1   1   1   2   2   2   2   2   2   2   2   2   2 
##  91  92  93  94  95  96  97  98  99 100 101 102 103 104 105 106 107 108 
##   2   2   2   2   2   2   2   2   2   2   1   1   4   1   1   1   1   1 
## 109 110 111 112 113 114 115 116 117 118 119 120 121 122 123 124 125 126 
##   1   1   1   1   1   1   1   1   1   1   1   1   2   2   2   2   2   2 
## 127 128 129 130 131 132 133 134 135 136 137 138 139 140 141 142 143 144 
##   2   1   1   1   1   1   1   1   1   1   1   1   1   1   1   1   1   1 
## 145 146 147 148 149 150 151 152 153 154 155 156 157 158 159 160 161 162 
##   1   1   1   1   1   1   1   1   1   1   1   4   4   1   1   1   1   1 
## 163 164 165 166 167 168 169 170 171 172 173 174 175 176 177 178 179 180 
##   1   1   1   1   1   1   1   1   1   1   2   2   2   2   2   2   2   2 
## 181 182 183 184 185 186 187 188 189 190 191 192 193 194 195 196 197 198 
##   2   2   2   2   2   2   2   1   1   1   1   1   1   2   2   2   2   2 
## 199 200 201 202 203 204 205 206 207 208 209 210 211 212 213 214 215 216 
##   2   1   1   2   2   2   2   2   2   2   2   2   2   2   2   2   2   2 
## 217 218 219 220 221 222 223 224 225 226 227 228 229 230 231 232 233 234 
##   2   2   2   2   2   2   2   2   2   2   2   2   2   2   2   2   2   2 
## 235 236 237 238 239 240 241 242 243 244 245 246 247 248 249 250 251 252 
##   2   2   2   2   2   2   2   2   2   2   2   2   2   2   2   2   2   2 
## 253 254 255 256 257 258 259 260 261 262 263 264 265 266 267 268 269 270 
##   2   2   2   2   2   2   2   2   2   2   2   2   2   2   2   2   2   2 
## 271 272 273 274 275 276 277 278 279 280 281 282 283 284 285 286 287 288 
##   2   2   2   2   2   2   2   2   2   2   2   2   2   2   2   2   2   2 
## 289 290 291 292 293 294 295 296 297 298 299 300 301 302 303 304 305 306 
##   2   2   2   2   2   2   2   2   2   2   1   1   1   2   2   2   2   2 
## 307 308 309 310 311 312 313 314 315 316 317 318 319 320 321 322 323 324 
##   2   2   2   2   2   2   2   2   2   2   2   2   2   2   2   2   2   2 
## 325 326 327 328 329 330 331 332 333 334 335 336 337 338 339 340 341 342 
##   2   2   2   2   1   1   1   2   2   2   2   2   2   2   2   2   2   2 
## 343 344 345 346 347 348 349 350 351 352 353 354 355 356 357 358 359 360 
##   1   1   1   1   1   2   2   2   2   1   1   2   2   2   3   3   3   3 
## 361 362 363 364 365 366 367 368 369 370 371 372 373 374 375 376 377 378 
##   3   3   3   3   3   3   3   4   3   3   3   3   3   3   3   3   3   3 
## 379 380 381 382 383 384 385 386 387 388 389 390 391 392 393 394 395 396 
##   3   3   3   3   3   3   3   3   3   3   3   3   3   3   3   3   3   3 
## 397 398 399 400 401 402 403 404 405 406 407 408 409 410 411 412 413 414 
##   3   3   3   3   3   3   3   3   3   3   3   3   3   4   4   4   4   4 
## 415 416 417 418 419 420 421 422 423 424 425 426 427 428 429 430 431 432 
##   4   4   4   4   4   4   3   3   3   4   4   4   4   4   4   4   4   4 
## 433 434 435 436 437 438 439 440 441 442 443 444 445 446 447 448 449 450 
##   4   4   4   4   4   4   4   3   3   3   3   3   3   4   3   3   3   3 
## 451 452 453 454 455 456 457 458 459 460 461 462 463 464 465 466 467 468 
##   4   3   3   3   4   4   4   4   3   3   3   3   3   3   3   3   4   3 
## 469 470 471 472 473 474 475 476 477 478 479 480 481 482 483 484 485 486 
##   3   3   3   3   3   3   3   3   3   3   3   3   3   3   3   3   3   3 
## 487 488 489 490 491 492 493 494 495 496 497 498 499 500 501 502 503 504 
##   3   3   3   3   3   3   3   1   1   1   1   1   1   1   1   2   2   2 
## 505 506 
##   2   2 
## 
## Within cluster sum of squares by cluster:
## [1] 395218.3 924118.8 181891.7 313208.7
##  (between_SS / total_SS =  90.6 %)
## 
## Available components:
## 
## [1] &quot;cluster&quot;      &quot;centers&quot;      &quot;totss&quot;        &quot;withinss&quot;    
## [5] &quot;tot.withinss&quot; &quot;betweenss&quot;    &quot;size&quot;         &quot;iter&quot;        
## [9] &quot;ifault&quot;</code></pre>
<p>Now I compare the results above and as I can see, the <code>snow</code> version isn’t that much different than the <code>lapply</code> version. The biggest problem in converting from <code>lapply</code> to one of the parallel operations is <strong>handling the data properly and efficently</strong>. In this example, it is easy. The dataset was in a package, so all I need to do was to load the package on all workers.</p>
<p>I will quote some coments on the function <code>clusterEvalQ</code> from the book where I am learning paralle R</p>
<blockquote>
<p>“clusterEvalQ() takes two arguments: the cluster object, and an expression that is evaluated on each of the workers. It returns the result from each of the workers in a list, which we don’t use here. I use a compound expression to load MASS and return NULL to avoid sending unnecessary data back to the master process. That isn’t a serious issue in this case, but it can be, so I often return NULL to be safe.” (<a href="http://shop.oreilly.com/product/0636920021421.do">Parallel R by Q. Ethan McCallum and Stephen Weston (O’Reilly). Copyright 2012 Q. Ethan McCallum and Stephen Weston, 978-1-449-30992-3.</a>)</p>
</blockquote>
</div>
<div class="footnotes">
<hr />
<ol>
<li id="fn1"><p>Don’t confuse these clusters with cluster objects and cluster workers<a href="#fnref1">↩</a></p></li>
</ol>
</div>



<!-- dynamically load mathjax for compatibility with self-contained -->
<script>
  (function () {
    var script = document.createElement("script");
    script.type = "text/javascript";
    script.src  = "https://cdn.mathjax.org/mathjax/latest/MathJax.js?config=TeX-AMS-MML_HTMLorMML";
    document.getElementsByTagName("head")[0].appendChild(script);
  })();
</script>

<h4>
<a href="http://mayweiwang.github.io/" class="Return">Return to homepage</a>
</h4>
</body>
</html>
