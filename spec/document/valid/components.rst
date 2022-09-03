Components
-----------

.. _auxiliary-novalues:

No live values in context: :math:`\novalues\tyctx`
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

* There must be no live values in :math:`\tyctx.\TCPARENT`.

* Every type in :math:`\tyctx.\TCVALUES` must be of the form
  :math:`\evaltype^\dagger`.

* For each instance in :math:`\tyctx.\TCINSTANCES`, every extern
  declaration which is not dead must have a descriptor which is not of
  the form :math:`\EEMDVALUE~\evaltype`.

* Then there are no live values in the context :math:`\tyctx`.

.. math::
  \frac{
    \begin{array}{@{}c@{}}
    \novalues\tyctx.\TCPARENT\\
    \forall i, \exists \evaltype, \tyctx.\TCVALUES[i] = \evaltype^\dagger\\
    \begin{aligned}\forall i, \exists \overline{\eexterndeclad_j},{}&\tyctx.\TCVALUES[i] = \eexterndeclad\\\land{}&{}\forall j, \neg \exists \evaltype, \eexterndeclad_j = \EEMDVALUE~\evaltype\\\end{aligned}\\
    \end{array}
  }{
    \novalues \tyctx
  }

:math:`\overline{\definition_i}`
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

* :math:`\definition_1` must have some type :math:`{\ecomponenttype}_1`
  in context :math:`\{ \TCPARENT~\tyctx \}`.

* For each :math:`i > 1`, :math:`\definition_i` must have some type
  :math:`{\ecomponenttype}_i` in the context produced by typechecking
  :math:`\definition_{i-1}`.

* There must be no live values in the final context.

* Then the component :math:`\overline{\definition_i}` has the type
  produced by finalizing :math:`\bigoplus_i {\ecomponenttype}_i`.

.. math::
  \frac{
    \begin{array}{@{}c@{}}
    \tyctx_0 = \{ \TCPARENT~\tyctx \}\\
    \forall i, \tyctx_{i-1} \vdash \definition_i : {\ecomponenttype}_i \dashv \tyctx_i\\
    \novalues\tyctx_n\\
    \end{array}
  }{
    \tyctx \vdash \overline{\definition_i}^n
    : \lcfinalize\bigoplus \overline{{\ecomponenttype}_i}\rcfinalize
  }

Core sort indices: :math:`\tyctx \vdash \coresortidx : \core:importdesc`
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~


Instantiate arguments: :math:`\tyctx \vdash \sortidx : \eexterndesc`.
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Core modules
............

* If the type :math:`\tyctx.\TCCORE.\CTCMODULES[i]` exists in the
  context and is a subtype of :math:`\ecoremoduletype`, then
  :math:`\{\SISORT~\SCORE~\CSMODULE, \SIIDX~i\}` is valid with respect
  to extern descriptor :math:`\EEMDCOREMODULE~\ecoremoduletype`.

.. math::
  \frac{
    \tyctx \vdash \tyctx.\TCCORE.\CTCMODULES[i] \subtypeof \ecoremoduletype
  }{
    \tyctx \vdash \{ \SISORT~\SCORE~\CSMODULE, \SIIDX~i \}
      : \EEMDCOREMODULE~\ecoremoduletype
  }

Functions
.........

* If the type :math:`\tyctx.\TCFUNCS[i]` exists in the context and is
  a subtype of :math:`\efunctype`, then :math:`\{\SISORT~\SFUNC,
  \SIIDX~i\}` is valid with respect to extern descriptor
  :math:`\EEMDFUNC~\efunctype`.

.. math::
  \frac{
    \tyctx \vdash \tyctx.\TCFUNCS[i] \subtypeof \efunctype
  }{
    \tyctx \vdash \{ \SISORT~\SFUNC, \SIIDX~i \}
      : \EEMDFUNC~\efunctype
  }

Values
......

* If the type :math:`\tyctx.\TCVALUES[i]` exists in the context and is
  a subtype of :math:`\evaltype`, then :math:`\{\SISORT~\SVALUE,
  \SIIDX~i\}` is valid with respect to extern descriptor
  :math:`\EEMDVALUE~\evaltype`.

.. math::
  \frac{
    \tyctx \vdash \tyctx.\TCVALUES[i] \subtypeof \evaltype
  }{
    \tyctx \vdash \{ \SISORT~\SVALUE, \SIIDX~i \}
      : \EEMDVALUE~\evaltype
  }

