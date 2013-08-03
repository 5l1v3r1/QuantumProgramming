About this Repository
=====================

In the last couple days (starting on Jul 28, 2013) I have been experimenting with quantum programming concepts and trying to train myself to think like a quantum programmer. To test my ideas and validate my understanding, I have been writing small QCL programs. This is a collection of those programs and should serve primarily as a timeline of my development as a quantum programmer.

In addition, I have already created some functions which I believe would be worthy of a future "quantum standard library." I will document some of these functions in this *README*.

Some Useful Functions
=====================

`adder2.qcl` contains a function `AddReg(a, b, c)` for quantum addition. The variables `a`, `b`, and `c` must be equal in size. The function sums `a` and `b` and stores the result in `c`. It is assumed that `c` is <0| when passed in. Another useful function is `AddInPlace(a, b)` which adds `a` to `b` and stores the result in `a`. While this seems nice, the function still temporarily allocates a third register for computational purposes.

`doubleop.qcl` is ridiculously useful. The `DoubleV(a,b,c)` function applies a phase shift `a` to `b` if `c` = <11|. `DoubleNot(a,b)` flips `a` if `b` is `<11|`. `StringV` and `StringNot` act the same way, but the last argument can be any length. If the last argument is not all 1s, the operation will not be performed.

`equality.qcl` allows you to compare two quantum registers. The `NotIfEqual(a,b,c)` flips `a` if `b` is equal (bit-by-bit) to `c`. The `CNotIfEqual(a,b,c,d)` function is similar, but it only operates if all qubits in `d` are set to `<1|`.

`splitval.qcl` is something which I was only able to make once I had created the above libraries. Quite simply put, `SplitVal(r,a,b)` turns `r` into an equal entanglement of state `a` and state `b`. That is, splitting `<3|` and `<5|` would yield `0.5 <3| + 0.5 <5|`. 

License
=======

Why would you care about a license on code that nobody can even *use* yet? But seriously, check out the [GPL](http://www.gnu.org/licenses/gpl.html).
