Reset to Radiotap Namespace
===========================

Bit Number  not applicable, bit 29 in *every* ``it_present`` word

Structure  no contents

Required Alignment  N/A

This field is reserved in **all namespaces and every** ``it_present`` **word**, the standard radiotap namespace as well as all vendor namespaces. It is mutually exclusive with the *Vendor Namespace* field, setting both is undefined.

Upon interpreting this field, the interpreter shall reset its presence-bitmap index to 0 and its namespace to the default radiotap namespace, and change to the default radiotap namespace, before it interprets subsequent presence-bitmap words.