Types
.....

* If the type :math:`\tyctx.\TCTYPES[i]` exists in the context and is
  a subtype of :math:`\edeftype`, then :math:`\{\SISORT~\STYPE,
  \SIIDX~i\}` is valid with respect to extern descriptor
  :math:`\EEMDTYPE~\edeftype`.

.. math::
  \frac{
    \tyctx \vdash \tyctx.\TCTYPES \subtypeof \edeftype
  }{
    \tyctx \vdash \{ \SISORT~\STYPE, \SIIDX~i \}
      : \EEMDTYPE~\edeftype
  }

Instances
.........

* If the type :math:`\tyctx.\TCINSTANCES[i]` exists in the context and
  is a subtype of :math:`\einstancetype`, then
  :math:`\{\SISORT~\SINSTANCE, \SIIDX~i\}` is valid with respect to
  extern descriptor :math:`\EEMDINSTANCE~\einstancetype`.

.. math::
  \frac{
    \tyctx \vdash \tyctx.\TCVALUES[i] \subtypeof \evaltype
  }{
    \tyctx \vdash \{ \SISORT~\SVALUE, \SIIDX~i \}
      : \EEMDVALUE~\evaltype
  }

.. math::
  \frac{
    \tyctx \vdash \tyctx.\TCINSTANCES[i] \subtypeof \einstancetype
  }{
    \tyctx \vdash \{ \SISORT~\SINSTANCE, \SIIDX~i \}
      : \EEMDINSTANCE~\einstancetype
  }

Components
..........

* If the type :math:`\tyctx.\TCCOMPONENTS[i]` exists in the context
  and is a subtype of :math:`\ecomponenttype`, then
  :math:`\{\SISORT~\SCOMPONENT, \SIIDX~i\}` is valid with respect to
  extern descriptor :math:`\EEMDCOMPONENT~\ecomponenttype`.

.. math::
  \frac{
    \tyctx \vdash \tyctx.\TCVALUES[i] \subtypeof \evaltype
  }{
    \tyctx \vdash \{ \SISORT~\SVALUE, \SIIDX~i \}
      : \EEMDVALUE~\evaltype
  }

.. math::
  \frac{
    \tyctx \vdash tyctx.\TCCOMPONENTS[i] \subtypeof \ecomponenttype
  }{
    \tyctx \vdash \{ \SISORT~\SCOMPONENT, \SIIDX~i \}
      : \EEMDCOMPONENT~\ecomponenttype
  }

Start arguments :math:`\tyctx \vdash \overline{\valueidx_i} : \resulttype`
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Definitions
~~~~~~~~~~~

:math:`\DCOREMODULE~\core:module`
.................................

* The core module :math:`\core:module` must be valid (as per Core
  WebAssembly) with respect to the elaborated core module type
  :math:`\ecoremoduletype`.

* Then :math:`\DCOREMODULE~\core:module` is valid with respect to the
  empty component type, and sets :math:`\TCCORE.\CTCMODULES` in the
  context to the orginal :math:`\tyctx.\TCCORE.\CTCMODULES` followed
  by :math:`\ecoremoduletype`.

.. math::
  \frac{
    \vdash \core:module : \ecoremoduletype
  }{
    \begin{aligned}
    \tyctx \vdash{}&\DCOREMODULE~\core:module\\
    :{}&\forall \varnothing. \varnothing \to \exists \varnothing. \varnothing\\
    \dashv{}&\tyctx \oplus \{ \TCCORE.\CTCMODULES~\ecoremoduletype \}\\
    \end{aligned}
  }

:math:`\DCOREINSTANCE~\CIINSTANTIATE~\coremoduleidx~\overline{\coreinstantiatearg_i}`
.....................................................................................

* No two instantiate arguments may have identical :math:`\CIANAME` members.

* The type :math:`\tyctx.\TCCORE.\CTCMODULES[\coremoduleidx]` must
  exist in the context, and for each :math:`\coreimportdecl` in that type:

  + There must exist an instantiate argument whose :math:`\CIANAME`
    member matches its :math:`\core:IMODULE` member, such that:

    - If the argument's :math:`\CIAINSTANCE` member is
      :math:`\coreinstanceidx`, then the type
      :math:`\tyctx.\TCCORE.\CTCINSTANCES[\coreinstanceidx]` must
      exist in the context, and furthermore, must contain an export
      whose :math:`\core:ENAME` member matches the import declarations
      :math:`\core:INAME` member, and whose :math:`\core:EDESC` member
      is a subtype of the import declaration's :math:`\core:IDESC` member.

