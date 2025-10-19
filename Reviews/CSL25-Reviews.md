SUBMISSION: 65
##TITLE: Cyclic System T with Lambda Binder

###----------------------- REVIEW 1 ---------------------

SUBMISSION: 65
TITLE: Cyclic System T with Lambda Binder
AUTHORS: Stefano Berardi, Daisuke Kimura, Makoto Tatsuta, Ugo De'Liguoro and Koji Nazakawa

----------- Overall evaluation -----------

SCORE: -1 (weak reject)

----- TEXT:

####Context

The infinitary lambda calculus has been originally defined as a metric completion of the regular set of lambda-terms. This calculus is proved to be strongly normalizable, provided that one considers infinite reductions of arbitrary ordinal length, that are moreover "strongly convergent". Intuitively, this means that-when approaching a limit-the depth of the contracted redexes must tend to infinity. More recently, the infinitary lambda calculus has been redefined coinductively. The equivalence between the two systems relies on a Compression Lemma, stating that any reduction M ->>> N of length gamma (an ordinal) can be transformed into a countable reduction from M to N. Non-wellfounded proofs, and in particular cyclic proofs, have become a growing area of interest in computer science because they provide a powerful alternative to traditional inductive and coinductive proof techniques. Instead of requiring explicit induction principles, they encode inductive reasoning through gl
obal conditions that ensure cycles in the proof correspond to valid inductive arguments. This approach is helpful to improve our understanding of the foundations of proof theory, especially in relation to fixed-point logics and sequent calculi.

####Contents

The present paper builds on recent work by Das, who studied a variant of Gödel’s system T, denoted CT, in which programs are circularly typed rather than relying on an explicit recursion combinator. Whereas Das considers terms of CT constructed from combinators, this paper instead examines a language generating potentially infinite lambda-terms, with particular attention to the regular ones. Here, regular means that a term has only finitely many distinct subterms. The first contribution of this paper is to show that Brotherston and Simpson’s Global Trace Condition can be adapted to this setting, and that every well-typed regular term satisfying this condition enjoys a termination property. Informally, the Global Trace Condition requires that all infinite branches contain a trace of some argument N that passes infinitely many times through the right-hand side of a conditional. In my understanding, this idea is analogous to productivity in coinductive rewriting systems and
 to strong convergence in infinitary lambda-calculus.
A second contribution of the paper is a proof that all infinite reductions in this restricted system converge to a limit, together with a characterization of that limit. These results, which were previously established only for the combinatory version of CT, are here extended to the lambda-calculus version with explicit binders.

####Evaluation

The topic of the paper is clearly within the scope of the conference, and its results can be of interest to the scientific community. That said, I have several concerns regarding the mathematical formalization of the lambda-calculus component of the system, in particular the treatment of the lambda-binder. The handling of alpha-conversion deviates from standard approaches in the literature and does not appear mathematically sound (see my discussion below). Nevertheless, the underlying idea is clear, and I believe the definition can be adjusted to address this issue. 
The presentation of the type system also raises questions. The lambda-terms are explicitly typed, yet a redundant context is introduced  (as far as I understand) merely to ensure that there are finitely many free variables. About the uniqueness of the types inhabiting a term, it should be remarked that it follows from the type-annotations on the variables. I am also concerned with the rewriting system presented in the paper. While one-step reduction is well defined, the definition of infinite reductions is left unclear. Presumably, they are intended to be infinite sequences of terms M_n such that M_i -> M_{i+1}, but this is never made explicit. Since the paper studies termination in this context, these notions should be formally defined and carefully discussed.
In addition, the definitions of stationary and non-stationary connections in Section 3 are very difficult to follow. The few lines of informal explanation preceding Definition 22 are not sufficient to help the non expert reader. I would strongly recommend providing more intuition before the formal definitions, and introducing them with the help of an appropriate graphical formalism.

Finally, beyond issues of presentation, I remain uncertain whether the results offer a sufficiently strong improvement over the analogous results already established for the combinatory system. 

####Problem with alpha conversion

I am worried about Definition 6 (alpha-conversion). While I understand the intuitive meaning of the operation that the authors are describing, I cannot convince myself of the correctness of its formalization.  First, I don't think that phi is defined on variables, rather on variables occurrences. Otherwise, it would be impossible to alpha-rename (\x.xx)(\x.xx) to, say, (\x.xx)(\y.yy) because all the occurrences of x would be uniformly renamed into y. Similarly for the example given in the paper before Definition 7, f = \x.cond(x,f0) cannot be renamed into f = \x.cond(x,f = \y.cond(y,f0)0) without speaking of variable occurrences. 
Something that it is not clear is whether the authors want the property "t ~alpha u" implies "u ~alpha t". With the current definition, it is unclear why an injection t -> u should give rise to an injection in the other direction. If the authors do not expect this property, then they should clearly state it and not call this operation a "conversion", since it is misleading. 

Proposed correction: define alpha-renaming properly for infinitary terms u, v and then restrict alpha conversions in such a way that "if u ~alpha v holds, then u is Reg iff v is Reg". 

