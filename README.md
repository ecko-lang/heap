# Heap - Ecko Std Lib Package

A priority queue (min-heap) for [Ecko](https://ecko.sh), written in Ecko as an
immutable **skew heap**. Push/pop/peek, heapify, and top-k.

## Install

```bash
ecko get github.com/ecko-lang/heap
```

## Usage

```ecko
import heap

h = heap.new()
h = heap.push(h, 5, "task")     # (priority, value)
r = heap.pop(h)                 # [ [1, "..."], new_heap ]  - smallest first
heap.peek(h)                    # [priority, value] or null
heap.top_k([5, 1, 4, 2], 2)     # [1, 2]
```

## API

| Function | Description |
|---|---|
| `new()` | An empty heap |
| `push(h, priority, value)` | A new heap with the item added |
| `pop(h)` | `[ [priority, value], new_heap ]` - min first (raises kind-`"value"` if empty) |
| `peek(h)` | `[priority, value]` of the min, or `null` |
| `size(h)` · `is_empty(h)` | count / emptiness |
| `from_list(pairs)` | heapify a list of `[priority, value]` pairs |
| `top_k(items, k)` | the `k` smallest values of a plain list, ascending |

A heap is `null` (empty) or a node `{ p, v, l, r }`. Every operation returns a
new heap; `push`/`pop` are O(log n) amortized (no list copying).

## Testing

```bash
ecko test tests/
```

## License

MIT - see [LICENSE](LICENSE).
