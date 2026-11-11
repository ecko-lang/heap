# heap

A priority queue (min-heap) for [Ecko](https://ecko.sh), written in Ecko as an
immutable skew heap: push, pop, peek, heapify and top-k. Pure computation - no
capabilities.

## Install

```bash
ecko get github.com/ecko-lang/heap
```

```ecko
import heap
```

## Usage

```ecko
import heap

mut h = heap.new()
h = heap.push(h, 3, "deploy")
h = heap.push(h, 1, "test")
h = heap.push(h, 2, "build")
h = heap.push(h, 1, "lint")

print(heap.size(h))  # 4
print(heap.peek(h))  # [1, test]

while not heap.is_empty(h) {
    let (item, rest) = heap.pop(h)
    print(item)
    h = rest
}
# [1, test]
# [1, lint]
# [2, build]
# [3, deploy]

print(heap.top_k([9, 3, 7, 1, 5], 3))  # [1, 3, 5]
```

## API

| function | returns |
|---|---|
| `new()` | an empty heap |
| `push(h, priority, value)` | a new heap with the item added |
| `pop(h)` | `[[priority, value], new_heap]`, smallest priority first |
| `peek(h)` | `[priority, value]` of the smallest item, or `null` when empty |
| `size(h)` | the item count as an Int |
| `is_empty(h)` | `true` when the heap holds no items |
| `from_list(pairs)` | a heap built from a list of `[priority, value]` pairs |
| `top_k(items, k)` | the `k` smallest values of a plain list, ascending |

## Notes

### Errors

| kind | reason | when |
|---|---|---|
| `heap` | `empty` | `pop` on an empty heap |
| `bug` | `not_a_heap` | an argument passed as a heap did not come from `heap.new()` |
| `bug` | `bad_priority` | a priority is not an Int, Float, Decimal or String, or cannot be ordered against the heap's other priorities |
| `bug` | `bad_argument` | `from_list` got something other than a list of pairs; `top_k` got a negative or non-Int `k`, or items that cannot be ordered |

### Behaviour

- A heap is a value: every operation returns a new heap and none changes the
  one it was given. Its contents are an implementation detail; use the
  functions above rather than reading its fields.
- `push` and `pop` are O(log n) amortized; `size`, `is_empty` and `peek` are
  O(1). No operation recurses, so a heap of any shape and size is safe.
- Ints and Floats mix as priorities. Decimals and Strings each need a heap of
  their own.
- Items with equal priority come out in the order they were pushed.
- `top_k` sorts the list; it does not build a heap.

## Testing

```bash
ecko test
```

## License

[MIT](LICENSE)
