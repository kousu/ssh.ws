
* [ ] Use git submodules to track paramikojs instead of just copying it in
* [ ] Fix paramikojs to be nodejs compatible. At the very least, python_shim.js and BigInteger.js access `navigator` and `window` without checking if it exists first. Also none of the modules use UMD headers.