.. math::
  \frac{
    \begin{array}{@{}c@{}}
    \tyctx.\TCCORE.\CTCMODULES[\coremoduleidx] = \overline{\coreimportdecl_j} \to \overline{\ecoreinstancetype}\\
    \begin{aligned}
    \forall j, \exists i,&\coreinstantiatearg_i.\CIANAME = \coreimportdecl_j.\core:IMODULE\\
    \land{}& \tyctx.\TCCORE.\CTCINSTANCES[\coreinstantiatearg_i.\CIAINSTANCE] = \overline{\coreexportdecl_l}\\
    \land{}& {\begin{aligned}[t]
      \exists l,&\coreexportdecl_l.\core:ENAME = \coreimportdecl_j.\core:INAME\\
      \land{}&\coreexportdecl_l.\core:EDESC \subtypeof \coreimportdecl_j.\core:IDESC\\
    \end{aligned}}
    \end{aligned}\\
    \forall i,\forall i', \coreinstantiatearg_i.\CIANAME = \coreinstantiatearg_{i'}.\CIANAME \Rightarrow i = i'\\
    \end{array}
  }{
   \begin{aligned}
    \tyctx \vdash{}&\DCOREINSTANCE~\CIINSTANTIATE~\coremoduleidx~\overline{\coreinstantiatearg_i}\\
    :{}&\forall\varnothing.\varnothing \to \exists\varnothing.\varnothing\\
    \dashv{}&\tyctx \oplus \{ \TCCORE.\CTCINSTANCES~\ecoreinstancetype \}
    \end{aligned}
  }

:math:`\DCOREINSTANCE~\CIEXPORTS~\overline{\{\CENAME~\name_i, \CEDEF~\coresortidx_i \}}`
........................................................................................

* Each :math:`\name_i` must be distinct.

* Each :math:`\coresortidx_i` must be valid with respect to some
  :math:`\core:importdesc_i`.

* Then :math:`\DCOREINSTANCE~\CIEXPORTS~\overline{\{\CENAME~\name_i,
  \CEDEF~\coresortidx_i \}}` is valid with respect to the empty module
  type, and sets :math:`\TCCORE.\CTCINSTANCES` in the context to the
  original :math:`\TCCORE.\CTCINSTANCES` followed by
  :math:`\overline{\{ \CEDNAME~\name_i,
  \CEDDESC~\core:importdesc_i\}}`.

.. math::
  \frac{
    \begin{array}{@{}c@{}}
    \forall i, \tyctx \vdash \coresortidx_i : \core:importdesc_i\\
    \forall i j, \name_i = \name_j \Rightarrow i = j
    \end{array}
  }{
    \begin{aligned}
    \tyctx \vdash{}& \DCOREINSTANCE~\CIEXPORTS~\overline{\{\CENAME~\name_i, \CEDEF~\coresortidx_i \}}\\
    :{}& \forall\varnothing.\varnothing \to \exists\varnothing.\varnothing\\
    \dashv{}& \tyctx \oplus \{ \TCCORE.\CTCINSTANCES~\overline{\{ \CEDNAME~\name_i, \CEDDESC~\core:importdesc_i\}} \}\\
    \end{aligned}
  }

:math:`\DCORETYPE~\coredeftype`
...............................

* The type :math:`\coredeftype` must elaborate to some :math:`\ecoredeftype`.

* Then the definition :math:`\DCORETYPE~\coredeftype` is valid with
  respect to the empty module type, and sets :math:`\TCCORE.\CTCTYPES`
  in the context to the original :math:`\tyctx.\TCCORE.\CTCTYPES`
  followed by :math:`\ecoredeftype`.

.. math::
  \frac{
    \tyctx \vdash \coredeftype \leadsto \ecoredeftype
  }{
    \tyctx \vdash \DCORETYPE~\coredeftype
    : \forall\varnothing.\varnothing \to \exists\varnothing.\varnothing
    \dashv \tyctx \oplus \{ \TCCORE.\CTCTYPES~\ecoredeftype \}
  }

:math:`\DCOMPONENT~\component`
..............................

* It must be possible to split the context :math:`\tyctx` such that
  the component :math:`\component` is valid for some type
  :math:`\ecomponenttype` in the first portion of the context

