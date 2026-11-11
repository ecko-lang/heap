# Changelog

## 0.38.0

### Fixed

- `size` no longer fails with "recursion limit exceeded" on a large heap built
  from descending priorities. It is now O(1).
- Items with equal priority now always come out in the order they were pushed.
  Before, ties could come out in any order.
- Pushing a priority that cannot be ordered against the heap's others (an Int
  and a String, a Decimal and a Float, `null`) now fails at `push` with a
  `bug`/`bad_priority` error naming `heap.push`, instead of a bare comparison
  error.
- Passing something that is not a heap (`heap.is_empty([])`) now fails with
  `bug`/`not_a_heap` instead of answering wrongly or failing deep inside.
- `top_k` refuses a negative `k` and items that cannot be ordered with a
  `bug`/`bad_argument` error naming the function.

### Breaking

- A heap is no longer `null` or a bare node map; it is an opaque value from
  `heap.new()`. Migration: create heaps with `heap.new()` or
  `heap.from_list(...)` and test emptiness with `heap.is_empty(h)`, not
  `h == null`.
- `pop` on an empty heap throws kind `heap` (reason `empty`), not kind
  `value`. Migration: match `"heap"` where you matched `"value"`.