####Minor issues

find &. replace : indexes -> indices

48 binder lambda -> is this CT-lambda?
62 n-safe reductions. It is unclear what "n" is at this point
93. "we say that u is an immediate subterm if u is an immediate subtree" You should also define " proper subterms of t" because they are not just subterms different from t. 
102. Num is the set of numerals. -> We denote by Num the set of numerals.
131 "by induction on the definition of ~alpha."  Your definition of ~alpha is not inductive (nor coinductive for that matter). My impression is that your regular terms can all be coinductively generated by a finite grammar, and that you are doing a coinduction over that grammar.
Definition 7)3. You remark that the type context is redundant, you should explain why it is needed. Namely, to impose that all variable occurrences are typed with the same type.
footnote 1. they can used -> they can be used
Definition 8. These rules would be more readable if depicted in the usual tree-like form "premises/conclusion"
169. A more generic name like "structural" might be more appropriate, if you group weakening and exchange together. 
210 "a node x in T" Previously x was reserved for variables, not nodes.
Caption of Figure 1. Explain here what the arrows stand for, rather than in the foonote.
264 there is unique -> there is a unique
274. two kind of -> two kinds of 
278 indexes -> indices
"all reduction strategies ... strongly normalize" That is not well-written. A single reduction strategy normalizes the term t, a term is strongly normalizable if every possible reduction sequence starting from t eventually terminates.
413 in the the -> in the
420 was well-typed -> is well-typed
figure 2 caption. recall here the definition of r.
494 has an exactly one type -> has exactly one type 
635 godel -> Godel


###----------------------- REVIEW 2 ---------------------

----------- Overall evaluation -----------

SCORE: 1 (weak accept)

----- TEXT:

This paper introduces a novel sufficient termination condition for terms in
infinitary lambda calculus with conditional on zero. To that end, it builds
on existing work in infintary lambda-calculus and non-wellfounded proof theory
by lifting the so-called global trace condition (GTC) to the full syntax of
infintary lambda-terms including binders. Previously, this was only available
for infinitary combinator terms with variables. The presented result seems to
be a major step towards the goal of representing Gödel's System T in a framework
where recursion is explicitely unfolded to possibly infinite terms.

The paper is well-structured and contains interesting examples. All major
definitions and results are appropriately motivated and illustrated. Detailed proofs
of the the results as well as additional examples can be found in the extensive
appendix. To the best of my knowledge, this is a solid contribution to the
field of infinitary lambda calculus, so I lean towards acceptance. For non-experts,
the final presentation of the paper could be greatly improved by

(i) stating the connection to previously defined versions of GTC
(ii) motivating the use of the presented system instead of using
     Gödel's System T directly

Detailed Comments:

- p5, Proposition 9:
The statement about the list of immediate subterms is not true for the ap_v rule.
My suggestion is to slightly modify the statement it as follows:
if the premises of r are some \Gamma_1 |- t_1 : A_1, ... , x^A \in FV(\Gamma)

- p6, Figure 1:
The blue arrow in ap_v should go to the type on the right of |- and then continue
upwards; in particular the current blue arrow in the application of weak does
not follow your definition. I would also annotate the leftmost rule application
with "var" for completeness.

- p6, Example 14:
I think it would be helpful to state that all leftmost paths (ending in the
application of var on the left).

- p8, paragraph starting at l288:
Here, you use "sequent" instead of "judgement", please stick to "judgement".
Moreover, I would call "k" an "argument index" instead of an "argument".
In general, I think it would improve the clarity of the text if you
formally defined "argument" as either "unnamed argument" or "named argument".
Finally, \theta' is technically not a premise of \theta but a child node
of \theta which is labeled by a premise of the rule label of \theta.

- p8ff, Definitions 20+21:
According to your definitions, the notation x_i^{A_i} in typing contexts
should be written as x_i : A_i. Moreover, I think it would be helpful
to already explain the meaning of the color blue for arrows before
Def. 20.

- p10, Definition 22:
It is not clear to me how a trace is defined. From looking at the proofs
and thinking about the size-change principle, I think the definition
should read ((k_m,\theta_m),(k_{m+1},\theta_{m+1}),...),
i.e., dom(\tau) = m,m+1,...
Please clarify this and give an explicit definition of dom(.).

- p10, l382:
Whereas you cite sources which contain the term "general trace condition",
this is not the case for [12] which you reference here. Please make clear
to which notion your GTC in [12] corresponds. If possible, a rough summary
on the needed changes in order to incorporate a binder would be very
helpful to readers which are unfamiliar with the field.

- p10, l389:
"CT-lambda is a decidable subset of Reg [20]": This sounds weird
since it seems like CT-lambda was already used in [20] which of course
does not make sense. I assume you mean decidability of the sufficient
condition for termination as stated on the next page. Please reformultate.

- p11, Remark 24:
This explanation (at least to me) makes little sense upon first reading.
I think it is still worthwile to note, but consider reformulation and add
the necessity of this in Figures 1 and 2 which makes your motivation immediately
clear.

- p11, l430:
I would drop the qualification "unique" trace because the trace can start at any
point according to your definition.