* Then the definition :math:`\DCOMPONENT~\component` is valid with
  respect to the empty component type, and sets the context to the
  second portion of the aforementioned split of the context, further
  updated by setting :math:`\TCCOMPONENTS` to the original
  :math:`\tyctx_2.\TCCOMPONENTS` followed by :math:`\ecomponenttype`.

.. math::
  \frac{
    \begin{array}{@{}c@{}}
    \tyctx = \tyctx_1 \boxplus \tyctx_2\\
    \tyctx_1 \vdash \component : \ecomponenttype\\
    \end{array}
  }{
    \tyctx \vdash \component
    : \forall\varnothing.\varnothing \to \exists\varnothing.\varnothing
    \dashv \tyctx_2 \oplus \{ \TCCOMPONENTS~\ecomponenttype \}
  }

:math:`\DINSTANCE~\IINSTANTIATE~\componentidx~\overline{\instantiatearg_i}`
...........................................................................

* The type :math:`\tyctx.\TCCOMPONENTS[\componentidx]` must exist in
  the context, and for each :math:`\eexterndecl` in that type:

  + There must exist an instantiate argument whose :math:`\IANAME`
    member matches its :math:`\EEDNAME` member and whose
    :math:`\IAARG` is valid with respect to its :math:`\EEDDESC`.

* Then
  :math:`\DINSTANCE~\IINSTANTIATE~\componentidx~\overline{\instantiatearg_i}`
  is valid with respect to the empty module type, and sets
  :math:`\TCINSTANCES` in the context to the original
  :math:`\tyctx.\TCINSTANCES` followed by :math:`\einstancetype` of
  :math:`\tyctx.\TCCOMPONENTS[\componentidx]`, and marks as dead in the
  context any values present in :math:`\overline{\instantiatearg_i}`.

