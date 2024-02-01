# Provenance Notation

PROV-N adopts a functional-style syntax consisting of a predicate name and an ordered list of terms. All PROV data model types have an identifier. All PROV data model relations involve two primary elements, the subject and the object, in this order. 

The grammar is specified using a subset of the Extended Backus-Naur Form (EBNF) notation, as defined in Extensible Markup Language (XML). 

EBNF specifies a series of production rules (production). A production rule in the grammar defines a symbol *expr* (nonterminal symbol) using the following form: 

> expr ::= term

Symbols are written with an initial capital letter if they are the start symbol of a regular language, otherwise with an initial lowercase letter. A production rule in the grammar defines a symbol <TERMINAL> (terminal symbol) using the following form:

> <TERMINAL> ::= term

Almost all expressions defined in the grammar include an identifier. Most expressions can also include a set of attribute-value pairs, delimited by square brackets. Identifiers are optional except for Entities, Activities, and Agents. Identifiers are always the first term in any expression. 

+ Communication

+ Invalidation

+ Derivation / Revision  / Quotation

