
* [ ] Use git submodules to track paramikojs instead of just copying it in
* [ ] Fix paramikojs to be nodejs compatible. At the very least, python_shim.js and BigInteger.js access `navigator` and `window` without checking if it exists first. Also none of the modules use UMD headers.
* [ ] Do some sort of buffering to reduce network traffic
* [ ] Check if we were loaded over ssl and warn if not
* [ ] Write a handler for the various interactions ssh requires, e.g. the host key not 
* [ ] Store data (e.g. known host keys and our private key) in cookies / indexeddb/something
* [ ] Package signatures? Is there any sane way to handle this when things are being downloaded over and over again , or do we need to rely on SSL?
