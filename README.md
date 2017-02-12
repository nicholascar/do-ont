# Decision-O
The Decision ontology

## Introduction
The Decision Ontology (DO) provides basic means for describing decision and decisionmaking. It is formalized in the Web 
Ontology Language (OWL) and can be accessed here. The current DO prototype is intended to be extended with additional 
features as the work on the decision format progresses.

## Ontology document
Turtle format: [decision.ttl](decision.ttl)  
RDF XML format: [decision.owl](decision.owl)  
HTML format: *coming*

## Use
### What it can be used for?
Some of the questions that can be answered using DO:
* What problem/question initiated the decision-making process? 
* What options are being considered? 
* What criteria are being used for respective options? 
* What requirements, recommendation or other possible norms are associated with proposed criteria? 
* What is involved in choosing the respective options? 
* What is the result of a decision-making process? 
* What is affected by a given norm/requirement? 
* What satisfies a criterion? 
* What does not satisfy a criterion? 
* What kind of exceptions are defined? 
* What options should be/must not be considered? 
* What are the recommended criteria? 
* What are the required criteria?

### Usage scenarios
In general, there are two main use scenarios for DO:
* archiving current or historical decision-making processes and their outputs (data-driven use)
* outlining decision-making scenarios (patterns, templates) in order to provide guidelines for the decision-makers 
 (normative use)
 
Combining these two approaches would enable confronting the normative descriptions with actual decision-making data and 
thus giving sophisticated means for analyzing archived decisions which could be particularly useful for validation 
purposes.

##### Data-driven use
Recording facts by using OWL individuals. DO provides a conceptual framework and semantic foundation for analyzing 
decision-making data. The OWL file can be filled with data that can be used in many ways.

##### Normative use
Modeling decision-making patterns by defining OWL classes containing an outline of a generic decision. This could be 
useful for representing knowledge derived from some legal regulations, requirements, industry standards or obtained 
from domain experts. What can be achieved here is a description of the domain decisions enabling new ways of sharing, 
understanding, reusing this knowledge (for example by users of common standards, clients seeking information etc.).

#### Decision-making process
A complex process that starts with a question and may result in indication of a an answer being solution to the initial problem. It is important to note that a decision-making is something substantially different than decision, which is an output of the process of deciding. Usually it can be represented by the following pattern:

1. Decision-making starts with a question.
2. The decider gathers and analyzes some information
3. The decider evaluates possible options.
4. One of the options may get recognized as the right/appropriate/best possible solution
to the initial question/problem or the decider may choose to restrain from choice. What
justifies this act could be an objective evaluation of clearly defined criteria but also an
intuition, emotion or other subjective factor.

In most cases stages 2-3 consist of many (concurrent or sequential) actions, events, processes related to information 
gathering, processing, verifying etc. In some cases a decision-making can be viewed as a complex process involving many 
“sub-decisions” preceding the recognition of the initial problem solution. In our current work we have focused on the 
basic elements of the above pattern (the question, gathering information, considering options, choosing solution). It 
should be considered to what extent the DO should support the modeling of correlated issues such as: information verification and retrieval etc.

#### Allowing different criteria for identity (or continuity) of the decision-making
Sometimes it may be hard to tell when one decision-making ends and the other begins. Even in the mentioned example: is 
it a single decision-making process or two distinct ones connected with each other by the same issue they both concern? 
The case could become even more complicated when dealing with subdecisions and decision-processes with changing 
participants. It seems appropriate to leave that issue open enabling the core decision ontology to be extended with 
modules containing various solutions of that particular problem. 

#### Decision as an outcome of decision-making process
There is a fundamental ontological difference between the process of deciding and its outcome - a decision. Moreover, 
allowing more elastic boundaries of decision-making (see above) can result in single decision-making having more than 
one decision as its outcome.

#### Allowing incomplete decision-making stages
In some cases it may be useful to record a decision-making stage even if it doesn’t have any decision as its outcome. 
For example a patient may be ordered some further tests which may last a couple of days in which some other crucial 
parameters of decision-making can change resulting in a new stage of the deciding process (the newly recognized facts 
may encourage to continue modelling with a new stage of decision-making).

