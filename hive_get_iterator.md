**`std::hive::get_iterator` breaks Lakos rule**

Both overloads of `std::hive::get_iterator` are marked as `noexcept`
([hive.operations](https://wg21.link/hive.operations)) even though these functions have
preconditions, thus breaking Lakos rule. There is the related question of whether these
functions should have their preconditions hardened, but that discussion would be about
evolving the standard rather than fixing a defect in the normative text.

**Proposed resolution:**

Wording is relative to [N5032](https://wg21.link/n5032):

* [hive.overview] (synopsis):
```cpp
iterator get_iterator(const_pointer p)<del> noexcept</del>;
const_iterator get_iterator(const_pointer p) const<del> noexcept</del>;
```
* [hive.operations]:
```cpp
iterator get_iterator(const_pointer p)<del> noexcept</del>;
const_iterator get_iterator(const_pointer p) const<del> noexcept</del>;
```
