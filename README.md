Sparse RL with DAPD + SAC

Reimplementation of DAPD (Data Adaptive Pathway Discovery), a gradient-saliency pruning method, applied to a Soft Actor-Critic agent and tested on three MuJoCo continuous-control tasks: HalfCheetah-v4, Hopper-v4, Ant-v4.

---Idea---
Instead of training a dense network, periodically score each weight by how much the loss depends on it (|weight × gradient|), keep only the top-k% most important weights, and zero out the rest via a binary mask — then keep training the sparse network. Tested at 90%, 95%, and 98% sparsity to see how much of the network can be pruned before performance degrades.

---Features---
SAC agent (actor, double-Q critic, target network, Polyak averaging) from scratch.
MaskedLinear layer that applies a binary pruning mask in the forward pass.
DAPDController that computes saliency scores and updates the mask during a warmup phase, then freezes it for the rest of training.

---Results---
Actor loss decreases smoothly and critic loss stabilizes once the pruning mask is frozen (see plots/). Add 1-2 sentences on how sparsity level affected final return once you've compared 0.90 vs 0.95 vs 0.98.