.. math::
  \frac{
    \begin{array}{@{}c@{}}
    \tyctx.\TCCOMPONENTS[\componentidx] = \forall\overline{\boundedtyvar_j}.\overline{{\eexterndecl}_k} \to \einstancetype\\
    \forall j, \exists {\edeftype}_j, {\edeftype}_j \subtypeof \boundedtyvar_j\\
    \overline{\eexterndecl'}_k\to\einstancetype' = (\overline{{\eexterndecl}_k} \to \einstancetype)[\overline{{\edeftype}_j/\boundedtyvar_j}]\\
    \begin{aligned}
    \forall k, \exists i, &\instantiatearg_i.\IANAME = {\eexterndecl'}_k.\EEDNAME\\\land{}&\tyctx \vdash \instantiatearg_i.\IAARG : {\eexterndecl'}_k.\EEDDESC
    \end{aligned}\\
    \forall l, \evaltypead_l = \begin{cases}
       \tyctx.\TCVALUES[l]^\dagger&\text{if }\begin{aligned}\exists i,{}&\instantiatearg_i.\IAARG.\SISORT = \SVALUE\\\land{}&\instantiatearg_i.\IAARG.\SIIDX = k\\\end{aligned}\\
       \tyctx.\TCVALUES[l]&\text{otherwise}\\
    \end{cases}\\
    \forall m, {\einstancetypead}_m = \begin{cases}
      \einstancetype'&\text{if }m = \norm{\tyctx.\TCINSTANCES}\\
      \exists\boundedtyvar^\ast.\overline{\eexterndecl^\dagger}_n &\text{if }
        \begin{aligned}
          \exists i,{}&\instantiatearg_i.\IAARG.\SISORT = \SCOMPONENT\\
          \land{}&\instantiatearg_i.\IAARG.\SIIDX = m\\
          \land{}&\tyctx.\TCINSTANCES[m] = \exists\boundedtyvar^\ast. \overline{\eexterndeclad_n}\\
        \end{aligned}\\
      \tyctx.\TCINSTANCES[m] & \text{otherwise}\\
    \end{cases}
    \end{array}
  }{
    \begin{aligned}
    \tyctx \vdash{}&\DINSTANCE~\IINSTANTIATE~\componentidx~\overline{\instantiatearg_i}\\
    :{}&\forall\varnothing.\varnothing \to \exists\varnothing.\varnothing\\
    \dashv{}&\tyctx' \ominus \{ \TCVALUES, \TCINSTANCES \} \oplus \{ \TCINSTANCES~\overline{\einstancetypead}_m, \TCVALUES~\overline{\evaltypead_l} \}\\
    \end{aligned}
  }

:math:`\DINSTANCE~\IEXPORTS~\overline{\{ \ENAME~\name_i, \EDEF~\sortidx_i \}}`
..............................................................................

* Each :math:`\name_i` must be distinct.

* Each :math:`\sortidx_i` must be valid with respect to some
  :math:`{\eexterndesc}_i`.

* Then :math:`\DINSTANCE~\IEXPORTS~\overline{\{ \ENAME~\name_i,
  \EDEF~\sortidx_i \}}` is valid with respect to the empty module
  type, and sets :math:`\TCINSTANCES` in the context to the original
  :math:`\tyctx.\TCINSTANCES` followed by :math:`\lifinalize
  \overline{\exists(\Gamma.\TCVARS). \EEDNAME~\name_i,
  \EEDDESC~{\eexterndesc}_i}\rifinalize`, and marks as dead in the
  context any values present in :math:`\overline{\sortidx_i}`.

* TODO: What is the right way to choose which type variables to put
  into the existential here?

.. math::
  \frac{
    \begin{array}{@{}c@{}}
      \forall i, \tyctx \vdash \sortidx_i : {\eexterndesc}_i\\
      \forall i j, \name_i = \name_j \Rightarrow i = j\\
    \forall j, \evaltypead_j = \begin{cases}
       \tyctx.\TCVALUES[j]^\dagger&\text{if }\begin{aligned}\exists i,{}&\sortidx_i.\SISORT = \SVALUE\\\land{}&\sortidx_i.\SIIDX = j\\\end{aligned}\\
       \tyctx.\TCVALUES[j]&\text{otherwise}\\
    \end{cases}\\
    \einstancetype = \lifinalize\exists(\Gamma.\TCVARS).\overline{ \EEDNAME~\name_i, \EEDDESC~{\eexterndesc}_i}\rifinalize\\
    \forall k, \einstancetypead_k = \begin{cases}
      \einstancetype&\text{if } k = \norm{\tyctx.\TCINSTANCES}\\
      \exists\boundedtyvar^\ast.\overline{{\eexterndecl^\dagger}_l}&\text{if }
        \begin{aligned}
          \exists i,{}&\sortidx_i.\SISORT = \SINSTANCE\\
          \land{}&\sortidx_i.\SIIDX = k\\
          \land{}&\tyctx.\TCINSTANCES[k] = \forall\boundedtyvar^\ast. \overline{\eexterndeclad_l}\\
        \end{aligned}\\
      \tyctx.\TCINSTANCES[k]&\text{otherwise}
    \end{cases}
    \end{array}
  }{
    \begin{aligned}
    \tyctx \vdash{}& \DINSTANCE~\IEXPORTS~\overline{\{ \ENAME~\name_i, \EDEF~\sortidx_i \}}\\
    :{}& \forall\varnothing.\varnothing \to \exists\varnothing.\varnothing\\
    \dashv{}& \tyctx\ominus\{\TCINSTANCES,\TCVALUES\} \oplus \{ \TCINSTANCES~\overline{\einstancetypead_k},\TCVALUES~\overline{\evaltypead_j} \}
    \end{aligned}
  }

:math:`\DALIAS~\{ \ASORT~\sort, \ATARGET~\ATEXPORT~\instanceidx~\name \}`
.........................................................................

* The type :math:`\tyctx.\TCINSTANCES[\instanceidx]` must exist in the
  context.

* Some extern descriptor with a matching :math:`\name` and some desc
  :math:`\desc` must exist within :math:`\tyctx.\TCINSTANCES[\instanceidx]`.

* Then :math:`\DALIAS~\{ \ASORT~\sort,
  \ATARGET~\ATEXPORT~\instanceidx~\name \}` is valid with respect to
  the empty component type, and sets :math:`\F{index\_space}(\sort)`
  to the original :math:\tyctx.\F{index\_space}(\sort)` followed by
  :math:`\desc`.

.. math::
  \frac{
    \begin{array}{@{}c@{}}
    \tyctx.\TCINSTANCES[\instanceidx] = \overline{{\eexterndeclad}_i}\\
    \exists i, {\eexterndeclad}_i.\EEDNAME = \name\\
    \forall j, {\eexterndeclad'}_j = \begin{cases}
      {\eexterndeclad}_j^\dagger&\text{if } \sort = \SVALUE \land j = i\\
      \forall\boundedtyvar^\ast.\overline{{\eexterndecl}_k^\dagger}&
        \begin{aligned}
          \text{if }&\sort = \SINSTANCE \land j = i\\
          \land{}&\eexterndeclad = \forall\boundedtyvar^\ast.\overline{\eexterndeclad_k}\\
        \end{aligned}\\
      {\eexterndeclad}_j&\text{otherwise}\\
    \end{cases}\\
    \end{array}
  }{
   \begin{aligned}
    \tyctx \vdash{}& \DALIAS~\{ \ASORT~\sort, \ATARGET~\ATEXPORT~\instanceidx~\name \}\\
    :{}& \forall\varnothing.\varnothing \to \exists\varnothing.\varnothing\\
    \dashv{}& \tyctx \oplus \{ \F{index\_space}(\sort)~{\eexterndeclad}_i.\EEDDESC, \TCINSTANCES[i]~\overline{{\eexterndeclad'}_j} \}\\
    \end{aligned}
  }

:math:`\DALIAS~\{ \ASORT~\sort, \ATARGET~\ATCOREEXPORT~\coreinstanceidx~\name \}`
..................................................................................

* The type :math:`\tyctx.\TCCORE.\CTCINSTANCES[\coreinstanceidx]`
  must exist in the context.

* :math:`\sort` must be :math:`\SCORE~\coresort`.

* Some export declarator with a matching :math:`\name` and some desc
  :math:`\desc` must exist within
  :math:`\tyctx.\TCINSTANCES[\instanceidx]`.

* Then :math:`\DALIAS~\{ \ASORT~\sort,
  \ATARGET~\ATCOREEXPORT~\coreinstanceidx~\name \}` is valid with
  respect to the empty component type, and sets
  :math:`\F{index\_space}(sort)` to the original
  :math:`\tyctx.\F{index\_space}(\sort)` followed by :math:`\desc`.

.. math::
  \frac{
    \begin{array}{@{}c@{}}
    \sort = \SCORE~\coresort\\
    \tyctx.\TCCORE.\CTCINSTANCES[\coreinstanceidx] = \overline{\coreexportdecl_i}\\
    {\coreexportdecl}_i.\CEDNAME~\name\\
    \end{array}
  }{
    \begin{aligned}
    \tyctx \vdash{}& \DALIAS~\{ \ASORT~\sort, \ATARGET~\ATCOREEXPORT~\coreinstanceidx~\name \}\\
    :{}& \forall\varnothing.\varnothing \to \exists\varnothing.\varnothing\\
    \dashv{}& \tyctx \oplus \{ \F{index\_space}(\sort)~{\coreexportdecl}_i.\CEDDESC \}
    \end{aligned}
  }

:math:`\DALIAS~\{ \ASORT~\sort, \ATARGET~\ATOUTER~\u32_o~\u32_i \}`
...................................................................

* :math:`\sort` must be one of :math:`\SCOMPONENT`,
  :math:`\SCORE~\CSMODULE`\, :math:`\STYPE`, or
  :math:`\SCORE~\CSTYPE`.

* :math:`\tyctx.\TCPARENT[\u32_o].\F{index\_space}(\sort)[\u32_i]` must
  exist in the context.

* Then :math:`\DALIAS~\{ \ASORT~\sort, \ATARGET~\ATOUTER~\u32_o~\u32_i
  \}` is valid with respect to the empty component type, and sets
  :math:`\F{index\_space}(\sort)` in the context to the original
  :math:`\tyctx.\F{index\_space}(\sort)` followed by
  :math:`\tyctx.\TCPARENT[\u32_o].\F{index\_space}(\sort)[\u32_i]`.

.. math::
  \frac{
    \sort \in \{ \SCOMPONENT, \SCORE~\CSMODULE, \STYPE, \SCORE~\CSTYPE \}
  }{
    \begin{aligned}
    \tyctx \vdash{}& \DALIAS~\{ \ASORT~\sort, \ATARGET~\ATOUTER~\u32_o~\u32_i \}\\
    :{}&\forall\varnothing.\varnothing \to \exists\varnothing.\varnothing\\
    \dashv{}&\tyctx \oplus \{ \F{index\_space}(\sort)~\tyctx.\TCPARENT[\u32_o].\F{index\_space}(sort)[\u32_i] \}\\
    \end{aligned}
  }

:math:`\DTYPE~\deftype`
.......................

* The type :math:`\deftype` must elaborate to some :math:`\edeftype`.

* Then :math:`\DTYPE~\deftype` is valid with respect to the empty
  component type, and sets :math:`\TCTYPES` in the context to the
  original :math:`\tyctx.\TCTYPES` followed by :math:`\edeftype`.

.. math::
  \frac{
    \begin{array}{@{}c@{}}
    \tyctx \vdash \deftype \leadsto \edeftype\\
    \F{fresh}(\tyvar)\\
    \end{array}
  }{
    \begin{aligned}
    \tyctx \vdash{}&\DTYPE~\deftype\\
    :{}&\forall\varnothing.\varnothing \to \exists(\tyvar :\TBEQ~\edeftype).\varnothing\\
    \dashv{}&\tyctx \oplus \{ \TCVARS~(\tyvar :\TBEQ~\edeftype), \TCTYPES~\tyvar \}\\
    \end{aligned}
  }

:math:`\DCANON~\CLIFT~\core:funcidx~\overline{\canonopt_i}~\typeidx`
.......................................................................

* :math:`\tyctx.\TCTYPES[\typeidx]` must exist and be a
  :math:`\efunctype`.

* :math:`\F{canon\_lower\_type}(\efunctype, \overline{\canonopt_i})` must
  be equal to :math:`\tyctx.\TCCORE.\CTCFUNCS[\core:funcidx]`.

* Then
  :math:`\DCANON~\CLIFT~\core:funcidx~\overline{\canonopt_i}~\typeidx`
  is valid with respect to the empty component type, and sets
  :math:`\TCFUNCS` in the context to the original
  :math:`\tyctx.\TCFUNCS` followed by :math:`\efunctype`.

.. math::
  \frac{
    \begin{array}{@{}c@{}}
    \tyctx.\TCTYPES[\typeidx] = \efunctype\\
    \tyctx.\TCCORE.\CTCFUNCS[\core:funcidx] = \F{canon\_lower\_type}(\efunctype, \overline{\canonopt_i})\\
    \end{array}
  }{
    \tyctx \vdash \DCANON~\CLIFT~\core:funcidx~\overline{\canonopt_i}~\typeidx
    : \varnothing \to \varnothing
    \dashv \tyctx \oplus \{ \TCFUNCS~\efunctype \}
  }

:math:`\DCANON~\CLOWER~\funcidx~\overline{\canonopt_i}`
........................................................

* The type :math:`\tyctx.\TCFUNCS[\funcidx]` must exist in the context.

* :math:`\F{canon\_lower\_type}(\tyctx.\TCFUNCS[\funcidx],
  \overline{\canonopt_i})` must be defined (to be some
  :math:`\core:functype`.

* Then :math:`\DCANON~\CLOWER~\funcidx~\overline{\canonopt_i}` is
  valid with respect to the empty component type, and sets
  :math:`\TCCORE.\CTCFUNCS` in the context to the original
  :math:`\tyctx.\TCCORE.\CTCFUNCS` followed by that
  :math:`\core:functype`.

.. math::
  \frac{
  }{
    \begin{aligned}
    \tyctx \vdash{}&\DCANON~\CLOWER~\funcidx~\overline{\canonopt_i}\\
    :{}&\forall\varnothing.\varnothing \to \exists\varnothing.\varnothing\\
    \dashv:{}&\tyctx \oplus \{ \tyctx.\TCCORE.\CTCFUNCS~\F{canon\_lower\_type}(\tyctx.\TCFUNCS[\funcidx], \overline{\canonopt_i}) \}\\
    \end{aligned}
  }

:math:`\DSTART~\{ \FFUNC~\funcidx, \FARGS~\overline{\valueidx_i} \}`
....................................................................

* The type :math:`\tyctx.\TCFUNCS[\funcidx]` must be defined in the context.

* The arguments :math:`\overline{\valueidx_i}` must be valid with
  respect to the parameter list of the function.

* Then :math:`\DSTART~\{ \FFUNC~\funcidx,
  \FARGS~\overline{\valueidx_i} \}` is valid wiht respecte to the
  empty component type, and sets :math:`\TCVALUES` in the context to
  the original :math:`\tyctx.\TCVALUES` followed by the types of the
  return values of the function.

.. math::
  \frac{
    \begin{array}{@{}c@{}}
    \tyctx.\TCFUNCS[\funcidx] = \eresulttype \to \eresulttype'\\
    \tyctx \vdash \overline{\valueidx_i} : \eresulttype\\
    n = \F{length}(\tyctx.\TCVALUES)\\
    \forall j, \evaltypead'_j = \begin{cases}
      \tyctx.\TCVALUES[j]^\dagger&\text{if }j < n \land j \in \overline{\valueidx_i}\\
      \tyctx.\TCVALUES[j]&\text{if }j <n\land j \notin \overline{\valueidx_i}\\
      {\eresulttype}'_{j-n}&\text{otherwise}\\
    \end{cases}\\
    \end{array}
  }{
    \begin{aligned}
    \tyctx \vdash{}&\DSTART~\{ \FFUNC~\funcidx, \FARGS~\overline{\valueidx_i} \}\\
    :{}&\forall\varnothing.\varnothing \to \exists\varnothing.\varnothing\\
    \dashv{}&\tyctx \ominus \{ \TCVALUES \} \oplus \{ \TCVALUES~\overline{\evaltypead'_j} \}\\
    \end{aligned}
  }

:math:`\DIMPORT~\{ \IDNAME~\name, \IDDESC~\importdesc \}`
.........................................................

* The :math:`\importdesc` must elaborate to some :math:`\forall\boundedtyvar^\ast.\eexterndesc`.

* Then the definition :math:`\DIMPORT~\{ \IDNAME~\name,
  \IDDESC~\importdesc \}` is valid with respect to the component type
  whose export list is empty and whose import list is the singleton
  containing :math:`\{ \EEDNAME~\name, \EEDDESC~\eexterndesc \}`, and
  updates the context with :math:`\EEDDESC`.

.. math::
  \frac{
    \tyctx \vdash \importdesc \leadsto \forall\boundedtyvar^\ast.\eexterndesc
  }{
    \begin{aligned}
    \tyctx \vdash{}&\DIMPORT~\{ \IDNAME~\name, \IDDESC~\importdesc \}\\
    :{}&\forall\boundedtyvar^\ast.\{ \EEDNAME~\name, \EEDDESC~\eexterndesc \} \to \varnothing\\
    \dashv{}&\tyctx \oplus \{ \TCVARS~\boundedtyvar^\ast, \eexterndesc \}\\
    \end{aligned}
  }

:math:`\DEXPORT~\{ \ENAME~\name, \EDEF~\sortidx \}`
...................................................

* The :math:`\sortidx` must be valid with respect to some
  :math:`\eexterndesc`.

* Then the definition :math:`\DEXPORT~\{ \ENAME~\name, \EDEF~\sortidx
  \}` is valid with respect to the component type whose import list is
  empty and whose export list is the singleton containing :math:`\{
  \EEDNAME~\name, \EEDDESC~\eexterndesc \}`

.. math::
  \frac{
    \begin{array}{@{}c@{}}
    \tyctx \vdash \sortidx : \eexterndesc\\
    \forall j, \evaltypead'_j = \begin{cases}
      \tyctx.\TCVALUES[j]^\dagger&\text{if }\sortidx.\SISORT=\SVALUE\land \sortidx.\SIIDX = j\\
      \tyctx.\TCVALUES[j]&\text{otherwise}\\
    \end{cases}\\
    \forall k, \einstancetypead'_k = \begin{cases}
      \forall\boundedtyvar^\ast.\overline{{\eexterndecl^\dagger}_l}&
        \begin{aligned}
          \text{if }&\sortidx.\SISORT = \SCOMPONENT \land \sortidx.\SIIDX = j\\
          \land{}&\tyctx.\TCINSTANCES[j] = \forall\boundedtyvar^\ast.\overline{\eexterndeclad_l}\\
        \end{aligned}\\
      \tyctx.\TCINSTANCES[j]&\text{otherwise}\\
    \end{cases}\\
    \end{array}
  }{
    \begin{aligned}
    \tyctx \vdash{}&\DEXPORT~\{ \ENAME~\name, \EDEF~\sortidx \}\\
    :{}&\forall\varnothing.\varnothing \to \exists\varnothing.\{ \EEDNAME~\name, \EEDDESC~\eexterndesc \}\\
    \dashv{}&\tyctx \ominus \{ \TCVALUES, \TCINSTANCES \} \oplus \{ \TCVALUES~\overline{\evaltypead'_j}, \TCINSTANCES~\overline{\einstancetypead'_k} \}\\
    \end{aligned}
  }
 
