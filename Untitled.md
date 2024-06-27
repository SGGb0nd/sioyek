Certainly! Here's the explanation using LaTeX-style dollar signs for inline equations and double dollar signs for displayed equations.

### Correct Formulation

When we have the observed effect sizes $\hat{\beta}$ from GWAS, the relationship is given by:

\[ \hat{\beta} = R \beta + X^\top \epsilon \]

Here:

-  $\hat{\beta}$ is the vector of observed SNP effect sizes.
-  $R$ is the LD matrix of the SNPs.
-  $\beta$ is the vector of true SNP effect sizes.
-  $X$ is the standardized genotype matrix (each column corresponding to a SNP's genotypes standardized to mean 0 and variance 1).
-  $\epsilon$ is the error term, often related to the residuals from the phenotype model.

The error term $X^\top \epsilon$ more accurately reflects the residual noise term, rescaled by the genotype matrix, and now we need to understand how this translates to the expectation of the squared effect size.

### Variance Decomposition

Given the formulation:

\[ \hat{\beta} = R \beta + X^\top \epsilon \]

### Expected Squared Effect Size

1. **Observed Variance**: The variance of the observed effect size $\hat{\beta}_k$:

\[ \text{Var}(\hat{\beta}_k) = \text{Var}\left( \sum_j R_{kj} \beta_j + X_k^\top \epsilon \right) \]

2. **Error Term Contribution**: Because the error term contributes noise, we should consider its variance contribution separately:
   
   - The variance of $X_k^\top \epsilon$ depends on the genotype marker $X_k$ and the residual variance of $\epsilon$:
   
   \[ \text{Var}(X_k^\top \epsilon) = \sigma_e^2 (1 - R_{kk}) \]

   Assuming $\epsilon$ is independent and identically distributed with variance $\sigma_e^2$, where $1 - R_{kk}$ represents the portion not explained by LD.

3. **Genetic Contribution**: The true genetic effect size variance component is related to the LD-adjusted variance of $\beta$:

\[ \text{Var}\left(\sum_j R_{kj} \beta_j\right) = \sum_j R_{kj}^2 \text{Var}(\beta_j) = \sigma_\beta^2 R_{kk} \]

4. **Combining Contributions**: Combining both contributions (genetic and error), we get:

\[ \text{Var}(\hat{\beta}_k) = \sigma_\beta^2 R_{kk} + \sigma_e^2 (1 - R_{kk}) \]

### Expectation of Squared Effect Size $\mathbb{E}(\hat{\beta}_k^2)$:
Since $\hat{\beta}_k$ is unbiased:

\[ \mathbb{E}(\hat{\beta}_k) = 0 \]

Thus, the expectation of the squared effect sizes, given the variance components, can be expressed as:

\[ \mathbb{E}(\hat{\beta}_k^2) = \text{Var}(\hat{\beta}_k) = \sigma_\beta^2 R_{kk} + \sigma_e^2 (1 - R_{kk}) \]

### Why \( R_{S_i} \) in \(\sigma_e^2\) Disappears:

#### Simplified Term Explanation:
1. **Definition and Components**:
   - $\hat{\beta}_k$ represents the observed marginal effect size of a particular SNP $k$.
   - For SNP $k$, the expectation $\mathbb{E}(\hat{\beta}_k^2)$ integrates contributions from genetically correlated SNPs (captured by $R$) and the residual variance.

2. **Independence and Linear Combination**:
   - The property of variance for independent random variables states that the variance of a sum of independent random variables is the sum of the variances.
   - Since $\epsilon$ is the noise term assumed independent of $\beta$, the variance introduced by $\epsilon$ adds directly as a scalar term without needing to be adjusted by $R$.

3. **Variance Only Affected by $R$ in Genetic Term**:
   - The term $\text{Var}(R \beta)$ is affected by $R$ because it adjusts the covariance structure among SNPs due to LD. This term captures how true genetic effect sizes ($\beta$) are correlated—hence involving $R$.
   - However, the residual variance $\text{Var}(\epsilon)$, represented as $\sigma^2 I$, is independent of the LD structure. Therefore:
     \[ \text{Var}(\epsilon) = \sigma^2 I \]
     This term remains unaffected by $R$ because $\epsilon$ is uncorrelated with the genetic structure ($\beta$).

4. **Summarizing Effects**:
   - **Total Variance**: When considering the total variance of $\hat{\beta}$, it acknowledges both the genetic variance modulated by $R$ and the residual variance:
     \[ \text{Var}(\hat{\beta}) = R \text{Var}(\beta) R^T + \sigma^2 I \]
   - **Expected Squared Effect**: Consequently, the expected squared effect size $\mathbb{E}(\hat{\beta}_k^2)$ encapsulates:
     - The genetic effect component adjusted by $R$: $\sigma^2_\beta R_{ii}$.
     - The residual component $\sigma^2$, which is not dependent on $R$.

#### Result:
Therefore, the term $\sigma_{e}^2$ (or $\sigma^2$ for the residual variance) does not include $R$ because this variance component is purely a function of the noise in the GWAS estimation process, which is assumed to be independent of the LD structure represented by $R$. Thus, $R$ disappears in the term $\sigma_{e}^2$ when calculating the expected squared effect sizes.

### Conclusion:

Thus, the expectation of $\hat{\beta}_k^2$ includes contributions from both the genetic effects and the noise. The LD matrix $R$ influences the genetic component directly but does not appear explicitly in the residual variance term because this captures all remaining noise not explained by the LD structure. This results in the expectation of the squared effect size being a simple addition of these two components.