- p11, l432:
I like this description, I think it should already be given for Figure 1 at the
point where this is discussed. Also, I think your notation becomes clearer when
the double meaning of the blue arrows is removed by just leaving the black
back edges.

Typos/Reformulations:

p02 footnote 1: They can used -> They are / will be used
p03 l104: tree: let -> tree: Let
p04 l142: "if the type assignment presents" I understand what you mean,
          but I have never heard that phrase. Maybe reformulate?
p08 l276: describe a case -> describes a case
p08 l277: define connection -> define connections
p08 l281: and: there is -> and there is
p08 l292: for the rules: application, -> for the rules rules application, 
p08 l296: to upper B_k -> to the upper B_k
p09 l317: k-unnamed -> k-th unnamed
p09 l341: cond,S,0: the -> cond,S,0: The
p09 l353: k-unnamed -> k-th unnamed
p09 l353 (k+1)-unnamed -> k+1-th unnamed
p10 l373: indexes -> indices
p10 l373: \Pi -> Graph(\Pi)
p10 l378: which implies are -> which implies a
p10 l380: pre-proof \Pi that the term t is well-typed ->
          pre-proof \Pi witnessing the well-typedness of a term t
p10 l389: that satisfies -> that satisfy
p11 l420: Example 14 was -> Example 14 is
p11 l422: consists of -> consisting of
p11 l424: infinite many -> infinitely many
p11 l438: in the figure 2 -> in Figure 2
p13 l489: >= n -> > n
p13 l501: infinite progressing -> infinitely progressing


###----------------------- REVIEW 3 ---------------------

----------- Overall evaluation -----------

SCORE: 1 (weak accept)

----- TEXT:

In the last few years several works have explored the design of cyclic proof systems corresponding to Gödel System T [12,13,9,11,10]. However, in all such systems the terms, which are non well-founded trees, are not presented in the form an infinitary lambda-calculus (as in [2,1,18]), as one would expect, but rather as combinators, where each combinator tracks one sequent calculus rule.

The reasons for this apparently unnatural choice are well-explained e.g. in [12, Sec. 8.4]: due to the non well-founded nature of the proof system, one has to be careful that the term assignment is sufficiently "continuous", that is, that it replaces infinite but well-defined entities with infinite but well-defined entities. Yet, this is not obvious if the terms are taken to be infinite lambda-terms, as this may lead to ill-defined terms like e.g. ...t(t(t0)). 

This paper proposes a term assignment for cyclic System T based on an infinitary lambda-calculus that is meant to solve this problem. 
The solution consists in restricting the setting to "left-finite" infinite derivations, that is, derivations in which all leftmost paths starting from any node are finite. 
The paper focuses then on the class CT-lambda of well-typed (hence left-finite), regular and progressing terms. The main result (Theorem 32) is that "safe" reduction for such terms is strongly normalizing. Here safe reductions are those that never reduce the second argument of a conditional operator, since such reductions are well-known to be non-terminating (take e.g. t=cond(0,lambda x.t(S(x)))). A second result is the definition of a notion of limit for an arbitrary reduction of a CT-lambda term: this is obtained by exploiting Theorem 32 and progressively constructing normal forms for safe reductions at growing nesting depths of contexts of the form C[]=cond(0,[]).

The paper is globally well-written and presents an approach that seems to solve an open problem in the literature on the subject (yet, I am not knowledgeable enough in the field to estimate how satisfying this solution can be for an expert). 

Probably the introduction could do more to motivate and explain the difficulties related to the definition of a lambda-term assignment for cyclic proofs.

Moreover, I think the authors should provide a clearer comparison with the cited literature on infinitary lambda-calculi [2,1,18]. In particular, is the notion of safe reduction new or is it related to other approaches in the literature?

The literature on cyclic proofs focuses a lot on complexity aspects as well as on the proof-theoretic strength of the considered systems. This work does not say much about it, so two natural questions are: what is the complexity of checking the left-finite condition on a regular term? Can the strong normalization argument be established in theories like ACA_0 (considered for example in [12])? 

 


####MINOR COMMENTS:

- lines 45-46: "reductions not in the second argument of any cold strongly normalizes" please cite a source.
- lines 54-57: I did not understand what you mean, please reformulate
- lines 91-93: could you define what you mean by a subtree? For example, given a term 
t= cond(0,lambda x.t), would cond(0,lambda x.cond(0,lambda x.t) be a subtree? But in this case a regular term need not have finitely many subtree I guess (since one can iterate my example) Should a sub-tree be actually a sub-tree that is also a sub-term?
- lines 172 - 173: it would help to give some intuitions here for the separation of the two rules
- lines 201-205: this example looks similar to the one at p. 55 of [12], which is indeed supposed to suggest the difficulty of designing a lambda-term notation for cyclic derivations. 
- On Section 2.3: please provide some informal motivation for the safety condition
- line 401: "judment" -> "judgement"
- I think Lemma 41 from the Appendix should be at least stated in section 6, in order to give an idea of how the notion of totality leads to the Main Theorem.
