---
layout: post
title: "A tutorial on how to design a simple prediction model"
description: ""
category: "Python"
tags: []
---
{% include JB/setup %}



  <div tabindex="-1" id="notebook" class="border-box-sizing">
    <div class="container" id="notebook-container">

<div class="cell border-box-sizing text_cell rendered">
<div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<h3 id="this-blog-aims-to-give-a-tutorial-on-how-to-write-a-prediction-model-in-python-in-less-than-a-breakfast-time-">This blog aims to give a tutorial on &quot;how to write a prediction model in Python in less than a breakfast time&quot;.</h3>
<h3 id="most-of-the-top-data-scientists-and-kagglers-build-their-first-effective-model-quickly-and-submit-the-simplest-solution-provides-a-bench-mark-solution-to-optimize-">Most of the top data scientists and Kagglers build their first effective model quickly and submit. The simplest solution provides a bench mark solution to optimize.</h3>
<h3 id="this-tutorial-is-to-show-you-how-to-predict-the-courtry-of-destination-a-user-is-going-to-book-on-airbnb-">This tutorial is to show you how to predict the courtry of destination a user is going to book on Airbnb.</h3>
<h3 id="i-will-divide-the-whole-job-into-small-tasks-with-each-giving-both-the-explaination-and-the-code-demo-without-further-ado-let-s-rock-">I will divide the whole job into small tasks, with each giving both the explaination and the code demo. Without further ado, let&#39;s rock!</h3>
<h3 id="the-tasks-are-">The tasks are :</h3>
<blockquote>
<ul>
<li>Data exploration</li>
<li>Data cleaning</li>
<li>Data modelling </li>
</ul>
</blockquote>
</div>
</div>
</div>
<div class="cell border-box-sizing text_cell rendered">
<div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<h4 id="step-1-data-exploration">Step 1 : Data Exploration</h4>
<ul>
<li>1.1 Load libraries</li>
<li>1.2 Load data</li>
<li>1.3 View data features/columns and summary</li>
<li>1.4 Get to know your variables : categorical, numerical, string, ID, target</li>
<li>1.5 First visualization of the data</li>
</ul>
</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">
In&nbsp;[1]:
</div>
<div class="inner_cell">
    <div class="input_area">
<div class="highlight"><pre><span class="c"># 1.1 Load libraries</span>
<span class="kn">import</span> <span class="nn">pandas</span> <span class="kn">as</span> <span class="nn">pd</span>
<span class="kn">from</span> <span class="nn">pandas</span> <span class="kn">import</span> <span class="n">Series</span><span class="p">,</span><span class="n">DataFrame</span>

