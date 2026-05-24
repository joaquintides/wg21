**`std::hive::sort` should add _Cpp17MoveConstructible_ to its preconditions on `T`**

`std::hive::sort` ([hive.operations](https://wg21.link/hive.operations)) requires
that `T` be _Cpp17MoveInsertable_ into `hive`, _Cpp17MoveAssignable_, and _Cpp17Swappable_.
It does not require `T` to be _Cpp17MoveConstructible_, which is a prerequisite for the
internal use of `std::sort` by the implementation. Note that, in general,
_Cpp17MoveInsertable_ into `hive` (or any container) does not imply _Cpp17MoveConstructible_.
Both the de facto reference implementation for `std::hive` (Matthew Bentley's
[plf::hive](https://github.com/mattreecebentley/plf_hive)) and the ongoing[
implementation for VS](https://github.com/NylteJ/STL/tree/hive) use `std::sort`
directly on `T`.

Strictly speaking, the lack of this precondition can be salvaged by invoking `std::sort`
on a range of values of type `X`, where `X` is an ad-hoc type wrapping a `T` value and
an allocator object which implements move construction in terms of
`std::allocator_traits<A>::construct`. So, even if this issue is resolved as NAD, that
would be informative for standard library implementors so that they can potentially fix
their code.

**Proposed resolution:**

Wording is relative to [N5032](https://wg21.link/n5032):

* [hive.operations]/13:
_Preconditions_: `T` is _Cpp17MoveInsertable_ into `hive`, <ins>_Cpp17MoveConstructible_,</ins>
_Cpp17MoveAssignable_, and _Cpp17Swappable_.
