# Links for further study of FLAME GPU (FGPU) Domain Specific Language (DSL)

Comments and edits very welcome by adding an Issue or Pull Request.

## 1. Eclipse Modelling  Framework (EMF) with Ecore metamodel

 Widely used together with Graphical Modelling Framework (GMF) and with Xtext for both text and graphical DSLs.

https://www.eclipse.org/modeling/transformation.php

https://www.eclipse.org/modeling/textual.php

https://en.m.wikipedia.org/wiki/Xtext

https://www.eclipse.org/Xtext/documentation/

Xtext can easily do far more complex DSLs than needed for CSXMs and automatically generates language tools with all mod cons (syntax hints etc) for text editing by non-programmers using plug-ins for Eclipse or IntelliJIDEA or web browser. Can generate code from model much more flexibly than XSLT.

Simple grammar including Agent function interfaces with names of input and output arguments similar to the existing XML schema should easily be able to track dependencies and generate list of layers instead of requiring user to explicitly list them in XML model. Feedback while editing models could assist modellers to design CSXMS with good layering.

## 2. PyEcore

There is a pure python implementation of the EMF Ecore metamodel which works with pure python textX corresponding to Xtext and can exchange models with Eclipse EMF via standard XMMI files.

https://modeling-languages.com/pyecore-python-eclipse-modeling-framework/

https://pyecore.readthedocs.io/en/latest/

https://github.com/pyecore/pyecore

Used with pygeppetto:

http://docs.geppetto.org/en/latest/

http://www.geppetto.org/

https://github.com/openworm/pygeppetto

### textX

https://textx.github.io/textX/latest/

https://github.com/aranega/textX (fork integrating textX with pyecore)

https://github.com/textX/textx-multi-metamodel-example

https://goto40.github.io/self-dsl/

https://github.com/goto40/self-dsl

