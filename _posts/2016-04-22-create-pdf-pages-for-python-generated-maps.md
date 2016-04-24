---
layout: post
title: "Create PDF pages for Python Generated maps"
description: ""
category: 
tags: []
---
{% include JB/setup %}



 


  <div tabindex="-1" id="notebook" class="border-box-sizing">
    <div class="container" id="notebook-container">

<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">
In&nbsp;[1]:
</div>
<div class="inner_cell">
    <div class="input_area">
<div class="highlight"><pre><span class="sd">&quot;&quot;&quot;</span>
<span class="sd">This is a demo of creating a pdf file with several pages,</span>
<span class="sd">as well as adding metadata and annotations to pdf files.</span>
<span class="sd">&quot;&quot;&quot;</span>

<span class="kn">import</span> <span class="nn">datetime</span>
<span class="kn">import</span> <span class="nn">numpy</span> <span class="kn">as</span> <span class="nn">np</span>
<span class="kn">from</span> <span class="nn">matplotlib.backends.backend_pdf</span> <span class="kn">import</span> <span class="n">PdfPages</span>
<span class="kn">import</span> <span class="nn">matplotlib.pyplot</span> <span class="kn">as</span> <span class="nn">plt</span>

<span class="c"># Create the PdfPages object to which we will save the pages:</span>
<span class="c"># The with statement makes sure that the PdfPages object is closed properly at</span>
<span class="c"># the end of the block, even if an Exception occurs.</span>
<span class="k">with</span> <span class="n">PdfPages</span><span class="p">(</span><span class="s">&#39;multipage_pdf.pdf&#39;</span><span class="p">)</span> <span class="k">as</span> <span class="n">pdf</span><span class="p">:</span>
    <span class="n">plt</span><span class="o">.</span><span class="n">figure</span><span class="p">(</span><span class="n">figsize</span><span class="o">=</span><span class="p">(</span><span class="mi">3</span><span class="p">,</span> <span class="mi">3</span><span class="p">))</span>
    
    <span class="n">plt</span><span class="o">.</span><span class="n">plot</span><span class="p">(</span><span class="nb">range</span><span class="p">(</span><span class="mi">7</span><span class="p">),</span> <span class="p">[</span><span class="mi">3</span><span class="p">,</span> <span class="mi">1</span><span class="p">,</span> <span class="mi">4</span><span class="p">,</span> <span class="mi">1</span><span class="p">,</span> <span class="mi">5</span><span class="p">,</span> <span class="mi">9</span><span class="p">,</span> <span class="mi">2</span><span class="p">],</span> <span class="s">&#39;r-o&#39;</span><span class="p">)</span>
    <span class="n">plt</span><span class="o">.</span><span class="n">title</span><span class="p">(</span><span class="s">&#39;Page One&#39;</span><span class="p">)</span>
    <span class="n">pdf</span><span class="o">.</span><span class="n">savefig</span><span class="p">()</span>  <span class="c"># saves the current figure into a pdf page</span>
    <span class="n">plt</span><span class="o">.</span><span class="n">close</span><span class="p">()</span>

    <span class="n">plt</span><span class="o">.</span><span class="n">rc</span><span class="p">(</span><span class="s">&#39;text&#39;</span><span class="p">,</span> <span class="n">usetex</span><span class="o">=</span><span class="bp">True</span><span class="p">)</span>
    <span class="n">plt</span><span class="o">.</span><span class="n">figure</span><span class="p">(</span><span class="n">figsize</span><span class="o">=</span><span class="p">(</span><span class="mi">8</span><span class="p">,</span> <span class="mi">6</span><span class="p">))</span>
    <span class="n">x</span> <span class="o">=</span> <span class="n">np</span><span class="o">.</span><span class="n">arange</span><span class="p">(</span><span class="mi">0</span><span class="p">,</span> <span class="mi">5</span><span class="p">,</span> <span class="mf">0.1</span><span class="p">)</span>
    <span class="n">plt</span><span class="o">.</span><span class="n">plot</span><span class="p">(</span><span class="n">x</span><span class="p">,</span> <span class="n">np</span><span class="o">.</span><span class="n">sin</span><span class="p">(</span><span class="n">x</span><span class="p">),</span> <span class="s">&#39;b-&#39;</span><span class="p">)</span>
    <span class="n">plt</span><span class="o">.</span><span class="n">title</span><span class="p">(</span><span class="s">&#39;Page Two&#39;</span><span class="p">)</span>
    <span class="c">#pdf.attach_note(&quot;plot of sin(x)&quot;)  # you can add a pdf note to</span>
                                       <span class="c"># attach metadata to a page</span>
    <span class="n">pdf</span><span class="o">.</span><span class="n">savefig</span><span class="p">()</span>
    <span class="n">plt</span><span class="o">.</span><span class="n">close</span><span class="p">()</span>

    <span class="n">plt</span><span class="o">.</span><span class="n">rc</span><span class="p">(</span><span class="s">&#39;text&#39;</span><span class="p">,</span> <span class="n">usetex</span><span class="o">=</span><span class="bp">False</span><span class="p">)</span>
    <span class="n">fig</span> <span class="o">=</span> <span class="n">plt</span><span class="o">.</span><span class="n">figure</span><span class="p">(</span><span class="n">figsize</span><span class="o">=</span><span class="p">(</span><span class="mi">4</span><span class="p">,</span> <span class="mi">5</span><span class="p">))</span>
    <span class="n">plt</span><span class="o">.</span><span class="n">plot</span><span class="p">(</span><span class="n">x</span><span class="p">,</span> <span class="n">x</span><span class="o">*</span><span class="n">x</span><span class="p">,</span> <span class="s">&#39;ko&#39;</span><span class="p">)</span>
    <span class="n">plt</span><span class="o">.</span><span class="n">title</span><span class="p">(</span><span class="s">&#39;Page Three&#39;</span><span class="p">)</span>
    <span class="n">pdf</span><span class="o">.</span><span class="n">savefig</span><span class="p">(</span><span class="n">fig</span><span class="p">)</span>  <span class="c"># or you can pass a Figure object to pdf.savefig</span>
    <span class="n">plt</span><span class="o">.</span><span class="n">close</span><span class="p">()</span>

    <span class="c"># We can also set the file&#39;s metadata via the PdfPages object:</span>
    <span class="n">d</span> <span class="o">=</span> <span class="n">pdf</span><span class="o">.</span><span class="n">infodict</span><span class="p">()</span>
    <span class="n">d</span><span class="p">[</span><span class="s">&#39;Title&#39;</span><span class="p">]</span> <span class="o">=</span> <span class="s">&#39;Multipage PDF Example&#39;</span>
    <span class="n">d</span><span class="p">[</span><span class="s">&#39;Author&#39;</span><span class="p">]</span> <span class="o">=</span> <span class="s">u&#39;Jouni K. Sepp</span><span class="se">\xe4</span><span class="s">nen&#39;</span>
    <span class="n">d</span><span class="p">[</span><span class="s">&#39;Subject&#39;</span><span class="p">]</span> <span class="o">=</span> <span class="s">&#39;How to create a multipage pdf file and set its metadata&#39;</span>
    <span class="n">d</span><span class="p">[</span><span class="s">&#39;Keywords&#39;</span><span class="p">]</span> <span class="o">=</span> <span class="s">&#39;PdfPages multipage keywords author title subject&#39;</span>
    <span class="n">d</span><span class="p">[</span><span class="s">&#39;CreationDate&#39;</span><span class="p">]</span> <span class="o">=</span> <span class="n">datetime</span><span class="o">.</span><span class="n">datetime</span><span class="p">(</span><span class="mi">2009</span><span class="p">,</span> <span class="mi">11</span><span class="p">,</span> <span class="mi">13</span><span class="p">)</span>
    <span class="n">d</span><span class="p">[</span><span class="s">&#39;ModDate&#39;</span><span class="p">]</span> <span class="o">=</span> <span class="n">datetime</span><span class="o">.</span><span class="n">datetime</span><span class="o">.</span><span class="n">today</span><span class="p">()</span>
</pre></div>

</div>
</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">
In&nbsp;[13]:
</div>
<div class="inner_cell">
    <div class="input_area">
<div class="highlight"><pre><span class="c"># cross-validation</span>
<span class="k">print</span><span class="p">(</span><span class="n">__doc__</span><span class="p">)</span>


<span class="kn">import</span> <span class="nn">numpy</span> <span class="kn">as</span> <span class="nn">np</span>
<span class="kn">import</span> <span class="nn">sklearn</span>
<span class="kn">from</span> <span class="nn">sklearn</span> <span class="kn">import</span> <span class="n">cross_validation</span><span class="p">,</span> <span class="n">datasets</span><span class="p">,</span> <span class="n">svm</span>

<span class="n">digits</span> <span class="o">=</span> <span class="n">datasets</span><span class="o">.</span><span class="n">load_digits</span><span class="p">()</span>
<span class="n">X</span> <span class="o">=</span> <span class="n">digits</span><span class="o">.</span><span class="n">data</span>
<span class="n">y</span> <span class="o">=</span> <span class="n">digits</span><span class="o">.</span><span class="n">target</span>

<span class="n">svc</span> <span class="o">=</span> <span class="n">svm</span><span class="o">.</span><span class="n">SVC</span><span class="p">(</span><span class="n">kernel</span><span class="o">=</span><span class="s">&#39;linear&#39;</span><span class="p">)</span>
<span class="n">C_s</span> <span class="o">=</span> <span class="n">np</span><span class="o">.</span><span class="n">logspace</span><span class="p">(</span><span class="o">-</span><span class="mi">10</span><span class="p">,</span> <span class="mi">0</span><span class="p">,</span> <span class="mi">10</span><span class="p">)</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area"><div class="prompt"></div>
<div class="output_subarea output_stream output_stdout output_text">
<pre>
Automatically created module for IPython interactive environment

</pre>
</div>
</div>

</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">
In&nbsp;[22]:
</div>
<div class="inner_cell">
    <div class="input_area">
<div class="highlight"><pre><span class="k">print</span> <span class="n">X</span><span class="o">.</span><span class="n">shape</span><span class="p">,</span> <span class="n">y</span><span class="o">.</span><span class="n">shape</span><span class="p">,</span> <span class="n">digits</span><span class="o">.</span><span class="n">images</span><span class="o">.</span><span class="n">shape</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area"><div class="prompt"></div>
<div class="output_subarea output_stream output_stdout output_text">
<pre>
(1797, 64) (1797,) (1797, 8, 8)

</pre>
</div>
</div>

</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">
In&nbsp;[10]:
</div>
<div class="inner_cell">
    <div class="input_area">
<div class="highlight"><pre><span class="n">scores</span> <span class="o">=</span> <span class="nb">list</span><span class="p">()</span>
<span class="n">scores_std</span> <span class="o">=</span> <span class="nb">list</span><span class="p">()</span>
<span class="k">for</span> <span class="n">C</span> <span class="ow">in</span> <span class="n">C_s</span><span class="p">:</span>
    <span class="n">svc</span><span class="o">.</span><span class="n">C</span> <span class="o">=</span> <span class="n">C</span>
    <span class="n">this_scores</span> <span class="o">=</span> <span class="n">cross_validation</span><span class="o">.</span><span class="n">cross_val_score</span><span class="p">(</span><span class="n">svc</span><span class="p">,</span> <span class="n">X</span><span class="p">,</span> <span class="n">y</span><span class="p">,</span> <span class="n">n_jobs</span><span class="o">=</span><span class="mi">1</span><span class="p">)</span>
    <span class="n">scores</span><span class="o">.</span><span class="n">append</span><span class="p">(</span><span class="n">np</span><span class="o">.</span><span class="n">mean</span><span class="p">(</span><span class="n">this_scores</span><span class="p">))</span>
    <span class="n">scores_std</span><span class="o">.</span><span class="n">append</span><span class="p">(</span><span class="n">np</span><span class="o">.</span><span class="n">std</span><span class="p">(</span><span class="n">this_scores</span><span class="p">))</span>
</pre></div>

</div>
</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">
In&nbsp;[20]:
</div>
<div class="inner_cell">
    <div class="input_area">
<div class="highlight"><pre><span class="k">with</span> <span class="n">PdfPages</span><span class="p">(</span><span class="s">&#39;multipage_pdf.pdf&#39;</span><span class="p">)</span> <span class="k">as</span> <span class="n">pdf</span><span class="p">:</span>
    <span class="n">plt</span><span class="o">.</span><span class="n">figure</span><span class="p">(</span><span class="n">figsize</span><span class="o">=</span><span class="p">(</span><span class="mi">3</span><span class="p">,</span> <span class="mi">3</span><span class="p">))</span>
    
    <span class="n">plt</span><span class="o">.</span><span class="n">plot</span><span class="p">(</span><span class="n">C_s</span><span class="p">,</span> <span class="s">&#39;r-o&#39;</span><span class="p">)</span>
    <span class="n">plt</span><span class="o">.</span><span class="n">title</span><span class="p">(</span><span class="s">&#39;Page Five&#39;</span><span class="p">)</span>
    <span class="n">pdf</span><span class="o">.</span><span class="n">savefig</span><span class="p">()</span>  <span class="c"># saves the current figure into a pdf page</span>
    <span class="n">plt</span><span class="o">.</span><span class="n">close</span><span class="p">()</span>
    
    <span class="n">plt</span><span class="o">.</span><span class="n">rc</span><span class="p">(</span><span class="s">&#39;text&#39;</span><span class="p">,</span> <span class="n">usetex</span><span class="o">=</span><span class="bp">True</span><span class="p">)</span>

    <span class="n">plt</span><span class="o">.</span><span class="n">figure</span><span class="p">(</span><span class="n">figsize</span><span class="o">=</span><span class="p">(</span><span class="mi">8</span><span class="p">,</span> <span class="mi">6</span><span class="p">))</span>
    
    <span class="n">plt</span><span class="o">.</span><span class="n">semilogx</span><span class="p">(</span><span class="n">C_s</span><span class="p">,</span> <span class="n">scores</span><span class="p">)</span>
    <span class="n">plt</span><span class="o">.</span><span class="n">semilogx</span><span class="p">(</span><span class="n">C_s</span><span class="p">,</span> <span class="n">np</span><span class="o">.</span><span class="n">array</span><span class="p">(</span><span class="n">scores</span><span class="p">)</span> <span class="o">+</span> <span class="n">np</span><span class="o">.</span><span class="n">array</span><span class="p">(</span><span class="n">scores_std</span><span class="p">),</span> <span class="s">&#39;b--&#39;</span><span class="p">)</span>
    <span class="n">plt</span><span class="o">.</span><span class="n">semilogx</span><span class="p">(</span><span class="n">C_s</span><span class="p">,</span> <span class="n">np</span><span class="o">.</span><span class="n">array</span><span class="p">(</span><span class="n">scores</span><span class="p">)</span> <span class="o">-</span> <span class="n">np</span><span class="o">.</span><span class="n">array</span><span class="p">(</span><span class="n">scores_std</span><span class="p">),</span> <span class="s">&#39;b--&#39;</span><span class="p">)</span>
    <span class="n">locs</span><span class="p">,</span> <span class="n">labels</span> <span class="o">=</span> <span class="n">plt</span><span class="o">.</span><span class="n">yticks</span><span class="p">()</span>
    <span class="n">plt</span><span class="o">.</span><span class="n">yticks</span><span class="p">(</span><span class="n">locs</span><span class="p">,</span> <span class="nb">list</span><span class="p">(</span><span class="nb">map</span><span class="p">(</span><span class="k">lambda</span> <span class="n">x</span><span class="p">:</span> <span class="s">&quot;</span><span class="si">%g</span><span class="s">&quot;</span> <span class="o">%</span> <span class="n">x</span><span class="p">,</span> <span class="n">locs</span><span class="p">)))</span>
    <span class="n">plt</span><span class="o">.</span><span class="n">ylabel</span><span class="p">(</span><span class="s">&#39;CV score&#39;</span><span class="p">)</span>
    <span class="n">plt</span><span class="o">.</span><span class="n">xlabel</span><span class="p">(</span><span class="s">&#39;Parameter C&#39;</span><span class="p">)</span>
    <span class="n">plt</span><span class="o">.</span><span class="n">ylim</span><span class="p">(</span><span class="mi">0</span><span class="p">,</span> <span class="mf">1.1</span><span class="p">)</span>
    
    <span class="n">plt</span><span class="o">.</span><span class="n">title</span><span class="p">(</span><span class="s">&#39;Page Sive&#39;</span><span class="p">)</span>
    <span class="n">pdf</span><span class="o">.</span><span class="n">savefig</span><span class="p">()</span>  <span class="c"># or you can pass a Figure object to pdf.savefig</span>
    <span class="n">plt</span><span class="o">.</span><span class="n">close</span><span class="p">()</span>

  
   
</pre></div>

</div>
</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">
In&nbsp;[]:
</div>
<div class="inner_cell">
    <div class="input_area">
<div class="highlight"><pre> 
</pre></div>

</div>
</div>
</div>

</div>
    </div>
  </div>

