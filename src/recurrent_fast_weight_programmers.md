# Recurrent Fast Weight Programmers

> [Paper](https://proceedings.neurips.cc/paper_files/paper/2021/hash/3f9e3767ef3b10a0de4c256d7ef9805d-Abstract.html) | [Code](https://github.com/IDSIA/recurrent-fwp)

## Introduction

With linear transformers, we can prove FWP are effective and fast. 
In this case both slow and fast networks are Feed Forward Networks, and consist of the same layer. 

What if we add recurrence to slow and fast networks?

## Delta RNN

Use RNN for fast weights. 

Add recurrent term to feedforward of linear transformer. 

\\( y^{(t)} = W^{(t)}q^{(t)} + R^{(t)}f(y^{(t-1)}) \\)

where \\( R^{(t)} \\) is the recurrent matrix with additional fast weights, and 
\\( f(y^{(t-1)}) \\) is the output of fast net at previous time step + softmax activation function. 

## Recurrent Delta RNN

Make also slow network recurrent via the fast network, taking fast network previous output as input.

\\( k^t = W_kx^t + R_k f(y^{t-1}) \\)
\\( v^t = W_vx^t + R_v f(y^{t-1}) \\)
\\( q^t = W_qx^t + R_q f(y^{t-1}) \\)

where \\( R_k, R_v, R_q \\) are the recurrent matrices for the slow network (slow weights), and each equation corresponds to query, key and value pairs calculations for attention of the slow network.

## Problems

The network causes additional complexity with regards to linear transformers, but it is still linear (same order of complexity).