<span class="c"># numpy, matplotlib, seaborn</span>
<span class="kn">import</span> <span class="nn">numpy</span> <span class="kn">as</span> <span class="nn">np</span>
<span class="kn">import</span> <span class="nn">matplotlib.pyplot</span> <span class="kn">as</span> <span class="nn">plt</span>
<span class="kn">import</span> <span class="nn">seaborn</span> <span class="kn">as</span> <span class="nn">sns</span>
<span class="n">sns</span><span class="o">.</span><span class="n">set_style</span><span class="p">(</span><span class="s">&#39;whitegrid&#39;</span><span class="p">)</span>
<span class="o">%</span><span class="k">matplotlib</span> <span class="n">inline</span>

<span class="c"># machine learning</span>
<span class="kn">from</span> <span class="nn">sklearn.linear_model</span> <span class="kn">import</span> <span class="n">LogisticRegression</span>
<span class="kn">from</span> <span class="nn">sklearn.svm</span> <span class="kn">import</span> <span class="n">SVC</span><span class="p">,</span> <span class="n">LinearSVC</span>
<span class="kn">from</span> <span class="nn">sklearn.ensemble</span> <span class="kn">import</span> <span class="n">RandomForestClassifier</span>
<span class="kn">from</span> <span class="nn">sklearn.neighbors</span> <span class="kn">import</span> <span class="n">KNeighborsClassifier</span>
<span class="kn">from</span> <span class="nn">sklearn.naive_bayes</span> <span class="kn">import</span> <span class="n">GaussianNB</span>
<span class="kn">from</span> <span class="nn">sklearn</span> <span class="kn">import</span> <span class="n">cross_validation</span>
<span class="kn">import</span> <span class="nn">xgboost</span> <span class="kn">as</span> <span class="nn">xgb</span>
</pre></div>

</div>
</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">
In&nbsp;[2]:
</div>
<div class="inner_cell">
    <div class="input_area">
<div class="highlight"><pre><span class="c"># 1.2 Load data</span>
<span class="n">train</span> <span class="o">=</span> <span class="n">pd</span><span class="o">.</span><span class="n">read_csv</span><span class="p">(</span><span class="s">&#39;Kaggle data comp 1/input/train_users_2.csv&#39;</span><span class="p">)</span>
<span class="n">test</span> <span class="o">=</span> <span class="n">pd</span><span class="o">.</span><span class="n">read_csv</span><span class="p">(</span><span class="s">&#39;Kaggle data comp 1/input/test_users.csv&#39;</span><span class="p">)</span>
<span class="n">train</span><span class="p">[</span><span class="s">&#39;Type&#39;</span><span class="p">]</span> <span class="o">=</span> <span class="s">&#39;Train&#39;</span> <span class="c">#Create a flag for Train and Test Data set</span>
<span class="n">test</span><span class="p">[</span><span class="s">&#39;Type&#39;</span><span class="p">]</span> <span class="o">=</span> <span class="s">&#39;Test&#39;</span>
<span class="n">fullData</span> <span class="o">=</span> <span class="n">pd</span><span class="o">.</span><span class="n">concat</span><span class="p">([</span><span class="n">train</span><span class="p">,</span><span class="n">test</span><span class="p">],</span><span class="n">axis</span><span class="o">=</span><span class="mi">0</span><span class="p">)</span> <span class="c"># Combined both Train and Test Data set</span>
</pre></div>

</div>
</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">
In&nbsp;[3]:
</div>
<div class="inner_cell">
    <div class="input_area">
<div class="highlight"><pre><span class="k">print</span> <span class="n">train</span><span class="o">.</span><span class="n">shape</span><span class="p">,</span> <span class="n">test</span><span class="o">.</span><span class="n">shape</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area"><div class="prompt"></div>
<div class="output_subarea output_stream output_stdout output_text">
<pre>
(213451, 17) (62096, 16)

</pre>
</div>
</div>

</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">
In&nbsp;[4]:
</div>
<div class="inner_cell">
    <div class="input_area">
<div class="highlight"><pre><span class="c"># 1.3 View the column names / summary of the dataset</span>
<span class="k">print</span> <span class="s">&#39;</span><span class="se">\n</span><span class="s">------------------------------------------------------------------</span><span class="se">\n</span><span class="s">&#39;</span>
<span class="k">print</span> <span class="s">&#39;Information of our data:&#39;</span><span class="p">,</span> <span class="n">fullData</span><span class="o">.</span><span class="n">info</span><span class="p">()</span>
<span class="k">print</span> <span class="s">&#39;</span><span class="se">\n</span><span class="s">------------------------------------------------------------------</span><span class="se">\n</span><span class="s">&#39;</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area"><div class="prompt"></div>
<div class="output_subarea output_stream output_stdout output_text">
<pre>

------------------------------------------------------------------

Information of our data:&lt;class &apos;pandas.core.frame.DataFrame&apos;&gt;
Int64Index: 275547 entries, 0 to 62095
Data columns (total 17 columns):
Type                       275547 non-null object
affiliate_channel          275547 non-null object
affiliate_provider         275547 non-null object
age                        158681 non-null float64
country_destination        213451 non-null object
date_account_created       275547 non-null object
date_first_booking         88908 non-null object
first_affiliate_tracked    269462 non-null object
first_browser              275547 non-null object
first_device_type          275547 non-null object
gender                     275547 non-null object
id                         275547 non-null object
language                   275547 non-null object
signup_app                 275547 non-null object
signup_flow                275547 non-null int64
signup_method              275547 non-null object
timestamp_first_active     275547 non-null int64
dtypes: float64(1), int64(2), object(14)
memory usage: 37.8+ MB
 None

------------------------------------------------------------------


</pre>
</div>
</div>

</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">
In&nbsp;[5]:
</div>
<div class="inner_cell">
    <div class="input_area">
<div class="highlight"><pre><span class="c"># 1.4 Get to know your variables</span>
<span class="c"># Check the data types of all variables (or columns if you want)</span>
<span class="n">fullData</span><span class="o">.</span><span class="n">dtypes</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area"><div class="prompt output_prompt">
    Out[5]:</div>


<div class="output_text output_subarea output_pyout">
<pre>
Type                        object
affiliate_channel           object
affiliate_provider          object
age                        float64
country_destination         object
date_account_created        object
date_first_booking          object
first_affiliate_tracked     object
first_browser               object
first_device_type           object
gender                      object
id                          object
language                    object
signup_app                  object
signup_flow                  int64
signup_method               object
timestamp_first_active       int64
dtype: object
</pre>
</div>

</div>

</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">
In&nbsp;[6]:
</div>
<div class="inner_cell">
    <div class="input_area">
<div class="highlight"><pre><span class="c"># 1.5 First Visualization of the data</span>
<span class="c"># Plot the distribution of the labels</span>
<span class="n">fig</span><span class="p">,</span> <span class="p">(</span><span class="n">axis1</span><span class="p">,</span> <span class="n">axis2</span><span class="p">)</span> <span class="o">=</span> <span class="n">plt</span><span class="o">.</span><span class="n">subplots</span><span class="p">(</span><span class="mi">1</span><span class="p">,</span><span class="mi">2</span><span class="p">,</span><span class="n">figsize</span><span class="o">=</span><span class="p">(</span><span class="mi">8</span><span class="p">,</span><span class="mi">4</span><span class="p">))</span>
<span class="n">sns</span><span class="o">.</span><span class="n">countplot</span><span class="p">(</span><span class="n">x</span><span class="o">=</span><span class="s">&#39;country_destination&#39;</span><span class="p">,</span> <span class="n">data</span><span class="o">=</span><span class="n">fullData</span><span class="p">,</span> <span class="n">palette</span><span class="o">=</span><span class="s">&quot;husl&quot;</span><span class="p">,</span> <span class="n">ax</span> <span class="o">=</span> <span class="n">axis1</span><span class="p">)</span>
<span class="n">sns</span><span class="o">.</span><span class="n">countplot</span><span class="p">(</span><span class="n">x</span><span class="o">=</span><span class="s">&#39;country_destination&#39;</span><span class="p">,</span> <span class="n">data</span><span class="o">=</span><span class="n">train</span><span class="p">,</span> <span class="n">palette</span><span class="o">=</span><span class="s">&quot;husl&quot;</span><span class="p">,</span> <span class="n">ax</span> <span class="o">=</span> <span class="n">axis2</span><span class="p">)</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area"><div class="prompt output_prompt">
    Out[6]:</div>


<div class="output_text output_subarea output_pyout">
<pre>
&lt;matplotlib.axes._subplots.AxesSubplot at 0x10d379cd0&gt;
</pre>
</div>

</div>

<div class="output_area"><div class="prompt"></div>


<div class="output_png output_subarea ">
<img src="data:image/png;base64,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
LQE2AhND01OAu4BewEJ3X17N7RKJkeJZpD5Ue0QgM/kw17F56s0B5uSUbQDOyFP3SeDILuqiiBRJ
8SzS8xVzZ0ERERGpU0oEREREIqZEQEREJGJKBERERCKmREBERCRiSgREREQipkRAREQkYkoERERE
IqZEQEREJGJKBERERCKmREBERCRiSgREREQipkRAREQkYkoEREREIqZEQEREJGJKBERERCKmREBE
RCRiSgREREQipkRAREQkYkoEREREIqZEQEREJGJKBERERCKmREBERCRiSgREREQitnstPtTMhgIp
4CPAVuCO8P9W4AJ3T5vZucBkYDMww90fNLN+wDxgCNAOTHL31WY2Brg+1F3k7tOrvU0iMVIsi/R8
VR8RMLPewC3AW0ADcC0wzd3HheWTzWwfYCowFjgRuMLMGoHzgGdC3TuBy0KzNwNnu/vRwGgzG1nN
bRKJkWJZpD7U4tTA94DZwF/D8mHuvji8/jkwHjgcWOrum9x9HfAicChwFLAg1F0AjDezJqDR3VeE
8oWhDRGpLMWySB2oaiJgZp8BXnX3RaGoIfyX0Q4MAgYCbxQoX9dJWXa5iFSIYlmkflR7jsBngbSZ
jQdGAnNJzhFmDATWkuwMmrLKm/KU5yvLbqNTra2tDC1jA1pbW2lvbwdg5cqVZX2B2W2I9FDdJpZ3
RSYWy43l7DZEeqqqJgLufkzmtZk9CkwBvmdmx7j748AE4GFgGTDTzPoAfYFDSCYfLQVOApaHuovd
vd3MOsxsf2AFcAJw+c760tLSwqrHni55G1paWmhubgagqamJ554ouYnt2hDpzlKpVN7y7hTLuyIT
i+XGcnYbIt1doXiuyVUDWdLAV4DbwgSiZ4F7w0zjWcASktMX09x9o5nNBuaa2RJgIzAxtDMFuAvo
BSx09+XV3hCRyCmWRXqomiUC7n5c1uKxed6fA8zJKdsAnJGn7pPAkV3cRREpgmJZpGfTDYVEREQi
pkRAREQkYkoEREREIqZEQEREJGJKBERERCKmREBERCRiSgREREQipkRAREQkYkoEREREIqZEQERE
JGJKBERERCKmREBERCRiSgREREQipkRAREQkYkoEREREIqZEQEREJGJKBERERCKmREBERCRiSgRE
REQipkRAREQkYkoEREREIqZEQEREJGJKBERERCKmREBERCRiu1fzw8ysN/BDYD+gDzAD+CNwB7AV
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
"
>
</div>

</div>

</div>
</div>

</div>
<div class="cell border-box-sizing text_cell rendered">
<div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<h4 id="step-2-data-cleaning">Step 2 : Data Cleaning</h4>
<ul>
<li>1.1 Drop out unnecessary variables</li>
<li>1.2 Find out all categorical variables and process them one by one (loop)<ul>
<li>1.2.1 Visualze the distribution of the variable values</li>
<li>1.2.2 (optional) Date-type variable have to be split </li>
<li>1.2.3 (optional) Fill NaN values with median values</li>
<li>1.2.4 (optional) Make sure the data type of newly created variables is justified, e.g., &#39;Year&#39;, is an &#39;int&#39; instead of &#39;float&#39; type</li>
<li>1.2.5 (optional) Binary process (&#39;one value&#39; versus &#39;non- one value&#39;)</li>
<li>1.2.6 Look for new insights due to the use of new variables</li>
</ul>
</li>
<li>1.3 Convert any remaining non-numerical variables to numerical</li>
<li>1.4 Particular process of some important numerical variables, e.g., age</li>
</ul>
</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">
In&nbsp;[7]:
</div>
<div class="inner_cell">
    <div class="input_area">
<div class="highlight"><pre><span class="c"># 1.1 Drop unecessary columns, these columns won&#39;t be useful in analysis and prediction</span>
<span class="n">fullData</span> <span class="o">=</span> <span class="n">fullData</span><span class="o">.</span><span class="n">drop</span><span class="p">([</span><span class="s">&#39;date_account_created&#39;</span><span class="p">,</span> <span class="s">&#39;timestamp_first_active&#39;</span><span class="p">],</span> <span class="n">axis</span> <span class="o">=</span> <span class="mi">1</span><span class="p">)</span>
</pre></div>

</div>
</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">
In&nbsp;[8]:
</div>
<div class="inner_cell">
    <div class="input_area">
<div class="highlight"><pre><span class="c"># 1.2 Find out all categorical variables (choose those numerical variables, just change &#39;o&#39; to &#39;int64&#39;)</span>
<span class="n">colType</span> <span class="o">=</span> <span class="n">fullData</span><span class="o">.</span><span class="n">columns</span><span class="o">.</span><span class="n">to_series</span><span class="p">()</span><span class="o">.</span><span class="n">groupby</span><span class="p">(</span><span class="n">fullData</span><span class="o">.</span><span class="n">dtypes</span> <span class="o">==</span> <span class="s">&#39;O&#39;</span><span class="p">)</span><span class="o">.</span><span class="n">groups</span> 
<span class="n">colType</span><span class="p">[</span><span class="bp">True</span><span class="p">]</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area"><div class="prompt output_prompt">
    Out[8]:</div>


<div class="output_text output_subarea output_pyout">
<pre>
[&apos;Type&apos;,
 &apos;affiliate_channel&apos;,
 &apos;affiliate_provider&apos;,
 &apos;country_destination&apos;,
 &apos;date_first_booking&apos;,
 &apos;first_affiliate_tracked&apos;,
 &apos;first_browser&apos;,
 &apos;first_device_type&apos;,
 &apos;gender&apos;,
 &apos;id&apos;,
 &apos;language&apos;,
 &apos;signup_app&apos;,
 &apos;signup_method&apos;]
</pre>
</div>

</div>

</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">
In&nbsp;[9]:
</div>
<div class="inner_cell">
    <div class="input_area">
<div class="highlight"><pre><span class="k">def</span> <span class="nf">FillNaNRandom</span><span class="p">(</span><span class="n">df</span><span class="p">,</span><span class="n">columnName</span><span class="p">):</span>
    <span class="n">count_col</span> <span class="o">=</span> <span class="nb">len</span><span class="p">(</span><span class="n">np</span><span class="o">.</span><span class="n">unique</span><span class="p">(</span><span class="n">df</span><span class="p">[</span><span class="n">columnName</span><span class="p">]</span><span class="o">.</span><span class="n">value_counts</span><span class="p">()))</span>
    <span class="n">count_nan</span> <span class="o">=</span> <span class="n">df</span><span class="p">[</span><span class="n">columnName</span><span class="p">]</span><span class="o">.</span><span class="n">isnull</span><span class="p">()</span><span class="o">.</span><span class="n">sum</span><span class="p">()</span>
    <span class="n">range_col</span> <span class="o">=</span> <span class="n">df</span><span class="p">[</span><span class="n">columnName</span><span class="p">]</span><span class="o">.</span><span class="n">value_counts</span><span class="p">()</span><span class="o">.</span><span class="n">index</span>
    <span class="k">print</span> <span class="s">&quot;There are </span><span class="si">%s</span><span class="s"> different values in the list of :</span><span class="se">\n</span><span class="si">%s</span><span class="s">&quot;</span> <span class="o">%</span> <span class="p">(</span><span class="nb">len</span><span class="p">(</span><span class="n">range_col</span><span class="p">),</span> <span class="n">range_col</span><span class="p">)</span>

    <span class="k">if</span> <span class="n">count_nan</span> <span class="o">&gt;</span> <span class="mi">0</span><span class="p">:</span>
        <span class="n">rand</span> <span class="o">=</span> <span class="n">np</span><span class="o">.</span><span class="n">random</span><span class="o">.</span><span class="n">randint</span><span class="p">(</span><span class="mi">0</span><span class="p">,</span> <span class="n">count_col</span><span class="p">,</span> <span class="n">size</span> <span class="o">=</span> <span class="n">count_nan</span><span class="p">)</span>
        
        <span class="c"># Create a random selection of the 7 possible categorical values for all &#39;count_ran_department&#39; (i.e., 6085) &#39;NaN&#39; records</span>
        <span class="n">RandforNaN</span> <span class="o">=</span> <span class="n">range_col</span><span class="p">[</span><span class="n">rand</span><span class="p">]</span>

        <span class="c"># Find indexes for the NaN values</span>
        <span class="n">NaNIndex</span> <span class="o">=</span> <span class="n">df</span><span class="p">[</span><span class="n">columnName</span><span class="p">]</span> <span class="o">!=</span> <span class="n">df</span><span class="p">[</span><span class="n">columnName</span><span class="p">]</span>
        <span class="n">df</span><span class="p">[</span><span class="n">columnName</span><span class="p">][</span><span class="n">NaNIndex</span><span class="p">]</span> <span class="o">=</span> <span class="n">RandforNaN</span>
        <span class="k">print</span> <span class="s">&#39;There are : </span><span class="si">%s</span><span class="s"> NaN values in this variable!&#39;</span> <span class="o">%</span> <span class="n">count_nan</span>
    <span class="k">else</span><span class="p">:</span>
        <span class="k">print</span> <span class="s">&#39;There is no NaN values for this variable!&#39;</span>
    <span class="k">return</span> <span class="n">df</span>
</pre></div>

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
<div class="highlight"><pre><span class="c"># There are 12 original categorical variables in total</span>
<span class="c"># 1. &#39;affiliate_channel&#39; variable</span>
<span class="c"># (1) Visualization</span>
<span class="n">fig</span><span class="p">,</span> <span class="n">axis1</span> <span class="o">=</span> <span class="n">plt</span><span class="o">.</span><span class="n">subplots</span><span class="p">(</span><span class="mi">1</span><span class="p">,</span><span class="mi">1</span><span class="p">,</span><span class="n">sharex</span><span class="o">=</span><span class="bp">True</span><span class="p">,</span><span class="n">figsize</span><span class="o">=</span><span class="p">(</span><span class="mi">8</span><span class="p">,</span><span class="mi">4</span><span class="p">))</span>
<span class="n">sns</span><span class="o">.</span><span class="n">countplot</span><span class="p">(</span><span class="n">x</span><span class="o">=</span><span class="s">&#39;affiliate_channel&#39;</span><span class="p">,</span> <span class="n">data</span><span class="o">=</span><span class="n">fullData</span><span class="p">,</span> <span class="n">palette</span><span class="o">=</span><span class="s">&quot;husl&quot;</span><span class="p">,</span> <span class="n">ax</span><span class="o">=</span><span class="n">axis1</span><span class="p">)</span>

<span class="c"># (2) Fill NaN values randomly</span>
<span class="n">fullData</span> <span class="o">=</span> <span class="n">FillNaNRandom</span><span class="p">(</span><span class="n">fullData</span><span class="p">,</span> <span class="s">&#39;affiliate_channel&#39;</span><span class="p">)</span>

<span class="c"># (3) Binary process</span>
<span class="n">fullData</span><span class="p">[</span><span class="s">&quot;affiliate_channel&quot;</span><span class="p">]</span> <span class="o">=</span> <span class="p">(</span><span class="n">fullData</span><span class="p">[</span><span class="s">&quot;affiliate_channel&quot;</span><span class="p">]</span> <span class="o">==</span> <span class="s">&#39;direct&#39;</span><span class="p">)</span><span class="o">.</span><span class="n">astype</span><span class="p">(</span><span class="nb">int</span><span class="p">)</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area"><div class="prompt"></div>
<div class="output_subarea output_stream output_stdout output_text">
<pre>
There are 8 different values in the list of :
Index([u&apos;direct&apos;, u&apos;sem-brand&apos;, u&apos;sem-non-brand&apos;, u&apos;seo&apos;, u&apos;other&apos;, u&apos;api&apos;, u&apos;content&apos;, u&apos;remarketing&apos;], dtype=&apos;object&apos;)
There is no NaN values for this variable!

</pre>
</div>
</div>

<div class="output_area"><div class="prompt"></div>


<div class="output_png output_subarea ">
<img src="data:image/png;base64,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
cf8LFZl1vWlGFO0AAAAASUVORK5CYII=
"
>
</div>

</div>

</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">
In&nbsp;[11]:
</div>
<div class="inner_cell">
    <div class="input_area">
<div class="highlight"><pre><span class="c"># There are 12 categorical variables in total</span>
<span class="c"># 2. &#39;affiliate_provider&#39; variable</span>
<span class="c"># (1) Visualization</span>
<span class="n">fig</span><span class="p">,</span> <span class="n">axis1</span> <span class="o">=</span> <span class="n">plt</span><span class="o">.</span><span class="n">subplots</span><span class="p">(</span><span class="mi">1</span><span class="p">,</span><span class="mi">1</span><span class="p">,</span><span class="n">sharex</span><span class="o">=</span><span class="bp">True</span><span class="p">,</span><span class="n">figsize</span><span class="o">=</span><span class="p">(</span><span class="mi">8</span><span class="p">,</span><span class="mi">4</span><span class="p">))</span>
<span class="n">sns</span><span class="o">.</span><span class="n">countplot</span><span class="p">(</span><span class="n">x</span><span class="o">=</span><span class="s">&#39;affiliate_provider&#39;</span><span class="p">,</span> <span class="n">data</span><span class="o">=</span><span class="n">fullData</span><span class="p">,</span> <span class="n">palette</span><span class="o">=</span><span class="s">&quot;husl&quot;</span><span class="p">,</span> <span class="n">ax</span><span class="o">=</span><span class="n">axis1</span><span class="p">)</span>

<span class="c"># (2) Fill NaN values randomly</span>
<span class="n">fullData</span> <span class="o">=</span> <span class="n">FillNaNRandom</span><span class="p">(</span><span class="n">fullData</span><span class="p">,</span> <span class="s">&#39;affiliate_provider&#39;</span><span class="p">)</span>

<span class="c"># (3) Binary process</span>
<span class="n">fullData</span><span class="p">[</span><span class="s">&quot;affiliate_provider&quot;</span><span class="p">]</span> <span class="o">=</span> <span class="p">(</span><span class="n">fullData</span><span class="p">[</span><span class="s">&quot;affiliate_provider&quot;</span><span class="p">]</span> <span class="o">==</span> <span class="s">&#39;direct&#39;</span><span class="p">)</span><span class="o">.</span><span class="n">astype</span><span class="p">(</span><span class="nb">int</span><span class="p">)</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area"><div class="prompt"></div>
<div class="output_subarea output_stream output_stdout output_text">
<pre>
There are 18 different values in the list of :
Index([u&apos;direct&apos;, u&apos;google&apos;, u&apos;other&apos;, u&apos;facebook&apos;, u&apos;bing&apos;, u&apos;craigslist&apos;, u&apos;padmapper&apos;, u&apos;vast&apos;, u&apos;yahoo&apos;, u&apos;facebook-open-graph&apos;, u&apos;gsp&apos;, u&apos;meetup&apos;, u&apos;email-marketing&apos;, u&apos;naver&apos;, u&apos;baidu&apos;, u&apos;yandex&apos;, u&apos;wayn&apos;, u&apos;daum&apos;], dtype=&apos;object&apos;)
There is no NaN values for this variable!

</pre>
</div>
</div>

<div class="output_area"><div class="prompt"></div>


<div class="output_png output_subarea ">
<img src="data:image/png;base64,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
AAAASUVORK5CYII=
"
>
</div>

</div>

</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">
In&nbsp;[12]:
</div>
<div class="inner_cell">
    <div class="input_area">
<div class="highlight"><pre><span class="c"># There are 12 categorical variables in total</span>
<span class="c"># 3. &#39;country_destination&#39; variable</span>
<span class="c"># (1) Visualization</span>
<span class="n">fig</span><span class="p">,</span> <span class="n">axis1</span> <span class="o">=</span> <span class="n">plt</span><span class="o">.</span><span class="n">subplots</span><span class="p">(</span><span class="mi">1</span><span class="p">,</span><span class="mi">1</span><span class="p">,</span><span class="n">sharex</span><span class="o">=</span><span class="bp">True</span><span class="p">,</span><span class="n">figsize</span><span class="o">=</span><span class="p">(</span><span class="mi">8</span><span class="p">,</span><span class="mi">4</span><span class="p">))</span>
<span class="n">sns</span><span class="o">.</span><span class="n">countplot</span><span class="p">(</span><span class="n">x</span><span class="o">=</span><span class="s">&#39;country_destination&#39;</span><span class="p">,</span> <span class="n">data</span><span class="o">=</span><span class="n">fullData</span><span class="p">,</span> <span class="n">palette</span><span class="o">=</span><span class="s">&quot;husl&quot;</span><span class="p">,</span> <span class="n">ax</span><span class="o">=</span><span class="n">axis1</span><span class="p">)</span>

<span class="c"># (2) Binary process</span>
<span class="n">fullData</span><span class="p">[</span><span class="s">&quot;booked&quot;</span><span class="p">]</span> <span class="o">=</span> <span class="p">(</span><span class="n">fullData</span><span class="p">[</span><span class="s">&#39;country_destination&#39;</span><span class="p">]</span><span class="o">!=</span> <span class="s">&#39;NDF&#39;</span><span class="p">)</span><span class="o">.</span><span class="n">astype</span><span class="p">(</span><span class="nb">int</span><span class="p">)</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area"><div class="prompt"></div>


<div class="output_png output_subarea ">
<img src="data:image/png;base64,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
AElFTkSuQmCC
"
>
</div>

</div>

</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">
In&nbsp;[232]:
</div>
<div class="inner_cell">
    <div class="input_area">
<div class="highlight"><pre><span class="c"># There are 12 categorical variables in total</span>
<span class="c"># 4. &#39;date_first_booking&#39; variable</span>
<span class="c"># (1) Visualization</span>
<span class="n">fig</span><span class="p">,</span> <span class="n">axis1</span> <span class="o">=</span> <span class="n">plt</span><span class="o">.</span><span class="n">subplots</span><span class="p">(</span><span class="mi">1</span><span class="p">,</span><span class="mi">1</span><span class="p">,</span><span class="n">sharex</span><span class="o">=</span><span class="bp">True</span><span class="p">,</span><span class="n">figsize</span><span class="o">=</span><span class="p">(</span><span class="mi">15</span><span class="p">,</span><span class="mi">8</span><span class="p">))</span>
<span class="n">sns</span><span class="o">.</span><span class="n">countplot</span><span class="p">(</span><span class="n">x</span><span class="o">=</span><span class="s">&#39;date_first_booking&#39;</span><span class="p">,</span> <span class="n">data</span><span class="o">=</span><span class="n">fullData</span><span class="p">,</span> <span class="n">palette</span><span class="o">=</span><span class="s">&quot;husl&quot;</span><span class="p">,</span> <span class="n">ax</span><span class="o">=</span><span class="n">axis1</span><span class="p">)</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area"><div class="prompt output_prompt">
    Out[232]:</div>


<div class="output_text output_subarea output_pyout">
<pre>
&lt;matplotlib.axes._subplots.AxesSubplot at 0x12ab49190&gt;
</pre>
</div>

</div>

<div class="output_area"><div class="prompt"></div>


<div class="output_png output_subarea ">
<img src="data:image/png;base64,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
zszMVPbN5XKbjls2Ozurs2fPlp7XFemhhx7S/v37Nz3f6tfu3LlzGhwb07lz5yrPt/oaLi0tVb2O
VzbGWXXe8fFx5XM53fvCCxrev19zc3NaWVnZdB2qt18de/n/l9NpPfPMM5qYmNhw/6bjZBf10ksv
Va57+f75+XnpjbtrXqPyY6t/NsvP+9VXX5XeuLHaXn3c6uc8Pz+/oYpbfn1Wspn1fdeWoinFs7fu
819YWJD2jlZd14H17TsmVE/p/murbk812Hf/ptv19x2q3F7ZMSTpmrXt9Su1petYHc94g3NMVD1u
36btG/ed3PJ2/XOsx3PN2u16++584/q+A2u3S7Ftfa32XLP+uD2qf47Sz8ieyr6jW+y7sLCg8apr
OVF1e7LB467V+vW5Tltfn/1V+1bfvv6qxy0sLOi7155DJpNRTNdVnlP1z3P5fXXu3LnK75Ty75Hq
z4fy738/+LsTQQkjkfwVSW+W9OuGYexXKXF8yDCMnzBN8zFJPyPpkUYHOXr0aLBRBigWK32YHD58
OORI0G6xWEyPfVU6cuQIr28L6r1Hrt4ei8Wkx6RDhw7pK+c2X3e/77Vmz7vVY8tq7RuLxaQnSgnp
gQMHNvwei8ViGhoakta+Izt06FDpxmtfqTyvWCwm/XPpvqNHj5YqWGdLx6t+7uXzbHjcmqGhIR08
eHBDXENDQ9q9e7c0Y+nQoUM6ePBgZduBAwd08ODBjcc++YVKfOVjVR93/XizOnLkSOU8+/fvl6y5
yvOvxPFPpf9NTU1JF6qS9hc2rjNYfp7lc0iqfFpMT09rcHBQOl91zsdL166878GDBzc2gnl+/QvJ
6enp9Wv69KnKdUin09LzqdLzPffShtculUpJ517WoUOHSs/Xea3y2pWvWel439hwnsHBQcnMbnpO
A8PDleu0b98+yXHWv7x4/gVNTU1px47NH9vT09PS8y+W/u/E1x///Ivr90uSE19/Hdxk6XrbcU1N
Ta0d4+XStoX6f2zu379//WdTKj3v581S4pq5tGHfynGl0nN205Xtk5OTkptZj8f8TuVxExMTslfX
j6GFwsbr8tRzG/Z1rlRdVytV2a4tGttW39/MvucWN9+ut++ri1vfrmVqakpyrlT2jTc4x8Li+uO+
46xvv7qZ78TEhC5WxeBW3X69wTnOV+17ocG+a98BaGJiQkuZqtiWt37cpQtVtxfq77t//35lnExl
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
McQA7y+cAAAAAElFTkSuQmCC
"
>
</div>

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
<div class="highlight"><pre><span class="c"># Type : Date</span>
<span class="c"># (2) Split a &#39;date&#39; variable into 2 variables, i.e., &#39;year&#39; and &#39;month&#39;</span>
<span class="k">def</span> <span class="nf">get_year</span><span class="p">(</span><span class="n">date</span><span class="p">):</span>
    <span class="k">if</span> <span class="n">date</span> <span class="o">==</span> <span class="n">date</span><span class="p">:</span> <span class="c"># if the value is nan, nan is not equal to another nan</span>
        <span class="k">return</span> <span class="nb">int</span><span class="p">(</span><span class="nb">str</span><span class="p">(</span><span class="n">date</span><span class="p">)[:</span><span class="mi">4</span><span class="p">])</span>
    <span class="k">return</span> <span class="n">date</span>

<span class="k">def</span> <span class="nf">get_month</span><span class="p">(</span><span class="n">date</span><span class="p">):</span>
    <span class="k">if</span> <span class="n">date</span> <span class="o">==</span> <span class="n">date</span><span class="p">:</span> <span class="c"># if the value is nan, nan is not equal to another nan</span>
        <span class="k">return</span> <span class="nb">int</span><span class="p">(</span><span class="nb">float</span><span class="p">(</span><span class="nb">str</span><span class="p">(</span><span class="n">date</span><span class="p">)[</span><span class="mi">5</span><span class="p">:</span><span class="mi">7</span><span class="p">]))</span>
    <span class="k">return</span> <span class="n">date</span>

<span class="c"># Create Year and Month columns</span>
<span class="n">fullData</span><span class="p">[</span><span class="s">&#39;Year&#39;</span><span class="p">]</span> <span class="o">=</span> <span class="n">fullData</span><span class="p">[</span><span class="s">&#39;date_first_booking&#39;</span><span class="p">]</span><span class="o">.</span><span class="n">apply</span><span class="p">(</span><span class="n">get_year</span><span class="p">)</span>
<span class="n">fullData</span><span class="p">[</span><span class="s">&#39;Month&#39;</span><span class="p">]</span><span class="o">=</span> <span class="n">fullData</span><span class="p">[</span><span class="s">&#39;date_first_booking&#39;</span><span class="p">]</span><span class="o">.</span><span class="n">apply</span><span class="p">(</span><span class="n">get_month</span><span class="p">)</span>

<span class="c"># (3) Fill NaN of the new created variables &#39;Year&#39; and &#39;Month&#39;</span>
<span class="n">fullData</span><span class="p">[</span><span class="s">&#39;Year&#39;</span><span class="p">]</span><span class="o">.</span><span class="n">fillna</span><span class="p">(</span><span class="n">fullData</span><span class="p">[</span><span class="s">&#39;Year&#39;</span><span class="p">]</span><span class="o">.</span><span class="n">median</span><span class="p">(),</span> <span class="n">inplace</span><span class="o">=</span><span class="bp">True</span><span class="p">)</span>
<span class="n">fullData</span><span class="p">[</span><span class="s">&#39;Month&#39;</span><span class="p">]</span><span class="o">.</span><span class="n">fillna</span><span class="p">(</span><span class="n">fullData</span><span class="p">[</span><span class="s">&#39;Month&#39;</span><span class="p">]</span><span class="o">.</span><span class="n">median</span><span class="p">(),</span> <span class="n">inplace</span><span class="o">=</span><span class="bp">True</span><span class="p">)</span>

<span class="nb">type</span><span class="p">(</span><span class="n">fullData</span><span class="p">[</span><span class="s">&#39;Year&#39;</span><span class="p">]</span><span class="o">.</span><span class="n">iloc</span><span class="p">[</span><span class="mi">2</span><span class="p">])</span> <span class="c"># numpy.float64</span>

<span class="c"># (4) Be careful of the data type of &#39;Year&#39; and &#39;Month&#39; variables. They are float instead of int.</span>
<span class="c"># Convert them to &#39;int&#39;</span>
<span class="n">fullData</span><span class="p">[[</span><span class="s">&#39;Year&#39;</span><span class="p">,</span> <span class="s">&#39;Month&#39;</span><span class="p">]]</span> <span class="o">=</span> <span class="n">fullData</span><span class="p">[[</span><span class="s">&#39;Year&#39;</span><span class="p">,</span> <span class="s">&#39;Month&#39;</span><span class="p">]]</span><span class="o">.</span><span class="n">astype</span><span class="p">(</span><span class="nb">int</span><span class="p">)</span>
</pre></div>

</div>
</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">
In&nbsp;[14]:
</div>
<div class="inner_cell">
    <div class="input_area">
<div class="highlight"><pre><span class="c"># (5) Look for new insights</span>
<span class="c"># NOTICE : in year 2014 and 2015, there wasn&#39;t &quot;no-booking&quot;</span>
<span class="n">fig</span><span class="p">,</span> <span class="n">axis1</span> <span class="o">=</span> <span class="n">plt</span><span class="o">.</span><span class="n">subplots</span><span class="p">(</span><span class="mi">1</span><span class="p">,</span><span class="mi">1</span><span class="p">,</span><span class="n">figsize</span><span class="o">=</span><span class="p">(</span><span class="mi">8</span><span class="p">,</span><span class="mi">4</span><span class="p">))</span>
<span class="n">sns</span><span class="o">.</span><span class="n">countplot</span><span class="p">(</span><span class="n">x</span><span class="o">=</span><span class="s">&quot;Year&quot;</span><span class="p">,</span><span class="n">hue</span><span class="o">=</span><span class="s">&quot;country_destination&quot;</span><span class="p">,</span> <span class="n">data</span><span class="o">=</span><span class="n">fullData</span><span class="p">,</span> <span class="n">palette</span><span class="o">=</span><span class="s">&quot;husl&quot;</span><span class="p">,</span> <span class="n">order</span><span class="o">=</span><span class="p">[</span><span class="mi">2010</span><span class="p">,</span><span class="mi">2011</span><span class="p">,</span><span class="mi">2012</span><span class="p">,</span><span class="mi">2013</span><span class="p">,</span><span class="mi">2014</span><span class="p">,</span><span class="mi">2015</span><span class="p">],</span> <span class="n">ax</span><span class="o">=</span><span class="n">axis1</span><span class="p">)</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area"><div class="prompt output_prompt">
    Out[14]:</div>


<div class="output_text output_subarea output_pyout">
<pre>
&lt;matplotlib.axes._subplots.AxesSubplot at 0x1116f9350&gt;
</pre>
</div>

</div>

<div class="output_area"><div class="prompt"></div>


<div class="output_png output_subarea ">
<img src="data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAgIAAAERCAYAAAAJ789kAAAABHNCSVQICAgIfAhkiAAAAAlwSFlz
AAALEgAACxIB0t1+/AAAIABJREFUeJzt3Xl8lNXZ//HPsIQECVsAQRFDRC8rkQcNDyIoilq1PFrF
iiAaFwRcQKUqUlIQpYoLS5VfqVZAZXNDtFVR0aIVhIKYp0XQh6MoCUtVQBOSkJD998dMYgJZBjIz
yWS+79eLFzPXnDlz3eeVmbnmvs99H09paSkiIiISmZrUdwIiIiJSf1QIiIiIRDAVAiIiIhFMhYCI
iEgEUyEgIiISwVQIiIiIRLBmwezczM4CHnPODaoQGwGMc871990fDYwBioCHnXMrzCwGWAJ0BLKB
G51z+8ysH/Ckr+37zrlpvj6mAoN98fHOuY3B3C4REZHGImh7BMzsfmAe0KJC7AxgZIX7nYE7gf7A
JcCjZhYF3A5scs4NBBYBk31PeQa41jl3DnCWmfU2szOBgc65s4DhwNxgbZOIiEhjE8xDA9uAqwAP
gJnFAY8A48tiQF9grXOu0DmX5XtOL2AA8J6vzXvARWYWC0Q557b74iuBi3xt3wdwzu0EmvleS0RE
RGoRtELAOfc63l31mFkTYAFwD5BToVlrYH+F+9lAG188q4bYofGq+hAREZFaBHWOQAVJQA/gaSAa
OM3MZgMfAbEV2sUCmXi/8GNriIG3AMgECqrpQ0RERGoRkkLAN3kvEcDMTgReds7d45sj8IiZtcBb
IPwC2AKsxTv5byPwK2C1cy7bzArMLAHYDlwMPAgUA0+Y2UzgBKCJc+6nmvJJTU3VAgsiIhJxkpKS
PIfGQlEIHPql6ymLOee+N7M5wBq8hylSnHP5ZvY0sNDM1gD5wAjfc28DlgJNgZVlZwf42v3T18cd
/iSVlJRUp40SEREJJ6mpqVXGPZG4+mBqamqpCgEREYkkqampVe4R0AWFREREIpgKARERkQimQkBE
RCSCqRAQERGJYCoEREREIpgKARERkQimQkBERBqVlStXkp2dHZC+rrzyyiNqv2zZMgDWrFnD22+/
fUTP/fTTT9mxYwf79u1jxowZR/TculAhICIijcqSJUvIz8+vl9d+7rnnADj33HO57LLLjui5r7/+
OhkZGXTo0IEJEyYEI70qhWqtARERkSrl5OQwYcIEMjIyaN68ORMmTGD69Ok0a9aMLl26MH36dN56
6y327dvHmDFj2LBhA++88w5jxozh/vvvp3379qSlpXHzzTfTuXNntm7dSkpKCqNGjWLGjBk0b96c
gQMH0qRJE8aMGUNaWhqzZ89mzpw5Vebz+OOPk5qaSnx8PMXFxYD3F/7cuXPxeDxccMEFjB49mhde
eIGVK1dSVFTE6NGjyc3N5bvvvuOBBx7gjDPOYO/evfTu3ZsFCxbg8XjYuXMnkyZN4pxzzmHevHms
W7eOrKwsBg0axMUXX8wnn3zCV199xYwZM3j00UeZP38+Tz/9NB999BEAycnJXH755SQnJ9OzZ082
b95M69at+fOf/4zHc9h1gvymPQIiIlKvXnrpJfr06cPLL7/MrbfeyrRp05g9ezZLlizh+OOPZ/ny
5ZW+6Cre/u677/jjH//IggULWLRoEf379+fUU0/l0UcfpbS0lOjoaF588UVGjBjB3//+dwDeeust
hgwZUmUumzdvJi0tjVdffZVx48Zx8OBBSktLefzxx1mwYAEvvvgiqampfPPNN7z77rvMnDmT5557
jpKSEq688kq6dOnCtGnTKvWZlZXFM888w8MPP8xLL71ESUkJHo+H559/npdeeok333yTU045hXPP
PZcHH3yQ6OhoALZu3Upqaiqvvvoqixcv5tlnny0/5DFw4ECWLl1KQUEBzrk6jb8KARERqVe7du2i
V69eAJxzzjnk5eVx3HHHAXDmmWfy7bffVmpfUlJSfrt79+40a9aMTp06HXY4wOPx0L17dwBat25N
586d+eabb1i3bh0DBw6sMpf09HR69uwJQLdu3Wjfvj0ZGRns2bOH2267jRtuuIEffviBnTt38tBD
D/Hkk09y55131ngo4uSTTwagY8eO5Ofn06RJE3Jzc7nvvvuYPn06RUVFVT5v+/bt9O7dG4AWLVrQ
o0cPdu/eDcApp5wCUOV2HykVAiIiUq+6d+/OF198AXgn+mVmZvLdd98B3uvjd+vWjRYtWrBnzx7A
+0u5TFW7xD0eD8XFxZSWllZ6/Morr2TOnDkkJibStGnTanPZvHkzALt37yYjI4N27drRtWtXFixY
wOLFi7n66qs5+eSTWb58OY888gjz5s3j6aefBqBs/Z6K6/gcmuPWrVv58ssvmTlzJrfccgsHDhwo
f6ws77JcNm3aBMDBgwfZunUrXbp0qXa7j5bmCIiISL0aNmwYEydOZNWqVURFRfGnP/2Je++9l9LS
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
"
>
</div>

</div>

</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">
In&nbsp;[15]:
</div>
<div class="inner_cell">
    <div class="input_area">
<div class="highlight"><pre><span class="c"># There are 12 original categorical variables in total</span>
<span class="c"># 5. &#39;first_affiliate_tracked&#39; variable</span>
<span class="c"># (1) Visualization</span>
<span class="n">fig</span><span class="p">,</span> <span class="n">axis1</span> <span class="o">=</span> <span class="n">plt</span><span class="o">.</span><span class="n">subplots</span><span class="p">(</span><span class="mi">1</span><span class="p">,</span><span class="mi">1</span><span class="p">,</span><span class="n">sharex</span><span class="o">=</span><span class="bp">True</span><span class="p">,</span><span class="n">figsize</span><span class="o">=</span><span class="p">(</span><span class="mi">15</span><span class="p">,</span><span class="mi">8</span><span class="p">))</span>
<span class="n">sns</span><span class="o">.</span><span class="n">countplot</span><span class="p">(</span><span class="n">x</span><span class="o">=</span><span class="s">&#39;first_affiliate_tracked&#39;</span><span class="p">,</span> <span class="n">data</span><span class="o">=</span><span class="n">fullData</span><span class="p">,</span> <span class="n">palette</span><span class="o">=</span><span class="s">&quot;husl&quot;</span><span class="p">,</span> <span class="n">ax</span><span class="o">=</span><span class="n">axis1</span><span class="p">)</span>

<span class="c"># (2) Fill NaN values randomly</span>
<span class="n">fullData</span> <span class="o">=</span> <span class="n">FillNaNRandom</span><span class="p">(</span><span class="n">fullData</span><span class="p">,</span> <span class="s">&#39;first_affiliate_tracked&#39;</span><span class="p">)</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area"><div class="prompt"></div>
<div class="output_subarea output_stream output_stdout output_text">
<pre>
There are 7 different values in the list of :
Index([u&apos;untracked&apos;, u&apos;linked&apos;, u&apos;omg&apos;, u&apos;tracked-other&apos;, u&apos;product&apos;, u&apos;marketing&apos;, u&apos;local ops&apos;], dtype=&apos;object&apos;)
There are : 6085 NaN values in this variable!

</pre>
</div>
</div>

<div class="output_area"><div class="prompt"></div>
<div class="output_subarea output_stream output_stderr output_text">
<pre>
-c:15: SettingWithCopyWarning: 
A value is trying to be set on a copy of a slice from a DataFrame

See the the caveats in the documentation: http://pandas.pydata.org/pandas-docs/stable/indexing.html#indexing-view-versus-copy

</pre>
</div>
</div>

<div class="output_area"><div class="prompt"></div>


<div class="output_png output_subarea ">
<img src="data:image/png;base64,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
SAQAAGAiJO7FquqsqrrXFx+qqlOr6g/vxXL/uqpee2+fF/ZVVfUzVXVJVf32TvrYL5dZVR1YVc+/
D8ufX1XGqBsZAAAPGklEQVQvvBfL/XZVnbLIvlON9/b5WF5V9YtVdeZuLvOIqvqXS1UTu6+qvrjI
fg+pqueMt3+pqh63tJWxzfi39Y17aKxNVbV2T4y1txMS926vTrL/fVjeVYtgec0lubW7X7KLPiyv
b0/y8/dh+Xu7zXZnufk1+h3ZO9yb7fRjSU7a04Vwnyx2O/5gkn+VJN396919w9KVxHb25Gui19fR
avoKjFWhqn4mSXX3q6vqoCR/k+SmJJ9Osj7JoUn+TZIfT3JUkj+sqt9K8qYkdyb5vSR3JHlRkgdk
+GX/ySRfTfIfkjwuydokr01y2/icD0zy/yR5V3f/4fhpzBMyBNC3dvf7q+rEJBcluXUcf3ZpfxJU
1QOS/Mck351hW/xmknNyz+/C15Nck+TJSR6c5EkZfgfeleEN5ReSnNzd37HsxbMzR1fVdd19QlX9
VZKPJzk2w7769CRrEvvlMvvlJN9XVXcl+fMkD0ry/CRnJtmQ5PAkn+nun6uqI5JcluSwDNvqp7cN
UlXfk+Q947JfSPL7Sb5tfPgXuntjVZ2d5KwkNyc5JMn7ty+mqp6b5GUZ9ue/Hftvq/E1Y7enV9W/
GWt7TXf/1/H+v01yV5JPjn9Hzk9y4vhcz+/uv7mvP6x9wfi3+ClJHjr+e12SX03SGbbLORm29UyG
91LndfdVVfWMJK9J8pUM+/R7x9nis7t72yzTF7v7qKp6VJJLM/yt/sckZyR5VZKDq+ra7v6vy7W+
q9W4HX8iyUEZ/i7+VobX2fVJfjHJv8jwHumQJLeMt5+b5OfGIc6fN9Ybkhza3S9ZaF/LsI8eW1Uv
yLDP/dH4nE9NcnCSRyb59e6+rKoen+S3k2zJ8FpwR3f76rY9oKpekeSnknwrydXd/aodvG7fkeR3
cs/vxnnd/Sc7GPPHM+z/d2TYt38uyQ8l+Xfj8g9Lckl3v72qXjSOf3eSG7r7ZUu1rkvNTOL9z/af
YGy7f313/3iSP0vynO7+/SRfTPLsDL/wB3b3yd397iSPSvK07v6RJJ/NECKekeTw7j4uyROT/PA4
7kySDyZ52/hG9PQkR4/L/miSX66qw5JckuS53f2kJH+9JGvO9l6Y5EvdfVKS05JckOEN4fXdfVqS
A5P8w7hNPpvklAxvJv+uu5+Q4Y/bw1aicHZp2349k+S93X1qkr9Pcvr4mP1yeV2QYR96XZLPjvvc
3yf56vizfVyS46vq4UnOS/LHY59XJHn8OMb3ZggNZ3T3xiTnJvnz7v7RDPvyJeMblZcnOS7DG8e5
bPeaX1WHZ9h3nzhu71vH5S8Ya/vVDK/5/2t8HXh5knOq6iHjcj86LvcdVXXaOP7/6O6TBMTdMpdk
v/Fn/JQMH8YcluT13X1GhiB4RXefkuGD298fT/94a5LTxt+bW3YydpK8OcmF3X1ihvDyg0nemOQ9
AuIedUh3Py3Jryc5p7ufmeFv5fOTPCTD9jo+Q9h/XIbt89XxPdXHkqSqfiPJ/mNA/LYsvK9dkORj
3f2Oec89lyFY/kSGWcZXje1vT3Jmd/9Ykr9bypXfl1TVD2TYH08Y96tHVdXTsvDrdiV5y7ivnpXk
xTsYc02S303yk+Pf6k+M481l+ADp9CQnJPnF8TX+Z5K8eHz+z1XVfTnib0UJifdva8Z/c0n+cmz7
QoZwsL2ed/vLSS6rqj/IMEPxgCTrklyXJN19a3f/yjj2yRk+BTloXPYHkmyoqquSfCTDi+bRSY7q
7r8d+1y9J1aOXfreDDOF6e6vZ3gT+8gk/318/NaxLUm+lmEbfm/u2c6d4XeB+7f5+/a2/dB+ubzW
zPv/xvH2HUmOrKr3ZnhD96D889fS67r7vWP/p2SYLbh7vP8DSX5u3Ga/l+HN6Pck+Vx3f7O7705y
bZI1VfWrVXXV2PeRGULdP4zjXJ3k+7erdy73zBp/KckDx7GPSPKRcZzvG8fKvHVi93w0Sbr7ixle
bw/PPX9rvzfjPtfd/zvJ7UkenuS27v7a2GdH++S237f5v0sf6u4/2+5x7ru5DEffJMPRU58bb9+a
4aiqb2Y4IuvSJN+ZYR9P/ul7qodl2J8fNN5faF87Zic1bHv+/5V7XtO/vbu31XLNbq4TO1ZJ/qK7
7xrvX5Ph9XOh1+0vJnlhVb0rydnZ8dGVD01ye3f/n+3GTJJPdPdd3f2PSTZm+D342SQvqaqPJ/mu
7MX7s5B4/3NHhmnvJHlshhe4+b9ga+bdvzv3nJN4d5KMswvnZ5hqf0GSb4z9P5fhE7JU1WFV9afj
2B9O8swkF1bVt4/9ruruJ2Y4pPV9GT7l+vuq2rZTnLDnVped+FySH0mSqprJcHjM/8zOj5ffmHH7
VNUjM7y4cf+20Pa0Xy6vu3LP38NtIe/0JI8YZ41+OUMA3PZa+vgkqaqT510s4aIMhx5dVlX7jf1+
c9xmz8twqNPfJvn+qjp4/HT68Unmuvs13f3Ese//zHBY6QPHcU/N8Ib17nk1LvSm46YMHzScNo7z
OxnfFM1bJ3bPtr+ZD8sQxL+ce36Wn8vwYU6q6jsyHPL/90kOq6ojxz7Hj/9Pf9er6rtyzyHI83+X
nlNVL84/3c7sGTv6m3lgkmd097OT/EKGn/v891fbfKm7n5Jh331yhn10+33tL7LjbbfQ83+hqh49
3vbavef8TZLjqmr/8TX25Awfki30uv36DKdz/HSG0z52tN/dkuTQqjpqvH9K7vkQ4YfHMR+Y5NEZ
XuNfkOHw8lMzHJK6125fL0T3P5dnOGfpmgxT5rfnnx6SNP/2NUn+dF57uvu2DJ9OX5fkv2TYOb69
uz+Y5GvjuJdnOLQlGd6g3JzhHMX/2N0fSvL1qro6yaeS3D3OYv18hsNp/jzDjuDE3qX3e0kOH7fZ
VRkOhbt5J/3nMpwDdXRVfSLDNr1jyatkT5r2c/vlsro5w6zCQZl3iH+SY6rqYxleL6/P8Eb/DRnO
B7wqw/b53bH/XHf/eYbZ/VcmuTDJs8Z+H8wwg3hLhkPSPpnkygyzGP/E2Oe1Sa6qqusyBIpLMgSU
tVX1a/nnh6nOjcu9NcnVVfUXGT5M2DbL7Pfi3nnUuG99MMM5iHfNe+wNSX50fK39L0nOGmcvzkny
p+NyD8nws/9vSW4dt8v5GUJGkvz7JK8ef0eem+Fw5b/O8Pv1rKVeuX3IQu+f5jLsf9teV9+d4Sid
h2+3zPzbz89wHuHd+ef72o0ZtusPVNX256AtNNaLkvxBVf1Zhg8j/tlrAbttbjzU/z9neB98fZKb
uvuPs/Dr9vuSvLmqPpLh3NRvW2jQ7p7LEPw+UFWfzHDKx7bD/g8dt+HVSV7X3V/NsA9fU1UfzXCk
x/VLtcJLbc3cnL8dsFpU1QlJHtTdfzZeFOFPu/tRK10XwN6khq+ueGh3v2Wla2H1GS9u8p+7+5aq
+tUkd3b3BStdF4tXVacm+b+6+6UrXctScXVTWF3+Z4bzK16b4dyKBU/EBmCXfIrOUvlSkiur6usZ
zo/cre/T5H7hn114bLUxkwgAAMDEOYkAAABMhEQAAAAmQiIAAAATIREAAICJq5sCsFepqj9IclKS
7+nu/Re5zOOTPLO7X3Uvn/N1SZ6X4XvSfmB8/tcleW53P62q3pnh+0yvTHJpdz9tCWu5avwS7/tk
W83dfdm9WPZfJ3lad//sfa0DgPsfIRGAvc2ZSQ7s7m/txjLfl+Rh9+E5n5fkyd39+aq6a97zv3d8
fC7Dlzn/nyQ7DIh7qJZT7sOy8636S7gDcO8IiQDsNarqg0nWJPlyVa3t7kPGGbHDkzwyySuTnJrk
tCR3JfmTJL+V5PVJDqmqV3f3G3cw9gFJLkny/RlCXCd5ZpKLknxnkj+pqs+Pz/+pqnphhi/E/u55
Yxyd5OPdfXRVrU9ycZIHJTkyyVuSvGt+LUl+PcmbMwS//ZO8s7sv2sn6Xzz+f113n1BVX07y38Z6
H79Q/d19R1X92yQvHH8mH5o/i1lVD8wwA/qe7r6kqn46ycsynJIym+TF3X1nVT03yXlJvp7k80nu
2FGdAOzdnJMIwF6ju//VePMHk9w876Evd/f3JfnrJE/p7sckOTHJ92QIM69J8ic7CoijE5Lc0d3b
ljs4yendfXaS/z3efvpYx2OTfHkH42ybnXt+kl/t7scn+dEkF3b3bdvVclaGGcgNSY5L8oyqesJO
1v8Xxv9PGJsOT/LGsZ6F6n/qeHjrOUkel+TYJBuq6rHj8gcm+UCGsHtJVX1/kp9PckJ3/9C4jr9Y
VQ/PEGZPHes8OGYhAVYtM4kA7I3WzLs9l+T68fb/SvKNqvpkkv+a5DXjLNia7Zb5Z7r7mqr6SlW9
OMn3JnlUhlnAe+sVSU6vqldlCLWHzKt9Wy2nJfnBqvrR8f4hSdYn+eRuPM/1u6j/R5J8sLu3jP1/
PEnGn8mvZphdfMb42BPH5a6vqiRZm2E28YQk/293f2lc9p1Jnr4bNQKwFzGTCMBqcEeSdPddGWa6
XpNhlu26qnrUYgaoqn+V5D0ZDqf8gyRXZxfBchfelyFI/Y8kr97BWPsl+ffd/UPjzN1JSd65O0/S
3XcmO63/m/Ofu6oeXlUPzhCu/zDJn2Y4BHZbPf95Xj3HJfmFse/8+u/anRoB2LsIiQDs7eYHoB9M
8okkV3f3v0/y2SSVISjt6uiZH8sQkC5L8qUkJ2c4T3CxNWwfAk9L8tru/lCGwzRTVfsl+da8Wj6W
5KyqOqCqHpTkmgznFu7MXVW1UF07qv+aDDOah4znXb43yYZxmb/McB7n88af3ceT/GRVHTHONF6S
ISR+MskJVfWdY/tzdvUDAWDvJSQCsLeZW+D/uSTp7s8kuS7JxqqaTXJThpmyTyU5vqresJNx35Hk
OVV1Q5LfzXDRm+9eoN/cArfntvuXJOcn+WRVXZvh8M/PJTk6w+Gh22p5e5K/zRDWbkjy+9199c5X
P3+S5NNVdeB2tSxU/9Hd/ZcZvrrjuiSfTvKJ7v7otoW6+2tJXpXk95JszPDVHh8bbyfJr3X3zRnO
a7xyrPOOOCcRYNVaMzfnNR4AAICBC9cAsM+oqh/J8LUUC3nq+D2HK6qqHpnk/Tt4+Pnd/d+Xsx4A
9j1mEgEAAJg4JxEAAICJkAgAAMBESAQAAGAiJAIAADAREgEAAPj/269jAQAAAIBB/tb7RlEWTRIB
AABYLjN56yuHjPwAAAAASUVORK5CYII=
"
>
</div>

</div>

</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">
In&nbsp;[16]:
</div>
<div class="inner_cell">
    <div class="input_area">
<div class="highlight"><pre><span class="c"># There are 12 original categorical variables in total</span>
<span class="c"># 6. &#39;first_browser&#39; variable</span>
<span class="c"># (1) Visualization</span>
<span class="n">fig</span><span class="p">,</span> <span class="n">axis1</span> <span class="o">=</span> <span class="n">plt</span><span class="o">.</span><span class="n">subplots</span><span class="p">(</span><span class="mi">1</span><span class="p">,</span><span class="mi">1</span><span class="p">,</span><span class="n">sharex</span><span class="o">=</span><span class="bp">True</span><span class="p">,</span><span class="n">figsize</span><span class="o">=</span><span class="p">(</span><span class="mi">15</span><span class="p">,</span><span class="mi">8</span><span class="p">))</span>
<span class="n">sns</span><span class="o">.</span><span class="n">countplot</span><span class="p">(</span><span class="n">x</span><span class="o">=</span><span class="s">&#39;first_browser&#39;</span><span class="p">,</span> <span class="n">data</span><span class="o">=</span><span class="n">fullData</span><span class="p">,</span> <span class="n">palette</span><span class="o">=</span><span class="s">&quot;husl&quot;</span><span class="p">,</span> <span class="n">ax</span><span class="o">=</span><span class="n">axis1</span><span class="p">)</span>

<span class="c"># (2) Fill NaN values randomly</span>
<span class="n">fullData</span> <span class="o">=</span> <span class="n">FillNaNRandom</span><span class="p">(</span><span class="n">fullData</span><span class="p">,</span> <span class="s">&#39;first_browser&#39;</span><span class="p">)</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area"><div class="prompt"></div>
<div class="output_subarea output_stream output_stdout output_text">
<pre>
There are 55 different values in the list of :
Index([u&apos;Chrome&apos;, u&apos;Safari&apos;, u&apos;-unknown-&apos;, u&apos;Firefox&apos;, u&apos;Mobile Safari&apos;, u&apos;IE&apos;, u&apos;Chrome Mobile&apos;, u&apos;Android Browser&apos;, u&apos;AOL Explorer&apos;, u&apos;Opera&apos;, u&apos;Silk&apos;, u&apos;IE Mobile&apos;, u&apos;BlackBerry Browser&apos;, u&apos;Chromium&apos;, u&apos;Mobile Firefox&apos;, u&apos;Maxthon&apos;, u&apos;Apple Mail&apos;, u&apos;Sogou Explorer&apos;, u&apos;SiteKiosk&apos;, u&apos;RockMelt&apos;, u&apos;Iron&apos;, u&apos;IceWeasel&apos;, u&apos;Yandex.Browser&apos;, u&apos;Pale Moon&apos;, u&apos;CometBird&apos;, u&apos;SeaMonkey&apos;, u&apos;Camino&apos;, u&apos;TenFourFox&apos;, u&apos;Opera Mini&apos;, u&apos;wOSBrowser&apos;, u&apos;CoolNovo&apos;, u&apos;Avant Browser&apos;, u&apos;Opera Mobile&apos;, u&apos;Mozilla&apos;, u&apos;OmniWeb&apos;, u&apos;SlimBrowser&apos;, u&apos;Comodo Dragon&apos;, u&apos;Crazy Browser&apos;, u&apos;TheWorld Browser&apos;, u&apos;Flock&apos;, u&apos;Stainless&apos;, u&apos;PS Vita browser&apos;, u&apos;Googlebot&apos;, u&apos;Kindle Browser&apos;, u&apos;NetNewsWire&apos;, u&apos;Google Earth&apos;, u&apos;UC Browser&apos;, u&apos;Conkeror&apos;, u&apos;Outlook 2007&apos;, u&apos;IBrowse&apos;, u&apos;Palm Pre web browser&apos;, u&apos;IceDragon&apos;, u&apos;Nintendo Browser&apos;, u&apos;Arora&apos;, u&apos;Epic&apos;], dtype=&apos;object&apos;)
There is no NaN values for this variable!

</pre>
</div>
</div>

<div class="output_area"><div class="prompt"></div>


<div class="output_png output_subarea ">
<img src="data:image/png;base64,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
O/P0kc/fvmXu052t/DXXXLNJ488Enqmpqbz/rcdk9513mNN4N9+6Kq877dM/GP/GTWj3ppSdi82Z
57f9wdHsZRwPAAAgAElEQVTZZee5naCuvHV1/vCUzwwSbjenzb/7tqOzcJe5n1TftnJ13v2H69q9
OdM+4dSjs9Ouc9tG7lixKmectPnT3Zxxp6am8rPvOC477Dr3P6GzasWd+ce3nLNV272lx92a0x5d
V8ec9ofZYZdd5jTeqpUr8+m3vm2rrKfNHX9bHHdrTntbHHdrTvuBMO7WnPa2Mu7WnPa2OO7WnPaW
/rvt89auXbtFJziEUsp7kvxHrfW8/vn6Wute91V+cnJy25tJAACAAe23337zxj2NbfUO5tIkRyc5
r5RyYJIvbajwlliQAAAAD3XbasD8/5P8dCllaf/8K1uzMQAAAGyjj8gCAADwwPOwrd0AAAAAHhwE
TAAAAAYhYAIAADCIbfUlPz9QSvnxJO9K8ogkj0zyv5JcmuRVtdZjxzC9RUn+JslXk+yb5M4k+yeZ
TvKd/u9fk6TW+vY51vmuJL+c5P8kuSPJmiS/U2v9rw2U/5kkH07yviTH1lr/tn/3b0kem+TztdZf
KaU8M8nP1lrfPrKs9k5bVh+ptZ5cSjkiyat79b+c5Mwkn6i1XjiHtj8vyRuTzEtbB39Wa/14r/Pv
knwlydq0v136zT7sj5KcXmv9817HmiQfqrWeMNLGZyb5kb4snp/kV2qtx5ZSTk5yUpKDkvxBrfXo
UsqeSb6V5NeTvDnJXyd5S5IVSb6RZEGSRyV5QZIb+7Lbq5c5PcldSY5J8t4kv5lkvyT/neQva61/
3dv4/bS3Fd/R5/PzSXZN8hNJbklyeNrfZq1p20SS/HmS80bXT6/rS0kma60/9HKqUsp3aq2PKaW8
Isnutdb3rPf9J7Ju/fxEkiNrrbfcx3o5OcmXk7wnyfIk8/sy3T7JPUkenuTfk3y71vrS2eoYqetF
WbfdXD7y1dVJ3p22rRxUSjl7ZHnM+Ota60dG6joibf84Nsl3k/xTb8vdafvQH9Raz5ylDf9jmfRt
/fYkL8oGttm+z34zbX3PS/JTfZo/nmQqyed6O85I294WpG17/5Vkj7R9+qm11kf1ab661lo3sLxG
97k3pW3vu9Rabx8p8299Onemb0+11tevV8/vjbR1g33CfbTj5LR95a4k/9nnfeckz0jrv27aUL19
uX2i1npQ//ydWutjNmH6PzR+H/aKJKek7Zczvlxr/a1SyllJLqy1nldKeVKSq9L2qan+885p+9Ou
SUqt9S1zaMP6y/B3k7w8bV+/PcnP1Fo/MdPWJKuS7Flr/bGZeU7y2SS/muTtSV6Z5JIkz07r16Z7
Hdf38m9O8q+11itnacs/p63zt6b1DX9ea/3QLOVGj2lPT3Jv2vraIcl1SY6rtd6zgXn+8SSTaX3U
05N8b2Z+ZuZp/fVYSnlkktOS7NPn68AkT6+1fn1kOb4gSUnrS2paX3p3Wr9wy2j7erkfOi7XWk++
rzb3afxbNrJv9XKL0vriyZHBj+nT+maS7dLW9V+kHavX73+/muT/1Fp/upRydZInp+2H85J8P8kf
11rfW0rZI8kHkzwxyS5JrkzypFrrgaWUqSSLk1yU5G211kt63W9O8pwkR6T1lT+ddqz5WpK/nzkn
6fP6W7XWL5VS9kryzFrrP5VSPpfkKUleU2v9+172B+trZNvYo09/ZZLvzWX59vF3SNufHldrXVtK
OSit/zug1vqfpZQd+/fH97b/eNb1U3skmVdr/fHRPu4+1k/t6+BhadvIjkluTduPFyT52Mzxv4/z
piS/neRJaecvn0jyoWxkPx/p4w5OO/bvlrYdPCvJX9RaX9vLnZe2vRyfdjx82EiZN/Yyf5J27B/d
lr6X5ANJjh89nyylfLnW+vS+Hkf7i7PSzjvemGRRkguTXFxr/c3+/dlJvp7kbWnbx7w+zzf0ae7Q
x/14+vEwbf/9TB//WWnbxg/OHUb2h3vTtv2knQ9dsP4xZQPL8YisO1+b8b20Y+APHYP6fD2/1vrr
s9Szd/p66/N5V5I31Vqv7t8/Ka0P3yPJ9Wnbw5tHj42z1PmiJP+R9nLPHWqtPzFLmUVJvlJr3WmW
787OeucGpZQXJ/lo2vnQNUmekHacvzfJnyT5Ylo///209fLVJKvT1tPOaetppySH9s+fGJnkPn2e
/nK9dhyR1r+Nbkc3JvndWus5vR94T182C9K219+utd49so6/kbZPfj+tr70zyQm11i/e1/Lbmrbp
O5illF3SVuzraq0/mX5QTOt4x2Vt/5e0k5Vjk1xZa9211vq0WuuRtda3zzVcdscmmaq17l9rPSLJ
65N8ZAPlfz6tQ/1S2oHrF0a+e0RaZ742SWqtV/UT3R8sq7QD1OlJnl5KefVI2WNrrXevN48b88Ek
P1dr/am0A9LbSymP6uP/S18eP1lrfVbageaEJG8YPbgkuTnJs0spu/U2vj4tbK9N2+nXv1BwTdrJ
zoyXph001qbtgNemdZQf79vF4Uke35fNM5P8bNpJ5kfSDiJ/k9ZJvLrXe12fl5eWUn6+T2NtWsg9
stZ6QNrBabe0zuHItLD0C2knLkf2YTdnvfVTSnl6b8dsy3ftev//kFnWz4b+/M5oXUendYaH11rn
p62D85PcurFw2R2d5A1pB7ojR/69ZpZp/u56ZWbbjmeWydq0beJv0oL7+bOFy/XmZ/1hb5jjNvuN
JL+Y5Oha608n+f/SwsuPph3s/zTt4tSfpoWPVUnOqrU+Ke0g/8iRaW5w35jZ5/rHl/d5e8ksbf+l
0e2plLLfzJellB+baesc+4T7cl2Sm/p0jki7qDAv7SR6U+sd4o1wa5Ocu9428lv9u39O6wcWpG2f
X0yyotZ6aJIvJHlhkn+ZazvuYxl+uNb6+h4IZ/qC/9HGfgI90959+/9vSDvZXJy2La1O8oWZcJkk
tdZ3zRYuu/lJnrqRNq9/TPuntBO1T9RaD+7FjpnD+Lf18T+bZO9SyodH52+WUc9Mck2t9fC+rKaT
fKqUsrAvx2PS+sgXJDmsz8vb0o65M/v8TPuOzSzH5X6s2ZBNOe58ZXQbSvLOtNByZK31sCQfS+tj
Zut/d0uyZ9/OFiW5oh+/d0m7CHVqKWXntOP7RbXWZ9Van5J2MvfokbbOLLdfHmnXn6b1KXcleWzv
m16d1tc8s7dhxyRPqLXO/Hm1n0pyyEi9u6Yt49HlMrpuT0o7Ad0/LQB8OHNbvqm1rkrbr2ZO0p+f
Fiye3z8flBYsHt379x/0U0lekWT3Usp+6/Vxs7kxrR/9eJL/N8kVaSfzz0s7Hr+xlLJwpPzL+7yN
nsvMdVv4elr4eGdv57lpF49ePFLm+P5v+7Rj+1fSluMx/XwltdbfmWVbWr/fns1of/HPaf3UVFpo
ubbP74yD0y723d6n9Rtp+9pNtdZnpp3LvHuk/Lkz4XIjvpK2Xp+VFpLvyXrHlI3NQ9adr83sUydn
9mPQ09MutvyQUsojknw6yUm11if0c8K3pfWZ6fvbp9P6tI+P9OufWL+u9fxW2g2K+3v8ma1feWna
OdstaX3AU9MuiqxNW197pgXqf0ryqiRrev+2JMlXex/z1LTA+J2RZXZiWjCc7Tzmvtq/tpSyXdqy
eXev68C0c6NTRsp9Je0izCfT1vHD0s5NNiVrbFHb9FtkSynHJdln9CpNKWWntJ34HWmd3J5JPlNr
fVu/2vTdtA78BWk7y5PSrvq8t9b6d73MF9M2pNvTrjI9N+0K5nPS7oQtTdtYvpfk1LSrDKNX6Y9I
v1JRSlmedvXj6rSDz4fSDg53pW24v5p1d1Z+K23DeWb//B+9HUekXe05Oq2jfljaieN30zqUHdOu
rJyddrC7s7fz4WkH2lf1eXl42kb6t2l38fZOu1p3U9oVmZ173V9NC6GfSAtuO6d1zF9Lu7o6c+X+
Q2k71Jf7rH837ar5UX257tSnt1+Sb6ddCb437eT9xv796l72u72OR/Z23pl2InB71h3Y1/Tlcntv
z7y0q6KP7stzdZKJ/vOCPq01WXe3+d7e9u378Jv7z3+T5NfSOuV7si64XZZ2hWpV2na0LO3q1ovT
Tgo+n+SCtMC/T9qB/slZd3X57v5v5z7uk3r7vt7ncbe08PEjfZ4e2af9ziSv7ctnTdrVyBvT1vWd
fdiKtJO8XXtbr0pb1y/r7f1e//6ovg6/WGv9hb493pp2ErQs/aSnT/e6tBOhH+vLcOZq4J1Zt019
u7f3jr48v5R2cjSvf747bZ94dF9O16QdjPavtR5ZSvlmn/edRubz/LSTkIv6Mvp+X77z+nyekbbt
L+nr58a+Hr+Vtk39RJ/Gyl5+RZLd07blk9IO9n/Tl/GStDtIe6ZtI4f3tn4n67bPeWn71KvTTr6+
l3aycFra9rCiL5+fTtt+7urLZYe0Jwp+p9e/NMlP9vrWpJ1sPD7tCYuj0/aNvdIOco9L8nu11g/0
dfTIvm4/nLaPHtLn55a+fh/bl/Ur08LOrb3uZ6c9DfCGUsofpvVbv1ZrXZgkpZTJvs7PTjto79vb
OnNw/dE+73f09u7b521h2rb7ub4sHt3bsWNa/zkvrR8ovZ01bT/YIcnFaX3n3X3dfyjtKYP39/Fu
TrvwdXFf/membUO/l3aA/be+nPbp6++8tL7r7r78r+vr4IlZd2X55rSLVM/s87VdX49TfR53Gmn3
H6YF1/+V5sa0k63X9DuYt6X1e9/tdb0rrb94TF8u92Tkol5aX7wsyQG9rienXeD4kbRt7lNpx5//
7Otn77R99B/T1vkL0/qIr/dlubKPu2/aydC3k5yVdpHk9r6cb+3TuaWPsyCtP9gnbRt+b9o2+LW0
/eWetH3iF9L6ibVpF9vOSNs/durLdbe0ffjAPm93p20b59Zaf7uU8t+93rW9zqf3dXJ7X5c39bbP
7FPfSNt2Z/az7/b5vyPr9sd39jbu2Nt2V9qJ6N+nHY/PSjumfCrt+Llv2n7y8LS7lkf2OndLO9l7
dm/jrX3ZLUlb97em9c1r0o4dy9L6uZkLhrv3eV6ZdcebR6b17Z/v3830wdf3Zf+0XsfM/vg7SX6/
z8vtfR5+uY/37bQ7Fu/s6+wzaftVSetr7+j1zvRPq9O2wxvStvVlvdyFfRn/VJ/uHWn9yT192S3M
ujtQ8/q0Lsi6sDWz7C/v057pW27t6+uZafvAqrSLo1f0+Xx8Wv9f0vq6r6Tt2x/ry3hZWp9wTl8G
T07bb347LdDennauVfq6eljadnRdn59vpm3bu/a2XtXL7N3n5fLexuel7Ucz5wrTfblMpPXhb+j1
PLLP56+m/Wm7J6TtTzPL6frelnlZdzxb0+d9p77OVqX1IU9Lu2j44V7vqj79mT7n7iR/nLYtHdyX
8R19PV6VFqjXZt0dsivSttVX9np2Sds+VvVlsX0vv6J/95tpgX/ftIBxbF9Ov5O2/87sc5ekbT/P
6vN4b5+f3fv83JK2bX65f16c1mf9Sdpx5fC+PHfsy/6bvb4FSf53X4Yz51Mz7XtEn9YvpG0Pn0t7
auYpva7bk3yu1vrrpZRzsu4i7PfTnn7YOclf9mmu6Ovu6rRtfua8eMe0vmZNWj/6hv7/d9O2/TV9
nOf25T1zgXhNX24fTNs+LurD/iWtn/t42hNWP9mX0WRflrv39k2kbb979WW9Jq2fflRv08yx86tp
fdRkH+/QPmzP3pblfV6e2n/+997W5Wn7ydfTtqXja603jjxh85a0bfp9aecjZ6at/6/1dXVx2jYx
069O93W8e9pFwg+k3QH9jbRw+r+T/FXasfiGvo6uTuvzlqX1+09N68dv6W2/Ju187cIkq+sGnhTd
pu9gpnWE140OqLXekXWPZByTdnD5zf712rQrJ89JC13frbUeknYSfmopZfde5gu11qPSTlbu6OWv
TluBL03rkM5P20A+kmT/UsqKUsoVpZRL0jbwGY9Pe0TnDWk77en9Ssd70q64nZLW6Tw7Lai8PG0H
e3faSejb006MdkzbwL6ctqL/OO3AsSwtuG6fdoVuYdrB8+FpQeGYXv78tE7slrQTn9VpG81T0jqW
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
CAQ2Cv4fz68afc+XekAAAAAASUVORK5CYII=
"
>
</div>

</div>

</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">
In&nbsp;[17]:
</div>
<div class="inner_cell">
    <div class="input_area">
<div class="highlight"><pre><span class="c"># There are 12 original categorical variables in total</span>
<span class="c"># 7. &#39;first_device_type&#39; variable</span>
<span class="c"># (1) Visualization</span>
<span class="n">fig</span><span class="p">,</span> <span class="n">axis1</span> <span class="o">=</span> <span class="n">plt</span><span class="o">.</span><span class="n">subplots</span><span class="p">(</span><span class="mi">1</span><span class="p">,</span><span class="mi">1</span><span class="p">,</span><span class="n">sharex</span><span class="o">=</span><span class="bp">True</span><span class="p">,</span><span class="n">figsize</span><span class="o">=</span><span class="p">(</span><span class="mi">15</span><span class="p">,</span><span class="mi">8</span><span class="p">))</span>
<span class="n">sns</span><span class="o">.</span><span class="n">countplot</span><span class="p">(</span><span class="n">x</span><span class="o">=</span><span class="s">&#39;first_device_type&#39;</span><span class="p">,</span> <span class="n">data</span><span class="o">=</span><span class="n">fullData</span><span class="p">,</span> <span class="n">palette</span><span class="o">=</span><span class="s">&quot;husl&quot;</span><span class="p">,</span> <span class="n">ax</span><span class="o">=</span><span class="n">axis1</span><span class="p">)</span>

<span class="c"># (2) Fill NaN values randomly</span>
<span class="n">fullData</span> <span class="o">=</span> <span class="n">FillNaNRandom</span><span class="p">(</span><span class="n">fullData</span><span class="p">,</span> <span class="s">&#39;first_device_type&#39;</span><span class="p">)</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area"><div class="prompt"></div>
<div class="output_subarea output_stream output_stdout output_text">
<pre>
There are 9 different values in the list of :
Index([u&apos;Mac Desktop&apos;, u&apos;Windows Desktop&apos;, u&apos;iPhone&apos;, u&apos;iPad&apos;, u&apos;Other/Unknown&apos;, u&apos;Android Phone&apos;, u&apos;Android Tablet&apos;, u&apos;Desktop (Other)&apos;, u&apos;SmartPhone (Other)&apos;], dtype=&apos;object&apos;)
There is no NaN values for this variable!

</pre>
</div>
</div>

<div class="output_area"><div class="prompt"></div>


<div class="output_png output_subarea ">
<img src="data:image/png;base64,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
FaMPb1X2tOK7u6vqX5Lcr6r+OcmfZ2hxSIYNaUNVvTHJnTJceXhld589W05VPTXJA5P8QZIHJ7lH
VX06yfERSPcvAAASv0lEQVQZWuiuSfK5JKeO9X9IkluN/87o7r/Z7SW1sH/I0Kr08iQPTfL6JH9Q
VYcmWZfkgmS6UltJXpvkO0mOzvBF/8Xu/tg4n6cmuSzD8j6nqg7KsKzvkOEA/fIMwf7F3f2wqnps
hlbMH6mq45I8Icmbk7wsyZYk/5nkZ7v7W1vVeX9aP7tkvMJ5l62GHZTkZklml+cjqurnkhyW5HfG
FrOfz/zzfXKG5XenJH/Q3WeNF2VemWF9XJHkl8fv4b7kp5Jc0N2XzA7o7jeP+47XJPlKVf3T+Nbz
x4PITTP0YLi0ql6S5H4Zt+/ufvt4xfirGVoiH5Jh+3pGbji4bG3V2EJ+dJIjktw+yW909/lz3p/d
Tk9J8s8Zvpd3z7AffER3X1VVL8sNQemtGfaF7+3uHx1/v/bvu/uWVXW7DN/zt43z/z3rdaeX4I77
ngNqd3+7ql6b4cD7iW0sy6dn2C9cn+SS7n7mbFlVdWyG7e/RGXo6HDL+DNMXk5yZ5LsZ9lVPHst8
U4ar+LdJ8nfd/btb1e9pSWZbNX8hyZ939+fn1Pf3qurfquq2SX4xyXfGfU+SvHpskU6G48y3M2w/
d85wQfh53f2BqtqQpJNsGVsO/irDtvGbO7Ecd9vYqvu5DPvzs5OcNW63H0tyTIag8XPd/e9V9YIM
28mXkxyVG7bX+2b4LvzK+P5jMrSOXNjdzxnH+XKS/zVO5+5JvjCWvSN1nO/4vSrJg6vq5Az7sjO6
+z1zPnPUOK1DMvQyOTXDfv3IDNv7o3ZqQe3FtrOP3zx+z/8sQ8vMbTJsg++sqkdmOOZfkWH/8dYl
rfgS2Uu38bn7wMOSbB7//qGq+vsM+/93dfcLqupHM/9+7G1J/j3DPvuj3f30qrp55jn32clFNtc3
k/xgVf1ykvO6+xNVda9kahH9eIZl+K0kF2X4jv1Ahgt/12c4vtw8w0X3V3X3a+YcF2+Z5NIkd62q
3xnnZe5yuUWGc79Z8+1bv+e8srv/aoF1e1qG4+ZMkr/s7j/Zal732v2+lsTF8X9yw47/Xkn+KUmq
alWGjfGk7r53hnB4ryRPTfJv3X3fDFeXjt2BaXw1Qyg4PcNJ1wOSPCXDBnKzDC1wP5PhhHBuF4/T
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
"
>
</div>

</div>

</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">
In&nbsp;[18]:
</div>
<div class="inner_cell">
    <div class="input_area">
<div class="highlight"><pre><span class="c"># There are 12 original categorical variables in total</span>
<span class="c"># 8. &#39;Gender&#39; variable</span>
<span class="c"># (1) Visualization</span>
<span class="n">fig</span><span class="p">,</span> <span class="n">axis1</span> <span class="o">=</span> <span class="n">plt</span><span class="o">.</span><span class="n">subplots</span><span class="p">(</span><span class="mi">1</span><span class="p">,</span><span class="mi">1</span><span class="p">,</span><span class="n">sharex</span><span class="o">=</span><span class="bp">True</span><span class="p">,</span><span class="n">figsize</span><span class="o">=</span><span class="p">(</span><span class="mi">8</span><span class="p">,</span><span class="mi">4</span><span class="p">))</span>
<span class="n">sns</span><span class="o">.</span><span class="n">countplot</span><span class="p">(</span><span class="n">x</span><span class="o">=</span><span class="s">&#39;gender&#39;</span><span class="p">,</span> <span class="n">data</span><span class="o">=</span><span class="n">fullData</span><span class="p">,</span> <span class="n">palette</span><span class="o">=</span><span class="s">&quot;husl&quot;</span><span class="p">,</span> <span class="n">ax</span><span class="o">=</span><span class="n">axis1</span><span class="p">)</span>

<span class="c"># (2) Assign other categories to either &#39;MALE&#39; or &#39;FEMALE&#39; category</span>
<span class="n">i</span> <span class="o">=</span> <span class="mi">0</span>
<span class="k">def</span> <span class="nf">get_gender</span><span class="p">(</span><span class="n">gender</span><span class="p">):</span>
    <span class="k">global</span> <span class="n">i</span>
    <span class="k">if</span> <span class="n">gender</span> <span class="o">!=</span> <span class="s">&#39;FEMALE&#39;</span> <span class="ow">and</span> <span class="n">gender</span> <span class="o">!=</span> <span class="s">&#39;MALE&#39;</span><span class="p">:</span>
        <span class="k">return</span> <span class="s">&#39;FEMALE&#39;</span> <span class="k">if</span> <span class="p">(</span><span class="n">i</span><span class="o">%</span><span class="k">2</span><span class="p">)</span> <span class="k">else</span> <span class="s">&#39;MALE&#39;</span>
    <span class="n">i</span> <span class="o">=</span> <span class="n">i</span><span class="o">+</span><span class="mi">1</span>
    <span class="k">return</span> <span class="n">gender</span>
<span class="n">fullData</span><span class="p">[</span><span class="s">&#39;gender&#39;</span><span class="p">]</span> <span class="o">=</span> <span class="n">fullData</span><span class="p">[</span><span class="s">&#39;gender&#39;</span><span class="p">]</span><span class="o">.</span><span class="n">apply</span><span class="p">(</span><span class="n">get_gender</span><span class="p">)</span>

<span class="c"># (3) Map &#39;MALE&#39;to &#39;0&#39; and &#39;FEMALE&#39; to &#39;1&#39;</span>
<span class="n">fullData</span><span class="p">[</span><span class="s">&quot;gender&quot;</span><span class="p">]</span> <span class="o">=</span> <span class="n">fullData</span><span class="p">[</span><span class="s">&quot;gender&quot;</span><span class="p">]</span><span class="o">.</span><span class="n">map</span><span class="p">({</span><span class="s">&quot;FEMALE&quot;</span><span class="p">:</span> <span class="mi">1</span><span class="p">,</span> <span class="s">&quot;MALE&quot;</span><span class="p">:</span> <span class="mi">0</span><span class="p">})</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area"><div class="prompt"></div>


<div class="output_png output_subarea ">
<img src="data:image/png;base64,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
"
>
</div>

</div>

</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">
In&nbsp;[19]:
</div>
<div class="inner_cell">
    <div class="input_area">
<div class="highlight"><pre><span class="c"># (4) Look for insights</span>
<span class="n">fig</span><span class="p">,</span> <span class="p">(</span><span class="n">axis1</span><span class="p">,</span> <span class="n">axis2</span><span class="p">)</span> <span class="o">=</span> <span class="n">plt</span><span class="o">.</span><span class="n">subplots</span><span class="p">(</span><span class="mi">2</span><span class="p">,</span><span class="mi">1</span><span class="p">,</span><span class="n">sharex</span><span class="o">=</span><span class="bp">True</span><span class="p">,</span><span class="n">figsize</span><span class="o">=</span><span class="p">(</span><span class="mi">15</span><span class="p">,</span><span class="mi">8</span><span class="p">))</span>
<span class="c"># frequency of country_destination for every gender</span>
<span class="n">sns</span><span class="o">.</span><span class="n">countplot</span><span class="p">(</span><span class="n">x</span><span class="o">=</span><span class="s">&quot;gender&quot;</span><span class="p">,</span><span class="n">hue</span><span class="o">=</span><span class="s">&quot;country_destination&quot;</span><span class="p">,</span> <span class="n">data</span><span class="o">=</span><span class="n">fullData</span><span class="p">[</span><span class="n">fullData</span><span class="p">[</span><span class="s">&#39;country_destination&#39;</span><span class="p">]</span> <span class="o">!=</span> <span class="s">&#39;NDF&#39;</span><span class="p">],</span> <span class="n">palette</span><span class="o">=</span><span class="s">&quot;husl&quot;</span><span class="p">,</span> <span class="n">ax</span><span class="o">=</span><span class="n">axis1</span><span class="p">)</span>
<span class="c"># frequency of booked Vs no-booking users for every gender</span>
<span class="n">sns</span><span class="o">.</span><span class="n">countplot</span><span class="p">(</span><span class="n">x</span><span class="o">=</span><span class="s">&quot;gender&quot;</span><span class="p">,</span><span class="n">hue</span><span class="o">=</span><span class="s">&quot;booked&quot;</span><span class="p">,</span> <span class="n">data</span><span class="o">=</span><span class="n">fullData</span><span class="p">,</span> <span class="n">palette</span><span class="o">=</span><span class="s">&quot;husl&quot;</span><span class="p">,</span> <span class="n">ax</span><span class="o">=</span><span class="n">axis2</span><span class="p">)</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area"><div class="prompt output_prompt">
    Out[19]:</div>


<div class="output_text output_subarea output_pyout">
<pre>
&lt;matplotlib.axes._subplots.AxesSubplot at 0x110a56f10&gt;
</pre>
</div>

</div>

<div class="output_area"><div class="prompt"></div>


<div class="output_png output_subarea ">
<img src="data:image/png;base64,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
6N27Ny1bttxgLR999BEAn376KYsWLWKHHXZgt91245FHHmHcuHGcffbZ7LXXXjz77LPceeedjB49
moceegiATCazzr8bqnHGjBn89a9/ZcSIEVx00UUsW7Zs7Xdr6l5Ty7Rp0wD46quvmDFjBrvssssG
z3tLeYdQkiRJUtGce+653HDDDbz++uskk0l+/vOfc91115HJZNhll1244oorWLFiBY8//jgDBgyg
Z8+eGwyCAH369OHaa6/lmmuuWef7I488kqFDhzJ69OgN1rLffvux77770q9fP7p168b2229PIpHg
6quvZuDAgaxcuZJevXpx3nnnkUql6N+/P23atOG8884DoHfv3vzgBz/gW9/61np1rfl7jz32YOnS
pZx//vl0796dPfbYg2XLlrH//vvzH//xHwwbNoxEIsHee+/NgQceyHnnnUdNTQ0XX3wx22+//QbP
e0sl6qfXbVVlZWWmoqKi2GVs0MyZM/ns548XZcno/yz8jJ2u/J7PEEqSJGmbVl1dzaBBg3jssceK
XUpRVFZWUlFRsV569A6hJEmSpG3arFmzuO6667j66qsB+Oc//8kPf/jD9fpde+21NOUbSflgIJQk
SZK0TevZsyfPP//82s8777wz48aNK2JFTYebykiSJElSiTIQSpIkSVKJcsmoJEmSpGanpqaGdDqd
0zFTqRTJZDKnYzZ1BkJJkiRJzU46nabyjp+ye8dOORnvk8Wfw9BrSm73fQOhJEmSpGZp946dCvrq
tqlTp/LUU08xcuTItW0jRoxgzz33BOC3v/0tmUyG2tparrzySg4//PCC1bal8hoIQwgtgdFALyAD
XApUA48Cq4HpwBUxxkwIYRAwGFgJ3BFjnBhCaAM8DnQBqoCBMcaFIYRDgPuzfV+NMQ7L53lIkiRJ
UkMvgU8kElRVVfH444/zu9/9ju22247PPvuMfv368Yc//KEIVW6efG8qcyqwOsZ4BDAUuAu4DxgS
YzwSSACnhxC6AlcBhwEnAcNDCEngMmBatu9j2TEAfgGcnx33myGEPnk+D0mSJEklLpPJNNieTCap
ra3l17/+NXPnzmWnnXbitddeK3B1WyavgTDG+DxwSfZjClgEVMQYJ2fbXgaOB/4FmBJjrI0xLgFm
AQcAhwOvZPu+AhwfQigHkjHG2dn2SdkxJEmSJKngysrKGDt2LHPmzGHQoEEce+yxPPvss8Uuq1Hy
/gxhjHFVCOFR4AygH3BCva+rgO2BDsCXG2hfspG2Ne098lG7JEmSJK3Rpk0bampq1mlbvnw5ANXV
1dxyyy1A3YY3F198MQcffDB77bVXwevcHAXZVCbG+P0Qws7AH4Gyel91ABZTF/DK67WXN9DeUFv9
MTaqsrJyS8vPuzlz5lC4R2HXN336dKqqqopYgSRJkrR55syZQ/Xiz3M23ieLP+ezTfz/4uXLl/Ph
hx/y+uuv07FjR2pqapg8eTIhBK644gpuvfVWysrKqK2tJZlMEmNkyZIlGxyvKcj3pjIDgN1ijMOB
FcAq4P0QwlExxj8AJwOvUxcU7wwhtKYuMO5D3YYzU4BTgPeyfSfHGKtCCDUhhB7AbOBE4LZN1VJR
UZHr08uZ8vJyPnvzw6LN37t375LbXleSJEnN2/7770+6d++cjbcTjXsP4a233soDDzywNvgNHjyY
fv36kUgkGDFiBK1bt2b16tVccMEFnHrqqTmrb2tt6AZZvu8QPgM8GkL4A9AKuAaYAYzObhrzV+CZ
7C6jo4C3qHuucUiMsTqE8BAwNoTwFnW7k/bPjnspMB5oCUyKMb6X5/OQJGmblo8XPDdWKb4IWtLW
SyaTRbmpccIJJ3DCCSes196vXz/69etX8Hq2Vl4DYYxxBXBuA18d3UDfMcCYBo4/p4G+U4FDc1Ol
JEnK9QueG6tUXwQtSU2FL6aXJElA4V/wLEkqvny/h1CSJEmS1EQZCCVJkiSpRLlkVJIkSVKzk4/N
sEpxkysDoSRJkqRmJ51OM+nu/uy6Q9ucjPf3Rcs56cZfl9wmVwZCSZIkSc3Srju0ZY8u7Ypaw8yZ
M1myZAkHH3wwxx57LK+88kqzusvoM4SSJEmStIUmTZrErFmzil3GFvMOoSRJkiQ1Qm1tLTfddBPz
5s1j9erVnH/++Tz33HMkk0n23XdfAG699VbmzZsHwAMPPECbNm249dZbmTt3LqtXr+baa6+lb9++
nHrqqXTv3p1WrVoxcuTIop2TgVCSJEmSGuGpp56ic+fOjBgxgmXLlnHWWWdxzDHH0KtXLw444AAA
+vXrx0EHHcRNN93ElClTWLRoETvuuCN33XUXixYtYsCAAbz00kssX76cK664gr333ruo52QglCRJ
kqRG+Nvf/sZhhx0GQLt27ejRowdz585dZyOa3r17A9C5c2e++uorPv74Y95//32mTZsGwKpVq1i0
aBEA3bt3L/AZrM9AKEmSJKlZ+vui5Tkda/9N9Nlzzz15//33Of7441m6dCkff/wxZ511FqtWrdrg
MT169KBr165ccsklLF26lF/+8pd07NgRgEQikbP6t5SBUJIkSVKzk0qlOOnGX+dsvP2zY27MOeec
wy233EL//v356quvuPLKK9lhhx34yU9+wp577rlewEskEpx77rnccsstDBgwgKVLl9K/f38SiUST
CINgIJQkSZLUDCWTyYK/M7BVq1bcfffd67UfddRRALz++utr26677rq1f99zzz3rHVO/bzH52glJ
kiRJKlEGQkmSJEkqUQZCSZIkSSpRBkJJkiRJKlFuKiNJkiSp2ampqSGdTud0zFQqRTKZzOmYTZ2B
UJIkSVKzk06n+eXIc+jSqU1Oxlvw+Qou/MHTBd+5tNgMhJIkSZKapS6d2rDLTm0LNt+8efP4t3/7
N/bbb7+1bYcccgiPPPLI2raamhratm3LT3/6Uzp06FCw2raUgVCSJEmSGmmvvfZi3Lhxaz9/+umn
TJ48eZ22kSNH8swzz3DhhRcWo8TNkrdAGEJoBfwS2ANoDdwBzANeAmZmuz0YY5wQQhgEDAZWAnfE
GCeGENoAjwNdgCpgYIxxYQjhEOD+bN9XY4zD8nUOkiRJkrQxmUxmvc/z589njz32KFJFmyefdwi/
CyyIMQ4IIewATANuB+6LMY5c0ymE0BW4CqgA2gBvhxBeAy4DpsUYh4UQzgWGAtcCvwDOjDHODiFM
DCH0iTF+mMfzkCRJkiQAZs2axYABA9Z+/r//9/+ubfvyyy+prq7mtNNO48wzzyxilY2Xz0A4AXgm
+3cLoJa60BdCCKcDH1MX8PoCU2KMtUBtCGEWcABwOHBP9vhXgFtCCOVAMsY4O9s+CTgeMBBKkiRJ
yruePXuuszx03rx5a9uqq6u59NJL6dSpEy1aNI83/OUtEMYYlwFkQ9wE4GagDBgdY/wghDAEuJW6
MPdlvUOrgO2BDsCSjbStae+Rr3OQJEmS1HQt+HxFkxqrdevWjBgxgtNPP50DDzyQvffeOweV5Vde
N5UJIewO/AZ4IMb4ZAhh+xjjmvD3HPAzYDJQXu+wcmAxdcGvfCNtUBcQFzemlsrKyi09jbybM2cO
OxVx/unTp1NVVVXECiRJxVbMa5HXIUlbora2lr4n/jhn43UHvvjii43mhgULFrBs2bJ1+jTUds45
53DdddcxbFjT3+4kn5vK7Ay8ClweY3wj2/xKCOHqGON71C31fB/4I3BnCKE1dXcQ9wGmA1OAU4D3
gJOByTHGqhBCTQihBzAbOBG4rTH1VFRU5Ozccq28vJzP3izeqtfevXuX3PtWJEnrKua1yOuQpObk
29/+9ibbKioquPrqqwtVUqNsKOjm8w7hEOqWef44hLAmul8L/GcIoRaYDwyOMS4NIYwC3qLuWcMh
McbqEMJDwNgQwltANdA/O8alwHigJTApGy4lSZIkSZspn88QXgNc08BXRzTQdwww5mttK4BzGug7
FTg0R2VKkiRJUslqHlvfSJIkSZJyzkAoSZIkSSUqr7uMSpIkSVI+1NTUkE6nczpmKpUimUzmdMym
zkAoSZIkqdlJp9Pc+fN+7NC5LCfjLVr4FTdfOaHkdj02EEqSJElqlnboXEbnndsWdM6PP/6YESNG
sGLFCpYvX85RRx3FVVddBcDvfvc7br75ZiZNmsROOxXzTeON5zOEkiRJktQIS5Ys4Qc/+AE333wz
jz32GE8//TQzZ87kqaeeAmDChAn8+7//O08//XSRK208A6EkSZIkNcLrr7/OoYceSrdu3QBo0aIF
99xzD2eddRaffPIJS5Ys4eKLL+b5559n5cqVRa62cQyEkiRJktQICxYsYLfddlunrW3btrRq1Ypn
nnmGs846i/Lycvr06cOrr75apCo3j88QSpIkSVIj7LrrrvzlL39Zp23evHn8/e9/58UXX2S33Xbj
jTfe4Msvv2T8+PGccsopRaq08QyEkiRJkpqlRQu/KuhYRx99NA8//DD9+/dn9913p7a2lrvvvpu+
fftywAEHcP/996/te9JJJxFjJISQsxrzwUAoSZIkqdlJpVLcfOWEnI+5Me3bt+fuu+9m6NChrF69
mmXLlnHsscfyzjvvcO65567Tt1+/fowfP55hw4bltMZcMxBKkiRJanaSyWRR3hm43377MXbs2E32
u/jiiwtQzdZzUxlJkiRJKlEGQkmSJEkqUQZCSZIkSSpRBkJJkiRJKlFuKiNJkiSp2ampqSGdTud0
zFQqRTKZzOmYTZ2BUJIkSVKzk06nOWf0FbTp0j4n461YsJSnBz1QlJ1Li8lAKEmSJKlZatOlPW13
2b6gc37yySfce++9/POf/6SsrIyysjKuv/56Xn75ZV566SV22mknVq1aRfv27bnvvvsoLy8vaH2b
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
CAngIeDqBo5dEwL/DOwUQlgT/PoDxBiXAB+HEL4LkH3O8M28nYkkSV9jIJQkaSNijC9T9yzgB8BL
wN+B/wfcDvyeumWhAHdn/52pd3gGyGSXm55L3dLQSmCHev2+C1wcQpgG3Amc87XjJUnKm0Qm47VG
kqQNCSEcAvSKMT4WQmgFvANcEGOcvolDJUlq8gyEkiRtRAhhB+DXwC7Urax5NMY4srhVSZKUGwZC
SZIkSSpRPkMoSZIkSSXKQChJkiRJJcpAKEmSJEklykAoSZIkSSXKQChJkiRJJcpAKEmSJEklykAo
SZIkSSXKQChJkiRJJcpAKEmSJEklykAoSZIkSSXKQChJkiRJJcpAKEmSJEklykAoSZIkSSXKQChJ
kiRJJcpAKEmSJEklykAoSZIkSSXKQChJkiRJJcpAKEmSJEklykAoSZIkSSXKQChJkiRJJWq7fA0c
QmgBjAF6AauBQcAq4NHs5+nAFTHGTAhhEDAYWAncEWOcGEJoAzwOdAGqgIExxoUhhEOA+7N9X40x
DsvXOUiSJEnStiyfdwhPBNrFGI8AhgF3AfcBQ2KMRwIJ4PQQQlfgKuAw4CRgeAghCVwGTMv2fQwY
mh33F8D52XG/GULok8dzkCRJkqRtVj4D4Qpg+xBCAtgeqAEqYoyTs9+/DBwP/AswJcZYG2NcAswC
DgAOB17J9n0FOD6EUA4kY4yzs+2TsmNIkiRJkjZT3paMAlOAMmAG0Ak4DTiy3vdV1AXFDsCXG2hf
spG2Ne098lC7JEmSJG3z8hkIf0Tdnb+bQwi7AW8Arep93wFYTF3AK6/XXt5Ae0Nt9cfYqMrKyswW
noMkSZIkbRMqKioSX2/LZyBsx//ezVuUneuDEMJRMcY/ACcDrwN/BO4MIbSm7o7iPtRtODMFOAV4
L9t3coyxKoRQE0LoAcym7jnF2xpTTEVFRa7OS5IkSZKalcrKygbb8xkI7wV+FUJ4i7o7gzcBlcDo
7KYxfwWeye4yOgp4i7pnGofEGKtDCA8BY7PHVwP9s+NeCowHWgKTYozv5fEcJEmSJGmblchktv3V
lJWVlRnvEEqSJDU/NTU1pNPpYpchbVAqlSKZTBa7jE2qrKws+JJRSZIkaauk02nOe/jntOncqdil
SOtZsfBznrzkSnr16lXsUraYgVCSJElNWpvOnWjXdedilyFtk/L5HkJJkiRJUhNmIJQkSZKkEmUg
lCRJkqQSZSCs5ze/+Q1jx47domNvvPFGpk2btlnHPProozz33HNbNJ8kSZIkbS0DYT2JxHq7sG7W
sZt7/NbMJ0mSJElby11Gv+bNN9/k9ddfJ5PJcMcdd/Doo48yY8YMMpkM11xzDYceeijPPvssTz75
JC1atOCkk07iwgsvBCCTyTBp0iSef/557r//fqZOncoDDzxAIpHg2GOPZdCgQcycOZOhQ4fSrl07
EokEp512WpHPWJIkSVKpMhDWk8lk6Nq1K8OHD+f999/n7LPP5uSTT+aJJ57giy++4Hvf+x7jx49n
/PjxPP3007Ro0YKBAwdy1FFHAfDGG28wY8YMfvazn9GyZUt+8pOf8OSTT9K2bVsuu+wyjj32WO67
7z5uu+029t13X2688cYin7EkSZKkUmYgrCeRSHDggQcCsP/++7N06VIOOuggAHbccUfat2/PJ598
QgiB7bar+5/uG9/4BrNnzwbg/fffB2C77bbjiy++4J///CeXXnopAEuXLuWTTz5h7ty57LvvvgD0
6dOnoOcnSZIkSfX5DGE9mUyGv/zlLwB8+OGHtGnThj/96U8AfPHFFyxevJjddtuNGCMrV65k1apV
fPjhh+y+++4AXH/99fTp04exY8ey4447sttuu/HII48wbtw4zj77bPbaay/22GMP/vznPwMwffr0
4pyoJEmSJOEdwnUkEgnmz5/PwIEDSSQSTJw4kYcffpj+/ftTXV3NzTffzI477sj5559P//79WbVq
FSeccAIhhLXHX3nllfTr14/jjjuOq6++moEDB7Jy5Up69erFeeedxw033MBNN91EWVkZZWVlbiwj
SZIkqWgSmUym2DXkXWVlZaaioqLYZUiSJGkzzZw5kwuefYJ2XXcudinSepb945/86jvn06tXr2KX
skmVlZVUVFSsdzfKJaOSJEmSVKJcMippo2pqakin08UuQ2pQKpUimUwWuwxJkpotA6GkjUqn05z3
8M9p07lTsUuR1rFi4ec8ecmVzWKZjiRJTZWBUNImtencyWc3JEmStkF5DYQhhIHA97Mf2wDfAI4A
fgqsBqYDV8QYMyGEQcBgYCVwR4xxYgihDfA40AWoAgbGGBeGEA4B7s/2fTXGOCyf5yFJkiRJ26K8
BsIY41hgLEAI4efAGODHwJAY4+QQwkPA6SGEd4GrgArqguPbIYTXgMuAaTHGYSGEc4GhwLXAL4Az
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
"
>
</div>

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
<div class="highlight"><pre><span class="c"># There are 12 original categorical variables in total</span>
<span class="c"># 9. &#39;id&#39; variable</span>
<span class="c"># (1) Visualization</span>
<span class="n">fullData</span><span class="p">[</span><span class="s">&#39;id&#39;</span><span class="p">]</span><span class="o">.</span><span class="n">iloc</span><span class="p">[</span><span class="mi">0</span><span class="p">]</span> <span class="c"># it shows &#39;gxn3p5htnn&#39;</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area"><div class="prompt output_prompt">
    Out[20]:</div>


<div class="output_text output_subarea output_pyout">
<pre>
&apos;gxn3p5htnn&apos;
</pre>
</div>

</div>

</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">
In&nbsp;[21]:
</div>
<div class="inner_cell">
    <div class="input_area">
<div class="highlight"><pre><span class="c"># There are 12 original categorical variables in total</span>
<span class="c"># 10. &#39;language&#39; variable</span>
<span class="c"># (1) Visualization</span>
<span class="n">fig</span><span class="p">,</span> <span class="n">axis1</span> <span class="o">=</span> <span class="n">plt</span><span class="o">.</span><span class="n">subplots</span><span class="p">(</span><span class="mi">1</span><span class="p">,</span><span class="mi">1</span><span class="p">,</span><span class="n">sharex</span><span class="o">=</span><span class="bp">True</span><span class="p">,</span><span class="n">figsize</span><span class="o">=</span><span class="p">(</span><span class="mi">8</span><span class="p">,</span><span class="mi">4</span><span class="p">))</span>
<span class="n">sns</span><span class="o">.</span><span class="n">countplot</span><span class="p">(</span><span class="n">x</span><span class="o">=</span><span class="s">&#39;language&#39;</span><span class="p">,</span> <span class="n">data</span><span class="o">=</span><span class="n">fullData</span><span class="p">,</span> <span class="n">palette</span><span class="o">=</span><span class="s">&quot;husl&quot;</span><span class="p">,</span> <span class="n">ax</span><span class="o">=</span><span class="n">axis1</span><span class="p">)</span>

<span class="c"># (2) Fill NaN values randomly</span>
<span class="n">fullData</span> <span class="o">=</span> <span class="n">FillNaNRandom</span><span class="p">(</span><span class="n">fullData</span><span class="p">,</span> <span class="s">&#39;language&#39;</span><span class="p">)</span>

<span class="c"># (3) Binary process</span>
<span class="n">fullData</span><span class="p">[</span><span class="s">&quot;language&quot;</span><span class="p">]</span> <span class="o">=</span> <span class="p">(</span><span class="n">fullData</span><span class="p">[</span><span class="s">&quot;language&quot;</span><span class="p">]</span> <span class="o">==</span> <span class="s">&#39;en&#39;</span><span class="p">)</span><span class="o">.</span><span class="n">astype</span><span class="p">(</span><span class="nb">int</span><span class="p">)</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area"><div class="prompt"></div>
<div class="output_subarea output_stream output_stdout output_text">
<pre>
There are 26 different values in the list of :
Index([u&apos;en&apos;, u&apos;zh&apos;, u&apos;fr&apos;, u&apos;es&apos;, u&apos;ko&apos;, u&apos;de&apos;, u&apos;it&apos;, u&apos;ru&apos;, u&apos;ja&apos;, u&apos;pt&apos;, u&apos;sv&apos;, u&apos;nl&apos;, u&apos;tr&apos;, u&apos;da&apos;, u&apos;pl&apos;, u&apos;no&apos;, u&apos;cs&apos;, u&apos;el&apos;, u&apos;th&apos;, u&apos;hu&apos;, u&apos;id&apos;, u&apos;fi&apos;, u&apos;ca&apos;, u&apos;is&apos;, u&apos;hr&apos;, u&apos;-unknown-&apos;], dtype=&apos;object&apos;)
There is no NaN values for this variable!

</pre>
</div>
</div>

<div class="output_area"><div class="prompt"></div>


<div class="output_png output_subarea ">
<img src="data:image/png;base64,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
RU5ErkJggg==
"
>
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
<div class="highlight"><pre><span class="c"># There are 12 original categorical variables in total</span>
<span class="c"># 11-12. &#39;signup_method&#39; and &#39;signup_flow&#39; variable</span>
<span class="c"># (1) Visualization</span>
<span class="n">fig</span><span class="p">,</span> <span class="n">axis1</span> <span class="o">=</span> <span class="n">plt</span><span class="o">.</span><span class="n">subplots</span><span class="p">(</span><span class="mi">1</span><span class="p">,</span><span class="mi">1</span><span class="p">,</span><span class="n">sharex</span><span class="o">=</span><span class="bp">True</span><span class="p">,</span><span class="n">figsize</span><span class="o">=</span><span class="p">(</span><span class="mi">15</span><span class="p">,</span><span class="mi">8</span><span class="p">))</span>
<span class="n">sns</span><span class="o">.</span><span class="n">countplot</span><span class="p">(</span><span class="n">x</span><span class="o">=</span><span class="s">&#39;signup_method&#39;</span><span class="p">,</span> <span class="n">data</span><span class="o">=</span><span class="n">fullData</span><span class="p">,</span> <span class="n">palette</span><span class="o">=</span><span class="s">&quot;husl&quot;</span><span class="p">,</span> <span class="n">ax</span><span class="o">=</span><span class="n">axis1</span><span class="p">)</span>

<span class="c"># (2) Fill NaN values randomly</span>
<span class="n">fullData</span> <span class="o">=</span> <span class="n">FillNaNRandom</span><span class="p">(</span><span class="n">fullData</span><span class="p">,</span> <span class="s">&#39;signup_method&#39;</span><span class="p">)</span>
<span class="n">fullData</span> <span class="o">=</span> <span class="n">FillNaNRandom</span><span class="p">(</span><span class="n">fullData</span><span class="p">,</span> <span class="s">&#39;signup_flow&#39;</span><span class="p">)</span>

<span class="c"># (3) Binary process</span>
<span class="n">fullData</span><span class="p">[</span><span class="s">&quot;signup_method&quot;</span><span class="p">]</span> <span class="o">=</span> <span class="p">(</span><span class="n">fullData</span><span class="p">[</span><span class="s">&quot;signup_method&quot;</span><span class="p">]</span> <span class="o">==</span> <span class="s">&quot;basic&quot;</span><span class="p">)</span><span class="o">.</span><span class="n">astype</span><span class="p">(</span><span class="nb">int</span><span class="p">)</span>
<span class="n">fullData</span><span class="p">[</span><span class="s">&quot;signup_flow&quot;</span><span class="p">]</span> <span class="o">=</span> <span class="p">(</span><span class="n">fullData</span><span class="p">[</span><span class="s">&quot;signup_flow&quot;</span><span class="p">]</span> <span class="o">==</span> <span class="mi">3</span><span class="p">)</span><span class="o">.</span><span class="n">astype</span><span class="p">(</span><span class="nb">int</span><span class="p">)</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area"><div class="prompt"></div>
<div class="output_subarea output_stream output_stdout output_text">
<pre>
There are 4 different values in the list of :
Index([u&apos;basic&apos;, u&apos;facebook&apos;, u&apos;google&apos;, u&apos;weibo&apos;], dtype=&apos;object&apos;)
There is no NaN values for this variable!
There are 18 different values in the list of :
Int64Index([0, 25, 12, 3, 2, 23, 24, 1, 8, 6, 21, 5, 20, 16, 15, 14, 10, 4], dtype=&apos;int64&apos;)
There is no NaN values for this variable!

</pre>
</div>
</div>

<div class="output_area"><div class="prompt"></div>


<div class="output_png output_subarea ">
<img src="data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAA4oAAAHwCAYAAADgq5F2AAAABHNCSVQICAgIfAhkiAAAAAlwSFlz
AAALEgAACxIB0t1+/AAAIABJREFUeJzt3Xu4XXdd5/FPSg0tkIKUq1ItIPmKVgQCFigW0EoFvOGo
3IZBHFq5iDCjD/LUChVhUAQGiwgKIlfFKeLtKbRVbi2VSwlYjDDfWm1ivYzYYmlEaHo588dasecX
TpLTNuec9uT1ep4+OXvtddb+rT5Z2fu9f2uvvWFhYSEAAACw2yFrPQAAAABuXoQiAAAAA6EIAADA
QCgCAAAwEIoAAAAMhCIAAACDQ1dqw1X1NUnenOQbk9w6yUuTfC7JW5Jcl2Rbkud090JVnZTk5CTX
JHlpd59ZVYcneUeSOyfZmeRp3X1ZVT0kyWvmdc/p7pfMj/fiJI+dlz+/uy9YqX0DAABYz1ZyRvEp
Sf61u49P8r1JXpfkVUlOmZdtSPKDVXW3JM9N8rAkJyZ5eVVtTPKsJBfO674tyanzdt+Q5End/fAk
x1bV/avqgUmO7+5jkzxxfiwAAABuhJUMxTOSvGjR41yd5IHdfe687H1JTkjy4CTnd/fV3X1lkouT
3C/JcUnOmtc9K8kJVbUpycbuvmRefva8jeOSnJMk3X1pkkOr6sgV3DcAAIB1a8VCsbu/1N3/Psfd
GZlmBBc/3s4kt09yRJIv7mX5lftYtpxtAAAAcAOt2GcUk6SqjkryniSv6+7fq6pXLLr7iCRXZAq/
TYuWb1pi+VLLFm9j1162sVdbt25duKH7AwAAsJ5s2bJlw1LLV/JiNnfNdDros7v7g/PiT1fVI7r7
w0kek+T9ST6R5GVVdeskhyW5b6YL3Zyf6eI0F8zrntvdO6tqV1XdK8klSR6d5LQk1yZ5RVW9MslR
SQ7p7i/sb4xbtmw5YPsLAABwS7J169a93reSM4qnZDr980VVtfuzis9Lcvp8sZrPJnn3fNXT05Oc
l+nU1FO6+6qqen2St1bVeUmuSvLkeRvPTPLOJLdKcvbuq5vO63103sazV3C/AAAA1rUNCwsH5xmY
W7duXTCjCDcfu3btyvbt29d6GLBXRx99dDZu3LjWwwCAA2br1q2rf+opwA2xffv2vPL0H80djzxs
rYcCX+ULl38lP/vTZ2Tz5s1rPRQAWBVCEbjZuOORh+XOd73NWg8DAOCgt5LfowgAAMAtkFAEAABg
IBQBAAAYCEUAAAAGQhEAAICBUAQAAGAgFAEAABgIRQAAAAZCEQAAgIFQBAAAYCAUAQAAGAhFAAAA
BkIRAACAgVAEAABgIBQBAAAYCEUAAAAGQhEAAICBUAQAAGAgFAEAABgIRQAAAAZCEQAAgIFQBAAA
YCAUAQAAGAhFAAAABkIRAACAgVAEAABgIBQBAAAYCEUAAAAGQhEAAICBUAQAAGAgFAEAABgIRQAA
AAZCEQAAgIFQBAAAYCAUAQAAGAhFAAAABkIRAACAgVAEAABgIBQBAAAYCEUAAAAGQhEAAICBUAQA
AGAgFAEAABgIRQAAAAZCEQAAgIFQBAAAYCAUAQAAGAhFAAAABkIRAACAgVAEAABgIBQBAAAYCEUA
AAAGQhEAAICBUAQAAGAgFAEAABgIRQAAAAZCEQAAgIFQBAAAYCAUAQAAGAhFAAAABkIRAACAgVAE
AABgIBQBAAAYCEUAAAAGQhEAAICBUAQAAGAgFAEAABgIRQAAAAZCEQAAgIFQBAAAYCAUAQAAGAhF
AAAABkIRAACAgVAEAABgIBQBAAAYCEUAAAAGQhEAAICBUAQAAGAgFAEAABgIRQAAAAZCEQAAgIFQ
BAAAYCAUAQAAGAhFAAAABkIRAACAgVAEAABgIBQBAAAYCEUAAAAGQhEAAICBUAQAAGAgFAEAABgI
RQAAAAZCEQAAgIFQBAAAYCAUAQAAGAhFAAAABkIRAACAgVAEAABgIBQBAAAYCEUAAAAGQhEAAICB
UAQAAGBw6Eo/QFUdm+SXu/tRVfWAJH+a5G/mu3+ju8+oqpOSnJzkmiQv7e4zq+rwJO9IcuckO5M8
rbsvq6qHJHnNvO453f2S+XFenOSx8/Lnd/cFK71vAAAA69GKhmJVvSDJf03y7/OiLUle3d2vXrTO
3ZI8d77v8CQfqao/S/KsJBd290uq6glJTk3y/CRvSPL47r6kqs6sqvtnmhk9vruPraqjkvxBku9Y
yX0DAABYr1b61NOLk/xwkg3z7S1JHldVH66qN1XV7TIF3fndfXV3Xzn/zv2SHJfkrPn3zkpyQlVt
SrKxuy+Zl5+d5IR53XOSpLsvTXJoVR25wvsGAACwLq1oKHb3ezKdCrrbx5P8bHc/IsnfJXlxkk1J
vrhonZ1Jbp/kiCRX7mPZnsuX2gYAAAA30Ip/RnEPf9jdu4PuD5O8Nsm5mWJxt01JrsgUhJv2sSyZ
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
T/LA7j53vv99SR6d5Nok53f31UmurqqLk9wvyXFJfmVe96wkv1BVm5Js7O5L5uVnJzkhyV+uxg4B
AACsJ2vxGcUvJfnV7j4xyTOTvHOP+3cmuX2SI3L96al7Lr9yH8sWLwcAAOAGWosZxYuSXJwk3f03
VXV5kgcsuv+IJFdkCr9Ni5ZvWmL5UssWb2Oftm7deuP2YAk7duzIXQ7Y1uDA2rZtW3bu3LnWw9in
HTt2rPUQYJ9uCccRABwoaxGKT890CulzqurrMgXeOVX1iO7+cJLHJHl/kk8keVlV3TrJYUnum+lC
N+cneWySC+Z1z+3unVW1q6ruleSSTKeunra/gWzZsuWA7dSmTZvy+Q8505Wbp2OOOSabN29e62Hs
06ZNm/KJC9d6FLB3t4TjCABuiH1NnK1FKP52kt+pqt2fSXx6ksuTvHG+WM1nk7x7vurp6UnOy3SK
7CndfVVVvT7JW6vqvCRXJXnyvJ3dp7HeKsnZ3X3B6u0SAADA+rHqodjd1yR56hJ3PXKJdd+U5E17
LPtykh9bYt2PJ3nogRklAADAwWstLmYDAADAzZhQBAAAYCAUAQAAGAhFAAAABkIRAACAgVAEAABg
IBQBAAAYCEUAAAAGQhEAAICBUAQAAGAgFAEAABgIRQAAAAZCEQAAgIFQBAAAYCAUAQAAGAhFAAAA
BkIRAACAgVAEAABgIBQBAAAYCEUAAAAGQhEAAICBUAQAAGAgFAEAABgIRQAAAAZCEQAAgIFQBAAA
YCAUAQAAGAhFAAAABkIRAACAgVAEAABgIBQBAAAYCEUAAAAGQhEAAICBUAQAAGAgFAEAABgIRQAA
AAZCEQAAgIFQBAAAYCAUAQAAGAhFAAAABkIRAACAgVAEAABgIBQBAAAYCEUAAAAGQhEAAICBUAQA
AGAgFAEAABgIRQAAAAZCEQAAgIFQBAAAYCAUAQAAGAhFAAAABkIRAACAgVAEAABgIBQBAAAYCEUA
AAAGQhEAAICBUAQAAGAgFAEAABgIRQAAAAZCEQAAgIFQBAAAYCAUAQAAGAhFAAAABkIRAACAgVAE
AABgIBQBAAAYCEUAAAAGQhEAAICBUAQAAGAgFAEAABgIRQAAAAZCEQAAgIFQBAAAYCAUAQAAGAhF
AAAABkIRAACAgVAEAABgIBQBAAAYCEUAAAAGQhEAAICBUAQAAGAgFAEAABgIRQAAAAZCEQAAgIFQ
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
"
>
</div>

</div>

</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">
In&nbsp;[23]:
</div>
<div class="inner_cell">
    <div class="input_area">
<div class="highlight"><pre><span class="c"># 1.3 Process remaining &#39;object&#39; type variables</span>
<span class="c"># We will create a corresponding unique numerical value for each non-numerical value in a column.</span>
<span class="n">ID_col</span> <span class="o">=</span> <span class="s">&#39;user_id&#39;</span>
<span class="n">target_col</span> <span class="o">=</span> <span class="s">&#39;country_destination&#39;</span>

<span class="kn">from</span> <span class="nn">sklearn</span> <span class="kn">import</span> <span class="n">preprocessing</span>

<span class="k">for</span> <span class="n">f</span> <span class="ow">in</span> <span class="n">fullData</span><span class="o">.</span><span class="n">columns</span><span class="p">:</span>
    <span class="k">if</span> <span class="n">f</span> <span class="o">==</span> <span class="n">target_col</span> <span class="ow">or</span> <span class="n">f</span> <span class="o">==</span> <span class="n">ID_col</span> <span class="ow">or</span> <span class="n">f</span> <span class="o">==</span> <span class="s">&#39;Type&#39;</span><span class="p">:</span> <span class="k">continue</span>
    <span class="k">if</span> <span class="n">fullData</span><span class="p">[</span><span class="n">f</span><span class="p">]</span><span class="o">.</span><span class="n">dtype</span> <span class="o">==</span> <span class="s">&#39;object&#39;</span><span class="p">:</span>
        <span class="n">lbl</span> <span class="o">=</span> <span class="n">preprocessing</span><span class="o">.</span><span class="n">LabelEncoder</span><span class="p">()</span>
        <span class="n">lbl</span><span class="o">.</span><span class="n">fit</span><span class="p">(</span><span class="n">np</span><span class="o">.</span><span class="n">unique</span><span class="p">(</span><span class="nb">list</span><span class="p">(</span><span class="n">fullData</span><span class="p">[</span><span class="n">f</span><span class="p">]</span><span class="o">.</span><span class="n">values</span><span class="p">)))</span>
        <span class="n">fullData</span><span class="p">[</span><span class="n">f</span><span class="p">]</span> <span class="o">=</span> <span class="n">lbl</span><span class="o">.</span><span class="n">transform</span><span class="p">(</span><span class="nb">list</span><span class="p">(</span><span class="n">fullData</span><span class="p">[</span><span class="n">f</span><span class="p">]</span><span class="o">.</span><span class="n">values</span><span class="p">))</span>
</pre></div>

</div>
</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">
In&nbsp;[24]:
</div>
<div class="inner_cell">
    <div class="input_area">
<div class="highlight"><pre><span class="n">fullData</span><span class="o">.</span><span class="n">dtypes</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area"><div class="prompt output_prompt">
    Out[24]:</div>


<div class="output_text output_subarea output_pyout">
<pre>
Type                        object
affiliate_channel            int64
affiliate_provider           int64
age                        float64
country_destination         object
date_first_booking           int64
first_affiliate_tracked      int64
first_browser                int64
first_device_type            int64
gender                       int64
id                           int64
language                     int64
signup_app                   int64
signup_flow                  int64
signup_method                int64
booked                       int64
Year                         int64
Month                        int64
dtype: object
</pre>
</div>

</div>

</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">
In&nbsp;[25]:
</div>
<div class="inner_cell">
    <div class="input_area">
<div class="highlight"><pre><span class="c"># 1.4 Particular process of numerical variable &#39;age&#39;</span>
<span class="c"># 1.4.1 Find and remove outliers by assigning all age values &gt; 100 to NaN, these NaN values will be replaced with real ages below</span>
<span class="n">a</span> <span class="o">=</span> <span class="n">fullData</span><span class="o">.</span><span class="n">age</span><span class="o">.</span><span class="n">values</span>
<span class="n">fullData</span><span class="p">[</span><span class="s">&#39;age&#39;</span><span class="p">]</span> <span class="o">=</span> <span class="n">np</span><span class="o">.</span><span class="n">where</span><span class="p">(</span><span class="n">a</span> <span class="o">&gt;</span><span class="mi">100</span><span class="p">,</span> <span class="n">np</span><span class="o">.</span><span class="n">nan</span><span class="p">,</span> <span class="n">a</span><span class="p">)</span>

<span class="c"># get average, std, and number of NaN values in fullData</span>
<span class="n">average_age</span>   <span class="o">=</span> <span class="n">fullData</span><span class="o">.</span><span class="n">age</span><span class="o">.</span><span class="n">mean</span><span class="p">()</span>
<span class="n">std_age</span>       <span class="o">=</span> <span class="n">fullData</span><span class="o">.</span><span class="n">age</span><span class="o">.</span><span class="n">std</span><span class="p">()</span>
<span class="n">count_nan_age</span> <span class="o">=</span> <span class="n">fullData</span><span class="o">.</span><span class="n">age</span><span class="o">.</span><span class="n">isnull</span><span class="p">()</span><span class="o">.</span><span class="n">sum</span><span class="p">()</span>
<span class="k">print</span> <span class="n">count_nan_age</span>

<span class="c"># generate random numbers between (mean - std) &amp; (mean + std)</span>
<span class="n">rand</span> <span class="o">=</span> <span class="n">np</span><span class="o">.</span><span class="n">random</span><span class="o">.</span><span class="n">randint</span><span class="p">(</span><span class="n">average_age</span> <span class="o">-</span> <span class="n">std_age</span><span class="p">,</span> <span class="n">average_age</span> <span class="o">+</span> <span class="n">std_age</span><span class="p">,</span> <span class="n">size</span> <span class="o">=</span> <span class="n">count_nan_age</span><span class="p">)</span>

<span class="c"># fill NaN values in Age column with random values generated</span>
<span class="n">fullData</span><span class="p">[</span><span class="s">&quot;age&quot;</span><span class="p">][</span><span class="n">np</span><span class="o">.</span><span class="n">isnan</span><span class="p">(</span><span class="n">fullData</span><span class="o">.</span><span class="n">age</span><span class="p">)]</span> <span class="o">=</span> <span class="n">rand</span>

<span class="c"># convert type to integer</span>
<span class="n">fullData</span><span class="p">[</span><span class="s">&#39;age&#39;</span><span class="p">]</span> <span class="o">=</span> <span class="n">fullData</span><span class="o">.</span><span class="n">age</span><span class="o">.</span><span class="n">astype</span><span class="p">(</span><span class="nb">int</span><span class="p">)</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area"><div class="prompt"></div>
<div class="output_subarea output_stream output_stdout output_text">
<pre>
119556

</pre>
</div>
</div>

<div class="output_area"><div class="prompt"></div>
<div class="output_subarea output_stream output_stderr output_text">
<pre>
-c:16: SettingWithCopyWarning: 
A value is trying to be set on a copy of a slice from a DataFrame

See the the caveats in the documentation: http://pandas.pydata.org/pandas-docs/stable/indexing.html#indexing-view-versus-copy

</pre>
</div>
</div>

</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">
In&nbsp;[26]:
</div>
<div class="inner_cell">
    <div class="input_area">
<div class="highlight"><pre><span class="c"># 1.4.2 Check our converting, see if it makes sense</span>
<span class="n">fig</span><span class="p">,</span> <span class="p">(</span><span class="n">axis1</span><span class="p">,</span> <span class="n">axis2</span><span class="p">)</span> <span class="o">=</span> <span class="n">plt</span><span class="o">.</span><span class="n">subplots</span><span class="p">(</span><span class="mi">2</span><span class="p">,</span><span class="mi">1</span><span class="p">,</span><span class="n">figsize</span><span class="o">=</span><span class="p">(</span><span class="mi">15</span><span class="p">,</span><span class="mi">10</span><span class="p">))</span>

<span class="c"># frequency for age values(in case there was a booking)</span>
<span class="n">fullData</span><span class="p">[</span><span class="s">&#39;age&#39;</span><span class="p">][</span><span class="n">fullData</span><span class="o">.</span><span class="n">country_destination</span> <span class="o">!=</span> <span class="s">&#39;NDF&#39;</span><span class="p">]</span><span class="o">.</span><span class="n">hist</span><span class="p">(</span><span class="n">ax</span><span class="o">=</span><span class="n">axis1</span><span class="p">)</span>

<span class="c"># cut age values into ranges </span>
<span class="n">fullData</span><span class="p">[</span><span class="s">&#39;age_range&#39;</span><span class="p">]</span> <span class="o">=</span> <span class="n">pd</span><span class="o">.</span><span class="n">cut</span><span class="p">(</span><span class="n">fullData</span><span class="o">.</span><span class="n">age</span><span class="p">,</span> <span class="p">[</span><span class="mi">0</span><span class="p">,</span> <span class="mi">20</span><span class="p">,</span> <span class="mi">40</span><span class="p">,</span> <span class="mi">60</span><span class="p">,</span> <span class="mi">80</span><span class="p">,</span> <span class="mi">100</span><span class="p">])</span>

<span class="c"># frequency of country_destination for every age range</span>
<span class="n">sns</span><span class="o">.</span><span class="n">countplot</span><span class="p">(</span><span class="n">x</span><span class="o">=</span><span class="s">&quot;age_range&quot;</span><span class="p">,</span><span class="n">hue</span><span class="o">=</span><span class="s">&quot;country_destination&quot;</span><span class="p">,</span> <span class="n">data</span><span class="o">=</span><span class="n">fullData</span><span class="p">[</span><span class="n">fullData</span><span class="o">.</span><span class="n">country_destination</span> <span class="o">!=</span> <span class="s">&#39;NDF&#39;</span><span class="p">],</span> <span class="n">palette</span><span class="o">=</span><span class="s">&quot;husl&quot;</span><span class="p">,</span> <span class="n">ax</span><span class="o">=</span><span class="n">axis2</span><span class="p">)</span>

<span class="c"># drop age_range</span>
<span class="n">fullData</span><span class="o">.</span><span class="n">drop</span><span class="p">([</span><span class="s">&#39;age_range&#39;</span><span class="p">],</span> <span class="n">axis</span><span class="o">=</span><span class="mi">1</span><span class="p">,</span> <span class="n">inplace</span><span class="o">=</span><span class="bp">True</span><span class="p">)</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area"><div class="prompt"></div>


<div class="output_png output_subarea ">
<img src="data:image/png;base64,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
SZISGRglSZIkSYnc9GYX1dTUUFFRkdc5S0tLSafTeZ1TkiRJkhrKwLiLKioquOPng9lrn/Z5mW/p
kjXcdPVTjb7zqiRJkiRtzsCYB3vt0559Pt+xUT/nu+++y7hx41i9ejWrVq3ihBNO4JprrgHg97//
PTfddBMzZ86kW7dujdqXJEmSpJbDexiboeXLl/P973+fm266iSlTpvDkk0/yzjvv8MQTTwDw1FNP
8e1vf5snn3yyyJ1KkiRJas4MjM3Qiy++yDHHHMMBBxwAwG677cadd97JOeecw4cffsjy5cu59NJL
+e1vf8u6deuK3K0kSZKk5srA2AwtXryY/ffff5Nax44dadu2LU8//TTnnHMOJSUl9OvXj1mzZhWp
S0mSJEnNnfcwNkP77rsvf/nLXzapLVy4kL///e88++yz7L///rz00kssW7aM6dOnc/rppxepU0mS
JEnNmYExD5YuWdOoc5144on88pe/ZMiQIXzhC19g7dq1/PjHP+aoo46ib9++3HPPPRvHnnrqqcQY
CSHkrUdJkiRJrYOBcReVlpZy09VP5X3Obdlzzz358Y9/zMiRI6mtrWXlypWcfPLJvPLKK5x33nmb
jB08eDDTp09n1KhRee1RkiRJUstnYNxF6XS6KO+ZeNhhh/HII49sd9yll17aCN1IkiRJaonc9EaS
JEmSlMjAKEmSJElKZGCUJEmSJCUyMEqSJEmSErnpzS6qqamhoqIir3OWlpaSTqfzOqckSZIkNZSB
cRdVVFRw7sSr6NB1z7zMt3rxCp4cdm9Rdl6VJEmSpPoMjHnQoeuedOzRuVE/54cffshdd93FJ598
Qvv27Wnfvj033HADL7zwAs899xzdunVj/fr17Lnnntx9992UlJQ0an+SJEmSmj8DYzO0evVqrrzy
SkaPHs2Xv/xlAP785z9z++23c/TRR3PJJZdw3nnnAfDTn/6Up556iksuuaSYLUuSJElqhtz0phl6
6aWX6N+//8awCNC3b1+mTp0KQF1d3cb6Z599RpcuXRq9R0mSJEnNn2cYm6GFCxdywAEHbHx85ZVX
UlVVxeLFiznyyCN59tlnef7551m2bBnLly/nyiuvLGK3kiRJkporA2Mz1KNHD+bNm7fx8S9+8QsA
zjvvPNavX7/JJanPPPMMP/rRj3j44YeL0qskSZKk5svAmAerF69o1Lm++tWv8sADD/DGG29svCy1
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
WAAAAABJRU5ErkJggg==
"
>
</div>

</div>

</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">
In&nbsp;[27]:
</div>
<div class="inner_cell">
    <div class="input_area">
<div class="highlight"><pre><span class="n">fullData</span><span class="o">.</span><span class="n">dtypes</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area"><div class="prompt output_prompt">
    Out[27]:</div>


<div class="output_text output_subarea output_pyout">
<pre>
Type                       object
affiliate_channel           int64
affiliate_provider          int64
age                         int64
country_destination        object
date_first_booking          int64
first_affiliate_tracked     int64
first_browser               int64
first_device_type           int64
gender                      int64
id                          int64
language                    int64
signup_app                  int64
signup_flow                 int64
signup_method               int64
booked                      int64
Year                        int64
Month                       int64
dtype: object
</pre>
</div>

</div>

</div>
</div>

</div>
<div class="cell border-box-sizing text_cell rendered">
<div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<h4 id="step-3-data-modelling">Step 3 : Data modelling</h4>
<ul>
<li>Final drop of unnecessary columns </li>
<li>Defining traning and testing sets</li>
<li>Convert &#39;target_col&#39; to numerical values</li>
<li>Drop variables that are not useful for prediction</li>
<li>Select a model and use the model to predict</li>
</ul>
</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">
In&nbsp;[28]:
</div>
<div class="inner_cell">
    <div class="input_area">
<div class="highlight"><pre><span class="c"># Final drop of unnecessary columns</span>
<span class="n">fullData</span> <span class="o">=</span> <span class="n">fullData</span><span class="o">.</span><span class="n">drop</span><span class="p">([</span><span class="s">&#39;booked&#39;</span><span class="p">,</span><span class="s">&#39;id&#39;</span><span class="p">,</span><span class="s">&#39;Year&#39;</span><span class="p">,</span><span class="s">&#39;Month&#39;</span><span class="p">],</span><span class="n">axis</span><span class="o">=</span><span class="mi">1</span><span class="p">)</span>
<span class="n">fullData</span><span class="o">.</span><span class="n">dtypes</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area"><div class="prompt output_prompt">
    Out[28]:</div>


<div class="output_text output_subarea output_pyout">
<pre>
Type                       object
affiliate_channel           int64
affiliate_provider          int64
age                         int64
country_destination        object
date_first_booking          int64
first_affiliate_tracked     int64
first_browser               int64
first_device_type           int64
gender                      int64
language                    int64
signup_app                  int64
signup_flow                 int64
signup_method               int64
dtype: object
</pre>
</div>

</div>

</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">
In&nbsp;[29]:
</div>
<div class="inner_cell">
    <div class="input_area">
<div class="highlight"><pre><span class="c"># Defining traning and testing sets</span>
<span class="n">X_train</span> <span class="o">=</span> <span class="n">fullData</span><span class="o">.</span><span class="n">ix</span><span class="p">[</span><span class="n">fullData</span><span class="o">.</span><span class="n">Type</span> <span class="o">==</span> <span class="s">&#39;Train&#39;</span><span class="p">,</span><span class="s">&#39;Type&#39;</span><span class="p">:]</span>

<span class="n">Y_train</span> <span class="o">=</span> <span class="n">X_train</span><span class="p">[</span><span class="s">&quot;country_destination&quot;</span><span class="p">]</span>
<span class="n">X_train</span> <span class="o">=</span> <span class="n">X_train</span><span class="o">.</span><span class="n">drop</span><span class="p">([</span><span class="s">&quot;Type&quot;</span><span class="p">,</span> <span class="s">&#39;country_destination&#39;</span><span class="p">],</span><span class="n">axis</span><span class="o">=</span><span class="mi">1</span><span class="p">)</span>

<span class="k">print</span><span class="p">(</span><span class="s">&#39;---------&#39;</span><span class="p">)</span>
<span class="n">X_train</span><span class="o">.</span><span class="n">info</span><span class="p">()</span>
<span class="k">print</span><span class="p">(</span><span class="s">&#39;---------&#39;</span><span class="p">)</span>
<span class="n">X_test</span>  <span class="o">=</span> <span class="n">fullData</span><span class="o">.</span><span class="n">ix</span><span class="p">[</span><span class="n">fullData</span><span class="o">.</span><span class="n">Type</span> <span class="o">==</span> <span class="s">&#39;Test&#39;</span><span class="p">,</span><span class="s">&#39;Type&#39;</span><span class="p">:]</span>
<span class="n">X_test</span> <span class="o">=</span> <span class="n">X_test</span><span class="o">.</span><span class="n">drop</span><span class="p">([</span><span class="s">&quot;Type&quot;</span><span class="p">,</span> <span class="s">&#39;country_destination&#39;</span><span class="p">],</span><span class="n">axis</span><span class="o">=</span><span class="mi">1</span><span class="p">)</span>
<span class="n">X_test</span><span class="o">.</span><span class="n">info</span><span class="p">()</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area"><div class="prompt"></div>
<div class="output_subarea output_stream output_stdout output_text">
<pre>
---------
&lt;class &apos;pandas.core.frame.DataFrame&apos;&gt;
Int64Index: 213451 entries, 0 to 213450
Data columns (total 12 columns):
affiliate_channel          213451 non-null int64
affiliate_provider         213451 non-null int64
age                        213451 non-null int64
date_first_booking         213451 non-null int64
first_affiliate_tracked    213451 non-null int64
first_browser              213451 non-null int64
first_device_type          213451 non-null int64
gender                     213451 non-null int64
language                   213451 non-null int64
signup_app                 213451 non-null int64
signup_flow                213451 non-null int64
signup_method              213451 non-null int64
dtypes: int64(12)
memory usage: 21.2 MB
---------
&lt;class &apos;pandas.core.frame.DataFrame&apos;&gt;
Int64Index: 62096 entries, 0 to 62095
Data columns (total 12 columns):
affiliate_channel          62096 non-null int64
affiliate_provider         62096 non-null int64
age                        62096 non-null int64
date_first_booking         62096 non-null int64
first_affiliate_tracked    62096 non-null int64
first_browser              62096 non-null int64
first_device_type          62096 non-null int64
gender                     62096 non-null int64
language                   62096 non-null int64
signup_app                 62096 non-null int64
signup_flow                62096 non-null int64
signup_method              62096 non-null int64
dtypes: int64(12)
memory usage: 6.2 MB

</pre>
</div>
</div>

</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">
In&nbsp;[30]:
</div>
<div class="inner_cell">
    <div class="input_area">
<div class="highlight"><pre><span class="c"># Convert &#39;country_destination&#39; to numerical values</span>
<span class="c"># Get the name list of all countries </span>
<span class="n">range_countries</span> <span class="o">=</span> <span class="n">fullData</span><span class="o">.</span><span class="n">country_destination</span><span class="o">.</span><span class="n">value_counts</span><span class="p">()</span><span class="o">.</span><span class="n">index</span>

<span class="c"># Get the dictionary of the target column</span>
<span class="n">country_num_dic</span> <span class="o">=</span> <span class="nb">dict</span><span class="p">(</span><span class="nb">zip</span><span class="p">(</span><span class="n">range_countries</span><span class="p">,</span><span class="nb">range</span><span class="p">(</span><span class="nb">len</span><span class="p">(</span><span class="n">range_countries</span><span class="p">))))</span>
</pre></div>

</div>
</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">
In&nbsp;[31]:
</div>
<div class="inner_cell">
    <div class="input_area">
<div class="highlight"><pre><span class="k">print</span> <span class="n">country_num_dic</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area"><div class="prompt"></div>
<div class="output_subarea output_stream output_stdout output_text">
<pre>
{&apos;FR&apos;: 3, &apos;NL&apos;: 9, &apos;PT&apos;: 11, &apos;CA&apos;: 7, &apos;DE&apos;: 8, &apos;IT&apos;: 4, &apos;US&apos;: 1, &apos;NDF&apos;: 0, &apos;other&apos;: 2, &apos;AU&apos;: 10, &apos;GB&apos;: 5, &apos;ES&apos;: 6}

</pre>
</div>
</div>

</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">
In&nbsp;[32]:
</div>
<div class="inner_cell">
    <div class="input_area">
<div class="highlight"><pre><span class="c"># Create training labels</span>
<span class="n">Y_train</span>    <span class="o">=</span> <span class="n">train</span><span class="p">[</span><span class="s">&#39;country_destination&#39;</span><span class="p">]</span><span class="o">.</span><span class="n">map</span><span class="p">(</span><span class="n">country_num_dic</span><span class="p">)</span>
</pre></div>

</div>
</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">
In&nbsp;[34]:
</div>
<div class="inner_cell">
    <div class="input_area">
<div class="highlight"><pre><span class="c"># Select the model &#39;Random Forests&#39;</span>
<span class="n">random_forest</span> <span class="o">=</span> <span class="n">RandomForestClassifier</span><span class="p">(</span><span class="n">n_estimators</span><span class="o">=</span><span class="mi">100</span><span class="p">)</span>
<span class="n">random_forest</span><span class="o">.</span><span class="n">fit</span><span class="p">(</span><span class="n">X_train</span><span class="p">,</span> <span class="n">Y_train</span><span class="p">)</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area"><div class="prompt output_prompt">
    Out[34]:</div>


<div class="output_text output_subarea output_pyout">
<pre>
RandomForestClassifier(bootstrap=True, class_weight=None, criterion=&apos;gini&apos;,
            max_depth=None, max_features=&apos;auto&apos;, max_leaf_nodes=None,
            min_samples_leaf=1, min_samples_split=2,
            min_weight_fraction_leaf=0.0, n_estimators=100, n_jobs=1,
            oob_score=False, random_state=None, verbose=0,
            warm_start=False)
</pre>
</div>

</div>

</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">
In&nbsp;[35]:
</div>
<div class="inner_cell">
    <div class="input_area">
<div class="highlight"><pre><span class="c"># Use &#39;Random Forest&#39; model to predict on the training set</span>
<span class="n">Y_pred</span> <span class="o">=</span> <span class="n">random_forest</span><span class="o">.</span><span class="n">predict</span><span class="p">(</span><span class="n">X_test</span><span class="p">)</span>

<span class="n">random_forest</span><span class="o">.</span><span class="n">score</span><span class="p">(</span><span class="n">X_train</span><span class="p">,</span> <span class="n">Y_train</span><span class="p">)</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area"><div class="prompt output_prompt">
    Out[35]:</div>


<div class="output_text output_subarea output_pyout">
<pre>
0.9965284772617603
</pre>
</div>

</div>

</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">
In&nbsp;[36]:
</div>
<div class="inner_cell">
    <div class="input_area">
<div class="highlight"><pre><span class="c"># Use &#39;Random Forest&#39; model to predict on the testing set</span>
<span class="n">random_forest</span><span class="o">.</span><span class="n">score</span><span class="p">(</span><span class="n">X_test</span><span class="p">,</span> <span class="n">Y_pred</span><span class="p">)</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area"><div class="prompt output_prompt">
    Out[36]:</div>


<div class="output_text output_subarea output_pyout">
<pre>
1.0
</pre>
</div>

</div>

</div>
</div>

</div>
    </div>
  </div>

 


 

