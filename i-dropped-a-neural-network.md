---
description: https://huggingface.co/spaces/jane-street/droppedaneuralnet
---

# I Dropped a Neural Network

### Problem Description:

Calm luh problem from Jane Street. The premise is we have a Linear NN that looks like:&#x20;

```
class Block(nn.Module):
    def __init__(self, in_dim: int, hidden_dim: int):
        super().__init__()
        self.inp = nn.Linear(in_dim, hidden_dim)
        self.activation = nn.ReLU()
        self.out = nn.Linear(hidden_dim, in_dim)

    def forward(self, x):
        residual = x
        x = self.inp(x)
        x = self.activation(x)
        x = self.out(x)
        return residual + x

class LastLayer(nn.Module):
    def __init__(self, in_dim: int, out_dim: int):
        super().__init__()
        self.layer = nn.Linear(in_dim, out_dim)

    def forward(self, x):
        return self.layer(x)
```

We're given a directory with 97 pytorch "pieces" and historical data that contains datapoints w/ predictions for each. The pieces represent the weight and bias values after training on the data points in the historical data. The problem is that we do not know the order of the pieces. That is, we have 48 blocks of linear layers corresponding to two of the peices, but don't know which two pieces go together to find a block, or which order the blocks are arranges in the NN. Our job is to return the order of the pieces that leads to the results in the historical data (same prediction values on the data given).

### Solution

There's a rather elegant solution that allows us to not have to naively brute force or do a sort of hill climbing algorithm on the data directly. Even if we could find pairings, there are still 48 blocks to order, so 48! different permutations — this is too many! The approach comes from the realization that there is an implicit structure of residual networks that leads to a distinct pattern in the weights of a given block.&#x20;

In a deep resnet, we find that after training, each block forms a transformation close to the identity matrix; the sequence of blocks represents a sequence of small near-identity perturbations. This leads to structured blocks with strong diagonals.

Using this, we can break the problem into 2 steps:

1. Find block pairings of diagonally dominant matrices
2. Order the blocks found in step 1

**Step 1:**

To pair the pieces into blocks, we can do a pairwise comparison and calculate:&#x20;

$$
d(i, j) = \frac{\left| \operatorname{tr}\left(W_{\text{out}}^{(j)} W_{\text{in}}^{(i)} \right) \right|}{\left\| W_{\text{out}}^{(j)} W_{\text{in}}^{(i)} \right\|_F}
$$

We can then group the pairs greedily by pairing the weights the yield the highest $$d(i, j)$$.

Some experimentation shows that weights with the correct pairing results in much higher values than the incorrect pairings: $$d \in [1.76, 3.28]$$ vs $$d \in [0, 0.58]$$, respectively.

**Step 2:**

Now that we have the blocks of weight pairs, we need to order the blocks. To do this, we'll try different permutations, run the data through the res net, and then compare the MSE between our output and the prediction value in the historical data. We want to find convergence to 0 MSE, which represents the perfect reordering of the NN.&#x20;

Rather than brute forcing the order, we can do the ordering more intelligently by first finding a seed order, and then using a greedy hill climbing algorithm:&#x20;

1. Order the blocks by the Frobenius norm:
   1. $$\left| W_{\text{out}} , \mathrm{ReLU}!\left(W_{\text{in}} x + b_{\text{in}}\right) + b_{\text{out}} \right|_2$$
   2. Without ordering, this already leads to an initial MSE = 0.052399
2. Use a greedy hill climbing algorithm until convergence to MSE = 0
   1. Iterate through the blocks from index 0 to 47
   2. At each index, if swapping the block with it's i-1 th neighbor leads to a better MSE, perform the swap
   3. At the end of the interation, if MSE > 0, go back to the first block and repeat
   4. Continue until MSE = 0 (or there is no swaps, this should be equivalent if we arranged the pieces correctly)

In practice, this converges rather quickly:&#x20;

```
Initial MSE: 0.052399
  sweep   1  swaps=28  MSE=0.02696270
  sweep   2  swaps=22  MSE=0.01204974
  sweep   3  swaps=13  MSE=0.00817669
  sweep   4  swaps=10  MSE=0.00586302
  sweep   5  swaps=10  MSE=0.00405286
  sweep   6  swaps=9  MSE=0.00241334
  sweep   7  swaps=6  MSE=0.00099826
  sweep   8  swaps=3  MSE=0.00042281
  sweep   9  swaps=1  MSE=0.00033697
  sweep  10  swaps=1  MSE=0.00024728
  sweep  11  swaps=1  MSE=0.00018225
  sweep  12  swaps=1  MSE=0.00011796
  sweep  13  swaps=1  MSE=0.00005237
  sweep  14  swaps=1  MSE=0.00000000
  sweep  15  swaps=0  MSE=0.00000000

Final MSE:         0.00000000
Correlation w/ pred: 1.000000
```

We've now done it! MSE of our output from the NN we arranged and the prediction values in the historical data should be 0!