@article{Dejanovic2017,
    author = {Dejanovi\'{c}, I. and Vaderna, R. and Milosavljevi\'{c}, G. and Vukovi\'{c}, \v{Z}.},
    doi = {10.1016/j.knosys.2016.10.023},
    issn = {0950-7051},
    journal = {Knowledge-Based Systems},
    keywords = {Domain-Specific Language; Meta-model; Model; Model-Driven software development; Parser; Python },
    note = {},
    pages = {1--4},
    title = {{TextX: A Python tool for Domain-Specific Languages implementation}},
    url = {http://www.sciencedirect.com/science/article/pii/S0950705116304178},
    volume = {115},
    year = {2017}
}

http://www.igordejanovic.net/2016/05/06/implementing-martin-fowler-state-machine-dsl-in-textx.html

I. Dejanovi´ c, G. Milosavljevi´ c, R. Vaderna, Arpeggio: A flexible PEG parser for python, Knowledge-172
Based Systems 95 (2016) 71 – 74. doi: http://dx.doi.org/10.1016/j.knosys.2015.12.004

http://www.sciencedirect.com/science/article/pii/S0950705115004761174

https://tomassetti.me/quick-domain-specific-languages-in-python-with-textx/

The repo for including textX in pyecore is out of sync with the main textX repo at the moment but they are cooperating and might be happy to help, especially if related to RAMP.

## 3. Interpreted model debugging possible?

Main relevance of being pure python is that it could be used interpratively for debugging model together with Numba below, as well as for code generation. But also perhaps some possibilities for working directly with graphical models in Eclipse via Jython instead of just by exchange of XMMI files? 

## 4. Sismic executable Statechart modeller in python

A very powerful statechart modeller is also available in python. It provides extensive testing and validation and works with a Behaviour Driven Development process that looks to me well suited to the sort of modelling that would be done with CSXMS.

https://modeling-languages.com/sismic-python-api-statechart-execution/

https://sismic.readthedocs.io/en/latest/

Mens, T., Decan, A. & Spanoudakis, N.I. A method for testing and validating executable statechart models. Softw Syst Model 18, 837–863 (2019). https://doi.org/10.1007/s10270-018-0676-3

https://en.m.wikipedia.org/wiki/Behavior-driven_development

https://en.m.wikipedia.org/wiki/Cucumber_(software)

https://github.com/cucumber/cucumber

https://cucumber.io/docs/installation/

https://behave.readthedocs.io/ semi-official python cucumber
 
## 5. Hierarchical Statecharts 

The state machine models in current XML schema are much simpler than full UML Statecharts as above. But of course a complex hierarchical Statechart can generate code for simpler table driven implementation.

The more complex hierarchy is easier for modellers to understand and validate. An article by Steve Kelly explaining this with a classic example of trivial DSL for simple State Machine by Martin Fowler is here:

### Playing with Fower's DSM

https://www.metacase.com/blogs/stevek/blogView?showComments=true&entry=3414834520 

## 6. Agent function file in Numba python

Numba looks to me capable of being adapted to define Agent function method implementations in python and compiling them JIT with llvmlite to parallelized CUDA code. This is not clear as the main orientation of Numba is to just speedup work that would normally be done using python numpy arrays by running parallelized code using them.

http://numba.pydata.org/numba-doc/latest/index.html

http://numba.pydata.org/

http://llvmlite.pydata.org/

See also rest of Numfocus etc ecosystems:

https://numfocus.org/sponsored-projects

https://numfocus.org/sponsored-projects/affiliated-projects


**Numba: A LLVM-based Python JIT Compiler**
Siu Kwan Lam, Antoine Pitrou, Stanley Seibert

```
LLVM-HPC2015, November 15 - 20 2015, Austin, TX, USA
ACM 978-1-4503-4005-2/15/11$15.00.
DOI: http://dx.doi.org/10.1145/2833157.2833162.

Unlike most JIT compilers for interpreted languages, Numba
does not perform tracing nor replace the interpreter.In-
stead, it relies on the user actively transforming the Python
functions that need compiling at runtime. In Python, this is
done by applying a decorator to the function. The decorator
replaces the original Python function with a special object
that just-in-time compiles the function when it is first called
with a new type signature. To relieve users from the bur-
den of explicit type annotation, Numba inspects the types
of the arguments and performs local type inference on the
function. As a result, the compiler can have accurate type
information for each value in the function without tracing
the execution. {s 2, pdf 2/6}

One novel feature of Numba is its support for target-
ing different hardware.It currently provides an NVIDIA
CUDA[5] back-end using the NVVM [^3] library, and an AMD
HSA[6] back-end is also available on APU by using HLC[^4].
Both NVVM and HLC are vendor-specific version of LLVM
with additional support for their hardware. Rather than at-
tempting to create a portable execution model supported by
all targets, Numba directly exposes the execution model of
each GPGPU architecture to Python. This allows the user
to tailor their code to the specific features and performance
characteristics of each architecture. Numba provides access
to platform specific operations, such as thread barriers and
atomic operations on GPGPU targets. {s 2, pdf 2/6}
```

The "jitclass" feature that suggests to me use for FGPU Agent functions should be feasible is unfortunately still not implemented for GPUs but already in progress, so joining with Numba developers to implement it could be viable. 

I assume it would  require significant work with llvmlite to actually be able to inject Agent functions from numba into FGPU and do not understand enough about C++, CUDA and LLVM to be confident about what is feasible.

But the result could be that modellers can define and debug CSXMS models in python without noticing that they are using a C++ templates SDK at all. That seems well worth studying closely.

If that doesn't work out I think items 1 to 5 should still be relevant for replacing the current XSLT code generation with a more user friendly DSL, even though it would then still have to be a DSL for code generation rather than one which could be interacted with pythonically.

Here is long excerpt from Numba docs re "jitclass" feature:

http://numba.pydata.org/numba-doc/latest/user/jitclass.html

## Compiling Python classes with @jitclass

{This looks closest to what's needed for FGPU when implemented for GPU.

Spec has lists of FGPU Agent variables and types.

Then @jitclass(spec) has FGPU function file contents defined in python instead of C.
}

Note

This is a early version of jitclass support. Not all compiling features are exposed or implemented, yet.

Numba supports code generation for classes via the numba.jitclass() decorator. A class can be marked for optimization using this decorator along with a specification of the types of each field. We call the resulting class object a jitclass. All methods of a jitclass are compiled into nopython functions. The data of a jitclass instance is allocated on the heap as a C-compatible structure so that any compiled functions can have direct access to the underlying data, bypassing the interpreter.

Basic usage
Here’s an example of a jitclass:

```
import numpy as np
from numba import jitclass          # import the decorator
from numba import int32, float32    # import the types

spec = [
    ('value', int32),               # a simple scalar field
    ('array', float32[:]),          # an array field
]

@jitclass(spec)
class Bag(object):
    def __init__(self, value):
        self.value = value
        self.array = np.zeros(value, dtype=np.float32)

    @property
    def size(self):
        return self.array.size

    def increment(self, val):
        for i in range(self.size):
            self.array[i] = val
        return self.array
```

(see full example at examples/jitclass.py from the source tree)

In the above example, a spec is provided as a list of 2-tuples. The tuples contain the name of the field and the Numba type of the field. Alternatively, user can use a dictionary (an OrderedDict preferably for stable field ordering), which maps field names to types.

The definition of the class requires at least a __init__ method for initializing each defined fields. Uninitialized fields contains garbage data. Methods and properties (getters and setters only) can be defined. They will be automatically compiled.

{...}

The following operations of jitclasses work in both the interpreter and Numba compiled functions:

- calling the jitclass class object to construct a new instance (e.g. mybag = Bag(123));

- read/write access to attributes and properties (e.g. mybag.value);

- calling methods (e.g. mybag.increment(3));

Using jitclasses in Numba compiled function is more efficient. Short methods can be inlined (at the discretion of LLVM inliner). Attributes access are simply reading from a C structure. Using jitclasses from the interpreter has the same overhead of calling any Numba compiled function from the interpreter. Arguments and return values must be unboxed or boxed between Python objects and native representation. Values encapsulated by a jitclass does not get boxed into Python object when the jitclass instance is handed to the interpreter. It is during attribute access to the field values that they are boxed.

Limitations

A jitclass class object is treated as a function (the constructor) inside a Numba compiled function.

isinstance() only works in the interpreter.

Manipulating jitclass instances in the interpreter is not optimized, yet.

Support for jitclasses are available on CPU only. (Note: Support for GPU devices is planned for a future release.)

The decorator: @jitclass
numba.experimental.jitclass(spec)
A decorator for creating a jitclass.

arguments:

spec:
Specifies the types of each field on this class. Must be a dictionary or a sequence. With a dictionary, use collections.OrderedDict for stable ordering. With a sequence, it must contain 2-tuples of (fieldname, fieldtype).

returns:

A callable that takes a class object, which will be compiled.

