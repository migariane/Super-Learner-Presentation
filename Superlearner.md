# An Introduction to SuperLearner, a loss-based ensemble prediction algorithm
Scott Grey, PhD  
April 14, 2016  

## Overview

1. Background on the development of super learner and targeted learning
2. Theory behind the super learner algorithm
3. Application of super learner in R
4. Some (hopefully) helpful comments on utilizing super learner

## Background
<div class="centered">
"Essentially, all models are wrong, but some are useful"  
- George Box, 1979

</div>

Mantra of statisticians regarding the development of statistical models for many years  

In the 1990s an awareness developed among statisticians (Breiman, Harrell) that this approach was wrong  

- Parametric model assumptions rarely met
- Large number of variables makes it difficult to correctly specify a model  

Simultaneously, computer scientists and some statisticians developed the machine learning field to address the limitations of parametric models

## Targeted learning

Combines advanced machine learning with efficient semiparametric estimation to provide a framework for answering causal questions from data  

- Developed by Mark van der Laan research group at UC Berkeley
- Started with the seminal 2006 article on targeted maximum likelihood estimation  

Central motivation is the belief that statisticians treat estimation as *Art* not **Science**  

- This results in misspecified parametric models that are data-adaptively selected, but this part of the estimation procedure is not accounted for in the variance

## Estimation is a Science, *Not an Art* | Specific definitions required

1. **Data:** realizations of random variables with a probability distribution
2. **Model:** actual knowledge about the data generating probability distribution
3. **Target Parameter:** a feature of the data generating probability distribution
4. **Estimator:** an a priori-specified algorithm, benchmarked by a dissimilarity-measure (e.g., MSE) w.r.t. target parameter

## Data 

Random variable $O$, observed $n$ times, defined in a simple case as <math xmlns='http://www.w3.org/1998/Math/MathML'>
 <mrow>
  <mi>O</mi><mo>=</mo><mrow><mo>(</mo>
   <mrow>
    <mi>A</mi><mo>,</mo><mi>W</mi><mo>,</mo><mi>Y</mi></mrow>
  <mo>)</mo></mrow><mo>&#x223C;</mo><msub>
   <mi>P</mi>
   <mi>0</mi>
  </msub>
  </mrow>
</math>
 if we are without common issues such as missingness and censoring  

- $A$: exposure or treatment 
- $W$: vector of covariates
- $Y$: outcome 
- <math xmlns='http://www.w3.org/1998/Math/MathML'>
 <msub>
  <mi>P</mi>
  <mi>0</mi>
 </msub>
 </math>: the true probability distribution

This data structure makes for an effective examples but data structures found in practice are much more complicated

## Model

General case: Observe $n$ i.i.d. copies of random variable $O$ with probability distribution <math xmlns='http://www.w3.org/1998/Math/MathML'>
 <msub>
  <mi>P</mi>
  <mi>0</mi>
 </msub>
</math>


The data-generating distribution <math xmlns='http://www.w3.org/1998/Math/MathML'>
 <msub>
  <mi>P</mi>
  <mi>0</mi>
 </msub>
 </math> is also known to be an element of a statistical model <math xmlns='http://www.w3.org/1998/Math/MathML'>
 <mi>M</mi><mo>:</mo><msub>
  <mi>P</mi>
  <mn>0</mn>
 </msub>
 <mo>&#x2208;</mo><mi>M</mi>
</math>


A **statistical** model $M$ is the set of possible probability distributions for <math xmlns='http://www.w3.org/1998/Math/MathML'>
 <msub>
  <mi>P</mi>
  <mi>0</mi>
 </msub>
 </math>; it is a collection of probability distributions

If all we know is that we have $n$ i.i.d. copies of $O$, this can be our statistical model, which we call a non-parametric statistical model

## Target Parameters 
Define the parameter of the probability distribution $P$ as function of <math xmlns='http://www.w3.org/1998/Math/MathML'>
 <mi>P</mi><mo>:</mo><mi>&#x03C8;</mi><mrow><mo>(</mo>
  <mi>P</mi>
 <mo>)</mo></mrow>
</math>

In causal inference (specificly the Neyman-Rubin) framework, a target parameter for $A$ would be  
<math display='block' xmlns='http://www.w3.org/1998/Math/MathML'>
 <msub>
  <mi>&#x03C8;</mi>
  <mrow>
   <mi>R</mi><mi>D</mi></mrow>
 </msub>
 <mrow><mo>(</mo>
  <mi>P</mi>
 <mo>)</mo></mrow><mo>=</mo><msub>
  <mi>E</mi>
  <mi>W</mi>
 </msub>
 <mrow><mo>[</mo> <mrow>
  <mrow><mo>(</mo>
   <mrow>
    <mi>Y</mi><mo>&#x007C;</mo><mi>A</mi><mo>=</mo><mn>1</mn><mo>,</mo><mi>W</mi></mrow>
  <mo>)</mo></mrow></mrow> <mo>]</mo></mrow><mo>&#x2212;</mo><msub>
  <mi>E</mi>
  <mi>W</mi>
 </msub>
 <mrow><mo>[</mo> <mrow>
  <mrow><mo>(</mo>
   <mrow>
    <mi>Y</mi><mo>&#x007C;</mo><mi>A</mi><mo>=</mo><mn>0</mn><mo>,</mo><mi>W</mi></mrow>
  <mo>)</mo></mrow></mrow> <mo>]</mo></mrow>
</math>


## Slide with R Code and Output




## Slide with Plot

![](Superlearner_files/figure-html/unnamed-chunk-1-1.png)
