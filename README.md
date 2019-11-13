# golang-collections
Cheatsheet on what collection operations look like when using go (coming from a Scala/Vavr/JS perspective).

# Seq type operations

The following patterns work with slices.

    val start: Seq[Int] = Seq(0, 1, 2)
      .map(fn)
      .filter(fn)
      .flatMap(fn)
      .foldLeft(value, fn)
      .groupBy(fn)
      .toMap(fkey, fval)

## start.map(fn)

This operation can be performed in-place.

    mapped := make([]int, len(start))
    for _, v := range start {
      mapped = append(mapped, fn(v))
    }

## start.filter(fn)

    filtered := make([]int, 0, len(start))
    for _, v := range start {
      if fn(v) {
        filtered = append(filtered, v)
      }
    }

## start.flatMap(fn)

    flatMapped := make([]int, 0)
    for _, v := range start {
      flatMapped = append(flatMapped, fn(v)...)
    }

## start.foldLeft(value, fn)

    foldLefted := value
    for _, v := range start {
      foldLefted = fn(foldLefted, v)
    }

## start.groupBy(fn)

    grouped := make(map[int][]int)
    for _, v := range start {
      group := fn(v)
      coll, exists := grouped[group]
      if !exists {
        coll = make([]int, 1)
      }
      grouped[group] = append(coll, v)
    }

## start.toMap(fkey, fval)

    toMapped := make(map[int]int)
    for _, v := range start {
      toMapped[fkey(v)] = fval(v)
    }
