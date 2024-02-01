# Provenance Constraints

PROV statements involve identifiers, literals, placeholders, and attribute lists. **Identifiers** are, according to PROV-N, expressed as qualified names which can be mapped to URIs. However, in order to specify constraints over PROV instances, we also need **variables** that represent unknown identifiers, literals, or placeholders. These variables are similar to those in first-order logic. A variable is a symbol that can be replaced by other symbols, including either other variables or constant identifiers, literals, or placeholders.

Several definitions and inferences conclude by saying that some objects exist such that some other formulas hold. Such an inference introduces fresh existential variables into the instance. An **existential variable** denotes a fixed object that exists, but its exact identity is unknown. Existential variables can stand for unknown identifiers or literal values only; we do not allow existential variables that stand for unknown attribute lists.

Some placeholders indicate the absence of an object, rather than an unknown object. In other words, the placeholder is overloaded, with different meanings in different places.

An expression is called a **term** if it is either a constant identifier, literal, placeholder, or variable. 

### Substitution

A substitution is a function that maps variables to terms. Concretely, since we only need to consider substitutions of finite sets of variables, we can write substitutions as: 

\\([x_1 = t_1,...,x_n = t_n] \\)

can be applied to a term by replacing occurrences of \\(x_i \text{with} t_i\\).

### Formulas

For the purpose of constraint checking, we view PROV statements as formulas. 

An **instance** is analogous to a "theory" in logic, that is, a set of formulas all thought to describe the same situation. The set can also be thought of a single, large formula: the conjunction of all of the atomic formulas.

The definitions, inferences, and constraint rules in this specification can also be viewed as logical formulas, built up out of atomic formulas, logical connectives and quantifiers. 

In logic, a formula's meaning is defined by saying when it is satisfied. We can view definitions, inferences, and constraints as being satisfied or not satisfied in a PROV instance, augmented with information about the constraints. 

Unification is an operation that takes two terms and compares them to determine whether they can be made equal by substituting an existential variable with another term. 

