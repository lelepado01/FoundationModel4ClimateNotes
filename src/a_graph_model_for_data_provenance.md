# A Graph Model of Data Provenance

## Introduction

Provenance in databases has been defined for relational or complex object data, by propagating fine-grained annotations from the input to the output. 
Workflow in provenance aims to capture the complete description of evaluation of a process, which is crucial in verification of a scientific computation. 
Workflows and their provenance are often represented as directed acyclic graphs, but complicating the semantic that relates to the workflow of provenance and their runtime behaviour. This part is often achieved with extended data-flow languages.

The open provenance model has been developed as an exchange format for representing provenance graphs. 

A common language to express both databases queries and workflows is necessary. In this case Dataflows (DFL) was used.

In this work, a semantic that evaluates dataflow calculation expressions to provenance graphs containing values, evaluation nodes and links showing how the expression is evaluated is presented; as well as a precise implementation of this model. 

## Dataflow Language

DFL is a language for expressing dataflow computations, and it is a generalization of the relational algebra.
It is an extension of the NRC dataflow language, that only includes atomic values and functions. 

Both DFL and NRC are statically typed languages. 

## Value, Evaluation and provenance graphs

DFL expressions are normally evaluated over complex values, which are nested as a combination of atomic data values **d**, tuples of complex values \\( < A_1 : v_1, \dots , A_n : v_n > \\), and sets of complex values \\( \{ v_1, \dots , v_n \} \\). Complex values can be easily represented as trees or DAGs. 

Using *value graphs* we represent the evaluation of a DFL expression, and using *provenance graphs*, which are two-sorted graphs consisting of a value graph and an evaluation graph, we represent the evaluation of a program.

## Value Graphs

A value graph is a DAG, with labels on the nodes and edges. The nodes are labeled with alphabet \\( {{}, <>, \\text{copy}}\\), while the edges are labeled with the names of the attributes of the complex value. 
The formula \\( lab_l(n) \\) is used to indicate that the label of node \\( n \\) is \\( l \\) in the graph \\( G \\).

A tree shaped value graph is called a *value tree*, and one can always represent any complex values by the root node of a value tree.

## Evaluation Graphs

An *evaluation graph* \\( G = (V, E) \\) is a labelled directed acyclic graph, with nodes and labeles drawn from the set

\\( {x, c, f, <>, \pi_A, let_x, if, for_x, \dots} \\)

and optional edge labels drawn from the set: 

\\( {A, head, body, test, then, else, 1, 2, \dots} \\)

A valid evaluation graph is a graph constructed using specific rules (see paper), and can be extended by attaching new nodes and edges or by linking existing nodes. 

## Provenance Graphs

A *provenance graph* \\( G = (V, E) \\) is a DAG containing nodes and edges, with either a value or an evaluation label. It indicates the evaluation of a DFL expression, and is a two-sorted graph consisting of a value graph and an evaluation graph.

Given a provenance graph G and an evaluation node *e*, there is a notion \\((G, e) \\) of the node being locally consistant, with the intuition that the computation depicted in the part of the evaluation graph reachable from *e* matches the assignemnt of value nodes to evaluation nodes by the val-edges. 

It is possible to enforce local consistency by using first order constraint on a *provenance graph*. Global consistency can also be defined by induction on the structure of an expression. 

## Provenance Graph Semantics

To construct a consistent provenance graph we need to evaluate DFL expressions to construct both value and evaluation graphs. 

(See rules in paper)

The rules can be applied to build a provenance graph *bottom-up*. 

Given an ordinary assigment, we can always construct a graph G that defines value nodes for the values the variable and whose evaluation nodes correspond exactly to the values in X. 

## Querying Provenance Graphs

The provenance graph is a relational structure and as such it can be queried from simple paths to complex queries. 

It still seems to be a challenge to define known forms of provenance in databases in terms of provenance graphs. In this work, Datalog is used to define the semantics of provenance graphs.

## When and Why Provenance

In order to define forms of where and why provenance, we need to define a partial order on evaluation nodes. 
Where and Why provenance will be defined on tuples \\( (e, v) \\) such that *v* is reachable from *e* by a directed path. These pairs will be called instances. 

The **where-provenance** can be defined as follows: 

\\( Where((e_1, v_1), (e_2, v_2)) \leftarrow Before(e_1, e_2), Copy(v_2, v_1) \\)

meaning that the provenance of v_2 returned by the evaluation ending at e_2 is the same as that of value v_1 returned by the evaluation ending at e_1. 
There should be a unique (e_1, v_1) with respect to *Before*, so we can define the where-provenance as the instance (e_1, v_1).

The **why-provenance** on the other hand is defined using witnesses. The witness to the existence of a part *p* of the output of a query on input data *d* is a subtree of the input *d* such that re-running Q on the subtree still produces a as output the part *p*. 
Let *G* be the provenance graph with a distinguished evaluation node *r* and a value node *v*, let *U* be a connected subset of the result value node that contains *v*. Then a witness to *U* in *G* is a consistent subgraph of G that contains *U* and *r*. 

The Why-provenance of *V* is then the set of all minimal witnesses to *U* in *G*.