#### Representing temporal context
This is a general methodological issue, that still implies many discussions. Some of these discussion involve well-
known ontology experts unable to find a reasonable consensus. The main problem is: how to represent the mutable 
entities or the change of their properties in an ontology? What I did in my example is using OWL individuals to 
represent the same person in different stages of the decision-making process. What would be needed in a real-life 
application is to add some property which could allow the unambiguous reference to a person (for example insurance 
number). This is necessary because during decision-making one would often ascribe different or even contradict 
attributes at different stages of the process. Additional benefit: using different instances to provide “snapshot” view 
of reality allows developing fine-grained view of the reality - consider an example from my scenario: the throat 
infection diagnosed at t1 is represented by different OWL individual than the same kind of infection diagnosed at t2 
(after the allergic reaction), which illustrates that the medical disorder has probably undergone some change and may 
require a different treatment. This approach is one of the possible choices and the users of DO will have to decide 
whether or not it satisfies their needs.

#### Scalability issues
The decision ontology should provide a foundation for modelling decision-making on different granularity level. Ideally,
the decision ontology would consist of basic decision ontology and a set of modular extensions enabling more detailed 
modelling for more advanced use scenarios. When possible the core classes should be general enough to enable using them 
in different ontological and methodological contexts (for example we should not make assumptions about the definition of
a “process” because existing ontologies use different definitions of a process). So in order to enable scalability and 
wide adoption we should try to avoid or at least minimize making ontological assumptions about concepts originated from 
other domains. It seems that the successful adoption of decision ontology will probably significantly rely on the 
capability to be used as basis for community-based extensions.

#### Future work
1. develop extensions of the core DO for modeling of:  
    a. information gathering, processing and verification  
    b. decision metrics  
    c. decision-making criteria
2. implementing a use case
3. develop detailed documentation.


## How-to
#### How do I describe a decision making event?
* Add a subclass of **Decision_making** class.
* Consider adding the question representing the problem initiating the given decision-making process. Use **is_initiated_by** property to indicate a subclass (or member) of the **Question** class.
* Add options by using **is_consideration_of** property to indicate a subclass (or member) of **Option** class. See below for a details on describing options and their associated criteria.
* Add additional questions that have to be answered during the decision-making process. Use **initiates** property to indicate a subclass (or member) of the **Question** class.
* Add the outcome of the given decision-making process (this step can be omitted when describing decision-making patterns on TBox level). Use **has_result** property to indicate decisions that may result from considered options of a given decision-making process or to indicate a member of a **Decision** class in the case of describing a concrete process.

#### How do I describe an Option?
* Describe what exactly does a given option represent. Use **involves_choosing** property to indicate appropriate class or individual.
* Add options criteria. Use **has_criterion** property to indicate appropriate requirement, recommendation or other subclass or member of **Normative_value** class.

#### How do I describe option criteria?
* Describe what given criterion applies to. Use **has_validity_for** property to indicate appropriate class or individual.
* Describe how a criterion can be satisfied (or not satisfied). Use **is_satisfied_by** and/or **is_violated_by** to indicate appropriate class or individual.

#### How do I describe a norm (requirement, recommendation, etc.) related to a decision making event?
* Indicate what kind of decision-making does a given norm apply to. Use **has_validity_for** to indicate appropriate subclass or member of **Decision_making** class. 
* Describe how a given decision-making type should be conducted (create a decision-making pattern). Use **is_satisfied_by** and/or **is_violated_by** to indicate appropriate subclass or member of **Decision_making** class.

#### How do I describe a decision?
* Add option which represents the chosen solution. Use **indicates** property to specify a subclass or member of **Option** class 
* Indicate decision making process which a given decision is result of. Use **is_result_of** property to indicate appropriate subclass or member of **Decision_making** class.


## Examples
This [OWL file](examples/decision_example_03.ttl) contains a simple example: a decision-making case of choosing the 
appropriate therapy for a patient.used to illustrate the data-driven scenario mentioned above. It covers the following 
scenario: 

STAGE 1.  
A patient is diagnosed with a bacterial throat infection. The doctor needs to decide what treatment would be most 
appropriate. In order to prescribe the right drug he/she has to know whether or not the patient has an allergy for the 
drugs being considered for prescription and some parameters to evaluate correct dosing rules. 

STAGE 2.  
Patient P1 returns with some symptoms of allergic reaction, which suggests that P1 has allergy for Penicillin. The 
doctor decides to prescribe the other antibiotic.

## References
*Coming...*

YouTube video: https://www.youtube.com/watch?v=dbpQodni7F4


## License
This ontology and all other content in this repository are licensed under the [Creative Commons Attribution 4.0 International (CC BY 4.0)](https://creativecommons.org/licenses/by/4.0/) (also [LICENSE](LICENSE)).


## Authors and Contact
**Piotr Nowara**   
Primary Author  
<piotrnowara@gmail.com>  

**Nicholas Car**  
Geoscience Australia  
<nicholas.car@ga.gov.au>
